---
layout: post
title: MDP 数学模型
---

作者：王思炜

我们下面首先给出 MDP 问题的数学模型，然后给出状态价值函数的数学模型。

## MDP 数学模型

### 状态空间 $\mathcal{S}$

### 行为空间$\mathcal{A}(s)$

在某一状态 $s$ 下，可采取行为 $ a_1,a_2,a_3...$ 的集合

### 即时奖励$\mathcal{R}(s,a)$

|  🐱   |  🐀   |  🧀   |
| :--: | :--: | :--: |

在状态 $s$ 下，采取行为 $a$ ,得到的即时奖励。比如一只小老鼠在一张网格中某个网格$(s)$下，采取向右走的动作$(a_1)$,我就能走到奶酪网格中，那么此时得到的奖励是正数 $r(s,a_1)$，如果它采取向左走的动作，它会遇见一只猫，那么即时奖励是负数$r(s,a_2)$。

### 模型(Model)

$p(s'|s,a)$从某一状态$s$ 采取某一行为 $a$ 进入到下一个状态$s'$的概率。并且有：
$$
\sum_{s'\in \mathcal{S}}p(s'|s,a)=1
$$
$p(r|s,a)$从某一状态$s$ 采取某一行为 $a$ ，得到的即时奖励为 $r$ 的概率。并且有：
$$
\sum_{r\in \mathcal{R(s,a)}}p(r|s,a)=1
$$

### 策略(Policy)

$\pi(a|s)$ 一个条件概率，在状态 $s$ 下采取某一行为的概率。并且有：
$$
\sum_{a\in \mathcal{A(s)}}\pi(a|s)=1
$$

### 马尔科夫性质(Markov property)

无记忆性(memoryless):只和最近的状态有关
$$
p(s_{t+1}|s_t,a_t,s_{t-1},a_{t-1},...,s_0,a_0)=p(s_{t+1}|s_t,a_t),\\
p(r_{t+1}|s_t,a_t,s_{t-1},a_{t-1},...,s_0,a_0)=p(r_{t+1}|s_t,a_t),
$$

## 状态价值函数模型

-$\upsilon_\pi(s)$

### 定义

假设从某一状态$s$出发，执行某个动作$a$,得到一个即时奖励$r$，并且到达下一状态$s'$。从$s'$继续出发，重复执行此过程直到终止状态(如果没有终态，那么一直执行此过程)。

通过上述过程可以得到一条轨迹( trajectory , $\tau$ ): $\tau-s_0,a_0,r_1,s_1,a_1,r_2,...,r_t,s_t$

从一个确定的$s_0$出发，通过一个确定的策略 $\pi(a|s)$ 执行不同的动作 $a$ 可以得到很多条不同的轨迹$\tau$。

从一条轨迹中找到每次动作后的即时奖励($r_1,r_2,r_3,...,r_t$)

对一条轨迹上的所有即时奖励求加权和($0<\gamma<1$)：通常称之为 return
$$
\sum_{t=1}^{t}\gamma^{t-1} r_t=g_0 \notag
$$

由于从$s_0$出发根据一个固定的策略 $\pi(a|s)$ 可以得到很多条轨迹，每条轨迹都会得到一个 g。对这些不同轨迹得到的不同g,求均值或者称之为期望(大写字母代表的是随机变量)：
$$
\mathbb{E}[G_t|S_t=s_0]=\upsilon_\pi(s_0) \notag
$$
此表达式即在策略$\pi(a|s)$下，$s_0$状态的价值。$\upsilon_\pi(s)$只和状态$s$和策略$\pi(a|s)$有关。

### 性质

通过对公式(2)进行简单的变形，可以得到状态价值$\upsilon_\pi(s)$的另一种表达形式：
$$
\begin{align} 
G_t& =R_{t+1}+\gamma R_{t+2}+\gamma^{2}R_{t+3}+... \notag\\
& =R_{t+1}+\gamma(R_{t+2}+\gamma R_{t+3}+...) \notag\\
& =R_{t+1}+\gamma G_{t+1} \\
\end{align}
$$
上面的等式建立了$G_t$和$G_{t+1}$的关系。$\upsilon_\pi(s)$可以写成：
$$
\begin{align} 
\upsilon_\pi(s)&=\mathbb{E}[G_t|S_t=s] \notag\\
&=\mathbb{E}[R_{t+1}+\gamma G_{t+1}|S_t=s]\notag \\
&=\mathbb{E}[R_{t+1}|S_t=s]+\gamma\mathbb{E}[G_{t+1}|S_t=s]
\end{align}
$$
自此，$\upsilon_\pi(s)$分成了两部分。

第一部分：$\mathbb{E}[R_{t+1}|S_t=s]$
$$
\begin{align} 
\mathbb{E}[R_{t+1}|S_t=s]&=\sum_{a\in \mathcal{A(s)}}\pi(a|s)\mathbb{E}[R_{t+1}|S_t=s,A_t=a] \notag \\
&=\sum_{a\in \mathcal{A(s)}}\pi(a|s)\sum_{r\in\mathcal{R(s,a)}}p(r|s,a)·r
\end{align}
$$

第二部分：$\mathbb{E}[G_{t+1}|S_t=s]$
$$
\begin{align} 
\mathbb{E}[G_{t+1}|S_t=s]&= \sum_{s'\in \mathcal{S}}p(s'|s) \mathbb{E}[G_{t+1}|S_t=s,S_{t+1}=s']\notag\\
&=\sum_{s'\in \mathcal{S}}p(s'|s) \mathbb{E}[G_{t+1}|S_{t+1}=s'] \quad\quad (由于马尔科夫的无记忆性质可以忽略t时刻的状态)\notag\\
&=\sum_{s'\in \mathcal{S}}p(s'|s)\upsilon_\pi(s')\notag\\
&=\sum_{s'\in \mathcal{S}}\upsilon_\pi(s')\sum_{a \in \mathcal{A(s)}}\pi(a|s)p(s'|s,a)
\end{align}
$$

把公式(3)(4)代入到(2)中：
$$
\upsilon_\pi(s)=\sum_{a\in \mathcal{A(s)}}\pi(a|s) \bigg[\sum_{r\in\mathcal{R(s,a)}}p(r|s,a)·r+\gamma\sum_{s'\in \mathcal{S}}\upsilon_\pi(s')p(s'|s,a) \bigg]
$$
对于任意的状态 s 都要满足等式(5)。

<br/>

|[Index](./) | [Previous](5-mdp) | [Next](6-rl-intro)|
