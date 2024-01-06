---
layout: post
title: Reward 学习
---

Reward 学习，是 RL 的关键。比如 OpenAI 在 ChatGPT 中对 Reward 的学习。本节学习 Reward 学习的内容。

## 课程材料

- Stanford CS234 RL Lecture 16: Rewards, Value Alignment

## 论文

斯坦福 CS 224r 论文

- Variational Inverse Control with Events: A General Framework for Data-Driven Reward Definition. Fu et al. (2018)
- Deep reinforcement learning from human preferences. Christiano et al. (2017)

基于 LLM 的 Reward 设计最新研究论文

- Eureka: Human-Level Reward Design via Coding Large Language Models, Oct. 2023，通过 LLM 迭代优化 Reward 代码，完成机器手的增强学习训练，很有意思。[Website](https://eureka-research.github.io/)，基于 Isaac Gym RL 物理仿真实验环境 [Website](https://developer.nvidia.com/isaac-gym)，采用 [RL Games](https://github.com/Denys88/rl_games) 的 RL 算法实现。

- Reward Design with Language Models，2023 年 2 月，[Webpage](https://arxiv.org/abs/2303.00001)，把文本送给 LLM 让它给出 Reward

LLM as Judge

- Judging LLM-as-a-judge with MT-Bench and Chatbot Arena, I. Stonica, 2023, 发现 GPT-4 的判断和人差不多。


## 课本材料

N/A

## 练习

N/A

## 论文

- ICLR 2021 Quantifying Differences in Reward Functions

- ICLR 2021 Discovering a set of policies for the worst case reward

<br/>

|[Index](index) | [Previous](15-trpo) | [Next](18-irl) |
