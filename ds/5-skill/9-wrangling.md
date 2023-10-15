---
layout: post
title: 数据整理
---

本节介绍数据整理的技巧和方法，包括验证数据有效性，检查数据质量，修正问题，比如处理缺失值；数据变换，特征变换；数据变形，修改数据结构和粒度等。

我们用两个数据作为示例。一个是二氧化碳浓度的测量数据，一个是卫生检测的记录数据，其中包括文本。

## 数据读入

像前面介绍的，我们首先用 pathlib 库，os.path.getsize 函数，chardet.detect 函数，设置数据文件的路径，检测其大小，判断其编码。

```py
from pathlib import Path
import os
import chardet

co2_file_path = Path('data') / 'co2_mm_mlo.txt'

[os.path.getsize(co2_file_path), 
chardet.detect(co2_file_path.read_bytes())['encoding']]
```

我们然后用 pathlib 的 read_text 函数，读入文本，观察前面的几行。这是因为数据文件前面通常有一些说明文字。认真看看这些说明非常重要，有助于我们了解数据的 Scope。此外，我们需要找到真正的数据是从哪一行开始的，有没有表头行。了解了这些信息后，在后面 read csv 时可以进行相应的设定。这个代码非常简单，如下：

```py
file_path.read_text().split('\n')[:6]
```

我们然后读入 csv 文件。读的时候，我们可以设定一些参数，比如 header=None，就是这个文件第一行没有列名，就全是数据。所以，后面用 names 指定了各列的列名。然后，skiprows=72，这是因为这个文本文件的前72行是一些说明文字。我们得跳过它，别给它们当 csv 表格数据读进来。最后，sep='\s+' 是指定分割符。\s 代表空白字符，包括空格、回车、换行、Tab 键，+ 号是重复的修饰符，代表出现至少一次，上不封顶。下面是代码：

```py
co2 = pd.read_csv('data/co2_mm_mlo.txt',
        header=None,
        skiprows=72,
        sep='\s+',
        names=['Yr', 'Mo', 'DecDate',
        'Avg', 'Int', 'Trend', 'days'])
```

## 评估数据质量

读入后，我们来观察数据。

### 单变量数据质量评估

我们首先观察单个值：二氧化碳浓度、月份、每月的测量天数。

如果是时间序列数据，我们一般会画出来看看它的变化趋势。比如，在表中，二氧化碳浓度的月度平均数据值存在 Avg 列中，而 DecData 是测量月份的十进制表示。我们就可以画图看一下 Avg 随着月份变换的情况。观察后，我们可以看到 Avg 有稳定的上升趋势。

我们很可能会发现有异常值。这时就要看文档，看这个异常值是不是有特殊的含义，然后进行相应的处理。我们还可以用 Filtering，比如 co2[co2['Avg'] < 0]，把这个异常的记录找出来，看看具体是什么情况。如果它们是缺失值的话，那么可以根据对问题的理解，采用合适的方法，对它进行补齐。比如用交织的办法。

我们还可以观察它的分布。这有三种方法：

首先，我们也可以用 Pandas 函数 describe() 给出一个总体描述，包括最小值、25% 分位数、50% 分位数、75% 分位数等。这样我们也可以发现这里面确实有负值。

其次，对取值有限的值，比如月份，我们可以用 value_counts() 观察它各个取值的出现次数。比如，为了检查月份是否有缺失，我们可以用 co2['Mo'].value_counts().reindex(range(1,13)).tolist() 统计其各个值的个数。如果有很多 None 值，那么也要进行相应的处理。

最后，对各种数值，我们都可以用直方图画出它的出现频率。直方图的好处是它会自动分桶。从结果中，我们可能又会发现有的值不对，比如出现了 Day = -1 的情况。因此，又要看文档，看这个负值是不是有特殊的含义，然后进行相应的处理。

### 双变量数据质量评估

我们然后观察两个变量之间的关系。

我们首先看 Year 和 Days 的对应关系。它们是两个连续值，可以用 scatter 画散点图，观察它们的关系。

对一个离散值，一个连续值，可以用 groupby 将数据按离散值分组后，用 agg 函数，比如 mean，对连续值进行合并后，再观察它们的关系。或者用 sns.catplot 画 box 图等。

我们也可以用 strip 画一维抖动的散点图。这样我们就能观察它们的相关性。

```py
fig = px.strip(
    ins_and_num_vios,
    x=jitter(ins_and_num_vios['num_vio'], amt=0.5),
    y='score',
    width=400, height=250)
```

