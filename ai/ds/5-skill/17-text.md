---
layout: post
title: 正则表达式
---

大家看正则表达式感觉像看天书似的，是吧。但其实它挺简单的。

首先，它是一种模式。比如方括号括起来，就表示一种模式：括号里任一个字符都可以。比如 [012] 就表示 0 也行，1 也行，2 也行。[0-2] 就是 [012]，[0-9] 就是 0123456789 这十个数的任一个都可以，[X-Z] 就是 XYZ 三个字母中的任一个都可以。

如果在前面加一个 ^，就是排除。使用[^0-2] 就是不能是 0、1、2 这三个数。

上面是匹配一个字母的，如果想匹配多个连续的字母，就可以用“量词”。比如，[1-9]{2,3}就表示两个、三个数都可以。{1,} 就是说大于一个都可以。所以它表示的是数量。然后 * 就是 0 个、一个、两个、多个也可以。+ 就是至少要有一个。? 是 0 个或者 1 个。

有时候你必须要找这行的末尾，就用 $，如果你要找这行的开头，你用 ^。

还有一些缩写：比如，\w 代表 “a-zA-Z0-9_”，就是 word，而\W 代表 “^a-zA-Z0-9_”，\d 代表数字，\s 代表（包括空格、Tab键）

Python 的 re 模块有很多函数可以用正则表达式，包括 Search、Match、Findall、Sub（代替）、Split。Search 和 Findall 的区别是：Search 看到第一个就会认为找到了，就会返回，所以它只能找出来一个，而 Findall 找到一个后，会接着往后找，直到把所有的都找出来，再返回。

预先编译正则表达式，能够提高搜索的速度。

Pandas Series 的 str 有 contains、findall、replace、split 等函数可以用正则表达式。

下面是读入一个文本数据，根据里面的 *** 进行划分后，提取 name，date 和文本，填入 dataframe 的例子。

```py
import re

from pathlib import Path

text = Path('data/stateoftheunion1790-2022.txt')
        .read_text()

num_speeches = len(re.findall(r"\*\*\*", text))
print(f'There are {num_speeches} speeches total')

records = text.split("***")

def extract_parts(speech):
      speech = speech.strip().split('\n')[1:]
      [name, date, *lines] = speech
      body = '\n'.join(lines).strip()
      return [name, date, body]

def read_speeches():
    return pd.DataFrame(
    [extract_parts(l) for l in records[1:]], 
    columns = ["name", "date", "text"])
```

我们然后对 text 内的内容进行清洗。去掉括号、非字母的字符。

```py
def clean_text(df):

      bracket_re = re.compile(r'\[[^\]]+\]')
      not_a_word_re = re.compile(r'[^a-z\s]')

      cleaned = (df['text'].str.lower()
          .str.replace(bracket_re, '', regex=True)
          .str.replace(not_a_word_re, ' ', regex=True))

      return df.assign(text=cleaned)

df = (read_speeches()
    .pipe(clean_text))
```

下面，我们就可以用 NLTK、Sklearn 做进一步的自然语言处理的工作了。

<br/>

|[Index](../) | [Previous](15-air-quality)|
