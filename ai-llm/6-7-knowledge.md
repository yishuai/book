---
layout: post
title: 知识
---

大语言模型中是否包括知识？一直以来，结构化的知识（如知识图谱）和非结构化的知识（如文档、搜索引擎检索结果），被认为是“知识”。而大语言模型产生的文本，是基于文本预测的，并不是“知识”。

和“知识”相反的，是所谓的“幻觉”。OpenAI 的竞争者 [Anthropic](https://www.anthropic.com/) 最近推出的 Claude 据称减少了 50% 的“幻觉”。

在我们致力于的追踪问题上，也已经有很多的知识。这些结构化和非结构化的知识，如何和大语言模型相结合，帮助我们完成追踪的任务，非常值得研究。

## 论文

普林斯顿课程推荐论文：

- [Language Models as Knowledge Bases?](https://arxiv.org/pdf/1909.01066.pdf)
- [How Much Knowledge Can You Pack Into the Parameters of a Language Model?](https://arxiv.org/pdf/2002.08910.pdf)

Refer:
- [Knowledge Neurons in Pretrained Transformers](https://arxiv.org/pdf/2104.08696.pdf)
- [Fast Model Editing at Scale](https://arxiv.org/pdf/2110.11309.pdf)
- [Question and Answer Test-Train Overlap in Open-Domain Question Answering Datasets](https://arxiv.org/pdf/2008.02637.pdf)

### 华盛顿大学推荐论文

4: Are language models knowledge models?

语言模型是知识模型吗？

How much knowledge do language models have?

语言模型有多少知识？

1. [Language Models as Knowledge Bases? (Petroni et al., 2019)](https://aclanthology.org/D19-1250.pdf)
1. [Factual Probing Is [MASK]: Learning vs. Learning to Recall (Zhong et al., 2021)](https://arxiv.org/abs/2104.05240)
1. [Symbolic Knowledge Distillation: from General Language Models to Commonsense Models (West et al., 2021)](https://arxiv.org/abs/2110.07178)
1. [Time-Aware Language Models as Temporal Knowledge Bases (Dhingra et al., 2022)](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00459/110012/Time-Aware-Language-Models-as-Temporal-Knowledge)
1. [Language Models (Mostly) Know What They Know (Kadavath et al., 2022)](https://arxiv.org/abs/2207.05221)
1. [GreaseLM: Graph REASoning Enhanced Language Models for Question Answering (Zhang et al., 2022)](https://arxiv.org/abs/2201.08860)
1. [QA Is the New KR: Question-Answer Pairs as Knowledge Bases (Chen et al., 2022)](https://arxiv.org/abs/2207.00630)
1. [Discovering Latent Knowledge in Language Models Without Supervision (Burns et al., 2022)](https://arxiv.org/abs/2212.03827)

## 医学知识

- [Large Language Models Encode Clinical Knowledge (Singhal et al., 2022)](https://arxiv.org/abs/2212.13138)

- 哈工大华佗模型，基于“活字”，Bloom 7B
  - 《[HuaTuo: Tuning LLaMA Model with Chinese Medical Knowledge](https://arxiv.org/pdf/2304.06975.pdf)》
  - 创建了医学数据集，8 K，做 IFT，《[The CALLA Dataset: Probing LLMs’ Interactive Knowledge Acquisition from Chinese Medical Literature](https://arxiv.org/pdf/2309.04198.pdf)》
  - 《Knowledge-tuning Large Language Models with Structured Medical Knowledge Bases for Reliable Response Generation in Chinese》，[论文](https://arxiv.org/pdf/2309.04175.pdf)，[代码](https://github.com/SCIR-HI/Huatuo-Llama-Med-Chinese/)

## Agent Knowledge 论文

复旦大学的 LLM Agent 综述论文中提到的[知识相关论文](https://github.com/woooodyy/llm-agent-paper-list#112-knowledge)。

Pretrain model
- [2023/04] Learning Distributed Representations of Sentences from Unlabelled Data. Felix Hill (University of Cambridge) et al. arXiv. [paper]
- [2020/02] How Much Knowledge Can You Pack Into the Parameters of a Language Model? Adam Roberts (Google) et al. arXiv. [paper]
- [2020/01] Scaling Laws for Neural Language Models. Jared Kaplan (Johns Hopkins University) et al. arXiv. [paper]
- [2017/12] Commonsense Knowledge in Machine Intelligence. Niket Tandon (Allen Institute for Artificial Intelligence) et al. SIGMOD. [paper]
- [2011/03] Natural Language Processing (almost) from Scratch. Ronan Collobert (Princeton) et al. arXiv. [paper]

Linguistic knowledge
- [2023/02] A Multitask, Multilingual, Multimodal Evaluation of ChatGPT on Reasoning, Hallucination, and Interactivity. Yejin Bang et al. arXiv. [paper]
- [2021/06] Probing Pre-trained Language Models for Semantic Attributes and their Values. Meriem Beloucif et al. EMNLP. [paper]
- [2020/10] Probing Pretrained Language Models for Lexical Semantics. Ivan Vulić et al. arXiv. [paper]
- [2019/04] A Structural Probe for Finding Syntax in Word Representations. John Hewitt et al. ACL. [paper]
- [2016/04] Improved Automatic Keyword Extraction Given More Semantic Knowledge. H Leung. Systems for Advanced Applications. [paper]

Commonsense knowledge
- [2022/10] Language Models of Code are Few-Shot Commonsense Learners. Aman Madaan et al.arXiv. [paper]
- [2021/04] Relational World Knowledge Representation in Contextual Language Models: A Review. Tara Safavi et al. arXiv. [paper]
- [2019/11] How Can We Know What Language Models Know? Zhengbao Jiang et al.arXiv. [paper]

Actionable knowledge
- [2023/07] Large language models in medicine. Arun James Thirunavukarasu et al. nature. [paper]
- [2023/06] DS-1000: A Natural and Reliable Benchmark for Data Science Code Generation. Yuhang Lai et al. ICML. [paper]
- [2022/10] Language Models of Code are Few-Shot Commonsense Learners. Aman Madaan et al. arXiv. [paper]
- [2022/02] A Systematic Evaluation of Large Language Models of Code. Frank F. Xu et al.arXiv. [paper]
- [2021/10] Training Verifiers to Solve Math Word Problems. Karl Cobbe et al. arXiv. [paper]

Potential issues of knowledge
- [2023/10] FreshLLMs: Refreshing Large Language Models with Search Engine Augmentation. Tu Vu (Google) et al. arXiv [paper] [code]
- [2023/05] Editing Large Language Models: Problems, Methods, and Opportunities. Yunzhi Yao et al. arXiv. [paper]
- [2023/05] Self-Checker: Plug-and-Play Modules for Fact-Checking with Large Language Models. Miaoran Li et al. arXiv. [paper]
- [2023/05] CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing. Zhibin Gou et al. arXiv. [paper]
- [2023/04] Tool Learning with Foundation Models. Yujia Qin et al. arXiv. [paper]
- [2023/03] SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models. Potsawee Manakul et al. arXiv. [paper]
- [2022/06] Memory-Based Model Editing at Scale. Eric Mitchell et al. arXiv. [paper]
- [2022/04] A Review on Language Models as Knowledge Bases. Badr AlKhamissi et al.arXiv. [paper]
- [2021/04] Editing Factual Knowledge in Language Models. Nicola De Cao et al.arXiv. [paper]
- [2017/08] Measuring Catastrophic Forgetting in Neural Networks. Ronald Kemker et al.arXiv. [paper]

<br/>

| [Index](./) | [Previous](6-1-agi) | [Next](6-9-memory)
