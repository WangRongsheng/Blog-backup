---
title: '深度学习中的batch、epoch、iteration'
date: 2020-05-24 10:07:49
tags: [深度学习]
published: true
hideInList: false
feature: 
isTop: false
---

<!-- more -->
# 名词解释

|名词|定义|
|:-|:-|
|Epoch|使用训练集的全部数据对模型进行一次完整的训练，被称为“一代训练”|
|Batch|使用训练集中的一小部分样本对模型权重进行一次反向传播的参数更新，这一小部分样本被称为“一批数据”|
|Iteration|使用一个Batch数据对模型进行一次参数更新的过程，被称之为“一次训练”|

- （1）batchsize：批大小。在深度学习中，一般采用SGD训练，即每次训练在训练集中取batchsize个样本训练；

- （2）iteration：1个iteration等于使用batchsize个样本训练一次；

- （3）epoch：1个epoch等于使用训练集中的全部样本训练一次，通俗的讲epoch的值就是整个数据集被轮几次。

# 换算关系

<center><img src="https://s1.ax1x.com/2020/05/24/YzSM6S.png" alt="YzSM6S.png" border="0" /></center>

|梯度下降方式|Training Set Size|Batch Size|Number of Batches|
|:-|:-|:-|:-|
|BGD|N|N|1|
|SGD|N|1|N|
|Mini-Batch|N|B|N/B+1|

实际上，梯度下降的几种方式的根本区别就在于上面公式中的`Batch Size` 不同。

 > *注：上表中 Mini-Batch 的 Batch 个数为 N / B + 1 是针对未整除的情况。整除则是 N / B。

 # 示例

CIFAR10 数据集有 50000 张训练图片，10000 张测试图片。现在选择 Batch Size = 256 对模型进行训练。  

- 每个 Epoch 要训练的图片数量：50000
- 训练集具有的 Batch 个数：50000/256 = 195+1 =196
- 每个 Epoch 需要完成的 Batch 个数：196
- 每个 Epoch 具有的 Iteration 个数：196
- 每个 Epoch 中发生模型权重更新的次数：196
- 训练 10 代后，模型权重更新的次数：196*10=1960
- 不同代的训练，其实用的是同一个训练集的数据。第 1 代和第 10 代虽然用的都是训练集的五万张图片，但是对模型的权重更新值却是完全不同的。因为不同代的模型处于代价函数空间上的不同位置，模型的训练代越靠后，越接近谷底，其代价越小。
