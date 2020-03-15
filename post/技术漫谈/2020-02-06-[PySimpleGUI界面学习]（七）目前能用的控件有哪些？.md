---
layout: post
cid: 165
title: [PySimpleGUI界面学习]（七）目前能用的控件有哪些？
slug: 165
date: 2020/02/06 12:20:00
updated: 2020/02/06 12:21:12
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

上一篇文章中我们实现了一个文件浏览对话框，从程序来看，核心代码只有一句，即：

```python
event, values = sg.Window("我的脚本对话框").Layout([[sg.Text("打开文档")], 
        [sg.Input(), sg.FileBrowse()], [sg.Button("打开"), sg.Button("退出")]]).Read()
```
但是为了能使程序能够在命令行也可以执行，所以引入了  `sys` 这个包来检测用户的输入信息。

# 探索

目前为止，我们已经接触到的窗口控件有 `Text` 、`InputText` 、 `Button` 、`FileBrowse` 等，但是对于大量复杂的任务而言，只有这几个控件不足以完成任务，所以一般情况下，任何一个比较成熟的界面工具包都提供许多大同小异的控件，比如列表框、比如表格控件、比如进度条等等，这一篇我们就来探索一下目前PySimpleGUI已经将多少标准控件调用方式转换完成。

下面我们将粘贴一段 `PySimpleGUI` 网站中的一段代码来做一个简略演示：

```python
#!/usr/bin/env Python3      
# import PySimpleGUIQt as sg      
import PySimpleGUI as sg      

sg.ChangeLookAndFeel('GreenTan')      

# ------ Menu Definition ------ #      
menu_def = [['File', ['Open', 'Save', 'Exit', 'Properties']],      
            ['Edit', ['Paste', ['Special', 'Normal', ], 'Undo'], ],      
            ['Help', 'About...'], ]      

# ------ Column Definition ------ #      
column1 = [[sg.Text('Column 1', background_color='#F7F3EC', justification='center', size=(10, 1))],      
            [sg.Spin(values=('Spin Box 1', '2', '3'), initial_value='Spin Box 1')],      
            [sg.Spin(values=('Spin Box 1', '2', '3'), initial_value='Spin Box 2')],      
            [sg.Spin(values=('Spin Box 1', '2', '3'), initial_value='Spin Box 3')]]      

layout = [      
    [sg.Menu(menu_def, tearoff=True)],      
    [sg.Text('All graphic widgets in one window!', size=(30, 1), justification='center', font=("Helvetica", 25), relief=sg.RELIEF_RIDGE)],    
    [sg.Text('Here is some text.... and a place to enter text')],      
    [sg.InputText('This is my text')],      
    [sg.Frame(layout=[      
    [sg.Checkbox('Checkbox', size=(10,1)),  sg.Checkbox('My second checkbox!', default=True)],      
    [sg.Radio('My first Radio!     ', "RADIO1", default=True, size=(10,1)), sg.Radio('My second Radio!', "RADIO1")]], title='Options',title_color='red', relief=sg.RELIEF_SUNKEN, tooltip='Use these to set flags')],      
    [sg.Multiline(default_text='This is the default Text should you decide not to type anything', size=(35, 3)),      
        sg.Multiline(default_text='A second multi-line', size=(35, 3))],      
    [sg.InputCombo(('Combobox 1', 'Combobox 2'), size=(20, 1)),      
        sg.Slider(range=(1, 100), orientation='h', size=(34, 20), default_value=85)],      
    [sg.InputOptionMenu(('Menu Option 1', 'Menu Option 2', 'Menu Option 3'))],      
    [sg.Listbox(values=('Listbox 1', 'Listbox 2', 'Listbox 3'), size=(30, 3)),      
        sg.Frame('Labelled Group',[[      
        sg.Slider(range=(1, 100), orientation='v', size=(5, 20), default_value=25),      
        sg.Slider(range=(1, 100), orientation='v', size=(5, 20), default_value=75),      
        sg.Slider(range=(1, 100), orientation='v', size=(5, 20), default_value=10),      
        sg.Column(column1, background_color='#F7F3EC')]])],      
    [sg.Text('_'  * 80)],      
    [sg.Text('Choose A Folder', size=(35, 1))],      
    [sg.Text('Your Folder', size=(15, 1), auto_size_text=False, justification='right'),      
        sg.InputText('Default Folder'), sg.FolderBrowse()],      
    [sg.Submit(tooltip='Click to submit this window'), sg.Cancel()]    
]      


window = sg.Window('Everything bagel', default_element_size=(40, 1), grab_anywhere=False).Layout(layout)      

event, values = window.Read()      

sg.Popup('Title',      
            'The results of the window.',      
            'The button clicked was "{}"'.format(event),      
            'The values are', values)  
```

这段代码运行后的结果如下图所示： 

<img src="https://s2.ax1x.com/2020/02/06/1yrY34.png" alt="1yrY34.png" border="0" />

从运行结果来看，这里用到了菜单、滚动条、复选框等，其用法也都比较简单，愿意用的同学可以仔细阅读一下代码即可。

# 实战

在学习了这许多内容后，我们来做一个计时器小程序，这个程序很简单，当用户开始运行时，在界面窗口中用 `Text` 控件将时间按分、秒、毫秒的方式展现，需要注意的是，这个小程序是不断刷新界面的。具体代码如下:

```python
import PySimpleGUI as sg 
layout = [[sg.Text("计时器", size=(20,2), justification="center")],
            [sg.Text("", size=(10,2), font=("宋体", 20), justification="center", key="_OUTPUT_")],
            [sg.Text(" "*5), sg.Button("启动/停止", focus=True), sg.Button("退出")]]
window = sg.Window("计时器").Layout(layout)

timer_running = True
i = 0
while True:
    i += 1 * (timer_running is True)
    event, values = window.Read(timeout=10)
    if event is None or event == "退出":
        break
    elif event == "启动/停止":
        timer_running = not timer_running
    window.FindElement('_OUTPUT_').Update('{:02d}:{:02d}:{:02d}'.format(i//100//60, (i//100)%60, i%100))

window.Close()
```

这段代码是模拟一个计时器，并不是真实的计时器，因为只是用一个循环变量简单模拟，不同的电脑运行会感觉每秒时长有问题，有兴趣的同学可以引入time时间包进行细化。具体界面如下： 

<img src="https://s2.ax1x.com/2020/02/06/1ysC24.png" alt="1ysC24.png" border="0" />