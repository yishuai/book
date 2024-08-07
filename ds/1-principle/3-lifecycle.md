---
layout: post
title: 数据科学生命周期
---

本节我们介绍数据科学的目的、方法和生命周期，特别是如何提出问题。

我们现在应聘到了一个公司里面去了，做数据分析师。刚开始一定有点懵，对吧？不知道怎么开始工作？那我们先来学习一下数据科学的生命周期。

比如我在滴滴，老板交代一个任务。老板说：那个同学，我们滴滴卖菜已经卖了三个月了，亏了很多钱。你帮我做一下数据分析，还要接着搞吗？这时我们就知道了，来了一个任务，我们就要开展一个数据科学的生命周期。

# 内容

我们首先来看数据分析的目的。

## 目的

数据分析的目的，是从一些很混乱的数据中。获得一个启发，帮助决策。这跟咱们在学校评估算法时利用的 Benchmark 数据完全不一样。Benchmark 数据是整整齐齐的。但在现实工作中，大概率是这种情况：老板说你帮我分析一下这三个月我卖菜的数据。你就问老板：数据在哪？老板就会说：找那个人。我们就吭哧吭哧地跑过去找那个人。那个人说：我电脑上有一大堆 Excel 表可以给你，然后现在我们的电商平台上也有一大堆数据表可以给你。然后他就给你一个服务器的地址、用户名和密码，你自己上去看吧！

事实上，作为数据分析师，我们大量的时间都在收集、整理数据。别人不会来帮我们把数据整理好的。我们的起点是一大堆数据，其中一些有用，但大部分没用，而且格式五花八门，也不在一个地方。对此，我们要有心理准备。很多同学很理想化，到了公司，以为会有人把数据清理得干干净净的，就等着他来分析呢。这是不可能的。现实是：我们可能 80% 的时间就是在整理这些数据。大家想：跑模型，谁不会跑？但收集、整理数据，一般的人做不好。这其实是我们的核心工作。我重点强调一下这个。

## 学习内容

我们要学习的，是在具体问题的上下文中思考，寻找有规律的东西，然后基于这些规律进行预测、推理。

做数据分析，我们首先要弄清楚问题的上下文。比如说卖菜，哪天开始卖的？哪几个城市在卖？刚开始是不是比较火，卖得挺好，后面才不行的？这几十个城市是不是有的城市好，有的城市不行？我们都卖些什么菜了？你要了解这个问题有关的上下文，然后在这些上下文中进行分析思考。所以数据分析师必须深刻理解业务。否则的话，谁不会跑个模型，调个参数？然后我们还得批判性思考，并且有全局意识，搞清楚情况到底是啥样子的，然后才能分析得好。

其次，我们要寻找规律性的东西。我们在数据里面其实是要找到一些一般性的、有规律的东西，而不是找一个特例。比如说我告诉老板：我分析出来了，这个小区卖得特别好。那么老板就会说：它凭什么卖得这么好？它做对了什么，导致它卖得好？因此，咱们就得找出这个小区卖得好的规律。有了这个规律后，我们就可以从少数的样本，推广到全体人群。所以老板需要我们得到的是一些基本的、一般的规律，一些通用的东西，这样才有指导意义。

规律帮助我们预测。老板要的是要预测。他会说：已经发生的，就算了；已经亏了的，也追不回来了，关键是明天别亏，或者告诉我还要亏多少天才能够停止，这样他就可以决策。所以要做决策，最需要的就是预测。

预测有置信区间。老板也知道你肯定预测得不准，你又不是上帝，对吧？所以你告诉他一个置信区间是很重要的。你告诉老板：我这个预测，95% 的置信行区间是多少？比如说亏 100万，上下 5% 浮动。这就是说可能亏 95 万到 105 万。这个预测准确率和 50% 浮动，即从 50 万到 150 万波动，就不一样。老板看到这个，就会知道你专业。我们要输出的东西。

规律也帮助我们推理，提出建议。提出策略建议后，可以做 A/B 测试。比如：拿一个小区来做实验！这个小区，加这个策略，那个小区不加这个策略，然后比较它们的结果。这就是A/B测试。如果最后我们测一把，发现加了策略的小区就不亏了，那就说明这个方法可能真的管用。在互联网公司里经常干A/B测试。

总之，我们数据分析师的工作，就是从混乱的数据中，发现一些基本的规律，从而能够对未来进行预测。这个预测很可能不准，所以我们要给出置信区间。然后，为了检验政策建议，我们可以首先做A/B测试，就是做试点。试点成功后，再全面推行。

