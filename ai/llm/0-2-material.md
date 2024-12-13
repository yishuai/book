---
layout: post
title: 材料
---

目前的课程材料包括四类：

第一类是在自然语言处理（NLP）的课程中，有大语言模型的一章或者几章。这包括斯坦福大学的 NLP 经典课程 CS224n 中的一课；CS224U、CS329X 中的几课；Yandex 中的几课；DeepMind 和 Raspbery Pi 面向高中生的课程中的一课。这些课的材料如下：

- 斯坦福
  - CS224n Natural Language Processing with Deep Learning，大语言模型讲座，[材料](https://web.stanford.edu/class/cs224n/)
  - CS224U Natural Language Understanding，[材料](https://web.stanford.edu/class/cs224u/)，[代码](https://github.com/cgpotts/cs224u)
  - CS329X: Human-Centered NLP，[材料](https://web.stanford.edu/class/cs329x/)

- Yandex NLP，[2023](https://github.com/yandexdataschool/nlp_course/tree/2023/)，[2022](https://github.com/yandexdataschool/nlp_course/tree/2022)

- DeepMind，Raspberry Pi，Large Language Models (LLMs)，高中及以上，[材料](https://experience-ai.org/en/units/experience-ai-lessons/lessons/7)

第二类是老师讲授的 LLM 课。这包括斯坦福大学 CS324 的 2022 年版本；约翰霍普金斯大学老师的课程。这些课程的 PPT 是老师做的，属于课程材料。这些课程的材料如下：

- 斯坦福 CS324 2022 年 Large Language Models，[材料](https://stanford-cs324.github.io/winter2022)

- 约翰霍普金斯 UA，NLP: Self-supervised Models 本科，CS 601.471/671 [Spring 2024](https://self-supervised.cs.jhu.edu/sp2024/), [Spring 2023](https://self-supervised.cs.jhu.edu/sp2023/)

- 李宏毅，2024 春，生成式人工智能导论，[B 站视频](https://www.bilibili.com/video/BV1BJ4m1e7g8)

- 滑铁卢大学，Wenhu Chen, 2024 冬，CS 886: Recent Advances on Foundation Models，[网站](https://cs.uwaterloo.ca/~wenhuche/teaching/cs886/)，包括 PPT，Youtube 视频

第三类是研究生的论文研讨课。由研究生来讲论文。这包括华盛顿大学 Choi 老师、普林斯顿大学陈丹琪老师、约翰霍普金斯大学老师的课程。这些课程的 PPT 是同学做的，属于参考材料。这些课程的材料如下：

- 华盛顿大学，CSE 599 Exploration on Language, Knowledge, and Reasoning，[2023](https://cse599d1wi23.notion.site/cse599d1wi23/CSE-599-D1-Winter-2023-fe73cb56c11b45efb34e94c090480791)

- 普林斯顿，COS 597G (Fall 2022): Understanding Large Language Models，[材料](https://www.cs.princeton.edu/courses/archive/fall22/cos597G/)

- 约翰霍普金斯，GA（研究生），CSCI 601.771: Advanced Self-supervised Statistical Models，Fall 2022，[材料](https://self-supervised.cs.jhu.edu/fa2022/)

我们主要学习前两类课程的材料，然后参考第三类课程的论文列表。

第四类是聚焦应用开发的课程，这包括 Ng 老师的入门课，DeepLearing 网站上的全套练习课；伯克利 LLM 训练营；

- Ng 老师
  - Generative AI for Everyone 课程（[B 站视频](https://www.bilibili.com/video/BV11G411X7nZ)，[Coursera](https://www.coursera.org/learn/generative-ai-for-everyone)）。该课程包括 30 课，6 小时，三个单元：简介，项目，商业与社会。
  - DeepLearning.AI，[网站](https://www.deeplearning.ai/)
  - Letters from Andrew Ng，Personal messages to the AI community，[网站](https://www.deeplearning.ai/the-batch/tag/letters/)

- 伯克利
  - LLM 训练营，全栈深度学习，[LLM Bootcamp](https://fullstackdeeplearning.com/llm-bootcamp/spring-2023/)，2023
  - CS294/194-196: Responsible GenAI and Decentralized Intelligence, [Website](https://rdi.berkeley.edu/responsible-genai/f23)
  - The Future of Decentralization, AI, and Computing Summit! [Website](https://rdi.berkeley.edu/events/decentralizationaisummit)

第五类是面向科研人员的快速技术培训课程，包括 Karpathy 老师的介绍课。

- Andrej Karpathy 《给忙碌人的大语言模型介绍》，[中文论文列表](https://mp.weixin.qq.com/s/mt9W8Mf0LbZjbuRObyeWeQ)，[英文论文列表](https://blog.oxen.ai/reading-list-for-andrej-karpathys-intro-to-large-language-models-video/)，[Youtube 视频](https://www.youtube.com/results?search_query=Andrej+Karpathy)

- Andrej Karpathy，LLM101n: Let's build a Storyteller, [Github](https://github.com/karpathy/LLM101n)
  - Syllabus
    - Chapter 01 Bigram Language Model (language modeling)
    - Chapter 02 Micrograd (machine learning, backpropagation)
    - Chapter 03 N-gram model (multi-layer perceptron, matmul, gelu)
    - Chapter 04 Attention (attention, softmax, positional encoder)
    - Chapter 05 Transformer (transformer, residual, layernorm, GPT-2)
    - Chapter 06 Tokenization (minBPE, byte pair encoding)
    - Chapter 07 Optimization (initialization, optimization, AdamW)
    - Chapter 08 Need for Speed I: Device (device, CPU, GPU, ...)
    - Chapter 09 Need for Speed II: Precision (mixed precision training, fp16, bf16, fp8, ...)
    - Chapter 10 Need for Speed III: Distributed (distributed optimization, DDP, ZeRO)
    - Chapter 11 Datasets (datasets, data loading, synthetic data generation)
    - Chapter 12 Inference I: kv-cache (kv-cache)
    - Chapter 13 Inference II: Quantization (quantization)
    - Chapter 14 Finetuning I: SFT (supervised finetuning SFT, PEFT, LoRA, chat)
    - Chapter 15 Finetuning II: RL (reinforcement learning, RLHF, PPO, DPO)
    - Chapter 16 Deployment (API, web app)
    - Chapter 17 Multimodal (VQVAE, diffusion transformer)
  - Further topics to work into the progression above:
    - Programming languages: Assembly, C, Python
    - Data types: Integer, Float, String (ASCII, Unicode, UTF-8)
    - Tensor: shapes, views, strides, contiguous, ...
    - Deep Learning frameworks: PyTorch, JAX
    - Neural Net Architecture: GPT (1,2,3,4), Llama (RoPE, RMSNorm, GQA), MoE, ...
    - Multimodal: Images, Audio, Video, VQVAE, VQGAN, diffusion

- LLM Course: Course to get into Large Language Models (LLMs) with roadmaps and Colab notebooks, 非常全面、细致、实战的一套课程，包括三部分：LLM 基础（数学、Python for ML、神经元网络、NLP），LLM 原理（LLM 模型、数据集、预训练模型、SFT、RLHF、评估、存储优化、新趋势），LLM 应用（运行、向量存储、检索增强、运行优化、部署、安全），[Github](https://github.com/mlabonne/llm-course)
  - LLM Fundamentals covers essential knowledge about mathematics, Python, and neural networks.
  - The LLM Scientist focuses on building the best possible LLMs using the latest techniques.
  - The LLM Engineer focuses on creating LLM-based applications and deploying them.

- Scrimba，https://www.coursera.org/specializations/ai-engineering

## 课本

在课本方面，最经典的 SLP 课本中的第 12 章 Prompting and Instruct Tuning，还没有出。相关的技术方面的课本有：

语言模型
- Dan Jurafsky and James H. Martin, Speech and Language Processing (3rd ed. draft， Auguest， 2024), [网站](https://web.stanford.edu/~jurafsky/slp3/)
  - 3: N-gram Language Models
  - 2:	Regular Expressions, Tokenization, Edit Distance
    - 2: Text Processing - [pptx] [pdf]
    - 2: Edit Distance [pptx] [pdf]
  - 3:	N-gram Language Models
    - 3: [pptx] [pdf]
  - 4:	Naive Bayes, Text Classification, and Sentiment
    - 4: [pptx] [pdf]
  - 5:	Logistic Regression
    - 5: [pptx] [pdf]
  - 6:	Vector Semantics and Embeddings
    - 6: [pptx] [pdf]
  - 7:	Neural Networks
    - 7: [pptx] [pdf]
  - 8:	RNNs and LSTMs
  - 9:	Transformers
    - 9: [pptx] [pdf]
  - 10:	Large Language Models
    - 10: [pptx] [pdf]
  - 11:	Masked Language Models
  - 12:	Model Alignment, Prompting, and In-Context Learning
  - 14: Question Answering, Information Retrieval, and RAG

NLP 编程
- Delip Rao and Brian McMahan. Natural Language Processing with PyTorch (requires Stanford login).
- Lewis Tunstall, Leandro von Werra, and Thomas Wolf. Natural Language Processing with Transformers

NLP
- Jacob Eisenstein. Natural Language Processing
- Yoav Goldberg. A Primer on Neural Network Models for Natural Language Processing

深度学习
- Ian Goodfellow, Yoshua Bengio, and Aaron Courville. Deep Learning
- Eugene Charniak. Introduction to Deep Learning
- Michael A. Nielsen. Neural Networks and Deep Learning

## 资源

- Awesome-LLM: a curated list of Large Language Model，[Github](https://github.com/Hannibal046/Awesome-LLM)

- OpenAI Research，[Webpage](https://openai.com/research)

- 生成式 AI 和 LLM 资源 [Github](https://www.github-zh.com/projects/532465933-ai-notes)

- Large language models from scratch （[Youtube](https://youtu.be/lnA9DMvHtfI)） and Large Language Models: Part 2 ([Youtube](https://youtu.be/YDiSFS-yHwk)) - Graphics in 5 Minutes on YouTube

- 通往 AGI 之路，[飞书](https://waytoagi.feishu.cn/wiki/QPe5w5g7UisbEkkow8XcDmOpn8e)

<br/>

| [Index](./) | [Previous](0-1-intro) | [Next](1-1-lm)
