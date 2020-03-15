---
layout: post
cid: 270
title: 获取GoogleDrive无限网盘
slug: 270
date: 2020/03/14 20:11:00
updated: 2020/03/14 20:11:32
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 无限网盘
thumb2: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=320743311,4120194597&fm=26&gp=0.jpg
---


<!--more-->
<img src="https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=320743311,4120194597&fm=26&gp=0.jpg">
1. 首先登陆Google账号 [Google](https://www.google.com/)
<img src="https://s1.ax1x.com/2020/03/14/8lnXtS.png" alt="1" border="0">

2. 登陆成功后 进入GoogleDrive
<img src="https://s1.ax1x.com/2020/03/14/8lnOk8.png" alt="2" border="0">

3. 我们进入到自己的 drive 中后，是只有一个 我的云端硬盘 并且只有15GB的空间
<img src="https://s1.ax1x.com/2020/03/14/8lumc9.png" alt="8lumc9.png" border="0" />

4. 接下来我们新建一个页面访问 https://gd.zxd.workers.dev/
这是一个 [GitHub项目](https://github.com/yyuueexxiinngg/some-scripts/blob/master/workers/google/drive/create-share-teamdrive.js) 有兴趣的可以去看看，原理是通过js去创建一个 **团队网盘**

5. 打开链接后需要填入相关信息，邮箱填写你自己的
<img src="https://s1.ax1x.com/2020/03/14/8luy9g.png" alt="8luy9g.png" border="0" />

6. 信息填好后 点击 `提交` ，稍微等待一小会，会弹出成功的提示

7. 现在就可以关闭当前这个页面了，回到刚刚登陆的 GoogleDrive 会发现 刚刚的15GB还是15GB ,但是多了一个共享的网盘
<img src="https://s1.ax1x.com/2020/03/14/8lKnPS.png" alt="8lKnPS.png" border="0" />

我们可以看看管理信息
<img src="https://s1.ax1x.com/2020/03/14/8lKsVx.png" alt="8lKsVx.png" border="0" />
里面就你一个人是，并且是管理员。

至于那个档案所属域，我看代码里面好像是一个变量设置的，也不清楚是不是属于另外一个账号，所以这个共享的网盘，我们可以放放大容量的电影，镜像文件啥的，私密性的数据千万不要放，当然，无论是 GoogleDrive还是百度云，其实任何数据只要一上云就会有泄漏的风险，最保险的就是自己搭建NAS私有云。