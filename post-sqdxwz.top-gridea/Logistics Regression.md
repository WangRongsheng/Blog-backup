# 逻辑回归概述

> 线性回归和逻辑回归区别？

在前面讲述的回归模型中，处理的因变量都是数值型区间变量，建立的模型描述是因变量的期望与自变量之间的线性关系。比如常见的线性回归模型： 

<center><img src="https://s1.ax1x.com/2020/07/24/UvqkPe.png" alt="UvqkPe.png" border="0" /></center>

而在采用回归模型分析实际问题中，所研究的变量往往不全是区间变量而是顺序变量或属性变量，比如二项分布问题。通过分析年龄、性别、体质指数、平均血压、疾病指数等指标，判断一个人是否换糖尿病，Y=0表示未患病，Y=1表示患病，这里的响应变量是一个两点（0-1）分布变量，它就不能用h函数连续的值来预测因变量Y（只能取0或1）。

总之，线性回归模型通常是处理因变量是连续变量的问题，如果因变量是定性变量，线性回归模型就不再适用了，需采用逻辑回归模型解决。

**逻辑回归（Logistic Regression）是用于处理因变量为分类变量的回归问题，常见的是二分类或二项分布问题，也可以处理多分类问题，它实际上是属于一种分类方法。**

# sigmoid 函数

相较于线性回归的因变量 y 为连续值，逻辑回归的因变量则是一个 0/1 的二分类值，这就需要我们建立一种映射将原先的实值转化为 0/1 值。这时候就要请出我们熟悉的 sigmoid 函数了：

<center><img src="https://s1.ax1x.com/2020/07/24/UvqfIO.png" alt="UvqfIO.png" border="0" /></center>

其函数图形如下：

<center><img src="https://s1.ax1x.com/2020/07/24/UvqvFS.jpg" alt="UvqvFS.jpg" border="0" /></center>

除了长的很优雅之外，sigmoid 函数还有一个很好的特性就是其求导计算等于下式，这给我们后续求交叉熵损失的梯度时提供了很大便利。

 <center><img src="https://s1.ax1x.com/2020/07/24/UvLkwV.png" alt="UvLkwV.png" border="0" /></center>

# 逻辑回归模型的数学推导

<center><img src="https://s1.ax1x.com/2020/07/24/UvL7hF.png" alt="UvL7hF.png" border="0" /></center>

# 代码实现

```python
# -*- coding: utf-8 -*-

##针对梯度上升求最大似然估计，可先设置大一点的步长与0.02， 求取一个初步的最优解， 然后设置小一点的步长，进一步求取精度更高的参数

import numpy as np
import time 
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

def load_data ():
     dataSet = load_breast_cancer()
     
     return dataSet.data, dataSet.target
     
     
def sigmoid (X):
     return 1.0 / (1.0 + np.exp(-X))

def LR_train (train_x, train_y, maxCycle, alpha):
     
     numSamples, numFeatures = np.shape(train_x)
     weights = np.ones((numFeatures, ))  
     
#     需要注意 np.ones((numFeatures, )) 和 np.ones((numFeatures, 1)) 的区别，虽然其数值是一样的，但是索引不同
#     此处选择第一种是为了与数据集中的形式匹配
     
     for i in range(maxCycle):
          
          #梯度下降，用到所有样本, 通过所有样本找到梯度，然后调整权重, 需要多次迭代才能收敛（实验为500次）
#          output =sigmoid(np.dot(train_x, weights))
#          err = train_y - output
#          weights = weights + alpha * np.dot(train_x.transpose(), err)
          
          # SGD  随机梯度下降，每次用单个样本计算梯度方向，此处为因此用到所有样本计算梯度，收敛快，迭代次数少（实验为10次）。因样本少，所以
          # 两者计算时间相差不大，当数据量大时，SGD理论收敛要快计算时长要少
          for i in range(numSamples):
               output =sigmoid(np.dot(train_x[i,:], weights))
               err = train_y[i,] - output
               weights = weights + alpha * np.dot(train_x[i,:].transpose(), err)   
          
     return weights


def LR_test (test_x, test_y, weights):
     numSamples, numFeatures = np.shape(test_x)
     count = 0
     for i in range(numSamples):   
          if sigmoid(np.dot(test_x[i,:], weights)) > 0.5:  
               predict = 1
          else: 
               predict = 0
          if predict == test_y[i,]:
                count = count + 1
     return float(count/numSamples)

if __name__ == "__main__":
     data, label = load_data()  
     startTime = time.time()       
     train_x, test_x , train_y, test_y=train_test_split(data, label,test_size=0.25, random_state=33)
        
     weights = LR_train (train_x, train_y, 10, 0.01) 

     accuracy = LR_test (test_x, test_y, weights)
     
     print("准确率："+ str(accuracy))
     print("计算时长：" +str(time.time() - startTime))
```

# 逻辑回归特点

## 优点

1. 实现简单，广泛的应用于工业问题上；
2. 训练速度较快。分类速度很快
3. 内存占用少；
4. 便利的观测样本概率分数，可解释性强；

## 缺点

1. 当特征空间很大时，逻辑回归的性能不是很好；
2. 一般准确度不太高
3. 很难处理数据不平衡的问题

# 参考

https://www.cnblogs.com/hum0ro/p/9652674.html

https://recomm.cnblogs.com/blogpost/9129493?page=1