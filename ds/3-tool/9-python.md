---
layout: post
title: Python
---

本节我们学习 Python、Numpy、PyTorch、机器学习、深度学习、快速应用界面开发、大数据开发。

# Python

我们首先学习 Python。我们通过斯坦福大学 CS231n 的这个材料入门。打开这个[网页](http://cs231n.github.io/python-numpy-tutorial/)后，它这里有一个 Notebook。我们下载下来，打开，就可以学习了。

这里面教得特别简单，比如 x = 3，然后 x * 3。慢慢地，大家会觉得这些语法跟大家熟悉的 Matlab 差不多。然后是布尔值、字符串、数组、For 循环、字典、函数等等。不难吧？

怎么学呢，特别简单，首先看 Markdown 格子里的文字介绍。然后执行代码格子里的代码。比如说到了这个代码格子，你就点一下格子左上角这个箭头，它就会帮你跑。你就能看到结果，都不用你敲代码，简单吧。

如果有疑问，就选中这些文字或者代码，让 AI 解释就行了。记住，你可以和它说：我是一位小学生，请简明扼要地解释，不要长篇大论。

下面是一些很好的 Python 入门材料

- Python 入门和环境安装
  - 王一行同学，Python 入门指南，[Word 文档](https://yishuai.github.io/bigalgo/exercise/python.docx)，包括 Python 语法、Anaconda Python 环境安装等

- Numpy 入门，包括数组、矩阵、向量运算、广播
    - Justin Johnson, Numpy Tutorial for CS231N at Stanford, [Webpage](http://cs231n.github.io/python-numpy-tutorial/)
    - Sebastian Raschka, Video Mini-series on Numpy, Matplotlib， [Webpage](https://sebastianraschka.com/blog/2020/numpy-intro.html)，专业，配小视频，英文
    - CS124 Numpy Intro, [Github](https://github.com/cs124/pa0-python-jupyter-tutorial) 下 的 numpy_intro.ipynb，有空也可以看看该目录下的 pa0.ipynb，包括正则表达式等。

# 机器学习

我们然后可以首先学习一下陈老师的机器学习概念课程材料，了解一些基本的概念，然后看一下下面的 Python 机器学习入门材料，最后学习 Ng 老师的课程，成为一个机器学习专家。

- 机器学习基本概念
  - 陈一帅，人工智能的基本概念，第二部分，机器学习技术，[网站](https://yishuai.github.io/book/ai/dl/)

- Python 机器学习入门
  - 张璇，《Python机器学习快速上手入门指南》，[Word 文档](https://yishuai.github.io/bigalgo/exercise/mllab.docx) ，Iris实验代码和数据，[Zip 文件](https://yishuai.github.io/bigalgo/exercise/iris.zip)

- 机器学习
  - Andrew Ng 等老师，机器学习入门，Deeplearning.AI on Coursera, [学习网站](https://www.coursera.org/specializations/machine-learning-introduction), [B 站视频](https://www.bilibili.com/video/BV1Bq421A74G)，练习代码答案和笔记 [Github 1](https://github.com/greyhatguy007/Machine-Learning-Specialization-Coursera)，[Github 2](https://github.com/shantanu1109/Coursera-DeepLearning.AI-Stanford-University-Machine-Learning-Specialization)，[PPT](https://www.deeplearning.ai/courses/machine-learning-specialization/#course-slides)

# 深度学习

我们然后可以首先学习一下陈老师的深度学习概念课程材料，了解一些基本的概念，然后看一下下面的 PyTorch 深度学习入门材料，最后学习 Ng 老师的课程，成为一个深度学习专家。

- 深度学习基本概念
  - 陈一帅，人工智能的基本概念，第三部分，深度学习技术，[网站](https://yishuai.github.io/book/ai/dl/)

- PyTorch 深度学习入门
  - PyTorch 官方 Tutorial, [Website](https://pytorch.org/tutorials/)
  - [Pytorch官网快速入门](https://pytorch.org/tutorials/beginner/basics/intro.html)，内容：Tensor（向量）、autograd（梯度下降）、神经元网络等基本概念，可以点击网页左上角的 “Run in Microsof”t Learn” 或“Run in Google Colab” 链接，进行在线实验，也可以 “Download Notebook”，下载 Jupyter Notebook 在本地实验环境中运行；需要本机安装相关软件
  - Soumith Chintala，[Deep Learning with PyTorch: A 60 Minute Blitz](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html)， [中文翻译](https://zhuanlan.zhihu.com/p/25572330) 
  - 斯坦福 CS 224N PyTorch Tutorial, [Github](https://github.com/SunnyHaze/CS224N/blob/main/CS224N%20PyTorch%20Tutorial.ipynb), [Colab](https://colab.research.google.com/drive/13HGy3-uIIy1KD_WFhG4nVrxJC-3nUUkP?usp=sharing)
  - Berkeley CS285 Lec 3: PyTorch Tutorial, [Slides](https://rail.eecs.berkeley.edu/deeprlcourse/), [Youtube Video](https://www.youtube.com/playlist?list=PL_iWQOsE6TfVYGEGiAOMaOzzv41Jfm_Ps)，[Colab](https://colab.research.google.com/drive/12nQiv6aZHXNuCfAAuTjJenDWKQbIt2Mz#scrollTo=U5rl_7Kx5vk8)
  - 斯坦福 CS 224R DRL PyTorch 入门，[Colab](https://colab.research.google.com/drive/1sYhpnlk8ynK4xSSqVmqlhQfPU8b84gHJ?usp=sharing)

- 深度学习
  - Andrew Ng 等老师，深度学习入门，Deeplearning.AI on Coursera, [Coursera 学习网址](https://www.coursera.org/specializations/deep-learning)，[B 站视频](https://www.bilibili.com/video/BV11H4y1F7uH)，练习代码答案和笔记 [Github 1](https://github.com/fengdu78/deeplearning_ai_books)，[Github 2](https://github.com/amanchadha/coursera-deep-learning-specialization)，[Github 3](https://github.com/TheKidPadra/DeepLearning.AI-Deep-Learning-Specialization)， [Github 4](https://abdur75648.github.io/Deep-Learning-Specialization-Coursera/)，[笔记](https://aaronnotes.com/deeplearning-notes/)，[PPT](https://www.deeplearning.ai/courses/deep-learning-specialization/#course-slides)

# 界面开发

我们可以用下面的工具，快速地为我们的机器学习和深度学习模型，开发一个使用的界面，非常方便

- 机器学习模型的快速应用界面开发
  - Streamlit — A faster way to build and share data apps, [Github](https://github.com/streamlit/streamlit) 
  - https://www.gradio.app/，可以自动生成一个公共链接，让其他人可以从自己的设备远程与您计算机上的模型进行交互。

# AI 智能助手调用

我们可以在我们的应用中很方便地加入对 ChatGPT 等 AI 智能助手的调用。

- Python ChatGPT 应用开发
  - Ng 老师，AI Python for Beginners: Basics of AI Python Coding，[学习网站](https://learn.deeplearning.ai/courses/ai-python-for-beginners/lesson/1/introduction)

# 从 Python 入门到大数据开发

我们最后可以学习 Python 大数据开发。这是一套杜克大学的练习（[Github](https://github.com/cliburn/bios-823-2021/tree/main/notebooks)）。

这套材料从 A01 开始，首先介绍 Python、数据处理、SQL，然后介绍机器学习、深度学习、大数据 Spark。这些都是我们要学习的。我们先练习 A01 Python 概念和 A02 Numpy 概念。大家做完这个之后，就会成为真正的高手。我这么说不是骗你们的，因为这里面的东西都是一般的教程不会讲的，是真正的高手才会用的。即使你是学过 Python 的同学，我也建议你做一下，保证你有收获。你会发现：哇，原来 Python 开始这么玩。就很有意思。

<br/>

|[Index](../) | [Previous](7-jupyter) | [Next](11-resume)|
