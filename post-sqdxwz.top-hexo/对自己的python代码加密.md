---
title: 对自己的python代码加密
date: 2019-11-05 22:04:28
thumbnail: https://i.loli.net/2019/11/05/VHfgm1YKIMF64nv.png
tags: 代码加密
categories: Python
---

由于 Python 的动态特性和开源特点，导致 Python 代码很难做到很好的加密。社区中的一些声音认为这样的限制是事实，应该通过法律手段而不是加密源码达到商业保护的目的；而还有一些声音则是不论如何都希望能有一种手段来加密。于是乎，人们想出了各种或加密、或混淆的方案，借此来达到保护源码的目的。

<!--more-->

常见的源码保护手段有如下几种：

1. 发行.pyc文件

2. 代码混淆

3. 使用py2exe

4. 使用Cython

下面来简单说说这些方案。

## 1.发行.pyc 文件

**生产.pyc文件**：

```html
python -m compileall 文件名称
```

**解密.pyc文件**：

首先安装**uncompyle6** 库，然后在同文件下执行：

```html
uncompyle6 -o . 文件名
```
**批量解密.pyc文件**：

```python
# encoding=utf8
import os
import uncompyle6
from uncompyle6 import decompile_file
def main():
    path = 'C:\filename'.decode('utf8')        # Windows下
    for root, dirs, files in os.walk(path):
        if root != path:
            break
        for filename in files:
            if filename.endswith('pyc'):
                print filename
                os.system('uncompyle6 -o . %s'%filename)
    
if __name__ == '__main__':
    main()
```

优点：

- 简单方便，提高了一点源码破解门槛

- 平台兼容性好，.py能在哪里运行，.pyc就能在哪里运行

不足：

- 解释器兼容性差，.pyc只能在特定版本的解释器上运行

- 有现成的反编译工具，破解成本低

## 2.代码混淆

- 网站混淆：http://pyob.oxyry.com/

- 使用 pyobfuscate 库进行混淆

优点：

- 简单方便，提高了一点源码破解门槛
- 兼容性好，只要源码逻辑能做到兼容，混淆代码亦能

不足：

- 只能对单个文件混淆，无法做到多个互相有联系的源码文件的联动混淆
- 代码结构未发生变化，也能获取字节码，破解难度不大

## 3.使用py2exe

py2exe 是一款将 Python 脚本转换为 Windows 平台上的可执行文件的工具。其原理是将源码编译为.pyc文件，加之必要的依赖文件，一起打包成一个可执行文件。

使用py2exe进行打包的步骤较为简便。

1）编写入口文件。本示例中取名为hello.py：

```html
print 'Hello World'
```

2）编写setup.py：

```html
from distutils.core import setup
import py2exe

setup(console=['hello.py'])
```

3）生成可执行文件

```html
python setup.py py2exe
```
生成的可执行文件位于dist\hello.exe

优点：

- 能够直接打包成 exe，方便分发和执行

- 破解门槛比 .pyc 更高一些

不足：

- 兼容性差，只能运行在 Windows 系统上

- 生成的可执行文件内的布局是明确、公开的，可以找到源码对应的.pyc文件，进而反编译出源码

## 4.使用 Cython

使用Cython进行开发的步骤也不复杂。

1）编写文件hello.pyx或hello.py：

```html
def hello():
    print('hello')
```
2）编写setup.py：

```html
from distutils.core import setup
from Cython.Build import cythonize

setup(name='Hello World app',
     ext_modules=cythonize('hello.pyx'))
```

3）编译为.c，再进一步编译为.so或.pyd：

```html
python setup.py build_ext --inplace
```

执行python -c "from hello import hello;hello()"即可直接引用生成的二进制文件中的hello()函数。

优点：

- 生成的二进制 .so 或 .pyd 文件难以破解

- 同时带来了性能提升

不足：

- 兼容性稍差，对于不同版本的操作系统，可能需要重新编译

- 虽然支持大多数 Python 代码，但如果一旦发现部分代码不支持，完善成本较高

