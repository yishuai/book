---
layout: post
title: Spark Submit
---

在实际工作中，我们编写完一个 Spark 程序后，能够用 Submit 的方式提交给 Spark 执行。spark-submit 是 Spark 提供的用于提交和运行 Spark 应用程序的命令行工具。我们下面来练习这种方式。

首先我们新建一个 Python 文件，在里面把代码都写好。然后呢，我们在 Terminal 里执行spark-submit，将它提交给 Spark。Spark 就完成代码中的工作。

比如我们新建了一个文件 example.py，输入以下内容

```py
        from pyspark.sql import SparkSession

        # 创建 SparkSession
        spark = SparkSession.builder.appName("example").getOrCreate()

        # 创建一个 DataFrame
        data = [("Alice", 1), ("Bob", 2), ("Cathy", 3)]
        df = spark.createDataFrame(data, ["Name", "Value"])

        # 显示 DataFrame
        df.show()

        # 停止 SparkSession
        spark.stop()
```

我们然后在 Terminal 中输入命令 spark-submit example.py。这时，屏幕上会打印出很多内容。注意观察，其中出现了下述程序运行的结果

+-----+-----+
| Name|Value|
+-----+-----+
|Alice|    1|
|  Bob|    2|
|Cathy|    3|
+-----+-----+

# 配置和选项

Submit 时，我们可以写一些配置。例如：

--master：指定集群的 URL 或者使用 local 来在本地运行。
--deploy-mode：指定是 cluster 模式还是 client 模式。
--conf：设置额外的 Spark 配置参数。

spark-submit --master local[2] example.py

这个命令指定在本地运行，并使用 2 个核心。

# Word Count 示例

我们下面再看一个单词计数的示例

```py
from pyspark import SparkContext
from operator import add

sentence = "MapReduce Map Reduce Mapper Reducer MapReduce"
data = sentence.split()
# create a new instance of Spark pipeline
sc = SparkContext()
# Turning off info messages being displayed in spark control
sc.setLogLevel("OFF")
word_count = sc.parallelize(data, 128) \
                .map(lambda word: (word, 1)) \
                .reduceByKey(add) \
                .sortByKey(True) \
                .collect()
print(word_count)
sc.stop()
```

这个程序就是一个 RDD 的程序。它首先用 parallelize 读入单词列表，然后将每个单词都 Map 为一个键值对（Word，1），然后对单词做 GroupbyKey 后，再做 add （加法）的 Reduce 操作，最后用 sortByKey 对结果进行排序，最后 collect 得到输出。

我们提交了命令后，大家观察屏幕上的输出：它会提交到 Spark的集群上，然后开始调各种资源，启动各种服务，干了一堆事。因此，当我们的数据量很大的时候，它就会在成百上千台机器上开始并行地工作。这就是 Spark 的工作过程。

<br/>

|[Index](../) | [Previous](5-experi)|
