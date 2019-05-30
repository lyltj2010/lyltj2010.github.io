---
layout: post
title:  逻辑回归求导
date:   2019-05-30 12:00:00
category: "algo"
keywords: logistic regression, gradient
---

逻辑回归算法非常经典，其求解经常用梯度下降算法，本文简单推导梯度表达式，以备忘。

逻辑回归形式为

$$\hat y = \sigma(z) = \frac{1}{1 + exp(-w^Tx)}$$

为方便推导，记录中间变量$z$

$$z=w^Tx+b=w_1x_1+\dots+w_nx_n+b$$

则有

$$\hat y=\sigma(z)=\frac{1}{1+exp(-z)}$$

交叉熵损失形式为

$$-L(w,b)=yln\hat y + (1-y)ln(1-\hat y)$$

sigmoid导数形式比较简洁

$$\sigma'(z) = \sigma(z)(1 - \sigma(z))=\hat y(1-\hat y)$$

据此那么不难得出

$$\frac{\partial\hat y}{\partial w_i}=\hat y(1-\hat y)x_i$$

代入上式，对损失函数求导，详细步骤如下

$$\begin {align}
-\frac{\partial L(w, y)}{\partial w_i} 
    &= y\cdot\frac{1}{\hat y}\frac{\partial\hat y}{\partial w_i} + (1-y)\frac{1}{1-\hat y}\frac{\partial(1-\hat y)}{\partial w_i} \\
    &= y\cdot\frac{1}{\hat y}\frac{\partial\hat y}{\partial w_i} - (1-y)\frac{1}{1-\hat y}\frac{\partial\hat y}{\partial w_i} \\
    &= y(1-\hat y)x_i - \hat y(1-y)x_i \\
    &= (y - \hat y)x_i
\end {align}$$

即

$$\frac{\partial L(w, y)}{\partial w_i} = (\hat y-y)x_i$$

结果非常intuitive，即预测值与真实值diff越大，梯度越大，更新越快。


