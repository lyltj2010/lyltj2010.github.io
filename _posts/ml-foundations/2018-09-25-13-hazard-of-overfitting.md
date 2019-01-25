---
layout: post
title:  13 Hazard of Overﬁtting
date:   2018-09-25 12:00:00
category: "ml-foundations"
keywords: overfitting
---

什么是过拟合，什么引起过拟合，如何解决过拟合，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/13_handout.pdf)。

关注几个核心问题

+ What is Overﬁtting
+ The Role of Noise and Data Size
+ Dealing with Overﬁtting

## 过拟合

注意区分过拟合与Bad Generalization。当从简单模型切换到复杂模型时，$E_{in}$减少，但$E_{out}$增加，表示发生了过拟合。

![ml-foundations-bad-generalization-and-overfitting](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-bad-generalization-and-overfitting.png)


## Data Size

从Case Study入手，过拟合表现很直观。

![ml-foundations-overfitting-case-study](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-overfitting-case-study.png)

从下面learning curve看出，Data Size对过拟合影响明显。当数据量小的时候，用复杂模型，是很不明智的。

![ml-foundations-overfitting-learning-curve](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-overfitting-learning-curve.png)

## Noise

考察Noise的影响呢，设计如下实验：Gaussian iid noise $\epsilon$ with level $\sigma^2$。

$$y = f(x) + \epsilon = Gaussian(\sum_{q=0}^{Q_f}\alpha_qx^q, \sigma^2)$$

分别用$g_2$和$g_{10}$拟合上述target function，衡量过拟合程度，用$E_{out}(g_{10}) - E_{in}(g_2)$表示。

![ml-foundations-impact-of-noise-and-data-size](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-impact-of-noise-and-data-size.png)

《Learning From Data》教材封面的两张图！！！从中可以看出四个常见的过拟合因素。其中deterministic noise指的是，复杂模型的信息，简单假设捕获不了，表现的像noise一样。

> Target complexity acts like noise.

![ml-foundations-deterministic-noise](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-deterministic-noise.png)

## 解决过拟合

用一个开车的例子类比。简单的解决过拟合手段，比如简单的例子

+ data cleaning/pruning
    - possibly helps, but effect varies 
    - correct the label (data cleaning)
    - remove the example (data pruning)
+ data hinting
    - possibly helps, but watch out virtual example not iid
    - add virtual examples by shifting/... given digits

![ml-foundations-driving-analogy](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-driving-analogy.png)

更系统高效的手段，比如Regularization/Validation。


