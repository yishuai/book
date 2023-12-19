---
layout: post
title: Actor Critic
---

完全基于实验 Reward 的策略梯度方法，工作很不稳定。为此，人们引入 Baseline，值函数、Advantage，改进它工作的稳定性，促进它的收敛。

本节我们学习对 PG 的各种改进。它们的共同特点是在 PG 中引入 Value 函数，利用它，改进 PG 的梯度加权方法，使算法在训练中更稳定、更快收敛。

我们首先回顾一下 PG 的梯度加权方法。PG 的核心是利用测量获得的 Reward 有针对性地增强/弱化当前策略的 Action 选择。具体来说，就是在 Policy 的梯度下降，寻找最优策略时，用一个策略的 Action 的累积 Reward 作为它对应的梯度的权重；这样的话，如果这个 Action 的 Reward 是正的，梯度就会朝着它的方向上升，相对于增强这个策略的这个 Action 选择；如果这个 Action 的 Reward 是负的，梯度就会朝着它的反方向走，相对于弱化这个策略的这个 Action 选择。在具体算法中，PG 的梯度加权方法是通过 $$G_n$$ 实现的。$$G_n$$ 是PG 算法统计的、一个 Action 的“后续”衰减累积的 Reward。

所以，本节的各种改进算法，就聚焦改进 $$G_n$$。具体来说，它们在 PG 中引入 Value 函数，然后利用 Value，改进 PG 的 $$G_n$$ 函数，使算法在训练中更稳定、更快收敛。它们就是 PG 的升级版：REINFORCE Algorithm with a Baseline、 Actor Critic、Advantage Actor Critic (A2C)、Deep Deterministic Policy Gradient (DDPG)。我们下面对它们分别进行介绍。

### REINFORCE Algorithm with a Baseline

为了让 PG 算法在实际上可行，我们引入一个技巧：Baseline。这是因为 Reward 如果全是“正数”的话，各种梯度就都会往上涨。所以，我们把 Reward 减去一个 Baseline。这样的话，Reward 就有正有负了。比 Baseline 好的，才会被“增强”；比 Baseline 弱的，就会被“抑制”。我们可以数学上证明，减去这样一个 Baseline 是不会影响梯度的。但是，它会让我们的模型更加稳定。

那么选什么做 Baseline 呢？最简单的方法是将目前实验测量到的平均 Reward 作为 Baseline。它不是最好的，但在实际中，表现相当好，所以在实际中可以尝试。这部分内容，请参考伯克利 CS182 的 PPT 和课堂讨论（Discussion）材料。

我们首先引入值函数 $$V(s)$$，即当前策略下的状态 $$s$$ 的值。即然引入了值函数，我们当然要在实验的过程中，也对它进行更新。这里值得注意的是：我们可以借鉴 PG 的方法，也用 $$G_n$$ 函数作为它的梯度的权重，对它进行更新。这就是值函数的部分。

我们提出对 $$G_n$$ 的第一个改进：用值函数作为 Baseline，计算测量获得的 $$G_n$$ 和这个 Baseline 函数的差别。我们然后用这个差别，代替 PG 算法里的 $$G_n$$，用它作为权重，去加权当前动作对应的梯度。这就是 REINFORCE Algorithm with a Baseline 方法。实验结果表明，它的收敛速度更快（10倍）。

减去 Baseline 之后，我们的策略其实是和我们可以证明，

### Actor Critic

为了减少统计很多实验值带来的 Variance，我们采用前面介绍过的 Temporal difference 方法，即：把 $$G_n$$ 换成“测量获得的、当前 Action 的 Reward $$r_n$$” 加上 “测量获得的、下一个状态的 Value 的衰减值”，即$$r_n + \gamma V_w(s_{n+1})$$。它就是基于当前实验的 Reward，对 $$s_n$$ 值对最新估计。这时，我们的式子有这种形式：$$r_n + \gamma V_w(s_{n+1}) - V_w(s_n)$$。我们称之为值函数的 Temporal difference。这样做，就只考虑一次实验的 Reward 测量值了，减少了模型 的 Variance。

