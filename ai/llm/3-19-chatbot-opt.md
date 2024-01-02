---
layout: post
title: 对话系统优化
---

高质量的对话，是每个人都梦寐以求的。高质量的对话，有着一些共同的特征。首先，这个人要懂；其次，要会对话，即综合利用各种对话方式，比如提问、质疑、提示，来完成目标。

首先，不同的场景，有不同的对话质量的指标。比如，对于电商，可能是物美价廉；对于教育来说，可能是迅速掌握知识点，但也可能是促进思考。

以教育为例，这篇论文设计了一个基于 LLM 的机器人，能够提出问题，促进课堂中同学们之间的交互，帮助学习 [论文](https://www.semanticscholar.org/paper/Large-Language-Model-Driven-Classroom-Flipping%3A-Tan/64809140c38ce9d4bee3a30c59da9a1decd88b97)。

其次，如何在对话中学习，优化系统，这方面的算法很有意思，即：对话 Agent 在连续学习。这是我们理解的 OpenAI ChatGPT 正在采用的一种方式，即：它在根据和人对话的结果，挑战自己的对话策略，提高对话质量。利用 PPO 等增强学习算法，我们应该能够设计出这样的系统。

## 论文

普林斯顿课程推荐论文
- [LaMDA: Language Models for Dialog Application](https://arxiv.org/pdf/2201.08239.pdf)

Refer:
- [Recipes for building an open-domain chatbot](https://arxiv.org/pdf/2004.13637.pdf)
- [BlenderBot 3: a deployed conversational agent that continually learns to responsibly engage](https://arxiv.org/pdf/2208.03188.pdf), [Demo](https://blenderbot.ai/)

<br/>

| [Index](./) | [Previous](3-17-chatbot-dev) | [Next](3-20-rag-app-dev)
