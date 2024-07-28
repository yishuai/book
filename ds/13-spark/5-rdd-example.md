---
layout: post
title: RDD 操作示例
---

本节介绍两个 RDD 的例子。第一个是科学计算示例，用 Map 和 Reduce 计算 Pi。第二个是电影评分的处理示例。通过这些例子，我们演示 map、reduceByKey、mapValue、sorBy、take 等 RDD 函数的使用。

## RDD 操作示例

本小节介绍几个 RDD 操作的示例，这样大家就对 RDD 的操作有感觉了。

我们首先看下面的代码及其执行结果

```py
>>> data = sc.textFile('path/to/file')
>>> data.take(3)
[u'Apple,Amy', u'Butter,Bob', u'Cheese,Chucky']
>>> data.map(lambda line: line.split(',')).take(3)
[[u'Apple', u'Amy'], [u'Butter', u'Bob'], [u'Cheese', u'Chucky']]
```

上面代码的第一行的 sc 是加载 Spark 库后，系统提供的一个上下文环境变量，即 Spark Context，所以简称 sc。

因此，第一行是利用 sc 的 textFile 函数，将 path/to/file 这个文件的内容读入，转换为一个 RDD，然后存入 data 变量中。所以，这个 data 已经是个 RDD 了。

第二行，利用 RDD 的 take 函数，取出 data RDD 的前三个数据，显示在屏幕上。大家注意 data RDD 里面其实有很多个数据，但我们通过设置 take 的参数为 3，只显示前三个。

大家看结果：它返回了一个数组，里面包括三个字符串，分别是 u'Apple,Amy', u'Butter,Bob' 和 u'Cheese,Chucky'。

第三行，利用 RDD 的 map 函数，对 data RDD 里面的每一个元素，做 Map 操作。

Map 函数的用法，很像我们前面学过的 Pandas 的 Apply 函数。它接受一个函数作为输入，然后从头到尾，把数据里的每一个记录，都作为函数的输入，送到函数里，处理一遍，然后把输出返回出来。

上面的 Map 函数接受的是一个 Lambda 函数。我们来看这个 Lambda 函数是怎么写的。因为 RDD 里面的元素是通过逗号分割的，比如 'Butter,Bob' 这个元素。所以，Lambda 函数的输入是 line。它是一个字符串，会包括 'Butter,Bob' 这样的元素内容。我们因此就调用字符串变量的函数 split，用分割符“,”把这个字符串分开。因此，'Butter,Bob' 就会被分割为 [u'Butter', u'Bob']。你看，它就变成了一个数组了：第一个元素是 'Butter'，第二个元素是'Bob'。

这就是编写 RDD 程序的基本方法。

## 各种 RDD 操作

RDD 的操作和 MapReduce 的原理是完全匹配的。除了上面介绍的 map，还有 flatMap、mapValues、flatMapValues、filter、groupByKey、reduce、reduceByKey、sortBy、sortByKey、subtract、join 等函数。我们下面分别给出它们的示例：

## Map 操作

flatMap，filter，sortBy 的工作方式和 Map 类似：

```py
>>> data = sc.textFile('path/to/file')
>>> data.take(3)
[u'Apple,Amy', u'Butter,Bob', u'Cheese,Chucky']

>>> data.flatMap(lambda line: line.split(',')).take(6)
[u'Apple', u'Amy', u'Butter', u'Bob', u'Cheese', u'Chucky']

>>> data.filter(lambda line: re.match(r'^[AEIOU]', line)).take(3) 
[u'Apple,Amy', u'Egg,Edward', u'Oxtail,Oscar']

>>> data.sortBy(lambda line: line).take(3)
[u'Avocado,Adam', u'Anchovie,Alex', u'Apple,Amy']
```

```py
>>> data = sc.textFile('path/to/file')
>>> data = data.map(lambda line: line.split(','))
>>> data = data.map(lambda pair: (pair[0], pair[1]))
>>> data.take(3)
[(u'Apple', u'Amy'), (u'Butter', u'Bob'), (u'Cheese', u'Chucky')] 
```

在上面的代码中，第二个 Map 函数是将第一个函数返回的数组中的两个值，分别放在键值对里。这个括号括起来的内容，就是一个键值对。

## 键值对操作

groupByKey、reduceByKey、sortByKey 操作的是 Pair RDD。Pair RDD 中的元素是键值对：它的第一个元素是 Key，后一个是 Value。

```py
>>> data.mapValues(lambda name: name.lower()).take(3) 
[(u'Apple', u'amy'), (u'Butter', u'bob'), (u'Cheese', u'chucky')]

>>> data.flatMapValues(lambda name: name.lower()).take(3) 
[(u'Apple', u'a'), (u'Apple', u'm'), (u'Apple', u'y')]

>>> data.groupByKey().take(1)
[(u'Apple', <pyspark.resultiterable.ResultIterable object at 0x102ed1290>)] 

>>> for pair in data.groupByKey().take(1):
...     print “%s:%s” % (pair[0], “,”.join([n for n in pair[1])) 
Apple:Amy,Adam,Alex

>>> data.reduceByKey(lambda v1, v2: v1 + “:” + v2).take(1) 
[(u'Apple', u'Amy:Alex:Adam')]

>>> data.sortByKey().take(3)
[(u'Apple', u'Amy'), (u'Anchovie', u'Alex'), (u'Avocado', u'Adam')]
```

