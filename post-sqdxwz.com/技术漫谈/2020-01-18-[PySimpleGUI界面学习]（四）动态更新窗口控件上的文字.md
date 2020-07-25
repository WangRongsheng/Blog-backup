---
layout: post
cid: 98
title: [PySimpleGUI界面学习]（四）动态更新窗口控件上的文字
slug: 98
date: 2020/01/18 13:15:05
updated: 2020/01/18 13:15:05
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

上一篇文章在最后实战了一个小程序，这个小程序的功能是实现两数相加并将结果显示在命令窗口，目前看来，这当然只是一个过渡产品，界面编程的要求是要将所有数据在界面上表现出来，这样不仅仅出于一致性的考虑，更重要的是，这是界面编程的意义所在。

为了方便起见，现将上一篇教程中的代码抄录如下:

```python
import PySimpleGUI as sg
layout = [[sg.Text("加法器")], [sg.InputText(), sg.Text("+"), sg.InputText(),sg.Text("=")], [sg.Button("计算"), sg.Button("退出")]]
window = sg.Window("加法器").Layout(layout)
while True:
    button, values = window.Read()
    if button is None or button == "退出":
        break
    else:
        tmp_a = eval(values[0])
        tmp_b = eval(values[1])
        print("%s与%s和是%s" % (tmp_a, tmp_b, eval(tmp_a)+eval(tmp_b)))
window.Close()
```

# 进化

为了让程序计算结果显示在界面上，需要引入控件的一个方法Update，该方法的功能是用新的字符串来替代原控件上的字符串，但是应该在哪里来显示这个结果呢？

聪明的读者应该能很快想到好办法，这里只是简单在=号后面添加一个Text控件，首先将该控件上显示为空，待结果计算出来后，立刻将结果在该控件上显示就好了。

可是，新的问题又来了，在用户没有点击到这个控件时候，程序在运行时如何知道这个控件呢？

嗯，在PySimpleGUI工具包中，Window这个窗口类提供了一个查找控件的方法FindElement，但是这个方法需要依照一个关键字，所以，我们的办法就出来了，即给新增的标签控件增加一个新的关键字就好：

```python
sg.Text("", key="_RESULT_")
```
上面代码中的_RESULT_就是为FindElement方法提供的关键字，在程序运行时通过以下语句来实现查找：

```python
window.FindElement('_RESULT_')
```

这样就可以找到了我们需要更新其显示的标签控件。

整体代码如下：

```python
import PySimpleGUI as sg
layout = [[sg.Text("加法器")], [sg.InputText(), sg.Text("+"), sg.InputText(),sg.Text("="), sg.Text("", key="_RESULT_")], [sg.Button("计算"), sg.Button("退出")]]
window = sg.Window("加法器").Layout(layout)
while True:
    button, values = window.Read()
    if button is None or button == "退出":
        break
    else:
        tmp_a = eval(values[0])
        tmp_b = eval(values[1])
        tmp_result = tmp_a+tmp_b
        window.FindElement("_RESULT_").Update(str(tmp_result))
window.Close()
```

细心的人可以将两次代码仔细对比，自然会发现其中的不一样之处。

# 继续进化

等等，在我们运行上述程序后，会出现一个界面，但是当我们输入两个加数，再点击计算按钮时，结果是计算出来了，但是两个加数的输入框却被清空了，那么能不能在运算结束时还将两个加数输入框中的数字保留下来呢？

答案当然是可以，而且很简单，只需要在创建的两个加数文本框中添加一个do_not_clear的标识即可，默认情况下，该标识是False，即界面只要读取一次用户点击，即将当前文本框清空，倘若不想清空，只需要将该标识设置为True即可：

```python
sg.InputText(do_not_clear=True)
```

修正后的代码如下：

```python
import PySimpleGUI as sg
layout = [[sg.Text("加法器")], [sg.InputText(do_not_clear=True), sg.Text("+"), sg.InputText(do_not_clear=True),sg.Text("="), sg.Text("", key="_RESULT_")], [sg.Button("计算"), sg.Button("退出")]]
window = sg.Window("加法器").Layout(layout)
while True:
    button, values = window.Read()
    if button is None or button == "退出":
        break
    else:
        tmp_a = eval(values[0])
        tmp_b = eval(values[1])
        tmp_result = tmp_a+tmp_b
        window.FindElement("_RESULT_").Update(str(tmp_result))
window.Close()
```

运行结果如下：
<img src="https://s2.ax1x.com/2020/01/18/1pZqhT.png" alt="1pZqhT.png" border="0" />

# 如何更加完美

程序现在已经按照我们的意思完美运行，但是在计算完一道题目后，如何将这些已经填入的数据和计算的数据清空呢？

这时候就可以使用 '清除' 按钮了

代码如下：

```python
import PySimpleGUI as sg
layout = [[sg.Text("加法器")], [sg.InputText(do_not_clear=True, key="_SHU1_"), sg.Text("+"), sg.InputText(do_not_clear=True, key="_SHU2_"),sg.Text("="), sg.Text("", key="_RESULT_")], [sg.Button("计算"),sg.Button("清空"), sg.Button("退出")]]
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

仔细观察上述代码，你会发现许多不同的地方，尤其是返回值的引用，如果你没有按照上述代码来运行，只是更新一下原来的代码的话，会报出一个KeyError，这就是引入了关键字key后的一个小变化。

<img src="https://s2.ax1x.com/2020/01/18/1peQ4f.png" alt="1peQ4f.png" border="0" />