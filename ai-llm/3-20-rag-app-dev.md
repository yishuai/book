---
layout: post
title: 检索增强应用开发
---

In-Context Learning 让人们可以通过 Prompt 输入，让大语言模型帮我们做很多事情。因此，人们就想出各种办法，把东西放到 Prompt 里，送入大语言模型。比如，把整个一篇论文送入模型，让模型给出总结；又比如，把整个一本书送进模型，让模型按照这本书，教学生。此时，In-Context Learning 的限制，就是我们能够送入模型的 Prompt 的长度了。最近，GPT-4 Turbo 能够支持 120K 的 Prompt 长度，这对送进去一本小书，是足够了。

人们提出利用搜索来增强 Prompt。这篇论文是《Demonstrate-Search-Predict: Composing retrieval and language models for knowledge-intensive NLP》，Khattab et al., 2022。

在调用 LLM API 时，我们除了送入简单的 Prompt，还可以考虑送入本地文档，这就是所谓的 RAG (Retrival Augmented Generation: 检索增强的生成)。因为知识一般是本地存储的，所以这也牵涉到本地知识和远端大语言模型如何合作的问题。Andrej Karpathy 据此提出了 LLM OS 的概念。本地知识作为 Memory，LLM 作为 CPU。

## 课程材料

- 华盛顿大学 CSE 599 同学 Slides

## 练习

- 斯坦福 CS224U HW，Few-shot OpenQA with DSP，检索增强的 Incontext-Learning，[ipynb](https://github.com/cgpotts/cs224u/blob/main/hw_openqa.ipynb)

- 斯坦福 DeepLearning.AI Short Course，[Building and Evaluating Advanced RAG Applications](https://learn.deeplearning.ai/building-evaluating-advanced-rag)

## LangChain RAG 课程

LangChain 是做 RAG 的一个常用工具

- 斯坦福 DeepLearning.AI Short Course，[LangChain for LLM Application Development](https://learn.deeplearning.ai/langchain), [LangChain: Chat with Your Data](http://learn.deeplearning.ai/langchain-chat-with-your-data), [Vector Databases: from Embeddings to Applications](https://learn.deeplearning.ai/vector-databases-embeddings-applications)。网站上有练习代码，可以调 OpenAI，非常好

- [中文入门](https://github.com/liaokongVFX/LangChain-Chinese-Getting-Started-Guide)

- [基于 Langchain 与 ChatGLM 等大语言模型的本地知识库问答应用实现](https://github.com/chatchat-space/Langchain-Chatchat)，支持 各种 Chat LLM，国内各个公司的接口、HF Embedding 模型、中文 Splitter、Agent 生态，需要 GPU，[UI 界面](https://github.com/thomas-yanxin/LangChain-ChatGLM-Webui)

- 五里墩茶社 AI [B 站视频](https://space.bilibili.com/615957867/channel/collectiondetail?sid=1234459)

- 利用微软的 [Promptflow](https://github.com/microsoft/promptflow) ，可以非常方便地实现 LLM RAG 应用，比如这个 [基于 PDF 的 ChatBot](https://github.com/microsoft/promptflow/blob/main/examples/tutorials/e2e-development/chat-with-pdf.md)

<br/>

| [Index](./) | [Previous](3-19-chatbot-opt) | [Next](5-1-agent-dev)
