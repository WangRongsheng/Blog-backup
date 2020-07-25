# Labelme简介

LabelMe 是一个用于在线图像标注的 Javascript 标注工具。与传统图像标注工具相比，其优势在于我们可以在任意地方使用该工具。此外，它也可以帮助我们标注图像，不需要在电脑中安装或复制大型数据集。

# 安装使用

## 安装labelme

> 所有操作在已经安装Anaconda环境下运行：[Anaconda3 Win10安装教程](https://blog.csdn.net/weixin_38795242/article/details/100106454) 

1. 打开`Anaconda3`自带的`Anaconda Prompt`；
2. 创建一个虚拟的py环境：

```python
conda create –name=labelme python=3.6
```

3. 安装`pyqt`：

```python
conda install pyqt
```

4. 安装`labelme`：

```python
pip install labelme -i https://pypi.tuna.tsinghua.edu.cn/simple
```

> 这里我进行了*换源* ，原因是因为安装速度过慢！

<img src="https://s2.ax1x.com/2020/03/11/8EeHmR.png" alt="8EeHmR.png" border="0" />

- 左侧选项依次是：
    - 打开文件、打开目录、下一张、上一张、保存、创建多边形、编辑多边形、复制、删除、撤销操作、图片放大…
- 中间是：
  - 图片区域
- 右边显示的有：
    - flags、标签名称列表、多边形标注、图片文件列表
- 顶部菜单栏：
  - 文件、编辑、视图、帮助

## 使用labelme

此处打开一个图片文件夹做示范：

1. 点击左侧`Open Dir`选择需要标注的数据文件夹。

2. 在顶部 `edit` 菜单栏中可选不同的标记方案，依次为：`多边形`（默认），`矩形`，`圆`、`直线`，`点`。

3. 制作图像分割的数据，选择多边形，点击左侧的 `create polygons` ，回到图片，按下鼠标左键会生成一个点，完成标注后会形成一个标注区域，同时弹出labelme的框，键入标签名字，点击 `OK`或者`回车`完成标注。

<img src="https://s2.ax1x.com/2020/03/11/8EupdI.png" alt="8EupdI.png" border="0" />

4. 如果需要更改标注的数据，可以选择左侧的编辑框，或者把鼠标移动到标签上，点击鼠标右键，可以选择编辑标签或者标注的名字。在编辑模式下，把鼠标移动到边界上，右键，可以增加点。

5. 标注完成后点击`Save`保存。会在图片路径下生成同名的`json文件`。在目录下打开终端键入：

```html
labelme_json_to_dataset <文件名>.json 
```

会把生成的json转化成对应的数据文件：
```html
*.png 
info.yaml 
label.png 
label_names.txt 
label_viz.png
```

> 如果这里你嫌弃一个一个转化json文件太麻烦的话可以进行批量转化：
> 1. [利用labelme批量转换.json文件](https://blog.csdn.net/u010732965/article/details/83315617)
> 2. 也可以利用我写的一个python脚本：
> ```python
> import os
> path = './<文件名称>' # path为json文件存放的路径
> json_file = os.listdir(path)
> os.system("activate labelme")
> for file in json_file:
>    os.system("labelme_json_to_dataset.exe %s"%(path + '/' + file))
> ```
> >注意：要把所有的json文件放在**同一个文件夹**哦！

# 参考

1. [win10下 Anaconda使用conda连接网络出现错误(CondaHTTPError: HTTP 000 CONNECTION FAILED for url）](https://blog.csdn.net/u013383596/article/details/87718472)
2. [labeme批量转化json 未生成info.yaml解决办法](https://blog.csdn.net/weixin_43410539/article/details/104372086)
3. [官方项目地址](https://github.com/wkentaro/labelme)
4. [数据标注软件labelme详解](https://blog.csdn.net/u014061630/article/details/88756644)