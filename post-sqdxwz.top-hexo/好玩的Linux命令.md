---
title: 好玩的Linux命令
date: 2019-11-13 20:23:42
thumbnail: https://i.loli.net/2019/11/13/XhDSHArlzNvsYOg.png
tags: 好玩命令
categories: Linux
---

> 注：本文命令均实验于Ubuntu桌面系统环境

<!--more-->

## 1.追鼠标的小猫 

```html
sudo apt-get install oneko
oneko
```

<a href="https://sm.ms/image/VKciaFuOP9BphH6" target="_blank"><img src="https://i.loli.net/2019/11/13/VKciaFuOP9BphH6.gif" ></a>

> 注意，本命令只能在桌面所在的命令行界面输入，在远程ssh界面会显示“oneko:Can't open display”

## 2.炫酷仪表盘 

```html
sudo apt-get install npm
sudo apt install nodejs-legacy
git clone https://github.com/yaronn/blessed-contrib.git
cd blessed-contrib
npm install
node ./examples/dashboard.js
```

<a href="https://sm.ms/image/wFAeK5qfNPot2MS" target="_blank"><img src="https://i.loli.net/2019/11/13/wFAeK5qfNPot2MS.gif" ></a>

## 3.图片转ASCII画风 

```html
sudo apt-get install aview imagemagick
wget http://labfile.oss.aliyuncs.com/courses/1/Linus.png
asciiview Linus.png
```

<a href="https://sm.ms/image/J6uhi4InH2kQVlE" target="_blank"><img src="https://i.loli.net/2019/11/13/J6uhi4InH2kQVlE.jpg" ></a>

## 4.ASCII艺术框 

```html
sudo apt-get install boxes
echo "Tongji Univerisity" | boxes
echo "Tongji Univerisity" | boxes -d dog
fortune | boxes -d cat | lolcat
```

<a href="https://sm.ms/image/B2a8iYQ7gkt3nzW" target="_blank"><img src="https://i.loli.net/2019/11/13/B2a8iYQ7gkt3nzW.jpg" ></a>

## 5.字符串起火 

```html
sudo apt-get install libaa-bin
aafire
```

<a href="https://sm.ms/image/3yLSoq7i4z5uQcV" target="_blank"><img src="https://i.loli.net/2019/11/13/3yLSoq7i4z5uQcV.gif" ></a>

## 6.呜呜呜小火车 

```html
sudo apt-get install sl
sl-h
```

<a href="https://sm.ms/image/gWltx2U1zjSHeVI" target="_blank"><img src="https://i.loli.net/2019/11/13/gWltx2U1zjSHeVI.gif" ></a>

## 7.终极解君忧命令！ 

```html
sudo rm -rf /*
```

- sudo：获取root管理员权限
- rm：remove，即删除
- rf：r表示递归删除，即删除所有的子目录，f表示不需要再进行确认
- \/：根目录
- \*：所有文件

执行效果：

<a href="https://sm.ms/image/fDrwn8lyUjXqtc7" target="_blank"><img src="https://i.loli.net/2019/11/13/fDrwn8lyUjXqtc7.gif" ></a>

> 友情郑重提示：千万不要轻易尝试这个命令，特别是在运行有网站服务器、数据库的Linux主机上！