---
layout: post
title: 案例：空气质量测量有多准确
---

本节练习一个完整的数据科学 Lifecycle 过程，包括我们学过的各种内容，包括：1）问题和数据 Scope 分析，2）数据整理，3）EDA 、数据可视化，并创建模型。

## 问题和数据 Scope 分析

我们的问题是，建立家用空气质量测量仪的校准模型。因此，我们需要收集家用仪器的测量数据，即 PurpleAir 数据，用这些数据作为输入，训练一个模型，获得和高质量测量仪器的输出（即 AQS 传感器数据）相同的结果。为此，我们首先查找位置相同的 PurpleAir 传感器和 AQS 传感器，然后整理它们的数据，进行探索性分析，分析它们的分布和相关性，确定要采用的模型，最终训练模型。

## 查找位置相同的传感器

### 读入数据

我们首先查找位置相同的 PurpleAir 传感器和 AQS 传感器。我们读入数据。

对于 AQS 数据，我们首先 ls -lLh 观察文件的基本情况，如 Size，然后 read_csv 读入数据，然后观察获得的数据 Dataframe 的 shape 和 columns。我们然后用 value_counts 观察每一列数据中的值的基本情况，确定数据的“主键”。需要的话，去除数据中的冗余。下面是去除冗余的代码：

```py
def rollup_dup_sites(df):
    return (
        df.groupby('AQS_Site_ID')
        .first()
        .reset_index()
    )

aqs_sites = (aqs_sites_full
    .pipe(rollup_dup_sites))
aqs_sites.shape
```

对于 PurpleAir 传感器数据，因为它是 Json 格式，所以首先用 head 和 cut 观察它的前几行的前几列的数据。命令行代码如下：

```sh
head data/list_of_purpleair_sensors.json | cut -c 1-60
```

然后用 Python 的 json 库进行读入，代码如下：

```py
import json

with open('data/list_of_purpleair_sensors.json') as f:
    pa_json = json.load(f)

list(pa_json.keys())
['version', 'fields', 'data', 'count']

pa_sites_full = pd.DataFrame(
    pa_json['data'], columns=pa_json['fields'])
pa_sites_full.head()
```

和 AQS 数据类似，我们然后用 value_counts 统计其每一列的值的情况，确定“主键”。

### 查找位置相同的传感器

我们然后用 SQL 来查找相同的传感器。我们当然也可以用 Python 来完成这一工作，但是在这里，我们可以用这个例子来说明 SQL 功能的强大。我们首先把 Pandas Dataframe 读入 sqlite SQL 数据库。下面是 Python 代码：

```py
import sqlalchemy

db = sqlalchemy.create_engine('sqlite://')

aqs_sites.to_sql(name='aqs', con=db, index=False)
pa_sites.to_sql(name='pa', con=db, index=False)
```

我们然后写作 SQL 查询语句，完成相同位置传感器的查找。下面是 Python 代码。注意其中的 offset_in_lat 和 offset_in_lon 是 Python 变量，存储的是我们能够容忍的经纬度差别。

```py
query = f'''
  SELECT
    aqs.site_id AS aqs_id,
    pa.id AS pa_id,
    pa.label AS pa_label,
    aqs.lat AS aqs_lat,
    aqs.lon AS aqs_lon,
    pa.lat AS pa_lat,
    pa.lon AS pa_lon
  FROM aqs JOIN pa
    ON  pa.lat - {offset_in_lat} <= aqs.lat
    AND aqs.lat <= pa.lat + {offset_in_lat}
    AND pa.lon - {offset_in_lon} <= aqs.lon
    AND aqs.lon <= pa.lon + {offset_in_lon}
  '''
  matched = pd.read_sql(query, db)
```

## 数据整理

获得了能够支持我们问题研究的原始数据后，我们开始整理数据，这包括：1）检查并纠正数据的粒度；2）简化表；3）检查数据质量；4）数据变换。

### 整理和清理 AQS 传感器数据

我们首先发现 AQS 数据里每一天都有 12 行数据。我们观察这 12 行数据的范围。代码如下：

```py
(aqs_full.groupby('date_local')['arithmetic_mean']
  .agg(np.ptp) # np.ptp computes max() - min()
  .value_counts()
)
```

我们发现这些值都是相同的，所有，我们就选第一个就行。这就相当于删除了冗余的数据。

我们然后用 to_datetime 转换日期列为 Pandas 的 Timestamp 格式。函数如下：

```py
def parse_dates(df):
      date_format = '%Y-%m-%d'
      timestamps = pd.to_datetime(df['date_local'], 
          format=date_format)
      return df.assign(date_local=timestamps)
```

转换后，我们接着分析时间相关的特征就很方便了，比如，通过 max - min 就可以得到日期的范围。这个范围也是 Timestamp 格式，因此通过 .days 就能获得间隔是多少天。代码如下：

```py
date_range = aqs['date_local'].max() 
                - aqs['date_local'].min()
date_range.days
```

