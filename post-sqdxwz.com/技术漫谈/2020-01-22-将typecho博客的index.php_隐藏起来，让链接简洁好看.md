---
layout: post
cid: 125
title: 将typecho博客的index.php 隐藏起来，让链接简洁好看
slug: 125
date: 2020/01/22 11:08:00
updated: 2020/02/22 13:52:01
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - typecho技巧
thumb2: https://s2.ax1x.com/2020/01/22/1ASeJO.png
---


<!--more-->
# 一、引言

使用过typecho博客都知道，博客链接中会默认出现**index.php/**， 为了简洁好看，让我们动手隐藏它吧

# 二、操作

## 后台设置

<img src="https://s2.ax1x.com/2020/01/22/1ASeJO.png" alt="1ASeJO.png" border="0">

## 宝塔设置

> 如果不进行这一步操作，你会发现你点击自己的博文会出现404

放入代码：
```html
if (!-e $request_filename) {
  rewrite ^(.*)$ /index.php$1 last;
}
```
<img src="https://s2.ax1x.com/2020/01/22/1ASZFK.png" alt="1ASZFK.png" border="0">

重新刷新页面就完成了