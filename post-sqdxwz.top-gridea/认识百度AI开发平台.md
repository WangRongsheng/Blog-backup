<center><img src="https://s1.ax1x.com/2020/04/13/Gjx8TU.png" alt="Gjx8TU.png" border="0" /></center>

# 服务平台

## AI Studio

网址：https://aistudio.baidu.com/aistudio/index

`AI Studio` 是基于百度深度学习平台飞桨的一站式AI开发平台，提供在线编程环境、免费`GPU` 算力、海量开源算法和开放数据，帮助开发者快速创建和部署模型。

## EasyDL

网址：https://ai.baidu.com/easydl/

零算法训练模型,无需机器学习专业知识，只需上传并标注需要识别的示例数据即可一键训练模型。`EasyDL` 是百度大脑推出的定制化AI训练及服务平台，支持面向各行各业有定制AI需求的企业用户及开发者使用。支持从数据管理与数据标注、模型训练、模型部署一站式AI开发流程，通过原始图片、文本、音频、视频类数据经过`EasyDL` 加工、学习、部署可发布为公有云`API` 、设备端`SDK` 、本地化部署及软硬一体产品。`EasyDL` 产品从目标客户及应用场景的角度分为经典版、专业版、零售版两个核心产品。

- 经典版面向零算法基础或者追求高效率开发AI的企业用户，现已支持图像分类、物体检测、图像分割、文本分类、视频分类、声音分类六类模型类型定制。
- 专业版面向AI初学者或AI专业工程师推出的AI模型训练与服务平台，目前支持视觉及自然语言处理两大技术方向，内置百度海量数据训练的预训练模型，可灵活脚本调参，只需少量数据可达到优模型效果。
- 零售版专门面向零售场景的ISV、零售行业服务商等企业用户提供【商品识别场景】的AI服务获取方案，支持面向货架巡检、自助结算台、无人零售柜等商品检测场景提供定制商品检测训练平台及标准商品检测API两类服务。

## EasyEdge

网址：http://ai.baidu.com/easyedge/

可基于多种深度学习框架、网络结构的模型，快捷生成端计算模型及封装SDK，适配多种AI芯片与操作系统。基于Paddle Lite研发的端计算模型生成平台，能够帮助深度学习开发者将自建模型快速部署到设备端。只需上传模型，最快2分种即可生成端计算模型并获取SDK。

平台支持详情可参见下表：

- 上传模型支持框架：`Caffe (ssd)` 、`PyTorch (1.4)`  、`TensorFlow (1.14)` 、`PaddlePaddle (1.6.2)`
- 上传模型支持网络：`VGG16` 、`InceptionV3/V4` 、`MobilenetV1` 、`MobilenetV1-SSD` 、`YoloV3` 等20种 （2020.1.17 新增支持`YoloV3` 等网络、`NNIE` 芯片）
- AI芯片加速支持：通用`ARM` 芯片、通用x86芯片、英伟达`GPU` 、高通`Snapdragon GPU/DSP` 、英特尔`Movidius VPU` 、华为`HiSilicon NPU` 、华为海思`NNIE` 、苹果`A-Bionic`

# 工具

## AutoDL

`AutoDL` 的`Github` 链接：https://github.com/PaddlePaddle/AutoDL

一种高效的自动搜索构建最佳网络结构的方法，通过增强学习在不断训练过程中得到定制化高质量的模型。系统由两部分组成，第一部分是网络结构的编码器，第二部分是网络结构的评测器。编码器通常以 RNN 的方式把网络结构进行编码，然后评测器把编码的结果拿去进行训练和评测，拿到包括准确率、模型大小在内的一些指标，反馈给编码器，编码器进行修改，再次编码，如此迭代。经过若干次迭代以后，最终得到一个设计好的模型。

## PaddleHub

`PaddleHub` 的`Github` 链接：https://github.com/PaddlePaddle/PaddleHub