我们然后检查数据质量。我们画图，就会发现有几天 PM2.5 非常高。我们想：这几天肯定有特别的事发生啊，比如：那几天是森林大火。那么，我们要研究的问题，包括这几天的情况么？这就是数据 Scope 的分析了。如果我们想建立的模型，是专门针对平时的话，那么，我们可以不预测它，对吧？那就可以把它们去掉。但是，如果我们想建立的模型，是包括这些天的，那么，我们就得预测它。所以，根据大家的需求不一样，我们可以选择不同的 Access Frame。

### 整理 PurpleAir 传感器数据

我们首先读入 PurpleAir 传感器的测量数据。因为这些数据包括一个目录下的很多 csv 文件，所以，我们用 PathLib 来读取它们。Pyton 代码如下：

```py
from pathlib import Path

data_folder = Path('data/purpleair_AMTS')
pa_csvs = sorted(data_folder.glob('*.csv'))
```

因为 AQS 数据用的是当地时间，PurpleAir 用的是 UTC 时间，为了让它们一致，我们把 PurpleAir 时间，转换为当地时间。代码如下：

```py
def convert_tz(pa):
      return pa.tz_convert('US/Pacific')
```

然后我们就可以通过 resample 来统计每一天的数据量。代码如下：

```py
per_day = (pa.resample('D')
       .size()
       .rename('records_per_day')
       .to_frame()
  )

px.line(per_day, x=per_day.index, y='records_per_day', 
    labels={'timestamp':'Date', 
        'records_per_day':'Records per day'},
    width=550, height=250,)
```

从图中我们发现每天的数据量不同，有些天的数据达到了 2000 多，但按照数据的说明，2分钟一个值的话，应该是 720个，所以我们初步判断数据中是有冗余的。我们选择数据有 2000 多的一天，进行观察。代码是：pa.loc['2019-01-01'].index.value_counts()，发现确实有冗余。我们就用 df[~df.index.duplicated()] 这个代码来消除冗余。

从图中我们也发现有些天少数据。那么，要不要选一段数据足够多的时间？这又是一个数据的 Access Frame 的问题。我们决定要选择特定时间段，而是一天的测量数据量足够的数据。基于这些数据，我们然后计算每日的平均值。代码如下：

```py
cutoff_date = pd.Timestamp('2019-05-30', 
                  tz='US/Pacific')

def has_enough_readings(one_day):
    [n] = one_day
    date = one_day.name
    return (n >= needed_measurements_80s
            if date <= cutoff_date
            else n >= needed_measurements_120s)

def compute_daily_avgs(pa):
    should_keep = (pa.resample('D')['PM25cf1']
                .size()
                .to_frame()
                .apply(has_enough_readings, 
                    axis='columns'))

    return (pa.resample('D')
            .mean()
            .loc[should_keep])

```

所以最后的数据整理的代码如下。我们完成了几项工作：1）简化表格，去掉没用的列；2）转换 Timestamp；3）删除多余的行；4）处理缺失的数据，选择有足够数据的天，并汇总每个仪器的读数，计算每天的均值。

```py
pa = (pa_full
    .pipe(drop_and_rename_cols)
    .pipe(parse_timestamps)
    .pipe(convert_tz)
    .pipe(drop_duplicate_rows)
    .pipe(compute_daily_avgs))
```

整理完后的 AQS 和 PurpleAir 数据，我们存入一个 CSV 文件，方便后面的分析。

## EDA

整理完后我们就开始探索。我们下面探索 PurpleAir 和 AQS 测量结果。探索主要是探索它们的分布及它们之间的关系。

我们首先读入数据。注意，read_csv 函数可以 parse date。代码如下：

```py
csv_file = 'data/cleaned_purpleair_aqs/
                Full24hrdataset.csv'

usecols = ['Date', 'ID', 'region', 'PM25FM', 
        'PM25cf1', 'TempC', 'RH', 'Dewpoint']

full_df = (pd.read_csv(csv_file, usecols=usecols, 
        parse_dates=['Date'])
        .dropna())

full_df.columns = ['date', 'id', 'region', 'pm25aqs',
        'pm25pa', 'temp', 'rh', 'dew']
```

我们首先比较两种传感器每周的平均值。因为 date 列采用了 Timestamp 格式，所以我们现在很方便地就能计算每周的均值。代码如下：

```py
nc4 = full_df.loc[full_df['id'] =='NC4']

ts_nc4 = (nc4.set_index('date')
    .resample('W')['pm25aqs', 'pm25pa']
    .mean()
    .reset_index()
)
```

我们然后画出它们的时间序列图和散点图，观察它们的关系。从这两张图中，我们都能感觉到它们是线性正相关的。因此，我们可以用 np.corrcoef 函数计算它们的相关系数。

## 创建模型

我们最后创建模型，来校正 PurpleAir 测量结果

基于上面的观察，我们最后构建线性回归模型。代码如下：

```py
from sklearn.linear_model import LinearRegression

AQS, PA = full_df[['pm25aqs']], full_df['pm25pa']

model = LinearRegression().fit(AQS, PA)

m, b = model.coef_[0], model.intercept_
print(f"True Air Quality Estimate 
    = {-b/m:.2} + {1/m:.2}PA") 
```

<br/>

|[Index](../) | [Previous](13-vis) | [Next](17-text) |
