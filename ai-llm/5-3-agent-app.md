---
layout: post
title: Agent 应用
---

基于 LLM 的 Agent 的应用的论文，非常丰富。下面是复旦大学的 LLM Agent 综述论文中提到的[LLM Agent 应用相关参考论文](https://github.com/woooodyy/llm-agent-paper-list#2-agents-in-practice-applications-of-llm-based-agents)。大概包括以下几个方面：

首先，是单个 Agent，完成特定任务。按应用场景，包括网络应用、生活助手、科学探索（包括数学）、开放世界的各种任务；

然后，是与人交互的 Agent，包括：人下达指令，Agent 执行（教育、医疗、销售），还有人和 Agent 平等地交流。

最后，是多 Agent 联合完成任务，这包括合作、竞争；

具体论文如下：

## 综述论文

- The Rise and Potential of Large Language Model Based Agents: A Survey Zhiheng Xi (Fudan University) et al. arXiv. [论文](https://arxiv.org/abs/2309.07864)，[Github](https://github.com/woooodyy/llm-agent-paper-list)

## 单 Agent 任务完成

In web scenarios
- [2023/10] OpenAgents: An Open Platform for Language Agents in the Wild. XLang Lab (The University of Hong Kong) arXiv. [paper] [project page] [code] [demo]
- [2023/07] WebArena: A Realistic Web Environment for Building Autonomous Agents. Shuyan Zhou (CMU) et al. arXiv. [paper] [code]
- [2023/07] A Real-World WebAgent with Planning, Long Context Understanding, and Program Synthesis. Izzeddin Gur (DeepMind) et al. arXiv. [paper]
- [2023/06] SYNAPSE: Leveraging Few-Shot Exemplars for Human-Level Computer Control. Longtao Zheng (Nanyang Technological University) et al. arXiv. [paper] [code]
- [2023/06] Mind2Web: Towards a Generalist Agent for the Web. Xiang Deng (The Ohio State University) et al. arXiv. [paper] [code]
- [2023/05] Multimodal Web Navigation with Instruction-Finetuned Foundation Models. Hiroki Furuta (The University of Tokyo) et al. arXiv. [paper]
- [2023/03] Language Models can Solve Computer Tasks. Geunwoo Kim (University of California) et al. arXiv. [paper] [code]
- [2022/07] WebShop: Towards Scalable Real-World Web Interaction with Grounded Language Agents. Shunyu Yao (Princeton University) et al. arXiv. [paper] [code]
- [2021/12] WebGPT: Browser-assisted question-answering with human feedback. Reiichiro Nakano (OpenAI) et al. arXiv. [paper]
- [2023/05] Agents: An Open-source Framework for Autonomous Language Agents. Wangchunshu Zhou (AIWaves) et al. arXiv. [paper] [code]

In life scenarios
- [2023/10] OpenAgents: An Open Platform for Language Agents in the Wild. XLang Lab (The University of Hong Kong) arXiv. [paper] [project page] [code] [demo]
- [2023/08] InterAct: Exploring the Potentials of ChatGPT as a Cooperative Agent. Po-Lin Chen et al. arXiv. [paper]
- [2023/05] Plan, Eliminate, and Track -- Language Models are Good Teachers for Embodied Agents. Yue Wu (CMU) et al. arXiv. [paper]
- [2023/05] Augmenting Autotelic Agents with Large Language Models. Cédric Colas (MIT) et al. arXiv. [paper]
- [2023/03] Planning with Large Language Models via Corrective Re-prompting. Shreyas Sundara Raman (Brown University) et al. arXiv. [paper]
- [2022/10] Generating Executable Action Plans with Environmentally-Aware Language Models. Maitrey Gramopadhye (University of North Carolina at Chapel Hill) et al. arXiv. [paper] [code]
- [2022/01] Language Models as Zero-Shot Planners: Extracting Actionable Knowledge for Embodied Agents. Wenlong Huang (UC Berkeley) et al. arXiv. [paper] [code]

Innovation-oriented Deployment
- [2023/10] OpenAgents: An Open Platform for Language Agents in the Wild. XLang Lab (The University of Hong Kong) arXiv. [paper] [project page] [code] [demo]
- [2023/08] The Hitchhiker's Guide to Program Analysis: A Journey with Large Language Models. Haonan Li (UC Riverside) et al. arXiv. [paper]
- [2023/08] ChatMOF: An Autonomous AI System for Predicting and Generating Metal-Organic Frameworks. Yeonghun Kang (Korea Advanced Institute of Science and Technology) et al. arXiv. [paper]
- [2023/07] Math Agents: Computational Infrastructure, Mathematical Embedding, and Genomics. Melanie Swan (University College London) et al. arXiv. [paper]
- [2023/06] Towards Autonomous Testing Agents via Conversational Large Language Models. Robert Feldt (Chalmers University of Technology) et al. arXiv. [paper]
- [2023/04] Emergent autonomous scientific research capabilities of large language models. Daniil A. Boiko (CMU) et al. arXiv. [paper]
- [2023/04] ChemCrow: Augmenting large-language models with chemistry tools. Andres M Bran (Laboratory of Artificial Chemical Intelligence, ISIC, EPFL) et al. arXiv. [paper] [code]
- [2022/03] ScienceWorld: Is your Agent Smarter than a 5th Grader? Ruoyao Wang (University of Arizona) et al. arXiv. [paper] [code]

Lifecycle-oriented Deployment
- [2023/05] Voyager: An Open-Ended Embodied Agent with Large Language Models. Guanzhi Wang (NVIDIA) et al. arXiv. [paper] [project page] [code]
- [2023/05] Ghost in the Minecraft: Generally Capable Agents for Open-World Environments via Large Language Models with Text-based Knowledge and Memory. Xizhou Zhu (Tsinghua University) et al. arXiv. [paper] [code]
- [2023/03] Plan4MC: Skill Reinforcement Learning and Planning for Open-World Minecraft Tasks. Haoqi Yuan (PKU) et al. arXiv. [paper] [project page]
- [2023/02] Describe, Explain, Plan and Select: Interactive Planning with Large Language Models Enables Open-World Multi-Task Agents. Zihao Wang (PKU) et al. arXiv. [paper] [code]
- [2023/01] Do Embodied Agents Dream of Pixelated Sheep: Embodied Decision Making using Language Guided World Modelling. Kolby Nottingham (University of California Irvine, Irvine) et al. arXiv. [paper] [code]

## 与人交互的 Agent

Interactive Engagement between Human and Agent

Instructor-Executor Paradigm

Education
- [2023/07] Math Agents: Computational Infrastructure, Mathematical Embedding, and Genomics. Melanie Swan (UCL) et al. arXiv. [paper]
    - Communicate with humans to help them understand and use mathematics.
- [2023/03] Hey Dona! Can you help me with student course registration? Vishesh Kalvakurthi (MSU) et al. arXiv. [paper]
    - This is a developed application called Dona that offers virtual voice assistance in student course registration, where humans provide instructions.

Health
- [2023/08] Zhongjing: Enhancing the Chinese Medical Capabilities of Large Language Model through Expert Feedback and Real-world Multi-turn Dialogue. Songhua Yang (ZZU) et al. arXiv. [paper] [code]
- [2023/05] HuatuoGPT, towards Taming Language Model to Be a Doctor. Hongbo Zhang (CUHK-SZ) et al. arXiv. [paper] [code] [demo]
- [2023/05] Helping the Helper: Supporting Peer Counselors via AI-Empowered Practice and Feedback. Shang-Ling Hsu (Gatech) et al. arXiv. [paper]
- [2020/10] A Virtual Conversational Agent for Teens with Autism Spectrum Disorder: Experimental Results and Design Lessons. Mohammad Rafayet Ali (U of R) et al. IVA '20. [paper]

Other Application
- [2023/08] RecMind: Large Language Model Powered Agent For Recommendation. Yancheng Wang (ASU, Amazon) et al. arXiv. [paper]
- [2023/08] Multi-Turn Dialogue Agent as Sales' Assistant in Telemarketing. Wanting Gao (JNU) et al. IEEE. [paper]
- [2023/07] PEER: A Collaborative Language Model. Timo Schick (Meta AI) et al. arXiv. [paper]
- [2023/07] DIALGEN: Collaborative Human-LM Generated Dialogues for Improved Understanding of Human-Human Conversations. Bo-Ru Lu (UW) et al. arXiv. [paper]
- [2023/06] AssistGPT: A General Multi-modal Assistant that can Plan, Execute, Inspect, and Learn. Difei Gao (NUS) et al. arXiv. [paper]
- [2023/05] Agents: An Open-source Framework for Autonomous Language Agents. Wangchunshu Zhou (AIWaves) et al. arXiv. [paper] [code]

Equal Partnership Paradigm

Empathetic Communicator
- [2023/08] SAPIEN: Affective Virtual Agents Powered by Large Language Models. Masum Hasan et al. arXiv. [paper] [project page]
- [2023/05] Helping the Helper: Supporting Peer Counselors via AI-Empowered Practice and Feedback. Shang-Ling Hsu (Gatech) et al. arXiv. [paper]
- [2022/07] Artificial empathy in marketing interactions: Bridging the human-AI gap in affective and social customer experience. Yuping Liu‑Thompkins et al. [paper]

Human-Level Participant
- [2023/08] Quantifying the Impact of Large Language Models on Collective Opinion Dynamics. Chao Li et al. CoRR. [paper]
- [2023/06] Mastering the Game of No-Press Diplomacy via Human-Regularized Reinforcement Learning and Planning. Anton Bakhtin et al. ICLR. [paper]
- [2023/06] Decision-Oriented Dialogue for Human-AI Collaboration. Jessy Lin et al. CoRR. [paper]
- [2022/11] Human-level play in the game of Diplomacy by combining language models with strategic reasoning. FAIR et al. Science. [paper]

## 多 Agent

Coordinating Potential of Multiple Agents

Cooperative Interaction for Complementarity

Disordered cooperation
- [2023/07] Unleashing Cognitive Synergy in Large Language Models: A Task-Solving Agent through Multi-Persona Self-Collaboration. Zhenhailong Wang (University of Illinois Urbana-Champaign) et al. arXiv. [paper] [code]
- [2023/07] RoCo: Dialectic Multi-Robot Collaboration with Large Language Models. Zhao Mandi, Shreeya Jain, Shuran Song (Columbia University) et al. arXiv. [paper] [code]
- [2023/04] ChatLLM Network: More brains, More intelligence. Rui Hao (Beijing University of Posts and Telecommunications) et al. arXiv. [paper]
- [2023/01] Blind Judgement: Agent-Based Supreme Court Modelling With GPT. Sil Hamilton (McGill University). arXiv. [paper]
- [2023/05] Agents: An Open-source Framework for Autonomous Language Agents. Wangchunshu Zhou (AIWaves) et al. arXiv. [paper] [code]

Ordered cooperation
- [2023/10] AutoAgents: A Framework for Automatic Agent Generation. Guangyao Chen (Peking University) et al. arXiv. [paper] [code]
- [2023/09] MindAgent: Emerging Gaming Interaction. Ran Gong (UCLA) et al. arXiv. [paper] [code]
- [2023/08] CGMI: Configurable General Multi-Agent Interaction Framework. Shi Jinxin (East China Normal University) et al. arXiv. [paper]
- [2023/08] ProAgent: Building Proactive Cooperative AI with Large Language Models. Ceyao Zhang (The Chinese University of Hong Kong, Shenzhen) et al. arXiv. [paper] [code]
- [2023/08] AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors in Agents. Weize Chen (Tsinghua University) et al. arXiv. [paper] [code]
- [2023/08] AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation Framework. Qingyun Wu (Pennsylvania State University ) et al. arXiv. [paper] [code]
- [2023/08] MetaGPT: Meta Programming for Multi-Agent Collaborative Framework. Sirui Hong (DeepWisdom) et al. arXiv. [paper] [code]
- [2023/07] Communicative Agents for Software Development. Chen Qian (Tsinghua University) et al. arXiv. [paper] [code]
- [2023/06] Multi-Agent Collaboration: Harnessing the Power of Intelligent LLM Agents. Yashar Talebira (University of Alberta) et al. arXiv. [paper]
- [2023/05] Training Socially Aligned Language Models in Simulated Human Society. Ruibo Liu (Dartmouth College) et al. arXiv. [paper] [code]
- [2023/05] SwiftSage: A Generative Agent with Fast and Slow Thinking for Complex Interactive Tasks. Bill Yuchen Lin (Allen Institute for Artificial Intelligence) et al. arXiv. [paper] [code]
- [2023/05] ChatGPT as your Personal Data Scientist. Md Mahadi Hassan (Auburn University) et al. arXiv. [paper]
- [2023/03] CAMEL: Communicative Agents for "Mind" Exploration of Large Scale Language Model Society. Guohao Li (King Abdullah University of Science and Technology) et al. arXiv. [paper] [code]
- [2023/03] DERA: Enhancing Large Language Model Completions with Dialog-Enabled Resolving Agents. Varun Nair (Curai Health) et al. arXiv. [paper] [code]
- [2023/04] Self-collaboration Code Generation via ChatGPT. Yihong Dong (Peking University) et al. arXiv. [paper]

Adversarial Interaction for Advancement
- [2023/08] ChatEval: Towards Better LLM-based Evaluators through Multi-Agent Debate. Chi-Min Chan (Tsinghua University) et al. arXiv. [paper] [code]
- [2023/05] Improving Factuality and Reasoning in Language Models through Multiagent Debate. Yilun Du (MIT CSAIL) et al. arXiv. [paper] [code]
- [2023/05] Improving Language Model Negotiation with Self-Play and In-Context Learning from AI Feedback. Yao Fu (University of Edinburgh) et al. arXiv. [paper] [code]
- [2023/05] Examining the Inter-Consistency of Large Language Models: An In-depth Analysis via Debate. Kai Xiong (Harbin Institute of Technology) et al. arXiv. [paper]
- [2023/05] Encouraging Divergent Thinking in Large Language Models through Multi-Agent Debate. Tian Liang (Tsinghua University) et al. arXiv. [paper] [code]

<br/>

| [Index](./) | [Previous](5-1-agent-dev) | [Next](5-5-grounding)
