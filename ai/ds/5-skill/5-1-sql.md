---
layout: post
title: SQL 数据处理
---

本节介绍如何用 SQL 实现我们前面讲过的 Pandas 能够实现的常用数据处理工作，包括 Slicing、聚合、Join、变换。

## 简介

SQL 和 Pandas DataFrame 的关键不同是：Pandas DataFrame 的行有 Label，还有顺序，因此，我们可以用 loc 和 iloc 来做 Slicing。而 SQL 表格中的行没有 Label，也没有顺序。

主流的开源 SQL 系统包括 MySQL 和 PostgreSQL。我们平时听说 MySQL 可能多一些，但 PostgreSQL 功能也很强大，比如，它提供的函数就比 MySQL 的多，所以 PostgreSQL 也是非常值得学习的。此外，Python 还自带了 SQLite 数据库，方便我们使用。这样我们就不需要再去另装 MySQL 了。当然，到了大的商业环境下，还是要用 MySQL 和 PostgreSQL，因为它们有很多企业级数据库需要的功能。

我们可以用 Pandas.read_sql() 函数执行 SQL 查询。为此，我们先要通过 sqlalchemy 库的 create_engine 函数，引入数据库的文件，然后就可以写一个 SQL 语句来查询了，如下面的代码所示：

```py
import pandas as pd
import sqlalchemy
db = sqlalchemy.create_engine(
    'sqlite:///babynames.db')
query = ''' 
    SELECT *
    FROM baby;
    '''
pd.read_sql(query, db)
```

## SQL 数据处理

我们下面介绍 SQL 的各项具体数据处理功能。

首先，Slicing 列，我们通过 Select 实现。把需要的列名，写到 Select 后面就可以了。注意列名不用加引号。

其次，filtering 通过 where 实现。大家注意，这里 where 后面接的布尔表达式里的等于号，只有一个等于号，不像 Pandas 里面的布尔表达式中有两个等于号。注意这个地方容易错。它也支持“或”（OR）和“与”（AND）。

然后，排序通过 order by 实现。用 DESC 表示降序排列。

然后，简单聚合通过 SUM 函数实现，分组聚合通过 GROUP BY 实现。除了 SUM，它还有均值 AVG、计数 COUNT、最小值 MIN、最大值 MAX 等函数。在各种数据库系统中，PostgreSQL 提供的函数最多。

Join 的话，我们要清楚地写出 inner join 或者 left join，然后用 on 指定哪两列要相等。它不支持右 join，因为没有必要，我们在语句里，把两个表的顺序换一下，就好了。SQLite 甚至不支持 outer join，因为平常也不太用它。

我们下面用 SQL 来实现我们前面用 Pandas 实现过的例子：统计各名字类型的流行度随时间的变化，代码如下：

```sql
SELECT Category, Year, Sum(Count) AS Popularity
FROM baby_name INNER JOIN name_category
    ON baby_name.Name = name_category.nyt_name
GROUP BY Category, Year
ORDER BY Popularity DESC
LIMIT 10;

```

SQL 提供了各种对列进行变换的函数，比如 LENGTH(), SUBSTR() 函数可以对字符串的列进行变换。其中，LENGTH 函数取字符串的长度，SUBSTR 取字符串的子字符串。

如果有多步查询的话，可以用 WITH。它会创建一个中间表，然后在后面的 SQL 语句中就可以用这个表。如下例，我们首先对 Name 列做变换，提取其首字母，然后将其作为 Filtering 的条件：

```sql
WITH letters AS (
    SELECT *, SUBSTR(Name, 1, 1) AS Firsts
    FROM baby
  )
SELECT Firsts, Year, SUM(Count) AS Count
FROM letters
WHERE Firsts = "L"
GROUP BY Firsts, Year;
```

## 小结

总之，用 SQL 可以完成我们数据处理的常用功能，包括 Slicing、Aggregating、Join、Transform。这些功能和 Pandas 是对得上的。事实上，Pandas 是在 SQL 之后出来的，所以它实现了 SQL 的这些常用的功能。

除了上述功能，SQL 还有更多功能。事实上，在工作岗位中，几乎所有的数据处理工作都能够用 SQL 完成。随之大家的事件越来越多，就会掌握得越来越多。

<br/>

|[Index](../) | [Previous](3-7-aggre) | [Next](5-3-sql) |
