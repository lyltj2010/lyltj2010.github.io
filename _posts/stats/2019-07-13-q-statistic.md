---
layout: post
title:  Q统计量
date:   2019-07-13 12:00:00
category: "stats"
keywords: q statistic, diversity
---

Q统计量是衡量Ensemble模型中两两分类器（pair wise）有多不同的一个指标。

比如两个分类器分类结果

|  | $D_k correct(1)$ | $D_k wrong(0)$ |
| --- | --- | --- |
| $D_i correct(1)$ | a | b |
| $D_i wrong(0)$ | c | d  |

其中归一化（除以总样本）之后$a+b+c+d=1$，那么Q统计量为

$$Q_{i, k} = \frac{ad - bc}{ad + bc}$$

Intuition

> For statistically independent classifiers, $Q_{i,k} = 0$. $Q$ varies between -1 and 1. Classifiers that tend to recognize the same objects correctly will have positive values of $Q$, and those which commit errors on different objects will render $Q$ negative. For a set of $L$ classifiers, the averaged $Q$ statistics of all pairs is taken.

Refs

+ Ten Measures Of Diversity In Classifier Ensembles: Limits For Two Classifiers
+ [Diversity in Classifier
Ensembles](https://pralab.diee.unica.it/sites/default/files/Slides/Kuncheva_lecture_4_Cagliari.pdf)



