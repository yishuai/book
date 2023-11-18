---
layout: post
title: ZooKeeper
---

我们前面给大家打过伏笔，各种大数据系统的很多很重要的东西都存在 ZooKeeper 里头，包括 YARN、Hbase、MapReduce、Storm、Kafka，它们都把关键信息存在 ZooKeeper 里。比如很多系统里都有一个 Master 的节点。这个节点非常重要。它负责存储关键信息，给其它节点分配工作。那么，现在哪个节点是 Master 呢？这个信息就存在 ZooKeeper 里。

因为 ZooKeeper 保管着大数据系统运行中的关键信息，所以它就一定不能崩。Zoo Keeper 这个英文单词的意思是“动物园的管理员”。大家想想，动物园管理员如果崩溃了的话，那些狮子老虎突然跑出来了，是不是很可怕？所以 ZooKeeper 是特别重要的一个角色。

为了不崩，Zookeeper 本身就是一个分布式系统。世界上有不会崩的单台主机吗？没有。那怎么办呢？只能把很多主机连起来，组成一个分布式系统。这样的话，即使有一些主机崩了，其它主机还可以接着工作。

采用这种方法，ZooKeeper 为大数据系统提供了一个允许分布式节点进行信息共享的存储空间。大数据系统可以用它来存储关键的配置信息，由它来提供共享的命名空间、分布式同步、组服务等。它具有很高的可用性（就是说极不可能崩），总是能够为大数据系统共享的信息存储空间。

作为一个分布式系统，ZooKeeper 怎么实现这个信息共享的存储空间的呢？它利用一套分布式的算法，在各个节点间达成“状态的一致”。这就是“分布式状态一致性”算法。

所谓“分布式状态一致性”，指的是如下工作场景：

首先，它是一个没有中心节点的分布式系统。这就是说它有很多分散的、平等的节点，但没有中心节点，可以让大家可以来中心节点这里投票什么的。“没有中心节点”是有道理的，因为如果有中心节点的话，那这个节点出现故障了怎么办？所以不能有中心节点。

然后，在没有中心节点，节点间只能互相通信的情况下，所有节点都要对某一个状态达成一致。比如：选择哪个节点作为 Master 节点。在分布式系统中，所有的节点都必须选择一个节点作为 Master，对吧？不能说这边机器找机器 A 做 Master，那边机器找机器 B 做 Master，对不对？这样整个分布式系统就乱了。所以最后大家还是要达成一致，都找一个共同的 Master，这就是在 “Master 节点” 这个状态上，达成了一致。

让我们举个生活中的例子来说明 “分布式状态一致性”。比如，我们班上 60 个同学，要决定毕业旅行去哪里玩。大家最后一定要去一个地方玩，不能这些同学去昆明，但那些同学去上海。但是，我们没有班长，也没有一个可以集中投票的地方，可以让大家都到她这里来集中投票，全靠大家互相之间交流，最后大家所有人都达成一致，去同一个地方旅行。不会有这批人去了地方 A，而那批人去了地方 B 的。这就是在 “旅行目的地” 这个状态上，达成了一致。

Zookeeper 就能够实现上面所说的 “分布式状态一致性”。通过它，系统中总只会有一个 Master。这个 Master 一旦宕机，所有的计算机节点就开始互相聊，然后就聊出另外一个 Master 出来了。它就是这么顽强，有很强的抗毁能力。

所以 Zookeeper 解决了分布式系统中的状态一致性（consistence）问题，就是所有的这些节点，虽然是分布式的，各管各的，但它需要就某个状态达成一个一致的时候，它可以实现这个。

虽然在背后做了很多这样的事情，但 Zookeeper 开放的给我们用的接口非常简单：就是一个文件系统。我们登录上去后可以看到这个文件系统。我们看到里面有一个文件就写着哪个节点是 Master。但大家注意，这个 Master 节点信息并不存在某一个机器上的，它是所有的计算机目前就 Master 这个状态商量后达成的一致结果。只是 Zookeeper 给外部程序的访问做了抽象，看起来好像是个文件似的。所以各个节点都能来访问这个文件，看到 Master 节点的地址。这些节点读走这个信息就行了。但是具体这个 Master 是谁，
是 ZooKeeper 的很多分布式节点商量出来的。

注意，ZooKeeper 能够存储的数据块非常小。它被设计得只存储“状态信息”，比如配置、位置信息等。所以它存储的这些信息的大小都不能太大，。通常以千字节（如果不是字节）为单位。ZooKeeper 有一个内置的 1M 健全性检查，以防止它被用作大型数据存储。

## 实验

下面简单介绍如何访问和操作 Zookeeper。

登录上 ZooKeeper 的主机后，我们可以先 ls 看一眼。大家还记得 ls 是干什么的吗？就是看目录下的文件的。你 ls 一下，就会看到很多目录和文件。这就是一个类似于文件系统的命名空间。里面的文件和目录的名称也是由斜杠（“/”）分隔的。这些文件和目录被称为 znode。这些 znode 组成一个树。

在 znode 文件树上，我们可以执行各种操作，包括 create，delete，exists，setData，getData，getChildren。我们可以做这些操作，创建、删除、观察它存不存在、设置、读取，还可以获取它的子 znodes。比如这里有一个 znode 节点就存的 Master。你去读它，它就返回给你这个文件，里面存着 Master 地址。

znode 分为两种：永久和临时。一个节点创建的临时 znode，当这个节点下线后，就会被 ZooKeeper 自动删除。比如这里存着做 Map Reduce 任务的 Worker 的地址。它们的 znode 就是临时的。如果一个 Worker 机器宕机了，它对应的 znode 就消失了。

要创建一个临时的 znode，可以用 create -e 这个命令。e 代表你创建的是一个临时节点。比如：

		create -e /testmaster "ip"

一旦你创建完它，它的 znode 就像一个文件似的，会出现。你就可以读它，比如：

		get /testmaster

然后，假设你退出 ZooKeeper 这个节点。你一退出来，ZooKeeper 发现你不在了，就会把你刚才创建的这个临时节点删掉。你再进去看，这个 znode 就没了。这就是临时 znode。

ZooKeeper 还提供 znode 的注册-通知机制。节点可以通过注册，获得一个 znode 的改变通知消息。比如，节点可以注册获得 Master znode 的状态改变消息。如果 Master 发生改变，大家可以及时调整。

## 参考文献

- Apache ZooKeeper，https://cwiki.apache.org/confluence/display/ZOOKEEPER

<br/>

|[Index](../) | [Previous](9-0-manage) | [Next](9-3-paxos) |