---
layout: post
title: 最佳接收
---

## 最佳接收机的定义和最大后验概率准则

数字通信系统，我们在接收端面临这样一个任务：我们要“推理”（Inference）发送端发的是代表 0 的信号 $$s_0$$，还是代表 1 的信号 $$s_1$$。

要做这样的推断，有两种情况：

首先，即使我们什么也没有收到，我们也可以根据我们预先了解的信源发送 0 和 1 的概率 $$P(s_0)$$ 和 $$P(s_1)$$，来推理发送端会发送什么。用数学的语言说，如果 $$P(s_0)$$ > $$P(s_1)$$，我们就应该推断发送端发的是 $$s_0$$，否则，就推断发送的是 $$s_1$$。这样，我们的错误概率最小。

$$P(s_0)$$ 和 $$P(s_1)$$，通常被称为“先验概率”，即我们预先就知道的概率。

其次，当我们收到一个信号 $$r$$ 后，这个 $$r$$ 提供了一些信息，我们就应该根据这个 $$r$$ 的形状，去更新我们对 $$s_0$$ 和 $$s_1$$ 的概率推测。从数学上来说，我们就是要计算 $$P(s_0 \mid r)$$ 和 $$P(s_1 \mid r)$$，就是说，在收到 r 这个信号的条件下，我们重新估计 $$s_0$$ 和 $$s_1$$ 的概率。这个概率叫“后验概率”。

然后，我们比较 $$s_0$$ 和 $$s_1$$ 的后验概率，如果 $$P(s_0 \mid r) > P(s_1 \mid r)$$，我们就会推断发送端发的是 $$s_0$$，否则，就推断发送的是 $$s_1$$。这样，我们的错误概率最小。

换句话说，我们就是要在候选的信号 $$s_0$$ 和 $$s_1$$ 中，选后验概率最大的。这就是我们的推断的原则。这个原则是最优的，因为它能让我们的错误概率最小。

所以，按照这种规则进行推理的接收机，叫“最佳接收机”。而这个规则，就叫做 MAP：最大后验概率准则。

## 贝叶斯推理

那么，后验概率 $$P(s_0 \mid r)$$ 怎么求呢？很幸运的，贝叶斯老师在两百多年前（1742年前后）就思考过这个问题。佩服吧。他说，我们应该这么求

$$ P(s \mid r) = \frac{P(r \mid s)P(s)}{P(r)} $$

所以，我们的问题就变成：要比较 $$P(s_0 \mid r) = \frac{P(r \mid s_0)P(s_0)}{P(r)} $$ 和 $$ P(s_1 \mid r) = \frac{P(r \mid s_1)P(s_1)}{P(r)} $$。

等价于比较 $$ P(r \mid s_0)P(s_0) $$ 和 $$ P(r \mid s_1)P(s_1) $$。

观察上面的式子，大家是不是感觉到很有道理？

首先，其中包括了先验概率 $$P(s_0)$$ 和 $$P(s_1)$$。这个符合大家的期待吧？比如：如果 $$s_0$$ 的先验概率就是要大些，我们是要偏向 $$s_0$$ 一些，对吧？

其次，它又不是完全就看先验概率，而是看了 $$P(r \mid s_0)$$ 和 $$P(r \mid s_1)$$。那么，$$P(r \mid s_0)$$ 和 $$P(r \mid s_1)$$ 是什么东西呢？它们就是所谓的“似然”。

“似然”指的是：假设现在模型 $$s_0$$ 成立，此时我们观察到的数据 r 出现的概率。比如，我们假设硬币的正面朝上的概率是 0.4，这是我们对这个硬币的“模型”，然后我们观察到的实验数据是“正面、正面、反面”，那么，这个实验数据的似然就是 0.4 * 0.4 * 0.6 = 0.096。

所以，$$P(r \mid s_0)$$ 就是我们的观察 r 在“发送端发送 $$s_0$$”这个模型下发生的概率。$$P(r \mid s_1)$$ 就是我们的观察 r 在“发送端发送 $$s_1$$”这个模型下发生的概率。我们说“发送端发送 $$s_0$$”是个“模型”，大家可能不太习惯。请大家慢慢习惯一下。

因此，我们比较 $$ P(r \mid s_0) P(s_0) $$ 和 $$ P(r \mid s_1) P(s_1) $$ 时，也看了我们的观察 r 在“发送端发送 $$s_1$$”这个模型下发生的概率，和它在“发送端发送 s2”这个模型下发生的概率。

这也符合我们的期望吧？因为，如果观察 r 在“发送端发送 $$s_1$$”这个模型下发生的概率大，我们是要倾向于推断“发送端发的是 $$s_1$$”多一些，对吧？

这就是贝叶斯老师把 $$ P(s \mid r) $$ 表示为 $$ \frac{P(r \mid s)P(s)}{P(r)} $$ 的深意。这样的话，我们可以通过比较 $$ P(r \mid s)P(s) $$ 来进行推断。

