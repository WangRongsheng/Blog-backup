---
title: jupyter拓展功能
date: 2019-10-29 06:52:14
thumbnail: https://i.loli.net/2019/10/29/QJDseUELd8HpZo3.png
tags: Jupyter拓展
categories: Python
---

之前我曾经在我的笔记-[JUpyter使用方法](https://zzdproject.netlify.com/#/jupyter) 中谈到多种jupyter的使用方法，但是这几天我又发现了一些新的拓展功能，所以特意总结在这篇文章里。

<!--more-->

目录：

1. Pandas Profiling
2. 使用Cufflinks和Plotly绘制Pandas数据
3. Jupyter 中的格式编排
4. 在 Jupyter（或 IPython）中使一个单元同时有多个输出
5. 为 Jupyter Notebook 即时创建幻灯片

## 1.Pandas Profiling

使用该工具只需安装和导入 Pandas Profiling 包。

本文不再详述这一工具，如欲了解更多，请阅读：https://towardsdatascience.com/exploring-your-data-with-just-1-line-of-python-4b35ce21a82d

## 2.使用Cufflinks和Plotly绘制Pandas数据

使用python的人大多对 matplotlib 和 pandas 很熟悉。也就是说，你只需调用 .plot() 方法，即可快速绘制简单的 pd.DataFrame 或 pd.Series。

这已经很好了，不过是否可以绘制一个交互式、可缩放、可扩展的全景图呢？是时候让 Cufflinks\* \*出马了！（Cufflinks 基于 Plotly 做了进一步的包装。）

对于Plotly我已经发过一次教程在：[Plotly教程](https://github.com/WangRongsheng/Python-Plotly_jupyter-notebook)

在环境中安装 Cufflinks，只需在终端中运行**!pip install cufflinks --upgrade** 即可。

其他更多的使用方法请参见文档

- Cufflinks 文档：https://plot.ly/ipython-notebooks/cufflinks/
- Plotly 文档：https://plot.ly/

## 3.Jupyter 中的格式编排

一些常用的格式：

（1）蓝色、时尚：

```html
<div class="alert alert-block alert-info">
  This is <b>fancy</b>!
</div>
```

（2）红色、轻微慌张：

```html
<div class="alert alert-block alert-danger"> 
  This is <b>baaaaad</b>!
</div>
```

（3）绿色、平静：

```html
<div class="alert alert-block alert-success">
 This is <b>gooood</b>!
</div>
```

效果：

<center>
<a href="https://sm.ms/image/vhqEeZ6yo1bJniS" target="_blank"><img src="https://i.loli.net/2019/10/29/vhqEeZ6yo1bJniS.gif" ></a>
</center>

## 4.在 Jupyter（或 IPython）中使一个单元同时有多个输出

想展示 pandas DataFrame 的 .head() 和 .tail()，但由于创建运行 .tail() 方法的额外代码单元过于麻烦而不得不中途放弃，你是否有过这样的经历？现在不用怕了，你可以使用以下代码行展示你想展示的输出：

```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

## 5.为 Jupyter Notebook 即时创建幻灯片

使用**RISE** ，你可以仅通过一次按键将 Jupyter Notebook 即时转变为幻灯片。而且 notebook 仍然处于活跃状态，你可以在展示幻灯片的同时执行实时编码！

要想使用该工具，你只需通过 conda 或 pip 安装 RISE 即可。

```html
conda install -c conda-forge rise
或者
pip install RISE
```

现在，你可以点击新按钮，为 notebook 创建不错的幻灯片了：

<a href="https://sm.ms/image/WJejhYXlLkZzPFp" target="_blank"><img src="https://i.loli.net/2019/10/29/WJejhYXlLkZzPFp.jpg" ></a>
