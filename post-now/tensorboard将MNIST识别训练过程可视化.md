# 获取数据集

MNIST数据集官方网站：http://yann.lecun.com/exdb/mnist/

去把四个文件都下载下来，并放在名称为`MNIST_data` 的文件夹中：

- Training set images: train-images-idx3-ubyte.gz (9.9 MB, 解压后 47 MB, 包含 60,000 个样本)
- Training set labels: train-labels-idx1-ubyte.gz (29 KB, 解压后 60 KB, 包含 60,000 个标签)
- Test set images: t10k-images-idx3-ubyte.gz (1.6 MB, 解压后 7.8 MB, 包含 10,000 个样本)
- Test set labels: t10k-labels-idx1-ubyte.gz (5KB, 解压后 10 KB, 包含 10,000 个标签)

# 训练

> 可以进行超参数的修改！

```python
#coding:utf-8
from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
import tensorflow as tf

learning_rate = 0.001
train_epochs = 200
batch_size = 64
logs_path = 'tmp/logs'   #日志保存路径

n_input = 784
n_hidden1 = 100
n_hidden2 = 100
n_classes = 10

#name参数，记录变量名字
x = tf.placeholder(tf.float32, shape=[None, n_input], name='InputData')
y = tf.placeholder(tf.float32, shape=[None, n_classes], name='LabelData')
weights = {'w1': tf.Variable(tf.random_normal([n_input, n_hidden1]), name='W1'),
           'w2': tf.Variable(tf.random_normal([n_hidden1, n_hidden2]), name='W2'),
           'w3': tf.Variable(tf.random_normal([n_hidden2, n_classes]), name='W3')}
biases = {'b1': tf.Variable(tf.random_normal([n_hidden1]), name='b1'),
          'b2': tf.Variable(tf.random_normal([n_hidden2]), name='b2'),
          'b3': tf.Variable(tf.random_normal([n_classes]), name='b3')}

def inference(input_x):
    layer_1 = tf.nn.relu(tf.matmul(x, weights['w1']) + biases['b1'])
    tf.summary.histogram('layer_1', layer_1)   #记录变量直方图
    layer_2 = tf.nn.relu(tf.matmul(layer_1, weights['w2']) + biases['b2'])
    tf.summary.histogram('layer_2', layer_2)   #记录变量直方图
    out_layer = tf.matmul(layer_2, weights['w3']) + biases['b3']
    return out_layer

#定义计算过程的名字
with tf.name_scope('Inference'):
    logits = inference(x)
with tf.name_scope('Loss'):
    loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(logits=logits, labels=y))
with tf.name_scope('Optimizer'):
    optimizer = tf.train.AdamOptimizer(learning_rate=learning_rate)
    train_op = optimizer.minimize(loss)
with tf.name_scope('Accuracy'):
    pre_correct = tf.equal(tf.argmax(y, 1), tf.argmax(tf.nn.softmax(logits), 1))
    accuracy = tf.reduce_mean(tf.cast(pre_correct, tf.float32))

#记录张量的数据
tf.summary.scalar("Loss", loss)
tf.summary.scalar("Accuracy", accuracy)

init = tf.global_variables_initializer()
merged_summary_op = tf.summary.merge_all()   #定义记录运算

with tf.Session() as sess:
    sess.run(init)
    summary_writer = tf.summary.FileWriter(logs_path, graph=tf.get_default_graph())   #创建写对象
    total_batch = int(mnist.train.num_examples / batch_size)

    for epoch in range(train_epochs):
        for batch in range(total_batch):
            batch_x, batch_y = mnist.train.next_batch(batch_size)
            _, loss_, summary = sess.run([train_op, loss, merged_summary_op], feed_dict={x:batch_x, y:batch_y})   #执行记录运算
            summary_writer.add_summary(summary, epoch * total_batch + batch)     #将日志写入文件
        if epoch % 5 == 0:
            loss_, acc = sess.run([loss, accuracy], feed_dict={x:batch_x, y:batch_y})
            print("epoch {},  loss {:.4f}, acc {:.3f}".format(epoch, loss_, acc))

    print("optimizer finished!")

    #计算测试集的准确度
    test_acc = sess.run(accuracy, feed_dict={x:mnist.test.images, y:mnist.test.labels})
    print('test accuracy', test_acc)
```

# 可视化查看

在`tmp` 文件夹下写个`.bat` 文件，并且写入：

```html
tensorboard  --logdir path=你的文件位置
```

双击`.bat`文件 -> `http://localhost:6006/` 就可以看到了