## 问题

数据分析的核心是“问题”。我们下面来看一些典型的问题。在给老板干活之前，一定要把问题清楚地定义下来。否则的话，很可能你干了半天，老板说：你干的是什么？跟我的预期不符。这就是我们干一个任何一个活的时候，都要先做需求分析，把问题定义清楚。

一般来说，我们会面对四种问题：

第一个是有效性的问题，比如：疫苗是否有效？对滴滴来说，那就是我现在滴滴卖菜的界面上加了一个领菜的活动，这个活动是不是有效？这是一种典型的问题。

第二个是可信性的问题，比如：这个新闻是否可信？现在的新闻众说纷纭，一会看到一个说这样，一会看得一个说那样。那这个新闻是否可信呢？这里面是有一些科学分析方法的。比如我们可以看这个新闻到底是谁的新闻？是新华社的新闻？还是那些小道新闻？小道新闻就完全可以不看，不管他是 B 站上多么大的大 V。对于滴滴来说，可能就是现在有一个经理提出建议：怎么怎么做，就能把销售提高 10%，那我们要看看数据，分析一下他的这个论点是不是可信？就是看数据，找证据。

第三个是变化趋势的问题，比如：气候如何变化？对于滴滴来说，就是分析这个销售会怎么变化？这时我们要注意明确时间的尺度：是以年为单位，还是以日为单位？这就是两个问题了。

第四个是合理性的问题，比如：政策是否合理？付出多少？得到多少？真的值吗？对于滴滴来说，就是分析一下，这个建议是不是合理。

上面这些问题都是具有通用性的问题。我们摸清这些问题的规律，工作的时候就知道该怎么干。然后接到一个任务，首先搞清楚它是什么问题。最好是拿着问题到老板那边去，白纸黑黑字地写下来，否则的话，老板也可能会忘事的。写论文也是如此：开题的时候就要清楚地写好：我们研究的是这个问题。

## 小结

总之，数据科学的目的，是从混乱的数据里，找到启发，理解世界，帮助决策。学了数据科学课后，我们就能够用科学的眼光，去分析新冠疫苗有效性的数据，评估一个新闻是否可信，寻找气候变化的数据依据，或者探讨一项证据是否合理。

为此，我们首先要学会提出问题，学会在具体问题的语境中进行思考。这非常重要。数据科学学习的，是一种基于数据的思维方式。这种思维方式，基于数据的观察和证据，运用逻辑推理，避免逻辑谬误。

然后，我们要学会科学地设计实验，收集和分析数据。学了数据科学课后，老师让大家设计一个数据调查或者测量的方案，比如测量空气质量，我们也可以设计一个真正科学的方案去测，不是说随便在哪里摆一个设备就去测。这样测出来的数据本身就有问题，依靠这种数据进行决策会误导听众，也把我们带入歧途。

最后，我们要学会如何在数据里找到规律，建立模型，理解世界。我们在数据中找到的规律，建立的模型，应该有一定的普遍性，可以推广到我们观察数据之外的更广的场景中，指导我们的实践。

总之，我们的目的是请大家学会如何在数据中思考。怎么透过数据的迷雾，找到问题的答案。有的时候真的是迷雾啊，因为你的数据太大了，你根本不知道不知道怎么下手。然后数据非常复杂，你试图用它来跑一个模型，但根本不收敛。所以这里最核心的其实要学会如果思考。数据科学是个思考的科学啊。要想问题，在数据中思考，用数据来帮我们理解问题，展开思考。大家是不是喜欢看侦探小说。这个工作和侦探工作是差不多的。

# 生命周期

好，下面我们就真的要开始工作了。工作的话，不是一上来就要开始折腾的。咱们先做计划。这个计划可以是临时性的，因为后面还会再调整。

一开始的计划，应该包括数据科学的生命周期的四部分：1）问问题，2）获得数据，3）理解数据，4）理解世界。

首先，是“问问题”。第一步一定要把问题定义清楚。大家看左上角这个这是“问问题”。这就像我们读研究生时必须开题一样。你必须认真地开题！你不能不开题，或者胡乱开一个，然后就没有目标地一通写，那绝对是个灾难。在公司里干也是这样。我们要确保我们做的，是老板需要的，要不我们就是白干。所以咱们一定要先拼命地把问题定义清楚。

