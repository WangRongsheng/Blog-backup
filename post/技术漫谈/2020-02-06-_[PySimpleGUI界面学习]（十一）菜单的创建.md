---
layout: post
cid: 170
title:  [PySimpleGUI界面学习]（十一）菜单的创建
slug: 170
date: 2020/02/06 13:05:38
updated: 2020/02/06 13:05:38
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 简述

从 `windows1.0` 开始，计算机的图形用户界面就开始快速发展起来了，附加而来的许多标配元素也慢慢让几乎所有用户熟悉了，在许多人看来，一个图形界面带有菜单栏是再正常不过的一件事，那么，菜单栏究竟是什么东西呢？其实究其实际，它也并不会比一个普通的按钮有多高明的地方，只不过菜单栏往往是一组按钮，一般附加在窗体的正上方，而且其呈一行式排列，当用户点击其一时，它往往会呈抽屉式弹出一条菜单来，当然那只是诸多不同功能按钮的集合罢了。

# 菜单在PySimpleGUI中的实现

在 `PySimpleGUI`中，菜单是与窗体的创建分离开的，要创建一个菜单十分容易，和创建窗体的语法十分相似，即先定义一个列表，然后调用`PySimpleGUI`的`Menu`函数将该列表填入即可，当创建窗体时，将该`Menu`语句创建的菜单放置于窗体的第一行，其余就和前面创建窗体的方法一样了。

# 一个菜单的小例子

下面展示了一个简单的创建菜单的小例子：

```python
import PySimpleGUI as sg      

sg.ChangeLookAndFeel('LightGreen')      
sg.SetOptions(element_padding=(0, 0))      

# ------ Menu Definition ------ #      
menu_def = [['File', ['Open', 'Save', 'Exit'  ]],      
            ['Edit', ['Paste', ['Special', 'Normal', ], 'Undo'], ],      
            ['Help', 'About...'], ]      

# ------ GUI Defintion ------ #      
layout = [      
    [sg.Menu(menu_def, )],      
    [sg.Output(size=(60, 20))]      
            ]      

window = sg.Window("Windows-like program", default_element_size=(12, 1), auto_size_text=False, auto_size_buttons=False,      
                    default_button_element_size=(12, 1)).Layout(layout)      

# ------ Loop & Process button menu choices ------ #      
while True:      
    event, values = window.Read()      
    if event == None or event == 'Exit':      
        break      
    print('Button = ', event)      
    # ------ Process menu choices ------ #      
    if event == 'About...':      
        sg.Popup('About this program', 'Version 1.0', 'PySimpleGUI rocks...')      
    elif event == 'Open':      
        filename = sg.PopupGetFile('file to open', no_window=True)      
        print(filename) 

window.Close()   
```

其运行截图如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yWj41.png" alt="1yWj41.png" border="0" />

当用户点击其中的菜单按钮时，凡是有定义的菜单都会做出相应的反应。

如果用户在创建菜单时，在`Menu`函数的参数中添加`tearoff=True`时，再次运行程序，点击菜单时会发现在每个弹出的菜单下有条虚线，如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yfKKS.png" alt="1yfKKS.png" border="0" />

如果用户用鼠标双击这条虚线，该弹出的菜单将会自动独立飞出成为悬浮于主窗体的一个小窗体，相当酷。如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yf1Ej.png" alt="1yf1Ej.png" border="0" />

# 小结

这篇文章简单介绍了菜单如何创建，有兴趣的读者仔细研究这段代码，自然会发现许多有趣的东西。

