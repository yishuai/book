---
layout: post
title: 练习
---

# Hadoop 文件准备

因为 Spark 会从 Hadoop 的 /usr/cloudide 中读取文件，所以我们要首先在 Hadoop 里建立这个目录，然后把 Spark 程序需要读取的文件，上传到 Hadoop 里。

hdfs dfs -mkdir /user/cloudide
hdfs dfs -put SacramentocrimeJanuary2006.csv /user/cloudide/

注意，我们服务器上要有 SacramentocrimeJanuary2006.csv 这个文件。

# PySpark 编程练习

我们然后在 Terminal 中输入 pyspark，进入其操作界面，进行 Python 编程练习

在 PySpark 里，已经有两个变量我们可以使用了。一个是 sc，它代表了 Spark context。另一个是 spark，它代表了 SparkSession.

我们也可以用下面的语句，自己定义 spark

from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("example").getOrCreate()

我们然后就可以用 spark 进行编程。比如

data = [("Alice", 1), ("Bob", 2), ("Cathy", 3)]
df = spark.createDataFrame(data, ["Name", "Value"])
df.show()

或者读取 Hadoop 中 /user/cloudide/ 目录下的文件

df = spark.read.csv('SacramentocrimeJanuary2006.csv')

df.show(n=10)

# Jupyter Notebook 编程练习

我们也可以按照前面介绍过的方法，在 Terminal 中安装 Jupyter Notebook，然后在 Jupyter Notebook 中进行练习。比如完成 BIOS 下面的 C 系列 Spark Notebook 练习。

<br/>

|[Index](../) | [Previous](3-install) | [Next](6-submit)|