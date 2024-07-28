---
layout: post
title: Spark 安装
---

我们介绍 Spark 的安装。和 Hadoop 的安装类似，也是先下载、解压，然后设置环境变量。

在安装 Spark 之前，要单独安装 hadoop 吗？不需要。Spark 自带了 Hadoop 的一部分必要组件，使得你能够在本地运行 Spark 而无需额外安装 Hadoop。

# 下载

获得最新的 Spark 程序下载地址
- 网址：https://spark.apache.org/downloads.html
- 保持 Choose 选择框中的默认选项
- 点击 Download 后面的链接，比如 spark-3.5.1-bin-hadoop3.tgz
- 在打开的网页中，复制下载地址，比如 https://dlcdn.apache.org/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz

注意，上面下载的 Spark 的预编译二进制文件，是包括了 Hadoop。按照你的需要，也可以选择不包括 Hadoop 的。

下载，解压，并进行目录移动。下面是示例，请根据最新的 spark 版本号，修改具体的内容
- wget https://dlcdn.apache.org/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz
- tar -xvf *.tgz
- sudo mv spark-3.5.1-bin-hadoop3 /opt/spark

# 设置环境变量

编辑 shell 配置文件

修改 .zshrc，加入以下环境变量
- export SPARK_HOME=/opt/spark
- export PATH=$SPARK_HOME/bin:$PATH
- export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH

在 Terminal 中执行 source ~/.zshrc，使这些更改生效

# 安装 pyspark

我们接着安装 PySpark

在 Terminal 中执行
- pip install pyspark

# 运行 pyspark

在 Terminal 输入 pyspark

然后进入 Networking，点击 4040 端口后的 Address，观看 PySpark 管理界面

# 在 pyspark 中输入代码

from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("example").getOrCreate()
data = [("Alice", 1), ("Bob", 2), ("Cathy", 3)]
df = spark.createDataFrame(data, ["Name", "Value"])
df.show()

如果能够显示表中的内容，那么就说明我们已经可以进行 Spark 编程了。

<br/>

|[Index](../) | [Previous](17-mrlab)| [Next](5-experi)|