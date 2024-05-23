---
layout: post
title: 参数有效的微调
---

大语言模型的模型很大，除了在预训练好的模型上 Fine Tuning 模型的参数，我们还可以再简化一点：保持预训练好的模型不变，只是在模型的外层，再训练一个“适配器”，这就是所谓的“参数有效的微调”（PEFT：Parameter Efficient Fine-Tuning）。

PEFT 有很多方法，如 Prompt Tunning、Prefix Tunning、Adapters、LoRA、T-Few（IA3）。详见 Yandex PEFT PPT。

## 练习

- Yandex 2023 PEFT [ipynb 练习](https://github.com/yandexdataschool/nlp_course/blob/2023/week07_peft/practice.ipynb)

- Yandex 2022 LLM [ipynb 练习](https://github.com/yandexdataschool/nlp_course/blob/2022/week08_llm/practice.ipynb)，OPT LoRA，第 2 部分，同学答案 [PDF](./fig/lora-sol.pdf)

- 本地数据微调 LLM [教程](https://blog.oxen.ai/how-to-run-llama-2-on-cpu-after-fine-tuning-with-lora/) ：使用 LoRA 微调 Llama-2，将其导出到 ggml，并在 CPU 上运行。

- [Efficient Large Language Model training with LoRA and Hugging Face](https://www.philschmid.de/fine-tune-flan-t5-peft)

- Efficiently fine-tune Llama 3 with PyTorch FSDP and Q-Lora，4/22/2024, 英伟达（NVIDIA）H100 和英伟达（NVIDIA）A10G GPU 上创建和验证。配置文件和代码针对 4xA10G GPU 进行了优化，每个 GPU 均配备 24GB 内存，[英文原文](https://www.philschmid.de/fsdp-qlora-llama3?continueFlag=7e3b3f9059405e4318552e99bd128514)，[中文翻译](https://mp.weixin.qq.com/s/PR4fCky5a6geBdCbxsOURg)

## 课程材料

- 斯坦福 CS324 2022 年 [Adaptation](https://stanford-cs324.github.io/winter2022/lectures/adaptation/)

- Yandex 2023 PEFT [PPT](https://github.com/yandexdataschool/nlp_course/blob/2023/week07_peft/lecture_llm_tricks.pdf)，2022 LLM [PPT](https://drive.google.com/file/d/1IOx71suOn8uF_AbNrPhQxjnNNA5UGQY1/view?usp=share_link)

- EMNLP tutorial on PEFT by Jonas Pfeifer，[3.5 小时版](https://www.youtube.com/watch?v=KoOlcX3XLd4)，[短版](https://www.youtube.com/watch?v=StdrAJZsmw4)

- 约翰霍普金斯 UA 2024 Lec 12 Adaptation via tuning
  - head-tuning
  - prompt-tuning
  - adaptors
  - LoRA

## 软件

- 软件 [HF PEFT](https://github.com/huggingface/peft)：Parameter Efficient Fine-Tuning，有两种精调的方法，包括：LoRA、Prefix Tuning

- [Axolotl](https://github.com/OpenAccess-AI-Collective/axolotl) (Wing Lian): framework for fine-tuning LLMs，
    - Works with single GPU or multiple GPUs via FSDP or Deepspeed
    - Train various Huggingface models such as llama, pythia, falcon, mpt
    - Supports fullfinetune, lora, qlora, relora, and gptq

## 论文

约翰霍普金斯推荐论文

Suggested Reading: 
- The Power of Scale for Parameter-Efficient Prompt Tuning

Additional Reading:
- Prefix-Tuning: Optimizing Continuous Prompts for Generation
- Prompt Waywardness: The Curious Case of Discretized Interpretation of Continuous Prompts
- SPoT: Better Frozen Model Adaptation through Soft Prompt Transfer

普林斯顿大学课程论文

- Prompting as parameter-efficient fine-tuning
  - [Prefix-Tuning: Optimizing Continuous Prompts for Generation](https://arxiv.org/pdf/2101.00190.pdf)
  - [The Power of Scale for Parameter-Efficient Prompt Tuning](https://arxiv.org/pdf/2104.08691.pdf)

- Refer
  - [Factual Probing Is [MASK]: Learning vs. Learning to Recall](https://arxiv.org/pdf/2104.05240.pdf)
  - [P-Tuning v2: Prompt Tuning Can Be Comparable to Fine-tuning Universally Across Scales and Tasks](https://arxiv.org/pdf/2110.07602.pdf)， [V1](https://arxiv.org/pdf/2103.10385.pdf)
  - [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/pdf/2106.09685.pdf)， [B 站 Video](https://www.bilibili.com/video/BV1fs4y1C7vD)
  - [Towards a Unified View of Parameter-Efficient Transfer Learning](https://arxiv.org/pdf/2110.04366.pdf)

Yandex PPT 提到的论文

- Adapter
    - [Parameter-Efficient Transfer Learning for NLP](https://arxiv.org/abs/1902.00751)
    - [Adapting BigScience Multilingual Model to Unseen Languages](https://arxiv.org/abs/2204.04873)，发现 Adapters can do language adaptation

- Prompt Tuning （2022）
    - [Guiding Frozen Language Models with Learned Soft Prompts](https://blog.research.google/2022/02/guiding-frozen-language-models-with.html)
	- The Power of Scale for Parameter-Efficient Prompt Tuning，[论文](https://aclanthology.org/2021.emnlp-main.243.pdf)，[代码](https://github.com/google-research/prompt-tuning)，代码基于 JAX T5X，很容易看懂，跑起来，用 20 K 参数可以指导 11B 参数的模型的行为

- T-Few (IA3)
	- [Few-Shot Parameter-Efficient Fine-Tuning is Better and Cheaper than In-Context Learning](https://arxiv.org/abs/2205.05638)

- AdaLoRA
    - [Adaptive Budget Allocation for Parameter-Efficient Fine-Tuning](https://arxiv.org/abs/2303.10512)

- MultiTask Prompt Tuning
    - [Multitask Prompt Tuning Enables Parameter-Efficient Transfer Learning](https://arxiv.org/abs/2303.02861)

<br/>

| [Index](./) | [Previous](2-9-scaling) | [Next](2-19-codellm)
