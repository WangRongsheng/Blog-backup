---
title: pytorch实现神经网络
date: 2019-10-27 17:18:28
thumbnail: https://s2.ax1x.com/2019/10/27/KsLFkq.png
tags: [pytorch, 深度学习]
categories: AI
---

神经网络是通过torch.nn包来构建的

<!--more-->

然后我们先看一个神经网络的处理流程：

1 定义网络架构

2 将输入喂入神经网络

3 神经网络计算输入得出输出

3 对比输出与真实标签数据

4 计算第3步中输出与真实标签的差距，也就是loss

5 如果loss太大，就反向传播回去调整网络参数。再重复、2，3，4，知道loss小到我们的要求为止。

```python
import torch
import torch.nn as nn
import torch.nn.functional as F



class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        #定义卷积核 1是输入通道数，6是输出通道数，5是指5×5的卷积
        #所以类推就是第一个参数是输入通道，第二个是输出通道，第三个是卷积核尺寸
        self.conv1 = nn.Conv2d(1, 6, 5)
        self.conv2 = nn.Conv2d(6, 16, 5)
        #定义全连接参数
        self.fc1 = nn.Linear(16*5*5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    #定义前向传播
    def forward(self, x):
        #将第一层卷积后的结果放入激活函数relu 再 最大池化一下，（2，2）是池化的步长
        x = F.max_pool2d(F.relu(self.conv1(x)), (2, 2))
        #同上一层一样，不过有一点不一样就是如果x是正方形，也就是长宽都相等的话，步长可以只指定一个数字
        x = F.max_pool2d(F.relu(self.conv2(x)), 2)
        # 这个是将x变成一维数组，为全连接层做准备
        x = x.view(-1, self.num_flat_features(x))
        #全连接层
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x

    def num_flat_features(self, x):
        #第一个维度不要，因为第一个维度是输入数据的batch，batch也就是一次输入多少张图片
        size = x.size()[1:]
        num_features = 1
        for s in size:
            num_features*=s
        return num_features


net = Net()
print(net)

params = list(net.parameters())

print(len(params))
print(params[0].size())


#自定义一个输入32*32的数据
input = torch.randn(1, 1, 32, 32)
out = net(input)
print(out)

#将所有梯度清零，然后反向传播
net.zero_grad()
out.backward(torch.randn(1, 10))

output = net(input)
target = torch.randn(10)  #我们定义的真实值
target = target.view(1, -1)#将真实值的维度改成和输出值的维度
criterion = nn.MSELoss()

loss = criterion(output, target)
print(loss)
print(loss.grad_fn)  # MSELoss
print(loss.grad_fn.next_functions[0][0])  # Linear
print(loss.grad_fn.next_functions[0][0].next_functions[0][0])


#清零梯度
net.zero_grad()

print('反向传播前第一层参数b')
print(net.conv1.bias.grad)

loss.backward()

print('反向传播后第一层参数b')
print(net.conv1.bias.grad)


learning_rate = 0.01
for f in net.parameters():
    f.data.sub_(f.grad.data * learning_rate)


import torch.optim as optim

optimizer = optim.SGD(net.parameters(), lr=0.01)
optimizer.step()
```