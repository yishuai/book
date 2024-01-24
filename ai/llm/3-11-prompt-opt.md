---
layout: post
title: Prompt 优化
---

除了工程师们在研究 Prompt，学术界也在研究 Prompt。本节学习学术界的 Prompt 优化工作。它们有两类：得到更好的输出；抑制不想要的输出（比如 Bias）。我们称前者为 Prompt 优化，后者为“校准：Calibration”。

## Prompt 性能评估

人们首先评估了各种 Prompt 问法，下面是一些发现：

首先，问法很重要，比如：问一个情感分类问题，有各种问法。它们的性能不同。《Calibrate Before Use: Improving Few-Shot Performance of Language Models》, ICML 2021。

其次，例子的顺序也有关系，有时候是最好的，有时候接近随机。《Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity》, ACL 2022

然后，Label 是否正确，并不重要，但 Label 的内容重要。这个很神奇。《Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity》, ACL 2022

然后，通过优化方法，得到的下游任务性能最好的 Prompt 往往很难理解，简直是 Gibberish：《AUTOPROMPT: Eliciting Knowledge from Language Models with Automatically Generated Prompts》, 2020；《iPrompt: Explaining Data Patterns in Natural Language via Interpretable Autoprompting》。

最后，人习惯于逐渐调整 Prompt；Prompt 技巧是可以学习的，而学习的方法包括课程和在线社区的经验分享；Prompt 可以通过检索相关信息来加强；用户的 Prompt 包括描述性和指令性两种；当前 Prompt 的性能如何，等等。详见斯坦福 CS224U 的研究者从人机交互的角度，对 Prompt 的研究。

## Prompt 方法

人们也提出了各种神奇的 Prompt 方法：

首先，是告诉 GPT 它的“人设”，比如：“You are a high-school computer science expert"。这叫 “In-Context Impersonation” 技术。这篇论文是《In-Context Impersonation Reveals Large Language Models' Strengths and Biases》, 2023 年出版。

其次，是选择“自一致”的结果，即：要 GPT 返回多个结果（因为 GPT 有随机性，每次回答得会不一样），然后选择这些结果中比较稳定的结果。这就叫“Self-Consistency” 技术。这篇论文是《Self-Consistency Improves Chain of Thought Reasoning in Language Models》, 发表于 ICLR 2023。

然后，是先 Prompt，用 LLM 产生一些知识，然后用这些知识来增强 Prompt。这叫 “Generated Knowledge Prompting”。这篇论文是《Generated Knowledge Prompting for Commonsense Reasoning》, ACL 2022。

然后，是把问题分解为子问题，然后一步步地 Prompt，即：先问 To solve xx, we need to first solve, 得到第一步；然后 Prompt 得到第一步的解答；然后把解答拼到原题的后面，再问。当然，也可以 Prompt “Let’s break down the problem: ”， “What are the steps needed to solve the task?”。这叫 “Least-to-Most Prompting” 技术。

## 课程材料