便捷地获取`PaddlePaddle` 生态下的预训练模型，完成模型的管理和一键预测。配合使用`Fine-tune API` ，可以基于大规模预训练模型快速完成迁移学习，让预训练模型能更好地服务于用户特定场景的应用。`PaddleHub` 提供的预训练模型涵盖了图像分类、目标检测、词法分析、语义模型、情感分析、视频分类、图像生成、图像分割、文本审核、关键点检测等主流模型。

`PaddleHub` 以预训练模型应用为核心具备以下特点：

- 模型即软件，通过`Python API` 或命令行实现模型调用，可快速体验或集成飞桨特色预训练模型。
- 易用的迁移学习，通过`Fine-tune API` ，内置多种优化策略，只需少量代码即可完成预训练模型的`Fine-tuning` 。
- 一键模型转服务，简单一行命令即可搭建属于自己的深度学习模型API服务完成部署。
- 自动超参优化，内置`AutoDL Finetuner` 能力，一键启动自动化超参搜索。


## PARL

`PARL` 的`Github` 链接：https://github.com/paddlepaddle/parl

一个高性能、灵活的强化学习框架。
- 他们提供主流强化学习算法实现，严格地复现了论文对应的指标。
- 大规模并行支持。框架最高可支持上万个CPU的同时并发计算，并且支持多GPU强化学习模型的训练。
- 可复用性强。用户无需自己重新实现算法，通过复用框架提供的算法可以轻松地把经典强化学习算法应用到具体的场景中。
- 良好扩展性。当用户想调研新的算法时，可以通过继承提供的基类可以快速实现自己的强化学习算法


## ERNIE

持续学习语义理解框架艾尼（`ERNIE` ）利用百度海量数据和飞桨（`PaddlePaddle` ）多机多卡高效训练优势，通过深度神经网络与多任务学习等技术，持续学习海量数据和知识。基于该框架的艾尼（`ERNIE` ）预训练模型，已累计学习10亿多知识，助力各NLP任务显著提升。


## PaddleX

网址：https://www.paddlepaddle.org.cn/paddle/paddleX

飞桨全流程开发客户端，集飞桨核心框架、模型库、工具及组件等深度学习开发全流程所需能力于一身，不仅为您提供一键安装的客户端，开源开放的技术内核更方便您根据实际生产需求进行直接调用或二次开发，是提升深度学习项目开发效率的最佳辅助工具。

将深度学习开发从数据接入、模型训练、参数调优、模型评估、预测部署全流程打通，并提供可视化的使用界面， 省去了对各环节间串连的代码开发与脚本调用，极大地提升了开发效率。


## Paddle Lite

`Paddle Lite` 的`Github` 链接：https://github.com/PaddlePaddle/Paddle-Lite

文档：https://paddle-lite.readthedocs.io/zh/latest/

`FPGA` 部署:https://paddle-lite.readthedocs.io/zh/latest/demo_guides/fpga.html

`Paddle Lite` 致力于提供一套功能完整、易用、高性能的端侧推理引擎，方便广大开发者将应用部署到任何端侧设备之上。对比最初的 `beta` 版本，正式版在编译、文档、性能、硬件支持、平台支持等方面都有了较大的改进提升。核心用途是将训练出的模型在不同硬件平台场景下快速部署，根据输入数据，执行预测推理得到计算结果，支持实际的业务应用。


## PaddleCV

`PaddleCV` 的`Github` 链接：https://github.com/PaddlePaddle/models/tree/develop/PaddleCV

基于 `PaddlePaddle` 深度学习框架开发的智能视觉工具，算法，模型和数据的开源项目。百度在 `CV` 领域多年的深厚积淀为 `PaddleCV` 提供了强大的核心动力。`PaddleCV`集成了丰富的`CV` 模型，涵盖图像分类，目标检测，图像分割，视频分类，动作定位，目标跟踪，图像生成，文字识别，度量学习，关键点检测，3D视觉等 `CV` 技术。同时，`PaddleCV` 还提供了实用的工具，PLSC支持超大规模分类，`PaddleSlim` 和`PaddleLite` 支持工业级部署，以及 `PaddleDetection` 、`PaddleSeg` 面向产业的端到端开发套件，打通了模型开发、压缩、部署全流程。