在上面的代码中，就会对键值对进行基于 Key 的 Group、Reduce、Sort 等操作。

## 集合操作

subtract 会对两个 RDD 进行操作，从一个 RDD 中去掉和另一个 RDD 的共同元素。

```py
>>> data1 = sc.textFile('path/to/file1')
>>> data1.take(3)
[u'Apple,Amy', u'Butter,Bob', u'Cheese,Chucky']

>>> data2 = sc.textFile('path/to/file2')
>>> data2.take(3)
[u'Wendy', u'McDonald,Ronald', u'Cheese,Chucky']

>>> data1.subtract(data2).take(3)
[u'Apple,Amy', u'Butter,Bob', u'Dinkel,Dieter']
```

## Join

Join 合并两个 Pair RDD。它基于 RDD 的 Key 进行 Join。默认是 inner join。

```py
>>> data1 = sc.textFile('path/to/file1').map(lambda line: line.split(',')).map(lambda pair: (pair[0], pair[1]))
>>> data1.take(3)
[(u'Apple', u'Amy'), (u'Butter', u'Bob'), (u'Cheese', u'Chucky')]

>>> data2 = sc.textFile('path/to/file2').map(lambda line: line.split(',')).map(lambda pair: (pair[0], pair[1]))
>>> data2.take(3)
[(u'Doughboy', u'Pilsbury'), (u'McDonald', u'Ronald'), (u'Cheese', u'Chucky')]

>>> data1.join(data2).collect()
[(u'Cheese', (u'Chucky', u'Chucky'))]

>>> data1.fullOuterJoin(data2).take(2)
[(u'Apple',(u'Amy', None)), (u'Cheese', (u'Chucky', u'Chucky'))]
```

## 用 RDD 计算 pi

我们下面用 RDD 来实现 Euler 公式计算 pi。Euler 公式如下式所示：

$$\lim_{n \to \infty}\sum_{i=1}^n \frac{1}{i^2} = \frac{\pi^2}{6}$$

它对应的 RDD 代码如下：

```py
n = 1000000
ar = np.arange(n)
dat = sc.parallelize(ar, 2)
sqrs = dat.map(lambda i: 1.0/(i+1)**2)
t0 = time.time()
x = sqrs.reduce(lambda a,b: a+b)
t1 = time.time()
print("x=%f"%x)
print("time=%f"%(t1-t0))
```

首先看上面代码的数据初始化。在上面代码的第三行，为了获得从 1 到 1M 的数列的 RDD，它利用了 Spark Context 的 parallelize 函数，将从 1 到 1M 的数组，变成了分布式的 RDD dat。

然后看 Map。在第四行，它用 map 对 dat RDD 中的每一个元素进行计算，得到对应的 $$\frac{1}{i^2}$$，存入了 sqrs RDD。

最后看 Reduce。在第六行，它用 reduce 把 sqrs RDD 中的 1M 个 $$\frac{1}{i^2}$$ 的计算结果，累加起来。

当 Spark 收到 reduce 这个 RDD 的 Action 后，它就开始执行 map 和 reduce。当然，这些计算是通过分布式计算完成的。

## RDD 电影评分计数

我们下面看如何用 RDD 计算电影的用户平均评分。它的代码如下：

```py
from pyspark import SparkConf, SparkContext

# This function just creates a Python "dictionary" we can later
# use to convert movie ID's to movie names while printing out
# the final results.
def loadMovieNames():
    movieNames = {}
    with open("/home/u.item") as f:
        for line in f:
            fields = line.split('|')
            movieNames[int(fields[0])] = fields[1]
    return movieNames

# Take each line of u.data and convert it to (movieID, (rating, 1.0))
# This way we can then add up all the ratings for each movie, and
# the total number of ratings for each movie (which lets us compute the average)
def parseInput(line):
    fields = line.split()
    return (int(fields[1]), (float(fields[2]), 1.0))

if __name__ == "__main__":
    # The main script - create our SparkContext
    conf = SparkConf().setAppName("WorstMovies")
    sc = SparkContext(conf = conf)

    # Load up our movie ID -> movie name lookup table
    movieNames = loadMovieNames()

    # Load up the raw u.data file
    lines = sc.textFile("hdfs:///user/u.data")

    # Convert to (movieID, (rating, 1.0))
    movieRatings = lines.map(parseInput)

    # Reduce to (movieID, (sumOfRatings, totalRatings))
    ratingTotalsAndCount = movieRatings.reduceByKey(lambda movie1, movie2: ( movie1[0] + movie2[0], movie1[1] + movie2[1] ) )

    # Map to (movieID, averageRating)
    averageRatings = ratingTotalsAndCount.mapValues(lambda totalAndCount : totalAndCount[0] / totalAndCount[1])

    # Sort by average rating
    sortedMovies = averageRatings.sortBy(lambda x: x[1])

    # Take the top 10 results
    results = sortedMovies.take(10)

    # Print them out:
    for result in results:
        print(movieNames[result[0]], result[1])

```

