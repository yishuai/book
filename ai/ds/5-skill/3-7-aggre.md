---
layout: post
title: 聚合和变换
---

## 简单聚合

我们经常要对数据做合并，比如，做市场销售，每天一行销售记录，然后你想要统计一下这一周的总销售量，这就是合并求和。用 Python 的语法是：baby['Count'].sum()，就求和了。

## 分组聚合

分组聚合能够根据数据的特征对其进行分组，然后进行聚合。我们下面用一个例子来说明。

我们下面拿它来分析出生率随时间的变化。具体来说，我们想得到这样一张表：每一行是一年的出生的人数。因此，我们需要把 Baby 表里，Year 相同的行的 Count 加起来。为此，我们可以用 Group by 来实现。大家说，我要对什么做 Group 呢？是不是按 Year 来做 group？比如，我把 2000 年的行，都分到一个 group 里，然后对它们的 count 求和，是不是就得到了 2000 年的出生人数了？

为此，Python 代码就是 baby.groupby('Year')['Count'].sum()。注意，groupby 是个函数，所以它后面是单括号。然后 Count 是用方括号，因为这是 Slicing，即把 Count 这一列挑出来，然后对它们做求和（sum）。

这样得到的结果，是一个 Series。它的 index 是 Year。大家注意，Year 不是一列，而是它的 index。如果要画图的话，我们需要有一列是 Year，所以我们用 reset_index() 把 Year 的 index reset 为一列。这样的话，这个 series 就变成一个 dataframe 了，其中 Year 变成一列。因此，我们就有了两列，一列是 Year，一列是总数。这样，我们就可以用它们画图了。

类似的，我们也可以对多列进行分组聚合。比如，我们拿 Year 和 Sex，来做 group by，然后对 Count 求和，就得到一个两级 index 的 Series。我们用 to_frame() 函数把它转变成一个 dataframe，然后 reset index，它就有三列了：第一列是 year，第二列是 sex，最后一列是总数，这样咱们就求出来了每一年的每一种性别的出生人数，比如 2020 年男生有多少，2020 年女生有多少，2021 年男生多少个，2021 年女生有多少个，等等。

除了求和，我们还有其它的聚合函数，比如 max 最大值，mean 均值等。我们也可以自定义函数。这个函数的输入是一个 Series。比如写一个函数，拿着输入 Series 的最大值减去它的最小值，这就得到了它的范围。我们在对数据进行 group 以后，就可以用 .agg() 这个函数，调用它，计算每一组的范围。

再举一个自定义函数的例子。我自定义这样一个函数，先对输入 series 做一个 unique()，把每组里的元素中的冗余元素去掉，再做 len()，统计剩余的元素的个数，这就得到了这一组中元素的种类数。

## 元素个数统计

还有个特别重要的合并统计的函数叫 value_counts()。比如说我想统计 baby表的 Year 列里面一共出现了多少个不同的年份，然后每一个年出现了多少次，就可以用这个函数。注意，它还会把结果从高到低进行排序。这个函数特别有用，因为我们通常很想知道，一列里出现过哪些值，每个值出现了多少次，最频繁出现的那个值是谁，用这个函数就搞定了。

## 宽表聚合

Pivot table 这个函数，能够按照某两列里的元素进行分组，然后对每组进行聚合，再把结果转变为一个宽表，用起来非常方便。

比如，我们指定聚合后宽表的 index 是 Year，列（column）是 sex，它就会按照 Year 和 Sex 对数据进行分组，然后把每组进行聚合，最后把结果呈现为一个：以 Year 为行，以 Sex 为列的表。比如：2020 年是一行，2021 年是一行；Male 是一列，Female 是一列。其中每个格子里的数字是聚合函数的结果，比如人数的总和。这样的话，我们就得到了不同性别的人的出生率随时间的变化，就可以分别画出它们，进行比较了。

## Join 连接多个表

在做数据分析时，常常需要关联两个表。这就可以用 join 操作。比如说有两张表，一张表是 BabyName 表，一张表是这个名字的类型表，比如这个名字是“神话”类型的。我们想把这两张表关联起来。

