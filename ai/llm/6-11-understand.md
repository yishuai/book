---
layout: post
title: 理解
---

一个智能代理机器人要完成我们交给他的一件工作，需要有对世界的理解。这就是说他要有关于世界运行方式的模型（World Model）。

大语言模型“理解”语言吗？理解语言中包含的意义吗？对于教育、运维等场景下的各种概念，它理解吗？对我们想做异常的追踪，它理解什么是“异常”吗？它理解什么是“追踪”吗？它又理解“追踪”的逻辑吗？

## 课程材料

- 华盛顿大学 CSE 599 同学 Slides

## 论文

### Choi 老师论文

Generation vs understanding ([Yejin Choi](https://homes.cs.washington.edu/~yejin/))

- The Generative AI Paradox: "What It Can Create, It May Not Understand"，发现 LLM 虽然能够像专家那样生成，但却不理解最基本的东西。[论文](https://arxiv.org/abs/2311.00059)，[视频 1](https://www.ted.com/talks/yejin_choi_why_ai_is_incredibly_smart_and_shockingly_stupid/c)

### 华盛顿大学课程推荐论文

1: Do neural language models *understand* language?

神经语言模型“理解”语言吗？

What does it mean to understand language? Can models learn language without embodiment? Can we (even) separate the form and meaning? Does it matter if language models do or don’t?

理解语言意味着什么？模型可以在没有具体化的情况下学习语言吗？我们（甚至）可以将形式和意义分开吗？语言模型有或没有有关系吗？

1. [Language models as agent models (Andreas, 2022)](https://arxiv.org/abs/2212.01681)
1. [To Dissect an Octopus: Making Sense of the Form/Meaning Debate (Blog, Julian Micheal, 2020)](https://julianmichael.org/blog/2020/07/23/to-dissect-an-octopus.html)
1. [Is it possible for language models to achieve language understanding? (Blog, Christopher Potts, 2020)](https://chrisgpotts.medium.com/is-it-possible-for-language-models-to-achieve-language-understanding-81df45082ee2)
1. [Implicit Representations of Meaning in Neural Language Models (Li, 2021)](https://arxiv.org/abs/2106.00737)
1. [How could we know if Large Language Models understand language? (Blog, Sean Trott, 2022)](https://seantrott.substack.com/p/how-could-we-know-if-large-language)
1. [On the Dangers of Stochastic Parrots: Can Language Models Be Too Big? (Bender et al., 2021)](https://dl.acm.org/doi/pdf/10.1145/3442188.3445922)
1. [Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data (Emily M. Bender, Alexander Koller, 2020)](https://aclanthology.org/2020.acl-main.463/)
1. [Mapping Language Models to Grounded Conceptual Spaces (Patel, 2022)](https://openreview.net/forum?id=gJcEM8sxHK)
1. [Dissociating language and thought in large language models: a cognitive perspective (2023)](https://arxiv.org/abs/2301.06627)

### LLM Agent 论文

复旦大学的 LLM Agent 综述论文中提到的[LLM 理解人类的能力相关论文](https://github的.com/woooodyy/llm-agent-paper-list#deep-understanding)。

High-quality generation
- [2023/10] Towards End-to-End Embodied Decision Making via Multi-modal Large Language Model: Explorations with GPT4-Vision and Beyond Liang Chen et al. arXiv. [paper] [code]
    - This work proposes PCA-EVAL, which benchmarks embodied decision making via MLLM-based End-to-End method and LLM-based Tool-Using methods from Perception, Cognition and Action Levels.
- [2023/08] A Multitask, Multilingual, Multimodal Evaluation of ChatGPT on Reasoning, Hallucination, and Interactivity. Yejin Bang et al. arXiv. [paper]
    - This work evaluates the multitask, multilingual and multimodal aspects of ChatGPT using 21 data sets covering 8 different common NLP application tasks.
- [2023/06] LLM-Eval: Unified Multi-Dimensional Automatic Evaluation for Open-Domain Conversations with Large Language Models. Yen-Ting Lin et al. arXiv. [paper]
    - The LLM-EVAL method evaluates multiple dimensions of evaluation, such as content, grammar, relevance, and appropriateness.
- [2023/04] Is ChatGPT a Highly Fluent Grammatical Error Correction System? A Comprehensive Evaluation. Tao Fang et al. arXiv. [paper]
    - The results of evaluation demonstrate that ChatGPT has excellent error detection capabilities and can freely correct errors to make the corrected sentences very fluent. Additionally, its performance in non-English and low-resource settings highlights its potential in multilingual GEC tasks.

Deep understanding
- [2023/06] Clever Hans or Neural Theory of Mind? Stress Testing Social Reasoning in Large Language Models. Natalie Shapira et al. arXiv. [paper]
    - LLMs exhibit certain theory of mind abilities, but this behavior is far from being robust.
- [2022/08] Inferring Rewards from Language in Context. Jessy Lin et al. ACL. [paper]
    - This work presents a model that infers rewards from language and predicts optimal actions in unseen environment.
- [2021/10] Theory of Mind Based Assistive Communication in Complex Human Robot Cooperation. Moritz C. Buehler et al. arXiv. [paper]
    - This work designs an agent Sushi with an understanding of the human during interaction.

##
<br/>

| [Index](./) | [Previous](6-9-memory) | [Next](6-13-reasoning)
