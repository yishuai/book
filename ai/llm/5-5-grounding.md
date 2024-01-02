---
layout: post
title: Grounding
---

Agent 需要感知周围的环境，执行相应的动作。这常常被称为 Grounding，或者 Embodied Action，就是在一个真实的场景中，比如 3D 动画世界、对话系统中，采取各种“得体的”动作。

## 课程材料

- 华盛顿大学 CSE 599 同学 Slides

- 约翰霍普金斯 UA 2023 Talk, Rogerio Bonatti，Foundational Models for Robotics: Removing the Engineer from the Loop，April 27, 2023

- 约翰霍普金斯 UA 2023 Talk, Ruiqi Zhong, Getting AI to Do Things I Can’t: Scalable Oversight via Indirect Supervision

- 约翰霍普金斯 UA 2024 Lec 14 Connecting language to outside world
    - LMs and tools
    - Language models and robots

### 华盛顿大学课程论文

10: Beyond language understanding: multi-modality and embodiment?

How will the understanding of language benefit multi-modal applications and embodied agents?

1. [Language Models as Zero-Shot Planners: Extracting Actionable Knowledge for Embodied Agents (2022)](https://wenlong.page/language-planner/)
1. [Inner Monologue: Embodied Reasoning through Planning with Language Models (Google, 2022)](https://innermonologue.github.io)
1. [The Scope and Limits of Simulation in Cognitive Models (Ernest Davis, Gary Marcus, 2015)](https://arxiv.org/abs/1506.04956)
1. [Do As I Can, Not As I Say: Grounding Language in Robotic Affordances (Ahn et al., 2022)](https://arxiv.org/abs/2204.01691)

### 约翰霍普金斯论文

Acting in Grounded Environments:
- Do as I can, not as I say: grounded language in robotic affordances
- Language Models as Zero-Shot Planners: Extracting Actionable Knowledge for Embodied Agents
- PIGLeT: Language Grounding Through Neuro-Symbolic Interaction in a 3D World
- Experience Grounds Language

### 复旦大学推荐论文

下面是复旦大学 LLM Agent 综述论文中提到的[相关论文](https://github.com/woooodyy/llm-agent-paper-list#13-action-expand-action-space-of-llm-based-agents)。

得体的动作（Embodied Action）

- [2023/11] An Embodied Generalist Agent in 3D World. Jiangyong Huang (BIGAI & Peking University) et al. arXiv. [paper] [project page]
- [2023/11] JARVIS-1: Open-world Multi-task Agents with Memory-Augmented Multimodal Language Models. ZiHao Wang (Peking University) et al. arXiv. [paper] [code]
- [2023/10] Lemur: Harmonizing Natural Language and Code for Language Agents Yiheng Xu (University of Hong Kong) et al. arXiv. [paper] [code]
- [2023/10] Towards End-to-End Embodied Decision Making via Multi-modal Large Language Model: Explorations with GPT4-Vision and Beyond Liang Chen et al. arXiv. [paper] [code]
- [2023/07] Interactive language: Talking to robots in real time. Corey Lynch et al. IEEE (RAL) [paper]
- [2023/05] Voyager: An Open-Ended Embodied Agent with Large Language Models. Guanzhi Wang (NVIDIA) et al. arXiv. [paper] [project page] [code]
- [2023/05] AVLEN: Audio-Visual-Language Embodied Navigation in 3D Environments. Sudipta Paul et al. NeurIPS. [paper]
- [2023/05] EmbodiedGPT: Vision-Language Pre-Training via Embodied Chain of Thought. Yao Mu et al. Arxiv [paper] [code]
- [2023/05] NavGPT: Explicit Reasoning in Vision-and-Language Navigation with Large Language Models. Gengze Zhou et al. Arxiv [paper]
- [2023/05] AlphaBlock: Embodied Finetuning for Vision-Language Reasoning in Robot Manipulation. Chuhao Jin et al. Arxiv [paper]
- [2023/03] PaLM-E: An Embodied Multimodal Language Model. Danny Driess et al. Arxiv. [paper]
- [2023/03] Reflexion: Language Agents with Verbal Reinforcement Learning. Noah Shinn et al. Arxiv [paper] [code]
- [2023/02] Collaborating with language models for embodied reasoning. Ishita Dasgupta et al. Arxiv. [paper]
- [2023/02] Code as Policies: Language Model Programs for Embodied Control. Jacky Liang et al. IEEE (ICRA). [paper]
- [2022/10] ReAct: Synergizing Reasoning and Acting in Language Models. Shunyu Yao et al. Arxiv [paper] [code]
- [2022/10] Instruction-Following Agents with Multimodal Transformer. Hao Liu et al. CVPR [paper] [code]
- [2022/07] Inner Monologue: Embodied Reasoning through Planning with Language Models. Wenlong Huang et al. Arxiv. [paper]
- [2022/07] LM-Nav: Robotic Navigation with Large Pre-Trained Models of Language, Vision, and Action. Dhruv Shahet al. CoRL [paper] [code]
- [2022/04] Do As I Can, Not As I Say: Grounding Language in Robotic Affordances. Michael Ahn et al. Arxiv. [paper]
- [2022/01] A Survey of Embodied AI: From Simulators to Research Tasks. Jiafei Duan et al. IEEE (TETCI). [paper]
- [2022/01] Language Models as Zero-Shot Planners: Extracting Actionable Knowledge for Embodied Agents. Wenlong Huang et al. Arxiv. [paper] [code]
- [2020/04] Experience Grounds Language. Yonatan Bisk et al. EMNLP [paper]
- [2019/03] Review of Deep Reinforcement Learning for Robot Manipulation. Hai Nguyen et al. IEEE (IRC). [paper]
- [2005/01] The Development of Embodied Cognition: Six Lessons from Babies. Linda Smith et al. Artificial Life. [paper]

<br/>

| [Index](./) | [Previous](5-3-agent-app) | [Next](5-7-tool-usage)
