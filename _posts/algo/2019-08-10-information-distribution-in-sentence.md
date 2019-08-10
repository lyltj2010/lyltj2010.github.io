---
layout: post
title:  文本中的信息分布
date:   2019-08-10 12:00:00
category: "algo"
keywords: information distribution, sentence
---

文本包含信息，其信息来源于词及词的顺序，二者分别贡献多少信息呢？

在李航老师的一个分享**Deep Learning for Matching in Search and Recommendation**看到这个问题的探讨，挺有意思。

一个句子包含的信息大致有两个来源，一是Choice of Words；一是Order of Words。从信息论角度简单估算，假设

+ Size of vocabulary = 10,000
+ Average sentence length = 20

其信息量Rough contributions of information in bits

+ From the selection of words: $log2(10000^{20})=265.75$
+ From the order of words: $log2(20!)=61.08$

不难看出，词之间的顺序包含大约10%的信息量，其余信息量在词的选择

> Over 80% of the potential information in language being in the choice of words without regard to the order in which they appear.


