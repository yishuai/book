---
layout: post
title: 大数据的数据传输
---

本节介绍数据在大数据系统中如何传递。具体介绍三个工具，并进行实验：

- Kafka：它能够提供基于“Publish-Subscription”的消息传递机制。它在大数据系统中有广泛的应用

- Flume：它为Hadoop 提供数据，比如：把日志传输到HDFS中。它会缓存一下，对直接进入HDFS的流量进行控制，防止对HDFS过分频繁的操作

- Flink：一种功能强大的“流数据”的处理平台，在金融领域有广泛的应用。它以逐“事件”的方式处理流数据

我们最后完成一个综合实验，能够监视日志目录，将其更新的内容，通过Flume 送入 Kafka，然后进入 Flink 进行流式处理，进行统计，最后结果存入 MySQL。

<br/>

|[Index](../) | [Previous](9-5-resource) | [Next](11-1-kafka)|
