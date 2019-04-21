---
layout: post
title:  Python itertools模块详解
date:   2016-09-10 00:00:00
category: "python"
keywords: python,itertools,迭代模块
---


该模块包含了一系列处理可迭代对象(sequence-like)的函数，从此迭代更任性。  

迭代器有一些特点，比如lazy，也就是只有用到的时候才读入到内存里，这样更快更省内存；比如只能调用一次，会被消耗掉。


```python
import itertools as itls
```

### 合并迭代器: chain()与izip()
`chain()`函数接收n个可迭代对象，然后返回一个他们的合集的迭代器，纵向合并，上例子。


```python
for i in itls.chain([1,2,3],['a','b','c']):
    print i,
```

    1 2 3 a b c


`izip()`函数接收n个可迭代对象，然后将其合并成tuples，横向合并，功能类似`zip()`，只是返回的是iterator，而不是list。


```python
for i, j in itls.izip([1,2,3],['a','b','c']):
    print i, j
```

    1 a
    2 b
    3 c


### 切分迭代器: islice()
`islice()`函数接收一个迭代器，然后返回其切片，类似于`list`的`slice`切片操作。参数有`start`，`stop`和`step`，其中`start`和`step`参数时可选参数。


```python
print "Stop at 5:"
for i in itls.islice(itls.count(),5):
    print i,
```

    Stop at 5:
    0 1 2 3 4



```python
print "Start at 5, Stop at 10:"
for i in itls.islice(itls.count(),5,10):
    print i,
```

    Start at 5, Stop at 10:
    5 6 7 8 9



```python
print "By tens to 100:"
for i in itls.islice(itls.count(),0,100,10):
    print i,
```

    By tens to 100:
    0 10 20 30 40 50 60 70 80 90


### 复制迭代器: tee()
与Unix里`tee`方法语意一样，这里接收一个迭代器，然后返回n个(default 2)一样的迭代器。


```python
r = itls.islice(itls.count(),4)
i1, i2, i3 = itls.tee(r,3) # i1 and i2, like a copy

for i, j, k in itls.izip(i1,i2,i3):
    print i, j, k
```

    0 0 0
    1 1 1
    2 2 2
    3 3 3


有一点值得注意，初始的iterator不宜继续使用，如果你使用(consume)，那新的迭代器就不会产生这些值了，见例子。


```python
r = itls.islice(itls.count(),4)
i1, i2 = itls.tee(r)
for i in r:
    print 'r:', i
    if i > 0:
        break
for i in i1:
    print 'i1:', i

for i in i2:
    print 'i2:', i
```

    r: 0
    r: 1
    i1: 2
    i1: 3
    i2: 2
    i2: 3


可以看出，初始迭代器消耗了0,1，在新产生的迭代器里，就不会出现这些值了。

### Map迭代器
`imap()`函数对迭代器进行转换，类似于python内置的`map()`函数。下例把`xrange(5)`乘以2。


```python
print "Doubles:"
for i in itls.imap(lambda x: 2*x, xrange(5)):
    print i,
```

    Doubles:
    0 2 4 6 8


`imap()`可以同时接受多个可迭代对象，进行`map`操作。


```python
print "Multiples:"
for i in itls.imap(lambda x,y:(x, y, x*y), xrange(5),xrange(5,10)):
    print '%d * %d = %d' % i
```

    Multiples:
    0 * 5 = 0
    1 * 6 = 6
    2 * 7 = 14
    3 * 8 = 24
    4 * 9 = 36


`starmap()`与`imap()`功能类似，但有点区别，`starmap()`可以从`tuple`里解析出多个参数，而`imap()`只能从多个课迭代对象获取多个参数，看例子。


```python
values = [(0, 5), (1, 6), (2, 7), (3, 8), (4, 9)]
for i in itls.starmap(lambda x,y:(x,y,x*y), values):
    print '%d * %d = %d' % i
```

    0 * 5 = 0
    1 * 6 = 6
    2 * 7 = 14
    3 * 8 = 24
    4 * 9 = 36


### 产生新迭代器
`count()`，`cycle()`和`repeat()`函数提供了几个产生迭代器的便捷操作，非常nice。

#### `count()`
产生连续的整数，有下限(默认0)，没有上限(可以用xrange())。


```python
for i in itls.izip(itls.count(1),['a','b','c']):
    print i
```

    (1, 'a')
    (2, 'b')
    (3, 'c')


#### `cycle()`
无限重复给定的可迭代对象。


```python
i = 0
for item in itls.cycle(['a','b','c']):
    i += 1
    if i == 7:
        break
    print (i, item)
```

    (1, 'a')
    (2, 'b')
    (3, 'c')
    (4, 'a')
    (5, 'b')
    (6, 'c')


