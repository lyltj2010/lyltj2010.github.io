---
layout: post
title:  04 Feasibility of Learning
date:   2018-09-08 00:00:00
category: "ml-foundations"
keywords: hoeffding,feasibility-of-learning
---

一步步推导出学习是可行的，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/04_handout.pdf)。

首先定义Machine如何才叫学到东西了？

> 利用算法$A$从假设空间$H$中找到$g$，其在样本内数据集$D$的表现和样本外表现接近，也就是 $E_{in}(h) \approx E_{out}(h)$。

所以要探讨从$H$中，用算法$A$挑一个假设$h$，一定概率下能保证样本内外表现接近么？

课程大致思路：

1. Learning is Impossible?
2. Probability to the Rescue
3. Connection to Learning
4. Connection to Real Learning

## 学习不可行

**From a deterministic view**，是无法从已知数据集$D$中学习出unknow target function $f$的。不管数据集内拟合多好，数据集之外依然完全是未知的。比如这个人为构造的二分类问题

![ml-foundations-learning-is-impossible](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-learning-is-impossible.png)

不管在已知的五个点上拟合多好，其余三个点上依然有八种可能，具体是哪一种是不可知的。从确定性角度看，**learning is impossible**！

## 概率视角

**From a probabilistic view**，还是可以从$D$中学习一些东西的：

> We can indeed infer **something** outside $D$ using only $D$, but in a probabilistic way.

核心例子**Bin of Marbles**

![ml-foundations-hoeffding-inequality](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-hoeffding-inequality.png)

核心点是从sample推断population的相关信息，比如橙色球的比例。虽然无法精确保证$\nu=\mu$，但Hoeffding不等式理论上证明其偏差存在概率上界。

## Hoeffding不等式

Hoeffding不等式的Intuition：

$$p[|\nu - \mu| > \epsilon] \le 2exp(-2\epsilon^2N)$$

左边表示$\nu$和$\mu$差异大于某个值$\epsilon$，这是我们不期望看到的，我们称之为**坏事情**，那么Hoeffding不等式可以理解为：

> 坏事情发生是有概率上界的，且概率上界随样本量$N$增加而指数递减；所以好事情是Probably Approximately Correct(PAC)。

几点Insight

+ valid for all $N$ and $\epsilon$ 
+ does not depend on $\mu$, no need to know $\mu$
+ larger sample size $N$ or looser gap $\epsilon$, higher probability for $ν \approx \mu$

## Connection to Learning

类比**Bin of Marbles**的例子，可以用样本内表现infer样本外表现，且某一假设$h$样本内外表现差异大（坏事情）是有概率上界的。

![ml-foundations-connection-to-learning](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-connection-to-learning.png)

## Connection to Real Learning

以上这只是针对某一个特定的假设$h$，真实的学习场景用是$A$从$H$中挑选出特定的假设$g$，具体是哪个假设，只有数据集已知才能确定。但不管$g$取哪一个，我们可以保证

$$
\begin {split}
|E_{in}(g) -E_{out}(g)| > \epsilon => & |E_{in}(h_1) -E_{out}(h_1)| > \epsilon \\
							     & or |E_{in}(h_2) -E_{out}(h_2)| > \epsilon \\
							     & \dots \\
							     & or |E_{in}(h_M) -E_{out}(h_M)| > \epsilon \\
\end {split}
$$

根据Union Bound

$$P[B_1, B_2, \dots, B_M] \le P[B_1] + P[B_2] + \dots + P[B_M]$$

可推论出

$$
\begin {split}
P[|E_{in}(g) -E_{out}(g)| > \epsilon] = & P[ |E_{in}(h_1) -E_{out}(h_1)| > \epsilon \\
							     & or |E_{in}(h_2) -E_{out}(h_2)| > \epsilon \\
							     & \dots \\
							     & or |E_{in}(h_M) -E_{out}(h_M)| > \epsilon] \\
							     & \le \sum _{m=1}^MP[|E_{in}(h_m) -E_{out}(h_m)| > \epsilon]
\end {split}
$$

最终得到以下公式，保证学习可行性：

$$
P[|E_{in}(g) -E_{out}(g)|>\epsilon] \le 2M e^{-2\epsilon^2N}
$$





