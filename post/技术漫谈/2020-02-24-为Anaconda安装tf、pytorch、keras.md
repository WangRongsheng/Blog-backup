---
layout: post
cid: 255
title: 为Anaconda安装tf、pytorch、keras
slug: 255
date: 2020/02/24 23:46:00
updated: 2020/02/24 23:46:00
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 环境配置
thumb2: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1629994617,2449101888&fm=26&gp=0.jpg
---


<!--more-->

<img src="https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1629994617,2449101888&fm=26&gp=0.jpg" />

# Anaconda3介绍

简单来说，Anaconda是Python的包管理器和环境管理器。

先来解决一个初学者都会问的问题：我已经安装了Python，那么为什么还需要Anaconda呢？原因有以下几点：

1. Anaconda附带了一大批常用数据科学包，它附带了conda、Python和 150 多个科学包及其依赖项。因此你可以用Anaconda立即开始处理数据。

2. 管理包。Anaconda 是在 conda（一个包管理器和环境管理器）上发展出来的。在数据分析中，你会用到很多第三方的包，而conda（包管理器）可以很好的帮助你在计算机上安装和管理这些包，包括安装、卸载和更新包。

3. 管理环境。为什么需要管理环境呢？比如你在A项目中用到了Python2，而新的项目要求使用Python3，而同时安装两个Python版本可能会造成许多混乱和错误。这时候conda就可以帮助你为不同的项目建立不同的运行环境。还有很多项目使用的包版本不同，比如不同的pandas版本，不可能同时安装两个pandas版本。你要做的应该是在项目对应的环境中创建对应的pandas版本。这时候conda就可以帮你做到。

# Anaconda3的安装

1. [官网地址](https://www.anaconda.com/download/)
2. [清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/)

关于安装过程中的细节,如全局变量设置...可自行百度,下面我们转入正题

# Anaconda3安装tensorflow

1. 打开anaconda安装时自带的Anaconda prompt

2. 打开后,输入清华镜像的tensorflow的下载地址(如果你已经在墙外翱翔了,可以省略这一步):
 ```html
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
 ```
 
3. 接着我们开始创建一个python3.6的环境,因为如果你安装的是最新的anaconda,它默认环境为py3.7,并且在不久之前,tensorflow已经开始支持py3.6,所以我们创建一个py3.6环境:
 ```html
conda create -n tensorflow python=3.6
 ```
 
4. 启动anaconda中的py3.6环境:
 ```html
activate tensorflow
 ```
 
如果不能进入,则重新执行第3步骤

5. 进入py3.6的环境中后,我们就可以进行安装了(此处我们安装的是CPU版本的tensorflow):
 ```html
pip install --upgrade --ignore-installed tensorflow 
  ```
  
6. 当我们不使用tensorflow时,我们就可以使用:
 ```html
deactivate
 ```
 
 退出该环境
 
7. 开始测试一下是否安装成功:

重新打开Anaconda Prompt—>activate tensorflow—>python来启动tensorflow，并进入python环境
 ```python
#TensorFlow使用图(Graph)来表示计算任务；并使用会话(Session)来执行图，通过Session.close()来关闭会话（这是一种显式关闭会话的方式）。会话方式有显式和隐式会话之分。
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')  #初始化一个TensorFlow的常量
sess = tf.Session()  #启动一个会话
print(sess.run(hello))  
 ```
 
如果可以准确的输出结果,那么恭喜你,安装tensorflow成功!

# Anaconda3安装pytorch

1. 打开anaconda安装时自带的Anaconda prompt

2. 创建py3.6环境:
 ```html
conda create -n pytorch python=3.6
 ```
 
3. 启动anaconda中的py3.6环境:
 ```html
activate pytorch
 ```
 
4. PyTorch 的官网提供了简单的安装方法，只需简单的命令即可。

首先，打开 PyTorch 官网安装页面（需自备梯子）：https://pytorch.org/get-started/locally/

然后复制页面中Run this Command后的代码,粘贴在你的命令行,等待安装完成就可以了~

# Anaconda3安装keras

其实keras是可以与tensorflow在共同环境下使用的,所以我们可以直接将keras安装在我们的tensorflow环境中。

1. 打开anaconda安装时自带的Anaconda prompt

2. 创建py3.6环境:
 ```html
conda create -n tensorflow python=3.6
 ```
 
3. 启动anaconda中的py3.6环境:
 ```html
activate tensorflow
 ```
 
4. 直接运行命令:
 ```html
conda install keras
或者
pip install keras 
 ```
 
 等待安装完成即可。