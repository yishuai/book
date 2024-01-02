---
layout: post
title: 模型设计和训练
---

大语言模型需要大规模模型。本节介绍大语言模型的大规模模型的设计、训练和推理过程中的优化方法。随着大语言模型越来越大，但训练用的 GPU 硬件资源（如存储单元）是有限的，因此，人们提出了各种方法，来优化模型的存储和计算。

## 模型设计和训练

我们首先来看大语言模型基于的 Transformer 模型的设计和训练。

首先，Transformer 的模型结构有两项重要更新：SwishGLU 和 RMSNorm。最近，它也有一些改进，比如：相对位置编码，旋转表征、ALiBi 表征、Gated FFN。

其次，为了支持超过 1T 参数的模型训练，需要多 GPU 并行训练和优化存储。其中，通过采用“混合精度” 和 TensorCores ZeRO 冗余，降低对存储的需求。

然后，为了提高效率，还有各种技巧，包括：
- ZeRO Infinity —> CPU/NVMe Offloading
- 8-Bit 训练后量化
- PEFT

最后，训练 Transformer 也有很多[技巧](https://arxiv.org/abs/1804.00247)。GPT-3 的论文中也介绍了很多训练技巧。

上面的这些内容，详见斯坦福 CS224U 的 PPT 和 Yandex 课程的 PEFT PPT。

## 模型理解

人们探索了如何理解训练获得的语言模型。

首先，可以观察学习到的 Attention。如 Anthropic 2022 年 3 月发表的 [In-context Learning and Induction Heads](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html) 指出，“Induction heads” 是大多数 In-Context Learning 的内在机制。

其次，研究者在 GPT-2 中找到了一个用于自然语言任务的大电路，并对我们的人类可理解的解释进行了定量评估。这个电路由 26 个 Attention Head 组成，包括 Previous Token Head, Induction Head, Duplicate Token Heads，很有意思。《Interpretability in the Wild: a Circuit for Indirect Object Identification in GPT-2 Small》，2022。

最后，有研究者发现，Transformer 里的 FFN 层起到了 Key-Value 存储的效果《Transformer FFN Layers are Key-Values Memory》, EMNLP 2021。

## 课程材料

- 约翰霍普金斯 GA, Colin Raffel, Building Better Language Models, PPT

- 斯坦福 CS324 2022 年 [Modeling](https://stanford-cs324.github.io/winter2022/lectures/modeling/), [Training](https://stanford-cs324.github.io/winter2022/lectures/training/), [Parallelism](https://stanford-cs324.github.io/winter2022/lectures/parallelism/)

- 斯坦福 CS 224U: Natural Language Understanding 的讲座《[Fantastic Language Models and How to Build Them](https://web.stanford.edu/class/cs224u/slides/sidd-fantastic-lms-cs224u.pdf)》，Siddharth Karamcheti

- Yandex 2023 LLM [PPT](https://drive.google.com/file/d/1IOx71suOn8uF_AbNrPhQxjnNNA5UGQY1/view?usp=share_link)

- 华盛顿大学 CSE 599 同学 Slides

- 约翰霍普金斯 UA 2024 Lec 21 Model efficiency,
    - Quantization,
    - Distillation,
    - Efficient forms of self-attention,
    - Dealing with hallucination,

- 约翰霍普金斯 UA 2023 Talk, Decentralized Deep Learning: Running Large Neural Networks Together

## 软件

- 开源训练框架 DeepSpeed，《DeepSpeed: Extreme-scale model training for everyone》，[介绍](https://www.microsoft.com/en-us/research/blog/deepspeed-extreme-scale-model-training-for-everyone/)，[Github](https://github.com/microsoft/DeepSpeed)

## 论文

普林斯顿大学课程材料

Systems
- [LLM.int8(): 8-bit Matrix Multiplication for Transformers at Scale](https://arxiv.org/pdf/2208.07339.pdf)

Refer:
- [Megatron-LM: Training Multi-Billion Parameter Language Models Using Model Parallelism](https://arxiv.org/pdf/1909.08053.pdf)
- [Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM](https://arxiv.org/pdf/2104.04473.pdf)

Sparse models
- [Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity](https://jmlr.org/papers/volume23/21-0998/21-0998.pdf)

Refer:
- [Efficient Large Scale Language Modeling with Mixtures of Experts](https://arxiv.org/pdf/2112.10684.pdf)
- [Branch-Train-Merge: Embarrassingly Parallel Training of Expert Language Models](https://arxiv.org/pdf/2208.03306.pdf)
- [A Review of Sparse Expert Models in Deep Learning](https://arxiv.org/pdf/2209.01667.pdf)

约翰霍普金斯大学

模型 Generalism
- A Generalist Agent
- UnifiedQA: Crossing Format Boundaries With a Single QA System
- Perceiver IO: A General Architecture for Structured Inputs & Outputs
- Benchmarking Generalization via In-Context Instructions on 1,600+ Language Tasks
- Multitask Prompted Training Enables Zero-Shot Task Generalization
- Finetuned Language Models Are Zero-Shot Learners
- BC-Z: Zero-Shot Task Generalization with Robotic Imitation Learning

Diagnosis:
- Do Prompt-Based Models Really Understand the Meaning of Their Prompts?
- How transferable are features in deep neural networks?
- Frequency Effects on Syntactic Rule Learning in Transformers
- Are Multimodal Transformers Robust to Missing Modality?
- Capturing Failures of Large Language Models via Human Cognitive Biases

Model
- What Language Model Architecture and Pretraining Objective Work Best for Zero-Shot Generalization?

Additional Reading(s):
- GPT-NeoX-20B: An Open-Source Autoregressive Language Model, [Webpage](https://arxiv.org/abs/2204.06745)
- Unifying Language Learning Paradigms
- Do transformer modifications transfer across implementations and applications?
- Staged Training for Transformer Language Models

## 参考

- "Building ML models like we build open-source software" by Colin Raffel - https://www.youtube.com/watch?v=0oGxT_i7nk8
- Rotary position embeddings explanation from EleutherAI - https://blog.eleuther.ai/rotary-embeddings/
- Group query attention to reduce the memory usage for inference - https://arxiv.org/abs/2305.13245v2
- Gated activations improve transformer (apparently due to divine benevolence) - https://arxiv.org/abs/2002.05202

### 深度学习模型的实现

深度学习模型层出不穷。要跟上最新的趋势，最好的办法，可能是看 Lucidrains 的 [Github 仓库](https://github.com/lucidrains)。这个人特别神。他专门实现各种流行的、影响力很大的 AI 模型。从他实现什么模型，就能看出现在最流行什么模型。真的是精力旺盛。

## HF Transformer 模型参数

[代码](https://github.com/huggingface/transformers/blob/v4.12.5/src/transformers/training_args.py)

- --max_steps: Total number of training steps to run.
- --learning_rate: Highest learning rate in the learning rate schedule (by default, the learning rate schedule increases and decreases linearly, with the peak being this set learning rate)
- --warmup_steps: Number of steps to do a linear “warmup” from a small learning rate to the desired learning rate
- --save_steps: how many steps of training before saving (and evaluating on the val set)
- --per_device_train_batch_size: batch size per GPU. The total batch size is [number of GPUs] * per_device_train_batch_size
- --gradient_accumulation_steps: Allows for accumulating gradients across multiple sequential steps. This allows you to increase the batch size while trading off computation time. If this parameter is > 1, then the total batch size is [num GPUs] * per_device_train_batch_size * gradient_accumulation_steps
- --lr_scheduler_type: learning rate scheduler. The default is “linear” which does a linear increase and decrease to and from the learning_rate.
- --adafactor: use this flag if you want to use the Adafactor optimizer instead of AdamW (default). Adafactor can save on GPU memory by only saving 2 copies of the model instead of 3 needed for AdamW (mean, variance, gradient).

<br/>

| [Index](./) | [Previous](1-13-rlhf) | [Next](2-7-data)
