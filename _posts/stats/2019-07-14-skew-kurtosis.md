---
layout: post
title:  Skewness and Kurtosis
date:   2019-07-14 12:00:00
category: "stats"
keywords: skewness, kurtosis, distribution
---

Skewness and Kurtosis是表征分布形状的两个经典指标，简要介绍其含义及Intuition。

#### Skewness偏度

> 衡量一个分布的不对称性程度和方向。

![669px-Negative_and_positive_skew_diagrams_(English).svg.png (669×239)](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/Negative_and_positive_skew_diagrams_%28English%29.svg/669px-Negative_and_positive_skew_diagrams_%28English%29.svg.png)

分两种情况

**Positive Skewness**

> When the tail on the right side of the distribution is longer or fatter. The mean and median will be **greater than the mode**.

**Negative Skewness**

> When the tail of the left side of the distribution is longer or fatter than the tail on the right side. The mean and median will be **less than the mode**.

具体数值的**intuition**, rule of thumb

+ skewness在$(-0.5, 0.5)$, the data are fairly symmetrical
+ skewness在$[-1, -0.5]$ or $[0.5, 1]$, the data are moderately skewed
+ skewness在$(-00 ,-1)$ or $[1, +00]$ the data are highly skewed

#### Kurtosis峰度

最直观的，Kurtosis体现在峰值上，即

> 表征分布在均值处峰值的高低，直观上反应了峰部的尖度。可以据此判断数据分布相对于正态分布而言是更陡峭(peakedness)还是平缓(flattening)。

但其实更本质的是尾部的分布

> Kurtosis is all about the **tails** of the distribution — not the peakedness or flatness. It is used to describe the extreme values in one versus the other tail. It is actually the **measure of outliers** present in the distribution.

正态分布的Kurtosis值是3，其它分布的Kurtosis高低是相对正态分布的，有的实现里面会将Kurtosis减去3，其正负能反应相对于正态分布的形态。

**High kurtosis**，峰值更尖，尾部占比也就更多

> High kurtosis in a data set is an indicator that data has **heavy tails or outliers**. Sharper than a normal distribution, with values concentrated around the mean and longer tails.This means high probability for extreme values.

**Low kurtosis**，峰值更平，尾部占比也就更少

> Low kurtosis in a data set is an indicator that data has **light tails or lack of outliers**. Flatter than a normal distribution with a wider peak. The probability for extreme values is less than for a normal distribution, and the values are wider spread around the mean.

如下图几种常见分布的Kurtosis值

![1599px-Standard_symmetric_pdfs.png (1599×1142)](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Standard_symmetric_pdfs.png/1599px-Standard_symmetric_pdfs.png)

+ D: Laplace distribution, red curve (two straight lines in the log-scale plot), excess kurtosis = 3
+ S: hyperbolic secant distribution, orange curve, excess kurtosis = 2
+ L: Logistic distribution, green curve, excess kurtosis = 1.2
+ N: Normal distribution, black curve, excess kurtosis = 0
+ C: Raised cosine distribution, cyan curve, excess kurtosis = −0.593762...
+ W: Wigner semicircle distribution, blue curve, excess kurtosis = −1
+ U: Uniform distribution, magenta curve, excess kurtosis = −1.2

Refs

+ [Skewness - Wikipedia](https://en.wikipedia.org/wiki/Skewness)
+ [Kurtosis - Wikipedia](https://en.wikipedia.org/wiki/Kurtosis)
+ [Skew and Kurtosis](https://codeburst.io/2-important-statistics-terms-you-need-to-know-in-data-science-skewness-and-kurtosis-388fef94eeaa)
+ [偏度和峰度如何影响分布 - Minitab](https://support.minitab.com/zh-cn/minitab/18/help-and-how-to/statistics/basic-statistics/supporting-topics/data-concepts/how-skewness-and-kurtosis-affect-your-distribution/)



