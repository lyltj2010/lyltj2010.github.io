---
layout: post
title:  RecSys中的Graph Embedding
date:   2019-03-12 12:00:00
category: "paper"
keywords: graph embedding,recsys
---

阿里在2018KDD上发表一篇关于Graph Embedding在推荐方向应用的论文：Billion-scale Commodity Embedding for E-commerce Recommendation in Alibaba，工程实践价值较高，简记论文部分内容。

### 简介

论文基本思路是，基于用户行为，构建Item Graph，然后在Item Graph上随机游走，得到Item Sequence，借鉴Skip-Gram模型，同时融入side information，学习item的向量表达。

传统CF算法只考虑用户历史行为的商品共现「co-occurrence」信息，而在Item Graph上随机游走，可以捕捉商品之间高阶关系「higher-order similarities」。但学习稀疏商品「interaction很少」的Embedding仍然是一个问题，该论文利用Side Information「辅助信息，比如类目、品牌、价格等」缓解数据稀疏问题。

#### Item Graph构建

> Previous CF based methods only consider the co-occurrence of items, but ignore the sequential information, which can reflect users’ preferences more precisely.

即构建过程考虑Sequential Information，而非仅仅是共现。如下是一些实践经验

+ 数据清洗
    - 点击后停留时长小于1秒，视为误点击，剔除
    - 去除over-active用户点击行为 
+ 构建图
    - session-based
    - sequence-aware，两个item依次被点击视为一有向边
    - 边权重用频次表示

从用户行为序列，到Item Graph，到Random Walk序列以及应用Skip-Gram模型的示意流程如下图。

![paper-commodity-embedding-graph-embedding-overview](https://images-1256734305.cos.ap-beijing.myqcloud.com/paper-commodity-embedding-graph-embedding-overview.png)


#### Base Graph Embedding

有了Item Graph之后，DeepWalk思路相对直观。

> Use DeepWalk to learn the embedding of each node in a graph. They first generate sequences of nodes by running random walk in the graph, and then apply the Skip-Gram algorithm to learn the representation of each node in the graph.

从Item Graph中，能得出近邻矩阵$M$，其中$M_{ij}$表示节点$i$指向$j$的权重。由权重不难计算转移概率「边权重除以出度」。

$$
P(v_j|v_i) = \begin{cases}
  \frac{M_{ij}}{\sum_{j\in N_+(v_i)} M_{ij}}, && v_j\in N_+(v_i)\\
  0, && e_{ij} \notin E
\end{cases}
$$

其中$N_+{(v_i)}$表示节点的outlink neighbors。有了转移概率，随机游走便可得到游走序列「类似word2vec里的语料」，之后Skip-Gram模型即可得到节点向量表示。

#### GES & EGES

上述模型BGE可以学到所有商品向量表达，但对cold-start「those with no interactions of users」商品刻画不足。如何解决呢？论文给出答案是融入side information「类目、店铺、价格等」。这样做的Intuition是：side information相似的商品在embedding space中距离也应相近。

> Items with similar side information should be closer in the embedding space.

论文提供GES和EGES两种思路，其中GES将所有side information一视同仁「average pooling」，而EGES则对不同side information赋予不同权重「模型参数」，但二者模型结构基本一致。那接下来问题是：具体如何建模上述Intuition，融入side information呢？

![paper-commodity-embedding-framework](https://images-1256734305.cos.ap-beijing.myqcloud.com/paper-commodity-embedding-framework.png)

GES对$v$对应的$n+1$个向量采用average pooling策略，即

$$H_v = \frac{1}{n+1}\sum_{j=0}^n W_v^j$$

而EGES则将$n+1$向量的权重作为参数学习，即

$$H_v = \frac{\sum_{j=0}^n e^{a_v^j}W_v^j}{\sum_{j=0}^{n}e^{a_v^j}}$$

知道标签$y$之后，objective function定义为交叉熵

$$L(v,u,y) = -[ylog(\delta(H_v^T Z_u)) + (1-y)log(1-\delta(H_v^T Z_u))]$$

对应的算法伪代码如下

![paper-commodity-embedding-algorithm](https://images-1256734305.cos.ap-beijing.myqcloud.com/paper-commodity-embedding-algorithm.png)

相关符号

+ $v$ 表示节点「item」
+ $V$ 表示所有节点集合
+ $\lvert V \rvert$ 表示总节点个数
+ $d$ 表示Embedding向量维度
+ $n$ 表示side information的个数
+ $W^0_v$ 表示节点$v$对应Embedding
+ $W^s_v$ 表示节点$v$对应的第$s$个side information的Embedding
+ 其中$W_v^*$矩阵大小都是$\lvert V\rvert \times d$
+ $H_v$ 表示和side information聚合向量
+ $A\in R^{\lvert V\rvert\times (n+1)}$ 表示side info权重
+ $A_{ij}$ 表示$ith$节点$jth$ side info的权重
+ $a_v^j$ 表示节点$v$的第$jth$ side info的权重
+ $Z_u$ 表示节点$u$作为context node的向量表示

