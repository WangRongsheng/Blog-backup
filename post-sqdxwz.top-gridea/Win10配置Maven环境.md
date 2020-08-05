# 安装

1、百度一下Maven 进入官网安装:[Welcome to Apache Maven](https://maven.apache.org/)

<center><img src="https://s1.ax1x.com/2020/08/05/ari5z8.png" alt="ari5z8.png" border="0" /></center>

注：在这个页面下请看System Requirements一栏下面说到：**Maven 3.3或之后的版本是需要JDK 1.7或者更新版本的支持！**

所以，请确保`JDK`环境变量配置完整正确，笔者用的是`JDK 1.8`！

2、配置环境变量 以`Win10`为例子：

打开Win10的环境变量：

（1）在系统变量中新建添加如下两个变量`M2_HOME`与`MAVEN_HOME`，值为`Maven安装路径`：

<center><img src="https://s1.ax1x.com/2020/08/05/ariXiq.png" alt="ariXiq.png" border="0" /></center>

（2）编辑系统变量的`Path`，`新建`，添加`Maven的bin目录`，并全部`确定`，环境变量配置完成：

<center><img src="https://s1.ax1x.com/2020/08/05/arFPeJ.png" alt="arFPeJ.png" border="0" /></center>

# 测试

打开`cmd`，输入`mvn -version`回车显示版本信息即为成功
