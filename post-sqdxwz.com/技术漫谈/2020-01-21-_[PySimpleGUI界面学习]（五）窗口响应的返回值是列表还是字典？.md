---
layout: post
cid: 115
title:  [PySimpleGUI界面学习]（五）窗口响应的返回值是列表还是字典？
slug: 115
date: 2020/01/21 19:27:00
updated: 2020/01/21 19:27:59
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

在上一篇文章中我们在最后改进程序时发生了一个意外，即程序在运行时报出了KeyError错误，经过仔细检查，发现在窗口的控件创建时，如果指定了key关键字，那么在引用其返回值时，还用value[0]或value[1]时，就会出错，在本篇文章中，我们将仔细研究一下，界面窗口对于用户的点击在何时采用何种方式来返回。

# 例子1：返回值为列表(list)

```python
import PySimpleGUI as sg
layout = [[sg.Text("姓名"), sg.InputText("浪迹天涯")], [sg.Text("单位"), sg.InputText("天上人间")], [sg.Text("地址"), sg.InputText("四海为家")], [sg.Button("打印")]]
window = sg.Window("测试界面返回值的例子").Layout(layout)
button, values = window.Read()
print(values)
print("类型是{}".format(type(values)))
window.Close()
```

界面显示如下图所示：
<img src="https://s2.ax1x.com/2020/01/21/1kMyCQ.png" alt="1kMyCQ.png" border="0" />

当用户点击打印按钮时，程序将在命令窗口上打印出窗体上输入控件中的内容，并打印该返回值的类型。

从打印可以看出，此时程序对于用户的点击响应返回值为list类型，根据以前学过的知识可以知道，对于list类型中元素的引用需要以其序列来索引，即可以用values[0]、value[1]来获取。

# 例子2：返回值为字典(dict)

回顾上一篇文章最后的例子中，我们采用了value["_SHU1_"]、value["_SHU2_"]这样的形式来获取用户的输入值，这种是典型的字典(dict)引用方式。将上述例子稍做改动，做为例子2：

```python
import PySimpleGUI as sg
layout = [[sg.Text("姓名"), sg.InputText("浪迹天涯",key="_NAME_")], [sg.Text("单位",), sg.InputText("天上人间", key="_UNIT_")], [sg.Text("地址"), sg.InputText("四海为家", key="_ADDRESS_")], [sg.Button("打印")]]
window = sg.Window("测试界面返回值的例子").Layout(layout)
button, values = window.Read()
print(values)
print("类型是{}".format(type(values)))
window.Close()
```

这段代码的界面显示与上一个完全相同，所不同的是打印的结果不一样：

<img src="https://s2.ax1x.com/2020/01/21/1kQVVf.png" alt="1kQVVf.png" border="0" />

从上图的打印结果可以看出，这一次返回值的类型已经变成了字典(dict)类型。

# 小结

从上面两个小例子可以看出，当你给程序中的控件指定了关键字标识时，界面对用户行为的返回值是以字典(dict)的形式给出，而当用户不加任何key关键字时，界面对于用户行为的返回值是列表(list)。

在学习了这么多之后，有人可能会问，为什么做一个加法器时，输入框这么长呢，能不能缩短一些呢？比如原来竟然是这么长：

答案当然是可以啦，只需要在创建控件时加入size这个参数即可，于是上一篇最后一个小程序可修改为：

```python
import PySimpleGUI as sg
layout = [[sg.Text("加法器")], [sg.InputText(size=(10,1),do_not_clear=True, key="_SHU1_"), sg.Text("+"), sg.InputText(size=(10,1), do_not_clear=True, key="_SHU2_"),sg.Text("="), sg.Text("", key="_RESULT_")], [sg.Button("计算"),sg.Button("清空"), sg.Button("退出")]]
window = sg.Window("加法器").Layout(layout)
while True:
    button, values = window.Read()
    if button is None or button == "退出":
        break
    elif button=="清空":
        window.FindElement("_SHU1_").Update("")
        window.FindElement("_SHU2_").Update("")
        window.FindElement("_RESULT_").Update("")
    else:
        tmp_a = eval(values["_SHU1_"])
        tmp_b = eval(values["_SHU2_"])
        tmp_result = tmp_a+tmp_b
        window.FindElement("_RESULT_").Update(str(tmp_result))
window.Close()
```

运行结果如图所示：

<img src="https://s2.ax1x.com/2020/01/21/1kQNiF.png" alt="1kQNiF.png" border="0" />

