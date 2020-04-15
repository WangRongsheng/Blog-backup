# KNN算法概述

KNN可以说是最简单的分类算法之一，同时，它也是最常用的分类算法之一，注意KNN算法是**有监督学习**中的分类算法，它看起来和另一个机器学习算法K-means有点像（K-means是无监督学习算法），但却是有本质区别的。

# KNN算法介绍

KNN的全称是K Nearest Neighbors，意思是K个最近的邻居，从这个名字我们就能看出一些KNN算法的蛛丝马迹了。K个最近邻居，毫无疑问，K的取值肯定是至关重要的。那么最近的邻居又是怎么回事呢？其实啊，**KNN的原理就是当预测一个新的值x的时候，根据它距离最近的K个点是什么类别来判断x属于哪个类别** 。

<center><img src="https://s1.ax1x.com/2020/04/10/GI4rTA.png" alt="GI4rTA.png" border="0" /></center>

图中绿色的点就是我们要预测的那个点，假设K=3。那么KNN算法就会找到与它距离最近的三个点（这里用圆圈把它圈起来了），看看哪种类别多一些，比如这个例子中是蓝色三角形多一些，新来的绿色点就归类到蓝三角了。

<center><img src="https://s1.ax1x.com/2020/04/10/GI4cfP.png" alt="GI4cfP.png" border="0" /></center>

但是，**当K=5的时候，判定就变成不一样了** 。这次变成红圆多一些，所以新来的绿点被归类成红圆。从这个例子中，我们就能看得出K的取值是很重要的。

明白了大概原理后，我们就来说一说细节的东西吧，主要有两个，**K值的选取和点距离的计算** 。

## 距离计算

要度量空间中点距离的话，有许多几种度量方式，比如常见的曼哈顿距离计算，欧式距离计算等等。不过通常KNN算法中使用的是欧式距离，这里只是简单说一下，拿二维平面为例，**二维空间** 两个点的欧式距离计算公式如下：

<center><img src="https://s1.ax1x.com/2020/04/10/GI5e7d.png" alt="1011838 20181105210120839 1494903025" border="0"></center>

这个高中应该就有接触到的了，其实就是计算（x1,y1）和（x2,y2）的距离。拓展到多维空间，则公式变成这样：

<center><img src="https://s1.ax1x.com/2020/04/10/GI5nAA.png" alt="1011838 20181105210113366 1125611006" border="0"></center>

这样我们就明白了如何计算距离，KNN算法最简单粗暴的就是将预测点与所有点距离进行计算，然后保存并排序，选出前面K个值看看哪些类别比较多。但其实也可以通过一些数据结构来辅助，比如最大堆，这里就不多做介绍，有兴趣可以百度最大堆相关数据结构的知识。

> 各种度量方式：https://blog.csdn.net/m0_37075274/article/details/90273692

## K值选择

通过上面那张图我们知道K的取值比较重要，那么该如何确定K取多少值好呢？答案是通过交叉验证（将样本数据按照一定比例，拆分出训练用的数据和验证用的数据，比如6：4拆分出部分训练数据和验证数据），从选取一个较小的K值开始，不断增加K的值，然后计算验证集合的方差，最终找到一个比较合适的K值。

通过交叉验证计算方差后你大致会得到下面这样的图：

<center><img src="https://s1.ax1x.com/2020/04/10/GIISKS.png" alt="GIISKS.png" border="0" /></center>

这个图其实很好理解，当你增大k的时候，一般错误率会先降低，因为有周围更多的样本可以借鉴了，分类效果会变好。但注意，和K-means不一样，当K值更大的时候，错误率会更高。这也很好理解，比如说你一共就35个样本，当你K增大到30的时候，KNN基本上就没意义了。

所以选择K点的时候可以选择一个较大的临界K点，当它继续增大或减小的时候，错误率都会上升，比如图中的K=10。

# 代码实现

## python

```python
#引库
import numpy as np
import matplotlib.pyplot as plt
from math import sqrt
%matplotlib inline

#原始数据
data = [[1,0.9],[1,1],[0.1,0.2],[0,0.1]]
labels = ["A","A","B","B"]
test_data = [[0.1,0.3]]

#绘制原始数据散点图
print("===============================数据准备================================")
print("原始数据图像绘制...")
for i in range(len(data)):
    plt.scatter(data[i][0],data[i][1],color = "b")
plt.scatter(test_data[0][0],test_data[0][1],color='r')
plt.show()

#测试数据x=(0.1,0.3)
#采用欧式距离进行计算
print("===============================距离计算================================")
x = [[0.1,0.3]]

distance = []
labels_wz = []
for i in range(len(data)):
    d = 0
    d = sqrt((x[0][0]-data[i][0])**2 + (x[0][1]-data[i][1])**2)
    distance.append(d)
    labels_wz.append(i)
print("计算的距离为:\n",distance)
print("现在对应的标签位置为:\n",labels_wz)

#按照升序排序,并取距离较小的前3个
print("===============================距离排序================================")
for i in range(len(data)-1):
    for j in range(i+1,len(data)):
        if distance[i] > distance[j]:
            distance[i],distance[j] = distance[j],distance[i]
            labels_wz[i],labels_wz[j] = labels_wz[j],labels_wz[i]
print("排序后的距离为:\n",distance)
print("对应的标签的位置为:\n",labels_wz)
print("取距离最近的3个值:",distance[0:3])

#进行投票表决
print("===============================表决投票================================")
A = 0
B = 0
for i in range(len(labels_wz[0:3])):
    if labels[labels_wz[i]] == "A":
        A+=1
    else:
        B+=1
print("投票为A的数量为:",A)
print("投票为B的数量为:",B)
print("\n对照初始图中红色点(测试点)与前两个标签为A的离的最近,所以我们的计算与图中所呈现的结果一致!")
```

<center><img src="https://i.loli.net/2019/08/15/tfAl4XID2PbFZRG.png"></center>

## sklearn

```python
import numpy as np
import sklearn
from sklearn import datasets
from sklearn.neighbors import KNeighborsClassifier
X_train = np.array([[1,0.9],[1,1],[0.1,0.2],[0,0.1]])  #这里是数组形式哦，要注意哦，如果输入的dataframe（因为一般我们导入文件的话都是使用csv模式，导入进来一般是形成dataframe模式，我们需要在fit()函数中使用 X_train.values,y_train.values）

y_train=['A','A','B','B']
knn=KNeighborsClassifier(n_neighbors=1)
knn.fit(X_train,y_train)
knn.predict([[0.1,0.3]])#要注意，预测的时候也要上使用数组形式的
```

# KNN特点

## 优点

1）简单好用，容易理解，精度高，理论成熟，既可以用来做分类也可以用来做回归；

2）可用于数值型数据和离散型数据；

3）训练时间复杂度为O(n)；无数据输入假定；

4）对异常值不敏感。

## 缺点

1）计算复杂性高；空间复杂性高；

2）样本不平衡问题（即有些类别的样本数量很多，而其它样本的数量很少）；

3）一般数值很大的时候不用这个，计算量太大。但是单个样本又不能太少，否则容易发生误分；

4）最大的缺点是无法给出数据的内在含义。

至于什么时候应该选择使用KNN算法，sklearn的这张图给了我们一个答案：

<center><img src="https://i.loli.net/2020/04/10/T8wEisjyY31IhVK.png" ></a></center>

英文不懂？？看中文：

<center><img src="https://i.loli.net/2020/04/10/RjKcUsGzLip86Y2.png" ></a></center>

简单的说，当需要使用分类算法且数据比较大的时候就可以尝试使用KNN算法进行分类了。