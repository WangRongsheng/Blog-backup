---
layout: post
cid: 167
title:  [PySimpleGUI界面学习]（九）媒体播放器界面及脚本执行器
slug: 167
date: 2020/02/06 12:46:34
updated: 2020/02/06 12:46:34
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

在上一篇文章中研究了 `PySimpleGUI` 中回调的模拟以及一个小例子。在这一篇中，我们仍然通过几个例子来进一步说明利用 `PySimpleGUI` 进行开发的一些技术。

# 一个媒体播放器界面的开发

媒体播放器一般要放置一些图片按钮在界面上，这样会使界面显得更加生动一些，这个例子展示了如何在一个按钮上放置图片的例子，具体代码如下：

```python
import PySimpleGUI as sg
def MediaPlayerGUI():
    background = '#F0F0F0'
    sg.SetOptions(background_color=background, element_background_color=background)
    image_pause = './pause.png'
    image_restart = './prev.png'
    image_next = './next.png'
    image_exit = './exit.png'
    layout= [[sg.Text('Media File Player',size=(17,1), font=("Helvetica", 25))],
             [sg.Text('', size=(15, 2), font=("Helvetica", 14), key='output')],
             [sg.Button('', button_color=(background,background),
                image_filename=image_restart, image_size=(50, 50), image_subsample=2, border_width=0, key='Restart Song'),
              sg.Text(' ' * 2),
              sg.Button('', button_color=(background,background),
                image_filename=image_pause, image_size=(50, 50), image_subsample=2, border_width=0, key='Pause'),
              sg.Text(' ' * 2),
              sg.Button('', button_color=(background,background), 
                image_filename=image_next, image_size=(50, 50), image_subsample=2, border_width=0, key='Next'), 
              sg.Text(' ' * 2),
              sg.Button('', button_color=(background,background),
                image_filename=image_exit, image_size=(50, 50), image_subsample=2, border_width=0, key='Exit')],
            [sg.Text('_'*20)],
            [sg.Text(' '*30)],
            [
             sg.Slider(range=(-10, 10), default_value=0, size=(10, 20), orientation='vertical', font=("Helvetica", 15)),
             sg.Text(' ' * 2),
             sg.Slider(range=(-10, 10), default_value=0, size=(10, 20), orientation='vertical', font=("Helvetica", 15)),
             sg.Text(' ' * 2),
             sg.Slider(range=(-10, 10), default_value=0, size=(10, 20), orientation='vertical', font=("Helvetica", 15))],
             [sg.Text('   Bass', font=("Helvetica", 15), size=(9, 1)),
             sg.Text('Treble', font=("Helvetica", 15), size=(7, 1)),
             sg.Text('Volume', font=("Helvetica", 15), size=(7, 1))]
             ]
    window = sg.Window('Media File Player', auto_size_text=True, default_element_size=(20, 1),
                       font=("Helvetica", 25)).Layout(layout)
    while(True):
        event, values = window.Read(timeout=100)        # Poll every 100 ms
        if event == 'Exit' or event is None:
            break
        if event != sg.TIMEOUT_KEY:
            window.FindElement('output').Update(event)

MediaPlayerGUI()
```

关于以上媒体播放器的代码中，需要注意的有以下几个问题：一是所用的图片要注意用 `png` 格式，如果用的是`jpg` 格式，会报错。二是在各个按钮之间以空的Text来填充，这样从视觉上会有分开的效果，三是在用户点击按钮后，会将按钮的key更新显示在提前定义好的 `Text` 上，具体运行如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1y2NvD.png" alt="1y2NvD.png" border="0" />

这个例子的代码没有什么新的东西，主要是在按钮上如何放置一个图片，因为图片是圆形按钮，为了更好地显示该圆形图案，就将背景统一设置为一种颜色，这样就会使该图片的四周与周边图形融为一体。需要注意的是在图片设置中 `image_subsample` 属性的设置，该变量设置越小，图片在界面上就会显示越大，有兴趣的同学可以自行测试。

# 脚本启动器

再来一个例子，在这个例子中，我们来制作一个脚本启动器，即用界面来提供一个输入框，让用户在其中键入相应的系统命令，然后由程序来调用执行该命令，并将该命令的结果返回在界面上，有点替代 `CMD` 窗口的感觉，相当酷，而且很简单，代码如下：

```python
import PySimpleGUI as sg 
import subprocess

def ExecuteCommand(command, *args):
    try:
        sp = subprocess.Popen([command, *args], shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        out, err = sp.communicate()
        if out:
            print(out.decode("gbk"))
        if err:
            print(err.decode("gbk"))
    except:
        print("所输入的命令无法有效执行!")

layout = [
    [sg.Text("脚本输出...", size=(40,1))],
    [sg.Output(size=(88,20), key="_OUTPUT_")],
    [sg.Button("脚本1"), sg.Button("脚本2"), sg.Button("退出")],
    [sg.Text("命令：",size=(15,1)), sg.InputText(focus=True), sg.Button("运行",bind_return_key=True)]
]

window = sg.Window("脚本执行器").Layout(layout)

while True:
    event, values = window.Read()
    if event is None or event == "退出":
        break
    if event == "脚本1":
        ExecuteCommand('pip', 'list')
        # window.FindElement("_OUTPUT_").clear()
    elif event == "脚本2":
        ExecuteCommand("python", "--version")
    elif event == "运行":
        cmdtmp = values[0]
        cmdtmp = cmdtmp.split(" ")
        if len(cmdtmp) == 2:
            ExecuteCommand(cmdtmp[0],cmdtmp[1])
        elif len(cmdtmp) == 1:
            ExecuteCommand(cmdtmp[0])
        else:
            print("所输入的命令超过可执行能力，请输入'pip list'类似样式的命令！")

window.Close()
```

以上的代码运行如下图所示：

<img src="https://s2.ax1x.com/2020/02/06/1y2bxU.png" alt="1y2bxU.png" border="0" />

对于这个简单的程序需要说明的是，为了将命令执行的结果输出到界面的 `Output` 控件，引入了 `subprocess` 这个标准包，该包主要利用管道技术将程序的输出和错误返回管道中，之后方便在程序中使用，因为界面包中将` Output`默认定义了输出，所以在该程序中所有的`print`语句自动将结果打印输出至该控件中。需要注意的是在`windows`下需要将信息以`gbk`方式解码，在`linux`下要以`utf-8`方式解码。

对于`subprocess`这个包的解释已经超过本篇文件的内容范畴，只是为方便理解，需要提一点：对于操作系统的任何命令，操作系统通常是有三个部分在联动，一是`stdin`，即输入，二是`stdout`即输出，三是`stderr`即错误报警，在这个包中，利用`subprocess`的`Popen`命令执行完后，结果放在其`PIPE`中，需要以标准的输出来获取其内容，而`communicate`这个函数就可以将刚才的命令执行结果返回，当然只需要返回`stdout`和`stderr`即可。关于这部分的详细内容，请阅读相关操作系统的书籍。

# 小结

在本篇文章中，用两个小例子进一步介绍了界面编程的一些内容，同时结合一些Python常用工具包完成一些日常需要用到的功能，请细心的读者仔细体会。