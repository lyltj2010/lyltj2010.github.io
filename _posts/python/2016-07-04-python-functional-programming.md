---
layout: post
title:  Python函数式编程
date:   2016-07-04 00:00:00
category: "python"
keywords: python,函数式编程
---

用python也可以写出函数式风格的代码。

### Map

`map()`函数接收两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回，比循环更简洁，更易读。

```python
# default function
name_len = map(len, ["Sam", "John", "Ned Stark"])
print name_len
```

    [3, 4, 9]


```python
# lambda function
squares = map(lambda x: x * x, range(9))
print squares
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64]

```python
# self defined function
def toUpper(item):
      return item.upper()
 
upper_name = map(toUpper, ["sam", "john", "ned stark"])
print upper_name
```

    ['SAM', 'JOHN', 'NED STARK']


### Reduce
reduce把一个函数作用在一个序列[x1, x2, x3...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算(相当于计算结果后把这个值再放回去)，其效果就是：  

`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`


```python
# 累加
print reduce(lambda x, y: x+y, [1,2,3,4])
```

    10

```python
# 累乘
print reduce(lambda x, y: x*y, [1, 2, 3,4])
```

    24

```python
# 要把序列[1,2,3,4]变换成整数1234
print reduce(lambda x,y: 10*x + y, [1,2,3,4])
```

    1234


### Filter

`filter` 函数的功能相当于过滤器。调用一个布尔函数`bool_func`来迭代遍历每个`seq`中的元素；返回一个使`bool_seq`返回值为`true`的元素的序列。  

和`map()`类似，`filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。


```python
# 剔除偶数
def is_odd(n):
    return n % 2 == 1

filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15])
```


    [1, 5, 9, 15]


### All
当可迭代对象(比如list)里所有元素都为`True`的时候，返回`True`，类似对所有元素做`and`操作，但注意当可迭代对象为空时，仍然返回`True`。等级于：

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```


```python
all(['a', 'b', 'c'])  #列表list，元素都不为空或0
```

    True

```python
all([0, 1, 2, 3])  #列表list，存在一个为0的元素
```

    False

```python
all(('a', 'b', '', 'd'))  #元组tuple，存在一个为空的元素
```

    False

```python
all([]) # 空列表
```

    True

### Any

当可迭代对象有任何一个元素为`True`时，返回`True`，否则返回`False`，当可迭代对象为空时，返回`False`.  

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

```python
any([0,1,2])
```

    True

```python
any([0, '', False])  #列表list,元素全为0,'',false
```

    False


### Sorted

python内置的`sorted()`函数就可以对`list`进行排序:  

`sorted(iterable, cmp=None, key=None, reverse=False)`


```python
lst = [36, 5, -12, 9, -21]
```

```python
sorted(lst)
```

    [-21, -12, 5, 9, 36]

`sorted()`函数也是一个高阶函数，它还可以接收一个key函数来实现自定义的排序，例如按绝对值大小排序，其实相当于用传入的函数(比如abs)对list进行map，作为key，然后按key排序，返回list。  

keys排序结果 => [5, 9,  12,  21, 36]  
===========|==|==|==|==|  
最终结果=====> [5, 9, -12, -21, 36]


```python
sorted(lst,key=abs)
```

    [5, 9, -12, -21, 36]

```python
# 忽略大小写
sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)
['about', 'bob', 'Credit', 'Zoo']
```

    ['about', 'bob', 'Credit', 'Zoo']

```python
# 逆序
sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
['Zoo', 'Credit', 'bob', 'about']
```

    ['Zoo', 'Credit', 'bob', 'about']


### Pipeline

该部分来自[酷壳函数式编程](http://coolshell.cn/articles/10822.html)，写的真好。

这个技术的意思是，把函数实例成一个一个的action，然后，把一组action放到一个数组或是列表中，然后把数据传给这个action list，数据就像一个pipeline一样顺序地被各个函数所操作，最终得到我们想要的结果。  

pipeline 管道借鉴于Unix Shell的管道操作——把若干个命令串起来，前面命令的输出成为后面命令的输入，如此完成一个流式计算。（注：管道绝对是一个伟大的发明，他的设哲学就是KISS – 让每个功能就做一件事，并把这件事做到极致，软件或程序的拼装会变得更为简单和直观。这个设计理念影响非常深远，包括今天的Web Service，云计算，以及大数据的流式计算等等）

我们先来看一个如下的程序，这个程序的`process()`有三个步骤：

1. 找出偶数。
2. 乘以3
3. 转成字符串返回


```python
def process(num):
    if num % 2 != 0:
        return
    num = num * 3
    num = 'The Number: %s' % num
    return num
 
nums = [1, 2, 3, 4, 5]
 
for num in nums:
    print process(num)
```

    None
    The Number: 6
    None
    The Number: 12
    None


我们可以看到，输出的并不够完美，另外，代码阅读上如果没有注释，你也会比较晕。下面，我们来看看函数式的pipeline应该怎么写？  

不用这样嵌套`pipeline = convert_to_string(multiply_by_three(even_filter(nums)))`


```python
# 用map reduce filter等
def even_filter(nums):
    return filter(lambda x: x%2==0, nums)

def multiply_by_three(nums):
    return map(lambda x: x*3, nums)

def convert_to_string(nums):
    return map(lambda x: 'The Number: %s' % x,  nums)

def pipeline_func(data, fns):
    return reduce(lambda a, x: x(a), fns, data)

nums = [1, 2, 3, 4]
pipeline_func(nums, [even_filter, multiply_by_three, convert_to_string])
```

    ['The Number: 6', 'The Number: 12']


### 参考  

- [廖雪峰函数式编程](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317848428125ae6aa24068b4c50a7e71501ab275d52000)
- [python interview](https://github.com/taizilongxu/interview_python)
- [酷壳函数式编程](http://coolshell.cn/articles/10822.html)
