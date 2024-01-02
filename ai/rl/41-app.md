---
layout: post
title: 增强学习的应用
---

RL 有大量的应用。下面是滑铁卢课程老师给出的各个领域的 RL 的应用的论文，很有意思。

RL for Math
- Alhussein Fawzi, Matej Balog, Aja Huang, Thomas Hubert, Bernardino Romera-Paredes, Mohammadamin Barekatain, Alexander Novikov, Francisco J. R. Ruiz, Julian Schrittwieser, Grzegorz Swirszcz, David Silver, Demis Hassabis & Pushmeet Kohli (2022), Discovering faster matrix multiplication algorithms with reinforcement learning, Nature volume 610, pages47–53.

RL for Health
- Mariya Popova, Olexandr Isayev, Alexander Tropsha (2018), Deep reinforcement learning for de novo drug design, Science Advances, Vol 4, Issue 7.

RL for Games
- Julian Schrittwieser, Ioannis Antonoglou, Thomas Hubert, Karen Simonyan, Laurent Sifre, Simon Schmitt, Arthur Guez, Edward Lockhart, Demis Hassabis, Thore Graepel, Timothy Lillicrap & David Silver (2020), Mastering Atari, Go, chess and shogi by planning with a learned model, Nature volume 588, pages604–609.
- Linus Gisslén, Andy Eakins, Camilo Gordillo, Joakim Bergdahl, Konrad Tollmar (2021), Adversarial Reinforcement Learning for Procedural Content Generation, IEEE Conference on Games, pages 1-8.

RL for Finance
- Zhengyao Jiang, Jinjun Liang (2017), Cryptocurrency Portfolio Management with Deep Reinforcement Learning, Intelligent Systems Conference.
- Berend Jelmer Dirk Gort, Xiao-Yang Liu, Xinghang Sun, Jiechao Gao, Shuaiyu Chen, and Christina Dan Wang (2022), Deep Reinforcement Learning for Cryptocurrency Trading: Practical Approach to Address Backtest Overfitting, In Proceedings of 3rd ACM International Conference on AI in Finance (ICAIF). ACM, New York, NY, USA, 9 pages.

RL for Data Systems
- Ryan Marcus, Parimarjan Negi, Hongzi Mao, Chi Zhang, Mohammad Alizadeh, Tim Kraska, Olga Papaemmanouil, Nesime Tatbul (2019), Neo: A Learned Query Optimizer, PVLDB, 12(11): 1705-1718.

RL for Optimization
- Iddo Drori, Anant Kharkar, William R. Sickinger, Brandon Kates, Qiang Ma, Suwen Ge, Eden Dolev, Brenda Dietrich, David P. Williamson, Madeleine Udell (2020), Learning to Solve Combinatorial Optimization Problems on Real-World Graphs in Linear Time, IEEE International Conference on Machine Learning and Applications (ICMLA).

Credit Assignment in RL
- Thomas Mesnard, Théophane Weber, Fabio Viola, Shantanu Thakoor, Alaa Saade, Anna Harutyunyan, Will Dabney, Tom Stepleton, Nicolas Heess, Arthur Guez, Éric Moulines, Marcus Hutter, Lars Buesing, Rémi Munos, Counterfactual Credit Assignment in Model-Free Reinforcement Learning, International Conference on Machine Learning, PMLR 139.

Explainability
- Stratis Tsirtsis, Abir De, Manuel Gomez Rodriguez (2021), Counterfactual Explanations in Sequential Decision Making Under Uncertainty, NeurIPS.

RL in Software Verification
- Konstantin Böttinger, Patrice Godefroid, Rishabh Singh (2018), Deep Reinforcement Fuzzing, IEEE Symposium on Security and Privacy Workshops.

RL for Recommender Systems
- Lixin Zou, Long Xia, Zhuoye Ding, Jiaxing Song, Weidong Liu, Dawei Yin (2019), Reinforcement Learning to Optimize Long-term User Engagement in Recommender Systems, KDD.

RL as sequence modeling
- Michael Janner, Qiyang Li, Sergey Levine (2021), Offline Reinforcement Learning as One Big Sequence Modeling Problem, NeurIPS.

RL for Continual Learning
- Ju Xu, Zhanxing Zhu (2018), Reinforced Continual Learning, NeurIPS

RL for Computer Vision
- Li, H., Guo, Y., Wang, Z., Xia, S., & Zhu, W. (2019). AdaCompress: Adaptive compression for online computer vision services. In Proceedings of the 27th ACM International Conference on Multimedia (pp. 2440-2448).

RL for Traffic Control
- Tianshu Chu, Jie Wang, Lara Codecà, and Zhaojian Li (2020), Multi-Agent Deep Reinforcement Learning for Large-Scale Traffic Signal Control, IEEE Transactions on Intelligent Transportation Systems, Vol 21, No 3.

下面是 伯克利 CS 285 RL 课程中提到的 RL 的应用

- RT-2: Vision-Language-Action Models: https://robotics-transformer2.github.io/
    - Leveraging advances in pretrained models
    - ViT 然后进 LLM

- [芯片设计](https://ai.googleblog.com/2020/04/chip-design-with-deep-reinforcement.html)
- 图像生成
    - Kevin Black*, Michael Janner*, Yilun Du, Ilya Kostrikov, Sergey Levine. Training Diffusion Models with Reinforcement Learning. 2023.
    - LLaVA 加 DDPO，不断演进，按照文字，生成图片

- 机器人
    - Herzog et al. Deep RL at Scale: Sorting Waste in Office Buildings with a Fleet of Mobile Manipulators. 2023.

- 非常非常复杂的物理任务
    - Rudin et al., “Learning Locomotion and Local Navigation End-to-End.” 2022

- 复杂物理任务
    - Smith et al., “Learning and Adapting Agility Skills by Transferring Experience.” 2022.

- 用锤子
    - Rajeswaran, et al. 2018

- robotic grasping with Q-functions
    - QT-Opt, Kalashnikov et al. ‘18
    - Q-learning from images for real-world robotic grasping

- walking with policy gradients
    - High-dimensional continuous control with generalized advantage estimation, Schulman et al. ‘16
    - Trust region policy optimization with value function approximation

- robots and model-based RL
    - End-to-end training of deep visuomotor policies, L.* , Finn* ’16
    - Guided policy search (model-based RL) for image-based robotic manipulation

- Atari games with Q-functions
    - Playing Atari with deep reinforcement learning, Mnih et al. ‘13
    - Q-learning with convolutional neural networks

## Misc

Diffusion Policy
    Toyota Research's supposed breakthrough in leveraging DDPMs for learning policies for real-world Robotics
    https://github.com/lucidrains/diffusion-policy
    https://arxiv.org/abs/2303.04137

    Implementation of Diffusion Policy, Toyota Research's supposed breakthrough in leveraging DDPMs for learning policies for real-world Robotics

    What seemed to have happened is that a research group at Columbia adapted the popular SOTA text-to-image models (complete with denoising diffusion with cross attention conditioning) to policy generation (predicting robot actions conditioned on observations). Toyota research then validated this at a certain scale for imitation learning with real world robotic demonstrations. It is hard to know how much of a breakthrough this is given corporate press is prone to exaggerations, but let me try to get a clean implementation out, just in the case that it is.

    The great thing is, if this really works, all the advances being made in text-to-image space can translate to robotics. Yes, this includes stuff like dreambooth and perfusion.


<br/>

|[Index](index) | [Previous](33-transfer) | [Next](51-advanced) |
