---
layout: post
title: bellman equation 贝尔曼方程
---

作者：王思炜
### 贝尔曼方程的不同形式

从上一节中可以得到贝尔曼方程：

$$
\upsilon_\pi(s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s) \bigg[\sum_{r\in\mathcal{R(s,a)}}p(r|s,a)·r+\gamma\sum_{s'\in \mathcal{S}}\upsilon_\pi(s')p(s'|s,a) \bigg]
$$

其中：

$$\upsilon_\pi(s)$$和$$\upsilon_\pi(s')$$是将要求解的状态价值。

$$\pi(a\vert s)$$是给定的策略。因为状态值可以用来评估一个策略的好坏，所以从贝尔曼方程求解状态价值的过程是一个策略评估的过程。

$$p(r \vert s,a)$$和$$p(s'\vert s,a)$$代表了系统的物理模型(即已知从每个状态的每个行为发生的概率，和得到即时奖励的概率)。但是在大部分情况下，我们无法得知具体的物理模型，也就无从得知这两个概率分布，我们有的只是次次实验的数据，届时，将会介绍 model-free 的方法来计算状态价值。



根据全概率公式：$$p(a)=\sum_{i=1}^np(b_i)p(a\vert b_i)=\sum_{i=1}^np(a,b_i)$$

贝尔曼方程中$$p(r\vert s,a)$$和$$p(s'\vert s,a)$$可以用全概率公式替换：

$$
\begin{align} 
p(s'|s,a)&=\sum_{r\in\mathcal{R(s,a)}}p(s',r|s,a) \notag \\
p(r|s,a) &=\sum_{s'\in \mathcal{S}}p(s',r|s,a) \notag\\
\end{align}
$$

替换后的贝尔曼方程为：

$$
\upsilon_\pi(s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s)\sum_{s'\in \mathcal{S}} \sum_{r\in\mathcal{R(s,a)}}p(s',r|s,a)[r+\gamma\upsilon_\pi(s') ]
$$

### 矩阵向量形式的贝尔曼方程

令：

$$
r_\pi(s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s)\sum_{r\in\mathcal{R(s,a)}}p(r|s,a)·r \notag \\
p_\pi(s'|s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s)p(s'|s,a)\notag \\
$$

不难看出$$r_\pi(s)$$代表了策略$$\pi$$下的即时奖励的均值，$$p_\pi(s'\vert s)$$代表了状态转移矩阵，替换后原始的贝尔曼方程如下：

$$
\upsilon_\pi(s)=r_\pi(s)+\gamma\sum_{s'\in \mathcal{S}}p_\pi(s'|s)\upsilon_\pi(s') \notag
$$

对此我们可以对每一个状态 s 得到一个等式。综合这些等式：

$$
\underbrace{
\begin{bmatrix}
\upsilon_\pi(s_1)\\
\upsilon_\pi(s_2)\\
\upsilon_\pi(s_3)\\
\upsilon_\pi(s_4)\\
\end{bmatrix}
}_{\upsilon_\pi}
=
\underbrace{
\begin{bmatrix}
r_\pi(s_1)\\
r_\pi(s_2)\\
r_\pi(s_3)\\
r_\pi(s_4)\\
\end{bmatrix}
}_{r_\pi}
+
\gamma
\underbrace{
\begin{bmatrix}
p_\pi(s_1|s_1) & p_\pi(s_2|s_1)& p_\pi(s_3|s_1) & p_\pi(s_4|s_1)\\
p_\pi(s_1|s_2) & p_\pi(s_2|s_2)& p_\pi(s_3|s_2) & p_\pi(s_4|s_2)\\
p_\pi(s_1|s_3) & p_\pi(s_2|s_3)& p_\pi(s_3|s_3) & p_\pi(s_4|s_3)\\
p_\pi(s_1|s_4) & p_\pi(s_2|s_4)& p_\pi(s_3|s_4) & p_\pi(s_4|s_4)\\
\end{bmatrix}
}_{P_\pi}
\underbrace{
\begin{bmatrix}
\upsilon_\pi(s_1)\\
\upsilon_\pi(s_2)\\
\upsilon_\pi(s_3)\\
\upsilon_\pi(s_4)\\
\end{bmatrix}
}_{\upsilon_\pi}
\notag
$$

就可以得到贝尔曼方程的矩阵向量形式：

$$
\upsilon_\pi=r_\pi+\gamma P_\pi\upsilon_\pi
$$

根据矩阵向量形式，便可以求解 解向量$$\upsilon_\pi$$，显然：

$$
\upsilon_\pi=(I-\gamma P_\pi)^{-1}r_\pi
$$

但在实际中，我们更倾向于使用数值方法来计算解向量$$\upsilon_\pi$$(参考数值分析中线性方程组的的迭代解法)：

$$
\upsilon_{k+1}=r_\pi+\gamma P_\pi\upsilon_{k},\quad k=0,1,2,...
$$

### 动作价值$$q_\pi(s,a)$$

动作价值的定义可以参考状态价值的定义：

$$
q_\pi(s,a)=\mathbb{E}[G_t|S_t=s,A_t=a]
$$

同时动作价值和状态价值也有着千丝万缕的联系：

$$
\underbrace{
\mathbb{E}[G_t|S_t=s]
}_{\upsilon_\pi(s)}
=
\sum_{a\in \mathcal{A(s)}}
\underbrace{
\mathbb{E}[G_t|S_t=s,A_t=a]
}_{q_\pi(s,a)}
\pi(a|s)
$$

即，状态价值是该状态下可能产生的动作的动作价值的期望：

$$
\upsilon_\pi(s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s)q_\pi(s,a)
$$

根据贝尔曼方程的形式，显然动作价值还可以写成：

$$
q_\pi(s,a)=\sum_{r\in\mathcal{R(s,a)}}p(r|s,a)·r+\gamma\sum_{s'\in \mathcal{S}}\upsilon_\pi(s')p(s'|s,a)
$$

<br/>

| [Index](./) |  [Previous](5-1-math) |  [Next](5-3-Bellman-optimality-equation)| 