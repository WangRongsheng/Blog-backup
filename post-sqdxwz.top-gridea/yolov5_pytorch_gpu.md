 # 🔥 YOLOv5 PyTorch GPU 安装教程

### ✅ 第一步：关闭YOLOv5 PyTorch依赖

📌 将yolov5 目录中的`requirements.txt`中的PyTorch依赖关闭

```shell
# Base ----------------------------------------
matplotlib>=3.2.2
numpy>=1.18.5
opencv-python>=4.1.2
Pillow>=7.1.2
PyYAML>=5.3.1
requests>=2.23.0
scipy>=1.4.1
# torch>=1.7.0 （关闭）
# torchvision>=0.8.1 （关闭）
tqdm>=4.41.0
```

### ✅ 第二步：官网在线安装

📌 进入官网：https://pytorch.org/get-started/locally/

📌 以Linux `CUDA 11.3` 版本为例，进行选择

<div align="center" >
<img src="https://pycver.gitee.io/ows-pics/imgs/pytorch_web.png">
</div>
📌 复制安装指令，在conda虚拟环境中进行安装

```shell
pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
```



### ✅ 手动下载方法（离线版安装）

还可以通过手动的方式，根据自己的实验环境，自定义下载安装包

📌 方法一：进入官网下载地址，[torch安装包列表](https://download.pytorch.org/whl/torch/) | [torchvision安装包列表](https://download.pytorch.org/whl/torchvision/)

📌 方法二：进入官网指定的CUDA版本下载地址：https://download.pytorch.org/whl/cu113/torch_stable.html （以CUDA11.3为例）

```shell
# 标*部分可以根据自己的CUDA型号进行搜索，比如CUDA 10.2对应为102，CUDA11.3对应为113
https://download.pytorch.org/whl/cu***/torch_stable.html
```

📌 根据自己的实验环境，包括操作系统、CUDA类型、Python版本等，选择安装的`torch`和`torchvision`的安装包

<div align="center" >
<img src="https://pycver.gitee.io/ows-pics/imgs/pytorch_list.png">
</div>
📌 通过pip安装下载的PyTorch安装包

```shell
pip install ./torch-***.whl # 先安装
pip install ./torchvision-***.whl # 后安装 
```

❗ 注意：这里存在**安装顺序**，由于`torch`是`torchvision`的上级安装包，如果先安装`torchvision`，则会自动下载`torch`安装包。因此先安装`torch`，再安装`torchvision`



### ❤️ PyTorch版本

📌 官网：https://github.com/pytorch/pytorch/wiki/PyTorch-Versions

