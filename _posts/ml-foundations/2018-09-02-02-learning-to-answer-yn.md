---
layout: post
title:  02 Learning to Answer Yes/No
date:   2018-09-02 00:00:00
category: "ml-foundations"
keywords: learning-from-data,machine-learning,pla
---

从最简单最基础的**二分类**问题出发，演示一个简单机器学习算法PLA的完整过程，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/02_handout.pdf)。

## 回顾

The Learning Problem:

> $A$ takes $D$ and $H$ to get $g$ that approximate target function $f$.

这节课foucus在Hypothesis Set，用**Perceptron(linear binary classiﬁers)**演示如何解决二分类问题。如根据用户age/salary/等特征判定是否发放信用卡。

## PLA算法

算法形式极其简洁，权重x特征，大于零正例；小于零负例。

$$h(x) = sign(w^Tx)$$

算法迭代步骤，关键点是有错才改：

+ 初始化$\textbf w_0 = \textbf 0$
+ 找一个误分类点$y_n \textbf w_t^T \textbf x_n < 0$
+ 更新权重$\textbf w_{t+1} = \textbf w_t + y_n\textbf x_n$
+ 直到没有误分类点，返回$\textbf w$

最重要的是当发现误分类点时，更新权重：

$$\textbf w_{t+1} = \textbf w_t + y_n\textbf x_n$$

## Intuition

![ml-foundations-pla-intuition](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-pla-intuition.png)

最直观的Intutiton，每一步更新如何使结果更好？

+ $y = +1$: 误分则$\textbf w$和$\textbf x$夹角大于90度，更新$\textbf w$后使其往$\textbf x$靠近，夹角变小
+ $y = -1$: 误分则$\textbf w$和$\textbf x$夹角小于90度，更新$\textbf w$后使其离$\textbf x$更远，夹角变大

## 收敛性证明

PLA算法有前提是数据集**线性可分**。

> 线性可分: Exists perfect $\textbf w_f$ such that $y_n=sign(\textbf w_f^T\textbf x_n)$

如果数据集线性可分，能保证算法收敛吗？如何证明？思路是

+ 假设目标$\textbf w_f$完美分开数据集
+ 证明每一轮$\textbf w_f^T \textbf w_t$至少线性增加
+ 证明每一轮$\textbf w_t$长度无法达到线性增加
+ 其夹角会递减，有限迭代后，$\textbf w_t$会收敛到$\textbf w_f$

> Inner product of $\textbf w_f$ and $\textbf w_t$ grows fast; length of $\textbf w_f$ grows slowly.
> PLA ‘lines’ are more and more aligned with $\textbf w_f$ then halts.

因为$\textbf w_f$将每个数据都正确分类，所以：

$$y_n\textbf w_f^Tx_n \ge min_{n\in[1, N]} y_n\textbf w_f^Tx_n = \rho > 0$$

利用归纳法容易得到：

$$\begin{split}
\textbf w_f^T \textbf w_t  & = \textbf w_f^T \textbf w_{t-1} + y_n \textbf w_f^T\textbf x_n \\
					  & \ge  \textbf w_f^T \textbf w_{t-1} + \rho \\
					  & \ge t\rho
\end{split}$$

证明每次迭代，其內积至少是线性增长。內积大一定程度上反映两个向量夹角更接近，当然还需要考虑其长度。  

考虑向量长度：

$$\begin{split}
||\textbf w_t||^2 &= ||\textbf w_{t-1}||^2 + 2y_n\textbf w_{t-1}\textbf x_n + ||y_n\textbf x_n||^2 \\
			 &\le ||\textbf w_{t-1}||^2 + R^2 \\
			 &\le tR^2
\end{split}$$

其中：

$$R = max_{n\in[1, N]}||\textbf x_n||$$

可以看到，向量长度增加速度为$\sqrt t$，达不到线性。且$\textbf w_f$长度固定，综合上面两个结论：

$$\frac {\textbf w_f^T \cdot \textbf w_t}{||\textbf w_f|| \cdot ||\textbf w_t||} \ge \frac{\rho \sqrt t}{R ||\textbf w_f||}$$

最后推论出$t$存在上界：

$$t \le \frac {R^2 ||\textbf w_f||^2}{\rho^2}$$

## PLA改进

PLA只能处理线性可分数据集，Pocket PLA稍微改进：

> If $\textbf w_{t+1}$ makes fewer mistakes than $\textbf w_{t}$, replace $\textbf w_{t+1}$ by $\textbf w_{t+1}$.

数据集不可分情况下也能保证找到较优的解。
