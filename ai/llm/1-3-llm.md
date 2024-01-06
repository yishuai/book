---
layout: post
title: 预训练大语言模型
---

我们首先学习预训练大语言语言模型。所谓“预训练”，它指的是：利用语言模型，在海量的语料上训练 Token 的表征和模型，然后基于这些表征和模型，接着训练阅读理解、完形填空、写作等自然语言处理任务。一般来说，这样会获得很好的效果。

预训练模大语言模型有很多，比如括 BERT、RoBERTa、Electra、BART、T5、DeBERTa。我们下面介绍它们

## BERT

BERT 把 Transformer 用于 NLP 深度模型的预训练，开启了一个全新的时代。它展示了 Transformer 的强大能力能够支持更大的模型和更多的数据。从此，大语言模型开始蓬勃发展。

BERT 是在 Books 和 Wikipedia 数据上训练出来的。它的数据是 13GB。两种模型，Small 模型是 14M 参数，用 1 张 V100，训练 4 day 完成；Base 模型是 110M 参数，用 16 张 TPUv3，训练 4 day 完成。

## BERT 的 11 个朋友

BERT 之后，人们不断改进模型结构，用更多、更好的数据对模型进行训练，由此产生了一系列的大语言模型，即所谓的 BERT 的 11 个朋友。

首先，RoBERTa（2019）对 BERT 的训练方法进行了细致的梳理，提出了新的动态 Masking、调参、Loss。数据库扩大到 160GB。

此后，人们沿着两个方向进行工作：

第一个方向是 Electra（2020）和 DeBERTa v3（2021）的方向：引入“敌对”的方法。

Electra 引入了敌对的方法。它的方法是：用 BERT 对 Mask 后的单词进行补全之后，用 Electra 识别单词是不是“被模型补上的”。Electra 的训练速度比 BERT 快。它的 Small 模型也是 14M 参数，用 1 张 V100，6 hour 训练完成，比 BERT 的 4 天要短。Base 模型还是 110M 参数，16 TPUv3，4 day，这和 BERT 模型的一样。

而DeBERTa v3（2021）是 Electra 的升级版。

有意思的是，在 GPT-3 被发现有 Zero-Shot 能力之后，Electra 也被发现有这个能力。

第二个方向是 BART（2019）和 T5（2019）的方向：采用 Seq2Seq 的结构，通过生成进行训练。T5 是 BART 的升级版。

预训练大语言模型在实际中应用很广，十分值得学习。详见约翰霍普金斯 GA 课程的 PPT。

## 课程材料

- 约翰霍普金斯 GA
  - Lec 2 Preliminaries: Past, Architectures, Pre-training, Capabilities PPT： A Recent History of Language Models
  - Lec 3 BERT、ALBERT、Make BERT smaller PPT
  - Anjalie Field, Social Applications of Pre-trained Language Models, PPT

- Yandex 2023 LLM 讲座 [PPT](https://github.com/yandexdataschool/nlp_course/tree/2023/week06_llm)

- 斯坦福 CS224n Pretraining [PPT](https://web.stanford.edu/class/cs224n/slides/cs224n-2023-lecture9-pretraining.pdf) 

- [The Illustrated BERT, ELMo, and co](https://jalammar.github.io/illustrated-bert/)

- Berkeley CS294/194-196: Responsible GenAI, Berkeley, Foundations of LLM (slides)

## 论文

BERT (encoder-only models)
- [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805.pdf)
- [Deep contextualized word representations (ELMo)](https://arxiv.org/pdf/1802.05365.pdf)
- [Improving Language Understanding by Generative Pre-Training (OpenAI GPT)](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf)
- [RoBERTa: A Robustly Optimized BERT Pretraining Approach](https://arxiv.org/pdf/1907.11692.pdf)
- [ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators](https://arxiv.org/pdf/2003.10555.pdf)
- [ELECTRA is a Zero-Shot Learner, Too](https://arxiv.org/abs/2207.08141)
- [DeBERTa: Decoding-enhanced BERT with Disentangled Attention](https://arxiv.org/pdf/2006.03654.pdf)

T5 (encoder-decoder models)
- [Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer (T5)](https://arxiv.org/pdf/1910.10683.pdf)
- [BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension](https://arxiv.org/pdf/1910.13461.pdf)
- [mT5: A massively multilingual pre-trained text-to-text transformer](https://arxiv.org/pdf/2010.11934.pdf)
- [AlexaTM 20B: Few-Shot Learning Using a Large-Scale Multilingual (Seq2Seq Model)](https://arxiv.org/pdf/2208.01448.pdf)

<br/>

| [Index](./) | [Previous](1-1-lm) | [Next](1-5-gpt3)