因为我们是在用新的实验获得的结果和当前结果的不同，来更新模型，所以相对于是在针对当前模型的不足，进行有针对性的改进（即“批评”），所以，这种方法也叫 Actor Critic 方法。所以，“批评”其实是好事。没有批评，就没有进步。我们面对建设性的批评，要非常珍惜。要不实验就白做了，宝贵的失败也被白白浪费了。我们常说“失败是成功之母”，为什么呢？因为我们可以利用失败，做增强学习啊。

### Advantage Actor Critic (A2C)

Actor Critic 计算的是“值函数”的 Temporal difference，我们能不能把“值函数”换成“Q 函数”呢？这就是 A2C 算法。

我们首先介绍 Advantage 的概念。Advantage 函数是在状态 $$s$$ 下，一个 Action 相对于 Baseline $$V^{\pi}(s)$$ 取得了多少优势（Advantage）。即 $$A(s,a) = Q(s,a) - V^{\pi}(s)$$。

具体来说，我们将 $$r_n + \gamma V_w(s_{n+1}) - V_w(s_n)$$ 中的值函数 $$V(s)$$，换成 $$Q(s,a)$$。然后用这个 Advantage 值，代替 PG 算法里的 $$G_n$$，用它作为权重，去加权当前动作对应的梯度。这就是 A2C 算法。实验结果表明，它的收敛速度更快（10倍）。

注意。这里我们用类似更新“值网络”的方法，更新 Q 网络。详见 PPT。

### A2C 的设计逻辑

我们下面来详细理解 A2C 算法的设计逻辑。

我们首先介绍 Advantage 的概念。

A2C 算法的设计初衷是：如何改进 PG 算法中用到的、对在一个状态 s 下执行一个 Action a 获得的后续 “累积 Reward” $$G_n$$ 的估计。为此，人们想出以下办法：

第一个办法是：用我们前面学过的 (s,a) 的值函数 Q(s,a) 作为 $$G_n$$ 这个估计。我们专门训练一个模型来估计它。这就比根据噪声很大的测量结果对它进行统计，效果要好些。

第二个办法是：用我们前面学过的状态 s 的值函数 V(s) ，作为 $$G_n$$ 的Baseline。我们上面提到将目前实验测量到的平均 Reward 作为 Baseline。这种方法虽然有效，但还是有很多问题。如果用状态 s 的值函数 V(s) 作为 Baseline，就能突出当前 Action a 的“相对效果”，因此，达到“增强”对应的 Action 的效果。因此，我们又专门训练一个模型来估计它。

因此，我们最后用来对 PG 中的梯度进行加权的 $$G_n$$ 就变成了 $$A(s,a) = Q(s,a) - V^{\pi}(s)$$，这就是 Advantage。

我们然后介绍如何 Fit Q(s,a) 和 V(s) 的模型。

在 A2C 中，我们选择 Fit V(s)。为此，我们用 $$ Q(s_t,a_t) = r(s_t,a_t) + V^{\pi}(s_{t+1})$$ 来近似 Q。这时，$$A(s_t,a_t) = r(s_t,a_t) + V^{\pi}(s_{t+1}) - V^{\pi}(s_t)$$。所以，我们只需要 Fit $$V^{\pi}(s_t)$$ 的模型就可以了。

因此，我们需要通过实验，估计特定策略 $$\pi$$ 下的 $$V^{\pi}(s_t)$$。这在增强学习中被称为 “Policy Evaluation”，即：我们要评估当前策略下的值函数。显然，我们可以根据当前的策略，进行大量的实验，然后用测量获得的数据，得到这个值函数。这就是蒙特卡洛策略评估。这也是我们前面学过的 PG 采用的基本方法。

基于蒙特卡洛实验获得的数据，我们可以用深度模型来获得 $$V^{\pi}(s_t)$$ 的函数近似。这个模型的输入为当前状态 s，输出为实验测得的 s 后的 Reward 的累积和。所以，它就是一个经典的回归模型。

