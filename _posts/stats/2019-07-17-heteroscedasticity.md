---
layout: post
title:  Heteroscedasticity异方差
date:   2019-07-17 12:00:00
category: "stats"
keywords: box cox transformation, power transformation
---

Heteroscedasticity「异方差」是相对于Homoscedastic「同方差」而言，其定义如下
> Heteroscedasticity refers to data with **unequal variability** (scatter) across a set of second, predictor variables.

如果出现异方差，一般回归分析会受影响。简单讲是variability（常以variance衡量）沿着某个预测变量，不是恒定的，如果作图「预测变量与目标变量」，典型的会呈现**锥形**的散点图

![Heteroscedasticity.png (556×357)](https://upload.wikimedia.org/wikipedia/commons/a/a5/Heteroscedasticity.png)

一个例子，比如用家庭年收入预测在奢侈品上的花费，则奢侈品花费即是异方差的。

> As expected, there is a strong, positive association between income and spending.  Upon examining the residuals we detect a problem – the residuals are very small for low values of family income (almost all families with low incomes don’t spend much on luxury items) while there is great variation in the size of the residuals for wealthier families (some families spend a great deal on luxury items while some are more moderate in their luxury spending).  This situation represents heteroscedasticity because the size of the error varies across values of the independent variable. 

Refs

+ [Heteroscedasticity - Wikipedia](https://en.wikipedia.org/wiki/Heteroscedasticity)
+ [Heteroscedasticity: Simple Definition and Examples](https://www.statisticshowto.datasciencecentral.com/heteroscedasticity-simple-definition-examples/)
+ [Homoscedasticity - Statistics Solutions](https://www.statisticssolutions.com/homoscedasticity/)
+ [Confusing Stats Terms Explained: Heteroscedasticity](http://www.statsmakemecry.com/smmctheblog/confusing-stats-terms-explained-heteroscedasticity-heteroske.html)




