---
layout: post
cid: 168
title: [PySimpleGUI界面学习]（十）列表的使用及一个简易计算器例子
slug: 168
date: 2020/02/06 12:48:00
updated: 2020/02/06 12:56:58
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - 界面可视化
---


<!--more-->
# 回顾

在上一篇文章中，我们编写了一个简单的音乐播放器界面和一个脚本执行程序，展示了 `PySimpleGUI` 强大的功能，在这一篇中，我们继续来学习新的控件，并尝试用前面学习的内容编写一个简易计算器程序。

# 列表的使用

列表控件是我们日常用到的较多的一个控件，从表格制作到文件在文件夹中的排列，凡是需要排列的地方，我们总是第一个考虑是否需要一个列表控件来将所展示的数据进行有序化整理。下面这个小例子就展示了这个技术，为了和普通的文本区分开，将两者分别列于同一个窗体上，让读者可以自行对比。

代码如下：

```python
import PySimpleGUI as sg
sg.ChangeLookAndFeel('BlueMono')

col = [[sg.Text('行列 1', text_color='white', background_color='blue')],      
       [sg.Text('行列 2', text_color='white', background_color='blue'), sg.Input('可输入文本框 1')],      
       [sg.Text('行列 3', text_color='white', background_color='blue'), sg.Input('可输入文本框 2')]]      

layout = [[sg.Listbox(values=('Listbox Item 1', 'Listbox Item 2', 'Listbox Item 3'), select_mode=sg.LISTBOX_SELECT_MODE_MULTIPLE, size=(20,3)), sg.Column(col, background_color='blue')],      
          [sg.Input('别担心，这只是一个小测试。')],      
          [sg.OK()]]      

window = sg.Window('列表控件例子').Layout(layout)
event, values = window.Read()  
window.Close()

sg.Popup(event, values, line_width=200)  
```

```html
'OK'
```

其运行图如下所示：

<img src="https://s2.ax1x.com/2020/02/06/1yRoeH.png" alt="1yRoeH.png" border="0" />

当用户点击列表控件中的某一项时，在界面关闭后，程序将弹出一个对话框来显示用户的点击选项，这种方式展示了如何获取列表值：

<img src="https://s2.ax1x.com/2020/02/06/1yR7TA.png" alt="1yR7TA.png" border="0" />

# 一个简易计算器例子

在学习了这么多例子之后，我们来完成一个简易计算器的例子，这个例子可以完成整数的加减乘除运算，具体代码如下：

```python
import PySimpleGUI as sg

def jisuanqi():
    layout = [[sg.Text("计算器")], 
        [sg.InputText(do_not_clear=True, size=(19,3), key="_SHU1_",font=('Helvetica', 20))],
    ]
    #将0~9及加减乘除排列成四行四列
    lst0_9 = [1,2,3,"+",4,5,6,"-",7,8,9,"×","",0,"","÷"]
    tmp_shuzifuhao_lst = []
    for item in lst0_9:
        tmp_shuzifuhao_lst.append(sg.Button(str(item),button_color=('black', 'orange'), size=(4,2),font=('Helvetica', 18)))
        if len(tmp_shuzifuhao_lst) == 4:
            layout.append(tmp_shuzifuhao_lst)
            tmp_shuzifuhao_lst = []
    
    layout.append([sg.Button("计算", button_color=('white', 'springgreen4'), font=('黑体', 16), size=(7,2)), 
        sg.Button("清空",button_color=('white', 'springgreen4'), font=('黑体', 16),size=(7,2)), 
        sg.Button("退出",button_color=('white', 'springgreen4'), font=('黑体', 16),size=(7,2))])

    window = sg.Window("计算器").Layout(layout)

    while True:
        button, values = window.Read()
        if button is None or button=="退出":
            break
        elif button=="清空":
            window.FindElement("_SHU1_").Update("")
        elif button=="计算":
            shu1 = values["_SHU1_"]
            res_str = shu1.replace("×", "*")
            res_str = res_str.replace("÷", "/")
            try:
                result = eval(res_str)
                shu1 += "=" 
                shu1 += str(result)
                window.FindElement("_SHU1_").Update(shu1)
            except:
                window.FindElement("_SHU1_").Update("表达式有误，请查证！")
        else:
            shu1 = values["_SHU1_"]
            if shu1 == "" and (button not in ["+","-","×","÷"]):
                shu1 = button
            elif shu1 == "" and (button in ["+","-","×","÷"]):
                pass
            else:                
                if shu1[-1] in ["+","-","×","÷"] and (button in ["+","-","×","÷"]):
                    pass
                else:
                    shu1 += button
            window.FindElement("_SHU1_").Update(str(shu1))
    window.Close()

jisuanqi()
```

这段代码运行结果如图所示：

<img src="https://s2.ax1x.com/2020/02/06/1yWJXD.png" alt="1yWJXD.png" border="0" />

用户可以点击其中的数字及运算符号进行运算，代码并没有优化，有兴趣的读者可以仔细研究，在这段代码中用到了控件的更新、控件的排列、控件背景的设置等等。


现在为止，界面设计中的一些控件已经介绍了一部分，如果有兴趣，可以到其官方网站查阅相应的文档，下一章节，我们来研究一下菜单的设计。