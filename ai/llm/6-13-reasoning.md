---
layout: post
title: 推理
---

什么是推理？

“推理”一词是一个总称，包括演绎、归纳、溯因、类比、常识以及其他解决问题的“理性”或系统方法的能力。推理通常是一个涉及多个推理步骤的过程。推理通常被认为需要抽象，也就是说，推理能力不限于特定示例，而是更普遍。如果我能推理加法，我不仅可以解决 23+37，还可以解决我遇到的任何加法问题。如果我学习以 10 为底的加法并了解其他底数的加法，我的推理能力可以让我快速学会以任何其他底数加法。

作为一个生成模型，大语言模型不具有严格意义上的推理能力。

## 推理 Prompt

我们可以利用 LLM 进行推理。输入下面的 Prompt，让 LLM 返回推理过程：

Logical and commonsense reasoning exam.

Explain your reasoning in detail, then answer with Yes or No. Your answers should follow this 4-line format:

Premise: <a tricky logical statement about the world>.
Question: <question requiring logical deduction>.
Reasoning: <an explanation of what you understand about the possible scenarios>.
Answer: <Yes or No>.

Premise: the customer doesn’t have any loans
Question: Can we logically conclude for sure that the customer doesn’t have any auto
loans?
Reasoning: Let's think logically step by step. The premise basically tells us that

然后 GPT 会接着说，比如：the customer has no loans at all. Therefore, we can conclude that the customer doesn't have any auto loans either becasuse no loans = no auto loans.
Answer: Yes

## 因果

当异常发生时，追踪调查，分析导致异常的原因，这就是“诊断”。在教育中，这个被称为“知识追踪”；在智能运维中，这被称为“根原因分析”；在医学中，这被称为“病因诊断”。它们的共同特点是：根据异常发生时的各种表现，进行推理分析。

利用现有的通用大模型，以及各种领域的专用大模型（比如医学领域大模型），进行上述追踪任务，就是面向追踪的大语言模型。

- Adèle H. Ribeiro，Causality and its Role in Reasoning, Explainability, and Generalizability，LxMLS 2023 PPT

- Andrew Lampinen，Passive learning of active causal strategies in agents and language models，DeepMind，LxMLS 2023 PPT

## 课程材料

- 华盛顿大学 CSE 599 同学 Slides

## 论文

### Ng 老师推荐论文

- 反思
  - “Self-Refine: Iterative Refinement with Self-Feedback,” Madaan et al. (2023)
  - “Reflexion: Language Agents with Verbal Reinforcement Learning,” Shinn et al. (2023)
  - “CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing,” Gou et al. (2024)
- 

### Andrej Karpathy 推荐论文

- 系统一与系统二思维（Thinking Fast and Slow）
  - 丹尼尔·卡尼曼 描述了一个有两个系统的思想框架。系统1快速、直观、情绪化；系统2更慢、更慎重、更合乎逻辑

