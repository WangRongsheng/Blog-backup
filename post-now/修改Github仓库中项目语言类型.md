# 简介

众所周知，当我们使用`Github` 的时候，我们的项目语言很大程度上会影响别人的搜索和自己的强迫症被逼犯，那么我们是不是可以对我们的`Github` 项目的编程语言进行修改或者进行自主标明呢？

# 修改

> 在`Github`  中，采用`Linguist` 来自动识别**代码语言** 。

> 我们要做的就是对`linguist-language` 进行赋值，强制它识别某一种语言文件为我们想要它显示的语言。

我们需要在仓库的根目录下添加`.gitattributes`文件:并写入

```html
*.js linguist-language=python
```

这行代码的意思是：将文件中所有的`.js` 结尾的文件固定为`python` 语言。当然，我们也可以指定其它文件和其它语言。

<img src="https://s1.ax1x.com/2020/04/09/G4zT76.png" alt="G4zT76.png" border="0" />

显示的结果就更为：

<img src="https://s1.ax1x.com/2020/04/09/G5SKEV.png" alt="G5SKEV.png" border="0" />