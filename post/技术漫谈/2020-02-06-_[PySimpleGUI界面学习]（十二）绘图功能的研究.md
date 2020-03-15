---
layout: post
cid: 171
title:  [PySimpleGUI界面学习]（十二）绘图功能的研究
slug: 171
date: 2020/02/06 13:25:07
updated: 2020/02/06 13:25:07
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 简述

绘图是图形用户界面的一种最常用功能之一，将复杂的几何图形、建筑设计图、天体运行轨迹等等展示在图形界面上，无疑会更便于观察，这次我们就来研究一下`PySimpleGUI`中有关绘图的部分，在这部分，该包是直接调用`Tkinter`中有关图形绘制函数的，所以如果直接将`PySimpleGUI`更换为不同类库`PySimpleGUIQt`时，程序会报错。

当然，图形的绘制我们在另一个有关`pygame`的教程中会详细介绍更有效率移动图形的方法，在这一篇中，我们只是简单做一尝试即可。

# 一个简单的示例

对于一个细节的研究，最好的办法莫过于研究一段程序，下面的程序展示了如何利用`Canvas`函数来创建一个画布。

```python
import PySimpleGUI as sg
layout = [
    [sg.Canvas(size=(100, 100), background_color='red', key= 'canvas')],
    [sg.T('改变圆的颜色:'), sg.Button('红色'), sg.Button('蓝色')]
    ]

window = sg.Window('画布测试')
window.Layout(layout)
window.Finalize()

canvas = window.FindElement('canvas')
cir = canvas.TKCanvas.create_oval(50, 50, 100, 100)

while True:      
    event, values = window.Read()
    if event is None:      
        break
    if event == '蓝色':      
        canvas.TKCanvas.itemconfig(cir, fill="Blue")
    elif event == '红色':      
        canvas.TKCanvas.itemconfig(cir, fill="Red")
window.Close()
```

上段代码运行如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yfzIs.png" alt="1yfzIs.png" border="0" />

当用户点击设置不同颜色的按钮时，图中绘制的圆形会改变不同的颜色，比如用户点击蓝色按钮时，圆形填充蓝色：

<img src="https://s2.ax1x.com/2020/02/06/1yhCR0.png" alt="1yhCR0.png" border="0" />

从以上代码可以看出一个画布如何创建，用`TKcanvas`如何进行图形绘制。

# `Graph`的使用

在图形绘制时，还可以使用另一个函数即Graph，这个函数本身就创建一个画布，在该画布上也可以绘制各种图形，下面这段代码演示了如何用该函数来创建图形，有兴趣的读者可以对两者进行比较。

```python
import PySimpleGUI as sg
layout = [
            [sg.Graph(canvas_size=(400, 400), graph_bottom_left=(0,0), graph_top_right=(400, 400), background_color='red', key='graph')],
            [sg.T('改变颜色:'), sg.Button('红色'), sg.Button('蓝色'), sg.Button('移动')]
            ]

window = sg.Window('图形测试')
window.Layout(layout)
window.Finalize()

graph = window.FindElement('graph')
circle = graph.DrawCircle((75,75), 25, fill_color='black',line_color='white')
point = graph.DrawPoint((75,75), 10, color='green')
oval = graph.DrawOval((25,300), (100,280), fill_color='purple', line_color='purple'  )
rectangle = graph.DrawRectangle((25,300), (100,280), line_color='purple'  )
line = graph.DrawLine((0,0), (100,100))

while True:      
    event, values = window.Read()
    if event is None:      
        break
    if event is '蓝色':      
        graph.TKCanvas.itemconfig(circle, fill = "Blue")
    elif event is '红色':      
        graph.TKCanvas.itemconfig(circle, fill = "Red")
    elif event is '移动':      
        graph.MoveFigure(point, 10,10)
        graph.MoveFigure(circle, 10,10)
        graph.MoveFigure(oval, 10,10)
        graph.MoveFigure(rectangle, 10,10)

window.Close()
```

程序运行图如下：

<img src="https://s2.ax1x.com/2020/02/06/1yhJdH.png" alt="1yhJdH.png" border="0" />

当用户点击移动时，会发现我们创建的几个图形元素开始移动，但是细心的同学将会发现我们用DrawPoint创建的点图形不会移动：

<img src="https://s2.ax1x.com/2020/02/06/1yhBy8.png" alt="1yhBy8.png" border="0" />

如果你来观察其命令行时，会发现有这个警告输出：

<img src="https://s2.ax1x.com/2020/02/06/1y43pq.png" alt="1y43pq.png" border="0" />

仔细思考后，会察觉应该是该包本身的函数`Drawpoint`中应该有些问题。由于该包正在快速迭代开发中，其有些小问题是可以理解的。

但是遇到问题我们就要来查找，通过对程序的调试，发列在`PySimpleGUI`的源代码中`Drawpoint`这个函数在返回时，没有返回所创建的对象`id`，所以造成创建成功后只返回了`None`，于是该对象无法移动，代码截图如下所示：

<img src="https://s2.ax1x.com/2020/02/06/1y4cnO.png" alt="1y4cnO.png" border="0" />

将id的返回值添加上去后，如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1y4XNj.png" alt="1y4XNj.png" border="0" />

再来运行一下程序，就发现问题解决了。

<img src="https://s2.ax1x.com/2020/02/06/1y5MDO.png" alt="1y5MDO.png" border="0" />

# 小结

本篇对`PySimpleGUI`的绘图功能进行了介绍，通过查看源代码我们也可以看到，在`PySimpleGUI`中的`Graph`函数其实也只是对`Canvas`的一种封装，同时遇到问题无须担心，只要**按图索骥**肯定可以找到问题并解决它。