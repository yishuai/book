---
layout: post
title: 测量误差与方法
---

我们下面讨论导致测量误差。

大家看这张图。这个五角星真实值，比如火山口上二氧化碳的真实浓度。但是我们测量总是会有误差。这些红点就是测量点。其中一些红点离五角星近一点，说明它的误差小一点，有的离五角星远一些，说明它的误差大一点。这特别像我们投飞镖，你想投中中间的五角星，但老是会有一点点误差。仪器也是这样子的。

误差有两个原因：Bias（偏差）和 Precision（精度）。我们需要精心设计调查方法、调试仪器，减少这些误差。我们下面分别介绍它们。

# 偏差

我们首先看“偏差”。偏差的意思是测量的点，总是会偏向一个方向。比如这个二氧化碳浓度，它总是测得比实际值他高一点，比如真实值是 1，它总是报 1.1，1.03 这样子。这种叫做偏差。

偏差是因为测量工具的不足导致的。比如我们去买菜，有些秤老是给我们称得重一些，因为它被调偏了。这是偏差。所以偏差是有一定的规律的：你去买菜，商家一般不会给我们称得轻一点。偏差是仪器它会朝固定的一个方向给偏一些，所以叫偏差。

偏差是因为采用的仪器或模型的问题导致的，所以只能靠调整仪器或者模型来解决。比如说我们现在去听音乐会。乐手的一个曲子弄完，他要调一下乐器的音，因为你在那里激情四射、拼命的拉，弦很可能就松了，所以音就不准了，所以要调回来。

所以，对偏差，我们要注意调试好仪器，比如用标准砝码、参考气体来校准仪器。比如说有的市场有公平秤。你觉得一把秤有偏差，就拿这个公平秤的砝码，给这把秤校准一下，它就不偏了。

偏差是不能通过增加测量次数来解决的。你想，如果你的秤被调偏了，那么不论你称多少次，结果还是偏的，对吧？

在用户调研中，如果我们的调查方法不合适，那么就会带来偏差。比如进行电话调研，那么就偏向那些接电话的人，而那些没有电话，或者不接电话的人，就被忽视了。这可能就会带来我们调查结果的偏差。

# 精度

“精度”问题指的是：每一次测量的结果，会有随机性，会在真正的数值周围晃。这时候，仪器是不偏的：它没有坑我们，但它的测量不是很精确，总是在变化：有时候少一点，有时候多一点。这时我们就说它的精度不够。

我们可以观察测量结果，来评估仪器的精度。比如我们不断地测，然后观察它的测量结果的变化程度。通过计算各测量值相对于中值的偏离比值，或者它的标准差除上它的均值（即相对标准差），就可以评估。一般来说相对标准差在 10% 左右，我们都认为设备的精度还可以。

要解决精度问题，有两种方法：

第一种是用高精度的设备。高精确度的设备当然就比较贵了，比如说 200 万一台。它通常就比咱们在网上买的 20 块钱的精度高：20 万的可能在正负 0.1 之间变化，但 20 块钱的可能就在正负 1 之间变化。

第二种是增加测量次数。因为测量结果的变化是一会高，一会低，所以，我们通过测多次，然后对测量结果求平均，还是能够完美地估计这个真实的这个值。所以，精度的问题可以通过增加测量次数来缓解。

# 分层抽样

在测量人群的选择中，我们常采用分层抽样的方法。比如，按年龄，抽三组。每组里面都有 100 个人。调查完了之后呢，首先对每组的测量结果求平均，这么就减少了因为精度不够带来的误差；然后，再比较不同组的测量结果，这样就能看出不同年龄的人的区别，就是它们之间的偏差。

# 测量方法

基于上面的误差分析，我们下面设计前面提到的二氧化碳测量的测量方法。

首先需要确定的是测量仪器。我们用的是什么仪器？是便携式的、可以在现场测的仪器，还是那种高精度的，需要在专门实验室里安装好，才能进行测量的仪器？

不同的仪器有不同的测量方法。一种测量方法是咱们把仪器搬到火山上面去测。这样的测量最及时，但是那个山上面的测量条件不好，不太好部署高精度的仪器。所以还有一个测量方法是把山上的空气运到实验室，这样就可以用实验室的高精度仪器进行测量了。比如，你拿个盒子，装一盒空气，赶紧打包，回到北京实验室再测量。你想，我们要测量的是 100 万个分子里面有多少个二氧化碳分子，要测量准确的话，对测量的设备要求还是非常高的。

其次我们考虑仪器的偏差。为此，我们要对仪器进行校准。怎么校准呢？我们首先配制一个特别特别准的参考气体，它的 PPM 是精准已知的，比如 100 万个空气分子，我里面就放 400 个二氧化碳分子（因为自然空气中二氧化碳的浓度大约为 0.04%）。所以这个空气的 PPM 是极准的。然后我们就拿着仪器测一下这个参考气体。仪器如果测得准就好。如果测得不准，就赶紧调仪器。而且，在火山口上，每小时这样校准一次，每次测量 5 分钟。每天再对另外两个参考气体测量一次，每次测量 15 分钟，因为怕万一这个参考气体漏气不准了。此外，为了防止某个公司的设备有特地的偏差，我们就在这个公司买一台，在那个公司再买一台。挺不容易的吧？

最后，我们考虑仪器的样本数，以改进测量的精度。比如，如果发现测量值异常，就赶紧提高测量的频率，比如每五分钟测一下。

上面这个空气测量的例子，深刻地说明了科学的数据分析设计的重要性。毕竟，地球变暖是事关人类前途和命运的一个大事。如果测量结果说明地球确实不能呆了，那咱们还得跑火星上去，或者流浪地球。所以必须认真专业地设计，解决好数据范围、控制变量、测量方法的问题，确保测量的结果反映真实情况。

具体来说，我们做数据科学的第一步，就是搞清楚拟研究问题的目标人群和数据的测量人群，分析清楚和测量目标有关的控制变量，比如地理位置、时间、测量仪器、方法、样本分布等等。设计好测量方法，进行全面、准确的数据记录，并做好测量方法的设计，仪器的校准。这是整个后面数据科学研究工作的基础。否则的话，收集来的数据就是有偏差的，我们后面分析得再好，也没有用啊。

<br/>

|[Index](../) | [Previous](6-control) | [Next](8-compare)|
