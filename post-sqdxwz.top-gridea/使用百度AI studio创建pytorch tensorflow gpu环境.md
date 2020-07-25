---
title: '使用百度AI studio创建pytorch tensorflow gpu环境'
date: 2020-05-16 09:51:55
tags: [百度]
published: true
hideInList: false
feature: 
isTop: false
---

<!-- more -->
# 教程

<iframe id="spkj" src="https://player.bilibili.com/player.html?aid=540561043&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width=100%> </iframe>
<script type="text/javascript">  
document.getElementById("spkj").style.height=document.getElementById("spkj").scrollWidth*0.76+"px";
</script>

# 命令

```html
mkdir /home/aistudio/cuda10
mkdir /home/aistudio/cuda92
mkdir /home/aistudio/cudnn
mkdir /home/aistudio/tf

cp /home/aistudio/data/data32924/cudnn-9.2.tgz /home/aistudio/cudnn

cp /home/aistudio/data/data32924/cudnn-10.1.tgz /home/aistudio/cudnn

pip install torch==1.5.0+cu101 torchvision==0.6.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html -t /home/aistudio/cuda10
pip install torch==1.5.0+cu92 torchvision==0.6.0+cu92 -f https://download.pytorch.org/whl/torch_stable.html -t /home/aistudio/cuda92
pip install tensorflow-gpu==1.15 -t /home/aistudio/tf

cd cudnn
tar -zxvf cudnn-9.2.tgz
tar -zxvf cudnn-10.1.tgz
```

进入GPU环境：

```python
import sys
sys.path.append('/home/aistudio/cuda92')
sys.path.append('/home/aistudio/tf')

import torch
import tensorflow as tf
print(torch.cuda.is_available())
print(tf.test.is_built_with_cuda())
```