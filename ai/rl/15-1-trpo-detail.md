---
layout: post
title: TRPO 置信域策略优化 NPG 自然策略梯度
---

作者：王思炜



### Hessian matrix

其实就是函数的二阶偏导构成的矩阵:
$$
\quad \quad \quad\quad F=f(x_1,x_2,...,x_n)  \notag \\
\\
H(F)=
\begin{bmatrix}
\frac {\partial^2 F}{\partial x_1^2} & \frac {\partial^2 F}{\partial x_1\partial x_2} & \cdots &\frac {\partial^2 F}{\partial x_1\partial x_n}\\
\frac {\partial^2 F}{\partial x_2\partial x_1} & \frac {\partial^2 F}{\partial x_2^2} & \cdots &\frac {\partial^2 F}{\partial x_2\partial x_n}\\
\vdots&\vdots&\ddots&\vdots\\
\frac {\partial^2 F}{\partial x_n\partial x_1} & \frac {\partial^2 F}{\partial x_n\partial x_2} & \cdots &\frac {\partial^2 F}{\partial x_n^2}\\
\end{bmatrix}
$$

Hessian matrix是牛顿法解决优化问题时常用的工具.它定义了分布空间的局部曲率.





### Fisher Information Matrix

假设对于一个随机变量$$X$$,已知分布$$f$$,但是分布的参数$$\theta $$未知,其中$$\theta=(\theta_1,\theta_2,\theta_3...) $$是参数组成的向量

$$
P(X=x_i)=f(x_i\mid\theta)\notag
$$
例如:随机变量 $$X$$ 的取值 $$x_i$$ 表示抛掷 $$k$$ 次硬币，正面向上的次数，那么此时 $$\theta $$ 就代表了这个待估计的正面向上的概率值

那么这个概率就表示为：
$$
P({X=x_i})=C_k^{x_i}\theta^{x_i}(1-\theta)^{k-x_i}\notag
$$


评估$$\theta$$的好坏 score function:
$$
s(x_i\mid\theta)=\nabla_{\theta}logf(x_i\mid\theta)=\frac{\nabla_{\theta}f(x_i\mid\theta)}{f(x_i\mid\theta)} \notag\\
=(\frac{1}{f(x_i\mid\theta)}·\frac{\partial f(x_i\mid\theta)}{\partial \theta_1},\frac{1}{f(x_i\mid\theta)}·\frac{\partial f(x_i\mid\theta)}{\partial \theta_2},\frac{1}{f(x_i\mid\theta)}·\frac{\partial f(x_i\mid\theta)}{\partial \theta_3},...)\\
s(X\mid\theta)=\nabla_{\theta}logf(X\mid\theta)=

\begin{bmatrix}
\frac{1}{f(x_1\mid\theta)}·\frac{\partial f(x_1\mid\theta)}{\partial \theta_1}&\frac{1}{f(x_1\mid\theta)}·\frac{\partial f(x_1\mid\theta)}{\partial \theta_2}& \cdots&\frac{1}{f(x_1\mid\theta)}·\frac{\partial f(x_1\mid\theta)}{\partial \theta_n}\\

\frac{1}{f(x_2\mid\theta)}·\frac{\partial f(x_2\mid\theta)}{\partial \theta_1}&\frac{1}{f(x_2\mid\theta)}·\frac{\partial f(x_2\mid\theta)}{\partial \theta_2}& \cdots&\frac{1}{f(x_2\mid\theta)}·\frac{\partial f(x_2\mid\theta)}{\partial \theta_n}\\
\vdots & \vdots &\ddots& \vdots\\
\frac{1}{f(x_m\mid\theta)}·\frac{\partial f(x_m\mid\theta)}{\partial \theta_1}&\frac{1}{f(x_m\mid\theta)}·\frac{\partial f(x_m\mid\theta)}{\partial \theta_2}& \cdots&\frac{1}{f(x_m\mid\theta)}·\frac{\partial f(x_m\mid\theta)}{\partial \theta_n}
\end{bmatrix}
$$
score function 性质 :
$$
\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)]=0 \\

