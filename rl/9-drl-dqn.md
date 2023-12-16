---
layout: post
title: 深度增强学习和 DQN
---

当系统状态 S 很多时，比如围棋、游戏，Tabular 的 Q-learning 方法就无法实现了。这时，我们需要用深度学习模型，获得关于系统状态的深度模型。这就是深度增强学习。

具体来说，我们把 S 映射到向量上，把 Q 变成它的函数，然后用梯度下降的方法进行优化。这就是 Gradient Q-learning。当我们用神经元网络近似时，模型的非线性使模型的收敛并不容易，因此，我们通过 Experience Replay 和 Target Network 两个方法来训练它。这就是 Deep Q-Network（DQN）。DQN 成功地解决了各种我们熟悉的街机游戏（比如坦克大战）的问题。

### Gradient Q-Learning

当 S 很多时，怎么办呢？比如围棋，有 $$3^{361}$$ 种状态，或者游戏：它的界面图像有无数种状态。

这时，我们要把 s 和 a 映射到向量上，然后把 Q 变成它们的函数，用神经元网络近似，这就是 Gradient Q-Learning。它的算法如下图所示：

![](fig/gradient-q-learn.png)

如上图所示，我们还是像 Q-Learning 那样，在当前状态 s 下，根据策略，执行动作 a 之后，用下一个进入的状态的 s‘ 的各个 Action 中的最大 Q 值，经过衰减后，加上这次执行 a 获得的 Reward r，用它来近似 s 的 Q 函数。因此，近似误差就是它与真正的 Q 函数之间的 MSE。这就是神经元网络的 Loss 函数。将它对 w 求导，就得到了梯度，然后进行梯度下降，优化模型参数 w。

非线性 Gradient Q-Learning 会不收敛。直觉上，这是因为通过调整 w 来增加一对 s 和 a 的 Q 函数，不可避免地会影响这对 s 和 a 的邻居的 Q 函数。为此，实际中，我们有两个技巧来减少它跑飞（Divergence）：

第一个技巧是 Experience Replay。它把很多历史的经验 <s,a,s',a'> 先存下来。然后在训练时，从中随机地选取一批数据，基于它们进行训练。这种方法也叫 Replay buffers。这是因为连续实验时，相邻的样本之间会相关。因此，不能依靠连续的样本来训练。用 Replay Buffers 能够打破这种相关。

第二个技巧是 Target Network。它用一个另外的“目标网络”，周期地提取一个历史经验 <s,a,s',a'> 的 mini-batch，对它进行梯度更新。这是因为我们做 Online Q 函数的迭代时，Q 函数一直在变化，这时，我们用 Replay Buffer 中的以前的数据来训练，这些数据和最新的模型就对不上。所以，我们新加一个不经常更新的“目标网络”。这样能够改进模型训练的稳定性。

上面两个技巧的部分内容，请参考伯克利 CS182 的 PPT。

我们把深度神经元网络、Experience Replay、Target Network 用于 Gradient Q-Learning，这就是 DeepMind 提出的 Deep Q-network（DQN）。这个方法打游戏特别好用，比如我们熟悉的街机小游戏。

DQN 的算法如下图所示：

![](fig/dqn.png)

如上图所示，它和 Tabular Q-Learning 类似，但是加入了 Experience Replay 和 Target Network。

DeepMind 用于打游戏的 DQN 网络的结构如下：它首先通过 CNN 得到游戏状态（即界面上的图像显示）的深度表征，然后用“全联通网络”将其映射为游戏的操作动作。然后整个算法通过上述算法进行优化，取得了非常好的效果。

## 实现

对 DQN 的应用，伯克利 CS182 的 PPT 有以下建议：

首先，对连续 Action，有下面两方面建议：

第一，在深度模型的设计上，对连续 Action，我们可以把 S 和 a 输入深度学习模型，输出 Q 值；对离散 Action，我们可以输入 S，然后用多任务输出：每个 Action 输出一个 Q 值。

第二，在算法选择上，对连续 Action，我们用 DQN 选择 Action 进行实验时，可以选择的值太多了。此时，我们可以用后面将要学习的 AC 算法，只是把 AC 算法的 V 函数换成 Q 函数。这样来做，比较简单。

然后，在训练的过程中，因为模型不容易收敛，所以需要小心的编码。建议先在一个容易的、可靠的任务上先实验评估，确保自己的代码是对的，然后再在自己的复杂任务上跑算法。

此外，采用大一点的 Replay buffer 会帮助改进稳定性。

然后，训练刚开始的时候，模型很可能表现很差，就像随机工作似的。这时不要着急。它很可能后面就会找到突破口，然后有好的表现。

最后，可以刚开始用较高的探索（epsilon），然后逐渐减少。

## 示例

我们介绍两个例子：

最著名的例子是上面提到的 DeepMind 的例子。这是 2013 年 DeepMind 的《Human-level control through deep reinforcement learning》工作。它解决了采用 Q-learning with CNN，使用了 replay buffer，target network、One-step backup、One gradient step 等技巧，后续还可以被 double Q-learning 等各种技巧改进。

伯克利 CS182 还提到作者的一个例子《QT-Opt: Scalable Deep Reinforcement Learning of Vision-Based Robotic Manipulation Skills》，它能够控制机器人，做大规模的 Q Learning。

## 课程材料

