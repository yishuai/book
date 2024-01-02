---
layout: post
title: 获取子集
---

在数据的处理中，我们经常需要取得数据的子集。下面介绍两种常用的子集：切片（Slicing）和过滤（Filtering）。

## 切片

切片就像切水果一样，我们指定要切的位置，然后从表格中，把表中的一个部分，切下来。比如，从一个 14 列的表里头挑出 4 列。

切片包括两种切法：loc 和 iloc。

如果我们知道要切的内容的 Label，我们可以用 loc 来切。比如说我们要把 Babyname 表里的第 1 行，“Name”列的 cell（格子）切出来，我们可以用 baby.loc[1,'Name']。注意，在 Python 里表示字符串，单引号和双引号都可以，所以你可以用单引号也可以用双引号。此外，注意我们用的是方括号，不是单括号。单括号意味着函数，而方括号代表子集。

如果我们要切连续的块，因为行和列都是有顺序的，所以就可以用 baby.loc[0:3,'Name:Count'] 这种写法，取连续的一块。

如果我们要取整列，那么就可以把前面的行 Label 写成一个冒号，不设定起始点，也不设定结束点，就意味着把所有的行都取出来，那就是整列。比如 baby.loc[:,'Name']。这样取出来的列，是 Pandas 里很特别的一个数据结构：Series。注意，Series 和 DataFrame 是不同的，它们的函数有些一样，有些又不一样，这经常造成一点困扰，大家稍微注意一下。

因为取整列的操作太频繁了，所以我们可以缩写成为 baby['Count']。如果要切几列，就用列名的 list。这个 list 里带上你要的这些列的名字，我们就给它切出来了，比如 baby[['Name','Count']]。这就是 loc。注意 loc 需要的是 Label。

如果我们知道要切的内容的位置，我们可以用 iloc。它给的是位置编号。比如 iloc[0:3,0:2]。

## Filtering

Filtering 是过滤。我们写一个布尔表达式，比如 baby['Year'] == 2020，它就会把 baby['Year'] 这一列，每个数都跟 2020 比一下，是的话就 yes，就是 1，否的话就是 no，就是 0。然后用它作为行 Label，后面带个冒号，表示整行，就能把 2020 年的记录都挑出来，如 baby.loc[baby['Year'] == 2020,:]。当然，也可以简写为 baby[baby['Year'] == 2020]。

我们经常会通过 Filter 滤出我们感兴趣的记录，从而减少后续处理的数据量。比如我们可以把 2020 年的所有 baby 的行挑出来以后，我们可以用 sort_value 函数，按 Count 这一列的值（value）进行排序（Sort）。通过设定 ascending 为 false，我们就可以做降序排序。这样就把 count 最多，也就是最流行的名字排到了第一位。然后 head(7) 就能显示 2020 年最流行的前 7 名是哪几个名字了。代码如下图所示：

```py
(baby_name[baby['Year'] == 2020]
    .sort_value('Count', ascending = False)
    .head(7)
)
```

我们请大家思考一下如何研究下面的问题：我们发现 Luna 这个女孩的名字在 2000 年以前还不存在，没有谁起名字叫 Luna 的，但现在特别流行。我们想请大家分析一下，Luna 什么时候变流行的。大家想想，我们应该怎么 filtering？

我们首先看我们的目的：为了研究 Luna 的流行度随时间的变化，我们想要画一个图，是 Luna 的流行度随着时间变化的图。所以我们想得到一张表，这张表有一列是年份，另一列是 Luna 的人数，对吧？

所以我们是不是对这个表的 'Name' 做 Filtering，要 Name == Luna，就得到这张表了？但我们要找女孩子，万一有男孩子叫 Luna 的呢？因此，我们再加一个条件：sex == female。这就得到我们想要的记录了。所以我们，首先 baby name == Luna，给结果存到 Luna 里，然后在 Luna 里，把 female 的 Luna 挑出来，还是放到 Luna 里，然后在 Luna 里面切出两列：一列是count，一列是year，放到 Luna 里，下面我们就 plot Luna。你看真的是这样的：2000 年以前，没人叫 Luna 的，现在 8000 多个人叫。画其实挺好画的。px.line，画 Luna，x 轴是这个 Year，y 轴是 count，就能画出来。代码如下：

```py
luna = baby[baby['Name'] == 'Luna']
luna = luna[luna['Sex'] == 'F']
luna = luna[['Count', 'Year']]
px.line(luna, x='Year', y='Count',
          width=350, height=250)
```

## Query

Pandas 还提供一个 query 函数也可以做 Filtering。写起来挺漂亮的，比如 baby.query('Name' == 'Siri').query('Sex' == 'Female')。

为了突出显示某一个时间点，有时候我们需要加一根垂直线，这时我们可以用 add_vline 函数。v 就是 vertical，垂直的意思。然后指定它的 x 轴的位置即可。我们也可以设定这个线的颜色等于红线，是虚线，线宽 4，透明度 0.7。如下面的代码所示。

```py
siri = (baby.query('Name' == 'Siri').query('Sex' == 'Female'))
px.line(siri, x='Name', y='Count')
px.add_vline(x=2011, line_color='red', line_dash='dashdot', line_width=4, opacity=0.7)
```

上面的代码最后会画出 ‘Siri’ 这个名字的流行度随时间的变化，然后在 2011 年处画一根垂直线。画出来之后，我们就会发现，Siri 这个名字在 2011 年之前还有人取，后面就没人取了，为什么呢？因为苹果手机在这一年，用了 Siri 这个名字做它的语音助手的名字。大家会发现 2011 年处的垂直线，清楚地帮助我们表达了我们想表达的，就是 2011 年发生了特别是事件。这就是可视化的秘诀：要传递你想表达的信息。然后这个垂直线用了红色、虚线、宽度是4，而且还半透明，这样就即突出，又不干扰原图，读者就会觉得你很用心，会对你刮目相看。所以要用心，学习这些方法。

<br/>

|[Index](../) | [Previous](3-3-pandas) | [Next](3-7-aggre) |
