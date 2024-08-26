---
layout: post
title: 工具
---

Agent 会使用各种工具，并执行各种动作。这有点像机器人。

## 论文

### Ng 老师推荐论文

- “Gorilla: Large Language Model Connected with Massive APIs,” Patil et al. (2023)
- “MM-REACT: Prompting ChatGPT for Multimodal Reasoning and Action,” Yang et al. (2023)
- “Efficient Tool Use with Chain-of-Abstraction Reasoning,” Gao et al. (2024)   

### Andrej Karpathy 推荐论文

LLM 本身并不擅长执行我们已经为其编写了软件（如计算器）的任务。一个数字跟在另一个数字后面的概率很高并不意味着它是正确的数字。因此，我们需要LLM能够在执行过程中调用外部工具。以下是一些探讨LLM工具用法的论文

- Toolformer: Language Models Can Teach Themselves to Use Tools，[论文链接](https://arxiv.org/abs/2302.04761)
    - 这论文展示了LLM如何使用工具来增强他们在简单预测下一个单词效果不佳的领域的能力

- Large Language Models as Tool Makers，[论文链接](https://arxiv.org/abs/2305.17126)
    - Google Deepmind等单位作者不仅展示了LLM如何使用工具，还展示了他们如何首先创建工具。

- ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs，[论文链接](https://arxiv.org/abs/2307.16789)
    - 训练了一个ToolLlama，可以使大语言模型掌握16000多个真实世界的 API，从而执行复杂的指令

### 复旦大学推荐论文

下面是复旦大学 LLM Agent 综述论文中提到的[相关论文](https://github.com/woooodyy/llm-agent-paper-list#13-action-expand-action-space-of-llm-based-agents)。

Tool Using

- [2023/10] OpenAgents: An Open Platform for Language Agents in the Wild. XLang Lab (The University of Hong Kong) arXiv. [paper] [project page] [code] [demo]
- [2023/10] Lemur: Harmonizing Natural Language and Code for Language Agents Yiheng Xu (University of Hong Kong) et al. arXiv. [paper] [code]
- [2023/10] Towards End-to-End Embodied Decision Making via Multi-modal Large Language Model: Explorations with GPT4-Vision and Beyond Liang Chen (Peking University) et al. arXiv. [paper] [code]
    - HOLMES is a multi-agent cooperation framework that allows LLMs to leverage MLLMs and APIs to gather multimodal information for informed decision-making.
- [2023/07] ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs. Yujia Qin (Tsinghua University) et al. arXiv. [paper] [code] [dataset]
    - ToolLLM is a general tool-use framework encompassing data construction, model training and evaluation.
- [2023/05] Large Language Models as Tool Makers. Tianle Cai (Princeton University) et al. arXiv. [paper] [code]
    - LATM is a closed-loop framework that takes an initial step towards removing the dependency on the availability of existing tools.
- [2023/05] CREATOR: Disentangling Abstract and Concrete Reasonings of Large Language Models through Tool Creation. Cheng Qian (Tsinghua University) et al. arXiv. [paper]
    - CREATOR is a novel framework that empowers LLMs to create their own tools through documentation and code realization.
- [2023/04] Tool Learning with Foundation Models. Yujia Qin (Tsinghua University) et al. arXiv. [paper] [code]
    - This survey primarily introduces a new paradigm called "tool learning based on foundational models", which combines the advantages of specialized tools and foundational models, achieving higher precision, efficiency, and automation in problem-solving.
- [2023/04] ChemCrow: Augmenting large-language models with chemistry tools. Andres M Bran (Laboratory of Artificial Chemical Intelligence, ISIC, EPFL) et al. arXiv. [paper] [code]
    - ChemCrow is an LLM chemistry agent that integrates 13 expert-designed tools and augments the LLM performance in chemistry and emerge new capabilities.
- [2023/04] GeneGPT: Augmenting Large Language Models with Domain Tools for Improved Access to Biomedical Information. Qiao Jin (National Institutes of Health), Yifan Yang, Qingyu Chen, Zhiyong Lu. arXiv. [paper] [code]
    - GeneGPT is a model that answer genomics questions. It introduces a novel method for handling challenges with hallucinations by teaching LLMs to use the Web APIs.
- [2023/04] OpenAGI: When LLM Meets Domain Experts. Yingqiang Ge (Rutgers University) et al. arXiv. [paper] [code]
    - OpenAGI is an open-source AGI research platform. It introduces a paradigm of LLMs operating various expert models for complex task-solving and proposes an RLTF mechanism to improve the LLM's task-solving ability.
- [2023/03] HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face. Yongliang Shen (Zhejiang University) et al. arXiv. [paper] [code]
    - HuggingGPT is a system that leverages LLMs to connect various and multimodal AI models in machine learning communities to solve AI tasks.
- [2023/03] Visual ChatGPT: Talking, Drawing and Editing with Visual Foundation Models. Chenfei Wu (Microsoft Research Asia) et al. arXiv. [paper] [code]
    - Visual ChatGPT is a system that opens the door to investigating the visual roles of ChatGPT with the help of Visual Foundation Models.
- [2023/02] Augmented Language Models: a Survey. Grégoire Mialon (Meta AI) et al. TMLR. [paper]
    - This survey reviews works in which LMs are augmented with the ability to use tools. Augmented LMs can use external modules to expand their context processing ability.
- [2023/02] Toolformer: Language Models Can Teach Themselves to Use Tools. Timo Schick (Meta AI) et al. arXiv. [paper]
    - Toolformer shows that LLMs can teach themselves to use external tools with a handful of demonstrations for each API.
- [2022/05] TALM: Tool Augmented Language Models. Aaron Parisi (Google) et al. arXiv. [paper]
    - TALM introduces a method that combines non-differentiable tools with LMs, enabling the model to access real-time or private data.
- [2022/05] MRKL Systems: A modular, neuro-symbolic architecture that combines large language models, external knowledge sources and discrete reasoning. Ehud Karpas (AI21 Labs) et al. arXiv. [paper]
    - MRKL Systems augments LLMs with an easily extensible set of external knowledge and reasoning modules.
- [2022/04] Do As I Can, Not As I Say: Grounding Language in Robotic Affordances. Michael Ahn (Google) et al. CoRL. [paper]
    - SayCan applies LMs in real-world robotic tasks by combining advanced semantic knowledge from LLMs with the value function of pre-trained skills.
- [2021/12] WebGPT: Browser-assisted question-answering with human feedback. Reiichiro Nakano (OpenAI) et al. arXiv. [paper]
    - WebGPT answer questions using a webbrowsing environment. It uses imitation learning during training and then optimizes answer quality through human feedback.
- [2021/07] Evaluating Large Language Models Trained on Code. Mark Chen (OpenAI) et al. arXiv. [paper] [code]
    - Codex can synthesize programs from docstrings, that is, creating tools based on documentation.

<br/>

| [Index](./) | [Previous](5-5-grounding) | [Next](5-9-agent-research)
