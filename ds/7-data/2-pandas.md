---
layout: post
title: Pandas 处理关系
---

我们使用 Pandas 处理数据表。重点介绍以下四种功能：

第一种是选择子集。一般来说，我们的数据会特别特别多。比如淘宝的数据，它可能有几百列。咱们可能就分析其中几列就行。那怎么把这几列选择出来？这是我们常干的一件事情，叫选择子集。

第二个是聚合。比如说我们想统计一下咱们班上男生有多少个？这就要聚合一下：把男生聚到一起，然后计数，统计一下。我们也经常要做这种工作，是吧？

第三个是 Join，就是我们要把多个表连到一起。比如我们有学生表，里面存着大家的年龄、性别、学号。还有这门课的选课表，里头存着大家的学号。为什么不存大家的姓名呢？因为你们的姓名还可能重复呢！但学号肯定是不会重复的。这时候如果我想要分析这门课的同学中女生的数目，是不是需要根据选课表里大家的学号，找到学生表中大家的性别，然后进行统计？这就需要把这两个表 Join 起来，联合分析。

最后一个是转换。我们表里存的内容，很可能并不是我们真正需要的。比如：我想统计一下我们班上，姓赵的同学有几个？但是我们的表里面存的是大家的名字。所以我就要把大家的名字里面的第一个字先挑出来，然后再统计。这时候就要做一些转换的工作。

上面四个工作，是我们工作中最常用的，所以我们重点介绍它们。

编程的秘诀是练习。大家觉得编程是什么？有的同学说：这个 Python 有这么多函数，每个函数有这么多用法，我就天天背，背英语单词似的，把它背熟，是不是就是高手了？不是这样的，对吧？高手的特点是：老板交给我们一个任务，要我们分析个啥，我们能又快又好地完成，是不是？所以我们背的东西，都只是基础。最重要的是要练。

每次课后的练习，才是这门课的精华，请大家一定要练。上课只是学习中很小很小的一小部分，最重要的是大家课后多练习。所以我们的课后练习比较多。大家做不完没关系的，量力而为就行了，因为大家基础不一样。

首先，我们来介绍 Pandas 的安装。Pandas 是 Python 的专门处理表格数据的库。把Python 装完之后，我们要通过 pip install pandas 单独装它。

然后，Pandas 是专门处理表格数据的。表格数据就是像 Excel 表那样的数据。大家在 Excel 表的操作中，是不是经常排序、筛选什么的？这些工作，在 Pandas 里，专门有一些函数来干这些事情，特别方便。

学会 Pandas 对我们后面学习大数据也非常有用。大数据编程中，我们会学 Spark。Spark 编程可以用三种语言：Java、Scala、Python。Spark 为了方便大家使用，尽量采用了 Pandas 的语法。这就是说，我们学会 Panda 以后，学大数据编程也特别方便。

<br/>

|[Index](../) | [Previous](1-intro) | [Next](3-dataframe)|
