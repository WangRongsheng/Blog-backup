---
title: 'Mish:撼动深度学习ReLU激活函数的新继任者'
date: 2019-09-25 18:55:14
thumbnail: https://i.loli.net/2019/09/25/MtpOR6Qfu3ZXPEe.png
tags: 深度学习
categories: AI
---
> 对激活函数的研究一直没有停止过，ReLU还是统治着深度学习的激活函数，不过，这种情况有可能会被Mish改变。

<!--more-->

Diganta Misra的一篇题为“Mish: A Self Regularized Non-Monotonic Neural Activation Function”的新论文介绍了一个新的深度学习激活函数，该函数在最终准确度上比Swish(+.494%)和ReLU(+ 1.671%)都有提高。

他们的小型FastAI团队使用Mish代替ReLU，打破了之前在FastAI全球排行榜上准确性得分记录的一部分。结合Ranger优化器，Mish激活，Flat + Cosine 退火和自注意力层，他们能够获得12个新的排行榜记录！

<a href="https://sm.ms/image/PZMCh1OpjkRvYqf" target="_blank"><img src="https://i.loli.net/2019/09/25/PZMCh1OpjkRvYqf.jpg" ></a>

我们12项排行榜记录中的6项。每条记录都是用Mish而不是ReLU。(蓝色高亮显示，400 epoch的准确率为94.6，略高于我们的20 epoch的准确率为93.8:)

作为他们自己测试的一部分，对于ImageWoof数据集的5 epoch测试，他们说：

> Mish在高显著性水平上优于ReLU (P < 0.0001)。(FastAI论坛@ Seb)

Mish已经在70多个基准上进行了测试，包括图像分类、分割和生成，并与其他15个激活函数进行了比较。

# 什么是Mesh

直接看Mesh的代码会更简单一点，简单总结一下，Mish=x * tanh(ln(1+e^x))。

其他的激活函数，ReLU是x = max(0,x)，Swish是x * sigmoid(x)。

**PyTorch的Mish实现**：

<a href="https://sm.ms/image/Ya4lGfdXjN3o2qH" target="_blank"><img src="https://i.loli.net/2019/09/25/Ya4lGfdXjN3o2qH.jpg" ></a>

**Tensorflow中的Mish函数**：

Tensorflow：x = x *tf.math.tanh(F.softplus(x))

# Mish和其他的激活函数相比怎么样？

下图显示了Mish与其他一些激活函数的测试结果。这是多达73个测试的结果，在不同的架构，不同的任务上：

<a href="https://sm.ms/image/zrD2FSpymHT13s5" target="_blank"><img src="https://i.loli.net/2019/09/25/zrD2FSpymHT13s5.jpg" ></a>

# 为什么Mish表现这么好？

以上无边界(即正值可以达到任何高度)避免了由于封顶而导致的饱和。理论上对负值的轻微允许允许更好的梯度流，而不是像ReLU中那样的硬零边界。

最后，可能也是最重要的，目前的想法是，平滑的激活函数允许更好的信息深入神经网络，从而得到更好的准确性和泛化。

尽管如此，我测试了许多激活函数，它们也满足了其中的许多想法，但大多数都无法执行。这里的主要区别可能是Mish函数在曲线上几乎所有点上的平滑度。

这种通过Mish激活曲线平滑性来推送信息的能力如下图所示，在本文的一个简单测试中，越来越多的层被添加到一个测试神经网络中，而没有一个统一的函数。随着层深的增加，ReLU精度迅速下降，其次是Swish。相比之下，Mish能更好地保持准确性，这可能是因为它能更好地传播信息：

<a href="https://sm.ms/image/3udy29EoMmq8KwD" target="_blank"><img src="https://i.loli.net/2019/09/25/3udy29EoMmq8KwD.jpg" ></a>

更平滑的激活功能允许信息更深入地流动……注意，随着层数的增加，ReLU快速下降。

# 如何把Mish放到你自己的网络中？

Mish的PyTorch和FastAI的源代码可以在github的两个地方找到：

1、官方Mish github：https://github.com/digantamisra98/Mish

2、非官方的Mish使用inline提升速度：https://github.com/lessw2020/mish

# 总结

ReLU有一些已知的弱点，但是通常它执行起来很轻，并且在计算上很轻。Mish具有较强的理论渊源，在测试中，就训练稳定性和准确性而言，Mish的平均性能优于ReLU。

复杂度只稍微增加了一点(V100 GPU和Mish，相对于ReLU，每epoch增加大约1秒)，考虑到训练稳定性的提高和最终精度的提高，稍微增加一点时间似乎是值得的。

最终，在今年测试了大量新的激活函数后，Mish在这方面处于领先地位，许多人怀疑它很有可能成为AI未来的新ReLU。

英文文章地址：https://medium.com/@lessw/meet-mish-new-state-of-the-art-ai-activation-function-the-successor-to-relu-846a6d93471f