我们然后观察它们的分布。

对两个离散值，可以用 crosstab 统计它们各种数值组合的数目，看是不是分布不均匀，有的组合缺失严重。

### 评估问题

通过上面这些观察，我们要回答以下四个问题：

- 数据的 Scope，即数据的 Access Frame 是否符合拟研究的目标人群
- 测量和数值是否合理
- 变量间相关的特征如何，是否合理
- 哪些特征对未来的分析有用

## 缺失值处理

对缺失值的处理非常重要。

一列中缺失值如果太多，那么这一列可能就用处不大了，可以去掉。用 isnull 函数可以检查一个值是不是缺失值。因此，可以用类似 co2['Mo'].isnull().sum() 的代码统计一列中的缺失值的总数。

对缺失值可以进行补全（Imputation）。补全要符合逻辑，比如，如果一个同学是满分的话，那么，我们可以给他的错误数赋为 0。代码是 student.loc[student['score'] == 100, 'num_error'] = 0。又比如如果缺失的是经纬度，但逻辑上这个位置属于北京，那么就要用北京的经纬度来补。常用的补全方法还有均值、交织、随机。

## 特征变换

### 时间戳转换

我们首先介绍如何转换时间戳。对时间，一般通过 to_datatime 转换成 timestamp 格式。一旦转成 timestamp 格式，就可以通过 .dt.year 取它的年, .dt.dayofweek 取它是周几，非常方便。然后我们就利用这些信息来进一步观察数据，比如观察周末的数据量。

```py
date： 20160513
insp['date'].dtype
    int64

date_format = '%Y%m%d'
insp_dates = pd.to_datetime(insp['date'], 
    format=date_format)

insp_dates[:1]
0   2016-05-13
Name: date, dtype: datetime64[ns]

insp = insp.assign(timestamp=insp_dates,
           dow=insp_dates.dt.dayofweek)

fig = px.bar(insp['dow'].value_counts().reset_index(),
        x='dow', y='count',
        labels={'dow':'Inspection day'},
        height=250, width=350)

day = ['Mon','Tue','Wed','Thu','Fri','Sat','Sun']
fig.update_xaxes(ticktext=day, 
        tickvals=np.arange(0, 7, 1))

fig.update_layout(showlegend=False)
```

### 提取文本特征

Pandas DataFrame 通过 .str 让我们可以访问字符串值的内容。我们然后可以调用一些函数。比如，.str.contain() 可以检查它是否包含某些内容，比如字符串"high risk"、'clean|sanit'。

通过这个方面，我们就可以检查表格里的文本信息，从中提取特征，完成需要的特征工程工作，如下面的代码：

```py
def make_vio_categories(vio):

    def has(term):
        return vio['description'].str.contains(term)

    return vio[['business_id', 'timestamp']].assign(
        high_risk        = has(r"high risk"),
        clean            = has(r"clean|sanit"),
        food_surface     = (has(r"surface") & has(r"\Wfood")),
        vermin           = has(r"vermin"),
        storage          = has(r"thaw|cool|therm|storage"),
)

vio_ctg = vio2016.pipe(make_vio_categories)
vio_ctg
```

## 表结构调整

常用的表的格式有两种：宽表和长表。宽表的列数很多，每一行是一个 case，每一列是一个 feature。长表呢，只有三列，分别对应宽表的 Index、Feature Name 和 Value。宽表适合机器学习，而长表适合做数据分析，如统计和可视化。

我们可以用 melt 把宽表转换为长表，指定转换后长表的三个列名即可，分别是 id_vars (Index 列名。注意可以是多个 Feature 组成多级 Index)，var_name（ Feature Name 列名），value_name（表内容的列名）。

我们也可以用 pivot_table 把长表变为宽表，指定要转换的行的范围，要转换的三列（Index、Feature Name 和 Value）即可，分别放到 index，columns，values 里。

## 小结

这就是 Dataframe 的数据整理，包括观察数据质量、缺失值填充、特征变换、表格格式转换等。通过不断实践，我们就会对它们越来越熟悉。

在数据整理中，最重要的是保持对数据的好奇，这样我们就会潜入得越来越深。在这个过程中，我们要判断发现的问题的严重程度，是大问题还是小问题；我们逐渐理解和解释不同寻常的现象，发现数据的限制。

<br/>

|[Index](../) | [Previous](7-file) | [Next](11-eda) |
