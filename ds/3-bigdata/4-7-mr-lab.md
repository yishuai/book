---
layout: post
title: Map Reduce 代码示例
---

我们下面给大家介绍一个 Map Reduce 的示例代码。它的作用是统计用户对电影的评分的出现次数，比如：打 5 分的评分，一共出现了多少次。

## 总代码

这是一段 Python 代码。如下：

```py
from mrjob.job import MRJob
from mrjob.step import MRStep

class RatingsBreakdown(MRJob):
    def steps(self):
        return [
            MRStep(mapper=self.mapper_get_ratings,
            reducer=self.reducer_count_ratings)
        ]

    def mapper_get_ratings(self, _, line):
        (userID, movieID, rating, timestamp) 
            = line.split('\t')
        yield rating, 1

    def reducer_count_ratings(self, key, values):
        yield str(sum(values)).zfill(5), key

if __name__ == '__main__':
    RatingsBreakdown.run()
```

这段代码包括六个部分。下面分别对它们进行介绍

## 1、mrjob 库

第一部分是导入 Map Reduce 库。包括下面两行：

        from mrjob.job import MRJob
        from mrjob.step import MRStep

如这两行所示，它首先导入 mrjob 这个 Python 库。mrjob 让我们能够用 Python 编写 MapReduce 作业，并在本机、自己的Hadoop 集群，或者众多商业云计算平台上运行。

## 2、创建 Map Reduce Job 类

第二部分是创建 Map Reduce 类，这就是下面这句语句。

        class RatingsBreakdown(MRJob):

如这一行所示，这导入了 mrjob 库之后，我们就继承 MRJob 这个类，建立我们自己的 Map Reduce 类 ratingcount。如这个名字所示，它的功能是对用户的打分（Rating）进行计数（count）。“类”和“继承”都是面向对象编程的概念。请放心，不了解它们，对我们理解 Map Reduce 的代码影响不大。

## 3、定义 Map Reduce 步骤

第三部分是定义 Map Reduce 的步骤（Step）。这就是下面的这个 steps 函数。它是 MRJob 定义的一个函数。我们“重载”它，完成我们自己的功能。

        def steps(self):
          return [
            MRStep(mapper=self.mapper_get_ratings,
                reducer=self.reducer_count_ratings)
            ]

如果你对 C、java 这些编程语言比较熟悉，那么，这里需要解释一下上面的 Python 代码中对“缩进”的利用。你看上面这个 steps 函数。它不像 C 语言那样，在函数名字的后面，有一对花括号，把函数的具体语句（就是“函数体”）包括起来，而是加了一个冒号，然后用“缩进”来表示“函数体”。因此，在 steps(self) 后面，“缩进”比它更右的这些行，就是它的“函数体”。Python 就是用这一层一层的缩进，代替 C 和 Java 语言那一层层的花括号的。

如上面的代码所示，steps 函数所做的工作非常简单，它就用 mrjob 提供的 MRStep 函数，返回一个 MapReduce 工作。这个 MRStep 函数的第一个 mapper 参数，指定了 Map 要执行的函数 mapper_get_ratings reducer 参数，指定了 Reduce 要执行的函数 reducer_count_ratings。

如 Map 要执行的函数 mapper_get_ratings 的名字所示，Map 要干的工作，就是从每一行用户评分数据中，获取（get）评分（rating）。而如 Reduce 要执行的函数 reducer_count_ratings 的名字所示，它要做的，就是对不同的打分进行计数。所以这些都是 mrjob 这个库规定好了的。我们就往里面填 Map 要干啥，Reduce 要干啥就行。我们在 MRStep 里指定好，Map Reduce 平台就会自动地去做这个 Map 任务和 Reduce 任务。

## 4、Map 函数

第四部分是具体的 Map 函数了。它是下面这些代码：

        def mapper_get_ratings(self, _, line):
            (userID, movieID, rating, timestamp) 
                = line.split('\t')
            yield movieID, 1

如上面的代码所示，这个函数的输入是用户打分数据的一行（line）。这一行是一个字符串。那么，它是怎么获取（get）用户评分数据里的 rating （评分）的呢？