- Yandex 2023 LLM [PPT](https://drive.google.com/file/d/1IOx71suOn8uF_AbNrPhQxjnNNA5UGQY1/view?usp=share_link)

- 约翰霍普金斯 UA 2024 Lec 11 in-context learning
  - Definition and importance
  - Making sense of it
  - Adapting models (prompt engineering)
  - Multi-step prompting
  - Failures of ICL

- 斯坦福 CS 224U: Prompters before prompts and promptees [PPT](https://drive.google.com/file/d/1RIOAOTOOPyVLezFiIfGnYJSE8ofKuR4L/view)

- Learn Prompting，Intermediate，[Webpage](https://learnprompting.org/docs/category/%EF%B8%8F-intermediate)，包括上面提到的 Prompt 优化方法

- Jessica Rumbelow, mwatkins，[SolidGoldMagikarp (plus, prompt generation)](https://www.lesswrong.com/posts/aPeJE8bSo6rAFoLqg/solidgoldmagikarp-plus-prompt-generation)，6th Feb 2023

- Learn Prompting, Calibrating LLMs, [Webpage](https://learnprompting.org/docs/reliability/calibration)

## 练习

- Yandex NLP LLM [2023](https://github.com/yandexdataschool/nlp_course/blob/2023/week06_llm/practice.ipynb)，[2022](https://github.com/yandexdataschool/nlp_course/blob/2022/week08_llm/practice.ipynb)

- 斯坦福 CS324 2022 年 Project 1 Evaluating LLM Task 1， [PDF](https://stanford-cs324.github.io/winter2022/projects/CS324_P1.pdf)，评估 GPT-3 在 ANLI 上的效果

## 优化论文

普林斯顿课程阅读论文列表

- Prompting for few-shot learning
  - [Making Pre-trained Language Models Better Few-shot Learners](https://arxiv.org/pdf/2012.15723.pdf)，论文很好，自动 label 单词、模版搜索
  - [blog post](https://gaotianyu.xyz/prompting/)
  - [How Many Data Points is a Prompt Worth?](https://arxiv.org/pdf/2103.08493.pdf)

- Refer
  - [Exploiting Cloze Questions for Few Shot Text Classification and Natural Language Inference](https://arxiv.org/pdf/2001.07676.pdf)
  - [True Few-Shot Learning with Language Models](https://arxiv.org/pdf/2105.11447.pdf)
  - [Cutting Down on Prompts and Parameters: Simple Few-Shot Learning with Language Models](https://arxiv.org/pdf/2106.13353.pdf)
  - [Pre-train, Prompt, and Predict: A Systematic Survey of Prompting Methods in Natural Language Processing](https://arxiv.org/pdf/2107.13586.pdf)

## Calibration 论文

普林斯顿

- Calibration of prompting LLMs
  - [Calibrate Before Use: Improving Few-Shot Performance of Language Models](https://arxiv.org/pdf/2102.09690.pdf)
  - [Surface Form Competition: Why the Highest Probability Answer Isn’t Always Right](https://arxiv.org/pdf/2104.08315.pdf)

- Refer
  - [Noisy Channel Language Model Prompting for Few-Shot Text Classification](https://arxiv.org/pdf/2108.04106.pdf)
  - [How Can We Know When Language Models Know? On the Calibration of Language Models for Question Answering](https://arxiv.org/pdf/2012.00955.pdf)
  - [Language Models (Mostly) Know What They Know](https://arxiv.org/pdf/2207.05221.pdf)

JHU 课程参考论文

Calibration 1
- Calibrate Before Use: Improving Few-Shot Performance of Language Models

Additional Reading:
- Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity (LMs are sensitive to ICL example orders)
- Reframing Instructional Prompts to GPTk's Language (LMs are sensitive to phrasing of prompts)
- Beyond the Imitation Game: Quantifying and extrapolating the capabilities of language models

Calibration 2
- Language Models (Mostly) Know What They Know

Additional Reading(s):
- How Can We Know When Language Models Know? On the Calibration of Language Models for Question Answering
- An Information-theoretic Approach to Prompt Engineering Without Ground Truth Labels

## 人机交互优化

从人机交互的角度，评估当前 Prompt 方法的有效性评估

斯坦福 CS224U 推荐论文

- Evaluating Human-Language Model Interaction (Lee et al., 2022)
- Do Prompt-Based Models Really Understand the Meaning of Their Prompts? (Webson and Pavlick, 2022)，这篇论文很有意思。
- Are Language Models Worse than Humans at Following Prompts? It’s Complicated (Webson et al., 2023)
- GPT-4 Technical Report (OpenAI, 2023)

捕捉和分析 Prompt 过程的 Interaction Trace

- CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities (Lee et al., 2022)
- Choice Over Control: How Users Write with Large Language Models using Diegetic and Non-Diegetic Prompting (Dang et al., 2023)

## 教程

- LLM Observability，2023 年 9 月，[教程](https://arize.com/blog-course/large-language-model-monitoring-observability/)

## 系统

- Prompt base: All things prompt engineering, 论文 《Can Generalist Foundation Models Outcompete Special-Purpose Tuning? Case Study in Medicine》 提出的方法，包括三个技术：dynamic few-shot selection, self-generated chain of thought, and choice-shuffle ensembling，效果好。[Github](https://github.com/microsoft/promptbase)

## 
<br/>

| [Index](./) | [Previous](3-10-prompt-vision) | [Next](3-17-chatbot-dev)

