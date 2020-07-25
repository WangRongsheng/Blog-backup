---
title: win10配置Java开发环境
date: 2019-11-22 14:44:16
thumbnail: https://i.loli.net/2019/11/22/ziZwvrJqDmCn7cT.png
tags: 配置Java环境
categories: 杂谈
---

软件开发环境，是一个程序的运行的支撑，Java作为近年来最热门的编程语言之一，越来越多的新人程序员选择Java来学习，它的开发环境搭建也是学习和使用这一编程语言的基础。
今天我们将在Windows上配置Java的开发环境。

<!--more-->

<a href="https://sm.ms/image/x3CONMptcTi5uJ4" target="_blank"><img src="https://i.loli.net/2019/11/22/x3CONMptcTi5uJ4.jpg" ></a>

# 1.下载并安装JDK(JAVA Development Kit)

JDK是整个java开发的核心，它包含了JAVA的运行环境，JAVA工具和JAVA基础的类库。

> 下载地址：
http://www.oracle.com/technetwork/java/javase/downloads/index.html

安装JDK只需要按正常步骤安装即可

# 2.配置环境变量

## 基础配置

打开我的电脑，按照如下操作顺序：“鼠标右键-->属性-->高级系统设置-->高级-->环境变量”

<a href="https://sm.ms/image/zb6GcmSEqprThs7" target="_blank"><img src="https://i.loli.net/2019/11/22/zb6GcmSEqprThs7.jpg" ></a>

选择环境变量过后，我们可以看到如下界面，此时再选择“系统变量-->新建”，此时将会弹出新建系统变量的对话框，在变量名处输入“JAVA_HOME”，在变量值中输入JDK的安装路径，点击确定；

<a href="https://sm.ms/image/CZTdPL8Y9EfJOUz" target="_blank"><img src="https://i.loli.net/2019/11/22/CZTdPL8Y9EfJOUz.jpg" ></a>

修改”path”变量。在变量后增加两条路径

```html
%JAVA_HOME%\bin

%JAVA_HOME%\jre\bin
```

<a href="https://sm.ms/image/FIL26OmuTKb8fX5" target="_blank"><img src="https://i.loli.net/2019/11/22/FIL26OmuTKb8fX5.jpg" ></a>

## 新建/修改CLASSPATH 变量

如果存在 CLASSPATH 变量，选中点击 编辑。

如果没有，点击 新建。

输入/在已有的变量值后面添加：

```html
变量名：CLASSPATH
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
```

<a href="https://sm.ms/image/emZEnRfT9u23GPz" target="_blank"><img src="https://i.loli.net/2019/11/22/emZEnRfT9u23GPz.jpg" ></a>

## 检验环境变量是否配置成功 

Win+R打开dos窗口，分别输入java  ,javac  ,java –version

<a href="https://sm.ms/image/r5b3kVQNGmIe6wf" target="_blank"><img src="https://i.loli.net/2019/11/22/r5b3kVQNGmIe6wf.jpg" ></a>

如果你看到以上的内容，那么，恭喜，你的JAVA开发环境搭建成功了^_^。 