---
layout: post
title: Agent 研究
---

智能代理能够为我们完成任务，具有智能：感知环境，学习或获取知识，来提高其性能。

为了实现智能追踪的 Agent，我们需要结合增强学习（RL）和大语言模型（LLM）。在我们的追踪 Agent 的设计中，LLM 提供知识和推理能力，而 RL 感知环境，调整策略，改进追踪的有效性和可靠性。

## Multi Agent

Ng 老师推荐论文

- “Communicative Agents for Software Development,” Qian et al. (2023) (the ChatDev paper)
- “AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation,” Wu et al. (2023) 
- “MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework,” Hong et al. (2023)

## 论文

下面是 Github Awesome Autonomous Agent Papers [网页](https://github.com/lafmdp/Awesome-Papers-Autonomous-Agent) 中推荐的论文。

### RL-based agent

Instruction following
- [NeurIPS'23] Natural Language-conditioned Reinforcement Learning with Inside-out Task Language Development and Translation
- [NeurIPS'23] Guide Your Agent with Adaptive Multimodal Rewards [project]
- Compositional Instruction Following with Language Models and Reinforcement Learning
- RT-1: Robotics Transformer for Real-World Control at Scale [blog]
- RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control [blog]
- Open X-Embodiment: Robotic Learning Datasets and RT-X Models [blog]
- [NeurIPS'23] Guide Your Agent with Adaptive Multimodal Rewards [project]
- LEO: An Embodied Generalist Agent in 3D World [project]

Build agent based on World model
- [ICLR'23 Oral] Transformers are Sample-Efficient World Models [code]
- Learning to Model the World with Language
- MAMBA: an Effective World Model Approach for Meta-Reinforcement Learning

Language as knowledge
- Learning with Language Inference and Tips for Continual Reinforcement Learning
- Informing Reinforcement Learning Agents by Grounding Natural Language to Markov Decision Processes
- Language Reward Modulation for Pretraining Reinforcement Learning

LLM as a tool
- [NeurIPS'23] Efficient Policy Adaptation with Contrastive Prompt Ensemble for Embodied Agents
- [ICLR'23] Reward Design with Language Models [code]
- [ICML'23] RLang: A Declarative Language for Describing Partial World Knowledge to Reinforcement Learning Agents [Poster]
- [ICML'23] Do Embodied Agents Dream of Pixelated Sheep: Embodied Decision Making using Language Guided World Modelling [Project][Code]
- [ICML'23] Grounding Large Language Models in Interactive Environments with Online Reinforcement Learning
- Leveraging Large Language Models for Optimised Coordination in Textual Multi-Agent Reinforcement Learning
- Text2Reward: Dense Reward Generation with Language Models for Reinforcement Learning
- Language to Rewards for Robotic Skill Synthesis
- Eureka: Human-Level Reward Design via Coding Large Language Models
- STARLING: Self-supervised Training of Text-based Reinforcement Learning Agent with Large Language Models

Generalization across tasks
- A Generalist Agent
- AMAGO: Scalable In-Context Reinforcement Learning for Adaptive Agents

Continual learning
- ADAPTER-RL: Adaptation of Any Agent using Reinforcement Learning
- Online Continual Learning for Interactive Instruction Following Agents
- [NeurIPS'23] A Definition of Continual Reinforcement Learning

Combine RL and LLM
- [NeurIPS'23] Large Language Models Are Semi-Parametric Reinforcement Learning Agents
- RoboGPT : An intelligent agent of making embodied long-term decisions for daily instruction tasks
- Can Language Agents Approach the Performance of RL? An Empirical Study On OpenAI Gym
- RLAdapter: Bridging Large Language Models to Reinforcement Learning in Open Worlds

Transformer-based policy
- [NeurIPS'23] Cross-Episodic Curriculum for Transformer Agents. [project]

Trajectory to language
- [NeurIPS'23] State2Explanation: Concept-Based Explanations to Benefit Agent Learning and User Understanding
- [NeurIPS'23] Semantic HELM: A Human-Readable Memory for Reinforcement Learning
- [ICML'23] Distilling Internet-Scale Vision-Language Models into Embodied Agents
- Understanding Your Agent: Leveraging Large Language Models for Behavior Explanation

Trajectory predication
- Multi-agent Trajectory Prediction with Scalable Diffusion Transformer

Others
- Enhancing Human Experience in Human-Agent Collaboration: A Human-Centered Modeling Approach Based on Positive Human Gain
- A Competition Winning Deep Reinforcement Learning Agent in microRTS
- Aligning Agents like Large Language Models

### LLM-based agent

Multimodal
- [ICML'23] PaLM-E: An Embodied Multimodal Language Model
- Steve-Eye: Equipping LLM-based Embodied Agents with Visual Perception in Open Worlds
- Multimodal Web Navigation with Instruction-Finetuned Foundation Models
- You Only Look at Screens: Multimodal Chain-of-Action Agents
- Learning Embodied Vision-Language Programming From Instruction, Exploration, and Environmental Feedback
- An Embodied Generalist Agent in 3D World
- JARVIS-1: Open-world Multi-task Agents with Memory-Augmented Multimodal Language Models

Train LLM for generalization & adaptation
- FireAct: Toward Language Agent Finetuning
- Adapting LLM Agents Through Communication
- AgentTuning: Enabling Generalized Agent Abilities for LLMs
- Retroformer: Retrospective Large Language Agents with Policy Gradient Optimization

Task-specific designing
- [NeurIPS'23] Describe, Explain, Plan and Select: Interactive Planning with LLMs Enables Open-World Multi-Task Agents
- [NeurIPS'23] SwiftSage: A Generative Agent with Fast and Slow Thinking for Complex Interactive Tasks [Github]
- Rethinking the Buyer’s Inspection Paradox in Information Markets with Language Agents
- A Language-Agent Approach to Formal Theorem-Proving
- Agent Instructs Large Language Models to be General Zero-Shot Reasoners
- Ghost in the Minecraft: Hierarchical Agents for Minecraft via Large Language Models with Text-based Knowledge and Memory
- PaperQA: Retrieval-Augmented Generative Agent for Scientific Research
- Language Agents for Detecting Implicit Stereotypes in Text-to-image Models at Scale
- Suspicion-Agent: Playing Imperfect Information Games with Theory of Mind Aware GPT-4

Multi-agent (e.g., society, coperation)
- Building Cooperative Embodied Agents Modularly with Large Language Models
- OKR-Agent: An Object and Key Results Driven Agent System with Hierarchical Self-Collaboration and Self-Evaluation
- MetaGPT: Meta Programming for Multi-Agent Collaborative Framework
- AutoAgents: A Framework for Automatic Agent Generation
- Dynamic LLM-Agent Network: An LLM-agent Collaboration Framework with Agent Team Optimization
- AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors
- Exploring Collaboration Mechanisms for LLM Agents: A Social Psychology View
- REX: Rapid Exploration and eXploitation for AI agents

Experimental analysis
- Identifying the Risks of LM Agents with an LM-Emulated Sandbox
- Evaluating Multi-Agent Coordination Abilities in Large Language Models
- Large Language Models as Gaming Agents
- Benchmarking Large Language Models as AI Research Agents
- Adaptive Environmental Modeling for Task-Oriented Language Agents
- CLIN: A Continually Learning Language Agent for Rapid Task Adaptation and Generalization

Benchmark & Dataset
- [ICLR'23] Task Ambiguity in Humans and Language Models [code]
- SmartPlay : A Benchmark for LLMs as Intelligent Agents
- AgentBench: Evaluating LLMs as Agents
- Put Your Money Where Your Mouth Is: Evaluating Strategic Planning and Execution of LLM Agents in an Auction Arena
- SOTOPIA: Interactive Evaluation for Social Intelligence in Language Agents
- SocioDojo: Building Lifelong Analytical Agents with Real-world Text and Time Series
- WebArena: A Realistic Web Environment for Building Autonomous Agents
- LLM-Deliberation: Evaluating LLMs with Interactive Multi-Agent Negotiation Game
- Evaluating Large Language Models at Evaluating Instruction Following
- CivRealm: A Learning and Reasoning Odyssey for Decision-Making Agents

Applications
- Lyfe Agents: generative agents for low-cost real-time social interactions
- AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation

Algorithm design
- [ICLR'23 Oral] ReAct: Synergizing Reasoning and Acting in Language Models [code]
- [NeurIPS'23] AdaPlanner: Adaptive Planning from Feedback with Language Models [github]
- Prospector: Improving LLM Agents with Self-Asking and Trajectory Ranking
- Formally Specifying the High-Level Behavior of LLM-Based Agents
- Cumulative Reasoning With Large Language Models

Combined with RL
- [NeurIPS'23] Reflexion: language agents with verbal reinforcement learning [code]
- Teaching LLMs to Teach Themselves Better Instructions via Reinforcement Learning
- Language Agents with Reinforcement Learning for Strategic Play in the Werewolf Game

Others
- LUMOS: Towards Language Agents that are Unified, Modular, and Open Source
- Lemur: Harmonizing Natural Language and Code for Language Agents
- Language Agent Tree Search Unifies Reasoning Acting and Planning in Language Models

<br/>

| [Index](./) | [Previous](5-7-tool-usage) | [Next](6-1-agi)
