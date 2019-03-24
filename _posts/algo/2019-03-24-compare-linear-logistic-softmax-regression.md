---
layout: post
title:  Linear/Logistic/Softmax Regression对比
date:   2019-03-24 12:00:00
category: "algo"
keywords: glm, regression, ml
---

Linear/Logistic/Softmax Regression是常见的机器学习模型，且都是广义线性模型的一种，有诸多相似点，详细对比之。

### 概述

Linear Regression是回归模型，Logistic Regression是二分类模型，Softmax Regression是多分类模型，但三者都属于广义线性「输入的线性组合」模型「GLM」。

其中Softmax Regression可以看做Logistic Regression在多类别上的拓展。

> Softmax Regression (synonyms: Multinomial Logistic, Maximum Entropy Classifier, or just Multi-class Logistic Regression) is a generalization of logistic regression that we can use for multi-class classification (under the assumption that the classes are **mutually exclusive**).

### 符号约定

+ 样本 $(x^{(i)}, y^{(i)})$
+ 样本数 $m$
+ 特征维度 $n$
+ Linear Regression输出 $y^{(i)}$
+ Logistic Regression类别 $y^{(i)}\in\{0,1\}$
+ Softmax Regression类别 $y^{(i)}\in\{1,\ldots,K\}$
+ Softmax Regression类别数 $K$
+ 损失函数 $J(\theta)$
+ Indicator函数 $I\{boolean\}$

### 模型参数对比

Linear Regression，维度为$(n \cdot 1)$的向量

$$\theta = \begin{bmatrix}
  \vert \\
  \theta \\
  \vert
\end{bmatrix}
$$

Logistic Regression，维度为$(n \cdot 1)$的向量

$$\theta = \begin{bmatrix}
  \vert \\
  \theta \\
  \vert
\end{bmatrix}
$$

Softmax Regression，维度为$(n \cdot K)$的矩阵

$$\theta = \begin{bmatrix}
  \vert & \vert & \vert & \vert \\
  \theta^{(1)} & \theta^{(2)} & \dots & \theta^{(K)} \\
  \vert & \vert & \vert & \vert \\
\end{bmatrix}
$$

### 模型输出对比

Linear Regression输出样本的得分「标量」。

$$h_\theta(x) = \theta^Tx$$

Logistic Regression输出正样本的概率「标量」。

$$h_\theta(x) = P(y = 1 | x; \theta) = \frac{1}{1+\exp(-\theta^Tx)}$$

Softmax Regression输出为$K$个类别的概率「向量」。

$$
h_\theta(x) = \begin{bmatrix}
  P(y = 1 | x; \theta) \\
  P(y = 2 | x; \theta) \\
  \vdots \\
  P(y = K | x; \theta)
\end{bmatrix}
= \frac{1}{\sum_{k=1}^{K}{\exp(\theta^{(k)\top}x)}}
\begin{bmatrix}
  \exp(\theta^{(1)T} x) \\
  \exp(\theta^{(2)T} x) \\
  \vdots \\
  \exp(\theta^{(K)T} x) \\
\end{bmatrix}
$$

### 损失函数对比

Linear Regression是回归问题，损失函数一般取平方误差；Logistic/Softmax Regression是分类问题，损失函数一般用交叉熵。

分类问题，对样本$(x, y)$，模型输出在类别上的概率分布，可统一表示为条件概率$P(y\vert x)$，可以直接写出交叉熵表达式，也可以通过极大似然法则导出，最终效果一样。

Linear Regression。

$$J(\theta) = \frac{1}{2} \sum_{i=1}^m (h_\theta(x^{(i)} - y^{(i)}))^2$$

Logistic Regression。条件概率可以表示为

$$
\begin{align}
P(y|x) &=
    \begin{cases}
      h_\theta(x), && y = 1 \\
      1 - h_\theta(x), && y = 0
    \end{cases} \\
    &= h_\theta(x)^y(1-h_\theta(x))^{(1-y)} \\
    &= I\{y=1\}h_\theta(x) + I\{y=0\}(1-h_\theta(x)) \\
    &= I\{y=1\}P(y=1\vert x;\theta) + I\{y=0\}P(y=0\vert x;\theta)
\end{align}
$$

对所有训练样本，损失函数为

$$
\begin{align}
J(\theta) &= - \left[ \sum_{i=1}^{m} \sum_{k=0}^{1} I\left\{y^{(i)} = k\right\} \log P(y^{(i)} = k | x^{(i)} ; \theta) \right] \\
&= - \left[ \sum_{i=1}^m   (1-y^{(i)}) \log (1-h_\theta(x^{(i)})) + y^{(i)} \log h_\theta(x^{(i)}) \right]
\end{align}
$$

Softmax Regression。条件概率可以表示为

$$
P(y|x) = I\{y=1\}P(y=1\vert x; \theta) + \dots + I\{y=K\}P(y=K\vert x; \theta)
$$

对所有训练样本，损失函数为

$$
\begin{align}
J(\theta)
&= - \left[ \sum_{i=1}^{m} \sum_{k=1}^{K}  I\left\{y^{(i)} = k\right\} logP(y^{(i)}=k|x^{(i)};\theta)\right] \\
&= - \left[ \sum_{i=1}^{m} \sum_{k=1}^{K}  I\left\{y^{(i)} = k\right\} \log \frac{\exp(\theta^{(k)\top} x^{(i)})}{\sum_{j=1}^K \exp(\theta^{(j)\top} x^{(i)})}\right]
\end{align}
$$

对比式子Logistic/Softmax Regression，二者的损失函数形式完全一致，就是**交叉熵损失**。真实概率分布$p$和预估概率分布$q$的交叉熵为

$$H(p,q) = - \sum_x p(x) \log q(x)$$

+ 对Logistic Regression来说，真实概率分布为$[1, 0]$或$[0, 1]$
+ 对Softmax Regression来说，真实概率分布为$[1,0,0]$、$[0,1,0]$或$[0,0,1]$

### 梯度对比

Linear/Logistic/Softmax Regression都是广义线性模型的一种，其形式都极其相似，包括梯度。

Linear Regression梯度

$$\nabla_\theta J(\theta) = \sum_{i=1}^m x^{(i)}(h_\theta(x^{(i)}) - y^{(i)})$$

其中$h_\theta(x) = \theta^Tx$。

Logistic Regression梯度

$$\nabla_\theta J(\theta) = \sum_{i=1}^m x^{(i)}(h_\theta(x^{(i)}) - y^{(i)})$$

其中$h_\theta(x) = \sigma(\theta^Tx)$。

Softmax Regression梯度

$$\nabla_{\theta^{(k)}} J(\theta) = \sum_{i=1}^m x^{(i)} [P(y^{(i)} = k | x^{(i)}; \theta) - I(y^{(i)} = k)]$$

其中预测结果见上文**模型输出对比**内容，方便表示，分别对$\theta^{k}$求导。

梯度形式非常的**Intuitive**，更新尺度**正比于误差项**！

> The magnitude of the update is proportional to the error term $h_\theta(x^{(i)}) - y^{(i)}$; thus, for instance, if we are encountering a training example on which our prediction nearly matches the actual value of $y^{(i)}$,  then we ﬁnd that there is little need to change the parameters; in contrast, a larger change to the parameters will be made if our prediction $h_\theta(x^{(i)})$ has a large error (i.e., if it is very far from $y^{(i)}$).


