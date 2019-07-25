---
layout: post
title:  Scala Collections
date:   2019-07-26 12:00:00
category: "cs"
keywords: scala, collections
---

Scala和Java中的collection都很常用，参考几张图对比一下。

Scala集合分不可变集合和可变集合，其通用接口如下图

![collections-diagram.svg](https://docs.scala-lang.org/resources/images/tour/collections-diagram.svg)

主要分三大类，Seq、Set、Map，其中IndexedSeq支持常数时间复杂度的随机访问，而LinearSeq随机访问性能较差。

不可变集合，常见的有HashMap、Set、List等，其在整个集合中的位置如下图

![collections-immutable-diagram.svg](https://docs.scala-lang.org/resources/images/tour/collections-immutable-diagram.svg)

可变集合，常见的如ArrayBuffer等，类关系如图

![collections-mutable-diagram.svg](https://docs.scala-lang.org/resources/images/tour/collections-mutable-diagram.svg)

图示标识，粗线表示默认实现

![collections-legend-diagram.svg](https://docs.scala-lang.org/resources/images/tour/collections-legend-diagram.svg)

Java的集合框架也很丰富，类类之间关系如下图

![arts-java-collection](https://images-1256734305.cos.ap-beijing.myqcloud.com/arts-java-collection.png)

Refs

+ [Mutable and Immutable Collections](https://docs.scala-lang.org/overviews/collections/overview.html)
+ [Scala Documentation](https://docs.scala-lang.org/overviews/collections/introduction.html)




