---
layout: post
title: 多模 LLM
---

多模 LLM 模型以语言模型为核心，融合多模数据（比如图像、视频、语音、音乐）。

我们首先看视觉 LLM。Flamingo 是这方面的开创性工作。它在 LLM 中加入了视觉。

## 课程材料

- 斯坦福 CS224n Multimodal Deep Learning, [PPT](https://web.stanford.edu/class/cs224n/slides/Multimodal-Deep-Learning-CS224n-Kiela.pdf)

- Yandex 2023 PEFT PPT

- Vision and Language: A Primer，LxMLS 2023 PPT

- 约翰霍普金斯 UA 2024 Lec 14 Connecting language to outside world
    - Vision language models,
    - Speech-text models,

## 论文

### 空间位置

- Shikra: Unleashing Multimodal LLM's Referential Dialogue Magic, 2023, 指出空间位置的自然语言输入和输出，用于 VQA 和 Image Caption

### 普林斯顿大学课程论文

- [Flamingo: a Visual Language Model for Few-Shot Learning](https://arxiv.org/pdf/2204.14198.pdf)

Refer:
- [Blog post: Generalized Visual Language Models](https://lilianweng.github.io/posts/2022-06-09-vlm/)
- [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/pdf/2103.00020.pdf)
- [Multimodal Few-Shot Learning with Frozen Language Models](https://arxiv.org/pdf/2106.13884.pdf)
- [CM3: A Causal Masked Multimodal Model of the Internet](https://arxiv.org/pdf/2201.07520.pdf)

### Andrej Karpathy 推荐论文

- An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale，[论文链接](https://arxiv.org/abs/2010.11929)
    - 与最先进的卷积网络相比，Vision Transformer (ViT) 在计算机视觉任务上取得了优异的结果，同时需要更少的计算资源来训练。这是建立在文本-图像研究（如下面的 CLIP）基础上的重要基础读物

- CLIP - Learning Transferable Visual Models From Natural Language Supervision，[论文链接](https://arxiv.org/abs/2103.00020)，
    - OpenAI 大名鼎鼎的CLIP模型，是DALL.E的重要工作基础，论文研究将不同模态（文本和图像）的数据映射到共享的嵌入空间中。这种共享的多模式嵌入空间使文本到图像和图像到文本的任务变得更加容易，论文同时是Stable Diffusion等模型的基础

- NExT-GPT: Any-to-any multimodal large language models，[项目链接](https://next-gpt.github.io/)
    - 将LLM与多模态适配器和不同的扩散解码器连接起来，使NExT-GPT能够感知输入并以文本、图像、视频和音频的任意组合生成输出

- LLaVA - Visual Instruction Tuning, [论文链接](https://arxiv.org/abs/2304.08485)
    - 在文中，作者首次尝试使用仅语言版的GPT-4来生成多模态语言图像指令遵循数据。通过对这些生成的数据进行指令调整，作者引入了LLaVA：大语言和视觉助手，这是一种端到端训练的多模态模型，连接了视觉编码器和LLM，用于通用视觉和语言理解

- LaVIN - Cheap and Quick: Efficient Vision-Language Instruction Tuning for Large Language Models，[论文链接](https://arxiv.org/abs/2305.15023)
    - 提出了一种新颖且经济实惠的用于LLM视觉语言自适应的解决方案，称为混合模态适应（MMA）

- Emu Video: Factorizing Text-to-Video Generation by Explicit Image Conditioning，[论文链接](https://arxiv.org/abs/2311.10709)
    - Meta提出最出色的文本到视频生成工作

### JHU 课程推荐论文

Pretraining Vision-Language Models
- Multimodal Few-Shot Learning with Frozen Language Models
- Learning Transferable Visual Models From Natural Language Supervision

Additional Reading:
- An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale
- Scaling Up Visual and Vision-Language Representation Learning With Noisy Text Supervision
- Hierarchical Text-Conditional Image Generation with CLIP Latents
- Emerging Properties in Self-Supervised Vision Transformers
- MERLOT: Multimodal Neural Script Knowledge Models
- LiT: Zero-Shot Transfer with Locked-image text Tuning
- CM3: A Causal Masked Multimodal Model of the Internet

Pretraining Vision-Language Models
- Hierarchical Text-Conditional Image Generation with CLIP Latents

Additional Reading(s):
- Photorealistic Text-to-Image Diffusion Models with Deep Language Understanding
- Image as a Foreign Language: BEiT Pretraining for All Vision and Vision-Language Tasks
- Discovering the Hidden Vocabulary of DALLE-2
- High-Resolution Image Synthesis with Latent Diffusion Models

Pretraining Speech/Audio Models
- wav2vec 2.0: A Framework for Self-Supervised Learning of Speech Representations

Additional Reading(s):
- Jukebox: A Generative Model for Music
- mSLAM: Massively multilingual joint pre-training for speech and text
- Towards Learning Universal Audio Representations
- AudioLM: a Language Modeling Approach to Audio Generation
- Robust Speech Recognition via Large-Scale Weak Supervision
- ESPnet: End-to-End Speech Processing Toolkit
- Unsupervised Speech Recognition
- Masked Autoencoders that Listen
- Towards End-to-end Unsupervised Speech Recognition
- SSAST: Self-Supervised Audio Spectrogram Transformer

### LLM Agent 相关多模论文

复旦大学的 LLM Agent 综述论文中提到的[LLM 视觉和音频感知能力的相关论文](https://github.com/woooodyy/llm-agent-paper-list#12-perception-multimodal-inputs-for-llm-based-agents)。

Visual
- [2023/10] Towards End-to-End Embodied Decision Making via Multi-modal Large Language Model: Explorations with GPT4-Vision and Beyond Liang Chen et al. arXiv. [paper] [code]
- [2023/05] Language Is Not All You Need: Aligning Perception with Language Models. Shaohan Huang et al. arXiv. [paper]
- [2023/05] InstructBLIP: Towards General-purpose Vision-Language Models with Instruction Tuning. Wenliang Dai et al. arXiv. [paper]
- [2023/05] MultiModal-GPT: A Vision and Language Model for Dialogue with Humans. Tao Gong et al. arXiv. [paper]
- [2023/05] PandaGPT: One Model To Instruction-Follow Them All. Yixuan Su et al. arXiv. [paper]
- [2023/04] Visual Instruction Tuning. Haotian Liu et al. arXiv. [paper]
- [2023/04] MiniGPT-4: Enhancing Vision-Language Understanding with Advanced Large Language Models. Deyao Zhu. arXiv. [paper]
- [2023/01] BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models. Junnan Li et al. arXiv. [paper]
- [2022/04] Flamingo: a Visual Language Model for Few-Shot Learning. Jean-Baptiste Alayrac et al. arXiv. [paper]
- [2021/10] MobileViT: Light-weight, General-purpose, and Mobile-friendly Vision Transformer. Sachin Mehta et al.arXiv. [paper]
- [2021/05] MLP-Mixer: An all-MLP Architecture for Vision. Ilya Tolstikhin et al.arXiv. [paper]
- [2020/10] An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale. Alexey Dosovitskiy et al. arXiv. [paper]
- [2017/11] Neural Discrete Representation Learning. Aaron van den Oord et al. arXiv. [paper]

Audio
- [2023/06] Video-LLaMA: An Instruction-tuned Audio-Visual Language Model for Video Understanding. Hang Zhang et al. arXiv. [paper]
- [2023/05] X-LLM: Bootstrapping Advanced Large Language Models by Treating Multi-Modalities as Foreign Languages. Feilong Chen et al. arXiv. [paper]
- [2023/05] InternGPT: Solving Vision-Centric Tasks by Interacting with ChatGPT Beyond Language. Zhaoyang Liu et al. arXiv. [paper]
- [2023/04] AudioGPT: Understanding and Generating Speech, Music, Sound, and Talking Head. Rongjie Huang et al. arXiv. [paper]
- [2023/03] HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face. Yongliang Shen et al. arXiv. [paper]
- [2021/06] HuBERT: Self-Supervised Speech Representation Learning by Masked Prediction of Hidden Units. Wei-Ning Hsu et al. arXiv. [paper]
- [2021/04] AST: Audio Spectrogram Transformer. Yuan Gong et al. arXiv. [paper]

## Demo

- 谷歌的 Gemini 模型可以读论文中的线图，给出画出该图的代码，收集和分析数据，然后再运行绘图代码，得到更新后的图 [Youtube 视频](https://www.youtube.com/watch?v=sPiOP_CB54A)；也可以理解音频，比如“正月”的“正”应该怎么发音 [Youtube 视频](https://www.youtube.com/watch?v=D64QD7Swr3s)。

- [DALL-E mini demo](https://huggingface.co/spaces/dalle-mini/dalle-mini)

- [AllenAI vision demo](https://vision-explorer.allenai.org)，可以跑各种视觉应用，识别，语言，场景几何的常见模型

- [DreamStudio image generation demo](https://beta.dreamstudio.ai/)

- [Examples from AudioLM](https://google-research.github.io/seanet/audiolm/examples/)

- [Stable Diffusion model weights ](https://github.com/CompVis/stable-diffusion)

- GPT-4V，课程，https://www.coursera.org/learn/gpt-vision

## 练习

- 微软 Generative AI for Beginners，[第九章：构建图像生成应用](https://github.com/microsoft/generative-ai-for-beginners/blob/main/09-building-image-applications/translations/cn/README.md?WT.mc_id=academic-105485-koreyst)

## 软件

- LLaVA (Haotian Liu): open source multimodal model (language and vision)，[Github](https://github.com/haotian-liu/LLaVA)，[Demo](https://llava-vl.github.io/llava-interactive/)，论文：[NeurIPS'23 Oral] Visual Instruction Tuning: LLaVA (Large Language-and-Vision Assistant) built towards GPT-4V level capabilities.

- LLaVA 图像转文字：最简单的办法，是下载 llamafile（[Github](https://github.com/Mozilla-Ocho/llamafile)），然后在命令行里运行就好。这是 Mozilla 的一个项目，也支持 Mistral、WizardCoder、Rocket、Phi。

- [Deforum](https://deforum.art/) (Huemin): platform and open source community for AI animation。Building upon the work of Disco Diffusion, PyTTI, and VQGAN+CLIP, Deforum began as a powerful [Colab Notebook](https://colab.research.google.com/github/deforum-art/deforum-stable-diffusion/blob/main/Deforum_Stable_Diffusion.ipynb) and quickly evolved into an extension for the Automatic WebUI

- Whisper 语音识别：我在自己的 MAC 上用 CPP 方式安装了 OpenAI 的 Whisper 语音识别大模型 [Github](https://github.com/ggerganov/whisper.cpp)，对中文进行识别，发现效果很好

- Facebook [Audiocraft](https://github.com/facebookresearch/audiocraft) 是一个通过深度学习进行音频处理和生成的库。它具有最先进的 EnCodec 音频压缩器/标记器，以及 MusicGen，这是一个简单且可控的音乐生成 LM，具有文本和旋律调节功能。

<br/>

| [Index](./) | [Previous](2-19-codellm) | [Next](3-1-run)
