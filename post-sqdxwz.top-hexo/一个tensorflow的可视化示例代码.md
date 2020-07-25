---
title: 一个tensorflow的可视化示例代码
date: 2019-10-07 11:37:20
thumbnail: https://i.loli.net/2019/10/07/qAMD3aBunm9oeZp.png
tags: 深度学习
categories: AI
---
TensorFlow主要优势是灵活和可视化。TensorBoard是TensorFlow的一组可视化工具。熟悉的使用TensorBoard可以大大提高训练的效率。今天本文将介绍一下TensorBoard。

<!--more-->

```python
import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data

#载入数据
mnist=input_data.read_data_sets('mnist_data',one_hot=True)#noe_hot把像素点都转变成0或1的形式


#每个批次的大小，训练模型时，一次放入一批次
batch_size=100 #一批次100张图
#计算一共有多少个批次
n_batch=mnist.train.num_examples//batch_size# //是整除,得到批次数

#参数概要
def variable_summaries(var):#定义一个函数，作用是计算各种参数值
    with tf.name_scope('summaries'):
        mean=tf.reduce_mean(var)#计算平均值
        tf.summary.scalar('mean',mean)#记录平均值，将其命名为mean。summary.scalar用来显示标量信息
        with tf.name_scope('stddev'):
            stddev=tf.sqrt(tf.reduce_mean(tf.square(var-mean)))
        tf.summary.scalar('stddev',stddev)# 标准差
        tf.summary.scalar('max',tf.reduce_max(var))#最大值
        tf.summary.scalar('min',tf.reduce_min(var))#最小值
        tf.summary.histogram('histogram',var)#直方图

#命名空间
with tf.name_scope('input'):  #命名随意，比如input,下面的x和y要缩进，表示x，y放在input空间
#定义两个placeholder，配合上面命名空间，给x，y取个名字
   x=tf.placeholder(tf.float32,[None,784],name='x-input')#建立一个占位符，None是图片数，784是每幅图的像素个数
   y=tf.placeholder(tf.float32,[None,10],name='y-input')# 标签，建立一个占位符，10是指0-9十个数

with tf.name_scope('layer'):
#创建一个简单的神经网络，输入层784个神经元，输出层10个神经元，不设隐藏层
   with tf.name_scope('wights'):
      W=tf.Variable(tf.zeros([784,10]),name='W')#权值，设一个变量，置0
      variable_summaries(W)#把权值W当作参数，计算的各种指标
   with tf.name_scope('biases'):
      b=tf.Variable(tf.zeros([10]),name='b')#偏置值
      variable_summaries(b)#把偏置值b当作参数，计算的各种指标
   with tf.name_scope('wx_plus_b'):
      wx_plus_b=tf.matmul(x,W)+b
   with tf.name_scope('softmax'):
      prediction=tf.nn.softmax(tf.matmul(x,W)+b)#信号总和，经过softmax函数（激活函数）转化成概率值

#二次代价函数
#loss =tf.reduce_mean(tf.square(y-prediction))

#使用交叉熵代价函数
with tf.name_scope('loss'):
    loss=tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(labels=y,logits=prediction))
    tf.summary.scalar('loss',loss)

#使用梯度下降法
with tf.name_scope('train'):
    train_step=tf.train.GradientDescentOptimizer(0.2).minimize(loss)

#初始化变量
init=tf.global_variables_initializer()

with tf.name_scope('accuracy'):
    with tf.name_scope('correct_prediction'):
#训练好后求准确率，结果存放在一个布尔型列表中，argmax返回一维张量中最大的值所在的位置
        correct_prediction=tf.equal(tf.argmax(y,1),tf.argmax(prediction,1))#argmax函数是对行或列计算最大值，1表示按行，0表示按列，找到最大概率标签的位置。 equal函数是比较两个参数大小，相等的话返回True，不相等返回False
    with tf.name_scope('accuracy'):
#求准确率
        accuracy=tf.reduce_mean(tf.cast(correct_prediction,tf.float32))#cast()是类型转换函数，把布尔型参数转换为32位古典型,然后求平均值。true变成1.0，flse变成0
#Boolean→数值型：True转换为-1，False转换为0。数值型→Boolean：0转换为False，其他转换为True
        tf.summary.scalar('accuracy',accuracy)

#合并所有的summary,并将其加入到sess.run的语句里
merged=tf.summary.merge_all()

with tf.Session() as sess:
    sess.run(init)#初始化变量
    writer=tf.summary.FileWriter('./graphs',sess.graph)#'logs/'是路径，graph存在logs文件夹中，如果没有logs文件夹，这里会自动生成
    for epoch in range(51):#迭代21个周期，把所有图片训练21次
        for batch in range(n_batch):
            batch_xs,batch_ys=mnist.train.next_batch(batch_size)#一次分配100张图片，图片数据保存在batch_xs，标签保存在batch_ys
            summary,_=sess.run([merged,train_step],feed_dict={x:batch_xs,y:batch_ys})#每tain训练一次，统计一次参数merged，运行后得到的merged存在summary里

        writer.add_summary(summary,epoch)#将summary和运行周期epoch写入tensorboard文件
        acc=sess.run(accuracy,feed_dict={x:mnist.test.images,y:mnist.test.labels})#x输入测试图片，从而得到prediciton的y，从而和label y 对比
        print('Iter'+str(epoch)+',Testing Accuracy'+str(acc))
```

