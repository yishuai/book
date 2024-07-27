---
layout: post
title: Kafka
---

本节介绍 Kafka。大家有没有看过卡夫卡的小说？最喜欢卡夫卡的什么小说？《变形记》？《城堡》？好的。

本节我们要学习的是大数据里的 Kafka。它是大数据集群中的“数据总线”。在我们的大数据处理系统中，各种系统源源不断地产生消息，比如日志。这些消息首先汇聚到 Kafka。Kafka 会把它们存起来，然后分发给需要这些消息的服务。所以说 Kafka 是“数据总线”。但它不是真的一条线。它是一群分布式的服务器。这些服务器会存储收到的消息，然后接受其它服务的请求，提供这些消息。

Kafka 的应用场景包括：Event Streaming，比如它能够接收 Flume（一种监控日志目录的服务）、前端、后端服务器的消息，然后把这些消息发送给 Hadoop、Spark、Storm，实现实时分析。此时，这些服务器的各种消息就会源源不断地送给 Kafka。然后 Kafka 就把这些消息也源源不断地送给 Hadoop 它们，进行实时的 Streaming 处理。所以它在中间相当于一个数据总线。

Kafka 采用的是“发布 - 订阅”（Publish - Subscription）的消息传输模式。这个机制是这样子的：它有一个概念叫 Topic（话题）。一个属于这个话题的信息源，会源源不断往这个话题里面 Publish 消息，也就是把消息写进去。然后这个 Topic 的订阅者呢，就会从这个话题不断地收到新的消息。这就是它的工作方式。

但要注意，Kafka 本身是一个分布式系统。这种“发布-订阅”的消息访问机制，只是它给外部提供服务时的一个抽象。事实上，它是一个集群。这个集群会存储传入的消息，然后如果有服务订阅这些消息的话，它会再发给它们。而且，因为大数据系统的消息量特别大，比如说日志、传感器数据，都很多，所以 Kafka 集群通常也很大。

具体来说，Kafka 是一个消息发布/订阅集群。它存储“发布者”（Producer）的消息，然后	发布给想要这些消息的程序：消费者（Consumer）。Consumer 是订阅 Topic，接受消息的，而 Producer 是生产消息的，Kafka 就在中间。Kafka 把关于 Topic 的订阅等关键信息存在 Zookeeper 里。

我们下面来看 Kafka 是怎么进行消息存储的。它是一个分布式的存储系统。它把接收到的 Message 存在一个 Log 文件里头。这个 Log 文件是分区（Partition）存储的。一个 Topic 被划分为多个 Partition，分别存在不同的 Broker 的硬盘上。各个 Partition 存的数据是不重复的。它就是存的这一个个 Partition（分区）。然后，一个分区里又有多个 Segment（块）。每个 Segment 里面有Index。它能够按照这个 Index，找到具体的 Message 的位置。它就是这么存储和查找的。

Kafka 的分区机制，能够提高系统的吞吐量，并且容易扩展。一个 Topic 被划分为多个 Partition，分别存在不同的 Broker 的硬盘上。各个 Partition 存的数据是不重复的。这样的话，就跟 Spark 似的，各个分区的访问，就可以并行化。通过同时访问，提高系统的吞吐量。比如说，因为我们是一个大规模的分布式系统，很可能很多台机器同时往一个 Topic 里面写，所以，它一台服务器肯定扛不住。因此，它就做了这种分区的机制。这样也容易扩展。

Kafka 的分区是有备份的，以提高可靠性。这又和 Hadoop 类似。一个Partition在集群中有多个副本。它的复制机制是这样的：每个 Partition 有一个 Broker 作为 Leader，其它 Broker 就作为 Follower。这些 Follower 就跟着这个 Leader。Kafka 首先把消息存进 Leader，然后 Follower 从 Leader 这里再复制，进行同步。

为了提高吞吐量，Consumer 形成“组”，来读取 Topic 的消息。具体来说，系统用 ZooKeeper 存储一个 Topic 的 Consumer。Consumer 订阅了一个 Topic 后，就会被通知该 Topic 新到的消息。然后，Consumer 找 Partition 的 Leader 拉取（Pull）。多个 Consumer 组成一组。组内的 Consumers，可以访问不同的 Partition，以提高吞吐量。但一个 Partition 只能被一组内的一个 Consumer 访问，这样就不会重复读取。

比如，p0 p1 p2 p3 是 Topic A 的 Partition。c1 和 c2 形成 Consumer 组 A；c3、c4、c5、c6 形成组 B。然后，Consumer Group A 的 c1 和 c2 分工合作：c1 访问 p0、p3，而 c2 访问 p1、p2。所以 c1 和 c2 能够同时读取 Topic 里的数据。比如 c1 读 p0 的时候，c2 可以 读 p1。它们是并行的。这样读起来就快了。注意。c1 和 c2 合起来，会读完所有的 Partition。一个 Partition 也不漏。同时，c1 和 c2 也重复读一个 Partition。比如不会 c1 读 p3，c2 又读 p3。这就读重复了。这也是不行的。所以在一个 consumer 组里头，各个 consumer 是分工合作，各有各自的职责的。这就是 Kafka 的基于“组”的消费机制。

