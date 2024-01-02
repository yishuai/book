---
layout: post
title: 博弈论
---

博弈是多个 Agent 的智能决策问题。我们前面学习的马尔可夫决策过程是“单个” Agent 的决策制定。我们下面学习“多个” Agent 的决策制定。

在多 Agent 的决策制定中，每个 Agent 会考虑其他 Agent 的行为，来决定自己的行为。我们把这种问题称为“游戏”。怎么样，大家喜欢玩游戏吧？那大家肯定喜欢这一章。

在现实世界中，我们遇到的很多问题都是多 Agent 的决策制定问题。比如：竞拍、外交、体育、自动驾驶、公共福利等。

本节我们学习 Game theory。我们学习如何建立游戏的 Agent - Action - Utility 范式，然后研究 Agent 的“战略”。我们学习“Dominant”战略、确定动作选择下的战略纳什均衡、Pareto 最优、囚徒困境，以及混合战略下的纳什均衡。

## 游戏的 Utility 和分类

我们首先建立多 Agent 决策制定问题的数学模型。我们引入 Utility 函数的定义。每个 Agent 都有自己的 Utility。

基于一个游戏中的各个 Agent 的目标类型，可以分成以下三类：

第一类，如果一个游戏中的各个 Agent 有一个共同的 Utility，那这个游戏叫做“合作游戏”。比如 Hanabi（花火）游戏就是一种合作卡牌游戏。玩家不能观看自己的牌，只能看其他玩家的。大家有一个共同的目标，就是将不同花色的数字牌顺序排列完成并成功施放「花火」。玩家只能通过每回合有限的资讯，透过推理、整合和默契等来完成游戏。2013年，花火荣获德国游戏大奖，获得业界权威认可。

第二类，如果一个游戏中大家的 Utility 是冲突的，那这个游戏就是“竞争游戏”。比如下象棋。

第三类，如果一个游戏中大家即有合作，又有竞争，那就是“混合游戏”。

## 游戏的范式

我们然后给出游戏的“范式”，它包括 i：Agent，A：Action，U：Utility。我们把各个 Agent 的各种 Action 组合的 Utility 用矩阵的形式给出，就是这个游戏的 “Payoff 矩阵”。

如果在 “Payoff 矩阵” 的每一个格子里，各个 Agent 的 Utility 加起来，总和为 0，那这个游戏就是 “零和游戏”。“零和游戏”是比较残酷的，但也有很多不是“零和”的游戏。

我们下面来“玩”我们的“游戏”。首先，当然是制定游戏的“玩法”。我们要求 所有的 Agent 同时动作；它们互相之间没有沟通；它们在动作时，看不到其他人的动作。

我们的研究目标是：找到每个 Agent 的“战略”（Strategy）。这个战略可以是“混合”的，即以一定的概率，在一组动作中，随机选择；也可以是“纯粹”（Pure）的，即只会确切地执行一个动作。

我们的目的是：给每个 Agent 都找到一个“战略”。所有 Agent 的战略组合，就是一个“战略 Profile”。在一个战略 Profile $$\sigma$$下，Agent $$i$$获得的 Utility 记作 $$u_i(\sigma)$$。

## Dominant 战略均衡

我们首先确定一个 Agent 是否有 Dominant 战略，即：它在这个战略下获得的 Utility，在各种战略 Profile 下，是最优的；而且，比它的某一个战略获得的 Utility 要高。这种战略，就叫做 Dominant 战略；而其他战略，就叫做 Dominated 战略。显然，一个 Agent 会执行自己的 Dominant 战略。

当所有 Agent 都执行自己的 Dominant 战略时，我们说它们到达了基于 Dominant 战略的“均衡”（DSE）。此时，我们说这个游戏是 Dominance 可解的。

有时，虽然从初始范式中达不到 DSE，但在假设“Agent 是理性”的情况下，Agent 可以排除掉对方选择一些 Action 的可能。在结果的范式中，可能又有 DSE 了。详见课程 PPT。

## 纯战略纳什均衡

一个没有 DSE 的游戏，可能有 Nash 均衡。我们首先讨论“纯粹”（Pure）动作下的情形，即只会确切地执行一个动作。

为了理解 Nash 均衡，我们首先引入 Best Response 的概念。它指的是：已知其他人的战略的条件下，让一个人的 Utility 最大的战略。

那么，Nash 均衡是指这样一种战略 Profile：其中的每个 Agent 的战略，都是当前战略 Profile 的 Best Response。也就是说：Agent 此时没有动机去采取其它战略了。这时，就达到了均衡。详见课程 PPT 中的例子。一个游戏中的 Nash 均衡可能有很多。

