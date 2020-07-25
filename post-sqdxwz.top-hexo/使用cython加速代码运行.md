---
title: 使用cython加速代码运行
date: 2019-09-10 17:09:22
thumbnail: https://i.loli.net/2019/09/17/qlg39NeOJaR4sMp.png
tags: cython
categories: Python
---

# 引入

毫无疑问，Python是社区最喜爱的编程语言!到目前为止，它是最容易使用的语言之一，因为python代码是用一种直观的、人类可读的方式编写的。

然而，你经常会反复听到一些对Python的抱怨，尤其是来自C语言爱好者的抱怨，这些抱怨无非就是Python很慢。

<!--more-->

是的，他们并没有说错。

与许多其他编程语言相比，Python确实很慢。Benchmark game有一些比较不同编程语言在不同任务上的速度的可靠基准。

> https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/gpp-python3.html?source=post_page

对于Python，我们有几种不同的方法可以加快速度:

> 1.使用多进程库来使用所有的CPU核心
https://towardsdatascience.com/heres-how-you-can-get-a-2-6x-speed-up-on-your-data-pre-processing-with-python-847887e63be5
2.如果你使用Numpy、panda或Scikit-Learn，使用Rapids来加速GPU上的处理。
https://towardsdatascience.com/heres-how-you-can-accelerate-your-data-science-on-gpu-4ecf99db3430

如果你所做的实际上可以并行化，比如数据预处理或矩阵运算，这些都是很好的方法。

但是如果你的代码是纯Python的呢?如果你不得不使用一个很大的for循环，且不能将数据放入矩阵中，因为数据必须按顺序处理，那会怎样?有没有办法加快Python本身的速度呢?

答案是肯定的，**这就是Cython来加速原生Python代码的地方**。

# 什么是Cython？

Cython是Python和C/C++之间的一个中间步骤。它允许你编写纯Python代码，并且只需要做一些小修改，然后将其直接翻译成C代码。

你对Python代码所做的惟一调整就是向每个变量添加类型信息。通常，我们可以像这样在Python中声明一个变量:
```python
x = 5
```
使用Cython，我们将向该变量添加一个类型:
```python
cdef int x = 5
```
这告诉Cython，我们的变量是浮点类型，就像我们在C中所做的一样。对于纯Python，变量的类型是动态确定的。Cython中类型的显式声明使转换为C成为可能，因为显式类型声明是必须的。

安装Cython只需要一行简单的pip命令:
```
pip install cython
```

# Cython中的类型

使用Cython时，变量和函数分别有不同的类型。

对于变量我们有以下类型:

- cdef int a, b, c

- cdef char *s

- cdef float x = 0.5 (单精度)

- cdef double x = 63.4 (双精度)

- cdef list names

- cdef dict goals_for_each_play

- cdef object card_deck

注意所有这些类型都来自C/C++ ! 而对于方法我们有以下类型:

- def — 常规python函数，仅从python调用。
- cdef — 不能从python的代码中访问Cython的函数。即必须在Cython内调用
- cpdef — C 和 Python. 可以从C和Python中访问

了解了Cython类型之后，我们就可以直接实现加速了!

# 如何使用Cython加速python代码

我们要做的第一件事是设置Python代码基准:用于计算数值阶乘的for循环。原生Python代码如下:
```python
def test(x):
    y = 1
    for i in range(x+1):
        y *= i
    return y
```

相同功能的Cython方法看起来非常相似。首先，我们将确保Cython代码文件具有**.pyx**扩展名。对代码本身的惟一更改是，我们已经声明了每个变量和函数的类型。
```python
cpdef int test(int x):
    cdef int y = 1
    cdef int i
    for i in range(x+1):
        y *= i
    return y
```

Boom ! 可以看到我们的C代码已经编译好了，可以使用了!

你将看到，在Cython代码所在的文件夹中，你拥有运行C代码所需的所有文件，包括**run_cython.c**文件。如果你感兴趣，可以查看一下Cython生成的C代码!

现在我们准备测试我们新的并且超级快的C代码!查看下面的代码，它实现了一个速度测试，将原生Python代码与Cython代码进行比较。
```python
import run_python
import run_cython
import time

number = 10

start = time.time()
run_python.test(number)
end =  time.time()

py_time = end - start
print("Python time = {}".format(py_time))

start = time.time()
run_cython.test(number)
end =  time.time()

cy_time = end - start
print("Cython time = {}".format(cy_time))

print("Speedup = {}".format(py_time / cy_time))
```

代码非常直观，我们以与普通Python相同的方式导入文件，并以与普通Python相同的方式运行函数!

Cython几乎可以让你在所有原生Python代码上获得良好的加速，而不需要太多额外的工作。需要注意的关键是，循环次数越多，处理的数据越多，Cython可以提供的帮助就越多。

下表显示了Cython为不同的数值阶乘带来的加速性能。当数值为10000000的时候，可以看到，我们的Cython加速超过了**36**倍。

<a href="https://sm.ms/image/S5Htu6AUNiP7zOw" target="_blank"><img src="https://i.loli.net/2019/09/10/S5Htu6AUNiP7zOw.png" ></a>

# 注意

目前我的运行存在有
```html
DistutilsPlatformError: Unable to find vcvarsall.bat
```
错误,正在想办法解决,希望可以能尽快进入到一个c与python共存的世界

**注意:**该问题我已经解决，现在给出方法:

1. 安装vsstudio2019，教程在:[cython加速你的代码运行](https://b23.tv/av52977238)

2. 参考文章:[cython加速python使用](https://blog.csdn.net/rookie_is_me/article/details/88421373)

3. 我运行的代码源文件:[下载](https://www.lanzous.com/i64faxi)

4. [使用笔记](https://www.jianshu.com/p/cfcc2c04a6f5)