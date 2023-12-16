---
layout: post
title: 模拟策略学习
---

前面学习的基于值函数的增强学习，是沿用的 MDP 的基本思路。下面介绍另一种思路：学习“策略”。

对“策略”的学习，最简单的是学习智能“人”的策略。这就是模拟学习。如果我们收集了大量司机开车的行为数据，那么，基于这些数据，训练一个“策略”模型，这就是模拟策略学习。模拟学习也叫“行为克隆”。

虽然有很多困难，2017 年，Nvidia 还是通过模拟策略学习，把无人驾驶汽车开上了路。为此，他们用了很多技巧，比如，比较汽车上的左、中、右三个摄像头，如果发现中间的摄像头出现了前面左边摄像头里的东西，就认为汽车左偏了，就向右把它纠正。

模拟策略学习有三个难点

1）在真实世界中，司机的行为可能不是马尔可夫的，即他当前的动作不仅和当前状态有关，可能还和以前的状态相关。为此，人们提出用 RNN 考虑更长的观察。

2）在真实世界中，同样的状态下，多种 Action 都是合理的。这时，我们的机器学习模型怎么办。这就是 “Multimodal 行为” 问题。为此，人们提出混合高斯输出等方法。

3）在真实世界中，当我们在状态 s 下执行动作 a 后，进入的新状态，可能和收集的专家数据不一致。这样的话，我们就会逐渐偏离专家数据的轨道。为此，人们提出 DAgger，即首先用专家的行为学习一个策略；然后用这个策略做实验，把实验中观察到的状态，让专家来给出 Action，以此扩充专家数据，并基于新的扩充后的专家数据再继续训练。这个方法在很早以前，就训练出来了无人机，可以穿越树林。

模拟策略学习的缺点是它需要专家打标，成本比较高，但它依旧是一种实用的方法。在实际中，它有时会工作得很好，但需要根据实际问题，设计各种技巧，建立很准确的模型。可以尝试，但问题会比较多，效果不一定好。

实用方法

故意添加错误和更正
• 错误会带来伤害，但纠正会有所帮助。这个帮助往往能够抵消错误带来的伤害，并且还有增益
• 使用数据增强，添加一些“假”数据来演示修正（例如，侧向摄像头）

## 课程材料

- 滑铁卢 CS885 RL PPT
- 伯克利 CS182 深度学习，Imitation Learning PPT，上课视频 [B 站](https://www.bilibili.com/video/BV1PK4y1U751?p=42)，讨论材料 8
- Berkeley CS285 Lec 2: Supervised Learning of Behaviors, [slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)

## 课本材料

N/A

## 练习

- 伯克利 CS285 HW 1: Imitation learning (control via supervised learning), [Website](https://rail.eecs.berkeley.edu/deeprlcourse/)
- 伯克利 CS182 DL MuJoCo implement Imitation learning, Policy Gradients, DQN, and Actor Critic algorithms.
- 斯坦福 CS224R DRL HW 1: Imitation

## 论文

斯坦福课程提到的论文
- Deep Imitation Learning for Complex Manipulation Tasks from Virtual Reality Teleoperation. Zhang et al. (2017)

滑铁卢课题提到的论文

- Ho, J., & Ermon, S. (2016). Generative adversarial imitation learning. In NeurIPS (pp. 4565-4573).
- Torabi, F., Warnell, G., & Stone, P. (2018). Behavioral cloning from observation. In IJCAI (pp. 4950-4957).

伯克利课程提到的论文
- Bojarski et al. ‘16, NVIDIA
- ALVINN: Autonomous Land Vehicle In a Neural Network 1989
- Ross et al. “A Reduction of Imitation Learning and Structured Prediction to No-Regret Online Learning”
- A Machine Learning Approach to Visual Perception of Forest Trails for Mobile Robots
- Rouhollah Rahmatizadeh et al., Vision-Based Multi-Task Manipulation for Inexpensive Robots Using End-To-End Learning from Demonstration. 2017.
- de Haan et al., “Causal Confusion in Imitation Learning”
- Chi et al. Diffusion Policy: Visuomotor Policy Learning via Action Diffusion. 2023
  - imitation with diffusion models
- Zhao et al. Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware. 2023
  - imitation with latent variables
- imitation with Transformers
  - Brohan et al. RT-1: Robotics Transformer. 2023.
  - https://robotics-transformer.github.io/
  - Learning Latent Plans from Play
  - Collect data 
  - Train goal conditioned policy
  - Reach goals
- Unsupervised Visuomotor Control through Distributional Planning Networks
  - Going beyond just imitation?
  - Start with a random policy
  - Collect data with random goals
  - Treat this data as “demonstrations” for the goals that were reached
  - Use this to improve the policy
  - Repeat
- Learning to Reach Goals via Iterated Supervised Learning
- Shah*, Sridhar*, Bhorkar, Hirose, Levine. GNM: A General Navigation Model to Drive Any Robot. 2022.
  - Hindsight Experience Replay
  - Similar principle but with reinforcement learning
  - This will make more sense later once we cover off-policy value-based RL algorithms
  - Worth mentioning because this idea has been used widely outside of imitation (and was arguably first proposed there)
- Dagger Ross et al. ‘11

<br/>

|[Index](index) | [Previous](9-drl-dqn) | [Next](11-pg) |
