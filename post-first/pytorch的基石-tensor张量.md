---
title: pytorch的基石-tensor张量
date: 2019-10-23 20:31:17
thumbnail: https://i.loli.net/2019/10/23/UjyvObKFH63rYBg.png
tags: pytorch张量
categories: AI
---
学习使用前准备：

[安装pytorch](http://pytorch.org)

[pytorch安装问题解决](https://zhuanlan.zhihu.com/p/56936691)

目前我的pytorch仍然存在使用问题...

<!--more-->

## 1.tensor数学

要介绍Tensor这个数据类型，我觉得有必要扯一下数学。

我们都知道：

标量（Scalar）是只有大小，没有方向的量，如1，2，3等

向量（Vector）是有大小和方向的量，其实就是一串数字，如(1,2)

矩阵（Matrix）是好几个向量拍成一排合并而成的一堆数字，如[1,2;3,4]

![如图，我们可以看出，矩阵是二维的，向量是一维的，标量是零维的。](https://i.loli.net/2019/10/23/P9ob7ESkndh2CmZ.png)

那么张量（Tensor）是什么呢？是按照三维排列的一堆数字？

是的。但是也不完全正确。

其实标量，向量，矩阵它们三个也是张量，标量是零维的张量，向量是一维的张量，矩阵是二维的张量。

![张量就是按照任意维排列的一堆数字的推广。如图所示，矩阵不过是三维张量下的一个二维切面。要找到三维张量下的一个标量，需要三个维度的坐标来定位。](https://i.loli.net/2019/10/23/kLCAUNwI4jdViGb.png)

除此之外，张量还可以是四维的、五维的等等

数学扯完了，我们撸串代码操练操练。

## 2.基础练习

```python
import torch #引用torch包
x = torch.Tensor(2,3)  #构造一个2x3的矩阵，没初始化但仍然会有值
print(x)

'''
8.0118e+28  4.5768e-41  8.0118e+28

4.5768e-41  2.9747e-37  1.4013e-45

[torch.FloatTensor of size 2x3]  #可以看出数据类型是浮点数的2x3矩阵
'''
```

看矩阵看不出张量的道道，我们来点刺激的

```python
y=torch.Tensor(4,2,3) #构造一个4x2x3的张量，没初始化
print(y)

'''
(0 ,.,.) =

1.00000e-29 *

0.0000  2.5244  0.0000

2.5244  0.0000  0.0000



(1 ,.,.) =

1.00000e-29 *

0.0000  0.0000  0.0000

0.0000  0.0000  0.0000



(2 ,.,.) =

1.00000e-29 *

0.0000  0.0000  0.0000

0.0000  0.0000  0.0000



(3 ,.,.) =

1.00000e-29 *

0.0000  0.0000  0.0000

2.5244  0.0000  2.5244

[torch.FloatTensor of size 4x2x3]
'''
```

我们从上面的返回值可以看出，4x2x3的张量y由4个2x3的矩阵构成，这符合了我们数学上的定义。

## 3.Tensor的加法(四种)

我们先初始化两个张量：

![](https://i.loli.net/2019/10/23/aKb2mHCZu3VgITl.png)

```python
第一种：

>>>a+b

第二种：

>>>torch.add(a,b)

第三种：

>>>result = torch.Tensor(5,3)

>>>torch.add(a,b,out=result) #把运算结果存储在result上

第四种：

>>>b.add_(a) #把运算结果覆盖掉b
```

## 4.Tensor的部分截取

![](https://i.loli.net/2019/10/23/5f3mkoFLcSiWOgt.png)

## 5.Tensor的其他操作

除了加法以外，还有上百种张量的操作，比如说转置（transposing），切片（slicing）等，送个[链接](https://pytorch.org/docs/stable/torch.html) 给少侠，少侠自己在家慢慢操练了🏇。

## 6.Tensor与numpy的Array的相互转换

torch的tensor可以与numpy的array进行转换

### （1）tensor⇒array

```python
>>>b = a.numpy() #a为tensor
```

![](https://i.loli.net/2019/10/23/RAFfxeu1wGcoMNP.png)

### （2）array⇒tensor

```python
>>>b = torch.from_numpy(a)  #a为numpy的array
```

![](https://i.loli.net/2019/10/23/GV7ltc4BhqrvyxW.png)

## 7.CUDA

假如少侠你有一块nvidia的显卡并支持cuda（如GTX 1080），那么恭喜你，你可以使用显卡gpu进行tensor的运算。假如你我一样没有，考虑买一个吧

购买指南：[为你的深度学习任务挑选最合适GPU:从性能到价格的全方位指南](http://www.sohu.com/a/106650024_157627)

```python
>>>torch.cuda.is_available()  #看看是否支持cuda
```

假如返回的是True那么，下面的代码将带你飞。

```python
>>>x = x.cuda()

>>>y = y.cuda()

>>>x+y           #这里的x和y都是tensor，使用cuda函数以后，x和y的所有运算均会调用gpu来运算。
```


