---
layout: post
title:  12 Nonlinear Transformation
date:   2018-09-24 12:00:00
category: "ml-foundations"
keywords: nonlinear transformation
---

简要介绍非线性变换，见[详细课件](https://www.csie.ntu.edu.tw/~htlin/mooc/doc/12_handout.pdf)。

当非线性关系存在时，可能要考虑non-linear transformation，比如quadratic hypothesis set。主要考虑计算代价和泛化代价。

## Quadratic Hypothesis Set

常见的一种非线性变换。

![ml-foundations-quadratic-hypothesis-set](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-quadratic-hypothesis-set.png)

非线性变换，不仅要考虑计算代价，还要考虑泛化问题。当提取窥探数据的时候，可能会脑补地人为选择很多模型，要警惕。

![ml-foundations-danger-of-visual-choices](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-danger-of-visual-choices.png)

## Best Practice

复杂模型不一定好，不仅要考虑样本内误差，还要考虑泛化误差。总之，先尝试简单模型，问题不大。

![ml-foundations-structured-hypothesis-sets](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-structured-hypothesis-sets.png)

![ml-foundations-linear-model-first](https://images-1256734305.cos.ap-beijing.myqcloud.com/ml-foundations-linear-model-first.png)



