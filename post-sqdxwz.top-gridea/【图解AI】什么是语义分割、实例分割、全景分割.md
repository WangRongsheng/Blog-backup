图像分割（image segmentation）是计算机视觉中非常重要的研究和应用方向，是根据某些规则将图片中的像素分成不同的部分、打上不同标签。图解如下：

## 1、图像分类（image classification）

识别图像中存在的内容，如下图，有人（person）、树（tree）、草地（grass）、天空（sky）

![gkIJij.png](https://z3.ax1x.com/2021/04/29/gkIJij.png)

## 2、目标检测（object detection）

识别图像中存在的内容和检测其位置，如下图，以识别和检测人（person）为例

![gkI1eS.png](https://z3.ax1x.com/2021/04/29/gkI1eS.png)

## 3、语义分割（semantic segmentation）

对图像中的每个像素打上类别标签，如下图，把图像分为人（红色）、树木（深绿）、草地（浅绿）、天空（蓝色）标签

![gkI3dg.png](https://z3.ax1x.com/2021/04/29/gkI3dg.png)

## 4、实例分割（instance segmentation）

目标检测和语义分割的结合，在图像中将目标检测出来（目标检测），然后对每个像素打上标签（语义分割）。对比上图、下图，如以人（person）为目标，语义分割不区分属于相同类别的不同实例（所有人都标为红色），实例分割区分同类的不同实例（使用不同颜色区分不同的人）

![gkI8oQ.png](https://z3.ax1x.com/2021/04/29/gkI8oQ.png)

## 5、全景分割（panoptic segmentation）

语义分割和实例分割的结合，即要对所有目标都检测出来，又要区分出同个类别中的不同实例。对比上图、下图，实例分割只对图像中的目标（如上图中的人）进行检测和按像素分割，区分不同实例（使用不同颜色），而全景分割是对图中的所有物体包括背景都要进行检测和分割，区分不同实例（使用不同颜色）

![gkIQL8.png](https://z3.ax1x.com/2021/04/29/gkIQL8.png)