#### `repeat()`
重复给定的值，n次。


```python
for i in itls.repeat('over-and-over',3):
    print i
```

    over-and-over
    over-and-over
    over-and-over


当需要给一个序列添加一个不变对象的时候，用`repeat()`和`imap()`或`izip()`的combo特别有用。


```python
for i,s in itls.izip(itls.count(), itls.repeat('over-and-over',3)):
    print i, s
```

    0 over-and-over
    1 over-and-over
    2 over-and-over



```python
for i in itls.imap(lambda x,y:(x,y,x*y),itls.repeat(2),xrange(5)):
    print '%d * %d = %d' % i
```

    2 * 0 = 0
    2 * 1 = 2
    2 * 2 = 4
    2 * 3 = 6
    2 * 4 = 8


### 过滤迭代器
类似于内置的`filter()`功能，实现迭代器的筛选。

#### `dropwhile()`
对item进行判断，如果判断为`True`，继续；如果判断为`False`，不继续drop了，只`drop`之前判断为`True`的，保留之后的所有items，不再进行判断，全部保留。


```python
def should_drop(x):
    print 'Testing:', x
    return x < 1
for i in itls.dropwhile(should_drop,[ -1, 0, 1, 2, 3, 1, -2 ]):
    print 'Yielding:', i
```

    Testing: -1
    Testing: 0
    Testing: 1
    Yielding: 1
    Yielding: 2
    Yielding: 3
    Yielding: 1
    Yielding: -2


#### `takewhile()`
与`dropwhile()`功能相反，当判断为`False`的时候，就不继续take了，只保留之前判断为真item。


```python
def should_take(x):
    print 'Testing:', x
    return x < 2
for i in itls.takewhile(should_take,[ -1, 0, 1, 2, 3, 4, 1, -2 ]):
    print 'Yielding:', i
```

    Testing: -1
    Yielding: -1
    Testing: 0
    Yielding: 0
    Testing: 1
    Yielding: 1
    Testing: 2


#### `ifilter()`
`dropwhile()`和`takewhile()`都不是对所有元素过滤，而`ifilter()`则尽职尽责地对所有元素过滤。与其对应的是`ifilterfalse()`，只保留判定为`False`的item。


```python
def check_item(x):
    print 'Testing:', x
    return x < 1
for i in itls.ifilter(check_item, [ -1, 0, 1, 2, 3, -2 ]):
    print 'Yielding:', i
```

    Testing: -1
    Yielding: -1
    Testing: 0
    Yielding: 0
    Testing: 1
    Testing: 2
    Testing: 3
    Testing: -2
    Yielding: -2


### Group迭代器
> `groupby(iterable[, keyfunc])` Create an iterator which returns(key, sub-iterator) grouped by each value of key(value)  

按给定的`key`对可迭代对象分组，返回`sub-iterator`。


```python
things = [("animal", "bear"), ("animal", "duck"), ("plant", "cactus"), ("vehicle", "speed boat"), ("vehicle", "school bus")]
```

`groupby()`接收两个参数，一个`the data to group`，一个是`the function to group it with`。


```python
for key, group in itls.groupby(things, lambda x: x[0]):
    print key, group
```

    animal <itertools._grouper object at 0x10bce2150>
    plant <itertools._grouper object at 0x10bce2190>
    vehicle <itertools._grouper object at 0x10bce2150>


可以看出，分组后，返回三个`sub-iterator`，我们可以再用一层循环访问。


```python
for key, group in itls.groupby(things, lambda x:x[0]):
    for thing in group:
        print "A %s is a %s." % (thing[1], key)
    print ""
```

    A bear is a animal.
    A duck is a animal.
    
    A cactus is a plant.
    
    A speed boat is a vehicle.
    A school bus is a vehicle.
    


**且慢**，值得注意的一点是，在group之前，务必要按key排序，因为`groupby`方法遍历对象，当key变化的时候，就会新产生一个group。有例为证！


```python
things = [("animal", "bear"), ("plant", "cactus"), ("animal", "duck")]
```


```python
for key, group in itls.groupby(things, lambda x: x[0]):
    print key, group
```

    animal <itertools._grouper object at 0x10bce2410>
    plant <itertools._grouper object at 0x10bce2490>
    animal <itertools._grouper object at 0x10bce2410>


本来是应该分两组的，结果是三组，就是因为没有排序。


```python
new_things = sorted(things,key=lambda x: x[0])
for key, group in itls.groupby(new_things, lambda x:x[0]):
    print key, group
```

    animal <itertools._grouper object at 0x10bce2350>
    plant <itertools._grouper object at 0x10bce2410>


这个看上去就对了！