- 滑铁卢大学 CS486 人工智能 Deep Reinforcement Learning slides
- 伯克利 CS182 深度学习，Actor Critic PPT，[B 站视频](https://www.bilibili.com/video/BV1PK4y1U751?p=48)，讨论材料 9
- Berkeley CS285 Lec 8: Deep RL with Q-Functions, [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)
- Stanford CS234 RL Lecture 5/6: RL with function approximation
- Silver RL 2015 Lec 6: Value Function Approximation [website](https://www.davidsilver.uk/teaching/), [video](https://www.youtube.com/watch?v=2pWv7GOvuf0)
- DeepMind UCL Hadovan RL 2021 Lec 7 Function approximation in reinforcement learning 

## 课本材料

- Deep Reinforcement Learning ([slides](https://cs.uwaterloo.ca/~ppoupart/teaching/cs486-spring23/slides/cs486-lecture18.pdf) , [annotated slides](https://cs.uwaterloo.ca/~ppoupart/teaching/cs486-spring23/slides/cs486-lecture18-annotated.pdf))
- [GBC] Chap. 6,7,8
- [SutBar] Sec. 9.3, 9.4, 9.6, 9.7
- [Sze] Sec. 4.3.2

## 练习

- Denny Britz + Silver RL 2015 Lab 6
- 伯克利 RL bootcamp 2017 Lab 2 Chainer，Lab 3 DQN
- 伯克利 CS182 DL MuJoCo implement Imitation learning, Policy Gradients, DQN, and Actor Critic algorithms.
- Stanford CS234 DRL Assignment 2 DQN
- 滑铁卢 CS486 [练习 4](https://cs.uwaterloo.ca/~ppoupart/teaching/cs486-spring23/assignments.html)
  -  DQN 练习：Part 3: DQN implementation - dqn_agent.py
  -  Part 3: Main script to run DQN implementation - main.py
- CS885 [练习 1](https://cs.uwaterloo.ca/~ppoupart/teaching/cs885-fall22/assignments.html)，CartPole DQN
- Berkeley DeepRL Camp Lab 3: Deep Q-Learning. You will implement the DQN algorithm and apply it to Atari games. [website](https://sites.google.com/view/deep-rl-bootcamp/labs)
- CartPole 问题，修改代码，更改“目标网络”的更新频率、样本mini-batch数目：
  - 问题描述：https://www.gymlibrary.dev/environments/classic_control/cart_pole/
  - 代码描述： https://blog.gofynd.com/building-a-deep-q-network-in-pytorch-fa1086aa5435

## 论文

DRL 是目前的研究热点。因此，我们可以读最新的学术论文，获得更深的理解：

下面是斯坦福 CS 224R 提到的论文：

Q-Learning
- Playing Atari with Deep Reinforcement Learning. Mnih et al. (2013)

Practical Deep RL Implementation Techniques
- Deep Reinforcement Learning with Double Q-learning. Hasselt et al. (2015)
- QT-Opt: Scalable Deep Reinforcement Learning for Vision-Based Robotic Manipulation. Kalashnikov et al. (2018)
    - Large-scale Q-learning with continuous actions (QT-Opt)
    - Based Robotic Manipulation Skills

下面是伯克利 DRL 课程提到的论文：

Classic papers
- Watkins. (1989). Learning from delayed rewards: introduces Q-learning
- Riedmiller. (2005). Neural fitted Q-iteration: batch-mode Q-learning with neural networks

Q-learning papers
- Lange, Riedmiller. (2010). Deep auto-encoder neural networks in reinforcement learning: early image-based Q-learning method using autoencoders to construct embeddings
- Mnih et al. (2013). Human-level control through deep reinforcement learning: Q- learning with convolutional networks for playing Atari.
- Van Hasselt, Guez, Silver. (2015). Deep reinforcement learning with double Q-learning: a very effective trick to improve performance of deep Q-learning.
- Lillicrap et al. (2016). Continuous control with deep reinforcement learning: continuous Q-learning with actor network for approximate maximization.
- Gu, Lillicrap, Stuskever, L. (2016). Continuous deep Q-learning with model-based acceleration: continuous Q-learning with action-quadratic value functions.
- Wang, Schaul, Hessel, van Hasselt, Lanctot, de Freitas (2016). Dueling network architectures for deep reinforcement learning: separates value and advantage estimation in Q-function.

Q-learning on a real robot
- “Robotic manipulation with deep reinforcement learning and …,” Gu*, Holly*, et al. ‘17
  - Continuous actions with NAF (quadratic in actions)
  - Uses replay buffer and target network
  - One-step backup
  - Four gradient steps per simulator step for efficiency
  - Parallelized across multiple robots

Q-learning with continuous actions
- “Continuous control with deep reinforcement learning,” Lillicrap et al. ‘15
  - Continuous actions with maximizer network
  - Uses replay buffer and target network (with Polyak averaging)
  - One-step backup
  - One gradient step per simulator step

Fitted Q-iteration in a latent space
- “Autonomous reinforcement learning from raw visual data,” Lange & Riedmiller ‘12
  - Q-learning on top of latent space learned with autoencoder
  - Uses fitted Q-iteration
  - Extra random trees for function approximation (but neural net for embedding)

<br/>

|[Index](index) | [Previous](7-rl-q-learn) | [Next](10-imitation) |
