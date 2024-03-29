---
layout: post
title: 基带通信系统的可靠性
---

我们首先分析基带传输系统的误码率。这一分析非常有意思，也非常重要，请一定要掌握。

以 2 电平的基带系统为例。它的接收端的工作原理是：采样后，进行阈值判决。假设高斯噪声，我们建立这种基于“阈值判决“的误码率模型，如下：

我们首先求最佳阈值电平。我们写出平均误码率、判决电平、噪声功率、0/1 电平之间的函数，然后利用微积分，获得误码率最小时的最佳阈值电平。这时我们会发现这个最佳阈值电平和系统发送的 0/1 的概率是有关的：当它们的概率相同时，最佳阈值电平，就等于 0/1 电平的均值。

我们然后基于最佳阈值电平，获得误码率公式。我们会发现这个公式只和 0/1 电平的间隔，还有高斯噪声的方差有关。因为高斯噪声是零均值的，所以它的方差就是它的噪声功率。所以，这个公式也反映了误码率和信噪比的关系。

请大家理解上述公式的原理和意义，用它来分析各种码型的误码率。

在实际系统中，我们可以通过“眼图”来观察系统工作中经受的码间干扰的严重程度，然后通过“横向滤波器”来调节系统的传输函数，减少码间干扰。请学习课程 PPT，理解它们的原理和使用方法，比如横向滤波器系数的计算方法。

怎么样，理解了这么多关于基带通信系统的奇妙设计，大家觉得好玩吧？我们学习通信系统原理，最重要的是学习前辈大师的思想，体会他们创新的过程。Enjoy！

下面是 Quiz：

1. 画图分析二进制基带信号传输的抗高斯噪声性能，写出其数学表达式、最佳阈值电平方程，在图上标出 p(0)=p(1) 时的最佳阈值电平，写出此时误码率的数学表达式，证明信噪比相同时，双极性的误码率低于单极性。
1. 影响基带系统误码性能的因素有哪些？说出误码率随它们变化而变化的规律。
1. 如何产生眼图？
1. 眼图可以用来做什么？
1. 分别画出存在和不存在码间干扰的眼图，解释产生这样的图形的原因
1. 分别画出存在和不存在噪声的眼图，解释产生这样的图形的原因
1. 画出一个眼图，标出最佳取样时刻、闭合斜率、噪声边际、可抽样时间、过零失真、最大信号失真量
1. 时域均衡的作用是？
1. 画出时域均衡滤波器在基带传输系统中的位置
11. 画出利用横向滤波器实现时域均衡的原理图，为什么它被称为“迫零”调整？

<br/>

|[Index](./) | [Previous](4-9-partial) | [Next](5-3-2ask)|
