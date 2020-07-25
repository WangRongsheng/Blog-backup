---
layout: post
cid: 256
title: 将Git与Github进行SSH连接
slug: 256
date: 2020/02/25 10:27:00
updated: 2020/02/25 10:29:22
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - Git与Github
thumb2: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=112763915,265947675&fm=26&gp=0.jpg
---


<!--more-->
<img src="https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=112763915,265947675&fm=26&gp=0.jpg">

# Githu与Github

首先，
- `Git`是一款免费、开源的分布式版本控制系统；
- `Github`是用`Git`做版本控制的代码托管平台；

用一句话形容这二者的关系：Git是弓，你的代码是箭，Github是靶子。 Git是软件,它可在本地建立仓库,你写的代码的各个版本都可以存着 Github是网上仓库,你写的代码的各个版本都可以存着。 

# 安装使用

## 安装Git

1. 到[Git官网](https://git-scm.com/downloads)下载与你正在使用的操作系统(本文以`windows`为例)相对应的文件。一般地，选择`64-bit Git for Windows Setup`。
2. 安装时注意：勾选添加git到`环境变量`；在Windows Explorer Integration中勾选`Git Bash Here`。其余配置默认即可。
3. 安装完成后(可能需要**注销或重启**)，在任意一个文件夹空白处右键，检查是否有`Git Bash Here`的选项。

## 注册GitHub

到[GitHub官网](https://sqdxwz.com)注册一个账号。这里我以我的Github账号：`WangRongsheng` 为例进行演示。

## 配置git与github关联

### 设置邮箱和用户名

打开`Git Bash`(输入命令**均在Git Bash中进行**，以后不再声明)，分别输入下列命令(输入一行命令后需要回车，以后不再声明)：

```html
git config --global user.name "WangRongsheng"
git config --global user.email "603329354@qq.com"
```

下面这一行设置可以增强输出命令的可读性：

```html
git config --global color.ui auto
```

### 用ssh生成公钥

输入：

```html
ssh-keygen -t rsa -C "603329354@qq.com"
```

回车之后会出现如下所示的输出，直接按回车即可：

```html
Generating public/private rsa key pair.
Enter file in which to save the key
(/Users/your_user_directory/.ssh/id_rsa): (按回车键)
Enter passphrase (empty for no passphrase): (按回车键)
Enter same passphrase again: (按回车键)
```

这样密钥文件就生成了，默认在用户目录下，如：`C:\User\xxx\.ssh\` 这个文件夹中。其中的xxx是你的windows用户名。

### 将公钥添加到`github`中

1. 在`C:\user\xxx\.ssh\`文件夹中找到`id_rsa.pub`这个文件，用文本编辑器(如记事本)打开，复制里面的所有内容。
   
2. 登陆`github账号`，点击头像旁的`小三角`展开，点击`settings`-`SSH and GPG keys`-`New SSH key`，在`Title`中取一个名字（任意），`key`中粘贴你刚刚复制的内容。然后点击`Add SSH key`即可。

### 测试是否关联成功

输入：

```html
ssh -T git@github.com
```

出现以下结果即为成功：

```html
Hi WangRongsheng! You've successfully authenticated, but GitHub does not provide shell access.
```