---
layout: post
title: 常数模型和损失函数
---

本节学习观察数据分布，并用简单的常数模型来描述它，同时提出Loss 函数的概念。Loss 函数的概念是模型学习的基石。我们要好好理解它。

大家等公交车，是不是老觉得要等好久？那么，公交车晚点时间的分布到底是怎么样的呢？我们可以从北京市交管局查询到公交车的晚点时间数据，以此回答这个问题。

假设北京市交管局给我们一个这样的数据：车的计划到达时间，
它的实际到达时间。我们根据这两个数据，就可以算出它的晚点时间。

我们画出它的直方图，观察它的分布。一般来说，观察数据的第一步，就是画直方图。直方图会统计每一个 Bin（区间）里面的值出现的次数。用 Python 代码的话，代码如下：

```py
times = pd.read_csv('data/seattle_bus_times_NC.csv')
fig = px.histogram(times, x='minutes_late',
      width=450, height=250)
fig.update_xaxes(range=[-12, 60],
      title_text='Minutes late')
```

我们观察图，会发现晚点时间的分布有点像均值为 0 的高斯分布，但是长尾的，即：有少量延时很长的车次。

我们然后可以计算它的均值、中值和 Mode 值（就是出现次数最多的值）。

```py
print(f"mean:    {times['minutes_late'].mean():.2f} mins late")
print(f"median:  {times['minutes_late'].median():.2f} mins late")
print(f"mode:    {0:.2f} mins late")

mean:    1.92 mins late
median:  0.74 mins late
mode:    0.00 mins late
```

那么，均值、中值和 Mode 值中，哪个值最能代表晚点时间的分布呢？我们把用一个值来作为数据的代表，成为“常数模型”。

为了量化地评估模型的性能，我们引入 Loss 函数。Loss 函数汇总所有样本的真实值和它的模型值之间的差别。因此，通过它，可以客观地评估模型是否真实反映了实际数据的情况。

常见的 Loss 函数包括平均绝对误差（MAE）和均方误差（MSE）。有了 Loss 函数，我们就可以调节模型参数，比如“常数模型”的代表值，

我们可以通过尝试（Trial and Error）各种不同的“常数”，计算它们的 Loss 函数，然后选择 Loss 函数最小时的“常数”，作为最佳的常数模型。我们也可以通过各种优化的方法，比如梯度下降，找到令 Loss 函数最小的模型参数。当然，如果 Loss 函数足够简单，我们也可以用高等数学的方法，直接计算出最佳参数。比如，我们可以证明，如果选 MAE 作为 Loss 函数，最后优化下来，最佳值就是中值；而如果选 MSE 作为 Loss 函数，最后优化下来，最佳值就是均值。

选择什么样的 Loss 函数的，取决于我们的关注点。比如，司机愿意选什么 Loss？也许是 MAE，因为晚点对他的影响可能是线性的，比如：相对于晚点 1 分钟，晚点 3 分钟带来的 Loss 可能是 3 倍；但对于乘客来说呢？他会选什么 Loss？也许是 MSE，因为晚点对他的影响可能是非线性的，比如：相对于晚点 1 分钟，晚点 3 分钟带来的 Loss 可能是 9 倍，因为等 1 分钟可能还能忍受，但等 3 分钟真的太让人焦虑了，更不用说等 10 分钟了。那乘客一定崩溃了。所以，乘客可能会选择 MSE 作为 Loss 函数。所以，对于乘客来说，我们在上面计算的平均晚点时间，即 1.92 分钟，可能是最能代表他们的感受的“常数模型”。

Loss 函数也可以定制。比如说，如果这个公交车设计的特别好，他如果到早了，就在公交车站等着，不会走，等到计划的发车时间再走。那这时的 Loss 应怎么算？如果晚点超过三分钟，我们就要投诉，那这个 Loss 应该怎么算？这些都可以由我们来设计。

当 Loss 函数设完了以后，我们就可以通过优化，得到最优的模型参数，让 Loss 最小。

<br/>

|[Index](../) | [Previous](13-5-simulation) | [Next](13-9-bus)|

