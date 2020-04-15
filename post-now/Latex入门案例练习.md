# Latex入门案例

## 输出一句话

```latex
\documentclass{article}
\begin{document}
	hello, world
\end{document}
```

## 标题、作者和注释

```latex
\documentclass{article}
\author{My Name}
\title{The Title}
\begin{document}
\maketitle
hello, world % This is comment
\end{document}
```

## 章节和段落

```latex
\documentclass{article}
\title{Hello World}
\begin{document}
\maketitle
\section{Hello China} China is in East Asia.
\subsection{Hello Beijing} Beijing is the capital of China.
\subsubsection{Hello Dongcheng District}
\paragraph{Tian'anmen Square}is in the center of Beijing
\subparagraph{Chairman Mao} is in the center of Tian'anmen Square
\subsection{Hello Guangzhou}
\paragraph{Sun Yat-sen University} is the best university in Guangzhou.
\end{document}
```

## 加入目录

```latex
\documentclass{article}
\begin{document}
\tableofcontents
\section{Hello China} China is in East Asia.
\subsection{Hello Beijing} Beijing is the capital of China.
\subsubsection{Hello Dongcheng District}
\paragraph{Hello Tian'anmen Square}is in the center of Beijing
\subparagraph{Hello Chairman Mao} is in the center of Tian'anmen Square
\end{document}
```

## 换行

```latex
\documentclass{article}
\begin{document}
Beijing is
the capital
of China.

New York is

the capital

of America.

Amsterdam is \\ the capital \\
of Netherlands.
\end{document}
```

## 数学公式

```latex
\documentclass{article}
\usepackage{amsmath}
\usepackage{amssymb}
\begin{document}
The Newton's second law is F=ma.

The Newton's second law is $F=ma$.

The Newton's second law is
F=ma


The Newton's second law is
F=ma


Greek Letters $\eta$ and $\mu$

Fraction $\frac{a}{b}$

Power $a^b$

Subscript $a_b$

Derivate $\frac{\partial y}{\partial t} $

Vector $\vec{n}$

Bold $\mathbf{n}$

To time differential $\dot{F}$

Matrix (lcr here means left, center or right for each column)
\[
\left[
\begin{array}{lcr}
a1 & b22 & c333 \\
d444 & e555555 & f6
\end{array}
\right]
\]

Equations(here \& is the symbol for aligning different rows)
\begin{align}
a+b&=c\\
d&=e+f+g
\end{align}

\[
\left\{
\begin{aligned}
&a+b=c\\
&d=e+f+g
\end{aligned}
\right.
\]

\end{document}
```

## 插入图片

> 先搜索到一个将图片转成eps文件的软件，然后将图片保存为一个名字如figure1.eps。

```latex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics[width=4.00in,height=3.00in]{figure1.eps}
\end{document}
```

## 简单表格

```latex
\documentclass{article}
\begin{document}
\begin{tabular}{|c|c|}
a & b \\
c & d\\
\end{tabular}

\begin{tabular}{|c|c|}
\hline
a & b \\
\hline
c & d\\
\hline
\end{tabular}

\begin{center}
\begin{tabular}{|c|c|}
\hline
a & b \\ \hline
c & d\\
\hline
\end{tabular}
\end{center}
\end{document}
```

# 拓展知识

## 1.中文支持

曾经的LaTeX的中文支持是比较麻烦的一件事，但是现在使用MikTeX+WinEdt的中文支持非常容易。只需要把开头的`\documentclass{atricle}`换成`\documentclass{ctexart}`就可以了。如果是第一次使用`ctexart`的话，会自动下载和安装宏包和模板，之后就不会再下载了。
例子参考如下：

```html
\documentclass{ctexart}
\begin{document}
你好，世界
\end{document}
```

## 2.宏包

`\package{}`就是在`调用宏包`，对计算机实在外行的同学姑且可以理解为工具箱。
每一个宏包里都定义了一些专门的命令，通过这些命令可以实现对于一类对象（如数学公式等）的统一排版（如字号字形），或用来实现一些功能（如插入图片或制作复杂表格）。
通常在`\documentclass`之后，在`\begin{document}`之前，将文章所需要涉及的宏包都罗列上。

对于新人而言比较常用的宏包有：

- 编辑数学公式的宏包：`\usepackage{amsmath}`和 `\usepackage{amssymb}`
- 编辑数学定理和证明过程的宏包：`\usepackage{amsthm}`
- 插入图片的宏包：`\usepackage{graphicx}`
- 复杂表格的宏包：`\usepackage{multirow}`

## 3.模板

模板就是在`\documentclass{}`后面的大括号里的内容。

在这一份教程中，我们使用的是LaTeX默认自带的模板`article`，以及中文模板`ctexart`。

模板就是实现我之前所介绍的LaTeX的经验总结的第二点的实现方式。

一篇文章，我们定义了`section`，定义了`paragraph`，就是没有定义字体字号，因为字体字号这一部分通常来说是在模板中实现的。

一个模板可以规定，`section`这个层级都用什么字体什么字号怎么对齐，`subsection`这个层级用什么字体什么字号怎么对齐，`paragraph`又用什么字体什么字号怎么对齐。

当然模板里还可以包含一些自定义的口令，以及页眉页脚页边距一类的页面设置。

由于模板的使用，在我的使用经验里来看，绝对不可能算是基本入门级的内容，所以在正文里当然不会提及。

如果有人实在想学，如果LaTeX已经接触到这个程度上了，那么再去翻其他厚一些的教材，也不亏了。

## 4.参考文献和制作幻灯片

做参考文献的时候，文章也已经快写到尾声了，而幻灯片更不是进阶一些的需求。对这两个功能有需求的LaTeX user，使用LaTeX也已经相当熟练了，自己去google一下或查阅其他厚教程是很理所当然的，一点也不冤枉。

在此我就只提供两个搜索关键词，**参考文献**可以搜`bibtex`，**制作幻灯片**可以搜`beamer`。

# 学习资源

1. [中文LaTeX安装与使用](http://aff.whu.edu.cn/huangzh/中文LaTeX安装与使用.pdf)
2. [黄正华](http://aff.whu.edu.cn/huangzh/)
3. [LaTeX 中文模版收集](https://github.com/netspaces/LaTeX-Template-Cn)
4. [国外LaTex模板网站](http://www.latextemplates.com/)
5. [LATEX排版心得-北京大学李东风](http://www.math.pku.edu.cn/teachers/lidf/docs/textrick/tricks.pdf)
6. [LaTex文档](http://www.ctex.org/OnlineDocuments)
7. [bibTeX生成参考文献](http://aff.whu.edu.cn/huangzh/bibTeX生成参考文献.pdf)





















