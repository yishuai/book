---
layout: post
title: 本地模型运行
---
我们首先学习如何本地运行模型。在本地运行后，我们就可以调本地的 LM 的 API，进行系统的开发测试。

## 代码及命令行方式运行

最简单的办法，是下载 llamafile（[Github](https://github.com/Mozilla-Ocho/llamafile)），然后在命令行里运行就好。这是 Mozilla 的一个项目，目前支持 LLaVA 图像转文字、Mistral、WizardCoder、Rocket、Phi。

最基本的本地运行模型的方法是：在 HuggingFace 上下载 ggml 文件，然后本地用 C 语言编程，来运行。下面是 Andrej Karpathy 在他的 LLM 视频中介绍的方法。

如果是开发，我们可以使用 [Llama.cpp](https://github.com/ggerganov/llama.cpp)。它现在非常流行，开发社区非常好。虽然名字是 Llama，但它现在已经能运行很多的模型，并且有 Python 等接口，这样我们就可以用 Python 程序来和本地运行的模型交互。因为本机的资源有限，所以，它采用了 4-bit 整数量化，并针对 MacBook CPU 进行了优化。

如 Llama.cpp 的网页上所述，运行它的方式是“命令行”，我们输入命令，带上参数，以及我们的 Prompt，比如：make -j && ./main -m models/llama-13b-v2/ggml-model-q4_0.gguf -p "Building a website can be done in 10 simple steps:\nStep 1:" -n 400 -e，它就会输出结果。

如果是学习，我们可以从 [Karpathy 示例代码](https://github.com/karpathy/llama2.c/blob/master/run.c) 开始。这个代码是运行代码，但实际上 Karpathy 在这个仓库下，包括了完整的训练模型。具体来说，他重写了他原来写的实现 GPT-2 结构的 nanoGPT，实现了 Llama-2 的模型结构，然后用这个模型，在 TinyStories 数据集上进行了训练，得到了一个很小的 Llama-2 模型，才 15M。他也写了本地运行大模型的代码，能只需要大约 500 行 C 代码。这个代码会运行我们下载的 LLM 模型文件，接受我们的 Prompt，然后输出。

运行它的方式也是“命令行”，比如：./run stories42M.bin -t 0.8 -n 256 -i "One day, Lily met a Shoggoth"

Facebook 的 FairSeqv2 也提供了简单的编程接口，比如这个[调用 Mistral 8B 的例子](https://github.com/facebookresearch/fairseq2/tree/main/recipes/mistral)

### 图形界面运行

用命令行方式运行模型的方法并不直观，因此，人们提供了各种图形界面。

我们尝试了 [LM Studio](https://lmstudio.ai/) 。它提供了一个图形界面。在这个界面上，我们可以加载下载好的大语言模型，然后在它提供的对话界面中，和模型对话。它还提供了兼容 OpenAI 接口的 API。因此，我们在开发自己的对话机器人的时候，就可以访问本地的 API，这样加快开发速度，降低成本。等代码调试成功后，把 API 的地址，简单换为 OpenAI 的 API 即可。

启动了 LM Studio 的本地 Server 之后，它也可以为其他应用提供服务，比如 [Open Interpreter](https://github.com/KillianLucas/open-interpreter)，可以让 LLM 运行代码（Python、Javascript、Shell 等），比如[自动下载 Youtube 视频，然后编辑](https://colab.research.google.com/drive/1WKmRXZgsErej2xUriKzxrEAXdxMSgWbb?usp=sharing)，太可怕了。

我们尝试的时候，发现因为网络原因，不能一键下载 LLM。因此，我们上手动登录 Llama 的 HF 仓库，下载其中的 gguf 文件到本地硬盘的 .cache/lm-studio/model/username/llama/ 目录下，最后运行的。这里的 [B站介绍视频](https://www.bilibili.com/video/BV1th4y1i7eg) 也可以参考。

最近很火的 [Ollama](https://github.com/jmorganca/ollama) 看起来用起来也很方便，支持各种主流的模型，各种接口齐全。

## 云部署工具

我们系统的最终部署，得用云。下面是一个云部署工具。

- [SkyPilot](https://github.com/skypilot-org/skypilot): standard framework for multicloud AI training and serving，run LLMs, AI, and Batch jobs on any cloud. Get maximum savings, highest GPU availability, and managed execution—all with a simple interface.

## 大模型

目前，各种大模型层出不穷。根据子豪他们的在阿里的[魔搭社区](https://modelscope.cn/)的探索，阿里的[通义千问](https://tongyi.aliyun.com/)，似乎效果最好。最国际上，LLaMA-2、[Falcon-180B](https://arxiv.org/abs/2306.01116)、BLOOM-176B 模型用得比较多。

下面是几个 LLM

- LLaMA 2
  - 大模型开源的杰出之作
  - [网页](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models)，[Arxiv Dive](https://blog.oxen.ai/arxiv-dives-how-llama-2-works/)，[LLaMA 论文](https://arxiv.org/abs/2302.13971)，[LLaMA 2 论文](https://arxiv.org/abs/2307.09288)
  - [B 站视频](https://space.bilibili.com/471000665/channel/collectiondetail?sid=1572777)
  - 中文 LLaMA，《Efficient and Effective Text Encoding for Chinese LLaMA and Alpaca》，[论文](https://arxiv.org/pdf/2304.08177.pdf)，[代码 1](https://github.com/ymcui/Chinese-LLaMA-Alpaca/wiki/llama.cpp%E9%87%8F%E5%8C%96%E9%83%A8%E7%BD%B2)，[代码 2](https://github.com/ymcui/Chinese-LLaMA-Alpaca-2)

- ChatGLM2，[HF](https://huggingface.co/THUDM/chatglm2-6b)，[Github](https://github.com/THUDM/GLM)，[CPP 实现](https://github.com/li-plus/chatglm.cpp)

- 开源 GPT-3
	- [EleutherAI](https://huggingface.co/EleutherAI): GPT-Neo (6.7B), GPT-J (6B), GPT-NeoX (20B)
	- [Facebook/Meta](https://huggingface.co/facebook): 《[OPT: Open Pre-trained Transformer Language Models](https://arxiv.org/abs/2205.01068)》，[网页](https://alpa.ai/opt)
	- [BigScience](https://huggingface.co/bigscience): 《[BLOOM: A 176B-Parameter Open-Access Multilingual Language Model](https://github.com/ymcui/Chinese-LLaMA-Alpaca-2)》，[HF 目录](https://huggingface.co/bigscience/bloom)

- 哈工大，[活字](https://github.com/HIT-SCIR/huozi)
	- 基于 BigScience Bloom 7B 参数，15B Token 模型，做了 IFT，RLHF（16.9k 标注数据）

<br/>

| [Index](./) | [Previous](2-21-multi-modal) | [Next](3-8-prompt-eng)
