---
layout: post
title: TRPO 和 PPO
---

在策略调整后，能不能用上策略调整前的大量的实验结果，进行优化。TRPO 和 PPO 就是这样的方法。

## Off-Policy PG 学习

策略梯度的工作方式是 On-Policy 的，即：每次更新完策略模型的参数后，我们会抛弃以前的、基于老的策略模型获得的实验数据，然后基于新的策略模型，进行大量实验，收集数据，并基于这些全新的数据，进行训练。那这就有一个不足：就是新的模型，其实和老模型差不多，所以，我们把老模型的数据全部丢掉，岂不浪费了这些宝贵的实验数据？能不能把它们也用上呢？

基于以前的老模型数据进行训练，这可以被称为 Off-Policy 学习。我们通过 Importance Sampling 来实现。具体来说，当我们用老模型的轨迹数据，来估计新模型下一个轨迹的 Reward 时，我们对这个轨迹的概率进行加权：如果在新模型中这个轨迹出现的概率更高，那么就认为这个轨迹“更重要”，因此，在估计它的 Reward 时，用一个比它在老模型中获得的 Reward 更高的值。这就是 “Importance Sampling”。

在实际中，“Importance Sampling” 很好用：用老模型的数据时，我们就做上面的加权；用新模型的数据时，我们就把权重设为 1 就好了。其它和经典的 PG 都一样。

这样，我们就得到了 Off-Policy 的 PG 算法。在这里，我们又可以引入技巧“考虑因果”，即：在加权梯度时，只考虑 t 之前的 Action 的 Importance，因为，t 之前的轨迹只包括它们；在计算 Reward 时，页类似。这就是“考虑因果”的技巧。

在实际中，当序列很长时，把很多 Action 的 Importance 比值相乘，很可能会变得很小很小。所以，实际中就用当前 t 的 Importance 代替了。这就是所谓的“一阶近似”。在实际中，用得很普遍。

此时的模型也非常好实现，就把我们前面看过的有监督的策略学习方法的模型稍微改改就行，还是一个经典的深度学习模型。具体来说，有监督的策略学习方法的模型的目标函数，是以专家 Action 为目标 Label，以模型输出的 Softmax 为模型结果，计算两者的交叉熵。而我们现在的 Action 就是当前尝试的 Action；而目标函数要做两个加权：第一个权重是“值函数”；第二个权重是 “Importance Sampling”，因此，我们简单地把交叉熵乘这两个权重就可以了。然后还是最大化该目标函数。具体代码，请参考伯克利 CS182 的 PPT。

## 可信区方法

我们下面学习上述方法的一种更形式化的描述，即“可信区”方法。

PG 方法在更新策略模型的参数时，很难设置步长。因此，我们想转而优化一个 surrogate （代理）的目标函数：V。

通过 Surrogate 目标进行优化，一般仅仅在初始位置周围的一个小区域内搜索才 trustable（可信），所以，我们一般会把搜索的范围，限制在这个小的可信区域内。这就是本节要采用的“可信区”的基本概念。

因此，我们需要定义一个能够被用来判断是否还在“可信区”内的评估指标。这个指标可以是模型参数，也可以是模型的结果（即“策略”）。实验表明：模型参数稍微改一点，V 就会改变很大；而输出策略稍微改一点，V 也只稍微改一点。因此，我们用“输出策略”作为评估指标。所以，我们就是希望模型在输出策略旁边的可信区搜索。具体来说，我们用 KL 散度来描述我们搜索的策略和原策略的“距离”。

## Trust Region Policy Optimization (TRPO)

下面我们进行这种基于 Policy 的“可信区”的优化策略，即 Trust Region Policy Optimization（TRPO）

我们首先写出我们的优化目标函数。因为用 V 作为 Surrogate，所以，它就变为了：在各种初始状态下，让 V 尽可能增大（即新策略的 V 减去旧策略的 V）的模型参数。我们然后加一个约束条件，就是在这个新模型参数下的新策略，得在原策略的“可信区”内。这样，我们就把问题变成了对 V 的优化问题，但加上 Policy 的“可信区”限制。

在实际中，对目标函数，我们用实验测量的，各个状态下的各个 Action 的新/旧策略的模型输出概率的比值作为权重，去加权它们的 Advantage 函数，近似作为优化的目标函数。我们可以将它进行推导，证明它近似我们的原始目标函数。详见 PPT 上的推导过程。而对约束条件，我们用各个状态下的 KL 散度的均值，作为约束条件。

