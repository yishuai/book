---
layout: post
title: 增强学习
---

我们下面学习增强学习（Reinforcement learning）。

当 Transition 和 Reward 模型未知时，我们要通过实验，与环境交互，来找到最优策略，让 Reward 最大，这就是增强学习。

因为不知道 Transition 和 Reward 模型，所以，我们需要通过实验，然后从实验结果中“学习”，来进行决策制定。所以，它是一种从经验中学习决策和控制的方法。

强化学习的特点是：
- 数据不是独立同分布：之前的输出影响未来的输入！
- 真实答案未知，只知道如果我们成功或失败。更一般地说，我们知道 Reward。

为此，增强学习引入了如下重要 Idea：
- 探索（Exploration）：你必须尝试未知的行动才能获得信息
- 利用（Exploitation）：最终，你必须使用你所知道的
- 悔恨（Regret）：即使你学得很聪明，你也会犯错误
- 抽样（Sampling）：因为随机，所以必须反复尝试

也因此，增强学习比解决已知的 MDP 困难得多。

我们首先学习如何从实验中学习每个状态的值函数 V(s)。有两个办法：蒙特卡洛评估方法和 Temporal Difference 评估方法。

我们然后学习 Q-learning。我们通过实验获得状态 s 下执行特定策略下的动作 a 时的价值（Value）Q(s,a)。当获得了 Q 函数后，我们就可以选择值最大的 Action，实现“控制”（Control）。类似于从实验中学习 V(s)，我们可以用蒙特卡洛评估方法和 Temporal Difference 评估方法来学习 Q 函数。这就是 Q-learning。在 Q-learning 的学习中，我们需要平衡 Action 的“探索”和“利用”。

我们然后学习深度增强学习（DRL）。这适用于系统的状态 S 很多的情况，比如围棋、游戏。这时，我们把 S 映射到向量上，把 Q 变成它的函数，然后用梯度下降的方法进行优化。这就是 Gradient Q-learning。当我们用神经元网络近似时，模型的非线性使模型的收敛并不容易，因此，我们通过 Experience Replay 和 Target Network 两个方法来训练它。这就是 Deep Q-Network（DQN）。DQN 成功地解决了各种我们熟悉的街机游戏（比如坦克大战）的问题。

我们然后学习策略梯度（Policy Gradient）方法。它直接学习策略模型。通过 Log 技巧，它以测量获得的 reward 为权重，对策略模型的输出 Action 概率 Log 后对模型参数的导数进行加权，这样就能增强能够让 Reward 增加的梯度。这就是“增强学习”的含义。REINFORCE 就是这样的一种算法。

我们然后学习 Actor Critic 方法。它在策略梯度方法中，引入 Value 函数，用它来改进对策略的权重。具体来说，Actor Critic 通过 Temporal Difference 方法，改进了对 Reward 的估计，让算法更加稳定；Advantage Actor Critic（A2C）引入 Advantage，提高算法的收敛速度；而 Deep Deterministic Policy Gradient (DDPG) 适用于 Action 连续的情形，它集各种方法之大成，能够被用来控制机器人。

我们然后学习 TRPO：信任区域最近策略算法。它以 V 为优化目标，以策略“可信区”约束搜索的范围。因此，它以各状态下的各 Action 的新/旧策略的模型输出概率比为权重，计算它们的 Advantage 的加权和，作为优化目标，而以它们的策略 KL 散度为约束，这就是 TRPO 算法；PPO 进一步简化了约束条件，把策略变化太大的情况直接 Clip，大大简化了计算，成为 ChatGPT 采用的增强学习算法。

基于纯粹实验的 Q-learning 方法需要做大量实验，效率不高，因此，我们提出基于模型的增强学习，即：通过实验，学习 Transition 和 Reward 模型，然后用这些模型生成样本，基于这些样本，做值回归、策略回归、Gradient Q-learning。在生成样本的过程中，因为状态特别多，我们用 Partial Planning 和蒙特卡洛树搜索，优化搜索空间。

## 课程材料

- Berkeley CS285 Lec 4: Introduction to Reinforcement Learning, [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)
- Stanford CS234 RL 
  - Lecture 1/2: Introduction to Reinforcement Learning
  - Lecture 3: Tabular RL policy evaluation
- Silver RL 2015 Lec 4: Model-Free Prediction [website](https://www.davidsilver.uk/teaching/), [video](https://www.youtube.com/watch?v=2pWv7GOvuf0)
- DeepMind UCL Hadovan RL 2021 
  - Lec 5 Model Free Prediction
  - Lec 6 Model-free control
- 上海交大伯禹增强学习 Lec 1 强化学习简介
- 上海交大伯禹增强学习 Lec 17 3小时强化学习基础课件
- 上海交大伯禹增强学习 Lec 3 值函数估计
- 上海交大伯禹增强学习 Lec 4 无模型控制
- 上海交大伯禹增强学习 Lec 5 规划与学习
- 上海交大伯禹增强学习 Lec 6 近似逼近方法

## 课本材料

- SB (Sutton and Barto) Chp 5.1, 5.5, 6.1-6.3

## 练习

- Denny Britz + Silver RL 2015 Lab 4-5
- 上海交大伯禹增强学习 练习 第16章-模型预测控制.ipynb

<br/>

|[Index](index) | [Previous](5-mdp) | [Next](7-rl-q-learn) |
