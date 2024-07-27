---
layout: post
title: Flume
---

Flume 是一个能够提供缓存的“管道（Channel）”。比如我们想把系统产生的日志存到 HDFS 里，一般会用 Flume 监视日志的文件夹，由 Flume 来把更新的日志，送进 HDFS 中。Flume 刚开始是给 Hadoop 做的。和 Flume 比起来，Kafka 更通用。

Flume 在往 HDFS 中存的时候，会做一个缓存，因为如果很多零碎的日志蜂拥往 HDFS 里写的话，HDFS 可能受不了。所以 Flume 会先把这些零碎的日志缓存一下，相当于做了一个日志的聚合，积攒一些日志后，统一往 HDFS 里面写一次。这样就能减少对 HDFS 的压力。所以 Flume 特别适合监视日志的更新，然后把这些更新送给 HDFS 或者 Kafka 等。

在系统的维护工作中，日志是很重要的。大家尝试了安装 Hadoop、Spark 后是不是就体会到看日志的重要性了？很多信息，只能看日志。所以我们会看到像混沌学院的大数据职位，就要求掌握 Flume。可能是因为它的一个职责是维护系统。维护的一个很重要的工作就是看日志。

Flume 的配置类似 Kafka 的配置。它也是设置三个东西：
- Source：有各种 Source 类型，如日志文件、Kafka、HTTP
- Sink：有各种Sink类型，如 HDFS、HBase、Kafka
- Channel：这个 Channel 能干一些活，比如压缩、加密、过滤，所以它不是简单地把 Source 和 Sink 连一下。我们还可以设置 Channel 的缓存方式，是用内存还是用硬盘文件。大多数情况下，用内存就好了。

注意，Flume 和 Kafka 的区别是：Kafka 是把消息无限期地存着的，而 Flume 只是缓存。一旦Sink 已经处理了一条消息，比如一条日志已经存进 HDFS 了，它就会通知 Channel 删除该消息，然后 Flume 就会在缓存把这条日志删掉。

我们下面看两个 Flume 的实验。

第一个实验是监视一个目录，一旦目录下有新的文件，就自动存入 HDFS。

为此，我们首先设置 Source 的类型为 spooldir，并且指定要监视的目录：

    client.sources.s1.type = spooldir
    client.sources.s1.spoolDir = /tmp/flume_spooldir

这样 Flume 就会监视这个目录。

然后，我们设置 Channel 类型为 memory

    client.channels.c1.type = memory

最后，设置 Sink 为 HDFS

    client.sinks.sh1.type = hdfs 
    client.sinks.sh1.hdfs.path = /tmp/flume_avro 

所以，它的配置也是配 Source，Sink 还有 Channel。这样它就会监视 Source 目录里的文件，经过基于内存的 Channel 缓存后，存入作为 Sink 的 HDFS 中。

把这些配置文件弄完之后，我们启动 Flume 服务后，在 Source 目录下创建一个新的文件，就会发现 HDFS 里面也会有这个文件出现。

第二个实验是监视目录，把新文件送入 Kafka。为此，我们要先用 Kafka 创建一个 Topic，然后把 Flume 的 Sink 指向这个 Topic。这样配置后，启动 Flume，被监视目录下的不断出现的新文件，就会在 Kafka 里面被接收到了。

<br/>

|[Index](../) | [Previous](11-1-kafka) | [Next](11-5-flink) |
