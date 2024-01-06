---
layout: post
title: 指令微调
---

In Context Learning 有点像 GPT 歪打正着似的，发现的一种能力。它有时候产生很好的结果，有时候产生很奇怪的结果。比如，在图书、网络文本等数据集上训练的语言模型，虽然具备 Zero Shot 和 Few Shot Learning 的神奇能力，但也有一个问题，即：对比较开放的问题，语言模型不太听 Prompt 的。换句话说，它的回答和用户的想法不匹配（Align）。比如，如果要它用几句话向儿童介绍登月，它只会重复这句话：用几句话向儿童介绍登月，而不是完成我们交给它的“指令”。

那么，怎么改进呢？我们通过监督学习，来训练它输出我们希望的结果。

训练生成式大语言模型，有两种方法：“指令微调”（Instruction finetuning）和 Reinforcement Learning from Human Feedback (RLHF)。本节介绍指令微调，下节介绍 RLHF。

指令微调指的是：我们利用各种我们觉得不错的“指令-回复”数据，对大语言模型进行有监督的训练。这就是预训练大语言模型常用的 Pretraining / Finetuning 模型训练方法，即用各种“指令”去 Fine tune 它。

FLAN-T5 提出了指令微调这种方法。它的论文是《[Scaling Instruction-Finetuned Language Models](https://arxiv.org/pdf/2210.11416.pdf)》，获得的模型是 [FLAN-T5](https://huggingface.co/google/flan-t5-xxl)。我们可以访问这个网页，尝试一下它的效果，非常有意思。

FLAN-T5 进行指令微调的大规模指令数据集是 Super-Natural Instructions dataset。它包括 1.6K tasks, 3M+ examples，涵盖 Classification, sequence tagging, rewriting, translation, QA 等指令任务。提出该数据集的论文是 《[Super-NaturalInstructions: Generalization via Declarative Instructions on 1600+ NLP Tasks](https://arxiv.org/pdf/2204.07705.pdf)》。

为了对比各种指令微调后的模型效果，人们一般利用下面两个数据集：

第一个是大规模评估数据集 Massive Multitask Language Understanding (MMLU)。提出它的论文就是 《[Measuring Massive Multitask Language Understanding](https://arxiv.org/pdf/2009.03300.pdf)》。它包括 57 个需要很多知识的NLP 理解任务，包括大学生物，抽象代数，电子工程，大学数学，物理，医学等方面的习题。值得注意的是 MATH 数据也是这个作者弄的，包括了 1000 个数学竞赛题。提出 MATH 的论文是《[Measuring Mathematical Problem Solving With the MATH Dataset](https://arxiv.org/pdf/2103.03874)》。

第二个是 BIG-Bench 数据集。它包括 200+ 任务，涵盖逻辑推理，阅读理解，常识，QA，等 NLP 理解的任务。提出它的论文在 《[Beyond the Imitation Game: Quantifying and extrapolating the capabilities of language models](https://arxiv.org/pdf/2206.04615)》。这个数据包罗万象，甚至包括 ASCII art 这样的数据集。BIG-bench 包括了 127 种不同的评估集，比如“算术”、常识、判断是否说谎。[Github](https://github.com/google/BIG-bench)。

指令微调需要多少“指令”数据？需要上千条数据。我们可以基于拥有的数据情况，选择合适的使用大语言模型的策略。一般来说，当我们有几十或者上百个数据样本时，我们可以采用 Prompt 工程，通过 ICL 的方法，送入模型；当我们有上千的示例时，就可以做 Prompt tuning 等微调方法，如果有更多示例，就可以做 LoRA 等适配器方法。

指令微调现在非常流行。因为很多公司或者组织有自己的一些数据集，因此，它们一般会采用指令微调方法。

## 课程材料

- 斯坦福大学 CS 224N 第11讲 LLM [PPT](https://web.stanford.edu/class/cs224n/slides/cs224n-2023-lecture11-prompting-rlhf.pdf)

- Yandex 2022 LLM PPT

- 斯坦福 DeepLearning.AI Short Course，[Finetuning Large Language Models](https://learn.deeplearning.ai/finetuning-large-language-models), [Evaluating and Debugging Generative AI Models Using Weights and Biases](https://learn.deeplearning.ai/evaluating-debugging-generative-ai)

- 约翰霍普金斯 UA 2023 Talk, Yizhong Wang, Instruction Tuning of Large Language Models

- Berkeley Summit 2023, Stanford, Building and Studying Instruction-following Models, Slides, Video, Alpaca Tri：做指令微调的实验框架，先用 GPT-4 来做评估，然后再做真人评估

## 练习

- 斯坦福 CS224U, BERT fine-tuning with Hugging Face，[ipynb](https://github.com/cgpotts/cs224u/blob/main/finetuning.ipynb)

- 斯坦福 CS324 2022 年 Project 2 Building LLM，[PDF](https://stanford-cs324.github.io/winter2022/projects/CS324_P2.pdf)，修改数据，继续预训练 GPT-2

## 论文

普林斯顿课程论文

- Multitask Prompted Training for Zero-Shot Models
[Alexander Rush](https://rush-nlp.com/)

Refer:
- [Multitask Prompted Training Enables Zero-Shot Task Generalization](https://arxiv.org/pdf/2110.08207.pdf)
- [PromptSource: An Integrated Development Environment and Repository for Natural Language Prompts](https://arxiv.org/pdf/2202.01279.pdf)，[Github](https://github.com/bigscience-workshop/promptsource)
- [Scaling Instruction-Finetuned Language Models](https://arxiv.org/pdf/2210.11416.pdf)，FLAN paper
- [Super-NaturalInstructions: Generalization via Declarative Instructions on 1600+ NLP Tasks](https://arxiv.org/pdf/2204.07705.pdf)

约翰霍普金斯课程论文

- Generalization via Declarative Instructions on 1600+ NLP Tasks (Super-NaturalInstructions paper)
- Self-Instruct: Aligning Language Model with Self Generated Instructions (Self-Instruct paper)

<br/>

| [Index](./) | [Previous](1-7-incontext) | [Next](1-13-rlhf)
