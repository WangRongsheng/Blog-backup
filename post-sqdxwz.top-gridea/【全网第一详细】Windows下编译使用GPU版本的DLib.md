# 一、准备基础环境

因为要用上GPU所以提前准备好的:

1. CUDA

将cuda/bin和cuda/lib/x64以及cuda/include添加到环境变量Path

2. CUDNN

解压CUDNN然后把它对应文件夹中的文件添加到CUDA对应的文件夹目录下

> 可以参考：[深度学习GPU环境CUDA详细安装过程（简单快速有效）](https://zhuanlan.zhihu.com/p/358737417)

# 二、下载Dlib官方包

[https://github.com/davisking/dlib/releases](https://github.com/davisking/dlib/releases)

下载最新版本即可

# 三、安装cmake

[Windows下CMake安装教程](https://blog.csdn.net/u011231598/article/details/80338941)

# 四、编译Dlib

管理员模式`cmd`进入到`Dlib`文件夹下，输入：
```html
python setup.py install
```

等待编译完成！

# 五、嵌入到Python中使用（重要）

之前我一直不知道怎么编译好使用，直到我看到[这篇文章](https://www.cnblogs.com/drake233/p/10022489.html) ，里面作者详细说明了在Anaconda3中编译使用Dlib，经过我的实践确实可以用，他有一个关键的操作就是将编译的Dlib放到Anaconda3的目录下，所以我觉得在Python中使用应该也是如此，于是我：
```html
把编译好的Dlib整个文件夹放入到了 E:\python365\Lib\site-packages 下（放到你的python安装路径下）
```

# 六、测试使用

```python
import dlib
print(dlib.DLIB_USE_CUDA)
print(dlib.cuda.get_num_devices())
```

