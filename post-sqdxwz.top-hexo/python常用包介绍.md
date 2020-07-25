---
title: python常用包介绍
date: 2019-09-29 20:42:03
thumbnail: https://i.loli.net/2019/09/29/pc5xsTl6VaWof7B.png
tags: python常用包
categories: Python
---
# Python的常用包有哪些，分别有什么作用？

## Python常用包
1、Numpy（数值运算库）

2、Scipy（科学计算库）

<!--more-->

3、Matplotlib（基础可视化库）

4、Pandas（数据处理库）

5、Seaborn（高级可视化库）

6、Scikit-learn（流行的机器学习库）

## 各自作用
1、Numpy是最为流行的机器学习和数据科学包，Numpy包支持在多维数据上的数学运算，提供数据结构以及相应高效的处理函数，很多更高级的扩展库(包括Scipy、Matplotlib、Pandas等库）都依赖于Numpy库；

2、Scipy包用于科学计算，提供矩阵支持，以及矩阵相关的数值计算模块，其功能包含有最优化、线性代数、积分、插值、拟合、信号处理和图像处理以及其他科学工程中常用的计算；

3、Pandas用于管理数据集，强大、灵活的数据分析和探索工具，其带有丰富的数据处理函数，支持序列分析功能，支持灵活处理缺失数据等；

● Pandas基本的数据结构是Series和DataFrame；

● Series就是序列，类似一维数组；

● DataFrame相当于一张二维的表格，类似二维数组，它的每一列都是一个Series；

● 为了定位Series中的元素，Pandas提供了Index对象，每个Series都会带有一个对应的Index，用来标记不用的元素；

● DataFrame相当于多个带有同样Index的Series的组合（本质是Series的容器）；

4、Matplotlib库用于数据可视化，强大的数据可视化工具以及作图库，其主要用于二维绘图，也可以进行简单的三维绘图；

5、Seaborn库是基于Matplotlib的高级可视化库；

6、Sklearn库包含大量机器学习算法的实现，其提供了完善的机器学习工具箱，支持预处理、回归、分类、聚类、降维、预测和模型分析等强大的机器学习库，近乎一半的机器学习和数据科学项目使用该包。

# sklearn的常用包有哪些，分别有什么作用？

## sklearn库的结构

sklearn主要是用于机器学习，所以sklearn的模块也都是围绕机器学习算法的。sklearn因此可以分为这几个部分：Classification（分类），Regression（回归），Clustering（聚类），Dimensionality reduction（降维），Model selection（模型选择），Preprocessing（预处理）。

1.分类算法包括SVM（sklearn.svm.SVC等）、近邻（sklearn.neighbors）、随机森林（sklearn.ensemble.RandomForestClassifier）等。

2.回归算法包括SVR（sklearn.svm.SVR）、岭回归（sklearn.linear_model.Ridge）、Lasso（sklearn.linear_model.Lasso）等。

3.聚类算法包括K均值（sklearn.cluster.KMeans）、谱聚类（sklearn.cluster.SpectralClustering）等。

4.降维算法包括PCA（如sklearn.decomposition.PCA）、特征选择（sklearn.feature_selection，包括单变量特征选择等）、非负矩阵分解（如sklearn.decomposition.NMF、LatentDirichletAllocation）。

5.模型选择方法包括网格搜索（sklearn.model_selection.GridSearchCV）、交叉验证（有很多，比如sklearn.model_selection.KFold、cross_val_score）、评估指标（sklearn.model_selection.metrics，包括precision、recall、accuracy等）。

6.预处理方法包括基本的预处理方法（sklearn.preprocessing，包括标准化、类别化、离散化等）、特征抽取（sklearn.feature_extraction，包括文本特征抽取方法bag of words、tf-idf等）。

## 机器学习主要步骤中sklearn应用

1.数据集：sklearn.datasets中提供了很多数据集，初学时可将其作为基础数据。

2.数据预处理：sklearn.preprocessing，包括：降维、数据归一化、特征提取和特征转换（one-hot）等

3.选择模型并训练：分类、回归、聚类、集成等算法，涉及的模型主要是sklearn.linear_model、sklearn.cluster、sklearn.ensemble。

4.模型评分：sklearn.metrics，包括准确率、召回率等，算法自身也带有评分方法score。

5.模型的保存与恢复：可以用python的pickle方法（pickle.dump、pickle.load），或者sklearn.externals.joblib（joblib.dump、joblib.load）。

# 什么是正则化、如何理解正则化以及正则化的作用？

正则化-Regularization（也称为惩罚项或范数）就是通过对模型的参数在“数量”和“大小”方面做相应的调整，从而降低模型的复杂度，以达到避免过拟合的效果。

## 如何理解正则化

如果我们的目标仅仅是最小化损失函数（即经验风险最小化），那么模型的复杂度势必会影响到模型的整体性能；引入正则化（即结构风险最小化）可以理解为衡量模型的复杂度，同时结合经验风险最小化，进一步训练优化算法。

## 正则化的作用


正则化可以限制模型的复杂度，从而尽量避免过拟合的发生；模型之所以出现过拟合的主要原因是学习到了过多噪声，即模型过于复杂（也可以通过简化模型或增加数据集等方法尽量避免过拟合的发生）。

## 正则化的常见类型:

（1）L1正则化

可以通过稀疏化（减少参数“数量”）来降低模型复杂度的，即可以将参数值减小到0。

（2）L2正则化

可以通过减少参数值“大小”来降低模型的复杂度，即只能将参数值不断减小，但永远不会减小为0，只能尽量接近于0。

## 关联概念

过拟合、正则化、经验风险最小化、结构风险最小化、损失函数、模型复杂度、范数

# bias和variance是什么？

## 解释1 

bias 偏差 ：模型的期望（或平均）预测和正确值之间的差别；

variance 方差 ：模型之间的多个拟合预测之间的偏离程度。

## 解释2 

bias和variance分别从两个方面来描述了我们学习到的模型与真实模型之间的差距；

bias是 “用所有可能的训练数据集训练出的所有模型的输出的平均值” 与 “真实模型”的输出值之间的差异；

variance则是“不同的训练数据集训练出的模型”的输出值之间的差异。

## 解释3 

首先 Error = bias + variance

Error反映的是整个模型的准确度，bias反映的是模型在样本上的输出与真实值之间的误差，即模型本身的精准度，variance反映的是模型每一次输出结果与模型输出期望之间的误差，即模型的稳定性；

更准确地讲Error分成3个部分：Error = bias + variance + noise;