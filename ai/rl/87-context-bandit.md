---
layout: post
title: 上下文 Bandits
---

上下文 MAB 方法能够利用上下文特征，进行智能动作。前面两节学习的 Bandits 算法适用于抛硬币、掰老虎机，这种比较“傻”的游戏：就是“傻傻地”试，“硬”试出来哪个 Arm 是最优的。

那么，我们在选择 Arm 的时候，如果考虑当前问题和 Arm 的一些“属性”，是不是更好？要理解这一点，考虑下面这种情况：很多用户登陆我们的新闻网站，我们需要决定推荐“哪一篇”新闻给用户。此时，我们是不是可以基于用户的地理位置等“属性”、各个新闻的类型等“属性”，来选择Arm？在这里，“新闻”就是 Arm。

为了考虑“属性”，我们就得训练一个模型，来估计当前特定属性（包括用户属性、Arm 属性）组合下的各个 Arm 的 Reward，然后选择合适的 Arm。这就还是一个 Bandit 问题。但这个问题很特别：在机器学习的术语中，我们考虑的这些属性常被称为问题的“上下文”（Context），所以，这种 Bandit 问题被称为 Contexual Bandits 问题。

我们可以建立各种 Reward 模型。最常见的是线性模型。此时，Reward 是属性向量 x 的线性加权和。因此，我们需要根据实验获得的真实 Reward 来不断调整这个模型的参数 w，同时，利用更新过的模型，来选择新的 Arm。

类似于前一节学过的贝叶斯 Bandit 模型，我们下面建立这种贝叶斯线性回归模型。

我们用高斯分布来建立这个贝叶斯线性回归模型。具体来说，有两个高斯分布。第一个高斯分布，被用来模型 Reward：这个高斯分布的均值等于 w 和 x 的线性加权和。第二个高斯分布被用了模型第一个高斯分布的 w：我们一个 0 均值的高斯分布来模型它的分布。然后，当我们通过实验，得到了一个新的实验的 x 对应的 Reward，我们就可以通过贝叶斯公式，更新 w 的后验概率分布。因为高斯分布由它的均值和方差决定，所以，我们就更新它的均值和方差就可以了。请看 PPT 上它们的更新公式。

有了这个模型后，对新的一个 x，我们就可以利用 Reward 模型进行 UCB 或者 Thompson 采样。做 UCB 时，我们就利用上面计算得到的均值和方差就可以了；而做 Thompson 采样时，我们就要进行采样，再比较。

上述方法非常管用。微软 MSN 采用了该方法后，点击量提升了 26%，取得了很好的效益。

## 小结

本节我们学习了如何利用上下文信息，解决 MAB 问题。我们建立基于上下文特征向量的 Reward 模型，比如模型 Reward 是高斯分布，而该分布的均值是由上下文特征向量组成的线性模型。于是，我们就可以通过实验，改进对模型参数的估计，从而不断修正 Reward 模型。这就是 Contextual Bandit 模型。

## 课程材料

- 滑铁卢大学 CS885 人工智能 Contexual Bandits slides

## 课本材料

- [SutBar] Chap. 2.9

## 复习题

- 举例说明，什么是 Contextual Bandit 问题
- 写出 UCB 线性高斯 Bandit 算法，分析其优点和不足。
- 写出 Thompson 采样线性高斯 Bandit 算法，分析其优点和不足。

## 练习

- 微软 [Contexual Bandit 库](https://microsoft.github.io/SynapseML/docs/Explore%20Algorithms/Vowpal%20Wabbit/Contextual%20Bandits/)

## 论文

- Adversarial Attacks on Linear Contextual Bandits

- ICML 2021 Leveraging Good Representations in Linear Contextual Bandits

<br/>

|[Index](index) | [Previous](85-bayes-bandit) | [Next](91-game) |
