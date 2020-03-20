---
title: Github Pages设置自定义域名
date: 2019-11-09 12:24:51
thumbnail: https://i.loli.net/2019/11/09/uOZmRirqz2WL63N.png
tags: Github Pages
categories: 杂谈
---

今日想来，我手下也有6个域名了，不如给我的Hexo+Github建立的博客换上一个域名吧。

新域名在这：https://sqdxwz.top

<!--more-->

把自定义域名的步骤进行记录-**三步设置自定义域名**。

## 1.获取博客的ip地址

首先是用ping命令找到存放你的github pages的主机的IP地址，在终端里面用命令ping xxx.github.io便可完成，下图中红框内的就是我们要找的IP地址：

<a href="https://imgchr.com/i/MeTGK1"><img src="https://s2.ax1x.com/2019/11/09/MeTGK1.md.png" alt="MeTGK1.png" border="0" /></a>

## 2.域名解析

在购买域名的提供商为域名添加解析。我是在阿里云买的域名，因此我以阿里云的为例。在域名控制台选择想要绑定的域名，并点击解析：

<a href="https://imgchr.com/i/MeTwPe"><img src="https://s2.ax1x.com/2019/11/09/MeTwPe.md.png" alt="MeTwPe.png" border="0" /></a>

然后添加如下两条记录：

<a href="https://imgchr.com/i/MeTyrt"><img src="https://s2.ax1x.com/2019/11/09/MeTyrt.md.png" alt="MeTyrt.png" border="0" /></a>

## 3.Github仓库设置

在Github中，找到托管博客的xxx.github.io项目：

<a href="https://imgchr.com/i/MeTfPg"><img src="https://s2.ax1x.com/2019/11/09/MeTfPg.md.png" alt="MeTfPg.png" border="0" /></a>

进入到设置页面，并滑动到下方，找到Github Pages这一栏，在Custom Domain填上刚刚添加解析的域名并保存：

<a href="https://imgchr.com/i/MeT7q0"><img src="https://s2.ax1x.com/2019/11/09/MeT7q0.md.png" alt="MeT7q0.png" border="0" /></a>

到这儿就已经完成了，等待10分钟后就可以使用自定义的域名访问github pages所提供的页面了。

## 4.后续

如果你不想每次在**hexo g -d** 后都重新设置下域名。

你可以在本地的**source文件** 下添加一个**CNAME文件** ，里面填写自己的自定义域名就好了。


