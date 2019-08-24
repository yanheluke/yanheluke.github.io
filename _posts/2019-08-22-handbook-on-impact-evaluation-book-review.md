---
layout:     post
title:      『Handbook on Impact Evaluation』书评
subtitle:   因果推断手册
date:       2019-08-22
autor:      Yan He
header-img: img/in-post/impact_evaluation_bg_1.jpg
catalog:    true
tags:
    - 经济学
    - 因果推断
---
# 前言

这本书是我在coursera上《Measuring Causal Effects in the Social Sciences》课程的指定用书，下载链接在课程页面里有。
书评原文发在豆瓣上。

喏，就是这本书：
![img](https://s2.ax1x.com/2019/08/22/m0oCm8.jpg)

全书分为两部分，前半部分是关于impact evaluation的理论，后半部分是stata代码。

impact evaluation的理论/方法，也就是causal inference的方法，基本每一章讲一个。

# 内容

Chap.3 Randomization 随机化

Chap.4 Propensity Score Matching 倾向评分匹配

Chap.5 Double Difference 双重差分

Chap.6 Instrumental Variable Estimation 工具变量

Chap.7 Regression Discontinuity and Pipeline Methods 间断点回归

Chap.8 Measuring Distributional Program Effects

Chap.9 Using Economics Models to Evaluate Policies

准确说，我没看完这本书，只是挑了课程相关的几章，randomization, DID, IV。估计在很长的一段时间内也不会再看这本书，所以姑且做一个特点总结。

1. 数学推导极少

我看的时候是结合Mostly Harmless Econometrics看的，这本《基本无害的计量经济学》大家也都知道数学用的很少了，但架不住handbook on impact evaluation数学更少，几乎等于没有……作者应该是假设读者已经拥有中级以上的计量基础，所以直接不讲基础的OLS参数估计，比如提到IV时，直接说error term和treatment dummy variable T有correlation，会导致参数估计β存在bias，然后引入IV的假设，再得到β的无偏估计。

2. 案例多

可能因为作者Shahidur R. Khandker本身是世行的economist ，所以本书几乎每章都有近十个case study，来讲解impact evaluation的practice。感觉对相关专业和工作的人来说会很合适。

3. 有stata代码

很遗憾没看stata的部分，因为我用R啊……

# 结论（2019.8.22新增）
如果我自己选择的话，我更喜欢看基本无害的计量经济学，毕竟没有数学推导的话总觉得怪怪的。

另外，过了两三年回头看这篇书评，感觉自己已经忘得差不多了。一个是因果推断仍然比较偏理论，工作里用的实在是不多；另一个是自己也对这类传统计量经济学的方法不是很信服。
实际工作里，用得上因果推断的地方非常少，据我所知也是国外大厂在做AB test和广告投放的时候会考虑量化指标来衡量广告收益，其余的地方仍然是机器学习的天下。

读书的时候号称的经济学帝国主义（economic imperialism），现在应该改成计算机帝国主义了吧，笑:)
