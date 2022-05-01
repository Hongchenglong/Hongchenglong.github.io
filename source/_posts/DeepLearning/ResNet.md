---
title: 精读论文《Deep Residual Learning for Image Recognition》
tags: [Deep Learning]
---

为了解决深度学习的退化问题，作者提出了深度残差学习框架，让网络层去拟合残差映射。

<!-- more -->

# Deep Residual Learning for Image Recognition

## Abstract

更深层的神经网络更难训练。作者提出了一个残差学习框架，对输入层的残差函数进行学习。

## 1. Introduction

DCNN在图像分类上带来一系列突破。但是随着神经网络层数越深，训练误差越大，因此测试误差越大。

<img src="https://gitee.com/oeong/picgo/raw/master/images/20220202190314.png" alt="image-20220202190303077" style="zoom: 80%;" />

`Is learning better networks as easy as stacking more layers?` 堆叠更多的层数以后网络是否学习效果更好？但是堆叠更多的层后往往会遇到`vanishing/exploding gradients`梯度问题，会从一开始就阻止收敛。好在这个问题可以通过初始归一化`normalized initialization`和中间层归一化`intermediate normalization layers`来解决。

当网络开始收敛时，往往会出现退化`degradation`现象。随着网络深度的增加，准确率趋近饱和，然后迅速下降。意外的是，这不是由于过拟合`overfitting`造成的，更深的模型反而会有更高的训练误差。

为了==解决深度学习的退化问题==，作者提出了深度残差学习框架，让网络层去拟合残差映射。如果我们想要得到的映射为 $\mathcal{H}(\mathbf{x})$，则我们让添加的非线性网络层去拟合残差映射 $\mathcal{F}(\mathbf{x}):=\mathcal{H}(\mathbf{x})-\mathbf{x}$，则原始的映射就可以写成 $\mathcal{F}(\mathbf{x})+\mathbf{x}$。残差映射的实现可以通过图2所示的连接块实现，跳跃连接是一个**恒等映射**，没有引入额外的参数和计算复杂度，整个网络很容易实现。

<img src="https://gitee.com/oeong/picgo/raw/master/images/20220202194810.png" alt="image-20220202194803965" style="zoom:80%;" />

在`ImageNet`、`CIFAR-10`、`COCO`数据集上，大量的实验结果表明作者设计的`残差学习框架`的通用性，一方面不仅使得网络更容易优化，另一方面随着网络深度的增加，网络复杂度并没有明显增加，准确率却会提高很多。

## 2. Related Work

### Residual Representations. 

在图像识别中，VLAD是由相对于字典的残差向量编码的表示，并且费舍尔向量可以被表示为VLAD的概率版本。

### Shortcut Connections.

训练多层感知器(MLP)的早期实践是添加从网络输入到输出的线性层。

## 3. Deep Residual Learning

### 3.1. Residual Learning

### 3.2. Identity Mapping by Shortcuts

### 3.3. Network Architectures

#### Plain Network.

#### Residual Network. 

网络设计原则为：对于相同的输出特征图尺寸，卷积层具有相同数量的卷积核；如果特征图尺寸减半，则卷积核数量加倍，以便保持每层的时间复杂度。通过步长为2的卷积层直接执行下采样。下面以`ResNet-34`为例进行介绍：

第一个卷积层，卷积核大小为 7 × 7，卷积核个数为64，步长为2；
三个残差连接块，每一个连接块由两层卷积网络组成，卷积核大小为 3 × 3，卷积核个数为64；
四个残差连接块，每一个连接块由两层卷积网络组成，卷积核大小为 3 × 3，卷积核个数为128；
六个残差连接块，每一个连接块由两层卷积网络组成，卷积核大小为 3 × 3，卷积核个数为256；
三个残差连接块，每一个连接块由两层卷积网络组成，卷积核大小为 3 × 3，卷积核个数为512；
最后一个全连接层，整个网络包含卷积层和全连接层，共 1+(3+4+6+3)*2+1 = 34层。

