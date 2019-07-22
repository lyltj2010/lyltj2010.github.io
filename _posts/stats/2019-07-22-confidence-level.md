---
layout: post
title:  置信度
date:   2019-07-22 12:00:00
category: "stats"
keywords: confidence level, 置信度
---


置信度「Confidence Levels」是统计学中常见的概念，容易混淆，简单梳理记录。

> Confidence levels are expressed as a percentage (for example, a 95% confidence level). It means that should you repeat an experiment or survey over and over again, 95 percent of the time your results will match the results you get from a population (in other words, your statistics would be **sound**!).

统计学中常见的任务是用样本「Samples」的统计量去估计总体「Population」的统计量。置信度「以95%为例」的含义就是，如果重复100次估计，其中有95%的情况下，从样本中得到的估计值与总体对应的统计量是Match的。在区间估计「Confidence Intervals」情况下，做100次区间估计，有95个置信区间包含总体真值。因为95%的置信区间包含真实值，所以只做一次区间估计时，我们也认为这个区间是可信的。

如下图示，竖虚线表示总体的统计量，带黑点的线段表示一次次的置信区间估计。

![eab7e81a9a00080c6658d0ff2ac2e7ac_hd.jpg (720×1018)](https://pic4.zhimg.com/80/eab7e81a9a00080c6658d0ff2ac2e7ac_hd.jpg)

Refs

+ [如何理解置信度？ - 知乎](https://www.zhihu.com/question/20183513)
+ [Confidence Interval: How to Find a Confidence Interval: The Easy Way! - Statistics How To](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/confidence-interval/)



