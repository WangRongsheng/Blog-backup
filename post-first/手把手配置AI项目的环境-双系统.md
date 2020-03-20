---
title: 手把手配置AI项目的环境(双系统)
date: 2019-11-02 13:07:42
thumbnail: https://i.loli.net/2019/11/02/bhVSHjf8c3wEGBv.png
tags: 双系统
categories: 杂谈
---

此篇文章是为了介绍如何安装双系统（win+ubuntu），对于简单的一下过程不再描述，对于关键环节做出说明介绍。

<!--more-->

## 1.下载ubuntu镜像

可以先进入中国linux官网：https://cn.ubuntu.com/ ，选择Ubuntu桌面系统，之后选择下载ubuntu。

可以选择两个版本，这两个版本都是比较稳定的：

1. http://releases.ubuntu.com/18.04/

2. http://releases.ubuntu.com/16.04/

## 2.制作启动盘

建议实用**USBwriter** 进行制作

## 3.电脑磁盘分区

自行百度

## 4.设置BIOS，U盘启动

有些电脑需要设置BIOS启动，其他电脑我用过DELL等，都是直接开机长按F2,F12,F10都有，如何成功进入BIOS，百度一下自己的电脑即可。

当然如果是笔记本就是Fn+按键即可

## 5.开始安装Ubuntu

一波傻瓜式操作

## 6.分区

主要分以下这些：

```html
swap：用作虚拟内存，这个一般和自己的物理内存一般大
/：主要用来存放Linux系统文件
/boot:存放linux内核，用来引导系统的，如果是Legacy启动就要设置引导，UEFI就不用设置这个（UEFI要设置EFI文件）
/usr:存放用户程序，一般在/usr/bin中存放发行版提供的程序，用户自行安装的程序默认安装到/usr/local/bin中
/home:存放用户文件
```
当初压缩的磁盘如下图所示，选中那个空闲磁盘，然后点击+号，开始分配。

<a href="https://sm.ms/image/lnKGxUCBOs4zVXu" target="_blank"><img src="https://i.loli.net/2019/11/02/lnKGxUCBOs4zVXu.jpg" ></a>

① 分配swap，选择主分区，空间起始位置，大小最好和自己物理内存一样（我的是16G分配两倍，以后可能装个内存条所以分配32G），用于交换空间

<a href="https://sm.ms/image/FEjanXhHdep8QrM" target="_blank"><img src="https://i.loli.net/2019/11/02/FEjanXhHdep8QrM.jpg" ></a>

② 设置EFI引导，选择逻辑分区，空间起始位置，用于EFI系统分区，大小设置4G即可

③ 设置Boot引导，选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/boot，大小设置8G

④ 设置/，选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/，大小的话推荐100G.

⑤ 设置home，选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/home，home大一些300G

⑥ 设置usr，选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/usr，大小的话剩下100G。

以上分配方式，EFI需要依照前面的①步骤分配，其余②-⑥全部以home分配为例进行分配如下图类似，自行分配即可，不一样的只是分配的大小 

<a href="https://sm.ms/image/ZjfQMvzmsEaJH2L" target="_blank"><img src="https://i.loli.net/2019/11/02/ZjfQMvzmsEaJH2L.jpg" ></a>

分配好之后如下图方框所示，椭圆形为需要安装的前的最后一步设置引导器，选择设置为EFI的引导盘作为安装启动器设备，如下图所示。 

<a href="https://sm.ms/image/2lcSFuvPotEpefA" target="_blank"><img src="https://i.loli.net/2019/11/02/2lcSFuvPotEpefA.jpg" ></a>

<a href="https://sm.ms/image/u2capUBFsWNICkP" target="_blank"><img src="https://i.loli.net/2019/11/02/u2capUBFsWNICkP.jpg" ></a>

<a href="https://sm.ms/image/8CkmYrosnFx1ZTA" target="_blank"><img src="https://i.loli.net/2019/11/02/8CkmYrosnFx1ZTA.jpg" ></a>

等待完成就可以了。

## 7.设置启动引导

可以实用EasyBCD 2.3软件来设置引导，参考如下：https://blog.csdn.net/u014422976/article/details/80393841

自我感觉比较麻烦并且很多时候不好用，这里推荐使用BOOT引导，即：首先进入电脑BIOS设置后，把boot的linux启动项调到windows上面即可，之后保存重启即可进入每次就有选系统的界面了。

## 8.一些问题的解决

解决方法：

Pro1：安装ubuntu的时候由于分辨率问题，导致安装界面显示不全（如图），没法继续安装
https://zhidao.baidu.com/question/522177686034499645.html?word=Ubuntu 安装过程中分辨率不兼容

Pro2：最后的引导问题：
https://blog.csdn.net/u014422976/article/details/80393841

Pro3：装Ubuntu老停在ubuntu界面
https://zhidao.baidu.com/question/923767939677091819?g_f=11301026&word= 装Ubuntu老停在ubuntu界面

Pro4：ubuntu 安装完成后重启电脑报错: BUG soft lockup 的解决办法
https://blog.csdn.net/xrinosvip/article/details/80447139

Pro5: 解決搜狗输入法无法安装的问题：
https://blog.csdn.net/qq_22186119/article/details/70316727

Pro6: ubuntu搜狗输入法中文无法切换英文：
https://blog.csdn.net/kang_tju/article/details/54630994

Pro7：装完双系统之后,linux和windows转换最后windows下时间错乱，早了八个小时解决方案
https://blog.csdn.net/qq_40197828/article/details/79334158

Pro8: Linux（Ubuntu16.04）调节屏幕亮度（亮度控制条消失的问题）：
https://blog.csdn.net/kingthon/article/details/81190898



