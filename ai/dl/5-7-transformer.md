---
layout: post
title: Transformer
---

基于 Self-Attention，人们提出了 Transformer 这个强大的序列模型。目前所有的主流深度学习模型都是基于 Transformer 构建的，应用非常广泛。

## 模型设计

Transformer 包括四方面的设计：

首先是位置编码，应对“缺少序列信息”。为此，它采用 sin/cos 编码，获得单词的相对位置；

其次是多头注意力机制，让一个单词可以 Query 多个位置的单词。这是因为一个 Self Attention 的 Query，在做了 Softmax 后，会聚焦到一个词上。因此，用多个头（8个一般就够），让单词可以 Query 多个位置；

然后是增加非线性能力。Self-Attention 是线性的，因此，为了提高模型的模型能力，在层之间，加非线性激活函数；

最后是 Masked decoding 机制。在生成一个单词时，因为此时后面的单词还不知道，所以不能 Attention 到这些单词。所以，通过 Mask 的方式，避免模型会 Attention 到后面的单词。

## 模型结构

它具体由两部分组成：编码器和解码器。

编码器包括三部分：

1）输入、位置表征

2）自注意机制，得到 C
- Scaled QKV Attention
    - softmax(QK/sqrt(D))，D 是单词表征的维度
- 多头
    - 允许一个注意力模块，照顾到一个输入序列中的多个部分
- 对 Padding 的位置，把 Attention 分数设为负无穷，这样 softmax 后，就被忽略了

3）FF layer
- 线性后，非线性激活，再线性

解码器

1）Masked 自注意力
- Q 的 i，如果大于 K 的 j，就把 Attention 分数设为负无穷，这样softmax后，就被忽略了

2）编码器 - 解码器 注意力
- Q：从 target 来
- K，V：从 source 来
- 像前面RNN的Attention了

## 特点

Transformer 采用 Layer normalization，对一层的 a 的向量做归一化。这是因为在 MLP 中常用的 Batch normalization 在这里不太适用。首先，训练数据的 batch 小，然后，sequance 的长度不一样。

Transformer 模型有如下好处
- 适合长范围连接
- 容易并行化
- 变换能够更深
- 比 RNN 和 LSTM 都好

Transformer 的不足是它采用注意力机制。该机制的计算复杂度是 O(n^2)，很高。

## 课本

- Dive in Deep Learning，[11. Attention Mechanisms and Transformers](https://d2l.ai/chapter_attention-mechanisms-and-transformers/index.html)

## 课程材料

- 伯克利 Transformer PPT
- [The Annotated Transformer](http://nlp.seas.harvard.edu/annotated-transformer/)
- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)

### 复习题

- 画图说明 Self-Attention 的基本原理，写出其数学形式。解释为什么需要它
- 画图说明 Positional encoding 的基本原理，写出其数学形式。解释为什么需要它
- 画图说明 多头注意力 Multi-Head Attention 的基本原理，写出其数学形式。解释为什么需要它
- 画图说明 Masked attention 的基本原理，写出其数学形式。解释为什么需要它
- 画出 Transfomer 的结构图，解释每一个模块的作用

### 练习

- CS224N: Hugging Face Transformers Tutorial，[Colab](https://colab.research.google.com/drive/1pxc-ehTtnVM72-NViET_D2ZqOlpOi2LH?usp=sharing)

- 多伦多大学 Pascal Poupart 老师 CS480 深度学习课程的[练习4](https://cs.uwaterloo.ca/~ppoupart/teaching/cs480-winter23/assignments.html)。内容为 RNN 自然语言处理模型。模型包括：RNN 编码器（分类），解码器（生成），Seq2Seq（翻译）。代码已可以跑通。需要对代码进行如下修改：GRU/LSTM、解码输入（包括Category）、Attention、Transformer。

- Transformer [腾讯文档](https://docs.qq.com/doc/DT3VSdXV5UEVleGpz)

## 参考

- Berkeley Summit 2023, NVIDIA, Megatron-LM, Slides, Video

<br/>

|[Index](./) | [Previous](5-5-attention) | [Next] (8-3-exercise)
