---
layout: post
title: 启发式算法
---

经典的 MAB 问题求解主要是在“探索”和“利用”之间试图兼顾。

## MAB 问题

当 s 只有一个的时候，这时的 RL 问题就叫 Bandits 问题。因为只有一个 s，所以，我们不需要学习 Transition 函数，只需要学习 Reward 函数。我们认为这个 Reward 函数是随机的。

老虎机就是一个 Bandits 问题。它只有一个状态。这个状态决定它吐钱的概率。老虎机有多个把手（Arm），每个 Arm 代表一个 Action。所以，Bandits 问题常被称为 Multi-Armed Bandits （MAB）问题，其中的 Actions 被形象地称为 Arm。

MAB 问题的本质是：我们需要进行尝试，来学习系统的这个状态 s。我们期望在这个过程中，获得的 Reward 最大。

除了模型老虎机，MAB 在实际中有广泛的应用，比如实验设计（临床试验）、在线广告投放、网页个性化、推荐系统、网络（数据包路由）。

遗憾的是，MAB 没有一个已知的 Tractable 的最优方案。

## 启发式算法

我们首先介绍两个简单的启发式方法：一个是 Greedy 策略，它总是优先执行那些目前发现最好的 Action；一个是 $$\epsilon$$-greedy，它有一定的概率 $$\epsilon$$，去探索那些不是最好的 Action。这个 $$\epsilon$$ 一般等于 1/t。t 是实验次数。

我们然后介绍一种更好的算法：UCB（Upper Confidence Bound），它比较每个 Action 的 Reward 的置信区间的上界，选择最高的上界的 Action 执行。每个 Action 的 Reward 的置信区间可以用 Hoeffding 不等式获得。它和实验次数有关：实验次数越多，区间的范围越小。

## 课程材料

- 滑铁卢大学 CS486 人工智能 Multi-armed Bandits slides
- Berkeley CS285 Lec 13: Exploration (Part 1), [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)
- Berkeley CS285 Lec 14: Exploration (Part 2), [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)
- Stanford CS234 RL Lecture 10/11/12: Fast Learning
- Silver RL 2015 Lec 9: Exploration and Exploitation [website](https://www.davidsilver.uk/teaching/), [video](https://www.youtube.com/watch?v=2pWv7GOvuf0)

## 课本材料

- [SutBar] Sec. 2.1-2.7, [Sze] Sec. 4.2.1-4.2.2
- Bandit Algorithms Book Chapter 7.1, Chapter 35

## 练习

- CS885 [练习 2](https://cs.uwaterloo.ca/~ppoupart/teaching/cs885-fall22/assignments.html)，epsilon-greedy，UCB
- 伯克利 CS285 HW 5: Exploration and Offline reinforcement learning, [Website](https://rail.eecs.berkeley.edu/deeprlcourse/)

## 复习题

- 给出 MAB 问题的 最优策略 的 数学表达式，介绍其物理意义
- 写出 Epsilon-Greedy 算法，分析其优点和不足。它是 最优策略 吗？
- 写出 UCB 算法，分析其优点和不足。它是 最优策略 吗？

<br/>

|[Index](index) | [Previous](81-mab-intro) | [Next](85-bayes-bandit) |
