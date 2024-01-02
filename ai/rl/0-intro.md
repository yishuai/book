---
layout: post
title: 决策制定
---

本节我们学习 Decision making 的 AI 算法。

我们首先学习静态决策制定的 Decision networks。我们分析影响决策的各种因素，建立它们之间的关系、它们和决策目标的关系、它们对效用的影响，量化评估各种方案的效用，做出最佳决策，并能定量地得到各种信息的价值。

我们然后学习序列决策制定。有大量的应用都是这种决策，比如机器人、投资、运营。这包括三种类型算法：

第一种是 Markov Decision Processes。这时，我们已知 Transition 和 Reward 模型，想要获得最优策略。我们学习两种算法：值回归和策略回归。

第二种是增强学习（Reinforcement learning）。当 Transition 和 Reward 模型未知时，我们要通过实验，与环境交互，来找到最优策略，让 Reward 最大，这就是增强学习。我们会学习很多算法，包括学习状态的值函数 V(s)、Q-learning、深度增强学习（包括 Gradient Q-learning、Deep Q-Network：DQN）、Policy Gradient（REINFORCE）、Actor Critic（Advantage Actor Critic：A2C、Deep Deterministic Policy Gradient：DDPG）、TRPO（PPO）。在增强学习中，Reward 的设计特别重要，因此，我们然后学习它。我们然后介绍 RL 的各种应用，以及在训练过程中的技巧。我们然后学习增强学习最近的进展，这包括：基于模型的模型，Offline 模型，基于约束的模型，概率分布模型，反向增强学习，序列模型，多任务迁移学习，元学习。

第三种是 Multi-armed bandits 算法。当系统有多个选项，每个选项只有一个状态，但 Reward 不可知时，我们需要通过实验找出 Reward 最大的选项。当我们不利用问题的上下文信息时，我们有基于频率统计的$$\epsilon$$-贪婪算法、UCB 算法和基于贝叶斯的 Thompson 采样方法；当我们利用这些上下文信息时，我们有 Contextual Bandit 算法。

我们最后学习 Game theory。我们学习如何建立游戏的 Agent - Action - Utility 范式，然后研究 Agent 的“战略”。我们学习“Dominant”战略、确定动作选择下的战略纳什均衡、Pareto 最优、囚徒困境，以及混合战略下的纳什均衡。

## 学习材料

- Berkeley CS285 DRL Lec 1: Introduction and Course Overview, [Slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)

<br/>

|[Index](index) | [Next](1-resource) |

