---
layout: post
title:  正定矩阵
date:   2019-07-24 12:00:00
category: "math-la"
keywords: positive definite matrix, 正定矩阵
---

正定/半正定矩阵是线性代数中很常见的概念，其定义如下

> In linear algebra, a symmetric $n\times n$ real matrix $M$ is said to be positive definite if the scalar $X^TMX$ is strictly positive for every non-zero column vector $X$ of $n$ real numbers. 

$$X^TMX \gt 0$$

其中$X$是向量，$M$是变换矩阵。这样理解正定/半正定，矩阵中$MX$表示对$X$进行**线性变换**，变换后记做$Y=MX$，则上式可以写成

$$X^TY \gt 0$$

其实就是和变化后的向量內积。

$$\cos (\theta)=\frac{X^{T} Y}{\|X\| *\|Y\|}$$

正定、半正定矩阵「直觉上」其代表一个向量与经过该矩阵变换后的向量夹角小于90度！

从几何角度的理解，可以将正定矩阵看做n维空间的一个椭球，其中

+ 椭球的轴向，表示特征向量
+ 椭球的轴长，表示特征值「特征值都大于零」

Refs

+ [Positive Definite Matrix](http://slpl.cse.nsysu.edu.tw/chiaping/la/pdm.pdf)
+ [矩阵的正定及半正定理解](https://www.zhihu.com/question/22098422)


