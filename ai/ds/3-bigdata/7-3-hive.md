---
layout: post
title: Hive
---

本节介绍 Hive。它能在 Hadoop 上支持对大数据的 SQL 查询。这是因为 SQL 历史悠久，是数据科学最基本的工具，很多人对它都非常熟悉，所以，在大数据的各种系统中，如 Hive、Spark 都对它提供了支持。

我们写一个 SQL 交给 Hive 去运行。SQL 语句中有 Select，Where 等等，Hive 会帮我们把它们分解成 Map Reduce 的查询操作。所以 Hive 是一个接口。

注意，Hive 并没有把 HDFS 里面的数据转变为表格形式存储。它并不改变 HDFS 里的数据。它只是维护了一个解释这些数据的方法。它定义了应该如何解释这些数据。然后，在把 HDFS 里的数据读出来之后，它对数据做个翻译。它只读，而不去改 HDFS 里的数据。

Hive 是这么定义表的格式的：

```py
CREATE TABLE ratings (
    userID INT, 
    movieID INT, 
    rating INT, 
    time INT)
ROW FORMAT DELIMTED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

LOAD DATA LOCAL INPATH '${env: HOME}/ml-100k/u.data'
OVERWRITE INTO TABLE ratings;
```

我们首先看上面代码中的 Create 语句。我们看的 Hive 在这里定义了这个表格的 Schema，即这个表的名字叫 rating，里面有四个字段。然后，这些字段，是用 Tab 键（\t) 分隔的。这就告诉了 Hive 在读 HDFS 数据的时候，应该根据这个 Schema 进行翻译。这就是 Schema on Read。因此，它只是一个壳，在读取数据时，按照指定的数据Schema，读取数据而已，真实数据的存储还是在 Hadoop 里，按 HDFS 的方式存储。

我们然后看上面代码里的 Load Data 语句。这里我们用了 local，意思是：把这个数据复制一份到 Hive 里后，本地的数据保持不变。我们一般都不想删除本地的数据，所以一般都用 local。如果我们想节省本地的磁盘空间，想把本地的空间腾出来，那么就可以不加 local 这个关键字，就真的把数据挪过去了。

最后，我们可以通过 PARTITIONED BY 来指定按照哪个字段对数据进行分区（Partition），比如按国家进行分区。把中国用户的数据放在一起，美国用户的数据放在一起。这样后面在查询的时候，就可以提高速度。

加载完数据后，我们就可以用类似 SQL 语句对数据进行查询了。Hive 的这种类似 SQL 的语言叫 HiveQL 语言。它能够提供View（视图图），并支持级联查询。这个 HiveQL 语言和一般关系数据库的 SQL 还是有略微的不同。在使用的时候，注意查询文档。

## SQL Map Reduce 实现

在大数据的环境下，要执行 SQL 操作，需要用到 Map Reduce 分布式计算模型。比如 Spark 收到我们上面举例的 SQL 语句，它会怎么用 Map Reduce 的方式工作呢？首先，因为这个 Rating 表很大很大，一台电脑存不下，所以先得对它进行分布式存储：可能前面这一万行存在一台机器上，另外一万行存在另外一台机器上。然后，它会让所有存有 Rating 表数据的机器，执行 Map 操作，就是大家都在自己存的数据里，挑出前 20 个打分最多的电影，并给出它们的打分数。最后，它会通过 Group by Key 这个 MapReduce 框架提供的功能，把某个电影在各个机器上的打分数，汇聚到一个 Reduce 机器上，进行总的打分统计。最后，它再根据这总的统计结果，排序，选出前 20 个打分最流行的电影。因此，它还是用 Map Reduce 分布式计算模型来实现的。只不过，Spark 会帮我们做，不需要我们考虑这些细节，我们看起来好像就特别简单：一行就可以搞定。其实它自己内部做了所有的这些事。

## 小结

本节介绍了一个适合大数据的数据库：Hive，它基于 Hadoop，能够提供类似 SQL 的数据库查询操作，因此就像用关系数据库那样方便。当然它也有局限，那就是当数据大的时候，运行速度慢，然后支持的功能有限，主要是“查询”功能。我们介绍它的 HiveQL 语言。它能够提供View（视图图），并支持级联查询。当然，它提供的结构化查询只是 Schema on Read，意思是，它只是一个壳，在读取数据时，按照指定的数据Schema，读取数据而已，真实数据的存储还是在 Hadoop 里，按 HDFS 的方式存储。

<br/>

|[Index](../) | [Previous](7-1-sql) | [Next](7-5-hbase) |
