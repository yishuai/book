---
layout: post
title: Agent 开发
---

智能代理能够为我们完成任务，比 Prompt 工程又进一步。

智能代理是最近的研究热点。Ng 老师 2023 年 12 月 21 日，NeurIPS 开会回来，说：autonomous agents 能够自动决定一个复杂的动作序列，最近已经足够好，可以完成很多应用，所以这是他最近在[研究](https://www.deeplearning.ai/the-batch/issue-228/)的。他说：当我有时间深入思考、形成自己的结论，甚至可能长期持有不受欢迎的观点并努力证明它时，我发现技术工作更有成就感。

大语言模型是 Agent 模型吗？有的研究者认为是。比如论文《Language Models as Agent Models》 [Andreas, 2022，论文](https://aclanthology.org/2022.findings-emnlp.423.pdf)。它发现 LLM 有各种关于世界的知识，并且能够模型“人”的 belief 和动作。比如，对于一个物理现象，如果我们告诉他，Pat, who is a physicist, predicts that 的话，它会接着写专业内容、符合物理学家特点的文字；而如果我们告诉他，Pat, who has never seen this demonstration before, predicts that 的话，它可能就会接着写通俗、符合大众特点的文字。

## 智能助手

Gemini 内置了 Agent 的推理、计划和执行功能，会根据用户需求，首先分类，决定回复的方式；然后澄清模糊的地方；然后设计产品定义；最后完成产品 [Youtube 视频](https://www.youtube.com/watch?v=v5tRc_5-8G4)。

## 编程 Agent

[GPT Pilot](https://github.com/Pythagora-io/gpt-pilot) 旨在用 ChatGPT 为应用程序编写大部分代码（也许 95%），目前 Github 有18.7k Stars，值得关注。

OpenAI 的 Code Interpreter 的开源实现 [Open Interpreter](https://github.com/KillianLucas/open-interpreter) 可以在我们的电脑上和我们对话，然后用 LLM 生成代码（Python、Javascript、Shell 等），然后运行，因此执行我们想要完成的工作。比如这个[示例](https://colab.research.google.com/drive/1WKmRXZgsErej2xUriKzxrEAXdxMSgWbb?usp=sharing)，能够自动下载 Youtube 视频，完成编辑，实在是太可怕了。

## Agent 编程框架

[AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) 是开源软件。它把用户自然语言交代的任务分解为子任务，然后启动新的 Agent 来完成这些任务，比如：创建网站、创建自媒体内容、翻译。它的 Github 里提供一个 4 步教程，教我们怎么从一个示例的模版，建立 Agent。

第一步，[综述](https://github.com/Significant-Gravitas/AutoGPT/blob/master/autogpts/forge/tutorials/001_getting_started.md)，基于模版，创建和运行 Agent。此时，Agent 的内容是空的。

第二步，[蓝图](https://github.com/Significant-Gravitas/AutoGPT/blob/master/autogpts/forge/tutorials/002_blueprint_of_an_agent.md)，介绍实现一个 Agent，需要的 Profile、Memory、Planning、Action 四步。

第三步，[逻辑](https://github.com/Significant-Gravitas/AutoGPT/blob/master/autogpts/forge/tutorials/003_crafting_agent_logic.md)，介绍 Task 的概念，了解它的生命周期；然后介绍针对 Agent 的 Prompt 设计，包括：约束、资源、能力、最佳方法；最后介绍怎么创建、运行各种“能力”的 Agent，并与它们交互。

第四步，[记忆](https://github.com/Significant-Gravitas/AutoGPT/blob/master/autogpts/forge/tutorials/004_memories.md)，介绍怎么给 Agent 记忆和学习的能力。这是目前的研究热点。

AgentGPT 类似 AutoGPT。不同之处是：我们可以下载 AutoGPT，在自己的电脑上运行；而 AgentGPT 是基于浏览器的，在他们的服务器上运行。

[BabyAGI](https://github.com/yoheinakajima/babyagi) 是一个Python 脚本，包括三个 Agents：任务执行、创建、优先级排序。工作原理是：用 GPT-4 做上面三个事，然后 Pincone 存储和检索任务相关数据；LangChain 包括更多数据和更高效决策。也可以调用本地的 Llama 模型。

SuperAGI 是开源软件，能够很方便地查看 Agent 的 Actions。

MicroGPT 是一个预训练的 LLM，82M 参数，可以分析股票、网络安全测试、订披萨等等。

参考：

- Tim Keary, Top 5 Autonomous AI Agents You Need to Know About in 2023, 30 October, 2023, [Webpage](https://www.techopedia.com/top-5-autonomous-ai-agents)

## Agent 网络

微软的 [Autogen](https://github.com/microsoft/autogen)，能够让很多不同功能的 LLM Agent 合作，完成项目。比如，在这个[合作求解数学题的例子](https://microsoft.github.io/autogen/blog/2023/06/28/MathChat)中，用一个 User Proxy Agent 和一个 LLM Assitant 配合。其中，User Proxy Agent 会尝试各种 Prompt 策略，如 CoT、tool-using，比如用 Python 程序求解，而 LLM Assitant 接受这些 Prompt，完成工作。这其实是术业有专工的分工的概念，挺对的。注意 Autogen 还支持[多模](https://microsoft.github.io/autogen/blog/2023/11/06/LMM-Agent)、本地 LLM、[GPT Assistant](https://microsoft.github.io/autogen/blog/2023/11/13/OAI-assistants)，这个 Agent 还是[可教的](https://microsoft.github.io/autogen/blog/2023/10/26/TeachableAgent)，很有意思。

这给我们的启发是：在运维中，应该有很多专门的 Agent，他们合作，解决问题。我们拟开发这样一个系统。

[ChatDev](https://github.com/OpenBMB/ChatDev) 就是一个类似的系统。它设置了 CEO、

## 课程

- 斯坦福 DeepLearning.AI Short Course，[Functions, Tools and Agents with LangChain](https://learn.deeplearning.ai/functions-tools-agents-langchain)

<br/>

| [Index](./) | [Previous](3-20-rag-app-dev) | [Next](5-3-agent-app)
