---
layout: post
title: 大规模数据
---

大语言模型的训练需要大规模数据。本节介绍大语言模型常用的训练数据，以及数据方面的研究工作。

## 数据集

[Common Crawl](https://commoncrawl.org/) 是目前活跃的开源数据。它被用来训练许多 LLM。

TB 级的多语言数据集有三个：
- BigScience，1.5 TB 文本数据，350 billion token，其中中文 17.7%，英文 30.3%，是从 OSCARv2 网络爬虫数据集中提取的：[介绍](https://bigscience.huggingface.co/blog/building-a-tb-scale-multilingual-dataset-for-language-modeling)
- mc4: commoncrawl 数据集，251 GB，[论文](https://arxiv.org/abs/1910.10683)，[数据](https://huggingface.co/datasets/mc4)
- oscar：commoncrawl 数据集，225 GB，[数据](https://huggingface.co/datasets/oscar)

英文大数据集有两个：
- Pile：825 GB，[论文](https://arxiv.org/pdf/2101.00027.pdf)
- C4: mc4 相对应的英文版，305 G，[数据](https://huggingface.co/datasets/c4)

常用的英文小数据有三个：
- bookcorpus，6 GB，74 M行，[数据](https://huggingface.co/datasets/bookcorpus	)
- openwebtext，41.7 GB，openAI，训练 GPT-2 的数据，[数据](https://huggingface.co/datasets/Skylion007/openwebtext)
- wikitext，549 MB，wiki 文章，[数据](https://huggingface.co/datasets/wikitext)

## Demo
- [A queryable interface to C4](https://c4-search.apps.allenai.org)

## 课程材料

- 斯坦福 CS324 2022 年 [Data](https://stanford-cs324.github.io/winter2022/lectures/data/)

- Sara Hooker, Understanding the role of data, scale and capacity in recent breakthroughs, LxMLS 2023 PPT

- 约翰霍普金斯 UA 2024 Lec 20 Scaling pre-training data,
    - Considerations regarding pre-training data (deduplication, diversity),
    - Scaling model size,
    - Scaling context window,
    - Scaling laws
    - Distributed training
Additional Reading:
    - Documenting Large Webtext Corpora: A Case Study on the Colossal Clean Crawled Corpus

## 论文

约翰霍普金斯大学论文

- Documenting Large Webtext Corpora: A Case Study on the Colossal Clean Crawled Corpus
- The Pile: An 800GB Dataset of Diverse Text for Language Modeling
- On the Effect of Pretraining Corpora on In-context Learning by a Large-scale Language Model
- Deduplicating Training Data Makes Language Models Better

普林斯顿课程推荐论文

- [Documenting Large Webtext Corpora: A Case Study on the Colossal Clean Crawled Corpus](https://arxiv.org/pdf/2104.08758.pdf)

Refer:
- [The Pile: An 800GB Dataset of Diverse Text for Language Modeling](https://arxiv.org/pdf/2101.00027.pdf)
- [Deduplicating Training Data Makes Language Models Better](https://arxiv.org/pdf/2107.06499.pdf)

最新论文

- EMNLP 2023 Large Language Models Can Self-Improve，大语言模型自己生成训练数据

- The RefinedWeb Dataset for Falcon LLM: Outperforming Curated Corpora with Web Data, and Web Data Only, 2023

- ICLR 2021 When Do Curricula Work? 训练时间有限时，先送容易的例子，再送复杂的，会帮助训练。

- What's in the Box? A Preliminary Analysis of Undesirable Content in the Common Crawl Corpus,  ACL-IJCNLP 2021 [Arxiv](https://arxiv.org/abs/2105.02732)，[Github](https://github.com/josephdviviano/whatsinthebox) 

# FineWeb Edu 数据打分提示

https://huggingface.co/datasets/HuggingFaceFW/fineweb-edu

Below is an extract from a web page. Evaluate whether the page has a high educational value and could be useful in an educational setting for teaching from primary school to grade school levels using the additive 5-point scoring system described below. Points are accumulated based on the satisfaction of each criterion:
• Add 1 point if the extract provides some basic information relevant to educational topics, even if it includes some irrelevant or non-academic content like advertisements and promotional material.
• Add another point if the extract addresses certain elements pertinent to education but does not align closely with educational standards. It might mix educational content with non-educational material, offering a superficial overview of potentially useful topics, or presenting information in a dicorganizod manner and incoherent writing style.
Award a third point if the extract is appropriate for educational use and introduces key concepts relevant to school curricula. It is coherent though it may not be comprehensive or could include some extraneous information. It may resemble an introductory section of a textbook or a basic tutorial that is suitable for learning but has notable limitations like treating concepts that are too complex for grade school students.
Grant a fourth point if the extract highly relevant and beneficial for educational purposes for a level not higher than grade school, exhibiting a clear and consistent writing style. It could be similar to a chapter from a textbook or a tutorial, offering substantial educational content, including exercises and solutions, with minimal irrelevant information, and the concepts aren't too advanced for grade school students. The content is coherent focused and valuable for structured learning.
• Bestow a fifth point if the extract is outstanding in its educational value, perfectly suited for teaching either at primary school or grade school. It follows detailed reasoning, the writing style is easy to follow and offers profound and thorough insights into the subject matter, devoid of any non-educational or complex content.
The extract: <extract>.
After examining the extract:
Briefly justify your total score, up to 100 words.
Conclude with the score using the format: "Educational score: <total points>"

<br/>

| [Index](./) | [Previous](2-5-model) | [Next](2-9-scaling)
