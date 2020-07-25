---
title: 提取ipynb文件中的py代码
date: 2019-11-08 21:07:53
thumbnail: https://i.loli.net/2019/11/08/sDrwh2ALpomfMev.png
tags: 提取ipynb文件
categories: Python
---

.ipynb是Anaconda3中Jupyter Notebook的文件格式，非常方便Python教学，在科学计算和数据分析等领域使用较多。在Jupyter Notebook中，使用菜单File==>Download as==>Python(.py)可以直接另存为.py文件，但是如果已经存在.ipynb文件该怎么去获得python代码呢？

<!--more-->

当我们利用记事本打开.ipynb文件时，会发现文件的格式跟json文件是一样的。这样的话可以使用Python标准库json进行解析，然后提取其中的Python代码。

参考代码：

```python
import json

with open("你的文件名称.ipynb",encoding="utf-8") as fp:
    content = json.load(fp)

with open("保存的文件名称.py","w",encoding="utf-8") as fp:
    for item in content["cells"]:
        fp.writelines([i.rstrip()+"\n" for i in item["source"]])
```

