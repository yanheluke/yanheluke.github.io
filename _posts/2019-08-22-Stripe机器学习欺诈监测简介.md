---
layout:     post
title:      Stripe机器学习欺诈监测简介
subtitle:   机器学习在支付风险管理领域的应用
date:       2019-08-22
autor:      Yan He
header-img: img/in-post/stripe_fraud_detection_bg.jpg
catalog:    true
tags:
    - fraud detection
    - 机器学习
    - Python
    - 风险管理
---

# 前言
这篇是对stripe的A primer on machine learning for fraud detection的总结（翻译）文。
原文链接：[A primer on machine learning for fraud detection](https://stripe.com/en-US/radar/guide)
BTW, 这篇文章主要是安利stripe自研的风控系统radar（为什么大家都喜欢自研一套然后拿出来卖钱

# 定义
stripe定义了两种情况，整篇文章都是围绕这两类交易来说的（trade-off）
* false negatives: 没拦截的欺诈交易
* false positives: 被风控误伤的交易

# stripe的优势
主要是接入了card networks，数据量大， 对一个接入的商户来说是新卡的交易，stripe认为80%的概率在他们的交易网络里已经出现过。

# 机器学习基础
都是常识，但是图做的蛮好看的。
![img](https://s2.ax1x.com/2019/08/22/mwuGLt.png)


# 特征工程
这一块比较重要。stripe分为两个流程：
1. 当提出一个feature idea之后，首先需要根据历史数据计算这个特征（如最常用的两个IP），一般会使用分布式计算如Hadoop，但即使是这样也可能耗时过长，因此stripe分行是优化计算，通过使用space-saving probabilistic data structure（概率数据结构，超过我知识范围了）
2. 新特征被添加进模型后，需要部署在生产环境。这时候面临的问题是对新进的交易需要实时计算新特征。比如需要根据每一笔新的交易动态的计算用户常用的两个IP；这块对时延要求较高，因为风控模块是被包含在stripe的API flow中的；

最后，对于每个新特征都进行上面两步是非常不效率的（terribly inefficient）。stripe认为应该有这样一种工作流：
声明式的定义特征（specify a feature in a declarative way），支持性的架构（supporting infrastructure）自动计算：历史数据直接计算特征用来训练；实时数据用于生产环境，且是低延迟的（low latency）；这是stripe的机器学习工程师目前focus的架构问题。

# 评估模型效果
## PR curve
![img](https://s2.ax1x.com/2019/08/22/mwu0zj.png)

## ROC curve
![img](https://s2.ax1x.com/2019/08/22/mwuryn.png)

## Score Distributions
这是一般不会提到的。如果是一个随机模型来给交易评分，得到的结果应该是服从[0,1]的均匀分布：
![img](https://s2.ax1x.com/2019/08/22/mwusLq.png)

但一个区分度较好的模型，得到的应该是一个双峰分布：
![img](https://s2.ax1x.com/2019/08/22/mwu6e0.png)
注意，一个双峰分布不代表模型是好的。

另外我的一个问题是这个图是好看，但unbalance的数据集里如何刻画出一个双峰分布来？高风险评分的样本一定是少数，光看图肯定没是画不出上面这种明显双峰特征的分布来的。

# counterfactual analysis反事实分析
类似消金建模里的拒绝推断，但是方法上差异很大，毕竟不可能放一部分风险用户进来观测后续；
stripe有一个专门的课程讲这块：https://www.youtube.com/watch?v=QWCSxAKR-h0
但我拖了小半年了还没看，嘻嘻。
