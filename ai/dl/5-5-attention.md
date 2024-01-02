---
layout: post
title: Attention
---

本节介绍 Attention 和 Self-Attention。

Seq2Seq 的一个问题是，输入序列的所有信息都被编码器编入了一个隐状态（在数学上，它是一个向量）。然后，解码器就依靠这个向量进行序列生成。因此，这个隐状态向量就构成了“瓶颈”。

以翻译为例，Attention 方法让基于 RNN 的解码器在解码一个单词时，能直接去 Query 编码器对输入各个单词的隐状态，避免了上面说的”瓶颈“。此时，解码器在解码一个单词时，各个单词编码获得的隐状态的贡献很可能“不均匀”，比如一个要被翻译出来的英文单词，可能主要取决于一个中文单词。因此，Attention 给每个编码单词一个权重，以反映这种不均匀的“注意力”特性。

Attention 的实现包括两步：第一步是用各个单词的编码状态 ht 和解码状态 sl，进行计算，得到“对齐分”（Alignment score），然后做 Softmax，得到各个单词的 Attention；第二步就是用这个 Attention 对编码状态 ht 进行加权，得到 Context 向量 a。

Attention 的利用方法有两处。第一处是更新 RNN 解码器：将 Context 向量 a、解码状态 s、输入单词 x 送入解码神经元，得到新的解码状态 s，送进下一层 RNN；第二处是输出：基于 a 和 s，得到输出 y。

## Self Attention

我们注意到，上面我们还是要去更新基于 RNN 的解码器的状态。但我们前面也提过，RNN 因为是循环更新的，实现起来并不容易。因此，人们就想，能不能不用 RNN 了。事实上，有了 Attention 之后，解码器在解码一个单词时，就直接去 Query 编码器对输入各个单词的隐状态，然后输出好了，为什么还需要 RNN 呢？

这就是 Self-Attention。Self Attention 同样会计算 Attention。但是这个 Attention 是单词之间的 Attention，所以叫 Self Attention。具体的 Attent 模型，请学习文后的课程材料。在计算各个单词的编码状态时，我们采用共享的权重（w）：h = sigmoid(w*x+b)。

我们然后可以通过堆叠多层 Self Attention，获得更强大的模型。

## 课本

- Dive in Deep Learning，[11. Attention Mechanisms and Transformers](https://d2l.ai/chapter_attention-mechanisms-and-transformers/index.html)

## 课程材料

- 伯克利大学 Seq2Seq PPT，Transformer PPT

<br/>

|[Index](./) | [Previous](5-3-rnn) | [Next] (5-7-transformer)
