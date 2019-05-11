---
layout: post
title:  对比损失
date:   2019-05-12 12:00:00
category: "algo"
keywords: loss, contrasive loss
---

Contrasive loss即对比损失，性质比较有趣，简单记录之。

### Contrasive Loss

图像检索任务中，经常会用到对比损失，该损失可以跟如下intuition对齐，即相同label的图像距离越近越好，不同label的图像距离越远越好，看如下Loss的巧妙设计。

$$L=\frac{1}{2 N} \sum_{n=1}^{N} y d^{2}+(1-y) \max (\operatorname{margin}-d, 0)^{2}$$

+ label=1 距离d越小，loss越小
+ label=0 距离d越大，loss越小，超过margin，loss为零

优化上述Loss，那么模型参数的调整可以使相同label的样本更近，不同label的样本更远。

> Contrastive Loss is often used in image retrieval tasks to learn discriminative features for images. The margin term is used to "tighten" the constraint: if two images in a pair are dissimilar, then their distance shoud be at least margin, or a loss will be incurred.

![algo-contrasive-loss](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-contrasive-loss.png)

### Ref

+ [Dimensionality Reduction by Learning an Invariant Mapping](http://yann.lecun.com/exdb/publis/pdf/hadsell-chopra-lecun-06.pdf)
+ [Some Loss Functions and Their Intuitive Explanations](https://jdhao.github.io/2017/03/13/some_loss_and_explanations/)

