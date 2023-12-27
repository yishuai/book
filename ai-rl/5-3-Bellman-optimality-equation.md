---
layout: post
title: bellman optimality equation 贝尔曼最优方程
---
作者：王思炜

### 贝尔曼最优方程

考虑一个最优问题：

$$
\upsilon_\pi(s)=max_{\pi}\sum_{a\in \mathcal{A(s)}}\pi(a|s)q_\pi(s,a)
$$

根据这个等式，需要找到一个最优的策略$$\pi$$ ，让$$\upsilon_\pi(s)$$达到最大。

首先看一个简单的优化问题：

$$
找到最优的系数：c_1,c_2,c_3的值，使该等式达到最大值：\notag\\
\sum_{i=1}^3c_iq_i=c_1q_1+c_2q_2+c_3q_3 \notag \\
其中q_i取任意实数，并且c_1+c_2+c_3=1;c_1,c_2,c_3\geq 0 \notag \\
$$

假设$$q_3\geq q_1,q_2$$，那么只要让$$q_3$$对应的权重$$c_3$$最大就可以了$$(c_3=1;c_1,c_2=0)$$。

$$
q_3=(c_1+c_2+c_3)q_3=c_1q_3+c_2q_3+c_3q_3\geq c_1q_1+c_2q_2+c_3q_3 \notag
$$

类比贝尔曼最优方程：最优方程中的$$\pi(a\vert s)$$可以看成$$c_i$$,因为$$\sum_a\pi(a\vert s)=1$$;最优方程中的$$q_\pi(s,a)$$可以看成$$q_i$$:

$$
\sum_{a\in \mathcal{A(s)}}\pi(a|s)q_\pi(s,a)\leq \sum_{a\in \mathcal{A(s)}}\pi(a|s)max_{a} q_\pi(s,a)=max_{a} q_\pi(s,a)
$$

显然，最优的策略就是让最大的动作价值所采取的行动的概率为 1：

$$
\pi(a|s)=
\left\{
\begin{aligned}
1 ,  a=a^* \\
0 , a\neq a^* \\
\end{aligned}
\right.
\\
a^*是使q_\pi(s,a)最大的动作。
$$

<br/>

| [Index](./) |  [Previous](5-2-bellman-equation) |  [Next](6-rl-intro)| 