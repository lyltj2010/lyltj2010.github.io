---
layout: post
title:  稀疏矩阵
date:   2019-07-19 12:00:00
category: "math-la"
keywords: sparse matrix, matrix, CRS
---

Sparse Matrix和Dense Mastrix不同，其中大部分元素为零，利用该特性，省略0的存储，可以更高效。以下是几种经典表达方式。

稀疏矩阵例子例子

$$
\left(\begin{array}{cccccc}{10} & {20} & {0} & {0} & {0} & {0} \\ {0} & {30} & {0} & {40} & {0} & {0} \\ {0} & {0} & {50} & {60} & {70} & {0} \\ {0} & {0} & {0} & {0} & {0} & {80}\end{array}\right)
$$

**COO**

> COO(Coordinate list) stores a list of (row, column, value) tuples.

$$
\begin{array}{ccc}{row} & {col} & {val} \\ {0} & {0} & {10} \\ {0} & {1} & {20} \\ {1} & {1} & {30} \\ {1} & {3} & {40} \\ {2} & {2} & {50} \\ {2} & {3} & {60} \\ {2} & {4} & {70} \\ {3} & {5} & {80}\end{array}
$$

**DOK**

> DOK(Dictionary of keys) consists of a dictionary that maps (row, column)-pairs to the value of the elements.

$$
\begin{array}{ll}{\text {keys}} & {\text {vals}} \\ {(0,0)} & {10} \\ {(0,1)} & {20} \\ {(1,1)} & {30} \\ {(1,3)} & {40} \\ {(2,2)} & {50} \\ {(2,3)} & {60} \\ {(2,4)} & {70} \\ {(3,5)} & {80}\end{array}
$$

**CRS**

Compressed row storage行压缩，存储mxn的矩阵，分别存储A、IA和JA三个向量。对应行压缩的还有列压缩。

$$
\left(\begin{array}{cccccc}{10} & {20} & {0} & {0} & {0} & {0} \\ {0} & {30} & {0} & {40} & {0} & {0} \\ {0} & {0} & {50} & {60} & {70} & {0} \\ {0} & {0} & {0} & {0} & {0} & {80}\end{array}\right)
$$

其中A存储矩阵的非零值，其长度为nnz（number of non zeros）；IA存储每一行的非零值在A中的位置区间，左闭右开区间，比如该例子IA前两个值为0和2，表示A中的[0, 2)位置是第一行的非零值，其长度我m+1；JA存储非零值对应的列坐标，其长度为nnz。

```text
A = [ 10 20 30 40 50 60 70 80 ]
IA = [  0  2  4  7  8 ]
JA = [  0  1  1  3  2  3  4  5 ]
```

Refs

+ [Sparse matrix - Wikipedia](https://en.wikipedia.org/wiki/Sparse_matrix)
+ [Sparse matrices (scipy.sparse)](https://docs.scipy.org/doc/scipy/reference/sparse.html)




