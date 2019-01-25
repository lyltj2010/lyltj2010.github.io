---
layout: post
title:  Ranking Metric
date:   2019-01-02 12:00:00
category: "algo"
keywords: ranking,ltr,metric
---

评估排序效果时，经常用到几个指标，简单记录之。

#### AUC

将排序效看做一个二分类问题，计算一系列false positive rate和true positive rate，绘制ROC区间，然后计算曲线下面积得到AUC，细节参考[ROC分析](http://yongle.site/algo/2018/12/16/roc-analysis.html)。

#### MAP

MAP: Mean average precision. 即计算average precision的均值。

![algo-ranking-metric-map](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-ranking-metric-map.png)

首先计算Precision@k，含义是前k个排序结果中，真实相关的比例。然后取不同的k值，计算average precision；最后在多个排序结果上平均。其中$l_k$是indicator function，当前位置文档相关记为1，否则为0。

#### NDCG

> Discounted cumulative gain (DCG) is a measure of ranking quality. In information retrieval, it is often used to measure effectiveness of web search engine.

简单讲就是计算前k个位置上累计的gain。其计算基于如下两个假设

+ Highly relevant documents are more useful if appearing earlier in search result.
+ Highly relevant documents are more useful than marginally relevant documents which are better than non-relevant documents.

一个排序列表，每个item有一相关性得分，计算其得分，并用位置discount（位置越靠后，gain的discount越重，因为假设相关item排前面更有用）。

$$DCG_k = \sum_{j=1}^k \frac {2^{rel_j}-1} {log_2(j+1)}$$

![algo-ranking-metric-ndcg](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-ranking-metric-ndcg.png)

最后需要将DCG归一化，做法是获取Ideal DCG(IDCG)，然后除以它即可。计算例子见参考文档。

#### 参考

+ [T7A-LEARNING TO RANK TUTORIAL.pdf](http://wwwconference.org/www2009/pdf/T7A-LEARNING%20TO%20RANK%20TUTORIAL.pdf)
+ [Discounted Cumulative Gain - Machine Learning Medium](https://machinelearningmedium.com/2017/07/24/discounted-cumulative-gain/)


