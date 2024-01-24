---
layout: post
title: 卷积神经元网络
---

我们下面学习卷积神经元网络（CNN）。它主要应用于计算机视觉。计算机视觉是一个很大的领域，有着悠久的历史。请首先参看[课程 1](https://bjtu-netcomm.github.io/ai/ai.html)，学习第三课：视觉，熟悉计算机视觉的基础知识。

卷积神经元网络提出的背景是图片分类。因为图片像素众多，如果用全连通网络，每个像素值都分配一个权重参数，参数会太多，而且没有必要。比如一张 1M 像素的图片，假设我们在输入层将图片中的每个像素都连接到一个神经元，那么输入层的一个神经元就需要 1M 参数。

为了减少模型参数的数量，人们借鉴了信号与系统里的“滤波器”方法，提出了 CNN（卷积神经元网络），用比图片小得多的“滤波器”，来对图片进行”卷积“操作。

具体来说，一个 CNN 层包括以下三种操作：

第一是卷积。它是用一个小尺寸的 Filter（比如 64*64 的方形 Filter，对图片进行上下扫描，做卷积操作。相对于将图片像素全部连接到一个神经元，这个 Filter 的参数就少很多。注意，CNN 的卷积操作不是我们通信系统里的卷积。在通信系统里的卷积包括四步：翻转、平移、相乘、相加。CNN 的卷积没有“翻转”这一步。

第二是非线性。比如用 ReLU 函数。这和神经元加非线性的原因是一样的，也是通过增加非线性，改进模型的非线性能力。

第三是池化。这一步卷积输出的高维结果，进行采样或者平均，进一步降低它的大小，以减少模型的参数数量。

通常，为了捕捉图片的各种特性，用一个 Filter 还不够。因此，在一个 CNN 模型中，经常对一个输入，训练多个 Filter。此时，每个 Filter 就叫做一个 Channel。这些 Channel 的结果在后续层的处理中，再被神经元结合到一起。

最后，很多 CNN 层叠加在一起，构成一个 CNN 模型。

在具体的实践中，CNN 的历史已经很久了。最早是 1997 年左右 LeCun 提出的 LeNet。它被用来做手写体数字的识别。它包括卷积、池化、全连通。LeNet 的网络还比较小。此后，基于深度学习的 AlexNet 在 2012 年引起了全世界的关注。它的创新之处是引入了 ReLU、Droput、GPU。然后，VGGNet 在 2014 年发现把卷积层叠在一起就可以了，一共 138M 参数。ResNet 在 2016 年发明了 Skip 连接，让输入和梯度都快速传播，也能解决梯度消失的问题。结果是：ResNet 参数比 VGG 少：ResNet-152 有 60M 参数。

在模型训练的过程中，CNN 常采用 Batch Normalization 的方法。该方法的目的是让输入在各个维度都进行尺度变换，使其均值为 0，方差为 1。这样能够改进模型训练的有效性。具体来说，是在 FC 和卷积层后面加，加在“非线性”前面或者后面。先对一个 Mini-batch 的样本训练一下，得到均值和方差，然后用它们做归一化。归一化后，再做一个 ax+b，其中 a 和 b 是可以学习的，让它们能够统一地尺度变换和平移。

我们在日常工作中，可以利用人们训练好的 CNN 模型，提取我们图片数据的特征，然后基于这些特征，训练我们自己的分类模型。

## 课本

- Dive in Deep Learning
  - [7. Convolutional Neural Networks](https://d2l.ai/chapter_convolutional-neural-networks/index.html)
  - [8. Modern Convolutional Neural Networks](https://d2l.ai/chapter_convolutional-modern/index.html)

- 斯坦福 CS231n [CNN 介绍](https://cs231n.github.io/convolutional-networks/)

## 课程材料

- 伯克利 CNN PPT
- MIT CNN PPT
- AI4All Play - Environment PPT
- AI4All Model - CNN PPT

## 体验

- Andrej Karpathy 开发的基于卷积神经元网络的图片分类任务的[网站](https://cs.stanford.edu/people/karpathy/convnetjs/demo/mnist.html)，获得直观体验。

## 示例

- Berkeley DeepRL Camp Lab 2: Introduction to Chainer. You will implement deep supervised learning using Chainer, and apply it to the MNIST dataset. [website](https://sites.google.com/view/deep-rl-bootcamp/labs)

## 练习

- AI4ALL MNIST Mini-Project, CNN handwritten digit recognition, [Colab](https://colab.research.google.com/drive/1iTn-955vrJ9Ezd-p99Ba-niIjwx_Ap10#scrollTo=G1O50g42BalH)
- AI4ALL CIFAR-10 Mini-Project Students, [Colab](https://colab.research.google.com/drive/1KTQQxkj37_2dydQee4uI4j-kEPl1WKOp)

<br/>

|[Index](./) | [Previous](1-5-train) | [Next] (3-5-vis)
