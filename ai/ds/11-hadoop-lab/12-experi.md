---
layout: post
title: HDFS 操作
---

假设我们已经在 Marscode 上安装好了 Hadoop。每次加载这个项目后，我们需要完成下面的步骤：

首先进入我们的工作目录

```bash
cd /cloudide/workspace/All-in-One/
```

然后启动 ssh

```bash
sudo service ssh start
```

启动 Hadoop

```bash
start-dfs.sh
start-yarn.sh
```

### 验证 HDFS work

```bash
hdfs dfs -ls /
```

# 练习 Hadoop 基本命令

我们下面练习一些常用的 Hadoop 命令：

1. 创建 HDFS 目录：

```bash
hdfs dfs -mkdir /user
hdfs dfs -mkdir /user/cloudide
```

2. 上传文件到 HDFS：

```bash
hdfs dfs -put localfile.txt /user/cloudide/
```

请注意你的本地目录下有 localfile.txt 这个文件。

3. 查看 HDFS 目录内容：

```bash
hdfs dfs -ls /user/cloudide/
```

4. 从 HDFS 下载文件：

```bash
hdfs dfs -get /user/cloudide/localfile.txt
```

5. 删除 HDFS 文件：

```bash
hdfs dfs -rm /user/cloudide/localfile.txt
```

<br/>

|[Index](../) | [Previous](11-gpt) | [Next](15-wordcount)|
