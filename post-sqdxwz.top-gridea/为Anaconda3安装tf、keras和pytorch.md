# 安装tensorflow

1、打开`anaconda`安装时自带的`Anaconda prompt`

2、打开后,输入清华镜像的`tensorflow` 的下载地址(如果你已经在墙外翱翔了,可以省略这一步):

 ```html
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
 ```
 
3、接着我们开始创建一个`python3.6` 的环境,因为如果你安装的是最新的`anaconda` ,它默认环境为`py3.7` ,并且在不久之前,`tensorflow` 已经开始支持`py3.6` ,所以我们创建一个`py3.6` 环境:

 ```html
conda create -n tensorflow python=3.6
 ```
 
4、启动`anaconda` 中的`py3.6` 环境:
 ```html
activate tensorflow
 ```
 
如果不能进入,则重新执行第3步骤

5、进入`py3.6` 的环境中后,我们就可以进行安装了(此处我们安装的是`CPU版本`的`tensorflow`):

 ```html
pip install --upgrade --ignore-installed tensorflow 
  ```
  
6、当我们不使用`tensorflow`时,我们就可以使用:

 ```html
deactivate
 ```
 
 退出该环境
 
7、开始测试一下是否安装成功:

重新打开`Anaconda Prompt`—>`activate tensorflow`—>`python`来启动`tensorflow`，并进入`python`环境

 ```python
#TensorFlow使用图(Graph)来表示计算任务；并使用会话(Session)来执行图，通过Session.close()来关闭会话（这是一种显式关闭会话的方式）。会话方式有显式和隐式会话之分。
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')  #初始化一个TensorFlow的常量
sess = tf.Session()  #启动一个会话
print(sess.run(hello))  
 ```
 
如果可以准确的输出结果,那么恭喜你,安装tensorflow成功!

# 安装Keras

我们继续在刚才`tensorflow` 的虚拟`python` 环境中安装`Keras`：

```html
pip install keras
```

查看是否成功：

```html
import keras
```

如果输出无异常，那么就是安装成功！

# 安装pytorch

首先，打开 `PyTorch` 官网安装页面（需自备梯子）：https://pytorch.org/get-started/locally/

<center><img src="https://s1.ax1x.com/2020/04/09/G5tP9f.png" alt="G5tP9f.png" border="0" /></center>

- `PyTorch Build` 就是选择下载稳定版（`Stable`）还是预览版（`Preview`），这里一般选择稳定版（`Stable`）
- `YourOS` 不多说，选择自己对应的操作系统类型
- `Package`：下载方式，教程提供的是 `Conda` 方式，这里我们使用 `Pip` 方式
- `Language`：即选择你的 `python` 版本（`Anaconda` 下载后自带 `python` ，可以在 `cmd` 输入 `python --version` 查看自己的 `python` 版本）
- `CUDA`：如果要下载 `gpu` 版本，那么就选择你对应的 `cuda` 的版本（不知道自己 `cuda` 版本的请戳：https://www.jianshu.com/p/d3b9419a0f89）；如果下载 `cpu` 版本，那么选择 None
- `Run this Command`：当你选择好版本后，会自动再次生成下载安装 `PyTorch` 的命令

然后复制页面中`Run this Command`后的代码,粘贴在你的命令行,等待安装完成就可以了~

查看是否成功：

```html
import torch
```

如果输出无异常，那么就是安装成功！