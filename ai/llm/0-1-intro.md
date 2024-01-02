---
layout: post
title: 简介
---

ChatGPT、编程 Copilot、DALL-E 等工具，给我们提供了一个非常强大的智能助手（Copiolot）。只需要我们把需求说清楚，它能帮助我们分析问题、做计划、搜集信息、看文章、写文章、写代码、画画。

它们的后面是大语言模型（LLM）。它是这样做到这一切的？如何用好它？它目前的能力怎么样，有什么不足，怎么改进？我们下面回答这些问题。

第一个问题：它是怎么做到这一切的？

我们首先介绍各种预训练大语言模型，如 BERT。它们是早期的大语言模型，为 GPT 等大语言模型打下了基础；然后介绍生成式大语言模型，即 GPT。我们然后介绍它的实现的两个客观条件：大规模模型和大规模数据。

我们然后介绍生成式大语言模型的三个核心技术。

第一个是 Zero-Shot (ZS) and Few-Shot (FS) In-Context Learning。这就是我们常说的 Prompt 技术。我们将介绍各种 Prompt 的示例、技巧和优化方法，学习如何更好地向大语言模型发出指令；我们然后介绍“检索增强的 Prompt 技术”。

第二个是 Instruction finetuning（FT）。除了模型本身的 Fine Tuning，我们也将介绍各种 Parameter Efficient FT 方法。这些方法能够让我们利用自己的数据和已有的大语言模型，高效地训练自己的大语言模型。

第三个是 Reinforcement Learning from Human Feedback (RLHF)。通过它，我们实现 LLM 和人类需求的”对齐“。OpenAI 在对齐上，花了非常大的功夫。它在 GPT 基础上，改进模型的“可使用性”和“安全性”（ HHH：Helpfulness、Honesty、Harmlessness），将系统和人类的需求“对齐”（Alignement），给我们带来了 ChatGPT 以及现在的众多生成式的人工智能产品。

我们也将介绍两种特别的 LLM：Code LLM 和视觉 LLM。它们是编程 Copilot 和 DALL-E 的基础。

第二个问题：如何用好它？

我们首先学习如何调用 API，开发基于大模型的简单应用，如对话机器人。我们然后学习智能 Agent：它们具有记忆、推理和计划的功能，因此能够完成更加复杂的工作。最后介绍我们感兴趣的大模型应用领域：教育、运维。

第三个问题：如何进一步提高大模型的能力，解决它面临的挑战？

我们首先研究它的以下能力：获得信任，获得道德，推理、语言理解、知识融入、与图结构融合等；然后介绍它对社会带来的冲击，在模型安全性上面临的挑战。我们将讨论这些挑战。学习如何减少偏见和毒舌、防止越狱与攻击。

## 课程材料

- 斯坦福 CS 224U Lec 1 Overview，[PPT](https://web.stanford.edu/class/cs224u/slides/cs224u-intro-2023-handout.pdf)

- Rich Sutton, The Bitter Lesson, March 13, 2019, [PDF](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)

<br/>

| [Index](./) | [Previous](./) | [Next](0-2-material)