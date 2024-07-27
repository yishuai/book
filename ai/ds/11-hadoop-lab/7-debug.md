---
layout: post
title: 故障排查
---

我们经常会遇到启动失败的情况。这时，请不要着急。

首先通过 jps 和 yarn 等命令，来查看系统状态。比如通过以下命令检查 ResourceManager 的状态：

```bash
yarn resourcemanager
```

也可以通过访问 9870 的 URL 来检查 Hadoop 的运行状态：

如果遇到问题，可以查看查看屏幕和日志里的报错信息，然后在 AI 的帮助下，进行排查。

我们下面首先介绍看屏幕上的报错信息：

当运行失败时，最重要的一手材料，就是看程序在屏幕上报出来的错误信息。这些错误信息是非常宝贵的。一个好的编程人员，会在这些错误信息中提供最有价值的信息。她绝对不会乱写的，因为她也是靠这些信息来帮助自己调试代码的。所以她会给我们留下来足够多的线索。如果她不留下足够的线索，那么，当出了一个 bug 时，她自己要拿这 2 万行代码，从第一行开始，到第 2 万结束，一行一行地看，这样行吗？所以她一定会在报错信息里给我们留下线索。这些线索就是我们调试问题的一手材料。比如我们到字节拉一个工程师来问，她也是看这些信息，然后进行分析。所以我们要学会也这样做。这是工作中需要的。

我们来看一个例子。我们运行 Map Reduce 程序后，失败了，屏幕上打印出了很多东西。我们就从后往前看，看到下面的错误信息：

[2024-07-20 07:00:48.758]Container exited with a non-zero exit code 1. Error file: prelaunch.err.

Last 4096 bytes of prelaunch.err :

Last 4096 bytes of stderr :

Error: Could not find or load main class org.apache.hadoop.mapreduce.v2.app.MRAppMaster

Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.mapreduce.v2.app.MRAppMaster

Please check whether your <HADOOP_HOME>/etc/hadoop/mapred-site.xml contains the below configuration:
<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=${full path of your hadoop distribution directory}</value>
</property>
<property>
  <name>mapreduce.map.env</name>
  <value>HADOOP_MAPRED_HOME=${full path of your hadoop distribution directory}</value>
</property>
<property>
  <name>mapreduce.reduce.env</name>
  <value>HADOOP_MAPRED_HOME=${full path of your hadoop distribution directory}</value>
</property>

大家看到没有，它提示我们：“Please check ...” （请你检查）。这就是非常专业的程序员写的。她直接告诉我们要怎么做。那么我们就按她说的做就好了。因此，我们就去检查 <HADOOP_HOME>/etc/hadoop/mapred-site.xml 这个配置文件，然后发现真的没有这个配置。所以我们就决定要加这些配置。

在加之前，我们还要认真理解这些文字的意思，不能就傻乎乎地复制粘贴。比如上面的配置，我们看到其中是这样的文字：${full path of your hadoop distribution directory}。这句话是不是有点像是一句交代？它是在和我们交代一个什么事情，就是让我们找到 Hadoop 的安装目录，把它的完整路径给它写到这个后面。这时候咱们就得去找。

因为我们在前面的环境变量配置中，已经配过 $HADOOP_HOME，所以我们已经知道 Hadoop 的安装目录了。那么，怎么把它加进去呢？如果我们还不确定的话，我们就可以问 AI。

我们可以这么问 GPT：

我运行 Hadoop 的 Mapreduce，出现了错误。它提示如下：Please check whether your <HADOOP_HOME>/etc/hadoop/mapred-site.xml contains the below configuration:

```xml
<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=${full path of your hadoop distribution directory}</value>
```

请问怎么办？

ChatGPT 回答如下：

这个错误提示表明 `mapred-site.xml` 配置文件缺少了 `yarn.app.mapreduce.am.env` 这一配置项，这项配置是用来指定 MapReduce 应用程序的环境变量的，其中包括 `HADOOP_MAPRED_HOME` 环境变量，它应该指向你的 Hadoop 安装目录。

解决步骤如下：

打开 `mapred-site.xml` 文件进行编辑，添加 `yarn.app.mapreduce.am.env` 配置，即在 `<configuration>` 标签内添加以下内容：

```xml
<configuration>
    <property>
        <name>yarn.app.mapreduce.am.env</name>
        <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
    </property>
</configuration>
```

确保将 `${HADOOP_HOME}` 替换为你的 Hadoop 安装目录的实际路径，例如 `/usr/local/hadoop` 或 `/opt/hadoop`。完整路径可能如下：

```xml
<property>
    <name>yarn.app.mapreduce.am.env</name>
    <value>HADOOP_MAPRED_HOME=/usr/local/hadoop</value>
</property>
```

大家看，GPT 还给我们了一个例子。这样我们就完全清楚该怎么修改了。

配置修改后，需要重新启动 Hadoop 服务以使更改生效：

```bash
stop-dfs.sh
stop-yarn.sh
start-dfs.sh
start-yarn.sh
```

<br/>

|[Index](../) | [Previous](6-gui) | [Next](9-log)|