那么，因为实验测得的 s 后的 Reward 有很高的 Variance，所以，我们又做一个改进，就是不用这些测量结果的累积和，而是引入先前 Fit 的值函数的估计。此时，我们的模型输出是 $$r(s_t,a_t) + V^{\pi}(s_{t+1})$$，其中 $$V^{\pi}(s_{t+1})$$ 就是前面 Fit 的值函数的估计。就这样不断滚动地训练新的值函数模型。这种方法也被叫做 Bootstrapped 估计，因为我们先训练一个模型，然后用这个模型，接着训练自己，这就是机器学习里经常用到的 “Bootstrap”（自举）方法。

上面介绍的 Policy Evaluation 方法在实际中，效果很好。比如 1992 年 Gerald Tesauro 提出的 TD-Gammon 方法，能够根据游戏的盘面，估计它的值；2016 年，AlphaGo 也是用这个方法，估计了游戏的盘面的值。

因此，我们就有了 Actor Critic 算法。它首先根据策略进行实验，基于实验数据，训练 V 函数。然后，用 $$r_n + V_w(s_{n+1}) - V_w(s_n)$$ 这个 Advantage 来做 PG。如此迭代，训练策略模型。

我们下面引入“折扣因子”。因为我们的实验可以无穷地延续下去，所以，观察上面的模型输出 $$r(s_t,a_t) + V^{\pi}(s_{t+1})$$，我们会发现，如果 Reward r 总是正值的话，它会累积到无穷。这样的话，我们的 V 函数模型就不知道怎么办了。因此，我们引入“折扣因子”，把模型输出换为 $$r(s_t,a_t) + \gamma V^{\pi}(s_{t+1})$$。这样做是有道理的，因为对我们的体验来说，当前的 Reward 是最让人开心的，而未来的 Reward 需要打一些折扣。当然，这只是一种形象的比喻。事实上，它就是一个让我们的工作能够继续下去的一个技巧。

我们也可以在 MDP 的层面，理解这个折扣因子。这相当于我们在我们的 MDP 里加了一个 Dead 的状态，其他状态都有 $$1- \gamma$$ 的概率，转到这个 Dead 状态。

有了折扣因子，我们的 AC 算法采用的 Advantage 就变成了 $$r_n + \gamma V_w(s_{n+1}) - V_w(s_n)$$ 这个 Advantage 来做 PG。

