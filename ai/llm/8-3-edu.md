---
layout: post
title: 大语言模型在教育中的应用
---

## Demo

谷歌的 Gemini 模型可以读入手写的数学和物理习题，检查其中的公式哪些对，哪些错，错在哪里，并且给出一步一步的推导过程；可以让它提供进一步的解释，它就可以提供关于一个话题的个性化解释；还可以要它提供进一步的练习题，它就提供个性化的练习题 [Youtube 视频](https://www.youtube.com/watch?v=K4pX1VAxaAI)。

Exploring artificial intelligence with StoryQ, [Website](https://concord.org/our-work/research-projects/storyq/), why Artificial Intelligence Belongs in English Class.

## 教育 AI 系统设计

要设计一个好的教育 AI 程序，需要了解一些基本的教育理论和方法，评估一些现有的 AI 教育应用，找到自己项目要解决的问题，并进行设计。

为此，我们下面学习 [MIT 6.S062/MAS.S10/MAS.s60 Generative Artificial Intelligence in K12 Education](https://mit-cml.github.io/gen-ai-fall-2023.github.io/) 课程。该课程会带我们走过上述过程，最后利用 ChatGPT、DALL-E 等生成式 AI 工具，开发一个面向 K12 学生的教育软件，并发表一篇论文。

该课程的具体内容如下：

第一课，熟悉 OpenAI API。用 OpenAI API 创建一个“猜人名”的游戏。注意，它代码里的 API 比较老了。在 Colab 里运行时，会被提示安装较低版本的 OpenAI 库。虽然如此，但这个代码还是有价值，适合入门。

第二课，介绍 ChatGPT 原理和 4 个学习理论：合作、互教、组内成员互补/多样化、高质量/适合学生需求的无处不在的反馈。然后，头脑风暴，提出项目创意。

第三课，理解生成式 AI 的 Bias、意想不到的结果，学习如何减少 Bias；学习如何分析系统的相关各方，建立 Ethical 矩阵；学习 Prompt 工程，生成图像的正/反方法。

第四课，学习联合国教科文组织 UNESCO 的面向学生 AI 能力的框架。这个框架包括 5 个方面：Mindset、Ethics、基础、技术、解决问题。每个方面包括 3 个层次：理解、应用、创造。明确 AI 教育的目的。

第五课，进行用户可用性测试，即先头脑风暴，用户的需求，然后召集志愿者，调研；最后进行测试，Think Aloud。

第六课，学习如何培训教师。了解成年人学习的特点。成年人在学习前，需要知道为什么要学；孩子会更探索、玩耍一些，也更能从结构化的设计中受益。

第七课，评估四套 AI 课程，和学校的一线教师一起讨论，用起来是否方便、内容、是否适合课堂教学。

最后是项目，我们可以看到麻省理工的同学们最后作品的视频、PPT 和论文。挺有意思的。这就是一个完整的基于 ChatGPT 的项目。

请点击上面的网页上的链接，获得各部分的材料，进行学习。

## 项目

我们下面基于学习到的教育理论和示例软件，开发自己的系统。下面是一个可能的系统，看大家是否感兴趣。

这个系统能够[培养珍贵的普通人](https://mp.weixin.qq.com/s/MuQKO5dAvdvuMlBLTTsdNg)；具体来说，为初入职场和社会的年轻人，逐渐走向自立，[提供支持](https://mp.weixin.qq.com/s/YzBJlbUwyqjdvi6eyW2Cqg)，主动、求真、双赢。

实现上来说，包括两部分：

第一部分是知识和技能，具体来说，知识包括：认识自我、职场、职业、世界；技能包括：目标管理、时间管理、计划执行、专业能力、职场关系、双赢思维、真诚沟通

第二部分是不断练习这些知识和技能，通过 5 步，不断解决现实生活中的问题：理解问题和挑战、确定目标、制定计划、落实计划、完成和复盘，最终实现自立。

## 企业开发经验分享

我们现在开发了一个小系统。那么，在 Github 这样的大公司，他们是怎么开发系统的呢？和我们上面做的其实差不多。下面是 GitHub Copilot 团队分享的他们构建 LLM 应用程序的经验。包括三步：首先定义问题，然后迭代，创造平滑的 AI 产品经验，最后优化质量、安全。我们 Build LLM 的应用，也要走这个流程：[How to build an enterprise LLM application: Lessons from GitHub Copilot](https://github.blog/2023-09-06-how-to-build-an-enterprise-llm-application-lessons-from-github-copilot/)，

## 会议

- AIED 2023 Empowering Education with LLMs - the Next-Gen Interface and Content Generation [WORKSHOP](https://ai4ed.cc/workshops/aied2023)，JUL 07, 2023

## 参考

- AI 角色扮演游戏 [AI Dungeon](https://play.aidungeon.com/)，设置场景，让学生闯关。[示例](https://play.aidungeon.com/adventure/7BggYuC3TtZ8/archer-world-arca/read)

- 第一批用AI自学的中学生：AI改变了我，Q1u，AI Adventure Tour，2024-01-23，[微信公众号](https://mp.weixin.qq.com/s/wQFNwv2aV2cnJTobze7FYw)

- 张峥，中国为何始终缺乏原始创新？面向未来的专业通识教育， 知识分子 2024-01-02，[微信公众号](https://mp.weixin.qq.com/s/wy2vufnqLOdB4vk0DUUMHg)


## 系统

- CS50's adaptation of ChatGPT for students and teachers, [Website](https://cs50.ai/), 针对 CS50 的学生对话系统，不会帮学生写代码，但能回答问题。
- 
<br/>

| [Index](./) | [Previous](8-1-aiops) | [Next](10-discussion)