## 实验

我们下面看具体的 Kafka 的配置。

配置一个 Kafka 的 Topic，包括三部分：
- Source：源
- Sink：目的
- Connector：连接器，连接 Source 和 Sink，进行数据的复制。具体复制的时候，Kafka 会分很多 Task，让多个 Worker 执行，来分布式地做。

具体来说，我们首先注册 Topic，然后定义这个 Topic 的 Source 和Sink，就是把信源和信宿给这个 Topic 登记、绑定上。这样配好后，信源以后发消息就会发到这个 Topic，然后信宿会收到这个消息。

我们下面用三个实验来体验一下这个过程。

第一个实验有点像大家发微信似的：你在这个终端写点东西，在那个终端能看见。为此，我们首先获取 Zookeeper 和 Kafka Broker 的地址。其中，Zookeeper 会存储 Topic 的信息。然后用 Terminal 登录 Kafka Broker，运行 Kafka-topics.sh 脚本： 

```shell
 ./kafka-topics.sh --create --zookeeper 192.168.0.14:2181/kafka --partitions  1  --replication-factor  1  --topic haha
```

如上面的命令行命令所示，我们创建（create）一个 Kafka 的 Topic。这个 Topic 的名字叫 “haha”。Partition 数目为 1，副本数为 1。因为 Topic 的信息存在 ZooKeeper 里，所以我们给出 Zookeeper 的地址为 192.168.0.14:2181。

然后我们就可以查看现有的 Topic 了。我们用下面的命令，列出 Zookeeper 上现有的 Topic，因为Topic 信息是存在 Zookeeper 里的。

```shell
查看topic
bin/kafka-topics.sh --list --zookeeper 192.168.0.14:2181/kafka
```

下面就用下面的命令，创建这个 Topic 的消费者。

```shell
bin/kafka-console-consumer.sh --topic haha --bootstrap-server 192.168.0.117:9092
```

如上面的命令所示，创建 Consumer 时，需要指定Topic 是 “haha”，指定 Broker 是 192.168.0.117:9092。

然后，在另一台电脑（或者终端）上，我们就可以用下面这个命令，创建 Producer（生产者）。我们同样指定Topic 是 “haha”，指定 Broker 是 192.168.0.117:9092。

```shell
bin/kafka-console-producer.sh  --broker-list  192.168.0.117:9092  --topic haha
```

完成了上面这些配置之后，我们会在这个机器上敲一个 “Hello”，那个机器（或者终端）上，就会实时地出现 “Hello”，就像收发微信的消息似的。

总结一下，这个实验包括三步：Create topic，创建 Consumer，	创建 Producer，就可以了。然后可以验证终端间的消息传输。

第二个实验是实现文档的自动更新。有点像腾讯文档似的，当别的编辑者编辑了文档后，我们能够实时地看到更新后的文档。

和第一个实验类似，我们还是 Create topic，创建 Consumer，	创建 Producer，就可以了。只是，这个 Producer 不是 Terminal 了，而是一个文件。这个文件一旦被改了的话，Consumer 就能看见。所以这个文件是被监视的一个文件。

因此，我们要首先修改 Kafka 的配置文件connect-file-sink.properties，在里面加上

        file=/home/my_sink.txt
        topics=my_connect-test2

这样就设置好了 Consumer 为 my_sink.txt 这个文本文件，并且指定了它的 Topic。

然后修改 Kafka 的配置文件connect-file-source.properties，在里面加上

        file=/home/my_test.txt
        topic=my_connect-test2

这样就设置好了 Producer 为 my_test.txt 这个文本文件，并且指定了它的 Topic。我们可以用 vi 打开上面的这两个配置文件，进行编辑。所以 vi 大家要学会啊。

我们然后运行下面的命令，启动这个 Kafka 连接，就可以了。注意，我们在这里采用 connect-standalone 是
因为我们用一台机器（Stand Alone）即做 Consumer 又做 Producer。

```sh
./connect-standalone.sh ~/connect-standalone.properties ~/connect-file-source.properties ~/connect-file-sink.properties
```

下面，如果我们修改 Producer 的 
Source 文件 my_test.txt，比如用 echo 这个终端命令，把一句话，加到它的最后，那么 Consumer 的 Sink 文件 my_sink.txt 也会看到这一句话的改动。

<br/>

|[Index](../) | [Previous](11-0-databus) | [Next](11-3-flume) |