![image-20220208175331741](https://gitee.com/oeong/picgo/raw/master/images/20220208175344.png)

从表1可以看到，`ResNet-18`和`ResNet-34`具有相同的残差连接块，每个连接块包含两个卷积层。而`ResNet-50/101/152`的每个连接块包含3个卷积层。作者把这种连接块称为`bottleneck`（如下图所示），这里主要使用了1 × 1 的卷积核，主要是用于**匹配特征图维度**以及从实践出发能够承担的起训练时间。

<img src="https://gitee.com/oeong/picgo/raw/master/images/20220208175643.png" alt="image-20220208175641450" style="zoom:80%;" />

### 3.4. Implementation

作者参考`AlexNet`和`VGG`来进行训练。首先对图像的短边进行尺度扩大，扩大到 [256, 480]，然后和AlexNet一样，随机选择 224 × 224 大小的图案。作者在这里使用到了`batch normalization` (BN) 技术；初始化权重并从零开始训练。梯度下降使用了`SGD`，`mini-batch`大小为256，总共进行了 $60\times10^4$ 次迭代。为了得到最好的实验结果，作者在多个尺度上进行评估，然后取平均分。

## 4. Experiments

### 4.1. ImageNet Classification

首先评估了`plain-18/34`两个网络，从表2可以看到，`plain-34`网络比`plain-18`有更高的错误率，从图4左图也可以看到，在训练过程中，出现了退化现象，随着网络深度的增加，训练误差反而变大。作者在论文中解释到：退化现象应该不是梯度消失引起的，因为整个训练使用了BN来训练，也查验了反向传播时梯度幅值也是正常的，作者怀疑可能是因为更深的网络有着更低的收敛速度，影响着训练误差的减小，这个问题未来会进一步研究。

接着是ResNet-18/34两个网络的评估，从表2和图4右图可以观察到三个现象：1. 网络越深，训练误差反而越小，退化问题可以通过残差学习得到解决；2. 与plain-34网络相比，训练误差下降了3.5%，随着网络深度的不断增加，网络性能进一步提高；3. 与palin-18/34网络相比，残差网络收敛速度更快。

<img src="https://gitee.com/oeong/picgo/raw/master/images/20220208185250.png" alt="image-20220208185249741" style="zoom:80%;" />

然后是`恒等跳跃连接和投影跳跃连接`的对比，可以看到三种连接都有助于提高网络性能，但是为了不增加网络结构的复杂度，作者这里主要选择恒等跳跃连接进行后续的实验。

下面是ResNet-50/101/152网络的评估，首先可以看到，尽管网络深度不断增加，但是复杂度依然低于VGG-16/19。随着网络深度的不断增加，错误率不断下降，同时在训练过程中也没有出现退化现象，在单个模型上取得了4.49%的错误率，在ImageNet2015比赛上，通过集成6个不同的模型，取得了3.57%的错误率。

# 思考

**残差结构与传统结构的本质区别在哪？输出是否一致呢？**

plain Net：building block的映射F(x)拟合H(x)，即F(x) := H(x)

Res Net：加入了skip connection 结构，此时 building block 的任务：F(x) := H(x)-x

**残差结构为什么比传统结构更好优化？**

提升了梯度与损失的相关性，进而使网络的学习能力增强，解决退化问题。

比如把5映射到5.1，那么引入残差前是F'(5)=H(5)=5.1，引入残差后是H(5)=F(5)+5=5.1, F(5)=0.1。这里的F'和F都表示网络参数映射，引入残差后的映射对输出的变化更敏感。

比如输出从5.1变到5.2，映射F'的输出增加了1/51=2%，而对于残差结构输出从5.1到5.2，映射F是从0.1到0.2，增加了100%。明显后者输出变化对权重的调整作用更大，所以效果更好。**训练残差的思想是去掉相同的主体部分，从而突出微小的变化，残差网络可以看做是差分放大器。**

**为什么残差网络可以进一步解决梯度消失？**

反向传播时，由于层数过深，很容易出现梯度问题。ResNet将BP过程中梯度相乘变成相加，便解决了梯度问题。

# 参考


- `ResNet`论文链接为：[https://arxiv.org/abs/1512.03385](http://xxx.itp.ac.cn/pdf/1512.03385.pdf)

- https://blog.csdn.net/cg129054036/article/details/120934900