我们首先看第一句。在这一句，它首先把 line 这个字符串进行切分（split）。怎么切呢？它用“tab键”（\t) 作为间隔符，进行切分。这会把这一行切为四个部分。每个部分都是一个字符串。然后，它把第一部分字符串放到 userid 这个变量里，第二部分放到 movieID 里，第三部分放到 rating 里，第四部分放到 timestamp 里。这种赋值的方法是 Python 语法。大家装了 Python 之后，可以在 Python 里试试，找找感觉啊。

我们然后看第二句。在这一句，它把切完之后得到的评分（rating），抛（yield）了出来。yield 是 Python 的一个关键字，叫做“抛出”。它是一种特别的函数返回方式。我们先理解它是 mapper_get_ratings 这个函数的返回。返回了什么呢？返回了 <movieID, 1> 这个键值对。

为了理解上面说的逻辑，让我们来看一个例子。比如说他现在拿到了一行：“用户A 《奥本汉姆》 4 20231001”，它就会抛出 <“《奥本汉姆》”, 1> 这个键值对。这个 Map 的工作就做完了。所以大家想想，如果现在这个数据里，有三十个同学都看了《奥本汉姆》，那它就会抛出三十个 <“《奥本汉姆》”, 1>。

Map 完成后，Map Reduce 系统就会收集所有这些“键值对”，进行 Group by Key。因为我们是分布式系统，很可能在这个服务器上有一千个数据，在那个服务器上有一千个数据。这个服务器上抛出了二十个 <“《奥本汉姆》”, 1>，那个服务器上抛出了十个 <“《奥本汉姆》”, 1>。那么这个 Map Reduce 系统就会做 Group by Key，就是把所有的以“《奥本汉姆》”为“键”（Key）的键值对，都分组到一起，把它们的值，合并到一个数组里。这个数组就包括 30 个 1。然后它就调 Reduce 函数，开始做 Reduce。

## 5、Reduce 函数

第五部分就是具体的 Reduce 函数了。它是下面这些代码：

        def reducer_count(self,key,values):
            yield str(sum(values)).zfill(5), key

如上面的这行代码所示，这个 Reduce 函数的输入 key 和 values 是 Map Reduce 平台给它整理好的，分别是一个“键”和这个“键”对应的“值”的数组，比如 key 是 “《奥本汉姆》”，values 是包括 30 个 1 的数组。

它首先调 Python 的 sum （求和）函数，把 values 里的 30 个 1 加起来，那就是三十。这就完成了 “《奥本汉姆》” 这个电影的打分的计数功能。它然后用 str（字符串）函数把数字 30 转变为字符串 “30”。这就是这个电影被多少人评过分，其实就是这个电影的流行度嘛。

它然后用 zfill(5) 在 “30” 的左边添 “0”，把它变为长度为 5 的字符串。因为 “30” 是 2 个字符，所以它会计算 5-2 = 3，因此在左边加上 3 个 “0”。所以这个 zfill 就是 zero fill。这样的话，不同长度的数字，显示起来，就有共同的长度。这样显示起来，就好看了。

最后，它用 yield 关键字，把获得的流行度字符串和 Key（里面存着电影的ID，比如《奥巴海姆》），返回出来。因此，它最后就能统计出来：30，《奥巴海姆》，40，《消失的你》这样的结果。

这样，它就实现了一个分布式的，基于用户电影评分数据的，统计电影流行度的 Map Reduce 过程。

## 6、主程序

第六部分是 Python 程序的主程序，就是运行 RatingsBreakdown 这个 Map Reduce 任务。

        if __name == ‘main’
            RatingsBreakdown.run()

## 小结

本节介绍了一个具体的 MapReduce 代码。它基于 Python mrjob Map Reduce 库，对用户电影评分数据进行操作，统计电影的用户打分数。其 Map 操作会输出 Key：电影 ID，Value：1，Reduce 操作会把这些 1 加起来，从而获得一部电影的打分数目。

<br/>


参考文献

- mrjob 文档：https://mrjob.readthedocs.io/en/latest/

<br/>

|[Index](../) | [Previous](4-5-mapreduce) | [Next](4-9-sys-archi) |
