---
layout: post
title:  一些函数
date:   2018-12-20 12:00:00
category: "algo"
keywords: 函数, 概率分布
---

策略、算法工作中，读论文或设计算法，经常会遇到一些性质很棒的函数，满足特定的需求，持续汇总积累。

## softmax

$$softmax(x_i) = \frac{exp(x_i)}{\sum_{j=1}^{n} exp(x_j)} = p_i$$

Softmax可以将**一组实数序列(r1, r2, r3, ...)**映射到**概率分布**(p1, p2, p3, ...)上。Softmax里max指会放大最大值的概率，soft指保留部分概率给小的值。

> The softmax function maps arbitrary values $x$ to a probability distribution $𝑝_i$. “max” because amplifies probability of largest $x_i$. “soft” because still assigns some probability to smaller $x_i$

![algo-softmax](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-softmax.png)

## sigmoid

$$\sigma(x) = \frac{1}{1+e^{-x}} = \frac{e^x}{1 + e^x}$$

可将任意实数映射到(0, 1)区间，其值有时候可解释为概率。当然，也可以添加参数，调整曲线的形状

$$\sigma(x) = \frac{1}{1+e^{-\alpha x}}$$


![algo-sigmoid](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-sigmoid.png)

其导数形式比较好，还可以用sigmoid函数本身表示：

$$\sigma'(x) = \sigma(x)(1-\sigma(x))$$


其与tanh函数也有关联，可简单根据值域推断出来：

$$tanh(x) = \frac{e^x-e^{-x}}{e^x+e^{-x}}= 2*\sigma(x)-1$$

## 低频加强

比如每个word在词库里有个频率分布，想大致按次频率分布采样，同时适当加强低频词，削弱高频词，如何做？word2vec论文里有类似办法，就是**unigram distribution U(w) raised to the 3/4rd power**解决。

$$P(w_i) = \frac{  {f(w_i)}^{3/4}  }{\sum_{j=0}^{n}{f(w_j)}^{3/4}}$$

对(0, 1)之间的数，取(0, 1)指数次幂，会使其值适当放大，越小的值，放大效应越明显。可以在google里输入以下语句查看函数性质

> plot y = x ** 0.75  and y = x

## 衰减函数

之间[一篇博客](http://yongle.site/algo/2018/12/06/decay-function.html)介绍衰减了函数，参考见[越近越好Elasticsearch: 权威指南](https://www.elastic.co/guide/cn/elasticsearch/guide/current/decay-functions.html)。

![algo-decay-function](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-decay-function.png)

