---
layout: post
title: 模型和数据的规模
---

本节介绍模型和数据的规模对大语言模型性能的影响。

首先，模型的 Loss 和训练的时间、数据集大小、模型规模的关系是 Power Law 的。基于这个关系，可以在资源有限的情况下，选择合适的数据量大小和模型规模，获得计算最优的模型。

其次，人们发现了所谓的“涌现（Emergent Abilities）”能力。涌现指的是：系统的量变导致其行为的质变。如果一种能力不存在于较小的模型中但存在于较大的模型中，则称该能力是涌现的。

关于涌现，治杰最近和我们分享了 NeuIPS 2023 的 Best Paper 《Are Emergent Abilities of Large Language Models a Mirage?》，说模型的 Loss 其实是逐渐下降的，只是由于测试集有限，或者评估方法是离散的，导致评估结果出现“涌现”的结果。很有意思。

## 课程材料

- 斯坦福 CS324 2022 年 [Scaling Laws](https://stanford-cs324.github.io/winter2022/lectures/scaling-laws/)

- Berkeley Summit 2023, Princeton, Open Dataset and Decentralized Compute for LLMs, Slides, Video, Tri Dao, 提出 Flash Attention 等硬件优化的模型，实现 RedPajama，规模比得上 Llama

- Berkeley Summit 2023, Berkeley, Rethinking LLM Evaluation, Slides, Video, Ion Stonica，用 GPT-4 评估 Vicuna，发现和人的评估有 80% 一致，还是不错的。

## 论文

普林斯顿大学课程参考论文

- [Training Compute-Optimal Large Language Models](https://arxiv.org/pdf/2203.15556.pdf)

Refer:
- [Scaling Laws for Neural Language Models](https://arxiv.org/pdf/2001.08361.pdf)
- [Scale Efficiently: Insights from Pre-training and Fine-tuning Transformers](https://arxiv.org/pdf/2109.10686.pdf)
- [Scaling Laws for Autoregressive Generative Modeling](https://arxiv.org/pdf/2010.14701.pdf)

约翰霍普金斯大学参考论文

Scaling
- Scaling Laws for Neural Language Models
- Scaling Laws for Autoregressive Generative Modeling
- Big Self-Supervised Models are Strong Semi-Supervised Learners
- Training Compute-Optimal Large Language Models
- Scaling Language Models: Methods, Analysis & Insights from Training Gopher
- Scale Efficiently: Insights from Pretraining and Finetuning Transformers

Andrej Karpathy 推荐论文

- Training Compute Optimal Language Models，[论文链接](https://arxiv.org/abs/2203.15556)，
    - 论文研究了语言模型中参数的数量与使用的训练数据的数量。论文表明，不断扩大参数数量和数据大小可以持续提供“更多的免费智能”

- Scaling Laws for Neural Language Models，[论文链接](https://arxiv.org/abs/2001.08361)，
    - 论文是支撑OpenAI一直把模型做大的重要研究工作。论文研究了训练大语言模型所需的参数数量、数据集大小和计算之间的比率

华盛顿大学参考论文

2: Is scale all we need for language models?

语言模型所需要的就是规模吗？

What are the emergent capabilities of large language models? Are we limited by the model size vs. data size? Is it really that the bigger is always the better? What about *inverse* scaling laws?

大型语言模型的新兴能力是什么？我们是否受到模型大小与数据大小的限制？真的是越大越好吗？那么逆缩放定律呢？

1. [Training Compute-Optimal Large Language Models (DeepMind, 2022)](https://arxiv.org/abs/2203.15556)
1. [Emergent Abilities of Large Language Models (Google, 2022)](https://arxiv.org/abs/2206.07682)
1. [In-context Learning and Induction Heads (Anthropic, 2022)](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html)
1. [Scaling Instruction-Finetuned Language Models (Google, 2022)](https://arxiv.org/abs/2210.11416)
1. [Scaling Laws for Neural Language Models (OpenAI, 2020)](https://arxiv.org/abs/2001.08361)
1. [Scaling Laws for Autoregressive Generative Modeling (OpenAI, 2020)](https://arxiv.org/abs/2010.14701)
1. [Scaling Laws for Generative Mixed-Modal Language Models (Meta, 2023)](https://arxiv.org/abs/2301.03728)
1. [Scaling Laws for Transfer (OpenAI, 2021)](https://arxiv.org/abs/2102.01293)
1. [Beyond neural scaling laws: beating power law scaling via data pruning (Meta, 2022)](https://arxiv.org/abs/2206.14486)
1. [Measuring Progress on Scalable Oversight for Large Language Models (Anthropic, 2022)](https://arxiv.org/abs/2211.03540)
1. [LLM.int8() and Emergent Features (Blog, Dettmers, 2022)](https://timdettmers.com/2022/08/17/llm-int8-and-emergent-features/)
1. [LLM.int8(): 8-bit Matrix Multiplication for Transformers at Scale (Dettmers, 2022)](https://arxiv.org/abs/2208.07339)
1. [Predictability and Surprise in Large Generative Models (Anthropic, 2022)](https://arxiv.org/abs/2202.07785)
1. [An Information-Theoretic Analysis of Compute-Optimal Neural Scaling Laws (2022)](https://arxiv.org/abs/2212.01365)
1. [Pathways Language Model (PaLM): Scaling to 540 Billion Parameters for Breakthrough Performance (Blog Google, 2022)](https://ai.googleblog.com/2022/04/pathways-language-model-palm-scaling-to.html)
1. [PaLM: Scaling Language Modeling with Pathways (Google, 2022)](https://arxiv.org/abs/2204.02311)
1. [GLaM: Efficient Scaling of Language Models with Mixture-of-Experts (Google, 2022)](https://arxiv.org/abs/2112.06905)
1. [Using DeepSpeed and Megatron to Train Megatron-Turing NLG 530B, A Large-Scale Generative Language Model (Megatron-Turing NLG 530B, Microsoft & NVIDIA, 2022)](https://arxiv.org/abs/2201.11990)
1. [Scaling Language Models: Methods, Analysis & Insights from Training *Gopher* (DeepMind, 2022)](https://arxiv.org/abs/2112.11446)
1. [Galactica: A Large Language Model for Science (Meta, 2022)](https://arxiv.org/abs/2211.09085)
1. [LaMDA: Towards Safe, Grounded, and High-Quality Dialog Models for Everything (Blog Google, 2022)](https://ai.googleblog.com/2022/01/lamda-towards-safe-grounded-and-high.html)
1. [Inverse scaling competition (public competition, 2022)](https://github.com/inverse-scaling/prize)
1. [Quantifying Memorization Across Neural Language Models (Carlini et al., 2022)](https://arxiv.org/abs/2202.07646)
1. [How does GPT Obtain its Ability? Tracing Emergent Abilities of Language Models to their Sources (Fu et al., 2022)](https://www.notion.so/How-does-GPT-Obtain-its-Ability-Tracing-Emergent-Abilities-of-Language-Models-to-their-Sources-b9a57ac0fcf74f30a1ab9e3e36fa1dc1?pvs=21)
1. [What Language Model Architecture and Pretraining Objective Work Best for Zero-Shot Generalization? (Wang et al., 2022)](https://arxiv.org/abs/2204.05832)

<br/>

| [Index](./) | [Previous](2-7-data) | [Next](2-16-peft)
