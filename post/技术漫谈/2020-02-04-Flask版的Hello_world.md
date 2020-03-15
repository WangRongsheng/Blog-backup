---
layout: post
cid: 160
title: Flask版的Hello world
slug: 160
date: 2020/02/04 20:12:00
updated: 2020/02/22 13:43:43
status: publish
author: 王荣胜
categories: 
  - 技术漫谈
tags: 
  - Falsk的hello world
thumb2: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1582360284849&di=9fadaaba39639a3d62a865e8074a0d93&imgtype=0&src=http%3A%2F%2Fwscont2.apps.microsoft.com%2Fwinstore%2F1x%2Fea9a3c59-bb26-4086-b823-4a4869ffd9f2%2FScreenshot.398115.100000.jpg
---


<!--more-->
# 前言

大家都知道，作为一个编程人员，学习一门语言的基础就是输出一个“Hello World”，今天就来实现下python的Web框架Flask的“Hello World”吧。

# 一、实现

完整代码：
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World'

if __name__ == '__main__':
    app.run()  #host='0.0.0.0',port=9000,debug=True
```

上面的代码所做的事情：
`
1. 导入Flask类，该类的实例可以创建一个WSGI服务
2. 创建Flask类的实例
3. 用route装饰器将URL和helloWorld()函数绑定:关于[装饰器](https://www.liaoxuefeng.com/wiki/1016959663602400/1017451662295584)
4. 当特定URL向WSGI发送请求会调用helloWorld函数，最终向客户端浏览器返回"Hello World"
5. 当python运行hello.py时，application实例开启服务

将上述代码保存（**不要保存为flask.py**，这会和Flask发生冲突）。

# 二、运行

## 1、启动

<img src="https://s2.ax1x.com/2020/02/04/1D8kh8.md.png" alt="1D8kh8.md.png" border="0">

## 2、结果

<img src="https://s2.ax1x.com/2020/02/04/1D8V1g.md.png" alt="1D8V1g.md.png" border="0">

# 三、注意

1. 不要直接在编译器运行，必须在**命令行**；[原因](https://blog.csdn.net/qq_41663800/article/details/88383011)
2. 在测试中不要指定端口（上述代码中我注释掉的），否则不能在网页中正常打开；
3. Debug是为了让开发人员在测试环境中进行直接debug，我们一般用不到，这里说一下Debug模式：
> 在开发情况下，常常需要在Flask运行时修改代码，开启Flask的Debug模式，每次修改代码Flask会立即生效。
方法一：
```python
app.run(debug=True)
```
方法二：
建立flask的配置文件config.py
```python
DEBUG = True
```
在app文件中
```python
import config
app.config.from_object(config)
```