这就是著名的 TRPO 算法。请看 PPT 上的算法描述。如 PPT 所示，我们像 A2C 算法似的，也计算 Advantage，更新 Q 函数。不同的是，我们现在不再用A2C 的 Advantage 加权的方法，做梯度上升，更新模型参数 $$\theta$$，而是用新的目标函数，去做梯度上升，增加 Advantage 高的 Action 的权重，同时限制策略得在“可信区”内。

TRPO 还用来“自然梯度”、“自动步长调节”，能够支持离散和连续的 Action。这些也是它的重要特点。

## Proximal Policy Optimization (PPO)

TRPO 的问题是基于策略的 KL 散度的约束条件，实现起来很困难。因此，人们对它进行简化：不再约束散度，而是直接约束策略输出的 Action 概率的变化幅度。具体来说，我们通过 Clip 函数，把策略输出的 Action 概率的变化幅度“硬性地”控制在 1 的左右。如果 Action 概率的变化幅度太大，我们的目标函数就不考虑它了。这就是 PPO 算法。

实验证明，PPO 方法工作的效果是最好的。它也是目前应用得最广的算法，比如 ChatGPT 里的 RLHF 就是用的这种算法。所以，一定要掌握哦。

## 小结

本节我们学习了 TRPO：信任区域最近策略算法。它以 V 为优化目标，以策略“可信区”约束搜索的范围。因此，它以各状态下的各 Action 的新/旧策略的模型输出概率比为权重，计算它们的 Advantage 的加权和，作为优化目标，而以它们的策略 KL 散度为约束，这就是 TRPO 算法；PPO 进一步简化了约束条件，把策略变化太大的情况直接 Clip，大大简化了计算，成为 ChatGPT 采用的增强学习算法。

## 课程材料

- 滑铁卢大学 CS885 人工智能 Trust Regions, Proximal Policies slides
- 伯克利 CS182 深度学习，Policy Gradient PPT，[B 站视频](https://www.bilibili.com/video/BV1PK4y1U751?p=45)，讨论材料 9
- Berkeley Deep RL Bootcamp 2017, Lecture 5, Natural Policy Gradients, TRPO, and PPO -- John Schulman ([video](https://www.youtube.com/watch?v=xvRrgxcpaHY) | [slides](https://drive.google.com/file/d/0BxXI_RttTZAhMVhsNk5VSXU0U3c/view?usp=sharing&resourcekey=0-6NrgDm29IIPlXsPESX2w4w))

## 课本材料

- [SutBar] Chap. 2

## 练习

- 上海交大伯禹增强学习 练习 第11章-TRPO算法.ipynb
- 上海交大伯禹增强学习 练习 第12章-PPO算法.ipynb
- 上海交大伯禹增强学习 练习 第13章-DDPG算法.ipynb
- 伯克利 RL bootcamp 2017 Lab 4 PG
- CS886 [练习 2](https://cs.uwaterloo.ca/~ppoupart/teaching/cs885-fall22/assignments.html)，REINFORECE with a baseline，PPO
- Berkeley DeepRL Camp Lab 4: Policy Optimization Algorithms. You will implement various policy optimization algorithms, including policy gradient, natural policy gradient, trust-region policy optimization (TRPO), and asynchronous advantage actor-critic (A3C). You will apply these algorithms to classic control tasks, Atari games, and roboschool locomotion environments. [website](https://sites.google.com/view/deep-rl-bootcamp/labs)
- Stanford CS234 DRL Assignment 3 PPO

## 论文

斯坦福 论文

- Schulman, Levine, Moritz, Jordan, Abbeel (2015) Trust Region Policy Optimization, ICML. 
- Schulman, Wolski, Dhariwal, Radford, Klimov (2017) Proximal Policy Optimization, arXiv.

伯克利论文

Deep reinforcement learning policy gradient papers
- Levine & Koltun (2013). Guided policy search: deep RL with importance sampled policy gradient (unrelated to later discussion of guided policy search)
- Schulman, L., Moritz, Jordan, Abbeel (2015). Trust region policy optimization: deep RL with natural policy gradient and adaptive step size
- Schulman, Wolski, Dhariwal, Radford, Klimov (2017). Proximal policy optimization algorithms: deep RL with importance sampled policy gradient

## 最新论文

- Pairwise Proximal Policy Optimization (P3O), Dec 2023， 伯克利 BAIR， RLHF 是基于“比较”的，因此，改进 PPO 支持比较，[Blog](http://bair.berkeley.edu/blog/2023/10/16/p3o/)

<br/>

|[Index](index) | [Previous](13-actor-critic) | [Next](17-reward) |
