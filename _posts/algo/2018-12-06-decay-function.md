---
layout: post
title:  衰减函数
date:   2018-12-06 12:00:00
category: "algo"
keywords: decay function, 衰减函数, 指数
---

最近做策略需要用到一些具有衰减性质的函数，最好有如下性质

+ 支持平滑/线性地衰减
+ 支持从某值开始衰减
+ 支持衰减速度控制

这些性质挺常用的，比如对时间衰减，再比如对距离做衰减等。直观的可以想到线性衰减，或者指数衰减，方向是对的，但需要调整。

拿指数衰减举例exp(-t)，其值很快值会衰减到接近0，衰减力度不可控，需要加入参数，能精细控制。ES里内置几个衰减函数，恰巧满足这些需求，见文档[Function Score Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-function-score-query.html)。

## 衰减函数
  

高斯衰减(GAUSS)

$$y = exp\big(\frac{max(0, |x-origin|-offset)^2}{\frac{scale^2}{ln(decay)}}\big)$$

指数衰减(EXP)

$$y = exp\big(\frac{ln(decay)}{scale}*max(0, |x-origin|-offset)\big)$$

线性衰减(LINER)

$$y = max\Big(1 - \big(\frac{max(0, |x-origin|-offset)}{\frac{scale}{1.0-decay}}\big), 0\Big)$$


其衰减曲线见下图

![algo-decay-function](https://images-1256734305.cos.ap-beijing.myqcloud.com/algo-decay-function.png)

其中参数含义想通

+ origin表示衰减开始的中心
+ offset 表示不衰减的距离
+ decay表示期望衰减到的某值，比如0.5
+ scale表示衰减到期望值的需要的跨度

上述函数可以轻松地，从某点开始衰减，并在特定位置衰减到某值，很直观地控制其衰减行为。


## 简单实现

```python
def exp(x, origin, offset, scale, decay):
    """
    指数衰减函数
    """
    result = math.e ** (math.log(decay, math.e) / float(scale) * max(0, abs(x - origin) - offset))

    return result


def guass(x, origin, offset, scale, decay):
    """
    高斯衰减函数
    """
    result = math.e ** (max(0, abs(x - origin) - offset) ** 2 / (float(scale * scale) / math.log(decay, math.e)))

    return result


def linear(x, origin, offset, scale, decay):
    """
    线性衰减函数
    """
    result = max(0, 1 - (max(0, abs(x - origin) - offset) / (scale / (1.0 - decay))))

    return result
```

