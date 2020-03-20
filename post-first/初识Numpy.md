---
title: 初识Numpy
date: 2019-09-28 09:19:02
thumbnail: https://i.loli.net/2019/09/28/yWpETVv56oARqdL.png
tags: Numpy
categories: Python
---
## Numpy简介

NumPy 是 Numerical Python 的简称，它是 Python 中的科学计算基本软件包。NumPy 为 Python 提供了大量数学库，使我们能够高效地进行数字计算。更多可点击[Numpy官网](http://www.numpy.org) 查看。

<!--more-->

关于Numpy需要知道的几点：

- NumPy 数组在创建时有固定的大小，不同于Python列表（可以动态增长）。更改ndarray的大小将创建一个新的数组并删除原始数据。

- NumPy 数组中的元素都需要具有相同的数据类型，因此在存储器中将具有相同的大小。数组的元素如果也是数组（可以是 Python 的原生 array，也可以是 ndarray）的情况下，则构成了多维数组。

- NumPy 数组便于对大量数据进行高级数学和其他类型的操作。通常，这样的操作比使用Python的内置序列可能更有效和更少的代码执行。

所以，Numpy 的核心是ndarray对象，这个对象封装了同质数据类型的n维数组。起名 ndarray 的原因就是因为是 n-dimension-array 的简写。接下来本节所有的课程都是围绕着ndarray来讲的，理论知识较少，代码量较多，所以大家在学习的时候，多自己动动手，尝试自己去运行一下代码。

## 创建ndarray

- 由python list创建

```python
# 1维数组
a = np.array([1, 2, 3])  
print(type(a), a.shape, a[0], a[1], a[2])

out:
<class 'numpy.ndarray'> (3,) 1 2 3

# 重新赋值
a[0] = 5                 
print(a)

out:
[5 2 3]

# 2维数组
b = np.array([[1,2,3],[4,5,6]])   
print(b)

out:
[[1 2 3]
 [4 5 6]]

print(b[0, 0], b[0, 1], b[1, 0])

out:
1 2 4
```

- 由numpy内置函数创建

```python
# 创建2x2的全0数组
a = np.zeros((2,2))  
print(a)

out:
[[ 0.  0.]
 [ 0.  0.]]

 # 创建1x2的全1数组
b = np.ones((1,2))  
print(b)

out:
[[ 1.  1.]]

# 创建2x2定值为7的数组
c = np.full((2,2), 7) 
print(c)

out:
[[7 7]
 [7 7]]

# 创建2x2的单位矩阵（对角元素为1）
d = np.eye(2)        
print(d)

out:
[[ 1.  0.]
 [ 0.  1.]]

#创建一个对角线为10,20,30,50的对角矩阵
d_1 = np.diag([10,20,30,50]) 
print(d_1)

out:
[[10 0 0 0]
 [ 0 20 0 0]
 [ 0 0 30 0]
 [ 0 0 0 50]]

#创建一个一维的0-14的数组
e = np.arange(15)   
print(e)

out:
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14]

#创建一个一维的4-9的数组
e_1 = np.arange(4,10)  
print(e_1)

out:
[4 5 6 7 8 9]

#创建一个一维的1-13且以间隔为3的数组
e_2 = np.arange(1,14,3)  
print(e_2)

out:
[ 1 4 7 10 13]

#创建一个一维的范围在0-10，长度为6的数组
f = np.linspace(0,10,6)  
print(f)

out:
#各个元素的间隔相等，为(10-0)/(6-1) = 2，若不想包含末尾的10，可以添加参数endpoint = False
[ 0.,  2.,  4.,  6.,  8., 10.]  

#把arange创建的一维数组转换为3行4列的二维数组
g = np.arange(12).reshape(3,4)  
print(g)                        

out:
#注意：使用reshape转换前后的数据量应该相同，12 = 3x4
[[ 0,  1,  2,  3],              
 [ 4,  5,  6,  7],
 [ 8,  9, 10, 11]]              

# 2x2的随机数组(矩阵),取值范围在[0.0,1.0)（包含0，不包含1）
h = np.random.random((2,2)) 
print(e)

out:
[[ 0.72776966  0.94164821]
 [ 0.04652655  0.2316599 ]]

#创建一个取值范围在[4,15)，2行2列的随机整数矩阵
i = np.random.randint(4,15,size = (2,2))  
print(i)

out:
[[6, 5],
 [5, 9]]

#创建一个从均值为0，标准差为0.1的正态分布中随机抽样的3x3矩阵
j = np.random.normal(0,0.1,size = (3,3))  
print(j)

out:
[[-0.20783767, -0.12406401, -0.11775284],
 [ 0.02037018,  0.02898423, -0.02548213],
 [-0.0149878 ,  0.05277648,  0.08332239]]
```

## 访问、删除、增加ndarray中的元素

这里主要是提供了一些访问、更改或增加ndarray中某一元素的基础方法。

### 访问&修改

类似于访问python list中元素的方式，按照元素的index进行访问或更改。

```python
#访问某一元素，这里可以自己多尝试
#访问一维数组的某一元素，中括号内填写index
print(np.arange(6)[3]) 
out:3

#访问二维数组的某一元素，中括号内填写[行,列]
print(np.arange(6).reshape(3,2)[1,1]) 
out:3

#访问三位数组中的某一元素，中括号内[组，行，列]
print(np.arange(12).reshape(2,3,2)[0,1,1]) 
out:3

#更改某一元素，用 = 进行赋值和替换即可
a = np.arange(6)
a[3] = 7      #先访问，再重新赋值
print(a)
[0 1 2 7 4 5]
```

### 删除

可使用np.delete(ndarray, elements, axis)函数进行删除操作。

这里需要注意的是axis这个参数，在2维数据中，axis = 0表示选择行，axis = 1表示选择列，但不能机械的认为0就表示行，1就表示列，注意前提**2维数据**中。

> 在三维数据中，axis = 0表示组，1表示行，2表示列。这是为什么呢？提示一下，三位数组的shape中组、行和列是怎样排序的？

所以，axis的赋值一定要考虑数组的shape。

```python
a = np.arange(12).reshape(2,2,3)
#思考下，这里删除axis = 0下的第0个，会是什么结果呢？自己试一下
print(np.delete(a,[0],axis = 0))  
```

再有一点需要注意的是，如果你想让原数据保留删除后的结果，需要重新赋值一下才可以。

```python
a = np.arange(6).reshape(2,3)
np.delete(a,[0],axis = 0)
print(a)

array([[0, 1, 2],
       [3, 4, 5]])  #原数据并未更改

a = np.delete(a,[0],axis = 0)  #重新赋值
print(a)

array([[3, 4, 5]])   #原数据已更改
```

### 增加

往ndarray中增加元素的办法跟python list也很类似，常用的有两种：

- 一种是添加（append），就是将新增的元素添加到ndarray的尾部

- 语法为：np.append(ndarray, elements, axis)

- 参数和delete函数一致，用法也一致，这里不再赘述

- 一种是插入（insert），可以让新增元素插入到指定位置

- 语法为：np.insert(ndarray, index, elements, axis)

- 参数中就多了一个index，指示的是插入新元素的位置。

这里值得注意的是，不论是append还是insert，在往多维数组中插入元素时，一定要注意对应axis上的shape要一致。再一个就是，和delete一样，如果你想要更改原数据，需要重新赋值。

## 切片和筛选

### ndarray切片

前面学了选择ndarray中的某个元素的方法，这里我们学习获取ndarray子集的方法——切片。

对于切片大家并不陌生，在list里面我们也接触过切片，一维的ndarray切片与list无异。需要注意的是，就是理解2维及多维ndarray切片。

- 2维矩阵切片

```python
a = np.arange(4*4).reshape(4,4)
print(a)

out:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])

a[:,:-1]

out:
array([[ 0,  1,  2],
       [ 4,  5,  6],
       [ 8,  9, 10],
       [12, 13, 14]])
```

这里可以看出，我们筛选了a矩阵中前三列的所有行，这是如何实现的呢？

切片的第一个元素:表示的是选择所有行，第二个元素:-1表示的是从第0列至最后一列（不包含），所以结果如上所示。

再看一个例子：

```python
a[1:3,:]

out:
array([[ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
```

筛选的是第2-3行的所有列。

- 一个常用的切片

以列的形式获取最后一列数据：

```python
a[:,3:]

out:
array([[ 3],
       [ 7],
       [11],
       [15]])
```

以一维数组的形式获取最后一列数据：

```python
a[:,-1]

out:
array([ 3,  7, 11, 15])
```

上面两种方法经常会用到，前者的shape为(4,1)，后者为(4,)。

### ndarray筛选

- 选择ndarray的对角线

所用函数为np.diag(ndarray, k=N)，其中参数k的取值决定了按照哪一条对角线选择数据。

默认k = 0，取主对角线；

k = 1时，取主对角线上面1行的元素；

k = -1时，取主对角线下面1行的元素。

**思考**：这个函数只能选择主对角线上的元素，那如果想要获取副对角线上的元素呢？

尝试自己搜索一下关键词numpy opposite diagonal寻找答案。

不建议你直接点getting the opposite diagonal of a numpy array。

- 提取ndarray中的唯一值

所用函数为np.unique(ndarray)，注意unique也可以添加参数axis来控制评判唯一值的轴方向，不好理解可以看示例：

```python
#查看二维数组a中的唯一值
a = [[0,1,2],
     [3,4,5],
     [0,1,2]]
print(np.unique(a))    
array([0, 1, 2, 3, 4, 5])

#查看a中的唯一行（也就是没有重复的行）
print(np.unique(a,axis = 0))  
array([[0, 1, 2],
       [3, 4, 5]])

#查看a中的唯一列
print(np.unique(a,axis = 1))  
array([[0, 1, 2],
       [3, 4, 5],
       [0, 1, 2]])

#查看a中第一行的唯一值
print(np.unique(a[0]))  
array([0, 1, 2])
```

- 通过布尔运算筛选

这里在中括号中添加筛选条件，当该条件的结果为True时（即满足条件时），返回该值。

```python
X[X > 10] #筛选数组X中大于10的数据
```

这里需要注意的是，当输入多个筛选条件时，&表示与，|表示或，~表示非。

## 运算与排序

### ndarray运算

- 集合运算

```python
np.intersect1d(x,y) #取x与y的交集
np.setdiff1d(x,y)   #取x与y的差集，返回的是在x中且没在y中的元素
np.union1d(x,y)     #取x与y的并集
```

- 算术运算
我们可以通过+、-、*、/或np.add、np.substract、np.multiply 、np.divide来对两个矩阵进行元素级的加减乘除运算，因为是元素级的运算，所以两个矩阵的shape必须要一致或者是可广播(Broadcast)。

这里所谓的可广播，就是指虽然A和B两个矩阵的shape不一致，但是A可以拆分为整数个与B具有相同shape的矩阵，这样在进行元素级别的运算时，就会先将A进行拆分，然后与B进行运算，结果再组合一起就可以。这里的A就是“可广播”矩阵。

> 上面涉及到的乘法是元素对应相乘，也就是点乘，那矩阵的叉乘呢？可以了解下numpy.matmul函数。

### ndarray排序

我们使用np.sort()和ndarray.sort()来对ndarray进行排序。

相同的是：

二者都可以使用参数axis来决定依照哪个轴进行排序，axis = 0时按照列排序，axis = 1时按照行排序；

不同的是：

np.sort()不会更改原数组；ndarray.sort()会更改原数组。
