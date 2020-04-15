# LaTeX概览

摘自维基百科：

> LaTeX， 是一种基于TEX的排版系统，由美国电脑学家莱斯利·兰伯特在20世纪80年代初期开发，利用这种格式，即使用户没有排版和程序设计的知识也可以充分发挥由TEX所提供的强大功能，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

简单点说：LaTeX 基于 TeX，主要目的是为了方便排版。在学术界的论文，尤其是数学、计算机等学科论文都是由 LaTeX 编写, 因为用它写数学公式非常漂亮。

**我的一点理解**：

在稍微了解一点 LaTeX 后，你会发现 `LaTeX 的工作方式类似 web page`，都是由源文件（.tex or .html）经由引擎（TeX or browser）渲染产生最终效果（得到 PDF 文件 或者 生成页面）。两者极其神似，包括语法规则与工作方式。所以呢，与 HTML 一样，入门其实很简单。

<img src="https://s2.ax1x.com/2020/02/22/3QaROI.png" alt="3QaROI.png" border="0" />

一般的规范写法中都是在 HTML 文件中写入 web page 的结构与内容，再由 css 控制页面生成的样式。当然你也可以选择在 HTML 中直接写入样式内容，不过这并不提倡。同样，在 LaTeX 有着同样的情况，你可以在 tex 源文件中同时写入内容和样式，也可以内容与样式分离，以网络上流传广泛的 [清华大学 LaTeX 模板](https://github.com/xueruini/thuthesis) 为例，以.cls(class)结尾的 thuthesis.cls 便可看作是与 css 起到同样作用的样式文件。

LaTeX 有所谓宏包的概念，`\usepackage{foo}` 即可使用宏包 foo 中定义的内容。所谓宏包就是一些写好的内容打包出来以便大家使用而已。这跟 C 语言的 `include` 是一致的，将文件加载进来进行使用。利用宏包，我们可以使用很多现成的好用的样式。当然了，如果要编写一个自己的个性化的宏包也是可以的，不过需要学习成本。

初期的话，我们可以选择一个 LaTeX 模板进行改造。不过第一次见到一些模板，可能会对其中很多文件的作用一头雾水. 下面是简单的介绍，详细内容可见在 [LaTeX 中进行文学编程](http://liam0205.me/2015/01/23/literate-programming-in-latex/) ，当然更多介绍的话可以自行搜索。

|LaTeX模板常见文件类型	|功能简要介绍|
|:-:|:-:|
|.dtx|	Documented LaTeX sources，宏包重要部分|
|.ins|	installation，控制 TeX 从 .dtx 文件里释放宏包文件|
|.cfg|	config， 配置文件，可由上面两个文件生成|
|.sty|	style files，使用\usepackage{...}命令进行加载|
|.cls|	classes files，类文件，使用\documentclass{...}命令进行加载|
|.aux|	auxiliary， 辅助文件，不影响正常使用|
|.bst|	BibTeX style file，用来控制参考文献样式|

class 与 style 似乎十分相像，它们在功能上的确很相似，但是也有区别。[这里](https://tug.org/pracjourn/2005-3/asknelly/nelly-sty-&-cls.pdf)  是关于 .cls 与 .sty 文件的区别.

额外推荐阅读材料: 来自北京大学李东风老师的 [LaTeX 排版心得](http://www.math.pku.edu.cn/teachers/lidf/docs/textrick/tricks.pdf) .

# 安装配置LaTeX

LaTeX 配置环境很简单，只需 2 步：

1. 根据平台选择一个 **TeX 发行版** 进行安装，建议选择最全功能最多的版本。
2. 选择一个合适的 **LaTeX 编辑器**。

## 安装Tex发行版

TeX 发行版的概念相当于 Linux 及其发行版，Linux 内核虽然只有一个，但是有很多基于内核的不同特色的 Linux 发行版，Ubuntu，Fedora 等等不胜枚举。

|OS|	TeX Distribution|
|:-:|:-:|
|Windows|	[CTeX](http://www.ctex.org/CTeXDownload)|
|Mac|	[MacTeX](http://tug.org/mactex/)|
|Windows, Linux|	[TeXLive](https://www.tug.org/texlive/)|

> Windows 用户推荐 TeXlive，不推荐 CTeX。

### 1.下载

[官网下载](https://www.latex-project.org/)

<img src="https://s2.ax1x.com/2019/11/10/MKR9Ig.md.png" alt="官网" border="0" /></a>
<img src="https://s2.ax1x.com/2019/11/10/MKRpdS.md.png" alt="Get" border="0" /></a>
<img src="https://s2.ax1x.com/2019/11/10/MK2OxI.md.png" alt="下载" border="0" /></a>
<img src="https://s2.ax1x.com/2019/11/10/MK2qGd.md.png" alt="下载" border="0" /></a>
<img src="https://s2.ax1x.com/2019/11/10/MK2xqf.md.png" alt="下载" border="0" /></a>
<img src="https://s2.ax1x.com/2019/11/10/MK2vsP.md.png" alt="下载" border="0" /></a>

### 2.安装

解压后点击运行程序。

<img src="https://s2.ax1x.com/2019/11/10/MKRwJH.md.png" alt="安装" border="0" /></a>

在线安装三个多G，有点慢，可以做点别的事情。

<img src="https://s2.ax1x.com/2019/11/10/MKR0Wd.md.png" alt="安装" border="0" /></a>

## 安装LaTeX 编辑器

> 建议编辑器安装texstudio。

### 1.下载

[官网下载](http://texstudio.sourceforge.net/)

直接download，然后安装

### 2.使用

修改语言：

`Options`—-`Configure TexStudio…`—-`General`—-`Language`—-`zh_CN`

命令里正常的，如果不一样需要手动修改：

<img src="https://s2.ax1x.com/2019/11/10/MKRbwT.md.png" alt="参数参考" border="0" /></a>

# 开始第一个 LaTeX 文档

打开 TeXstudio，新建一个 TeX 文件，写入以下内容：

```html
\documentclass{article}
\begin{document}
Here comes \LaTeX!
\end{document}
```

点击 `F5`（默认快捷键）`compile and view`（编译并查看），即可看到效果。

<img src="https://s2.ax1x.com/2020/02/22/3QDyM4.png" alt="3QDyM4.png" border="0" />

至此，一个极简易的 LaTeX 文档已经完成。以后要做的事情不过是多用多查，熟能生巧。此外记得找本 LaTeX 的书籍看一下，一来对于更为精细的知识做一个了解，二来可以作为工具书查询。




