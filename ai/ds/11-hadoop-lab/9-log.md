---
layout: post
title: 看日志
---

当我们发现问题的时候，很可能屏幕上没有错误信息。这时候，我们就要去看日志。

对大数据工程师来说，日志是最好的助手，因为系统会把执行中的各种信息都记录在日志里。因此，大家一定要学会看日志。

请大家开心地看日志。任何一个专家来给我们解决问题，都是先看日志。基于日志，我们把问题的逻辑给理清楚，这时候才能给 AI 描述清楚问题，这样 AI 才能给出有用的回答。

Hadoop 的日志存在 $HADOOP_HOME/logs/ 里。大家可以在这个目录下看到各个节点的日志。

```bash
cat $HADOOP_HOME/logs/userlogs/application_xxxxx_xxxx/container_xxxx_yyyyyyyyyyy/stdout
cat $HADOOP_HOME/logs/userlogs/application_xxxxx_xxxx/container_xxxx_yyyyyyyyyyy/stderr
```

通过这些日志可以进一步分析问题的根源。

比如 ResourceManager 的日志：

```bash
ls -l $HADOOP_HOME/logs/*resourcemanager*.log
vi $HADOOP_HOME/logs/*resourcemanager*.log
```

用 vi 打开一个日志后，我们可以用 / 来搜索日志里是否有故障相关的关键字，比如 ERROR。

我们也可以在 Terminal 里用 grep 来搜索日志里是不是有这些关键字。

```bash
grep ERROR $HADOOP_HOME/logs/*resourcemanager*.log
```

发现错误后，我们就可以进一步分析和排查，然后修改配置等。

配置修改后，需要重新启动 Hadoop 服务以使更改生效：

```bash
stop-dfs.sh
stop-yarn.sh
start-dfs.sh
start-yarn.sh
```

<br/>

|[Index](../) | [Previous](7-debug) | [Next](11-gpt)|