我们下面解释这些代码。

首先，是环境配置、获取和读入数据。在代码的第一句，我们从 pyspark 导入了 SparkConf 和 SparkContext 这两个函数。然后，在主程序 main 的开头，我们调用了 SparkConf 来设置程序的名字为 “WorstMovies”，然后调用 SparkContext 获得 Spark 运行环境的上下文 sc。最后，我们调用 sc 的 textFile 函数，读入存在 HDFS 里的原始数据。读进来后，放到 lines RDD 里。这里想强调一下，lines 就已经是个 RDD 了。这个是一个重点，要不大家不知道怎么产生 RDD。你就用 sc 的 textFile 函数读入 HDFS 里的文件，就生成一个 RDD 了。因为 HDFS 里的这个文件可能会很大，在几千台机器上存着，所以这个 RDD 它也可能很大。那么，Spark 会对它做切分，分成很多 Partition，也可能在几千台机器上都存得有。所以，虽然 Spark 为此会干很多很多事情，但编程是这么很简单的一行。

然后，我们在 lines RDD 上，做 map 操作，即：对 RDD 里的每一个数据，执行 parseInput 函数。我们来看 parseInput 这个函数。它首先对输入的行，做 split，然后给它转成一个这样一个键值对：键是 Movie ID，值是一个元组，里面包括打分和 1.0 这个数）。为什么要包括 1.0 这个数呢？因为我们后面要统计一个电影有多少次打分。这就是我们前面讲过的 Map 操作，把每一行都扔出来一个键值对。这些键值对，都存着 movieRatings RDD 里。

然后，我们对 movieRatings RDD 里面的键值对，做 reduceByKey。在Hadoop 里，reduceByKey 是 Hadoop 平台完成的，不用我们写出来，但在 Spark 里我们现在明确地把它写出来。这个 Key 就是 Movie ID。所以，它会自动地把同一个 Movie ID 的所有 (打分，1.0) 元组，分为一组，然后用 reduceByKey 函数输入的这个 Lambda 函数，对它们进行 Reduce 操作。

我们来看这个 Reduce 的 Lambda 函数。Lambda 函数的定义是这样的：在 lambda 关键字后面跟的是函数的输入参数，然后冒号后面跟的是它的返回值。所以，这个函数有两个输入参数：一个是电影 1，一个是电影 2。返回值是一个元组。这个元组的第一个元素是电影 1 的第 0 个元素，加上电影 2 的第 0 个元素，第二个元素是电影 1 的第 1 个元素，加上电影 2 的第 1 个元素。因此，它就会像一般的 reduce 函数那样，以一种“滚雪球”的方式，把一个电影的所有(打分，1.0) 元组累加起来，最后得到这个电影的总分和它的打分数目。这个结果被存在 ratingTotalsAndCount RDD 中。因此，ratingTotalsAndCount RDD 中就有很多电影的键值对：键是 Movie ID，值是由总分和打分数目组成的元组。

然后，我们用 mapValues 计算每个电影的平均分。因为ratingTotalsAndCount RDD 存着各个电影的总分和打分数目键值对：键是 Movie ID，值是由总分和打分数目组成的元组。所以，我们对这个键值对的“值”做 Map 就好了。这个 Map 操作很简单，就是把一个电影的总分除以它的打分总数，这个电影的平均分就计算出来了。这个结果还是一个键值对，键是 Movie ID，值是电影的平均分。存在 averageRatings RDD 里。

最后，我们用 sortBy 按电影的平均分对它们进行排序。我们选择的排序标准是 averageRatings RDD 的键值对的第 1 个元素，即电影的平均分。这样就会基于电影的平均分，对电影排序。因为 sortBy 会从低到高进行排序，所以最后 take 取出来的前 10 个电影，就是评分最低的电影，所以是 WorstMovies（是最坏的电影）。

大家看这个代码，跟我们前面写的，Hadoop 的 Map Reduce 代码完全不一样吧。Hadoop 的代码，你得写一个 map 函数、一个 reduce 函数。而 RDD 的编程，我们换了一种方式，通过 map、reduceByKey、mapVaues、sortBy 这些函数，完成基本的功能。注意，这些函数的输入都是一些处理函数。我们前面说过，Scala 是一种函数式的编程语言，因此它特别擅长做这种工作。大家也注意上面各个函数的输出都是 RDD。所以，它们是经过 Partition，分布式存储的。

<br/>

|[Index](../) | [Previous](3-rdd) | [Next](9-df) |
