---
layout: post
title: In-Context Learning
---

我们下面介绍 In-Context Learning （ICL）。它是生成式大语言模型的一种神奇的能力，即能够从我们送给它的少量文本中进行学习，然后输出我们需要的文本。比如：我们送给它一句话：“帮我写首诗吧，类似下面这首：床前明月光”，它就会从我们给出的例子“床前明月光”中进行学习，然后给我们写一首类似的诗。因此，In-Context Learning 是给模型送入一些 Context 文字，让模型参考这些 Context 进行生成。

ICL 的出现过程非常神奇。我猜测，与其说它是 OpenAI 主动设计的，不如说是 OpenAI 训练完 GPT 之后，发现的它的一种能力。

我们下面就来看看它是怎么出现的，以及它的演进过程。

## GPT-1

首先，人们在第一代 GPT 发现了大语言模型具有 In-Context Learning 的能力。第一代 GPT 在 2018 年完成。类似 BERT，它有 12 层 Transformer，117M 参数，在 7000 本书的 4.6GB 文本上训练。

第一代 GPT 模型训练完后，OpenAI 的研究者发现，可以用它来做“生成式的”分类。比如：要判断两句话是否矛盾（即 NLI 问题），OpenAI 把问题转化为“生成式的”，即：送进去二句话，然后问：“它们矛盾吗？答案是”。GPT 就会接着生成“是”或者“否”。这种看起来脑洞大开的方法，结果证明很有效。这就拉开了 ICL 大发展的序幕。

## GPT-2

GPT-1 出现一年后，GPT-2 出现。这是 2019年。它的论文名字是《Language Models are Unsupervised Multitask Learners》。GPT-2 的模型结构和 GPT一样，只是有了近 10倍 的参数（1.5B 参数）和数据（40 GB 文本）。这些数据中包括 Reddit 有三个赞的网文。用户点赞，说明回答得不错。

人们在第二代 GPT 中发现了更强的 ICL 能力。他们把这定义为一种 Zero Shot Learning 能力，即：不用给 GPT “两句话是否矛盾”这个问题的训练数据，直接问它就好了。OpenAI 认为这种能力是一种“无监督”的模型能力，即不需要在下游任务进行训练，就可以直接解决下游任务。当然，在 GPT 训练的语料里，一定有很多关于“矛盾”的语料，因此，GPT 应该见过类似的内容，否则它也不会有这样的能力。但这在机器学习的术语中，因为我们确实没有送进去过训练集，所以，这个被称为 Zero Shot Learning 也未尝不可。

人们基于 GPT-2 的 Zero-Shot Learning 能力，做了很多神奇的事。比如，先送入一个阅读理解的文本，然后送入一个“哪里”（where）的问题，GPT 就能够接着输出它“预测”的单词。这个单词往往是正确的。对于更难的问题，比如 Winograd Schema 挑战，它也能准确地回答“代词”（比如 it）指代的是谁。它在 LAMBADA 数据上也表现优秀，这是一些很难很难的阅读理解题。

特别有意思的是这个例子：人们发现，送入一段文本后，如果加一个 TL;DR（Too Long，Don't Read），GPT-2 就能输出总结。这就让人脑洞大开了。这让人们感到好奇：在 GPT-2 的 1.5B 参数模型中，到底有些什么。纷纷尝试各种方法探索。

## GPT-3

GPT-2 之后，OpenAI 继续提高模型和数据量的规模。一年后， GPT-3 出现了。它有 175B 参数，600GB 数据。这是 2020 年。

