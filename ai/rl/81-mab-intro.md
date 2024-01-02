---
layout: post
title: 多臂老虎机问题
---

多臂老虎机是一种特别的决策问题：系统有多个选项，每个选项只有一个状态，但 Reward 不可知时，我们需要通过实验找出 Reward 最大的选项。这就是多臂老虎机问题：Multi-armed bandits（MAB）。

我们首先学习不利用问题的上下文信息，完全靠实验，来找出 Reward 最大的选项。为此，我们有两种方法：

第一种是频率统计的方法：$$\epsilon$$-贪婪算法、UCB 算法。这些方法会以一定的概率尝试各个 Arm，以发现好的 Arm（即 Exploitation）；也会基于实验结果，以更高的概率去掰 Reward 高的 Arm，以获得最大的收益（即 Exploration）。

第二种是基于贝叶斯的方法：Thompson 采样方法。它通过建立各个 Arm 的 Reward 的概率模型，然后通过随机抽样、比较的方法，选择 Arm。这样就自然地融合了 Exploration 和 Exploitation。实验证明它也是一种很好的方法

我们然后学习如何利用上下文信息，解决 MAB 问题。我们建立基于上下文特征向量的 Reward 模型，比如模型 Reward 是高斯分布，而该分布的均值是由上下文特征向量组成的线性模型。于是，我们就可以通过实验，改进对模型参数的估计，从而不断修正 Reward 模型。这就是 Contextual Bandit 模型。

<br/>

|[Index](index) | [Previous](51-advanced) | [Next](83-mab) |