其次，是“获得数据”。定义清楚问题之后，我们就可以拿着这个问题，去找数据了。比如我要预测明天北京地区会亏多少，好的，那我就知道要找北京的数据了。那我要区分生鲜亏多少吗？还是只要考虑整个亏多少？根据这些问题的定义，我们就知道要找什么数据了。找数据的这个过程非常熬人，比如你去找这个人，但她可能不在，找那个人，他给你一个数据库的地址和登录密码。你又得去学习这个数据库的用法，去筛选和下载数据。下载下来数据后，你一看，怎么有很多的空值？！所以你又得接着再去找数据。

做研究一般有公开的数据集。大家也可以上 [Kaggle](https://www.kaggle.com/) 这个数据科学网站上去找找看，上面有各种各样的数据。然后，我们也可以做爬虫，到网上爬数据。有时候老师也会给我们一些数据。还有打一些比赛也有一些数据。最后，当然是我们自己设计调查问卷，或者部署测量仪器，自己收集数据了。

然后，是“理解数据”。怎么理解数据呢？首先可以做一些统计分析。最基本的就是看它的缺失值有多少。如果是 5% 的缺失还行，如果 90% 的缺失，那就算了吧，别用这个数据了，以免它给我捣乱，反而把我的预测给搞得不准。你理解了半天后发现：这个数据质量太差，不支持我研究预定的问题。这是很有可能的。这时候，同学们，不要不好意思，就明确地告诉老板：老板，我已经调研三天，所有各个部门的数据我都已经整理好，在这了，它们不支持我回答你老板你这个问题。你肯定不想我糊弄你对吧？咱们再重新搞个题目吧！这是很正常的。老板不会批评你的，反而会觉得你这个同学特别专业。

最后，是“理解世界”，就是建立模型。我们可能会建立最简单的模型，比如“均值模型”，也可能会建立更复杂的概率模型；我们可以会建立线性回归模型，也可能会建立更复杂的非线性机器学习模型，甚至深度学习模型。基于这些模型，我们可以进行仿真、假设检验，还有预测。在建立模型的过程中，我们可能会发现新的问题，为此我们可能会回到第一步，修正我们最初提出的问题。

“理解数据”和“理解世界”的结果，我们都可以通过论文、报告的形式发表，据此作出决策，或者提出自己的方案，给老板提出建议：应该怎么怎么搞。

所以大家就理解了，刚才我们看的那些招聘的要求，就是我们会在公司里这么做的。所以我们去面试的时候，他就会问你这些事。真实世界中，不是说我们就调调函数，调调参数，最后报一个误差，就完事了。上面这个过程，才是真正的流程。这就是我们进行数据科学工作的生命周期。

## 问问题

数据分析是围绕问题展开的。一般来说，有四种类型的问题：

第一种问题是描述性的，比如说房价最近怎么样？这需要我们对房价最近的情况做一个基于数据的描述。这是非常有意义的。我们就可以统计过去十年的房价，然后分析，然后发现最近房价猛跌，是不是可以赶紧买了？这是描述性质的问题。

第二种问题是探索性的，比如我们想探索一下：房价到底跟哪些因素有关？比如说这个房子的位置很好，二环以内，所以它的价格高；这个房子，房龄已经三十年了，所以价格低一点。这种探索性的问题，能够加深我们对房价的理解，也很重要吧？

第三种问题是推理性的，比如：房价现在为什么会跌？哦，因为现在购房需求不足。那么，为什么大家购房需求不足？因为国民收入占 GDP 的比重不高。我们可以收集相应的数据，来进行这样的推理。所以我们前面看得的字节要求大家做因果推理，就是这个。

第四种问题是预测性的。比如：房价还会再跌吗？这就是对未来的预测了。又或者，我们基于数据训练了一个模型，预测一个家长是不是会继续送孩子来辅导班。这些都是预测问题。

我们前面举的例子都是用滴滴的例子。事实上，上面的数据分析要领在其他很多领域都适用。我们做科研、地震预测、环境保护、机械实验，都有数据分析的问题。所以其实它是一个一般性的问题。

在其他的领域里头，我们研究的对象不同。在社会科学里面，我们研究的是一些人群。比如前面的快手的职位，他想让我们研究的是这些人的消费行为。而抖音希望我们研究用户的社会行为，即这些人点不点赞，分不分享。还有研究人群特征，比如说年龄、性别、消费水平、年收入。在自然科学中，我们研究的是物理模型，比如说做机械震动的实验，我们想研究的是它的模型。

## 好的问题

我们提出的问题要能被数据回答。因为咱们是数据科学，所以我们提出问题后，我们要能够收集到相关的数据，来进行数据科学研究。所以这个问题要能被数据回答。这是问题的关键。因此，提出问题时，我们就要想要测量什么，如何做数据收集，用什么测量方法，或者要去哪发现数据。

我们提出的问题也要尽可能清晰、聚焦、有意义。有了清晰的问题，我们后面的探索之路才会清晰；问题聚焦，我们才能够集中注意力，不跑偏、跑散；最后，问题一定要有意义：不仅有社会意义或者经济意义，最好对你个人也有意义，就是你觉得不解决这个问题，简直睡不着觉。我们研究生开题的时候，经常有同学说：我要改进这个算法。老师立刻就问你：你为什么要改进这个算法？这个算法从来没有人用它，你改进它干啥？所以你其实是要找一个更现实、宏观一点的意义。

满足上面要求的问题，就是好问题。一个好问题是成功的一半。在我们的研究过程中，可能超过一半的时间在找一个好问题。希望大家都能找到这样的问题。

## 数据收集方法

怎么知道一个问题有哪些数据支持呢？特别重要的就是你学会找人。大家有没有发现刚才招聘要求里都要求“积极主动”。什么叫积极主动？就是你要主动去找人。同学们，积极主动不是让你主动加班。老板其实不需要你主动加班。他需要的是你主动把这个事情给我摆平。所以，我们得主动去找各种各样的人。你和有可能知道数据的人说：中午咱们一起喝杯咖啡？喝的时候你就可以问他：老板让我预测明天会亏多少，你觉得能预测得出来吗？他说这个没戏，变化太快了。这也是一个信息。如果他说：这个可以，因为咱们这些数据都记着呢！你就可以问他：是啥数据？所以找人是很重要的。不要就是坐在电脑前面。这个不行。要走到别人的桌子旁边去跟人家套近乎。在学校里也是这样子。你要到老师、学长的座位去跟他聊，和学长一起去打羽毛球，然后你就可以问她了：最近研究啥？没错吧。这样的话，你才能得到最多的信息，大家就都愿意帮你。

最后我们就设计数据收集方法：首先我要到哪些人的电脑上面去拷贝她的数据，然后我要去访问哪几个数据库？这几个数据库是存在公司的服务器上的，还是存在阿里云上的？谁有账号？都得搞清楚。

除了收集已有的数据，你还可以要求为你专门生成一些数据，比如要求开发人员修改代码，系统人员修改系统配置，产生你需要的数据；你也可以要求做专门的调研，比如要求这个区域的销售经理帮我填一个调查问卷。这都是可以的。因为这是老板交代的活，为了完成这个任务，老板就得给你资源，对吧？你就拿着尚方宝剑，调配资源就行。所以，在这个过程中，你一定得积极主动。这就是前面的那些招聘信息中反复强调这一点的原因，因为你不是就跑一个函数，而是要克服困难，把这些东西全部搞定。

# 探索性数据分析

假设现在有一些数据在咱们手里上了，首先，我们要做探索性的数据分析。

探索性的数据分析，是做任何数据相关的研究的关键。我经常跟同学们强调：你想做一个科研，改进一个算法，你别一上来，就直接去改进这个算法。你能不能先把这个算法运行的那个数据，先做好探索性的分析？有的同学一上来就直接堆模型，一会儿 CNN，一会儿 RNN，一会儿 Transformer，整半天，然后说：老师，你看这个 Loss 函数它就死活不降，怎么办？老师这时候就会问你了：你的数据有什么特点？他就说我不知道？老师就说：你能不能探索性地分析一下这个数据？他说什么是探索性？探索性就是没有特别具体的目标，就是去看看这个数据。他说老师我懂了。

做探索性数据分析，统计分析也非常有用。比如，这个数据特别大，有几万条，我不能把它全部画出来看吧！所以这时候我们做些什么分析呢？我们可以观察他的统计特征。最基本的是看它的均值、方差、90% 分位数、最大值、最小值。然后看它的概率分布。有了这些信息的话，你对这个数据就有一个基本的了解。比如，以滴滴为例，我们看它的销售额在各个城市的分布，你发现 80% 的销售都来自于北京这个大城市，而其他 20% 的销售是其他那些小城市的。这个信息有意义吧？那我们就观察北京的。

画图也是探索性数据分析的好方法，比如时间序列图。你一看北京这一周销售额的情况，发现主要是周末大家都来滴滴买菜，平时大家都不来滴滴买菜。然后你看节假日。这样慢慢地你对这个数据就有感觉。如果你发现他一点规律都没有，那你就可以推断预测可能会不太准。如果你发现它还挺有规律的，那么就说明还是可以预测的。你就通过这种可视化，能发现很多有趣的模式和趋势。你也可以画 Box 图等，得到一些统计的观察。这就是探索性的数据分析。

探索性数据分析让你对数据有感觉，这时候你才知道自己这个算法应该怎么设计。因为世界上有无数的算法，凭什么这个算法在这个数据上效果好？肯定是这个算法适合这个数据。目前还没有一个模型能够一统天下，对吧？一定是不同的数据需要不同的模型。

## 发现数据的不足

探索性数据分析让你能够对数据做一些清洗。数据里常常会混入一些很极端的值。比如说这是一个气温数据。正常情况下，气温也就是零下20度到零上60度。但是这个里面突然混入一些很离奇的值，比如零下 200 度，或者零上 200 度。这时你通过观察最大值、最小值，就可以发现这些问题。那很显然，你应该要把它们去掉。否则你的分析结果就不符合实际情况了。

探索性数据分析让你能够对数据做补全。数据经常会出现缺失。你画出可视化的图之后，发现虽然缺了一些值，但是波形的基本规律还是有的，那么我们做一个插补就能把这个缺失值给补上，不会影响我最后的预测。但是如果你发现缺失把波形的趋势都破坏了，那你就知道这个数据就不行：把它弄进来做模型就是坑爹。

所以我经常跟同学们说：你做大数据、深度学习、机器学习，其实三分之一的时间是在分析数据。只有深刻理解了数据，我们的模型才会设计得好。很多时候，一个深度模型到底是六层还是八层，到底是用 Adam 还是用别的优化算法，区别不大，但是对数据了解清楚了，就会对问题理解深刻，就能想出独特的算法，模型效果就会好。是这个道理。最后，我们的论文逻辑是：我研究的这个问题是有意义的，现有的方法解决不了这个问题，为此，我提出了一个想法（这个想法可能来自数据分析），这个想法特别好，最后我拿一个数据来验证我这个想法是有效的。我们会这么说。这个逻辑链条就是圆的。这和我们研究滴滴的问题是一样的。

所以我们很强调同学们在研究生开题之前，一定要摸摸数据，把想法基本上验证通过，这就对后面的论文工作很有帮助。否则的话，你开了一个题，结果到了中间，发现做不出来，这个时候整个实验室都崩溃了。所以大家要重视数据分析，这个对大家顺利毕业也是有好处的。

## 小结

数据科学的生命周期是以一个问题出发。提出一个清晰、聚焦、有意义、能够被数据支撑的问题，是第一步。然后，第二步和第三步就是收集数据，进行探索性的数据分析。在这个过程中，我们通过可视化，总结数据，进行描述性分析，发现有趣的模式、趋势，寻找数据的不足，获得启发，然后再回过头来，清洗数据，获得更多数据，或者基于数据的限制，调整研究问题，不断迭代。这就是数据科学的生命周期。

当我们提出，或者遇到一个问题的时候，如果这个问题能够被数据解决，我们就去收集一些数据。数据到了我们手里后，我们就要做各种分析，去理解这个数据里面有啥，比如分析这个数据之间的相关性，然后训练一个模型，可以来做预测，帮助大家决策等等。这就是一个数据科学的一般的流程。数据的分析，可以用 Excel，也可以用 R 语言、Python。这些工具都可以的。关键是解决问题。对编程不熟的同学，不用担心。我们后面会掌握一个超级厉害的编程方法，就是 AI 辅助编程。

我们在课程的学习中，要做好案例，并且用一种最后你能写到你的简历里面的那种方式来做案例。大家以后写简历，写的会跟这个数据科学的生命周期一模一样，就是：我研究了一个这样的问题。为此，我收集了哪些数据，做了哪些分析，最后设计练了一个什么方法，得到了多少收益。这个收益一定要量化。比如说我给领导层提出的建议，最终帮助公司挽回了 300 万人民币的损失，或者说帮助公司盈利增长 2000 万。大家想想这样的简历都有说服力。这不等面试完成，公司就发 Offer 了，对吧？科研也是这样：同学们很容易陷入模型细节和 Loss 函数就是不下降，但其实我们最后论文答辩的时候，老师才不看你到底是七层还是八层，老师看的是你解决了什么问题？怎么解决的？最后性能比现有的算法好多少？这跟公司面试是一模一样的。

<br/>

|[Index](../) | [Previous](1-intro) | [Next](5-datascope)|