那么，为什么非要比较 $$ P(r \mid s) $$ 和 $$ P(s) $$ 呢？因为它们是可以通过测量来获得的啊。比如，我们是不是可以通过测量我们的信源，得到它发 0 和 1 的先验概率？ 这就是 P(s)。类似的，我们通过测量我们的噪声，发现它符合高斯分布，所以我们就可以用均值为 s 的高斯分布，来表示 $$ P(r \mid s)$$，对不对？

所以，贝叶斯老师的这个公式，让我们的推理成为了现实。这就是举世震惊的“贝叶斯推理”。自从贝叶斯发明它以后，影响了人类近 300 年了。在它之前，人们都是“经验”推理。但自从贝叶斯提出这个之后，人类的推理变成了数学推理。这就是贝叶斯定理的伟大之处。大家今天能通过通信原理学习它，是多么的赚到了！

## 最大似然准则

那么，当 $$s_0$$ 和 $$s_1$$ 的先验概率相等的情况下，比较 $$P(r \mid s_0) P(s_0)$$ 和 $$P(r \mid s_1) P(s_1)$$ 就等价于比较 $$P(r \mid s_0)$$ 和 $$P(r \mid s_1)$$。也就是说，我们比较 $$P(r \mid s)$$ 这个“似然”就行了。当 $$P(r \mid s_0) > P(r \mid s_1)$$ 时，我们就推断发送端发的是 $$s_0$$，否则，就推断发的是 $$s_1$$。

换句话说，就是我们比较 $$s_0$$ 和 $$s_1$$ 的“似然”，谁的“似然”大，我们就推断发送的是谁。这就叫“最大似然准则”。注意，只有在 $$s_0$$ 和 $$s_1$$ 的先验概率相等的情况下，它才等价于最佳接收。

## 基带双极性信号下的情形

让我们假设我们发送的是基带双极性信号，因此，我们的 $$s_0$$ = -1， $$s_1$$ = 1。假设噪声是高斯分布，我们有 $$P(r \mid s_0)$$ 等于均值是 -1 的高斯分布；$$P(r \mid s_1)$$ 等于均值是 1 的高斯分布。

比较 $$P(r \mid s_0)$$ 和 $$P(r \mid s_1)$$ 就相当于比较 $$ -(r-1)^2 $$ 和 $$ -(r+1)^2 $$。注意，我们比较的式子里有一个负号，这是因为高斯分布的指数是有负号的。

那么，这个 $$(r-1)^2$$ 和 $$(r+1)^2$$ 是什么呢？是不是分别是，在 X 轴上，r 这个值和 +1/-1 这两个值的欧式距离的平方？因此，比较 $$P(r \mid s_0)$$ 和 $$P(r \mid s_1)$$，就等价于比较 r 和 $$s_0$$/$$s_1$$ 的欧式距离。r 离 $$s_0$$ 的距离小，就推断发送端发的是 $$s_0$$，否则就推断发的是 $$s_1$$。

换句话说，对基带双极性信号，当我们假设噪声是高斯分布时，“最大似然准则”就相当于 r 和 s 之间的最小欧式距离准则。

因此，我们现在把最佳接收问题，变成了一个几何问题了！但目前，这还仅适用于基带双极性信号。我们能不能把它适用于其他所有的信号，比如 QAM、MPSK ？

答案是肯定的，但在此之前，我们需要学习怎么把一个信号的波形，转换为一个几何的坐标。此时，大家一定会说：啊！这是我们在 QAM 那部分已经学过的信号“星座图”。对！但下面我们要系统地学习“信号空间”。一旦有了“信号空间”，我们就可以把信号和系统的问题，变为几何问题。

## 信号空间概念

大家还记不记得，几何里的向量空间的基本概念？包括“内积”、“投影”、“单位正交基”、“矢量长度”、“范数”、“欧式距离”、“相关系数”。下面我们要把信号与系统的各种概念，映射到这些概念上去。

我们首先看“内积”的概念。两个向量的内积，就是它们的对应数值的相乘，然后相加。比如 [1,2] 和 [3,4] 的内积，就是 1 * 3 + 2 * 4 = 11。大家看，它们是“离散”的数值的对应相乘相加。那么，我们类似地定义两个连续信号的“内积”，就是它们的波形在时间上的相乘，然后积分。

有了“内积”的概念，我们就可以建立“正交”的概念：两个信号的内积为 0，它们就“正交”。

有了“正交”，我们就可以定义“单位正交基”信号：它们两两正交，能量为 1。

有了“基信号”，就可以把它们张成一个“信号空间”。

有了“内积”的概念，我们也可以建立“投影”的概念。：一个信号和一个基信号的“内积”，就是在它在这个基信号上的“投影”。

所以，“信号空间”中的任何一个信号，它在张成这个空间的“基信号”上的投影，组成的矢量，就是这个信号的“信号矢量”。

