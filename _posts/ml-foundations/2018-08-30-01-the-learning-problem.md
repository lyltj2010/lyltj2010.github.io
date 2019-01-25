---
layout: post
title:  01 The Learning Problem
date:   2018-08-30 00:00:00
category: "ml-foundations"
keywords: learning-from-data,machine-learning
---

本系列文章为林軒田老师[機器學習基石上](https://www.coursera.org/learn/ntumlone-mathematicalfoundations/home/welcome)课程学习笔记，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/01_handout.pdf)。

## 课程主线

+ When Can Machines Learn? (illustrative + technical)
+ Why Can Machines Learn? (theoretical + illustrative)
+ How Can Machines Learn? (technical + practical)
+ How Can Machines Learn Better? (practical + theoretical)

也就是要依次回答：何时可以用机器学习？为何可以机器学习？怎样机器学习？怎样更好地机器学习？构建一幅大Picture！

## 机器学习应用场景

首先有机器学习不同侧面的定义：

+ Improving some performance measure with experience computed from data
+ Use data to compute hypothesis $g$ that approximates target $f$

Key Essence of Machine Learning: 

+ A pattern exists(比如随机数生成不可学习)
+ We cannot pin it down mathematically(否则直接公式表示)
+ We have data on it

思考机器学习的这三个key essence，界定遇到的问题是否可用机器学习方法解决。  

以下是一些典型的应用场景：

+ When human cannot program the system manually, like navigating on Mars
+ When human cannot ‘deﬁne the solution’ easily, like speech/visual recognition
+ When needing rapid decisions that humans cannot do, like high-frequency trading
+ When needing to be user-oriented in a massive scale, like consumer-targeted marketing

## 问题的Formulation

首先明确其中五个元素：

+ 定义input space $x \in X$
+ 定义output space $y \in Y$
+ Target function: unknown pattern to be learned
+ Training examples: $D={(x1,y1), (x2,y2),\dots, (xN,yN)}$
+ Hypothesis: skill with hopefully good performance

最终机器学习Formulation为：

> 利用target function生成的training examples数据，通过learning algorithm从hypothesis set里找出 $g$ 使其尽可能接近target function $f$.

从上面可以看出一个假设，就是训练数据集$D$是从target function来的，为保证学习效果，$D$需要足够representative。