- Mastering the game of Go with deep neural networks and tree search，[论文链接](https://www.nature.com/articles/nature16961)，
    - 这是大名鼎鼎的AlphaGo对应的论文，这是计算机程序首次在围棋游戏中击败人类顶级职业选手，此前人们认为这一壮举至少还需要十年的时间

- Chain-of-Thought Prompting Elicits Reasoning in Large Language Models，[论文链接](https://arxiv.org/abs/2201.11903)，
    - 生成一组中间推理步骤可以提高LLM执行复杂推理的能力

- Tree of Thoughts: Deliberate Problem Solving with Large Language Models，[论文链接](https://arxiv.org/abs/2305.10601)，
    - 用语言模型研究了系统2思维，涉及更多的探索、战略前瞻或规划。通过这种解决问题的方法，你可以用时间换取准确性

- System 2 Attention，[论文链接](https://arxiv.org/abs/2311.11829)
    - Meta在论文中增加了第二个注意力步骤，来帮助LLM决定要关注和处理什么。这一步重新生成输入的上下文，只包含相关的部分，然后在关注这些重新生成的上下文后，产生最终的回答

### 约翰霍普金斯大学推荐论文

Rationalization/Explanations:
- The Unreliability of Explanations in Few-Shot In-Context Learning
- Can Rationalization Improve Robustness?
- Can language models learn from explanations in context?

Compositionality:
- Winoground: Probing Vision and Language Models for Visio-Linguistic Compositionality
- Socratic Models: Composing Zero-Shot Multimodal Reasoning with Language
- ReasonBERT: Pre-trained to Reason with Distant Supervision
- Reasoning Like Program Executors
- LinkBERT: Pretraining Language Models with Document Links

### 普林斯顿课程推荐论文

- [Chain of Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/pdf/2201.11903.pdf)
- [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/pdf/2205.11916.pdf)

Refer:
- [Explaining Answers with Entailment Trees](https://arxiv.org/pdf/2104.08661.pdf)
- [Self-Consistency Improves Chain of Thought Reasoning in Language Models](https://arxiv.org/pdf/2203.11171.pdf)
- [Faithful Reasoning Using Large Language Models](https://arxiv.org/pdf/2208.14271.pdf)

### 华盛顿大学课程推荐论文

3: Can language models reason? 语言模型可以推理吗？

Why is it that deep learning can play chess, fold proteins, yet cannot solve strikingly easy puzzles?

为什么深度学习可以下棋、折叠蛋白质，却不能解决极其简单的难题？

1. [Show Your Work: Scratchpads for Intermediate Computation with Language Models (Nye et al., 2021)](https://arxiv.org/abs/2112.00114)
1. [Chain of Thought Prompting Elicits Reasoning in Large Language Models (Wei et al., 2022)](https://arxiv.org/abs/2201.11903)
1. [Structured, flexible, and robust: benchmarking and improving large language models towards more human-like behavior in out-of-distribution reasoning tasks (Collins et al., 2022)](https://arxiv.org/abs/2205.05718)
1. [Large Language Models Still Can't Plan: A Benchmark for LLMs on Planning and Reasoning about Change (Valmeekam et al., 2022)](https://arxiv.org/abs/2206.10498)
1. [Language Models Are Greedy Reasoners: A Systematic Formal Analysis of Chain-of-Thought (Saparov and He, 2022)](https://arxiv.org/abs/2210.01240)
1. [Neural Theory-of-Mind? On the Limits of Social Intelligence in Large LMs (Sap et al., 2022)](https://arxiv.org/abs/2210.13312)
1. [Natural Language Deduction with Incomplete Information (Sprague et al., 2022)](https://arxiv.org/abs/2211.00614)
1. [Maieutic Prompting: Logically Consistent Reasoning with Recursive Explanations (Jung et al., 2022)](https://arxiv.org/abs/2205.11822)
1. [Language Models of Code are Few-Shot Commonsense Learners (Madaan et al., 2022)](https://arxiv.org/abs/2210.07128)
1. [Selection-Inference: Exploiting Large Language Models for Interpretable Logical Reasoning (Creswell et al., 2022)](https://arxiv.org/abs/2205.09712)
1. [Faithful Reasoning Using Large Language Models (Creswell and Shanahan 2022)](https://arxiv.org/abs/2208.14271)
1. [Binding Language Models in Symbolic Languages (2022)](https://lm-code-binder.github.io)
1. [Which Linguist Invented the Lightbulb? Presupposition Verification for Question-Answering (Kim et al., 2021)](https://arxiv.org/abs/2101.00391)
1. [CREPE: Open-Domain Question Answering with False Presuppositions (Yu et al., 2022)](https://arxiv.org/abs/2211.17257)

### Melanie Mitchell 论文

Memorization vs reasoning ([Melanie Mitchell](https://melaniemitchell.me/))

- Perspectives on the State and Future of Deep Learning, 2023, arXiv:2312.09323，[论文](https://arxiv.org/abs/2312.09323)

- Comparing Humans, GPT-4, and GPT-4V On Abstraction and Reasoning Tasks. To appear in Proceedings of the LLM-CP Workshop, AAAI-24. [论文](https://arxiv.org/abs/2311.09247v3)

- Can Large Language Models Reason? [Webpage](https://aiguide.substack.com/p/can-large-language-models-reason)，[视频 1](https://www.youtube.com/watch?v=uEN_rOxKkag)

- The debate over understanding in AI’s large language models，[Webpage](https://www.pnas.org/doi/full/10.1073/pnas.2215907120)

- How do we know how smart AI systems are? [Webpage](https://www.science.org/doi/10.1126/science.adj5957)

- AI Models of Conceptual Abstraction and Analogy-Making，博士后项目说明，[PDF](https://melaniemitchell.me/PostdocProjectDescription.pdf)

- Transcript of Episode 33 – Melanie Mitchell on the Elements of AI，[Webpage](https://jimruttshow.blubrry.net/the-jim-rutt-show-transcripts/transcript-of-episode-33-melanie-mitchell-on-the-elements-of-ai/)

- Book Artificial Intelligence: A Guide for Thinking Humans， 2019

## Agent 推理相关论文

复旦大学的 LLM Agent 综述论文中提到的[LLM 推理和计划能力相关论文](https://github.com/woooodyy/llm-agent-paper-list#114-reasoning--planning)。

Reasoning
- [2023/09] ReConcile: Round-Table Conference Improves Reasoning via Consensus among Diverse LLMs. Justin Chih-Yao Chen (University of North Carolina at Chapel Hill) et al. arXiv. [paper] [code]
- [2023/05] Self-Polish: Enhance Reasoning in Large Language Models via Problem Refinement. Zhiheng Xi (Fudan University) et al. arXiv. [paper] [code]
- [2023-03] Large Language Models are Zero-Shot Reasoners. Takeshi Kojima (The University of Tokyo) et al. arXiv. [paper] [code]
- [2023/03] Self-Refine: Iterative Refinement with Self-Feedback. Aman Madaan (Carnegie Mellon University) et al. arXiv. [paper] [code]
- [2022/05] Selection-Inference: Exploiting Large Language Models for Interpretable Logical Reasoning. Antonia Creswell (DeepMind) et al. arXiv. [paper]
- [2022/03] Self-Consistency Improves Chain of Thought Reasoning in Language Models. Xuezhi Wang (Google Research) et al. arXiv. [paper] [code]
- [2023/02] Multimodal Chain-of-Thought Reasoning in Language Models. Zhuosheng Zhang (Shanghai Jiao Tong University) et al. arXiv. [paper] [code]
- [2022/01] Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. Jason Wei (Google Research) et al. arXiv. [paper]

### 综述论文

- Towards Reasoning in Large Language Models: A Survey，[论文](https://arxiv.org/abs/2212.10403)

### Choi 老师论文

- Faith and Fate: Limits of Transformers on Compositionality，[论文](https://arxiv.org/abs/2305.18654)，发现多步推理能力有限

### 系统

- 谷歌 AI 通过图灵测试，大模型医生来了？图灵人工智能，2024-01-15，[微信公众号](https://mp.weixin.qq.com/s/Cft9ISgxolUDIacc97WMjA)

<br/>

| [Index](./) | [Previous](6-11-understand) | [Next](6-17-plan)
