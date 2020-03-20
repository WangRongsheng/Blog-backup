---
title: Python实现抠图换背景
date: 2019-10-02 19:08:15
thumbnail: https://i.loli.net/2019/10/02/DvGWrq9kA7dZS1n.png
tags: 抠图
categories: Python
---
曾几何时，「抠图」是一个难度系数想当高的活儿，但今天要介绍的这款神工具，只要 3 行代码 5 秒钟就可以完成高精度抠图，甚至都不用会代码，点两下鼠标就完成了。

<!--more-->

感受下这款抠图工具抠地有多精细：

<a href="https://sm.ms/image/lND3yYQmRt6MfqW" target="_blank"><img src="https://i.loli.net/2019/10/02/lND3yYQmRt6MfqW.jpg" ></a>

<a href="https://sm.ms/image/62lx89uR5zPGjvg" target="_blank"><img src="https://i.loli.net/2019/10/02/62lx89uR5zPGjvg.jpg" ></a>

这款工具叫：[Remove.bg](https://github.com/brilam/remove-bg)  。基于 Python、Ruby 和深度学习技术开发，通过强大的 AI 人工智能算法实现自动识别出前景主体与背景图，分分钟秒秒钟完成抠图。这样下去PS 设计师都快要下岗了。

怎么使用这款抠图工具呢？有多种简单方式。

## Python 实现

安装相应的库：

```cmd
pip install removebg
```

在[Removebg网站](https://www.remove.bg/) 上注册获取 API 后就可以使用了：

**单张图：**

```python
from removebg import RemoveBg
rmbg = RemoveBg("WPZ2Q4fraseKfAN9PPxxxxxx", "error.log") # 引号内是你获取的API
rmbg.remove_background_from_img_file("C:/Users/sony/Desktop/1.jpg") #图片地址
```

**批量图片：**

```python
from removebg import RemoveBg
import os

rmbg = RemoveBg("WPZ2Q4fraseKfAN9PPxxxxxx", "error.log")
path = '%s/picture'%os.getcwd() #图片放到程序的同级文件夹 picture 里面
for pic in os.listdir(path):
    rmbg.remove_background_from_img_file("%s\%s"%(path,pic))
```

## 网站实现

[Removebg网站](https://www.remove.bg/)

## 软件实现

oneindex下载：http://pan.sqdxwz.com/?/软件/