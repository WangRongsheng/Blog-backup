# 1、查看本机显卡

首先我们要确定本机是否有独立显卡，在`计算机管理设备管理器-显示适配器`中，查看是否有独立显卡。

![64TGQS.md.png](https://z3.ax1x.com/2021/03/21/64TGQS.md.png)

可以看到本机有一个集成显卡和独立显卡`NVIDIA GetForce GTX 1050`。

接下来，测试本机独立显卡是否支持CUDA的安装：[查询显卡是否支持安装](https://developer.nvidia.com/cuda-gpus) 。

![64ToQO.md.png](https://z3.ax1x.com/2021/03/21/64ToQO.md.png)

![64T7Oe.md.png](https://z3.ax1x.com/2021/03/21/64T7Oe.md.png)

从上图中，可以看到我本机的独立显卡是支持`CUDA`安装的，计算力是`6.1`。

# 2、CUDA下载

[CUDA下载](https://developer.nvidia.com/cuda-toolkit-archive)

![647fBQ.md.png](https://z3.ax1x.com/2021/03/21/647fBQ.md.png)

这里我选了`CUDA Toolkit 10.0`的版本，至于选择哪个版本，个人认为应该没多大差别，一般就是看这个版本是否要求GPU的计算能力是多少以上。大约是2.1G。

![647790.md.png](https://z3.ax1x.com/2021/03/21/647790.md.png)

# 3、CUDA安装

双击打开，显示解压安装目录，不需要改变，默认即可。

![64HEHH.png](https://z3.ax1x.com/2021/03/21/64HEHH.png)

接下来，进入`NVIDIA`安装过程，在这安装过程中，我一开始直接选择的精简安装，如果由于VS的原因，导致无法正常安装，可以换成自定义的安装方式，并将VS勾给去掉，便可以正常安装了，至于CUDA的安装目录，大家默认安装在C盘即可。

![64H8bQ.md.png](https://z3.ax1x.com/2021/03/21/64H8bQ.md.png)

# 4、CUDA环境变量设置

安装完成之后，便是配置环境变量。环境变量配置如下图所示。

![64Hd2V.md.png](https://z3.ax1x.com/2021/03/21/64Hd2V.md.png)

# 5、CUDA测试安装是否成功

打开`CMD`，输入：
```html
nvcc -V
```

![64H4KO.md.png](https://z3.ax1x.com/2021/03/21/64H4KO.md.png)

输出版本即为成功。
 
# 6、CUDNN的下载

[CUDNN下载](https://developer.nvidia.com/zh-cn/cudnn)

选择下载`download cudnn`，但这里需要你注册一个账号，然后进行问卷之后才可以进行下载页面，反正一步步操作即可。

然后因为我**上一步CUDA的版本是10.0,而CUDNN的版本要跟CUDA版本一致**，所以选择第二个下载即可。

![64bGQK.md.png](https://z3.ax1x.com/2021/03/21/64bGQK.md.png)

# 7、CUDNN安装

下载之后，解压缩，将CUDNN压缩包里面的`bin`、`include`、`lib`文件直接复制到`CUDA的安装目录`下，**直接覆盖安装** 即可。

![64bJsO.png](https://z3.ax1x.com/2021/03/21/64bJsO.png)

至此，所有的安装工作已经完成，你可以接下来去安装`pytorch-gpu`和`tensorflow-gpu`！

# 8、参考

[win10下pytorch-gpu安装以及CUDA详细安装过程](https://blog.csdn.net/Mind_programmonkey/article/details/99688839)
