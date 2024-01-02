---
layout: post
title: 检索增强模型
---

检索增强的大语言模型能检索上下文，查找和检索相关文档，将它们注入 Prompt，为 LLM 提供额外的信息，帮助 LLM 回答问题。提出这一思想的论文是《Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks》[论文链接](https://arxiv.org/abs/2005.11401)，[Arxiv Dive](https://blog.oxen.ai/arxiv-dives-rag/)。

## 课程材料

- 约翰霍普金斯 UA 2024 Lec 19 Dealing with limited context window
  - Retrieval-augmentation
  - Compressing context window
  - Memory modules

## 论文

### 约翰霍普金斯论文

Evolving Memory:
- Memorizing Transformers
- Fast Model Editing at Scale
- SERAC: Memory-based Model Editing at Scale
- Towards Teachable Reasoning Systems

### 普林斯顿课程论文

1. [Emergence of Maps in the Memories of Blind Navigation Agents (Wijmans et al., 2023)](https://arxiv.org/abs/2301.13261)

### 约翰霍普金斯推荐论文

Retrieval from Memory

- Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

Additional Reading:

- Scaling Laws for Neural Language Models
- REALM: Retrieval-Augmented Language Model Pre-Training
- Improving language models by retrieving from trillions of tokens
- An Efficient Memory-Augmented Transformer for Knowledge-Intensive NLP Tasks
- When Not to Trust Language Models: Investigating Effectiveness and Limitations of Parametric and Non-Parametric Memories.
- Unsupervised Dense Information Retrieval with Contrastive Learning
- Atlas: Few-shot Learning with Retrieval Augmented Language Models
- Relational Memory Augmented Language Models

普林斯顿课程推荐论文

Retrieval-based LMs
- [Improving language models by retrieving from trillions of tokens](https://arxiv.org/pdf/2112.04426.pdf)

Refer:
- [Generalization through Memorization: Nearest Neighbor Language Models](https://arxiv.org/pdf/1911.00172.pdf)
- [Training Language Models with Memory Augmentation](https://arxiv.org/pdf/2205.12674.pdf)
- [Few-shot Learning with Retrieval Augmented Language Models](https://arxiv.org/pdf/2208.03299.pdf)

华盛顿大学推荐论文

5: Parametric vs. non-parametric knowledge?

参数知识与非参数知识？

Should knowledge be neuralized or indexed? In what does condition one approach win over the other? Can we integrate the two?

知识应该神经化还是索引化？在什么情况下一种方法会胜过另一种方法？我们可以将两者结合起来吗？

1. [Generalization through Memorization: Nearest Neighbor Language Models (Khandelwal et al., 2020)](https://openreview.net/pdf?id=HklBjCEKvH)
1. [Dense Passage Retrieval for Open-Domain Question Answering (Karpukhin et al., 2020)](https://arxiv.org/abs/2004.04906)
1. [Training Language Models with Memory Augmentation (Zhong et al., 2022)](https://arxiv.org/abs/2205.12674)
1. [When Not to Trust Language Models: Investigating Effectiveness and Limitations of Parametric and Non-Parametric Memories (Mallen et al., 2022)](https://arxiv.org/abs/2212.10511)
1. [Rich Knowledge Sources Bring Complex Knowledge Conflicts: Recalibrating Models to Reflect Conflicting Evidence (Chen et al., 2022)](https://arxiv.org/abs/2210.13701)
1. [Transformer Memory as a Differentiable Search Index (Tay et al., 2022)](https://arxiv.org/abs/2202.06991)
1. [Reasoning Over Virtual Knowledge Bases With Open Predicate Relations (Sun et al., 2021)](http://proceedings.mlr.press/v139/sun21e.html)
1. [Adaptable and Interpretable Neural Memory Over Symbolic Knowledge (Verga et al., 2021)](https://aclanthology.org/2021.naacl-main.288/)
1. [Improving language models by retrieving from trillions of tokens (Borgeaud et al., 2021)](https://arxiv.org/abs/2112.04426)

## 记忆相关论文

如何提高 Agent 的记忆和学习能力，也是目前的研究热点。AutoGPT 入门指南中有关于记忆的论文（[Github](https://github.com/Significant-Gravitas/AutoGPT/blob/master/autogpts/forge/tutorials/004_memories.md)），包括提高 Transformers 的长度限制、总结记忆的内容、用向量和数据结构压缩记忆内容、从记忆中检索，等等方面。

复旦大学的 LLM Agent 综述论文中也提到了[LLM Agent 应用相关的 Memory 参考论文](https://github.com/woooodyy/llm-agent-paper-list#113-memory)。

<br/>

| [Index](./) | [Previous](6-7-knowledge) | [Next](6-11-understand)
