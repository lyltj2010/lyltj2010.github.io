---
layout: post
title:  Box Cox变换
date:   2019-07-16 12:00:00
category: "stats"
keywords: box cox transformation, power transformation
---

Box Cox变换是将数据正态化比较有力的工具。

> A Box Cox transformation is a way to transform **non-normal** dependent variables into a **normal** shape.

使数据**more normal distribution-like**，而且**stabilize variance**，性质较好。很多模型对数据分布有正态性假设，比如线性回归，此时对数据做正态变换很有必要。变换公式为

$$
y(\lambda)=\left\{\begin{array}{ll}{\frac{y^{\lambda}-1}{\lambda},} & {\text { if } \lambda \neq 0} \\ {\log y,} & {\text { if } \lambda=0}\end{array}\right.
$$

Intuition

公式中$\lambda$是可以优化参数，像R或Python中都有类似的实现。当$\lambda=0$时，是常见的对数变换；取其它值也是对数据做平移和拉伸。

其中对数变换，会将小数据之间的diff放大（inflate），将大数据之间diff缩小（reduce），从而使常见的right skew的分布变换成正态分布，如下图所示

![transformed_distribution.jpg (576×384)](https://blog.minitab.com/hubfs/Imported_Blog_Media/transformed_distribution.jpg)

![log_function.jpg (437×313)](https://blog.minitab.com/hubfs/Imported_Blog_Media/log_function.jpg)

看一个变换后的图例

![transformation.jpg (430×611)](https://blog.minitab.com/hubfs/Imported_Blog_Media/transformation.jpg)

注意Box Cox只在幂函数和对数函数中**搜索**最好的变换，但不能保证一定能达到正态性，变换完需要看看Q-Q Plot或者Normal Probability Plot重新Check下。

Refs

+ [Box Cox Transformation](https://www.statisticshowto.datasciencecentral.com/box-cox-transformation/)
+ [Power transform - Wikipedia](https://en.wikipedia.org/wiki/Power_transform)
+ [How Could You Benefit from a Box-Cox Transformation?](https://blog.minitab.com/blog/applying-statistics-in-quality-projects/how-could-you-benefit-from-a-box-cox-transformation)



