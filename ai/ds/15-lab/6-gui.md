---
layout: post
title: Hadoop 管理界面
---

通过访问 “Networking” 标签中的 9870 端口的 HTTP 地址，我们就能打开 Hadoop 的管理界面。

首先是预览。它会显示它现在在 9000 端口上待着呢，是 Active 的，是什么时候起来的，版本号是 3.4，这些基本信息。

然后呢，它会显示有一个 Datanode 节点活着。

在这里，也可以看文件系统的内容，包括读写权限，目录和文件。所以它就是一个分布式的文件系统。

日志也可以看到。为了看最新的日志，我们可以看一下日志的修改时间。打开后，会发现日志里东西特别多。东西多没关系。一般出了错的话呢，咱们就在里面搜有没有 ERROR，或者 FAILURE，来找到一些故障的线索。

然后是 Node manager 跟 Resource manager。注意除了 Name Node，还有一个 Secondary Name Node。这是因为 Name Node 特别重要。它一坏的话，整个系统就崩了，所以我们还有一个备份的 Name Node。它是实时备份的，能够立刻接手工作。没有问题。

<br/>

|[Index](../) | [Previous](5-hadoop) | [Next](6-gui)|
