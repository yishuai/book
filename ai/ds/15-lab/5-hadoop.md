---
layout: post
title: 安装 Hadoop
---

我们下面就要开心地安装 Hadoop 了。

请大家把前面的 SSH、Java 都配好后，再进行这一节的工作。这样会比较顺利一些。

下面是在一台已经有 Java 的 Ubuntu Linux 机器上安装 Hadoop 并练习基本命令的步骤。

# 下载、解压、目录移动

我们现在下载吧！

首先到 Hadoop 的[下载网站](https://downloads.apache.org/hadoop/common/)上，看一眼，找到最新的版本号。比如在 2024 年 7 月的最新的版本号是 3.4.0。

然后打开终端，用 wget 下载 Hadoop 的压缩文件。我们直接在服务器上用命令行，直接下载到服务器的硬盘上。不要先用鼠标，点右键另存到你的电脑上，然后再上传到服务器上。这样的话，太慢了。

用 `wget` 从 Apache Hadoop 的官方镜像下载 Hadoop 的二进制文件的命令如下。直接在命令行终端窗口里面敲就行了。然后下载速度特别快，每秒钟 9M 左右。

```bash
wget https://downloads.apache.org/hadoop/common/hadoop-3.4.0/hadoop-3.4.0.tar.gz
```

下载文件后，我们用下面这个命令对它进行解压。

```bash
tar -xzvf hadoop-3.4.0.tar.gz
```


解压后，我们将解压后的 Hadoop 目录移动到 `/usr/local/hadoop`。因为这个 /user/local 目录是系统拥有的目录，我们作为普通用户，不能对它操作，所以我们要 sudo。

```bash
sudo mv hadoop-3.4.0 /usr/local/hadoop
```

# 环境变量配置

我们然后用 vi 编辑我们 Home 目录下的 .zshrc 文件，加入环境变量。

```bash
vi ~/.zshrc
```

添加以下内容到文件末尾：

```bash
export HADOOP_HOME=/usr/local/hadoop
   export PATH=$PATH:$HADOOP_HOME/bin
   export PATH=$PATH:$HADOOP_HOME/sbin
   export HADOOP_MAPRED_HOME=$HADOOP_HOME
   export HADOOP_COMMON_HOME=$HADOOP_HOME
   export HADOOP_HDFS_HOME=$HADOOP_HOME
   export YARN_HOME=$HADOOP_HOME
   export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
```

请大家看一下上面这些环境变量，理解它们的含义。就像我们编程似的，不能在网上下载一个程序，你就开始跑。至少得单步跟踪一下，把每一步都搞懂，你再开始跑，对吧？这样才理解自己跑的是什么。设置环境变量也是如此。每加一行，都要大概看一下，加的是啥东西。比如，上面的 /usr/local/hadoop/bin 目录下，有些什么啊？我们可以 cd 到这个目录下去看一下。这样我们就慢慢积累了对它的知识。虽然刚开始看不大懂，但留个印象，以后就会想起来。

编辑完 .zshrc 后，我们 source 它一下，让它里面设置的变量在我们这个 Terminal 里就产生效果。否则它只会在我们新开一个 Terminal 的时候才会自动执行。因此，我们改它了以后，在这个 Terminal 里是不会立刻生效的。我们 source 一下，它就立刻生效了。

加载新的环境变量：

```bash
source ~/.zshrc
```

上面这些小细节都特别容易忘。所以我们在做这些事情的时候，大脑一定要清醒。对自己在干什么，要尽量理解它的意义。这样才会越来越积累经验。

# Hadoop 配置

我们下面配置 Hadoop 的伪分布模式。为什么是伪分布式呢？因为我们就一台电脑，所以是伪分布式。

我们首先编辑 `core-site.xml` 文件，配置 Hadoop HDFS 的服务端口 9000。以后各种其它系统来找 Hadoop，就会调这个端口。

```bash
vi $HADOOP_HOME/etc/hadoop/core-site.xml
```

在 `<configuration>` 标签中添加以下内容：

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

# 节点配置

我们然后配置它的节点，包括 namenode 和 datanode。

我们首先检查这些 node 的目录是否存在
- /usr/local/hadoop/hdfs/namenode
- /usr/local/hadoop/hdfs/datanode

如果不存在，请创建它们：

```bash
sudo mkdir -p /usr/local/hadoop/hdfs/namenode
sudo mkdir -p /usr/local/hadoop/hdfs/datanode
```

创建后，我们看看这些目录的 Owner 和 Group

```bash
ls -l /usr/local/hadoop/hdfs/
```

如果 Owner 和 Group 不是 cloudide，就要改一下

```bash
sudo chown -R $USER:$USER /usr/local/hadoop/hdfs/*
```

创建完 node 目录后，我们就可以配置它们了。我们编辑 `hdfs-site.xml` 文件：

```bash
vi $HADOOP_HOME/etc/hadoop/hdfs-site.xml
```

在 `<configuration>` 标签中添加以下内容，指定副本的数目和 node 的目录：

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:///usr/local/hadoop/hdfs/namenode</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:///usr/local/hadoop/hdfs/datanode</value>
    </property>
</configuration>
```

## 配置 MapReduce

我们下面配置 MapReduce。`mapred-site.xml` 文件是 Hadoop MapReduce 的主要配置文件之一，用于配置 MapReduce 相关的设置，包括 MapReduce 版本和其他参数。

我们编辑 `mapred-site.xml` 文件（如果文件不存在，可以复制模板文件）：

```bash
vi $HADOOP_HOME/etc/hadoop/mapred-site.xml
```

在 `<configuration>` 标签中添加以下内容。首先指定 MapReduce 的资源管理框架为 Yarn，然后指定 MapReduce 的程序、日志和环境。

```xml
<configuration>
    <!-- MapReduce 运行模式 -->
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <!-- 提供 MapReduce 应用程序的主类 -->
    <property>
        <name>mapreduce.application.master.classpath</name>
        <value>$HADOOP_HOME/share/hadoop/mapreduce/</value>
    </property>
    <!-- 设置 MapReduce 的日志目录 -->
    <property>
        <name>mapreduce.system.dir</name>
        <value>/user/cloudide/mapred/system</value>
    </property>
    <!-- 设置 MapReduce 的历史日志目录 -->
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>localhost:19888</value>
    </property>
    <property>
        <name>yarn.app.mapreduce.am.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/local/hadoop</value>
    </property>
    <property>
        <name>mapreduce.map.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/local/hadoop</value>
    </property>
    <property>
        <name>mapreduce.reduce.env</name>
        <value>HADOOP_MAPRED_HOME=/usr/local/hadoop</value>
    </property>
</configuration>
```

# Yarn 配置

我们也配置 Yarn。编辑 `yarn-site.xml` 文件：

```bash
vi $HADOOP_HOME/etc/hadoop/yarn-site.xml
```

在 `<configuration>` 标签中添加以下内容：

```xml
<configuration>
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>localhost</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

因为我们的 Yarn 也运行在本机，所以我们将 resourcemanager.hostname 设置为 localhost。如果我们的 ResourceManager 在其他主机上，请将 `localhost` 替换为该主机的主机名或 IP 地址。

# 初始化

我们然后格式化 HDFS

```bash
hdfs namenode -format
```

# 启动

然后启动 DFS 和 Yarn。这时候，我们会看到不断有端口被占用。

```bash
start-dfs.sh
   start-yarn.sh
```

上面的程序执行完后，请大家再等 1 分钟，因为程序在后台还在启动一些服务。当我们看到 8032 这些端口都启动了之后，就可以访问 “Networking” 标签中的 9870 端口的 HTTP 地址来验证 HDFS 是否正常运行。

<br/>

|[Index](../) | [Previous](3-java) | [Next](6-gui)|
