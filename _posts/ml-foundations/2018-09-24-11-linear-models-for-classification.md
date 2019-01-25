---
layout: post
title:  11 Linear Models for Classiﬁcation
date:   2018-09-24 12:00:00
category: "ml-foundations"
keywords: classiﬁcation, linear model
---

介绍线性模型用于分类场景，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/11_handout.pdf)。

## 线性模型

三个线性模型的对比，最核心的就是linear scoring function，后续处理不太一样。

![ml-foundations-linear-models-revisited](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-linear-models-revisited.png)

## Error Function

上述三个模型用的Error Function，由于$y \in \{+1,-1\}$，可以抽象出来一个变量$ys$，方便分析。

![ml-foundations-error-functions-revisited](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-error-functions-revisited.png)

可以看出其他Error Function都是0/1误差的一个上界。

![ml-foundations-error-functions-visualization](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-error-functions-visualization.png)

## Regression for Classification

Linear Regression和Logistic Regression都可以用来做分类。

![ml-foundations-regression-for-classification](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-regression-for-classification.png)

## 多分类

#### One Versus All

如果有$K$个分类，就训练$K$个分类器，每一个分别判断是不是属于类别$k$，最终合并这$K$个分类器。要用**soft classifiers**，不能用**binary classifiers**，因为会出现一个样本被分到多各类别，或者一个类别也被分到。

![ml-foundations-combine-soft-classiﬁers](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-combine-soft-classiﬁers.png)

算法描述如下：

> Multiclass via Logistic Regression: predict with maximum estimated $P(k|x)$

![ml-foundations-one-versus-all](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-one-versus-all.png)

OVA模式有个缺点就是样本不均衡。

#### One Versus One

如果有$K$个分类，训练$K(K-1)/2$个**binary classifers**，然后分别预测，被预测分类最多的那个作为最终分类。每个分类器只用到对应两个分类的样本数据，能解决样本不均衡问题。

![ml-foundations-combine-pairwise-classiﬁers](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-combine-pairwise-classiﬁers.png)

算法描述如下：

> Multiclass via Binary Classiﬁcation: predict the tournament champion

![ml-foundations-one-versus-one](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-one-versus-one.png)


