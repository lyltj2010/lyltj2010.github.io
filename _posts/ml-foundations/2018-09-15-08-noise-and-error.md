---
layout: post
title:  08 Noise and Error
date:   2018-09-15 00:00:00
category: "ml-foundations"
keywords: noise,error
---

在target function有noise的时候，VC bound holds；介绍最基本的错误衡量方式，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/08_handout.pdf)。

## Noise

理想情况下，存在一个target function，但噪音总会存在，比如信用卡审批例子

+ noise in $y$, good customer, mislabeled as bad
+ noise in $y$, same customers, different labels
+ noise in $x$: inaccurate customer information

关心的问题是，如果存在Noise，VC bound是否依然成立？  

考虑推导用最原始的Bin of Marbles的例子，如果`i.i.d.`，后面一系列推导假设类似，即VC bound holds。

![ml-foundations-noise-1](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-noise-1.png)

关于target distribution，其实可以看做

> ideal mini-target + noise

![ml-foundations-noise-2](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-noise-2.png)

## Error Measure

用以衡量$g$于$f$的相似程度。常见的比如point wise error measure，不同学习任务，对应的error measure也不一样。

![ml-foundations-error-measure](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-error-measure.png)

## Algorithmic Error Measure

Error measure一般要根据学习任务设定。

> err is application/user-dependent

比如**0/1 error penalizes both types equally**，但有些场景是不太适用的，比如**Fingerprint Veriﬁcation for Supermarket/CIA**。  

对超市来说，false accept代价很小，false reject代价稍大。

![ml-foundations-fingerprint-verfication-1](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-fingerprint-verfication-1.png)

对CIA来说，false accept代价极大，false reject代价不大。

![ml-foundations-fingerprint-verfication-2](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-fingerprint-verfication-2.png)


## Weighted Classiﬁcation

不同的误分类代价不同，权重不同，error measure也不一样，算法能保证$E_{in}^w(h)$较小吗？

$$
E_{in}^w(h) = \frac{1}{N}\sum_{n=1}^N
\big \{\begin {matrix}
1 &y_n = +1 \\
1000 & y_n = -1
\end {matrix}\big\} 
\cdot [y_n \ne h(x_n)]
$$

其实算法能保证$E_{in}^{0/1}$较小，$E_{in}^{w}$只需要把权重大的样本多访问几次，就得到等价问题。

![ml-foundations-weighted-classification](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-weighted-classification.png)


