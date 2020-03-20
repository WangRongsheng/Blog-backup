---
title: 解决在github上查看ipynb（大文件）笔记时加载很慢以及失败的问题
date: 2019-11-28 18:55:09
thumbnail: https://s2.ax1x.com/2019/11/28/QiOrGV.md.png
tags: 查看大文件
categories: 杂谈
---

# 问题

markdown和code能一起使用真是非常方便，在本地使用jupyter notebook书写笔记，然后上传到github上，不仅自己复习的时候方便查阅，还能帮到其他有需要的人。在github上查看ipynb文件以及大文件时，需要加载很长时间，而且经常加载失败。使用起来很不方便而且让人头疼、浪费时间。比如我查看优达学城的一个[深度学习](https://github.com/q759729997/Udacity_nd101_cn_p4/blob/master/dlnd_face_generation.ipynb) 的小项目，如果直接访问github仓库里的ipynb文件的话，会遇到加载失败或者等很久情况，如下图：

<!--more-->

<img src="https://s2.ax1x.com/2019/11/28/QiOSu4.png" alt="QiOSu4.png" border="0" />

# 解决

文件打不开很让人头疼，但是一个好的方法可以解决：
免费的[nbviewer开源项目](https://nbviewer.jupyter.org/) ，解决了上面的问题。所有上传到github上的ipynb文件，都会同步到nbviewer服务器上。笔记也经过了渲染，显示效果很棒，而且访问速度非常快，使用方法是在nbviewer主页上，输入别人或自己的github用户名，找到自己创建的仓库，再找到对应的笔记。比如上面无法显示的笔记，去nbviewer上查看的话，能快速打开笔记，方便查看笔记内容。例如输入刚才那位用户的ID：q759729997 或者刚才项目位置：q759729997/Udacity_nd101_cn_p4

<img src="https://s2.ax1x.com/2019/11/28/QiLXCV.png" alt="QiLXCV.png" border="0" />

瞬间就能打开自己想看的项目：

<img src="https://s2.ax1x.com/2019/11/28/QiL7Hs.png" alt="QiL7Hs.png" border="0" />

你们点击链接体验一下加载速度：[点击这里 深度学习项目](https://nbviewer.jupyter.org/github/q759729997/Udacity_nd101_cn_p4/tree/master/) ，然后再打开ipynb的笔记。
几万行的代码可以瞬间打开，不用因为加载失败或者打不开让你头疼。
你可别学经常使用github的不会这个技能。它可以让你大大的节省时间学习其他知识。