\begin{align}
证明:\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)]=&\sum_{i=1}^n f(x_i\mid\theta)·s(x_i\mid\theta) \notag \\
=&\sum_{i=1}^n f(x_i\mid\theta)·\frac{\nabla_{\theta}f(x_i\mid\theta)}{f(x_i\mid\theta)}\notag\\
=&\sum_{i=1}^n\nabla_{\theta}f(x_i\mid\theta)\notag\\
=&\nabla_{\theta}\sum_{i=1}^nf(x_i\mid\theta)\notag\\
=&\nabla_{\theta}1\notag\\
=&\notag0
\end{align}
$$



Fisher Information Matrix:

Fisher Information Matrix定义为: score function的协方差矩阵:
$$
I(\theta)=\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)^2] \notag\\
因为:\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)]=0\\
I(\theta)=\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)^2]-\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)]^2=Cov(s(X\mid\theta),s(X\mid\theta))=Var[s(X\mid\theta)]\\
F=\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)^2]=\mathbb{E}_{X\sim f(x\mid\theta)}[s(X\mid\theta)·s(X\mid\theta)^T]=\mathbb{E}_{X\sim f(x\mid\theta)}[\nabla_{\theta}logf(X\mid\theta)·\nabla_{\theta}logf(X\mid\theta)^T]
$$

### Fisher Information Matrix和Hessian matrix的关系

