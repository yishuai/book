---
layout: post
title: HBase
---

本节介绍 HBase。传统关系数据库是“按行存储”。每行是一个数据对象（记录），通过索引树来查找。这不适合大数据场景。大数据以查询为主，比如查询一个 Key 对应的列表。因此，HBase 采用“按列存储”。基于这种存储方式，HBase 能够很方便地提供基于 Key 的 Value 查询。

## HBase 的存储方式

HBase 的存储格式是：行键 + 时间戳 + 列族 + 列。通过时间戳，记录更新。然后各列的内容，按列族存储。在一个列族中，可以存储很多不同的“列”的值。这些列就是 Key。这样的话，空的 cell 不占存储空间，而且可以不经声明，直接加入新列。这就是它的“按列存储”。

举个例子。比如说我想要取出一个用户的所有电影评分信息。我可以用一个 User - Item 表来存储这些信息。比如一共有十个用户，这个表就有十行，每行是一个用户。然后如果有一百个电影，那这个表就有一百列，每列一个电影。但是，因为一般来说，一个用户只会看这一百部电影中的几部，所以，这个表里很多 Cell 都是空着的。所以，我们建一个这样大的表是不是不合适？我们想查询一个用户看了哪些电影，还得逐个看一下他所在的行的所有 100 个 Cell，看哪个电影是他看过的，这样是不是很不方便？

因此，我们就换成下面的表。这个表只有两列：行键，列族。如果用户 A 给电影 1 评分是 0.3，给电影 2 的评分是 0.7，我们就给用户加两行记录。这两行记录的“行键”都是“用户 A”，但“列族”里，一行是：{“电影 1”：0.3}，另一行是{“电影 2”：0.7}。我们称这里的电影名，就是“列”。所有的电影合在一起，就是列族。我们可以把这个列族命名为 “Rating”（打分）。这就是 HBase 的列存储。

采用上述“列族”存储方式的好处是：
- 节省空间：相对于传统的 User - Item 表，空的 cell 不占存储空间，所以节省了空间；
- 方便查询：我们通过查询“行键”，就能够把某个用户的所有电影评分都找出来；
- 方便加入新列：如果新出现了一个电影，我们不需要像传统表那样，修改表格的格式，再加一列。我们就在列族里，加一个新的“列”内容就好了。因此，可以不经声明，直接加入新列。

## HBase 系统架构

HBase 是分布式的。有的服务器负责一些行键，另外一些服务器负责另外一些行键。它有一个区域服务器记录每个服务器存储的行键的范围。每个服务器负责的行键范围可以拆分，也可以合并。HBase 用 Zookeeper 记录区域服务器位置，通过 Master 跟踪数据位置。

### HBASE 实验

我们下面学习一套 HBase 的代码。该代码用 HBase 存储电影的打分表。行键为用户，列族为打分，列是电影 ID。我们将连接 HBase 数据库，然后进行 create, drop, update, fetch 等操作。

```py
from starbase import Connection
from hdfs import InsecureClient

# 连接 HBase，创建表
c = Connection("192.168.0.243", "21309")
ratings = c.table('ratings')
if (ratings.exists()):
    print("Dropping existing ratings table\n")
    ratings.drop()

ratings.create('rating')
batch = ratings.batch()

# 连接 HDFS，读数据，更新 HBase
lian = InsecureClient(url='http://192.168.0.243:9870', user='root')
with lian.read('/user/u.data',encoding='utf-8') as ratingFile: 
  for line in ratingFile:
    (userID, movieID, rating, timestamp) = line.split()
    batch.update(userID, {'rating': {movieID: rating}})

print ("Committing ratings data to HBase via REST service\n")
batch.commit(finalize=True)

print ("Get back ratings for some users...\n")
print ("Ratings for user ID 1:\n")
print (ratings.fetch("1"))
print ("Ratings for user ID 33:\n")
print (ratings.fetch("33"))

ratings.drop()

```

如上面的代码所示，我们首先连接 HBase，创建表 ratings，然后，我们连接 HDFS，读数据，更新 ratings 表。其中，“行键”是 userID, “列族”是'rating'，“列”是 movieID，“值”是 rating。然后，我们用 ratings.fetch 取出特定 userID 用户的 rating 列族，就得到了他的所有评分。

## 小结

本节介绍了 HBase。传统关系数据库是按行存储。每行是一个数据对象（记录），通过索引树来查找。这不适合大数据场景。大数据以查询为主，比如查询一个 Key 对应的列表。因此，HBase 提供基于 Key 的 Value查询。它的存储格式是：行键 + 时间戳 + 列族 + 列。通过时间戳，记录更新	。然后各列的内容，按列族存储。“列”是Key。这样的话，空的 cell 不占存储空间，而且可以不经声明，直接加入新列。这就是它的“按列存储”。

我们然后介绍了 HBase 的架构，说明它用区域服务器管理“行键”，用 Zookeeper 提供区域服务器位置，通过 Master 跟踪数据位置。

我们最后介绍了 HBase 的实际使用，用 HBase 存储电影的打分表。行键为用户，列族为打分，列是电影 ID。我们将连接 HBase 数据库，然后进行 create, drop, update, fetch 等操作。

<br/>

|[Index](../) | [Previous](7-3-hive) | [Next](9-0-manage) |
