---
title: 'Python「剪藏」网页为 PDF'
date: 2020-05-20 18:41:37
tags: [Python]
published: true
hideInList: false
feature: 
isTop: false
---

<!-- more -->
# 简介

`Python` 的第三方库`pdfkit` ，这个模块可以将网页、`html` 文件以及字符串生成pdf文件。

把我们想要的网页保存到本地PDF文件，再结合PDF神器（Adobe Acrobat Pro DC）高亮标记文章的重点内容，很舒服~

下面介绍一下使用pdfkit保存网页、html文件为pdf文件的具体过程。

# 安装使用

## 安装

### 使用pip安装pdfkit库

使用pip安装`pdfkit` 库：

```html
pip install pdfkit
```

### 安装wkhtmltopdf.exe文件

`pdfkit` 是基于`wkhtmltopdf` 的`python` 封装，需要安装`wkhtmltopdf.exe` 。`wkhtmltopdf` 是轻量级软件，非常很容易安装。

下载地址:https://wkhtmltopdf.org/downloads.html

去官网下载安装好之后，将安装目录下的bin添加到环境变量的path中。

> 环境变量配置在Windows上的步骤依次为：右键“此电脑”->属性->高级系统设置->环境变量->系统变量->Path

## 使用

- 网页生成pdf：`pdfkit.from_url()`
- html文件生成pdf：`pdfkit.from_file()`
- 字符串生成pdf：`pdfkit.from_string()`

其中，第一个参数为准备保存的链接地址或者html文件，第二个参数为保存的文件路径。

```python
# 导入库
import pdfkit

path_wk = r'E:\wkhtmltopdf\bin\wkhtmltopdf.exe'    #安装位置
config = pdfkit.configuration(wkhtmltopdf = path_wk)
pdfkit.from_url(r'https://zhuanlan.zhihu.com/p/140750619', 'wenzhang.pdf' ,configuration=config)

'''
pdfkit.from_file('wenzhang.html','wenzhang1.pdf')
pdfkit.from_string('Hello Pdf!','wenzhang2.pdf')
'''
```