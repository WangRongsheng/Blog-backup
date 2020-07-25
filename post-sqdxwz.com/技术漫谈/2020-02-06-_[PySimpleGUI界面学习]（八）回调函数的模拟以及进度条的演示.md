---
layout: post
cid: 166
title:  [PySimpleGUI界面学习]（八）回调函数的模拟以及进度条的演示
slug: 166
date: 2020/02/06 12:36:02
updated: 2020/02/06 12:36:02
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

在前面几次教程中我们整体认知了 `PySimpleGUI` 这个工具包的基本使用方法，也见识了其中的一些控件使用。这个工具包主要是简化界面的编写，将界面对于用户输入的采集自动化完成。

# 回调函数模拟

在传统的界面编程中，程序员需要对控件的每一个响应编写一个回调函数，这个意思是指当用户点击某个按钮或是某个控件的状态改变时，程序需要做出的反应。

事实上，在 `PySimpleGUI` 这个工具包中，并不需要对专门的按钮去做一个回调函数编写，但是如果想实现也是一件容易的事情，下面的代码对这个进行一个简单的展示。

```python
import PySimpleGUI as sg

def button1():
    print("按钮1被点击")
    
def button2():
    print("按钮2被点击")
    
layout = [[sg.Text("请点击一个按钮")],
         [sg.Button("1"), sg.Button("2"), sg.Button("退出")]]

window = sg.Window("回调函数模拟").Layout(layout)

while True:
    event, values = window.Read()
    if event == "1":
        button1()
    elif event == "2":
        button2()
    elif event is None or event=="退出":
        window.Close()
        break
sg.PopupOK("完成！")
```

执行程序的界面如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yyPFf.png" alt="1yyPFf.png" border="0" />

当用户分别点击两个按钮时，控制台上将打印出各自按钮回调函数中所预先定义的语句。如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yyMkV.png" alt="1yyMkV.png" border="0" />

# 分析

由于 `PySimpleGUI` 这个工具包本身已经将界面的侦测自动化处理，所以上述的回调函数本身并没有真正揭示出回调函数对于普通界面编程的意义，但是从这个仿真模拟可以看出，这种比较类似于普通的回调，尽管以现在看方式来看，创建两个函数去打印两个语句有多余的感觉，但是如果从函数模块化编程的角度来考虑，将特别的功能独立出来，这种方式却也有其可取之处。

# 实战

现在我们还做一个简单的小例子，再一次来体会一下PySimpleGUI工具包封装的强大。

在这个小例子中，我们来试验一种特别的控件————进度条，即用一个简单的循环就可以将一个进度条创建出来，这种方式是不是特别酷？

代码如下：

```python
import PySimpleGUI as sg      

for i in range(10000):      
    sg.OneLineProgressMeter('一行进度条的例子', i+1, 10000, 'key')
```

这个神奇的例子将显示如下截图：

<img src="https://s2.ax1x.com/2020/02/06/1yycnA.png" alt="1yycnA.png" border="0" />

当然，我们很多时候希望自己能够来将进度条添加在我们的界面上，那就要用到该库中的 `ProgressBar` 这个控件，代码如下：

```python
import PySimpleGUI as sg

layout = [[sg.Text('一个自定义的进度条例子')],      
          [sg.ProgressBar(10000, orientation='h', size=(20, 20), key='progressbar')],      
          [sg.Button("退出")]]

window = sg.Window('自定义进度条').Layout(layout)      
progress_bar = window.FindElement('progressbar')      
for i in range(10000):
    event, values = window.Read(timeout=0)      
    if event == '退出'  or event is None:      
        break      
    progress_bar.UpdateBar(i + 1)      
window.Close()
```

这段代码演示了自定义进度条是如何工作的，其运行如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yybBn.png" alt="1yybBn.png" border="0" />

从运行来看，当用户点击退出按钮时，即使进度条没有完成，也会退出。不过从下面一个例子再来看的话，你会发现一个奇怪的事情，代码如下：

```python
import PySimpleGUI as sg

layout = [[sg.Text('一个自定义的进度条例子')],      
          [sg.ProgressBar(10000, orientation='h', size=(20, 20), key='progressbar')],      
          [sg.Button("执行"), sg.Button("退出")]]

window = sg.Window('自定义进度条').Layout(layout)      
progress_bar = window.FindElement('progressbar')  

while True:
    event, values = window.Read(timeout=10)   
    if event == '退出'  or event is None: 
        break
    elif event == "执行":
        for i in range(10000):
            progress_bar.UpdateBar(i+1)
window.Close()
```

以上代码的运行界面如图：

<img src="https://s2.ax1x.com/2020/02/06/1yc0Qe.png" alt="1yc0Qe.png" border="0" />

从运行中可知，当用户在进度条滚动时无论如何点击退出按钮，窗口也无法关闭。这是什么原因呢？原来这牵扯到另一个问题了，即同一个进程中，当界面在执行某一段代码时，是不会理会其他行为的，那么若想同时执行两个行为怎么办呢，这就是以后要讲到的线程问题了。