有了“信号矢量”，我们就可以方便地表示信号的能量：一个信号的投影值的平方和（就是它的“2 范数”的平方），就等于这个信号的“能量”。

有了“信号矢量”，我们也可以很方便地计算两个信号的波形的“相关系数”了，它就等于这两个信号的信号矢量的“相关系数”。

最后，“信号矢量”，我们也可以很方便地计算两个信号的波形的“距离”，它是两个信号的波形的差别的平方的积分。我们发现，它就等于这两个信号的信号矢量的“欧式距离”。这一点非常重要，我们后面会用到这一点。请大家先留意这个。

## 信号空间的格兰姆-施密特正交化方法

那么，给定 n 个信号，如何获得它们的单位正交基呢？我们还是利用格兰姆-施密特正交化方法，只是通过对应的信号操作。

具体来说，格兰姆-施密特正交化方法需要两个操作：

首先对一个信号做“单位化”，就是把这个信号除以它的“2 范数”。那这个“2 范数”就是这个信号的能量的开根号；

然后计算一个信号在一个单位正交基上的投影，那就是计算这个信号和这个正交基的“内积”，即它们在时域上的乘积，然后积分。

基于这两个操作，我们就可以不断迭代，获得这 $$n$ 个信号的正交基。详见 PPT。

请大家用上述方法，建立 ASK、PSK、FSK、QPSK、MASK、MFSK、MQAM 信号的正交化，并获得它们的各个信号的矢量表示。

## Quiz

### 信号空间

1. 什么是数字信号的最佳接收问题？
1. 什么是矢量空间？
1. 写出矢量 v 在矢量 u 上投影的数学计算公式，简述其物理意义
1. 什么是矢量的范数？写出其数学计算公式，简述其物理意义
1. 什么是两个矢量的欧氏距离？写出其数学计算公式，简述其物理意义
1. 什么叫“归一化正交基”？
1. 如何将有限信号集展开为正交函数的表示？
1. 什么是正交信号空间？QAM信号的归一化正交信号基是？
1. 如果构造有限信号集的正交信号空间？
11. 什么是信号矢量？如何用信号矢量表示信号的能量？
11. 什么是信号矢量空间？
11. 什么是两个矢量的相关系数？写出它的数学表达式。什么是两个矢量的Cos距离？
11. 什么是两个信号的相关系数？写出它的数学表达式。
11. 两个信号的相关系数和它们矢量的相关系数有什么关系？
11. 什么是两个信号的欧式距离？写出它的数学表达式。
11. 两个信号的欧氏距离和它们矢量的欧式距离有什么关系？
11. 什么是Constellation？
11. M进制数字通信，有几种不同信号？在信号空间上有多少个点？
11. 用什么方法可以进行向量的正交化？简述其原理
21. 用什么方法可以进行信号的正交化？简述其原理
21. 对 2ASK 信号进行信号的正交化，得到的正交基函数有几个，是什么？信号的正交表示是？信号的矢量形式是？它是几维调制？两个信号的相关系数是？信号点距离是？
21. 对 2PSK 信号进行信号的正交化，得到的正交基函数有几个，是什么？信号的正交表示是？信号的矢量形式是？它是几维调制？两个信号的相关系数是？信号点距离是？
21. 对 2FSK 信号进行信号的正交化，得到的正交基函数有几个，是什么？信号的正交表示是？信号的矢量形式是？它是几维调制？两个信号的相关系数是？信号点距离是？
21. 对 QPSK 信号进行信号的正交化，得到的正交基函数有几个，是什么？信号的正交表示是？信号的矢量形式是？它是几维调制？四个信号中，两两信号之间的相关系数是？信号点距离是？
21. 画出M进制调制系统的通用实现方式的框图，说明每一个模块的作用
21. MASK 信号的矢量表示是？最小的两两信号点之间的距离是？
21. MFSK 信号的矢量表示是？最小的两两信号点之间的距离是？
21. MPSK 信号的矢量表示是？最小的两两信号点之间的距离是？
21. MQAM 信号的矢量表示是？最小的两两信号点之间的距离是？

### 最佳接收准则

1. 什么是数字信号接收的“判决域”概念？请以二维信号空间为例，画图说明该概念，并指出何时会产生误码。
1. 当噪声为高斯噪声时，以二进制数字信号为例，请画出其错误率分析的图形，写出其错误率的公式。
1. 什么是先验概率？什么是后验概率？请写出数字通信系统中它们的数学表达式，并说明其物理意义
1. 什么是是 MAP 准则？为什么符合 MAP 准则的接收机是理想接收机？如何用电子器件实现MAP接收机？
1. 什么是“似然”？请写出数字通信系统中它们的数学表达式，并说明其物理意义
1. 什么是ML准则，请进行数学推导，说明何时 MAP 准则等价于 ML 准则？
1. 如果先验概率不等， MAP 准则可以演化为什么准则？

<br/>

|[Index](./) | [Previous](5-17-msk) | [Next](6-5-correlation)|
