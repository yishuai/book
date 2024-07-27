---
layout: post
title: DataFrame
---

本节介绍如何利用 Spark 进行表格数据的处理。为此，Spark 提供了DataFrame 和 SQL 两种方式。我们首先介绍 DataFrame 的基本概念，然后介绍两个 DataFrame 的处理代码。从中我们可以体会到，DataFrame 用起来确实方便。

Dataframe 的编程，不再像 RDD 那样能够对应到 MapReduce 的操作上了，而是更像 Pandas 的编程，因此更简洁、方便了。

但是 Dataframe 的底层实现，还是采用了 MapReduce 的方式。只不过是 Spark 帮我们把这些类似 Pandas 的语法“翻译”成了 MapReduce 的实现方式。所以，我们看起来是调了一个类似 Pandas 的函数，但其实后面有很多机器在并行地以 MapReduce 的方式工作。

## DataFrame 概念

表格数据有很好的结构，因此，Spark 用 DataFrame 来处理表格数据。我们可以用 DataFrame 的 printSchema 函数，显示它的表格结构。如下例所示

```py
> df.printSchema() root
|-- firstName: string (nullable = true)
|-- lastName: string (nullable = true)
|-- gender: string (nullable = true)
|-- age: integer (nullable = false)
```

如上面的代码所示，df 这个 DataFrame 包括四列。每一列的列名、数据类型都如上图所示。

利用 DataFrame，表格数据的处理变得非常简单、直观。下面是一些例子：

```py
from pyspark.sql import SparkSession

spark = SparkSession \
    .builder \
    .appName("Example") \
    .getOrCreate()

users = spark.read.json("people.json")

# Create a new DataFrame that contains only "young" users
young = users.filter(users["age"] < 21)

# Alternatively, using a Pandas-like syntax
young = users[users.age < 21]

# Increment everybody's age by 1
young.select(young["name"], young["age"] + 1) 

# Count the number of young users by gender
young.groupBy("gender").count()

# Join young users with another DataFrame, logs
young.join(log, logs["userId"] == users["userId"], "left_outer")
```

如上面的代码所示，DataFrame 的操作非常“直观”。熟悉 Python Pandas 或者 SQL 代码的同学会发现 DataFrame 的这些函数和它们很像。拿这些代码和 RDD 的代码比较，我们会发现，RDD 的代码还有 map、reduceByKey 这种反映 Map Reduce 计算操作的函数，但在上面的 DataFrame 代码，就完全没有了。比如，我们看第一行 Filter 代码。如果用 RDD，我们需要送进去一个 Lambda 函数，执行要检查的布尔逻辑。但如果用 DataFrame，我们就简单地写 users.filter(users["age"] < 21) 就可以，甚至，还可以更简单，像上面代码的第二行，写 users[users.age < 21] 就可以。真的是非常的直观。我们看第三行 Select，第四行 GroupBy 然后计数（count），第五行 Join 两个表的代码，都类似的直观、容易理解。事实上，如果我们熟悉 Pandas，就会发现这些函数和 Pandas 里的函数是差不多的。

像 RDD 一样，DataFrame 也是 Lazy 的。filter、select、drop、intersect、join 都是“变换”，而 count、collect、show、head、take 是“动作”。因为 DataFrame 针对表格数据做了优化，所以同样的数据，它运行起来比 RDD 的速度还快。

## Spark SQL

对表格数据的处理，除了 DataFrame，Spark 还让我们可以直接执行 SQL 语句。比如下面的代码：

```py
# Register the DataFrame as a SQL temporary view
users.createOrReplaceTempView("people")

sqlDF = spark.sql("SELECT * FROM people")
sqlDF.show()
```

如上面的代码所示，我们首先用 createOrReplaceTempView 把 users 登记为一个 SQL 临时 View，然后就可以执行 SQL 命令了。

## DataFrame 高级示例

我们下面看一个 DataFrame 的示例代码。这个代码首先计算每一部电影的平均用户打分，然后选出最流行的电影，显示它们的平均用户打分。代码如下：

```py
from pyspark.sql import SparkSession
from pyspark.sql import Row
from pyspark.sql import functions

spark = SparkSession.builder.\
        appName('foo').\
        getOrCreate()

def loadMovieNames():
    movieNames = {}
    with open("/home/u.item") as f:
        for line in f:
            fields = line.split('|')
            movieNames[int(fields[0])] = fields[1]
    return movieNames

def parseInput(line):
    fields = line.split()
    return Row(movieID = int(fields[1]), rating = float(fields[2]))

if __name__ == "__main__":

    # Create a SparkSession
    spark = SparkSession.builder.appName("PopularMovies").getOrCreate()

    # Load up our movie ID -> name dictionary
    movieNames = loadMovieNames()

    # Get the raw data
    lines = spark.sparkContext.textFile("hdfs:///user/u.data")

    # Convert it to a RDD of Row objects with (movieID, rating)
    movies = lines.map(parseInput)

    # Convert that to a DataFrame
    movieDataset = spark.createDataFrame(movies)

    # Compute average rating for each movieID
    averageRatings = movieDataset.groupBy("movieID").avg("rating")

    # Compute count of ratings for each movieID
    counts = movieDataset.groupBy("movieID").count()

    # Join the two together (We now have movieID, avg(rating), and count columns)
    averagesAndCounts = counts.join(averageRatings, "movieID")
    averagesAndCounts.show(20)

    # Pull the top 10 results
    topTen = averagesAndCounts.orderBy("avg(rating)").take(10)

    # Print them out, converting movie ID's to names as we go.
    for movie in topTen:
        print (movieNames[movie[0]], movie[1], movie[2])

    # Stop the session
    spark.stop()

```

如上面的代码所示，在主函数，我们首先对输入 RDD lines 进行 parseInput 的 map 操作，得到结果 movies RDD。然后，我们用 spark.createDataFrame 函数，将其转换为 DataFrame movieDataset。此后，就开始用 DataFrame 的函数来对其进行操作了：我们首先用 groupby 和 avg 计算电影的平均分，然后用 groupby 和 count 计算电影的流行度，然后用 join 把两个数据关联起来，最后用 orderBy 对其进行基于平均分的排序，然后用 take 挑出最高分的前 10 部电影的记录，打印出它们的流行度和用户平均打分。这些代码都非常简洁、直观。

注意，DataFrame 也是 Lazy 的。它的 Transformation 函数都是不立刻执行的，只有 Action 函数才会启动真正的执行过程。

## 小结

我们介绍了 Spark 的 DataFrame 和 SQL 语句支持。它们都是针对表格数据的。其中，DataFrame 类似 Python 和 R 的 DataFrame 语法，编码更简单。我们介绍了各种常用函数，如 filter，groupby，count，avg，join，show，take。除了 DataFrame，Spark 也提供 SQL 支持。在处理表格数据时，因为进行了优化，所以 DataFrame 和 SQL 性能都比 RDD 快。我们最后介绍了一个电影打分的 DataFrame 处理代码，其中包括 Create， Groupby，Avg，Count，Join，Filter，OrderBy 等常用操作。从中我们可以体会到，DataFrame 用起来确实方便。

## 参考文献

- Spark SQL Guide，https://spark.apache.org/docs/latest/sql-getting-started.html

<br/>

|[Index](../) | [Previous](5-rdd-example) |
