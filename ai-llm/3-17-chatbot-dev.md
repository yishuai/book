---
layout: post
title: 简单接口调用与系统开发
---

基于 LLM 提供的 API，我们可以开发各种简单的 LLM 应用。

## 体验

我们首先体验一个基于 Javascript 的客户端 LLM Chatbot 应用开发。它想要解决的问题是：学生在进行 MIT 的 Scratch 编程中，需要管理项目方向、设置目标，在它的工作上进行迭代。这个和我们想要解决的问题很相似。

打开[示例网站](https://mitmedialab.github.io/sparki)后，会出来一个对话的界面。首先，它会要我们输入自己的 OpenAI API 的 Key。

验证了我们给的 API key 是有效的后，它就开始问：What is it that you would like to do? I'm here to assist you with a couple of particular tasks. 并且列出了四个任务：讨论项目、编程帮助、学习 Jibo、学习这个工具。

比如，我们可以点“讨论项目”，然后输入“我没有想法”，它会回答：那没关系！如果你愿意，我可以给你一些项目的灵感。不过在开始之前，你可以先考虑一下你的项目可能会对哪些人产生影响呢？

我们可以打开浏览器的“开发者工具”，点击“Source”页面，看到它的 Javascript 代码。我们可以在开发者工具里设置断点，来跟踪理解它的工作原理。这个代码写得非常好。值得学习。

这个网站的源代码在它的（[Github 仓库](https://github.com/mitmedialab/sparki)）中。请下载后，按照 Github 仓库上的说明，在本地安装，然后用 node.js 运行它。它的代码有一点复杂，我们下面先学更简单的代码，后面再基于这个代码进行开发。

## 入门

为了入门基于 ChatGPT API 的网站开发，我们学习 MIT 媒体实验室提供的几个例子。请下载（[Github 仓库](https://github.com/mitmedialab/genai-code-demos)）。

首先请打开其中的 Introduction to GPT 这个 Jupyter notebook，练习 OpenAI 的接口，让 GPT 写一个小故事。我们可以在 Colab 上运行它。

我们然后学习做简单的网站。请打开上面仓库中的 Color 和 Story 目录中的代码。这是两个基于 ChatGPT 的简单对话网站。它们的功能很简单，就是调一下 OpenAI API，提一个小问题，然后显示在页面上，所以很容易看懂。

它们是用 node.js 运行的。请按网页上的 Setup 说明，安装 node, expressjs 后，就可以用 node index.js 命令，在本机运行，然后打开浏览器，访问它。然后打开浏览器的“开发者工具”，在 Source 选项卡中，找到 js 代码，设置断点，单步跟踪它的原理。弄清楚网页编程的基本方法。

## 课程

- 斯坦福 DeepLearning.AI Short Course，[Building Systems with the ChatGPT API](https://learn.deeplearning.ai/chatgpt-building-system)。

- 微软 Generative AI for Beginners，[第六章：创建文本生成应用](https://github.com/microsoft/generative-ai-for-beginners/blob/main/06-text-generation-apps/translations/cn/README.md?WT.mc_id=academic-105485-koreyst)，[第七章：创建聊天应用](https://github.com/microsoft/generative-ai-for-beginners/blob/main/07-building-chat-applications/translations/cn/README.md?WT.mc_id=academic-105485-koreyst)

## 工具

- OpenAI
  - API 官方 Python 库，[Github](https://github.com/openai/openai-python)
  - [Cookbook](https://cookbook.openai.com/), [Github](https://github.com/openai/openai-cookbook)

- LiteLLM：Call 100+ LLMs using the same Input/Output Format，[Website](https://docs.litellm.ai/docs/)

- [LMSys](https://lmsys.org/) (Lianmin Zheng, Wei-Lin Chiang, and Ying Sheng) 中的 Vicuna 模型，1M 数据集，CPU 30G 内存，或者 GPU，开创了基于开源的 LLM 进行 Fine tune 的潮流。它的模型中，包括 open models, systems, and evaluation platforms including Vicuna, FastChat, and Chatbot Arena。这个 Chat 框架，似乎正在成为主流的基于 LLM 的 Chat 开发框架。可以用来训练、评估 LLM Chatbot，也支持其它各种模型。[Github](https://github.com/lm-sys/FastChat)。

- ChatGPT-Next-Web，A cross-platform ChatGPT/Gemini UI (Web / PWA / Linux / Win / MacOS). 一键拥有你自己的跨平台 ChatGPT/Gemini 应用，[Github](https://github.com/ChatGPTNextWeb/ChatGPT-Next-Web)

- Ora，输入 Prompt，创造自己的 Chatbot，[网址](https://ora.ai/)

## 其他

- IBM 系列课程：[LLM](https://cognitiveclass.ai/courses?type%5B%5D=guided_project&sort%5B%5D=featured&skills%5B%5D=LLM&skills%5B%5D=Large+Language+Model+%28LLM%29)，[Generative AI](https://cognitiveclass.ai/courses?type%5B%5D=guided_project&sort%5B%5D=featured&skills%5B%5D=Generative+AI)
  - [Enhancing Applications with Embeddable AI](https://cognitiveclass.ai/learn/integration-of-embeddable-ai)
  - [Create a Voice Assistant with OpenAI's GPT-3 and IBM Watson](https://cognitiveclass.ai/courses/course-v1:IBMSkillsNetwork+GPXX0IWWEN+v1)
  - [Prompt Enginneering for Everyone](https://cognitiveclass.ai/courses/prompt-engineering-for-everyone)
  - [Land Your Dream Job: Build Your Portfolio with GenAI](https://cognitiveclass.ai/courses/course-v1:IBMSkillsNetwork+GPXX0UVUEN+v1)
  - [Build an AI Investment Advisor with LLM & LangChain](https://cognitiveclass.ai/courses/course-v1:IBMSkillsNetwork+GPXX05EIEN+v1)
  - Create AI powered apps with open source LangChain
  - [Build a Chatbot to Analyze PDF Documents Using LLM](https://cognitiveclass.ai/courses/course-v1:IBMSkillsNetwork+GPXX0WEVEN+v1)
  - Build a Brand Sentiment Analysis Extension for Twitter
  - Improve Customer Support with AI-powered Voice Services
  - How do people feel about a product? Use AI to get the answer
  - Build a Chatbot in less than an hour with watsonx!
  - The Art of Prompt Engineering
  - Create Your Own ChatGPT-like Website with Open Source LLMs
  - Mastering Translations with Generative AI in PyTorch
  - Summarize Your Private Data with LLMs & Generative AI
  - Automate the Boring Stuff With Large Language Models
  - Natural Language Processing with Hugging Face Transformers
  - Improve Customer Support Efficiency with Open-Source LLM
  - From Chaos to Order: Automate Documents Categorization by AI
  - Unlocking Multilingual Magic: Babel Fish with LLM STT TTS
  - Build Guardrails for Your AI with Open Source
  - Give Meaningful Names To Your Photos With IMG Captioning AI
  - Build an Image Style Transfer Tool using CycleGANs
  - Creating anime characters using DCGANs and Keras
  - Creating anime characters using DCGANs and PyTorch

<br/>

| [Index](./) | [Previous](3-11-prompt-opt) | [Next](3-19-chatbot-opt)
