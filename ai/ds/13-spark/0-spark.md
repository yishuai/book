---
layout: post
title: Spark
---

本节介绍 Spark。它是目前大数据处理采用的最主要的工具，广泛应用于银行、电信、互联网公司，非常值得学习。

我们首先介绍为什么 Spark 的 Map Reduce 计算比 Hadoop 的快？这主要是因为 Spark 使用内存，而 Hadoop 使用硬盘。一般来说，内存访问比磁盘访问要快上百倍。我们也介绍 Spark 的生态。它的生态非常强大，包括 Streaming 流式处理，MLlib 机器学习库，GraphX 图算法库等。

我们然后介绍 Spark 计算的核心数据元素：RDD（弹性分布式数据集）。我们首先介绍它的 Lineage （血统）机制、Partition 分区存储，然后介绍它的各种操作，包括创建、变换、控制、行动。我们特别介绍 RDD 的 Lazy 评估机制，这让 Spark 可以自动优化操作的执行计划，加快处理速度。最后介绍两个 RDD 编程的实际示例。通过理解 RDD，我们对 Spark 的内部机制就非常理解了。

我们然后介绍如何利用 Spark 进行表格数据的处理。为此，Spark 提供了DataFrame 和 SQL 两种方式。我们首先介绍 DataFrame 的基本概念，然后介绍两个 DataFrame 的处理代码。从中我们可以体会到，DataFrame 用起来确实方便。

<br/>

|[Index](../) | [Next](1-intro) |