我们先看 inner join。如果我们把 babyName 表和 name category 表做 inner join，它会这么做：从 babyname 表的第一行往下走，对每一行的 name，都在 category 表里找它。如果找到了，就把对应的 category 行，拼到这一行的末尾。如果名字在 category 表里没有找到，name 表里这一行，就不要了。也就是说，必须要两个表里都有它，才留着它。

在 Pandas 里，inner join 是用 merge() 函数实现的。这个函数默认是 inner join。在 join 时，我们要指定两张表中各自一列，这样它才知道按照哪两列来关联。

```py
baby_name.merge(name_category, 
        left_on='Name', 
        right_on='nyt_name')
```

注意，按上面的代码 Join 后得到的表里，既有 'Name' 列，又有 'nyt_name'，而这两列的内容是完全相同的，所以，其中一列是冗余的。我们一般会做一个 Slicing，去掉一列，以简化数据。

还注意，Pandas 还提供了一个 join 的函数，但这个函数没有 merge 函数灵活，所以我们一般不用 join，而是用 merge。

我们然后看 left join。和 inner join 不同，left join 如果在 category 表中找不到的话，它会留着 name 里面的这一行，然后用 None 来填充找不到的 Category 表中的对应的列。这样的话，能保证 Name 这个表完好无缺，但这时表里就增加了 None 值了。

我们最后看 outer join。它不仅像 left join 保留 name 里的行，而且还类似地，保留 category 里的行。当然，那些没有对应关系的表项，都会填 None。它的代码如下：

```py
baby_name.merge(name_category,
        left_on='Name',
        right_on='nyt_name',
        how='outer')
```
## 示例

我们下面完成一个表格合并然后聚合的分析例子。我们想分析各种类型的名字的流行度随时间变化的情况，比如“神话”类型名字的人数随时间怎么变化。

大家说说，首先应该干什么？是不是应该首先把两个表格 Join 起来？那么，是用 left join，还是 inner join ? inner join 的话就是两个表都要有这个名字才行，而 left join 的话就是右边表（比如 Category 表）没有，左边表（比如 Name 表）中的记录也留着，但 Category 填 None。因此，如果我们最后想统计 Category 为 None 的名字的流行度，那我们是不是要做 left join ？而如果我们不关心这些名字，那就可以用 inner join 去掉这些名字，对吧？

Join 完后，我们怎么统计每种类型的名字的流行度呢？要对谁做 group 呢？对 Category 做 Group，对吧？然后还要对 Year 也做 Group，因为我们需要统计每年的每种类型的名字的人的总数。所以，这就是最后的代码（假设我们不关心没有 Category 的人名，所以我们用默认的 inner join）：

```py
baby_name.merge(name_category, left_on ='Name', right_on='nyt_name')
    .groupby(['Category', 'Year'])['Count]
    .sum()
    .reset_index()
```

然后，我们就可以用 'Category' == 'Mythology' 对它的结果进行 Filtering，然后就画出 “Mythology” 类型的名字随时间变化的流行度图了。我们也可以用子图的方式，画出各种 Category 的图。

## 变换

Apply 让我们能够对某一列的元素，进行逐个的变换。

比如，我们想用 len() 函数逐个计算 Name 列中的字符串的长度，我们就可以用 baby_name['Name'].apply(len)，它就会得到新的一列，里面是 Name 列中字符串的长度。

如果我们想提取 Name 列中字符串的首字母，我们可以用 baby_name['Name'].apply(lambda x: x[0])，它就会取出输入字符串 x 的第一个字母 x[0] 然后返回，这样咱们就取出了每一个元素的首字母了。

Apply 的缺点是，它就像我们 Map 操作似的，是挨个挨个做的，所以表的行数如果很多，那么这么逐个地做，速度很慢。因此，如果我们是做数学操作，那么就像 baby['Year'] // 10 这样直接做就行。这样的话，Pandas 会用矩阵运算的方式来计算，就会快几十倍。

## 小结

这就是 Pandas DataFrame 部分的内容。我们平常用的比较多的就是 Pandas。正是因为大家对 Pandas 特别熟悉，所以 Spark 后来也提供一套同样的 API。所以大家熟悉了 Pandas 以后，用 Spark 的 DataFrame 也会很快上手。

<br/>

|[Index](../) | [Previous](3-5-subset) | [Next](5-1-sql) |