Fisher Information Matrix可以理解成 : 对数似然的Hessian matrix期望的负值
$$
\begin{align}
H(log[f(X\mid\theta)])&=\nabla_{\theta}s(X\mid\theta)\notag\\
&=\nabla_{\theta}\frac{\nabla_{\theta}f(X\mid\theta)}{f(X\mid\theta)}\notag\\
&=\frac{H(f(X\mid\theta))·f(X\mid\theta)-\nabla_{\theta}f(X\mid\theta)\nabla_{\theta}f(X\mid\theta)^T}{f(X\mid\theta)·f(X\mid\theta)}\notag\\
&=\frac{H(f(X\mid\theta))·f(X\mid\theta)}{f(X\mid\theta)·f(X\mid\theta)}-\frac{\nabla_{\theta}f(X\mid\theta)\nabla_{\theta}f(X\mid\theta)^T}{f(X\mid\theta)·f(X\mid\theta)}\notag\\
&=\frac{H(f(X\mid\theta)}{f(X\mid\theta)}-\left(\frac{\nabla_{\theta}f(X\mid\theta }{f(X\mid\theta)}\right)·\left(\frac{\nabla_{\theta}f(X\mid\theta)}{f(X\mid\theta)}\right)^T\notag\\

\mathbb{E}_{X\sim f(x\mid\theta)}[H(log[f(X\mid\theta)])]&=\mathbb{E}_{X\sim f(x\mid\theta)}\bigg[  \frac{H(f(X\mid\theta)}{f(X\mid\theta)}-\left(\frac{\nabla_{\theta}f(X\mid\theta }{f(X\mid\theta)}\right)·\left(\frac{\nabla_{\theta}f(X\mid\theta)}{f(X\mid\theta)}\right)^T \bigg]\notag\\
&=\mathbb{E}_{X\sim f(x\mid\theta)}\bigg[ \frac{H(f(X\mid\theta))}{f(X\mid\theta)}\bigg]-\mathbb{E}_{X\sim f(x\mid\theta)}\bigg[ \left(\frac{\nabla_{\theta}f(X\mid\theta }{f(X\mid\theta)}\right)·\left(\frac{\nabla_{\theta}f(X\mid\theta)}{f(X\mid\theta)}\right)^T\bigg]\notag\\
&=\int f(x\mid\theta)·\frac{H(f(x\mid\theta))}{f(x\mid\theta)}dx-\mathbb{E}_{X\sim f(x\mid\theta)}[\nabla_{\theta}logf(X\mid\theta)·\nabla_{\theta}logf(X\mid\theta)^T]\notag\\
&=H(\int f(x\mid \theta)dx)-F\notag\\
&=H(1)-F\notag\\
&=-F\notag\\


F&=-\mathbb{E}_{X\sim f(x\mid\theta)}[H(log[f(X\mid\theta)])]
\end{align}
$$


### Fisher Information Matrix和KL散度的关系

KL-divergence:交叉熵-信息熵
$$
\begin{align}
D_{KL}[p(x)\parallel q(x)]&=H(p(x)\parallel q(x))-H(p(x)) \notag \\
&=\sum_{x\in X} -p(x)logq(x)-\sum_{x\in X} -p(x)logp(x)\notag\\
&=\sum_{x\in X} p(x)log\frac{p(x)}{q(x)}
\end{align}
$$
对于连续型随机变量换成积分即可:
$$
D_{KL}[p(x)\parallel q(x)]=\int p(x)log\frac{p(x)}{q(x)}dx \notag \\
$$
即两个期望相减的形式:
$$
D_{KL}[p(x)\parallel q(x)]=\mathbb{E}_{x\sim p(x)}[logp(x)]-\mathbb{E}_{x\sim p(x)}[logq(x)]
$$
将$$p(x),q(x)$$看成同一分布不同参数的形式:
$$
D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]=\mathbb{E}_{x\sim p(x\mid\theta)}[logp(x\mid\theta)]-\mathbb{E}_{x\sim p(x\mid\theta)}[logp(x\mid\theta')] \notag
$$
对$$\theta'$$求一阶导数:
$$
\begin{align}
\nabla_{\theta'}D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]&=\nabla_{\theta'}\mathbb{E}_{x\sim p(x\mid\theta)}[logp(x\mid\theta)]-\nabla_{\theta'}\mathbb{E}_{x\sim p(x\mid\theta)}[logp(x\mid\theta')] \notag\\
&=-\nabla_{\theta'}\mathbb{E}_{x\sim p(x\mid\theta)}[logp(x\mid\theta')]\notag\\
&=-\mathbb{E}_{x\sim p(x\mid\theta)}[\nabla_{\theta'}logp(x\mid\theta')]\\
&=-\int p(x\mid\theta)\nabla_{\theta'}logp(x\mid\theta')dx \notag
\end{align}
$$
根据score function 性质,显然,
$$
\nabla_{\theta'}D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]=0 \notag
$$


对$$\theta'$$求二阶导数:
$$
\begin{align}
\nabla_{\theta'}^2D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]&=-\int p(x\mid\theta)\nabla_{\theta'}^2logp(x\mid\theta')dx \notag\\
&=-\int p(x\mid\theta)H(logp(x\mid\theta'))dx \notag\\
当\theta'=\theta时 : 
上式&=-\int p(x\mid\theta)H(logp(x\mid\theta))dx \notag\\
&=-\mathbb{E}_{x\sim p(x\mid\theta)}[H(logp(x\mid\theta))]\notag\\
&=F
\end{align}
$$
不难看出KL散度对$$\theta' $$的二阶导数就是Fisher Information Matrix

### KL散度的二阶泰勒展开

令:$$\theta'=\theta+d$$
$$
D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta+d)]\\
\approx D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta)]+(\nabla_{\theta'}D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]\mid_{\theta=\theta'})^Td+\frac{1}{2}d^T(\nabla_{\theta'}^2D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta')]\mid_{\theta=\theta'})d
$$
将之前求得的$$\theta=\theta'$$一阶导数二阶导数带入得:
$$
D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta+d)]\approx\frac{1}{2}d^TFd
$$


### Natural Gradient 

有一损失函数$$\mathcal{L}(\theta)$$

即我们要在KL散度的分布空间内，找到一个向量$$d$$，让参数 $$\theta $$移动 从而最小化损失函数
$$
在约束条件下: D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta+d)]=c\\
d^* = arg min_{d}\mathcal{L}(\theta+d)
$$
使用拉格朗日乘子法求极值并且将KL散度用二阶泰勒展开近似,$$\mathcal{L}(\theta+d)$$用一阶泰勒展开近似:
$$
d^* = arg min_{d}\mathcal{L}(\theta+d)+\lambda(D_{KL}[p(x\mid\theta)\parallel p(x\mid\theta+d)]-c)\\
\approx arg min_{d}\mathcal{L}(\theta)+\nabla_{\theta}\mathcal{L}(\theta)^Td+\frac{1}{2}\lambda d^TFd-\lambda c
$$
$$\mathcal{L}(\theta+d)$$最小时,$$\nabla_{d}\mathcal{L}(\theta+d)=0$$,即:
$$
\nabla_{d}(\mathcal{L}(\theta)+\nabla_{\theta}\mathcal{L}(\theta)^Td+\frac{1}{2}\lambda d^TFd-\lambda c)=0\\

\nabla_{\theta}\mathcal{L}(\theta)+\lambda Fd=0\\
d=-\frac{1}{\lambda}F^{-1}\nabla_{\theta}\mathcal{L}(\theta)
$$
由于$$\lambda$$是固定长度,自然梯度$$\tilde{\nabla}_{\theta}\mathcal{L}(\theta)$$就可以表示为:
$$
\tilde{\nabla}_{\theta}\mathcal{L}(\theta)=F^{-1}\nabla_{\theta}\mathcal{L}(\theta)
$$
令$$\alpha=-\frac{1}{\lambda}$$那么$$d=\alpha\tilde{\nabla}_{\theta}\mathcal{L}(\theta)$$

使用拉格朗日乘子法对$$\lambda$$求导,并使其一阶导数为0:
$$
c=\frac{1}{2}d^TFd\\
=\frac{1}{2}\alpha\nabla_{\theta}\mathcal{L}(\theta)^TF^{-1}\alpha\nabla_{\theta}\mathcal{L}(\theta)\\
解得:\alpha=\sqrt{\frac{2c}{\nabla_{\theta}\mathcal{L}(\theta)^TF^{-1}\nabla_{\theta}\mathcal{L}(\theta)}}
$$
最终用自然梯度更新$$\theta$$的的过程为:
$$
\theta=\theta+d=\theta+\alpha\tilde{\nabla}_{\theta}\mathcal{L}(\theta)=\theta+\sqrt{\frac{2c}{\nabla_{\theta}\mathcal{L}(\theta)^TF^{-1}\nabla_{\theta}\mathcal{L}(\theta)}}F^{-1}\nabla_{\theta}\mathcal{L}(\theta)
$$
但是上面的等式中出现了逆矩阵,这是我们不愿意看到的,在TRPO中,是用共轭梯度法来通过迭代的方式求逆矩阵的

### 自然梯度与策略梯度的结合(TRPO)

普通的策略梯度:
$$
\nabla_{\theta}J(\pi_{\theta})=\int_{\mathcal{S}}\rho^{\pi}(s) \int_{\mathcal{A}}\nabla_{\theta}\pi_{\theta}(a\vert s)q_{\pi}(s,a)dads \\
=\mathbb{E}_{s\sim \rho^{\pi},a\sim \pi_{\theta}}[\nabla_{\theta}\pi_{\theta}(a\vert s)q_{\pi}(s,a)]
$$
自然策略梯度:指的是约束策略的行动概率变化小于一定数值下(KL散度约束)，使得目标函数变化最大的方向($$d$$).
$$
d=\tilde{\nabla}_{\theta}J(\theta)=F(\theta)^{-1}\nabla_{\theta}J(\pi_{\theta})\\
F(\theta)^{-1}=\mathbb{E}_{s\sim \rho^{\pi}(s)}[F_s(\theta)]\\
F_s(\theta)=\mathbb{E}_{\pi(a;s,\theta)}[\frac{\partial log\pi(a;s,\theta)}{\partial\theta_i}\frac{\partial log\pi(a;s,\theta)}{\partial\theta_j}]
$$
再根据$$\theta=\theta+d$$进行策略网络参数的更新.

<br/>

| [Index](./) |  [Previous](15-trpo) |  [Next](17-reward)| 
