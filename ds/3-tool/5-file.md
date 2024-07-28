---
layout: post
title: 文件的读入与查看
---

我们的数据大多存在文件里。在读入文件的时候，常常遇到各种问题，下面介绍各种数据文件的读入和解析，包括文件路径、编码、大小和命令行工具。

## 文件路径

每个操作系统都有不同的构建文件路径的规则。例如，MacOS 和 Linux 使用右斜杠作为路径，如 ~/files/data.csv，而 Windows 使用左斜杠，如 C:\files\data.csv。因此，有的时候我们给大家的代码是用的右斜杠，但同学们是在 Windows 上跑，就会发现跑不通。这时，你就要改一下代码，把右斜
改成左斜杠。

为了避免上面这种手工的修改斜杠，我们可以用 Python 的 Pathlib 库。利用这个库，我们就可以像下面的代码这样，设定路径。但注意 Python 的版本需要 >= 3.4。

```py
from pathlib import Path
insp_path = Path() / 'data' / 'inspections.csv'

text = insp_path.read_text()

print('\n'.join(text.split('\n')[:5]))

"business_id","score","date","type"
19,"94","20160513","routine"
19,"94","20171211","routine"
24,"98","20171101","routine"
24,"98","20161005","routine"
```

## 文本文件读入

Pathlib 还提供了一个 read_text 函数，能够读入文本。这样读进来的内容，是一个很长的字符串。所以，我们可以用换行符来 split 一下它，得到行的数组。在这个数组里，每一行是一个元素。然后，如果我们想要显示前 5 行的话，我们可以再用换行符，把它们 join 起来，就能看到分行后的 5 行了。代码如上所示。

## 表格文件读入

表格文件一般有两种：csv 和 fwf 文件

我们经常读的是 csv 文件。csv 就是 comma seperated values，即：它里面的值是用逗号分隔的。我们可以用 Pandas 的 read_csv 函数来读入它。

除了 csv，还有一种文件叫做 fwf，它里面的值是通过固定的位置来划分的，也就是说它里面每个值的宽度是固定的。这样的话，就可以省去逗号。所以它是按固定宽度分割的，比如第一个值就占 0~6 这个位置，第二个值就占 7-10 这个位置。我们可以用 Pandas 的 read_fwf 函数来读入它。你需要告诉这个函数，0~6 是一列，7~10 是第二列，它就会帮你这么读出来这些值。

```py
colspecs = [(0,6), (14,29), (33,35), (35, 37), 
        (37, 39), (1213, 1214)]
varNames = ["id", "wt", "age", "sex", "race","type"]
dawn = pd.read_fwf('data/DAWN-Data.txt', 
    colspecs=colspecs, header=None, index_col=0, 
    names=varNames)
```

## 文件编码

我们有时候打开一个文件，发现都是乱码。这是文件编码的问题。

有三种常见的编码：ASCII、ISO-8859-1、UTF-8。

怎么知道一个文件是用的什么编码呢？有几种方法。

首先，可以用命令行工具 file -I 命令得到文件的编码。

然后，可以用 Python 的 chardet 库的 detect 函数推断文件编码。该函数返回推断出来的编码类型，还有一个“信心分数”。代码如下

```py
import chardet

line = '{:<25} {:<10} {}'.format

print(line('File Name', 'Encoding', 'Confidence'))

for filepath in Path('data').glob('*'):
    result = chardet.detect(filepath.read_bytes())
    print(line(str(filepath),
        result['encoding'],
        result['confidence']))
```

当然，猜总有不确定性。最好根据文档说明来设置。

如果是 ISO-8859-1 编码的文件，那么我们用 Pandas 的 read_csv 读入时，要告诉它这个信息。否则会报错，因为它会用 UTF-8 解码，结果就发现格式错误。代码如下：

```py
bus = pd.read_csv('data/businesses.csv', 
      encoding='ISO-8859-1')
```

## 文件大小

在 Python 里，如果我们把一个很大的文件全部读入一个 Python 变量的话，我们的 Python 程序就会占很大的内存。一般来说，这样做，会花掉文件大小 5 倍的内存。

那怎么办呢？最简单的是用各种命令行工具观察文件的大小。

首先，可以用 ls -lh 列出文件的详细信息，其中 -l 能够提供有关每个文件的额外信息，-h 以更易于理解的格式提供文件大小。

其次，可以用 wc 列出一个文件中文本的行数、单词数和字符数。

最后，可以用 du -Lsh 列出文件和文件夹占用的磁盘空间情况。其中，-s 显示文件和文件夹大小，-h 以标准的 KiB、MiB 或 GiB 格式显示大小。

另外一个方法是用 Python 的 os.path.getsize(file) 获得文件的大小。

总之，只有当文件大小在自己电脑能够承受的范围内，再将其读入变量。

如果文件大小超过机器能够承受的范围呢？就选择性地读入部分数据，即：Open 一个文件后，不一股脑地把所有文件内容读入变量，而是有选择性地读，只读入我们需要的行和列。

## 文件观察

有时候我们想用程序（比如 Word）打开一个大文件。此时，我们往往会等很久，还打不开，严重的时候，电脑还可能会死机。这怎么办呢？

我们可以用命令行工具，不打开这个大的文件，但也观察这个文件的部分内容。具体来说，有两个命令：

首先，可以用 head -4 name.csv 这样的命令，观察文件最前面的 4 行文本的内容。

其次，可以用 tail 命令观察文本最末尾的几行的内容。

<br/>

|[Index](../) | [Previous](4-vi) | [Next](7-jupyter) |
