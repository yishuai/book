---
layout: post
title: RLHF
---

虽然指令微调让语言模型学会了响应人的指令，但它还有两个不足：首先，对那些	开放任务，比如写一首诗，它们没有标准答案，怎么训练模型，让它能写一首好诗？其次，因为	有监督的学习，用单词是否匹配做 Loss，这和人对模型输出质量的判断其实不一致，比如：同义词其实也可以，而且不同的单词，重要性不一样。

本节介绍 Reinforcement Learning with Human Feedback（RLHF），即利用增强学习的方法，由“人”提供反馈，训练模型的策略，让它输出符合人类偏好（Preference）的结果。RLHF 让模型能够输出“人”真正想要的结果。

RLHF 是一种增强学习（RL）方法。增强学习是一个经典的学习模型，2013 年 Deep RL 将深度学习引入增强学习，产生了 AlphaGo 这样的人工智能机器人。但是，因为语言模型的增强学习很难调，所以增强学习一直没有被应用于语言模型。2017 年 OpenAI 发明了增强学习的 PPO 算法，让增强学习可以在大的神经元模型上训练。此后，慢慢出现了用增强学习进行语言模型的算法学习。

我们下面介绍 RLHF 的算法。我们的问题是：s 是 LM 的输出。我们希望优化我们的模型，最大化 Reward 的期望：E[R(s)]。为此，我们采用经典的求解增强学习问题的策略梯度方法（REINFORCE，1992年）。

## 策略梯度

我们首先介绍策略梯度的基本方法。我们的问题是：因为我们的目的是用梯度上升来最大化策略获得的 Reward，所以我们需要得到 Reward 对模型参数的梯度。这时，我们遇到一个难题，就是我们的 Reward 对模型参数并不可微，这怎么办？

为此，策略梯度方法采用了一个很有意思的技巧：log-导数的方法，把梯度变成 Reward 加权的 p(s) 的 Log 对模型参数的梯度的期望。p(s) 的 Log 对模型参数的梯度是可以通过深度学习模型获得的。因此，我们可以通过多次实验（即蒙特卡洛方法），得到这一梯度的期望。

这也正是“增强学习”为什么叫做“增强”的原因。因为用 Reward 做加权，这意味着，如果 Reward > 0，那么我们就会加上这个梯度，那么模型的参数就会往这个方向调，相对于“增强”这个方向；相反，如果 Reward < 0，那么我们就会减去这个梯度，那么模型的参数就会往反方向调。这就是我们为什么叫这个算法是“增强学习”的原因。利用这种方法，对任意不可微的 reward 函数，我们就都可以做增强学习了。

## Reward 学习

