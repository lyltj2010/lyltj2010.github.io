---
layout: post
title:  03 Types of Learning
date:   2018-09-04 00:00:00
category: "ml-foundations"
keywords: learning-from-data,machine-learning
---

从四个维度介绍常见机器学习类型，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/03_handout.pdf)。

## Output Space

从$Y$的维度考虑，不同的输出空间，对应不同的机器学习算法。

##### Binary Classification

二分类问题，输出空间为$Y=\{−1, +1\}$。常见例子比如：

+ credit approve/disapprove
+ email spam/non-spam
+ patient sick/not sick
+ ad proﬁtable/not proﬁtable

是极其重要的一类问题：

> Core and important problem with many tools as building block of other tools.

##### Multiclass Classification

多分类问题，输出空间为$Y=\{1,2,\dots, K\}$，二分类是$K=2$时候的特例。常见例子比如：

+ coin recognition
+ written digits ⇒ 0, 1, · · · , 9
+ pictures ⇒ apple, orange, strawberry
+ emails ⇒ spam, primary, social, promotion, update

##### Regression

回归问题，输出空间$Y=R$或者$Y=[lower, upper] \in R$，对应bounded regression。常见的例子比如：

+ patient features ⇒ how many days before recovery
+ company data ⇒ stock price
+ climate data ⇒ temperature

统计学中被广泛研究：

> Also core and important with many ‘statistical’ tools as building block of other tools.

##### Structured Learning

结构化学习，常见例子比如：

+ sentence ⇒ structure (class of each word)(序列标注)
+ protein data ⇒ protein folding
+ speech data ⇒ speech parse tree

> Huge multiclass classiﬁcation problem (structure = hyperclass) without ‘explicit’ class deﬁnition.

## Data Label

从data label $y_n$的有无、多少、形式划分：

+ supervised: all $y_n$
+ unsupervised: no $y_n$
+ semi-supervised: some $y_n$
+ reinforcement: implicit $y_n$ by goodness

##### Supervised Learning

> Supervised learning: every $x_n$ comes with corresponding $y_n$.

比如二分类、多分类问题，都是典型的监督学习。

##### Unsupervised Learning

> Unsupervised learning: diverse, with possibly very different performance goals.

无监督学习形式也很丰富，常见的比如：

+ clustering
    + ${x_n} ⇒ cluster(x)$
    + unsupervised multiclass classiﬁcation
    + i.e. articles ⇒ topics
+ density estimation
    + ${x_n} ⇒ density(x)$
    + unsupervised bounded regression
    + trafﬁc reports with location ⇒ dangerous areas 
+ outlier detection
    + ${x_n} ⇒ unusual(x)$
    + extreme ‘unsupervised binary classiﬁcation’
    + i.e. Internet logs ⇒ intrusion alert

##### Semi-supervised Learning

> Semi-supervised learning: leverage unlabeled data to avoid ‘expensive’ labeling.

常见的比如：

+ face images with a few labeled ⇒ face identiﬁer (Facebook)
+ medicine data with a few labeled ⇒ medicine effect predictor

详细解释见[Semi-supervised learning](https://en.wikipedia.org/wiki/Semi-supervised_learning)。

##### Reinforcement Learning

> Reinforcement: learn with ‘partial/implicit information’ (often sequentially).

样本形式$(x_n, y_n, goodness)$常见的比如：

+ (customer, ad choice, ad click earning) ⇒ ad system
+ (cards, strategy, winning amount) ⇒ black jack agent

## Different Protocol

不同Protocol对应不同Learning Philosophy：

+ batch: duck feeding
+ online: passive sequential
+ active: question asking (sequentially)(query the $y_n$ of the chosen $x_n$)

对应的训练数据也不相同：

+ batch: all known data
+ online: sequential (passive) data
+ active: strategically-observed data

##### Batch Learning

一次性从所有已知数据中学习。

> Batch supervised multiclass classiﬁcation: learn from **all known** data.

+ batch of (email, spam?) ⇒ spam ﬁlter
+ batch of (patient, cancer) ⇒ cancer classiﬁer
+ batch of patient data ⇒ group of patients

##### Online Learning

序列地接受数据，然后更新模型。

> Online: hypothesis ‘improves’ through receiving data instances sequentially

比如online spam ﬁlter, which sequentially:

1. observe an email $x_t$ 
2. predict spam status with current $g_t(x_t)$ 
3. receive ‘desired label’ $y_t$ from user, and then update $g_t$ with $(x_t, y_t)$

PLA can be easily adapted to online protocol.

##### Active Learning

当模型没有把握的时候，把问题交给用户，从而获取高质量样本。

> Active: improve hypothesis with fewer labels (hopefully) by asking questions strategically

## Different Input Space

根据输入空间的含义划分。

##### Concrete Features

> Concrete features: each dimension of $X \in R^d$ represents ‘sophisticated physical meaning’.

常见的比如：

+ (size, mass) for coin classiﬁcation
+ customer info for credit approval
+ patient info for cancer diagnosis
+ often including **human intelligence** on the task

这些具体特征，有明确的含义，可解释性很强，同时**easy for ML**。

##### Raw Features

> Raw features: often need human or machines to convert to concrete ones.

比如image pixels, speech signal等场景。

##### Abstract Features

> Abstract: again need feature conversion/extraction/construction.

比如一些ID特征：

+ student ID in online tutoring system (KDDCup 2010)
+ advertisement ID in online ad system


