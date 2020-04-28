> 本文只讲一元线性回归！

# 回归分析

回归分析是一种预测性的建模技术，它研究的是因变量（目标）和自变量（预测器）之间的关系。这种技术通常用于预测分析，时间序列模型以及发现变量之间的因果关系。通常使用曲线/线来拟合数据点，目标是**使曲线到数据点的距离差异最小** 。

# 线性回归概述

<center><img src="https://s1.ax1x.com/2020/04/25/JytjT1.png" alt="JytjT1.png" border="0" /></center>

线性回归是回归问题中的一种，线性回归假设目标值与特征之间线性相关，即满足一个多元一次方程。通过构建损失函数，来求解损失函数最小时的参数w和b。通长我们可以表达成如下公式：

<center><img src="https://s1.ax1x.com/2020/04/25/JytQd1.png" alt="JytQd1.png" border="0" /></center>

$\hat{y}$ 为预测值，自变量x和因变量y是已知的，而我们想实现的是预测新增一个x，其对应的y是多少。因此，为了构建这个函数关系，目标是通过已知数据点，求解线性模型中w和b两个参数。

# 线性回归算法步骤

1）给定数据集，进行初始输入。

2）获得目标/损失函数。

求解最佳参数，需要一个标准来对结果进行衡量，为此我们需要定量化一个目标函数式，使得计算机可以在求解过程中不断地优化。针对任何模型求解问题，都是最终都是可以得到一组预测值 $\hat{y}$  ，对比已有的真实值 y ，数据行数为 n ，可以将损失函数定义如下：

<center><img src="https://s1.ax1x.com/2020/04/25/JyULI1.png" alt="JyULI1.png" border="0" /></center>

即预测值与真实值之间的平均的平方距离，统计中一般称其为**MAE(mean square error)均方误差** 。把之前的函数式代入损失函数，并且将需要求解的参数w和b看做是函数L的自变量，可得：

<center><img src="https://s1.ax1x.com/2020/04/25/JyaMZj.png" alt="JyaMZj.png" border="0" /></center>

> 在统计中，除了MAE之外，还有：MSE、RMSE，具体可自行百度

现在的任务是求解最小化L时w和b的值，即核心目标优化式为：

<center><img src="https://s1.ax1x.com/2020/04/25/JyagyD.png" alt="JyagyD.png" border="0" /></center>

3）对损失函数进行求导，求解过程是使用最小二乘法(least square method)。

求解 w 和 b 是使损失函数最小化的过程，在统计中，称为线性回归模型的最小二乘“参数估计”(parameter estimation)。我们可以将 L(w,b) 分别对 w 和 b 求导，得到：

<center><img src="https://s1.ax1x.com/2020/04/25/JywF8P.png" alt="JywF8P.png" border="0" /></center>

令上述两式为0，可得到 w 和 b 最优解的闭式(closed-form)解：

<center><img src="https://s1.ax1x.com/2020/04/25/Jyw2ad.png" alt="Jyw2ad.png" border="0" /></center>

4）梯度下降，更新参数。

<center><img src="https://s1.ax1x.com/2020/04/25/Jyw7qg.png" alt="Jyw7qg.png" border="0" /></center>

## 梯度下降手工推导

<center><img src="https://i.loli.net/2019/08/12/whRuembzs69xDTK.jpg"></center>

# 代码实现

## python

```python
import numpy as np
from matplotlib import pylab as pl

# 定义训练数据
x = np.array([1,3,2,1,3])
y = np.array([14,24,18,17,27])

# 回归方程求取函数
def fit(x,y):
    if len(x) != len(y):
        return
    numerator = 0.0
    denominator = 0.0
    x_mean = np.mean(x)
    y_mean = np.mean(y)
    for i in range(len(x)):
        numerator += (x[i]-x_mean)*(y[i]-y_mean)
        denominator += np.square((x[i]-x_mean))
    print('numerator:',numerator,'denominator:',denominator)
    b0 = numerator/denominator
    b1 = y_mean - b0*x_mean
    return b0,b1

# 定义预测函数
def predit(x,b0,b1):
    return b0*x + b1

# 求取回归方程
b0,b1 = fit(x,y)
print('Line is:y = %2.0fx + %2.0f'%(b0,b1))

# 预测
x_test = np.array([0.5,1.5,2.5,3,4])
y_test = np.zeros((1,len(x_test)))
for i in range(len(x_test)):
    y_test[0][i] = predit(x_test[i],b0,b1)

# 绘制图像
xx = np.linspace(0, 5)
yy = b0*xx + b1
pl.plot(xx,yy,'k-')
pl.scatter(x,y,cmap=pl.cm.Paired)
pl.scatter(x_test,y_test[0],cmap=pl.cm.Paired)
pl.show()
```

## sklearn

```python
import numpy as np
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

x = [1,3,2,1,3]
x = np.reshape(x,newshape=(5,1))
y = [14,24,18,17,27]
y = np.reshape(y,newshape=(5,1))
# 调用模型
lr = LinearRegression()
# 训练模型
lr.fit(x,y)
# 计算R平方
print(lr.score(x,y))
# 计算y_hat
y_hat = lr.predict(x)
# 打印出图
plt.scatter(x,y)
plt.plot(x, y_hat)
plt.show()
```

# 线性回归特点

## 优点

（1）思想简单，实现容易。建模迅速，对于小数据量、简单的关系很有效。

（2）是许多强大的非线性模型的基础。

（3）线性回归模型十分容易理解，结果具有很好的可解释性，有利于决策分析。

（4）蕴含机器学习中的很多重要思想。

（5）能解决回归问题。

## 缺点
　　　　
（1）对于非线性数据或者数据特征间具有相关性多项式回归难以建模.

（2）难以很好地表达高度复杂的数据。