我们然后介绍 Online AC 算法。上面的算法是 Batch 算法，因为它每次会执行策略，收集一批数据，然后再更新 V 模型和策略模型。而 Online AC 算法会往下走一步，得到 $$(s,a,s',r)$$ 后，就立刻更新 V 和策略模型。

我们最后介绍 AC 算法的深度模型的设计。在实际中，我们可以用两个分别的深度模型，一个训练 V，一个训练策略；我们也可以用一个多任务的深度模型，让一个模型，既输出 V 又输出策略。前者简单、稳定；后者可以让两个模型分享信息；在实际中，我们都可以尝试。

我们最后说明：我们训练的策略模型就是 AC 里面的 A：Actor，因为是它在执行策略；而 V 就是 AC 里面的 C：Critic，它在不断评估 Actor 当前执行的策略的 Value，所以，它是 Critic。

上面的内容，请参考伯克利 CS182 的 PPT 和课堂讨论（Discussion）材料。

### Deep Deterministic Policy Gradient (DDPG)

如果 Action 是连续的，我们有 DDPG 算法。因为它的 Action 是“连续的”，因此，策略是“确定性的”，就是只会输出一个值。这不同于 A2C 方法。A2C 方法的输出是“离散的”，所以，它的输出是各种 Action 的概率，然后 A2C 基于这些概率，随机选择一个 Action 进行下一步。所以，我们称 A2C 为“随机”（Stochastic）方法。

DDPG 算法也是既有 Policy 网络，又有 Q 函数网络。然后，它采用了我们前面学过的 Experience Buffer 和 Target 网络。首先基于当前 Policy，执行一系列实验，存入 Experience Buffer。然后从 Experience Buffer 中取出 Mini-batch 的数据，用 Temporal Difference 的方法更新 Q 函数网络；用 Q 函数在 Action 处的梯度，来加权策略梯度。注意，这里没有用 Log 策略梯度了。具体的证明是发明 AlphaGo 的 Silver 等研究者在 2014 年做出的。详见他们的论文。他们用这个算法，来控制机器人。

### 小结

本节我们学习了 Actor Critic 方法。它在策略梯度方法中，引入 Value 函数，用它来改进对策略的权重。具体来说，Actor Critic 通过 Temporal Difference 方法，改进了对 Reward 的估计，让算法更加稳定；Advantage Actor Critic（A2C）引入 Advantage，提高算法的收敛速度；而 Deep Deterministic Policy Gradient (DDPG) 适用于 Action 连续的情形，它集各种方法之大成，能够被用来控制机器人。

## 课本材料

- [SutBar] Sec. 13.4-13.5, [Sze] Sec. 4.4, [SigBuf] Sec. 5.3

## 课程材料

- 滑铁卢大学 CS486 人工智能 Actor Critic slides
- 伯克利 CS182 深度学习
  - Policy Gradient PPT，[B 站视频](https://www.bilibili.com/video/BV1PK4y1U751?p=45)，讨论材料 9
  - Actor Critic PPT，[B 站视频](https://www.bilibili.com/video/BV1PK4y1U751?p=48)，讨论材料 9
- Berkeley CS285 Lec 6: Actor-Critic Algorithms, [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)

## 练习

- ms-DeepRL
- 伯克利 CS285 HW 3: Q-learning and actor-critic algorithms, [Website](https://rail.eecs.berkeley.edu/deeprlcourse/)
- 伯克利 CS182 DL MuJoCo implement Imitation learning, Policy Gradients, DQN, and Actor Critic algorithms.
- 伯克利 RL bootcamp 2017 Lab 4 PG
- 斯坦福 CS224R DRL HW 2: AC， Mujoco MPC

## 论文

斯坦福 CS 224r 论文

Actor-Critic Methods
- Trust Region Policy Optimization. Schulman et al. (2015)
- Proximal Policy Optimization. Schulman et al. (2017)
- Instruct GPT. Ouyang et al. (2022)
- Solving Rubik's Cube with a Robot Hand. Akkaya et al. (2019)

伯克利 Actor-critic suggested readings

Classic papers
- Sutton, McAllester, Singh, Mansour (1999). Policy gradient methods for reinforcement learning with function approximation: actor-critic algorithms with value function approximation

Deep reinforcement learning actor-critic papers
- Mnih, Badia, Mirza, Graves, Lillicrap, Harley, Silver, Kavukcuoglu (2016). Asynchronous methods for deep reinforcement learning: A3C -- parallel online actor-critic
- Schulman, Moritz, L., Jordan, Abbeel (2016). High-dimensional continuous control using generalized advantage estimation: batch-mode actor-critic with blended Monte Carlo and function approximator returns
- Gu, Lillicrap, Ghahramani, Turner, L. (2017). Q-Prop: sample-efficient policy- gradient with an off-policy critic: policy gradient with Q-function control variate

Actor-critic examples
- High dimensional continuous control with generalized advantage estimation (Schulman, Moritz, L., Jordan, Abbeel ‘16)
  - Batch-mode actor-critic
  - Blends Monte Carlo and function approximator estimators (GAE)

Asynchronous methods for deep reinforcement learning (Mnih, Badia, Mirza, Graves, Lillicrap, Harley, Silver, Kavukcuoglu ‘16)
- Online actor-critic, parallelized batch
- N-step returns with N = 4
- Single network for actor and critic

<br/>

|[Index](index) | [Previous](11-pg) | [Next](15-trpo) |
