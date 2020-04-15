# 简介

小学、中学有没有因为一个知识点犯错了多次被罚抄呢？有没有每次都是心里爆炸？本以为上了大学就再也不会有罚写，可是每次几千字的小论文是不是也是崩溃的？但是还好有时候可以使用电子文档，去百度`CV`就好了，但是你的老师有没有告诉你：**同学们务必要手写哦，不允许电子档！** ，心中一万句不服气...，今天就来用Word的多种字体来搭配一个我们自己的手写体吧，希望下次可以蒙混过关耶~

# 使用

## 准备工作

1. 字体下载
   
| 字体 | 下载链接 |
|:-:|:-:|
|陈静的字完整版|[下载](https://www.lanzous.com/i9rp86f)|
|李国夫手写字体|[下载](https://www.lanzous.com/i9rp8dc)|
|萌子字体(6000字)|[下载](https://www.lanzous.com/i9rp8va)|

> 在这里提供我使用的三种字体，其它手写字体可以自行百度下载~

2. `宏`代码

```vb
Sub 字体修改()
'
' 字体修改 宏
'
    Dim R_Character As Range


    Dim FontSize(5)
    ' 字体大小在5个值之间进行波动，可以改写
    FontSize(1) = "21"
    FontSize(2) = "21.5"
    FontSize(3) = "22"
    FontSize(4) = "22.5"
    FontSize(5) = "23"



    Dim FontName(3)
    '字体名称在三种字体之间进行波动，可改写，但需要保证系统拥有下列字体
    FontName(1) = "陈静的字完整版"
    FontName(2) = "萌妹子体"
    FontName(3) = "李国夫手写体"

    Dim ParagraphSpace(5)
    '行间距 在一定以下值中均等分布，可改写
    ParagraphSpace(1) = "12"
    ParagraphSpace(2) = "13"
    ParagraphSpace(3) = "20"
    ParagraphSpace(4) = "7"
    ParagraphSpace(5) = "12"

    '不懂原理的话，不建议修改下列代码

    For Each R_Character In ActiveDocument.Characters

        VBA.Randomize

        R_Character.Font.Name = FontName(Int(VBA.Rnd * 3) + 1)

        R_Character.Font.Size = FontSize(Int(VBA.Rnd * 5) + 1)

        R_Character.Font.Position = Int(VBA.Rnd * 3) + 1

        R_Character.Font.Spacing = 0


    Next

    Application.ScreenUpdating = True



    For Each Cur_Paragraph In ActiveDocument.Paragraphs

        Cur_Paragraph.LineSpacing = ParagraphSpace(Int(VBA.Rnd * 5) + 1)


    Next
        Application.ScreenUpdating = True


End Sub
```

## 开始使用

1. 下载字体后，直接双击`.ttf文件`安装字体就可以了；
2. 新建一个`word文档`，把正常的文字或者文章写好；
3. 打开`宏`，`新建一个宏命令`，并将我们`准备的代码完整填进去`；

> 注意：宏代码中的`字号`、`字体`等你还可以根据自己的需求更改！

4. 点击`运行`，保存就ok了；

> 如果不满意就要好好微调下哦，完全可以很像我们自己手写的字。

# 效果

## 原始文章

<img src="https://s2.ax1x.com/2020/02/28/3D7UfK.png" alt="QQ截图20200228174851" border="0">

## 修改后文章

<img src="https://s2.ax1x.com/2020/02/28/3D7JT1.png" alt="QQ截图20200228174754" border="0">

# 推荐

1. [手迹造字](http://www.myfont.me/)
2. [Handright](https://github.com/Gsllchb/Handright)
3. [手写体-中文字库自动生成系统](http://www.flexifont.com/flexifont-chn/login/)


