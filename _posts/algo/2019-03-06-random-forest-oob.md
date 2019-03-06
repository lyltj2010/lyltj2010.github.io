---
layout: post
title:  Random Forest OOB
date:   2019-03-06 12:00:00
category: "algo"
keywords: random forest, oob, boostrap
---

随机森林模型基于Bagging(Boostrap Aggregation)思想，学习多棵树，聚合结果来减少模型的variance。其中模型的diversity非常重要，一种增加diversity的手段是对原始数据集采样，然后在采样后数据集上训练模型。

#### Boostrap

Random Forest中采样用的是统计学中boostraping技术，即有放回采样。

> Bootstrap sample $\tilde D_t$: Re-sample $N$ examples from $D$ uniformly with replacement -- can also use arbitrary $N_0$ instead of original $N$.

#### OOB

一个问题是，out-of-bag（OOB理解为未采样到的样本）的样本大致数量是多少？如下图中红色星星所示即为OOB。

![algo-random-forest-oob](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-random-forest-oob.png)

可以近似计算。假设$N'=N$，则单个样本$(x_n, y_n)$是OOB的概率为：

$$(1-\frac{1}{N})^N$$

如果$N$足够大，上述值存在极限。

$$(1-\frac{1}{N})^N = \frac{1}{(\frac{N}{N-1})^N} = \frac{1}{(1 + \frac{1}{N-1})^N} \approx \frac{1}{e}$$

所以OOB大小约为

$$\frac{1}{e}N$$

