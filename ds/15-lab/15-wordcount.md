---
layout: post
title: Java MapReduce 实验
---

我们下面请 ChatGPT 带我们做一个最简单的 Hadoop Mapreduce 练习：

我们首先问 ChatGPT：

请给一个最简单的 Hadoop 编程的例子。

ChatGPT 回答：

好的！下面是一个简单的 Hadoop 编程例子，它实现了一个基本的单词计数程序（WordCount）。这个程序会读取一个文本文件，并计算文件中每个单词出现的次数。

# 1. 准备工作

首先，确保你的 Hadoop 集群已经启动，并且 HDFS 已经运行。你还需要有一个包含 Hadoop 编程的 Java 环境。

# 2. 编写 WordCount 程序

创建一个新的 Java 文件 `WordCount.java`，并编写以下代码：

```java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCount {

    public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
                word.set(itr.nextToken());
                context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text, IntWritable, Text, IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

我们来看上面的 Word count 程序。

首先是 Map。这个 Map 干的事情特别简单。它就是往外吐“键值对”：(单词，1)。什么意思呢？就是这个文本里面有几个单词，它就扔出来几次。比如有两个 Hello。它就会扔出来两个 (“Hello”,1), (“Hello”,1)。

然后 Hadoop 会自动做 GroupbyKey，就是把所有相同 Key 的键值对，汇集到一起。所以，如果文本里有 100 个 Hello，它就会收集到 100 个 1。

最后是 Reduce。它就是一个 for 循环，不断累加 1。所以，100 个 1 最后会得到 100。这就是对 Hello 这个单词的计数结果。对其它单词也类似。

这就是 MapReduce 程序工作的基本流程。

# 3. 编译 WordCount 程序

使用以下命令编译 `WordCount.java`：

```bash
javac -classpath `hadoop classpath` -d . WordCount.java
```

这将生成 `WordCount.class` 和其他相关的类文件。

# 4. 打包 WordCount 程序

使用以下命令将编译好的类文件打包成一个 JAR 文件：

```bash
jar cf wordcount.jar WordCount*.class
```

# 5. 在 Hadoop 上运行 WordCount 程序

1. 上传输入文件到 HDFS：

   假设你有一个名为 `input.txt` 的文件，包含一些文本。我们要对它进行单词计数。

   首先，将该文件上传到 HDFS：

   ```bash
   hdfs dfs -mkdir -p /user/cloudide/input
   hdfs dfs -put input.txt /user/cloudide/input/
   ```

2. 运行 WordCount 程序：

   使用以下命令运行 WordCount 程序：

   ```bash
   hadoop jar wordcount.jar WordCount /user/cloudide/input /user/cloudide/output
   ```

   这里 `/user/cloudide/input` 是输入文件的路径，`/user/cloudide/output` 是输出结果的路径。

    在程序运行的过程中，我们可以看到它会先 Map，然后做 Reduce。我们也可以在网页界面上看到工作的进展。

3. 查看结果：

   WordCount 程序运行完成后，你可以查看输出结果：

   ```bash
   hdfs dfs -cat /user/cloudide/output/part-r-00000
   ```

   这将显示每个单词及其出现的次数。

   注意：part-r-00000 可能只是一部分的输出。当数据非常大时，我们就还会有 part-r-00001，part-r-00002 这样的输出。

# 6. 清理

运行完程序后，你可以删除 HDFS 上的输入和输出目录：

```bash
hdfs dfs -rm -r /user/cloudide/input
hdfs dfs -rm -r /user/cloudide/output
```

通过这些步骤，你可以编写、编译、打包并运行一个简单的 Hadoop WordCount 程序。如果有任何问题或需要进一步的帮助，请随时提问！


<br/>

|[Index](../) | [Previous](12-expri) | [Next](17-mrlab)|
