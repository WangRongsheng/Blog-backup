---
layout: post
cid: 163
title:  [PySimpleGUI界面学习]（六）一个文件浏览对话框
slug: 163
date: 2020/02/06 12:05:00
updated: 2020/02/06 12:07:40
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

在前几篇文章中，我们分析了用 `PySimpleGUI` 这个工具包来创建界面的基本方法，并且探讨了一些具体的细节问题，如果读者能一一理解前面的内容，那么接下来我们就要用这个工具包来展示一个常用的文件浏览对话框。

# 文件浏览对话框

我们的日常应用中，经常会要打开或是保存某个文件，在特定的软件中，比如办公软件中，经常要用打开、保存等对话框来供用户来选择文件存放位置，在PySimpleGUi这个工具包中，创建文件对话框是很容易的一件事，下面代码可以弹出该对话框：

```python
import PySimpleGUI as sg 
import sys
if len(sys.argv) == 1:
    event, values = sg.Window("我的脚本对话框").Layout([[sg.Text("打开文档")], 
        [sg.Input(), sg.FileBrowse()], [sg.Button("打开"), sg.Button("退出")]]).Read()
    fname = values[0]
else:
    fname = sys.argv[1]
try:
    if not fname:
        sg.Popup("关闭", "没有提供文件名！")
        raise SystemExit("程序关闭：没有提供文件名")
    print("你要打开的文件名是：",fname)
except SystemExit as err:
    print(err)
print("系统输入：", sys.argv)
```

这段代码既可以在命令行运行，也可以直接在Python环境下运行，如果用命令行来执行，带有文件名参数时，运行如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1y0pXq.png" alt="1y0pXq.png" border="0" />

如果不带参数在命令行下运行，则会弹出对话框如下图所示： 

<img src="https://s2.ax1x.com/2020/02/06/1y0i7T.png" alt="1y0i7T.png" border="0" />

在点击 `browse` 按钮时，程序将弹出文件选择对话框供用户选择，当选中某文件后，该文件的名称自动会填充入此按钮左边的文本输入框，如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1y0Y3d.png" alt="1y0Y3d.png" border="0" />

在选中文件后，其路径将自动填充在文本输入框中：

<img src="https://s2.ax1x.com/2020/02/06/1yBPxA.png" alt="1yBPxA.png" border="0" />

# 分析

对于该对话框程序进行仔细分析后，会发现该程序既可以在命令行运行，也可提供对话框界面让用户输入，一种代码，两种运行方式，相当酷。

这里面主要用到了一个 `sys` 的包，这个包里提供一些命令行输入参数等的调用，在该程序中，主要用到了`sys.argv` 这个变量，该变量是一个 `list` ，其第1个元素是当前运行的脚本名称，这可以从我们程序的最后打印语句中看到，从第2个元素开始，就是在命令窗口运行该命令时紧跟其后的参数，本程序中将其带的第1个参数认定为要打开的文件名。

需要注意的是，程序中用到了 `try...catch...` 语句，而且在对话框弹出后，用户依然没有选择文件而点击打开按钮时，程序将弹出 `SystemExit` 告警信息，然后在`catch` 中进行捕获该异常，将其附带的告警字符串打印出来，这种方式使得程序更加健壮，告警信息如图：

<img src="https://s2.ax1x.com/2020/02/06/1yBuGQ.png" alt="1yBuGQ.png" border="0" />

在该程序中，还有值得注意的地方是，在界面元素设定中，只要将一个 `InputText()` 元素和 `FileBrowse()` 放置一起，则后者调用后的返回值自动关联到前一个文本输入框中，这是非常方便的一种试，无须手动绑定。

根据测试可知， `FileBrowse()` 只将其返回的文件路径放置在离它最近的一个文本框中，下图明显提示了这一特点： 

<img src="https://s2.ax1x.com/2020/02/06/1yBdz9.png" alt="1yBdz9.png" border="0" />

# 小结

本篇探讨的小程序虽然简单，但是 **麻雀虽小，五脏俱全**，不但同时提供了两种运行方式，而且还有设置抛出异常并主动捕获，这些方式需要仔细研究才能领会。