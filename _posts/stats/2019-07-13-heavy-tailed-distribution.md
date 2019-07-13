---
layout: post
title:  Heavy Tailed Distribution
date:   2019-07-13 12:00:00
category: "stats"
keywords: heavy-tailed distribution, 重尾分布
---

Heavy Tailed Distribution（重尾分布）是一系列很常见的分布，有一些特有的性质。

> A heavy tailed distribution has a tail that’s **heavier than an exponential distribution** (Bryson, 1974). In other words, a distribution that is heavy tailed goes to zero slower than one without heavy tails; there will be more bulk under the curve of the PDF. Heavy tailed distributions **tend to have many outliers with very high values**. The heavier the tail, the larger the probability that you’ll get one or more disproportionate values in a sample.

![heavy-tailed-300x178.png (300×178)](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2016/05/heavy-tailed-300x178.png)

重尾分布

分布特点：异常值较多，一些样本统计量会倾斜，**mean**可能非常misleading，被异常值带的很高；**sample variance**一般会比较大；同时**sample mean**会低估**polulation mean**；同时中心极限定理不work。

常见重尾分布

+ LogNormal Distribution
+ Pareto Distribution
+ Zipf Distribution
+ Student’s t Distribution
+ Cauchy Distribution

看其分布图示，如下两个分别是[LogNormal分布](https://www.statisticshowto.datasciencecentral.com/lognormal-distribution/)和[Cauchy分布](https://www.statisticshowto.datasciencecentral.com/cauchy-distribution-2/)。

![Probability distribution function of log-normal distribution](https://upload.wikimedia.org/wikipedia/commons/a/ae/PDF-log_normal_distributions.svg)

![450px-Cauchy_pdf.svg.png (450×360)](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Cauchy_pdf.svg/450px-Cauchy_pdf.svg.png)

Refs

+ [Heavy-tailed distribution - Wikipedia](https://en.wikipedia.org/wiki/Heavy-tailed_distribution)
+ [Heavy Tailed Distribution & Light Tailed Distribution: Definition](https://www.statisticshowto.datasciencecentral.com/heavy-tailed-distribution/)
+ [Microsoft PowerPoint - 2013-SIGMETRICS-heavytails.pptx](http://users.cms.caltech.edu/~adamw/papers/2013-SIGMETRICS-heavytails.pdf)