我们然后介绍 RLHF 采用的学习 Reward 的方法。它学习的是人的“偏好”（Preference）。具体来说，它通过“成对比较”，收集人类的偏好，然后专门训练一个深度学习模型，来预测人类的偏好。这个模型，就被用来作为 LM 的 reward 模型。DeepMind 的科学家发现，用 10B 参数，64K 数据，得到的 LM reward 模型就接近单个人的了。这篇极为重要的论文是《[Deep reinforcement learning from human preferences](https://arxiv.org/pdf/1706.03741.pdf)》。当然，后面也有研究者发现 模型预测的人的偏好并不可靠，比如论文《[Learning to summarize from human feedback](https://arxiv.org/pdf/2009.01325.pdf)》。

在 Reward 函数中，除了用户偏好，还包括最新模型输出分布和 RL 训练前模型输出分布的 KL 距离。这是因为他们不希望模型输出的分布有太大变化：因为 Reward 模型是基于 RL 训练前的模型输出获得的，所以，如果输出分布偏离了 RL 训练前的模型输出，那么 Reward 模型就失效了，语言模型的输出就会非常奇怪。

## InstructGPT

基于 RLHF 方法，OpenAI 的科学家开始训练 GPT 模型，让它输出符合人类偏好的回答，这就是 InstructGPT。这篇论文就是《[Training language models to follow instructions with human feedback](https://arxiv.org/pdf/2203.02155.pdf)》。OpenAI 的科学家发现，通过 RLHF 训练，模型的表现比“指令微调”后的模型有很大增益。

OpenAI 在训练 InstructGPT 的过程中，对 30K 任务进行了用户打标。这些任务包括	随机任务、	Few-shot 任务，还有很多用户提出的任务，比如头脑风暴：提出5个想法，恢复职业热情；文本生成：生成一个短故事，描述熊去了海边，交了朋友，又回家。他们首先做预训练，训练语言模型，预测下一个单词。然后训练Seq2Seq 的条件语言模型，包括编码器 - 解码器。在解码时采用 Beam Search 进行序列解码。基于 InstructGPT，OpenAI 最终推出了 [ChatGPT](https://openai.com/blog/chatgpt/)，掀起了至今都方兴未艾的 GPT 革命。

## 课程材料

- 斯坦福大学 CS 224N 第11讲 LLM [PPT](https://web.stanford.edu/class/cs224n/slides/cs224n-2023-lecture11-prompting-rlhf.pdf)

- Yandex 2023 RLHF PPT

- 华盛顿大学 CSE 599 同学 Slides

- 斯坦福 DeepLearning.AI RLHF Short Course，[网站](https://learn.deeplearning.ai/reinforcement-learning-from-human-feedback)

- 约翰霍普金斯 UA 2024 Lec 13 Adaptation as alignment to human instructions:
    - Instruction-tuning
    - RLHF and variants

## RLHF 论文

Andrej Karpathy 推荐论文

- Training Language Models to Follow Instructions (InstructGPT)，[论文链接](https://arxiv.org/abs/2203.02155)，[Arxiv Dive](https://blog.oxen.ai/training-language-models-to-follow-instructions-instructgpt/)
    - 从GPT-3到ChatGPT的大语言模型技术，涵盖微调、RLHF和对齐
    - GPT3 + RLHF paper

- RLAIF: Scaling Reinforcement Learning from Human Feedback with AI Feedback，[论文链接](https://arxiv.org/abs/2309.00267)，
    - 人工标注通常是LLM训练和对齐的最后步骤中的瓶颈。RLAIF使用现有的LLM来帮助以比人类更快的速度标注数据，以达到类似的结果

- Direct Preference Optimization: Your Language Model is Secretly a Reward Model，[论文链接](https://arxiv.org/abs/2305.18290)、[Semantic Scholar](https://www.semanticscholar.org/paper/Direct-Preference-Optimization%3A-Your-Language-Model-Rafailov-Sharma/0d1c76d45afa012ded7ab741194baf142117c495)
    - DPO被提议作为RLHF的更稳定的替代品。DPO稳定、高性能且计算量轻，无需拟合奖励模型、在微调期间从 LM 采样或执行重要的超参数调整
    - RLHF 需要首先学习深度 Reward 模型，然后进行采样。Manning 老师提出 DPO，学习 Closed form 形式的 Rewards，这样就不需要再采样了，而是直接判断策略是否最优，这样就把问题变为一个直接的分类问题，以学习最优策略。2023 年 12 月 28 日，该论文已经有 175 个引用。
    - NeurIPS 2023 Best Paper

JHU 课程推荐论文

- [Illustrating Reinforcement Learning from Human Feedback](https://huggingface.co/blog/rlhf)
- Deep reinforcement learning from human preferences (an early RLHF paper)

普林斯顿课程论文

- [Learning to summarize from human feedback](https://arxiv.org/pdf/2009.01325.pdf)
- [Fine-Tuning Language Models from Human Preferences](https://arxiv.org/pdf/1909.08593.pdf)
- [MemPrompt: Memory-assisted Prompt Editing with User Feedback](https://arxiv.org/pdf/2201.06009.pdf)
- [LaMDA: Language Models for Dialog Application](https://arxiv.org/pdf/2201.08239.pdf)

## 对齐 论文

- [A General Language Assistant as a Laboratory for Alignment](https://arxiv.org/pdf/2112.00861.pdf)
- [Alignment of Language Agents](https://arxiv.org/pdf/2103.14659.pdf)
- [Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback](https://arxiv.org/pdf/2204.05862.pdf)

## NLP 中的 RL 论文

华盛顿大学课程论文

Is reinforcement learning (not) for NLP?

***Why has RL not been impactful for NLP? Why do we hear about RLHF (RL with human feedback) now?***

1. [Deep reinforcement learning from human preferences (OpenAI, 2017)](https://arxiv.org/abs/1706.03741)
1. [Learning to summarize from human feedback (OpenAI, 2020)](https://arxiv.org/abs/2009.01325)
1. [Training language models to follow instructions with human feedback (OpenAI, 2022)](https://arxiv.org/abs/2203.02155)
1. [Is Reinforcement Learning (Not) for Natural Language Processing?: Benchmarks, Baselines, and Building Blocks for Natural Language Policy Optimization (Ramamurthy et al., 2022)](https://arxiv.org/abs/2210.01241)
1. [Quark: Controllable Text Generation with Reinforced Unlearning (Lu et al., 2022)](https://arxiv.org/abs/2205.13636)
1. [ScienceWorld: Is your Agent Smarter than a 5th Grader? (Wang et al., 2022)](https://arxiv.org/abs/2203.07540)
1. [Training Language Models with Language Feedback (Scheurer et al., 2022)](https://arxiv.org/abs/2204.14146)
1. [Constitutional AI: Harmlessness from AI Feedback (Bai et al., 2022)](https://arxiv.org/abs/2212.08073)
1. [Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback (Bai et al., 2022)](https://arxiv.org/abs/2204.05862)
1. [Proximal Policy Optimization (PPO) (OpenAI, 2017)](https://openai.com/blog/openai-baselines-ppo/)
1. [Self-critiquing models for assisting human evaluators (Saunders et al., 2022)](https://arxiv.org/abs/2206.05802)

## Human Feedback 的不一致性论文

Ambiguity: do we continue pretending that it doesn’t exist?
歧义：我们是否继续假装它不存在？

***Are ambiguous cases just human annotation noise? Do ambiguous examples hurt machine learning?***
歧义案例只是人类注释噪音吗？模棱两可的例子会损害机器学习吗？

1. [Did It Happen? The Pragmatic Complexity of Veridicality Assessment (de Marneffe et al., 2012)](https://aclanthology.org/J12-2003/)
1. [Inherent Disagreements in Human Textual Inferences (Pavlick & Kwiatkowski, 2020)](https://aclanthology.org/Q19-1043/)
1. [AmbigQA: Answering Ambiguous Open-domain Questions (Min et al., 2020)](https://aclanthology.org/2020.emnlp-main.466/)
1. [Jury Learning: Integrating Dissenting Voices into Machine Learning Models (Gordon et al., 2022)](https://arxiv.org/abs/2202.02950)
1. [Fine-tuning language models to find agreement among humans with diverse preferences (Bakker, 2022)](https://arxiv.org/abs/2211.15006)
1. [Investigating Reasons for Disagreement in Natural Language Inference (Jiang & de Marneffe, 2022)](https://arxiv.org/abs/2209.03392)
1. [The 'Problem' of Human Label Variation: On Ground Truth in Data, Modeling and Evaluation (Plank, 2022)](https://arxiv.org/abs/2211.02570)

<br/>

| [Index](./) | [Previous](1-11-finetune) | [Next](2-5-model)
