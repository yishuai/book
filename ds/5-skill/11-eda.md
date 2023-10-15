---
layout: post
title: 探索式数据分析
---

探索式数据分析（EDA）是一个发现的过程，不断提出问题，主动分析，通过画图，揭示数据的特征，发现数据中的模式，特别是意外的模式，获得对问题的理解，寻找问题的答案。可视化是 EDA 的关键。学习 EDA 的方法是学习案例，从中理解别人的思维过程。

## 特征类型

根据要探索的特征是定量特征还是定性特征，我们有不同的探索方法。比如，对于定量特征，我们可以画直方图、box 图、Rug 图、KDE 概率密度图、小提琴图。对于定性的特征来说，我们就可以画 bar 图、饼图等。而如果要分析两个特征之间的相关性，我们就可以画散点图等。此外，我们也可以通过均值、百分位数、最大、最小值等，对它们的分布进行观察。

因此，第一步是确定数据的特征的类型。我们可以用 Pandas 的 info 函数获得数据类型以及其它的很多信息。

我们然后观察特征的取值情况，并进行必要的变换。需要的话，可以折叠一些类型，或把数字特征转化为有顺序的定性特征。比如：

```py
kids = {1:"high", 2:"medium", 3:"low"}
dogs = dogs.assign(kids=dogs['children'].replace(kids))

with_play = dogs.assign(
    play=(dogs["group"] == "toy") |
       (dogs["group"] == "non-sporting"))
```

## 在分布中寻找什么

那么，我们观察什么呢？主要是观察“模式”。我们的人的眼睛是很敏感的，对“稠密”、“趋势”都非常敏感。我们要充分利用人眼的这个能力，获得对数据模式的启发。

我们可以画 KDE 密度曲线，然后观察它的模式：

```py
from scipy.stats import gaussian_kde

new_x = dogs['longevity'].dropna()

xs = np.linspace(min(new_x), max(new_x), 100)

bandwidth = 0.2
ys = gaussian_kde(new_x, bandwidth)(xs)

f2 = go.Figure(go.Scatter(x=xs, y=ys))
```

有哪些模式呢？如 Mode（最高点）、Skew（偏斜）、Tail（尾巴）、Gap（分割）等。

做直方图的时候，我们可以设定 Bin 的宽度。默认的它会给你均匀的分，但是有的时候我们想把一些 Bin 设宽一点，否则里面没值，就不平滑。

```py
bins = [-0.5, 0.5, 1.5, 2.5, 3.5, 9.5]
g = sns.histplot(data=dogs, x="ailments",
        bins=bins, stat="density")
g.set(xlabel='Number of ailments', ylabel='density')
```

## 在关系中寻找什么

发现两个特征间的关系，也很重要。

最常用的方法是散点图。人的眼睛是最好的观察相关性的工具，一眼就看出来了。

一个定量，一个定性的话呢。比如 Dog 有三个 Size：medium、small、large，然后我们想看 Size 和 Height 的关系。那我们就干脆就画三个根线呗。代码是 ax = sns.kdeplot(data=dogs, x='height', hue='size')。

我们也可以画不同 Size 的 Height 的 Box 图。Box 图中间的盒子是从 25 分位数到 75 分位数。中间的线，是它的中值。两边的须子有不同的设置。从 Box 图中，我们能看出来它是不是对称的。代码是 go.Box(x=dogs["size"], y=dogs["height"])。从 Box 图中，我们可以比较不同 Size 的 Height 分布的位置和分布的集中度（Spread）。

我们也可以画不同 Size 的 Height 的小提琴图。代码是 go.Violin(x=dogs["size"], y=dogs["height"]。小提琴图相当于把 KDE 的概率密度曲线画出来，因此它提供了更多的信息。但是，因为它做了平滑，所以可能并不准确。

## 三变量关系图

对定性特征，我们可以充分利用多面图（Facet，即一张图中有几个子图），用子图来区分一个定性特征的不同值，通过设置 facet_col 就可以了。

如果是三个定量，就得把其中一个定量特征做离散化，再做多面图。

在探索中注意辛普森悖论的出现，注意固定“控制变量”，对数据做分解可视化，观察子集中的变量关系。

## 探索指南

在 EDA 中我们可以关注以下问题：值的分布，特征之间的关系，值的分布在不同的子组中是否相同，是否有让人吃惊的模式。

探索中，最重要的是带着好奇的态度去观察，常问自己 What Next ？ So What ？以继续探索下去。

注意阅读文献、和专家讨论，了解背景知识很重要。

## 示例：房屋销售价格

作为一个例子，我们探索一下房价数据。

首先观察房价的分布。

```py
pd.set_option('display.float_format', '{:.2f}'.format)

percs = [0, 25, 50, 75, 100]
prices = np.percentile(sfh_df['price'], percs, method='lower')

pd.DataFrame({'price': prices}, index=percs)

percs = [95, 97, 98, 99, 99.5, 99.9]
prices = np.percentile(sfh_df['price'], 
    percs, method='lower')
pd.DataFrame({'price': prices}, index=percs)
```

发现 99.9% 的房价都在 4 M 以下，因此，选择这些房子。

画出房价的直方图，发现偏斜。对房价做 Log 变换。

问问题：What Next ？趋势？影响因素？

分析卧室数的影响：首先把超过 8 的卧室数，折叠为 8。然后用 Box 图，画出卧室数和房价的关系。发现卧室多的，房价要高。

```py
eight_up = sfh.loc[sfh['br'] >= 8, 'br'].unique()
sfh['new_br'] = sfh['br'].replace(eight_up, 8)
```

分析城市的影响：选择几个城市的数据，用 Box 图画出房价和城市的关系。

```py
cities = ['Richmond', 'El Cerrito', 'Albany', 'Berkeley', 'Walnut Creek', 'Lamorinda', 'Piedmont']

px.box(sfh.query('city in @cities'), 
      x='city', y='price', 
      log_y=True, width=450, height=250, 
      labels={'city':'', 'price':'Sale price (USD)'})
```

分析不同城市内，房子面积和单价的关系。用多面图。每个城市一个面。

发现很多模式
- 分布是偏斜的
- 单价随着面积增长而下降
- 不同城市房价不同

这些模式将有助于我们理解房价，建立房价模型。

<br/>

|[Index](../) | [Previous](9-wrangling) | [Next](13-vis) |