然后，人们在第三代 GPT 发现模型有 Few Shot Learning 的 ICL 能力。这篇论文的名字是《[Language Models are Few-Shot Learners](https://arxiv.org/pdf/2005.14165.pdf)》，非常经典。在这篇神奇的论文中，OpenAI 说明：GPT-3 具有 Few Shot 能力，即：给它几个例子，它就会照猫画虎地模仿着做。比如翻译单词，Word unscrambling 等。想想：我们人类不就是这么学习的吗？

要注意的是，GPT 的生成，只是“预测”后面的单词。所以并不是“事实”。除了很多令人满意的结果，人们也发现了很多奇怪的失败。详见 Yandex PPT。

## 思维链

最后，人们提出了“思维链”的 ICL 技术。它包括两种：

第一种思维链技术是 Few Shot 的。

GPT-3 的照猫画虎能力存在两个不足：1）对于数学运算，比如加法运算，如果只是给例子，人也会一头雾水，不知道这个符号到底什么意思，模型也很难找出其背后的数学规律；2）对于多步推理的任务，比如多步数学推理，如果不一步步说清楚地话，人也会很懵，模型也很难找出背后的逻辑顺序。

为此，谷歌的科学家提出了“思维链”（Chain of Thought）方法。就是在给例子的时候，不仅给出答案，还用自然语言，给出推理的步骤。然后，在生成时，首先生成推理的步骤，然后再生成答案。这就是 CoT Prompt：给出推理的思维链。

思维链技术需要一定的数据量。在 GSM8K 中学数学题上的测试表明，当模型参数一上 100B，性能迅速提高，接近有监督模型。但是，当模型参数少的时候，改进不多。这就是说，如果要它产生效果的话，模型的规模需要超过一定的门限。后来人们把这个现象称为“涌现”。这篇论文的题目是《[Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/pdf/2201.11903.pdf)》，介绍的[网页](https://ai.googleblog.com/2022/05/language-models-perform-reasoning-via.html)。

思维链技术给大语言模型带来了“推理”。比如，后来人们提出将思维的中间过程记录下来，不断地 Prompt。这篇论文就是《[Show Your Work: Scratchpads for Intermediate Computation with Language Models](https://arxiv.org/pdf/2112.00114.pdf)》。

第二种思维链技术是 Zero Shot 的，即：我们不给例子，而是直接输入：“Let's think step by step”。此时，我们发现：大语言模型就能进行有步骤的推理！

Zero Shot 的思维链技术，说明模型本身已学会了一定的推理能力，这让整个世界都感到震惊。这篇论文的题目是《[Large Language Models are Zero-Shot Reasoners](https://arxiv.org/pdf/2205.11916.pdf)》。在 MultiArith 和 GSM8K 这两个数据集上的评估显示，这样做虽比不上 Few Shot 的 CoT，但比没用 CoT 的 Zero-Shot 好很多很多。

人们然后继续优化，寻找最佳的思维链 Prompt。比如，人们用 LLM 生成各种 Prompt，然后进行了评估，结果发现，性能最好的是：Let's work this out in a step by step way to be sure we have the right answer ( 82 分 )；第二好的是：Let's think step by step（78.7 分）。有意思的是，Let's think like a detective step by step 只有 70.3 分。看来大语言模型不喜欢比喻。这篇论文即《[Large Language Models Are Human-Level Prompt Engineers](https://arxiv.org/pdf/2211.01910.pdf)》。

从用 LLM 解决 NLP 问题，到思维链技术，这就是 In-Context Learning 发展的历史。

### 课程材料

- 约翰霍普金斯 GA, Jason Wei, Emergence and reasoning in large language models, CoT, Self Consistency, PPT

- 斯坦福大学 CS 224N 第11讲 LLM [PPT](https://web.stanford.edu/class/cs224n/slides/cs224n-2023-lecture11-prompting-rlhf.pdf)

- 斯坦福 CS 224U: In-context learning，[PPT](https://web.stanford.edu/class/cs224u/slides/cs224u-incontextlearning-2023-handout.pdf)

- Yandex 2023 LLM [PPT](https://drive.google.com/file/d/1IOx71suOn8uF_AbNrPhQxjnNNA5UGQY1/view?usp=share_link)

## 论文

普林斯顿课程阅读论文列表

- GPT-3 (decoder-only models)
  - [Language Models are Few-Shot Learners (GPT-3)](https://arxiv.org/pdf/2005.14165.pdf)
  - [Language Models are Unsupervised Multitask Learners (GPT-2)](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)

- In-context learning
  - [Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?](https://arxiv.org/pdf/2202.12837.pdf)
  - [An Explanation of In-context Learning as Implicit Bayesian Inference](https://arxiv.org/pdf/2111.02080.pdf)

- Refer
  - [What Makes Good In-Context Examples for GPT-3?](https://arxiv.org/pdf/2101.06804.pdf)
  - [Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity](https://arxiv.org/pdf/2104.08786.pdf)
  - [Data Distributional Properties Drive Emergent In-Context Learning in Transformers](https://arxiv.org/pdf/2205.05055.pdf)
  - [What Can Transformers Learn In-Context? A Case Study of Simple Function Classes](https://arxiv.org/pdf/2208.01066.pdf)

约翰霍普金斯大学推荐论文

In-context Learning 

Suggested Reading:
- Beyond the Imitation Game: Quantifying and extrapolating the capabilities of language models
Additional Reading:
- Language Models are Few-Shot Learners (GPT3 paper)

Additional Reading(s):
- On the Effect of Pretraining Corpora on In-context Learning by a Large-scale Language Model
- What Can Transformers Learn In-Context? A Case Study of Simple Function Classes
- In-context Learning and Induction Heads

Limits of In-context Learning 1

Suggested Reading:
- Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?

Additional Reading(s):
- Data Distributional Properties Drive Emergent In-Context Learning in Transformers
- Beyond the Imitation Game: Quantifying and extrapolating the capabilities of language models
- How does in-context learning work? A framework for understanding the differences from traditional supervised learning

Limits of In-context Learning 2

Suggested Reading:
- Impact of Pretraining Term Frequencies on Few-Shot Reasoning

Additional Reading(s):
- Do Prompt-Based Models Really Understand the Meaning of Their Prompts?
- How transferable are features in deep neural networks?
- Frequency Effects on Syntactic Rule Learning in Transformers

<br/>

| [Index](./) | [Previous](1-5-gpt3) | [Next](1-11-finetune)
