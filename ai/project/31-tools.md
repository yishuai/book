---
layout: post
title: 编程工具
---

## Jupyter Notebooks
首先，Jupyter Notebooks 是大家会遇到的，在浏览器中运行编程教程的工具，用起来会非常开心。《Dive in Deep Learning》课本的章节 [23.1. Using Jupyter Notebooks](https://d2l.ai/chapter_appendix-tools-for-deep-learning/jupyter.html) 可供参考。

## 编程云

对于 GPU 和 TPU 加速，请随意使用 Google 的 [Colaboratory 环境](https://colab.research.google.com/)。这是一项免费的云服务，您可以在其中通过 GPU 或 TPU 加速运行 Python 代码（包括预装的 TensorFlow 和 PyTorch）。具有两个 CPU 和一个 GPU 或 TPU 的虚拟机最多可以运行 12 小时，之后必须重新启动。这个可以通过中 Colab 的界面上单击“编辑”，然后单击“笔记本设置”，然后选择“无”(CPU)、“GPU”或“TPU”进行硬件加速。《Dive in Deep Learning》课本的章节 [23.4. Using Google Colab](https://d2l.ai/chapter_appendix-tools-for-deep-learning/colab.html) 可供参考。Colab 出于学术目的每天提供最多 12 小时的免费 G​​PU 使用。人们可以用相对低的价格 [在 Colab 上获得更多计算](https://medium.com/@yufengg/how-to-upgrade-colab-with-more-compute-64d53a9b05dc)。

除了 Colab，[Kaggle](https://www.kaggle.com/general/108481) 也为我们提供 GPU。每个月限时 30 个小时。

然后，百度的[飞桨社区](https://aistudio.baidu.com/index)、阿里的[魔搭社区](https://modelscope.cn/home)，也提供了类似 Colab 的免费编程环境供大家使用。或可参考。

最后，[AWS](https://aws.amazon.com/education/awseducate/) and [Azure](https://azure.microsoft.com/en-us/free/students/) 两者都向学生提供初始资金。

## 常用工具

【MIT公开课】计算机课堂中根本学不到的知识 - CS Education，[B 站视频](https://www.bilibili.com/video/BV1XN4y187zp)，介绍了工作常用的工具。

## 电脑优化

大家如果是 Mac 电脑的话，可以尝试打开 Mac 自带的 GPU 加速。HuggingFace 的指南 《[Accelerated PyTorch Training on Mac](https://huggingface.co/docs/accelerate/usage_guides/mps)》 供参考。

<br/>

|[Index](./) | [Previous](29-web) | [Next](50-project)
