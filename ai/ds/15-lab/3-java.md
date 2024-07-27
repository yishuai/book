---
layout: post
title: JAVA 环境配置
---

# 介绍

熟悉完 SSH 之后，我们来搞清楚系统中的 JAVA。因为很多大数据程序是 Java 的，所以，我们要步步为营，把 Java 先弄清楚了。

# 问题

在运行大数据程序，比如启动 start-dfs.sh 的时候，可能出现以下问题：

Starting namenodes on [localhost]

localhost: ERROR: JAVA_HOME is not set and could not be found.

这个错误提示表明 JAVA_HOME 环境变量未设置，Hadoop 无法找到 Java 运行时环境。要解决这个问题，你需要设置 JAVA_HOME 环境变量。以下是具体步骤：

# 找到 Java 安装路径

首先，确定你的 Java 安装路径。可以使用以下命令查看：

```bash
which java | sed "s:bin/java::"
```

假设返回的路径是 `/opt/cloudide/jdk/jdk-17.0.10/`。

# 设置 Hadoop 的 JAVA_HOME 环境变量

对 Hadoop，我们可以编辑 Hadoop 的环境配置文件来设置 `JAVA_HOME`

编辑 `$HADOOP_HOME/etc/hadoop/hadoop-env.sh` 文件：

```bash
vi $HADOOP_HOME/etc/hadoop/hadoop-env.sh
```

在文件中找到 `# export JAVA_HOME=...` 行，取消注释并设置为你的 Java 安装路径，例如：

```bash
export JAVA_HOME=/opt/cloudide/jdk/jdk-17.0.10/
```

保存并关闭文件。

# 设置全局 JAVA_HOME

如果你希望全局设置 `JAVA_HOME` 环境变量，可以编辑 `~/.zshrc` 文件：

```bash
vi ~/.zshrc
```

在文件末尾添加以下行：

```bash
export JAVA_HOME=/opt/cloudide/jdk/jdk-17.0.10
export PATH=$PATH:$JAVA_HOME/bin
```

然后保存并关闭文件，加载新的配置：

```bash
source ~/.zshrc
```

# 验证 JAVA_HOME 环境变量

可以通过以下命令验证 `JAVA_HOME` 是否设置正确：

```bash
echo $JAVA_HOME
```

应该输出你的 Java 安装路径。

# Java 版本兼容性问题

Marscode 上的 Java 是 17。所以运行 Hadoop 时可能出现下面的错误：

Caused by: java.lang.reflect.InaccessibleObjectException: Unable to make protected final java.lang.Class java.lang.ClassLoader.defineClass(java.lang.String,byte[],int,int,java.security.ProtectionDomain) throws java.lang.ClassFormatError accessible: module java.base does not "opens java.lang" to unnamed module @5f565482

这个错误通常是因为 Java 版本兼容性问题，特别是使用了 Java 9 及以上版本，而 Hadoop 依赖一些内部 API 这些版本中默认被限制访问。

如果你必须使用 Java 9 及以上版本，可以尝试修改 Hadoop 的启动配置，添加 JVM 参数，允许访问受限制的模块。

vi `$HADOOP_HOME/etc/hadoop/hadoop-env.sh` 文件，添加以下行：

```bash
export HADOOP_OPTS="$HADOOP_OPTS --add-opens=java.base/java.lang=ALL-UNNAMED"
```

通过这些步骤，你应该能够解决 `InaccessibleObjectException` 错误。

<br/>

|[Index](../) | [Previous](1-ssh) | [Next](5-hadoop)|

