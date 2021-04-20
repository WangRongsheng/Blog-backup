## 1.YoloV5训练模型导出

https://github.com/ultralytics/yolov5/issues/251

> .pt->.onnx

## 2.onnx->ncnn

https://convertmodel.com/

> .onnx->ncnn

## 3.修改ncnn模型再导出（部分op不支持情况下）

在Linux环境下执行

安装autoconf和automake：
```html
# 安装autoconf和automake(一般只安装这两个模块就行了，不用操作 gcc libtool等)
yum -y install gcc automake autoconf libtool make
# 安装g++:
yum install gcc gcc-c++
```

安装protobuf：
```html
wget https://github.com/google/protobuf/releases/download/v3.6.1/protobuf-all-3.6.1.tar.gz
tar zxvf protobuf-all-3.6.1.tar.gz
./autogen.sh
./configure
make
make install
```

安装ncnn：
```html
git clone https://github.com/Tencent/ncnn.git
cd ncnn
git submodule update --init
mkdir build
cd build
cmake .. (本步如果您 yum install cmake3，可以使用 cmake3 .. )
make -j8
make install
```

## 4.导出修改的模型

终端进入`ncnn/build/tools`目录

可以发现`tools`目录下存在`ncnnoptimize`的可执行文件

```html
# 导出命令
# ./ncnnoptimize 你修改好的模型.param 你修改好的模型.bin model-opt.param model-opt.bin 0

./ncnnoptimize model.param model.bin model-opt.param model-opt.bin 0
```

## 5.部署在安卓或者苹果端

https://github.com/cmdbug/YOLOv5_NCNN

## 参考

- [NCNN深度学习框架之Optimize优化器](https://www.cnblogs.com/wanggangtao/p/11313705.html)
- [手工优化ncnn模型结构](https://zhuanlan.zhihu.com/p/93017149)
- [Centos7 NCNN 编译安装【亲测】](https://blog.csdn.net/qq_29750461/article/details/114803780)