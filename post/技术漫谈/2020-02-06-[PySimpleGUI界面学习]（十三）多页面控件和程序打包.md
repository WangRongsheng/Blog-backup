---
layout: post
cid: 172
title: [PySimpleGUI界面学习]（十三）多页面控件和程序打包
slug: 172
date: 2020/02/06 13:35:09
updated: 2020/02/06 13:35:09
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 简述

到目前为止，我们已经介绍了`PySimpleGUI`中大多数控件，也熟悉了用`PySimpleGUI`来开发一个用户界面的方法，这一系列的教程到此基本上也该结束了，在最后，这一篇教程中再介绍一种多页面控件的使用方法。

在一个程序开发好以后，最后的环节是发布，本篇也将对如何发布一个软件做一个简单的介绍。

# `TabGroup`控件的使用

在许多软件中，我们看到过多页面的排列方式，即将功能类似的一些设置放在同一个页面，而为了更紧凑地集合程序，有时我们会将同一大类的功能按其小功能分类列于同一个窗体上，这就要用到多页面控件。

创建一个多页面控件是相当容易的，下面代码展示了一个简单多页面的创建：

```python
import PySimpleGUI as sg

tab1_layout =  [[sg.T('第一个页面的文本')]]
tab2_layout = [[sg.T('第二个页面的文本')],  [sg.In(key='in')]]

layout = [[sg.TabGroup([[sg.Tab('页面1', tab1_layout, tooltip='tip'), sg.Tab('页面2', tab2_layout)]], tooltip='TIP2')],
          [sg.Button('读取数据')]]

window = sg.Window('多页面窗口', default_element_size=(20,1)).Layout(layout)

while True:    
    event, values = window.Read()
    if event is None:           # always,  always give a way out!    
        break  
    print(event,values)
window.Close()
```

对代码的进一步分析，可以看出`Tab函数`和`Window函数`的调用类似，而`TabGroup`的用法也如同`Window`一样，熟悉前面教程的读者应该能很快领会这些代码的意思。

<img src="https://s2.ax1x.com/2020/02/06/1yI3LT.png" alt="1yI3LT.png" border="0" />

# 打包发布程序

对于`Windows`用户而言，创建一个不依赖于`Python`环境而能运行的`EXE文件`是必要的，事实上，对`Python`程序打包是非常容易的一件事，只需要安装一个第三方包`PyInstaller`即可，安装包的方法很容易，即用以下代码即可：

```html
pip install PyInstaller
```

安装完毕后，可以在命令行下执行以下代码，即能生成可执行文件：

```html
pyinstaller -wF tabex.py
```

在文件所在的目录下，以命令行运行上述命令后，将发会现当前目录下多了两个文件夹，一个是`build`，一个是`dist`，在`dist目录`下，我们将找到生成的可执行文件，双击后可执行，如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yIom8.png" alt="1yIom8.png" border="0" />

有关于`PyInstaller`的打包参数了解，可以直接访问其官方网站：`http://www.pyinstaller.org/`该网站有详细的打包过程描述。

# 小结

止此，我们花了许多时间研究了`PySimpleGUI`这个工具包，从各种界面程序的创建来看，其方式相当简单，对于界面编程的新手来说，这是非常好的入门工具，当然，该包目前正在快速迭代开发中，从客观上来说，将各种不同的界面工具包装成统一的接口是非常困难的事情，然而这些天才的程序员们还依然在为着这个伟大的理想努力奋斗着，我们目前只是工具的使用者，希望有一天，大家也能为该项目贡献出优秀的代码。