要找到一个游戏中的 Nash 均衡，有两种办法：一种是从一个初始策略出发，通过迭代，找到它；另一种是固定一个 Agent 的策略，然后找到其它 Agent 的 Best Response。详见课程 PPT。

## Pareto 最优

要理解 Pareto 最优，我们首先定义 Pareto Dominance。它被用来比较两个策略 Profile A 和 B，即：我们说 A Pareto Dominate B，是说在 A 下，任何一个 Agent 的 Utility 都不低于 B 时它的 Utility，而且，有些 Agent 的 Utility 要高。

然后，如果没有其它策略 Profile Pareto Dominate A，我们就说 A 是 Pareto 最优的。注意，不是说策略 A Pareto Dominate 所有其它策略 Profile。

## 囚徒困境

我们下面分析囚徒困境。

我们首先分析囚徒困境的游戏中，Agent 是否有 Dominant 战略，即：它在这个战略下获得的 Utility，在各种战略 Profile 下，是最优的；而且，比它的某一个战略获得的 Utility 要高。我们发现，对 Bob 来说，他 Defect 是 Dominant 策略；对 Alice 来说，也同样如此。所以，Defect，Defect 是 Dominant 策略 Profile。

我们然后分析囚徒困境的游戏中，是否有 Nash 均衡，即其中的每个 Agent 的战略，都是当前战略 Profile 的 Best Response。也就是说：Agent 此时没有动机去采取其它战略了。这时，就达到了均衡。我们采用一个初始策略出发，迭代搜索的方法。假设从 Cooperate，Cooperate 出发，此时，Bob 有动机 Defect，到达 Cooperate，Defect；此时，Alice 有动机 Defect，到达 Defect，Defect。然后，到了 Defect，Defect，大家就都没有动机再改变了。所以，Defect，Defect 就是囚徒困境的 Nash 均衡；

我们最后分析囚徒困境的 Pareto 最优，即：是否有一个策略 Profile，没有其它策略 Profile Pareto Dominate 它呢？比如 Cooperate，Cooperate，就没有其它 Profile Dominate 它。Cooperate，Defect 也是如此；所以，它们都是 Pareto 最优。但 Defect, Defect 不是如此，有 Cooperate, Cooperate Dominate 它。

注意，Pareto 最优不是说策略 A Pareto Dominate 所有其它策略 Profile。如果按这个定义，那么 Cooperate，Defect 就不是 Pareto 最优了。所以，Pareto 最优的含义是，不能在不伤害一个人的情况下，改善另一个人。这时，就是 Pareto 最优了。

因此，囚徒困境的 DSE 和 Nash 均衡，不是 Pareto 最优的。

## 混合战略 Nash 均衡

“纯战略” Nash 均衡只允许 Agent 确切地执行一个动作。我们下面考虑“混合战略”的 Nash 均衡。

以“匹配硬币”游戏为例。此时，一个人想“相同”，另一个人想“不同”。那么，我们可以猜测对方的动作概率，然后做出最优选择。

我们首先修改此时的 Best Response 定义，把它变为：此时，每个 Agent 的策略的 Utility 期望，在当前其它 Agent 的策略情况下，都是最高的。Nash 老师证明：每个有限步骤的游戏，至少有一个这样的 Nash 均衡。这就是 Nash 定理。

我们可以证明，对“匹配硬币”的游戏，Alice 和 Bob 的混合战略 NE，是他们以 0.5 的概率出 Head，0.5 的概率出 Tail。怎么求出它呢？Alice 要找一个出 Head 的概率，让 Bob 出什么，Utility 都一样；类似的，Bob 也要找一个出 Head 的概率，让 Alice 出什么都不会 Utility 都一样；因此，在这个策略下，Alice 就可以随意出。当然，Bob 也可以随意出。这就达到了 Nash 均衡。

请完成 PPT 中的“舞会还是音乐会”的例子，进一步理解混合策略下的 Nash 均衡。

## 小结

本节我们学习了 Game theory。我们学习如何建立游戏的 Agent - Action - Utility 范式，然后研究 Agent 的“战略”。我们学习“Dominant”战略、确定动作选择下的战略纳什均衡、Pareto 最优、囚徒困境，以及混合战略下的纳什均衡。

## 课程材料

- 滑铁卢 Game Theory II slides 1 and 2
- Silver RL 2015 Lec 10: Case Study: RL in Classic Games [website](https://www.davidsilver.uk/teaching/), [video](https://www.youtube.com/watch?v=2pWv7GOvuf0)

## 课本材料

- [RN3] Sections 17.5

<br/>

|[Index](index) | [Previous](87-context-bandit) | [Next](101-multi-agent) |
