---
layout: post
title:  Python Collections模块解析
date:   2016-08-19 00:00:00
category: "python"
keywords: python,collections,python集合操作
---


`collections`模块提供了一些`python`内置数据类型的扩展，比如`OrderedDict`，`defaultdict`，`namedtuple`，`deque`，`counter`等，简单实用，非常值得学习了解。


```python
import collections
```

###  1. OrderedDict
顾名思义，有顺序的词典，次序不再是随机的。普通的`dict`不记录插入的顺序，遍历其值的时候是随机的，相反，`OrderedDict`记录插入的顺序，在迭代的时候可以看出差异。  

#### 遍历


```python
print 'Regular dictionary:'
d = {}
d['a'] = 'A'
d['b'] = 'B'
d['c'] = 'C'

for key, value in d.items():
    print key, value
```

    Regular dictionary:
    a A
    c C
    b B



```python
print 'OrderedDict:'
d = collections.OrderedDict()
d['a'] = 'A'
d['b'] = 'B'
d['c'] = 'C'

for key, value in d.items():
    print key, value
```

    OrderedDict:
    a A
    b B
    c C


#### 相等比较
比较两个词典是否相等，普通词典比较只看内容，内容相同即判定相等为真；而`OrderedDict`同时会考虑顺序，`item`被添加的顺序。


```python
print 'dict       :',
d1 = {}
d1['a'] = 'A'
d1['b'] = 'B'
d1['c'] = 'C'

d2 = {}
d2['b'] = 'B'
d2['a'] = 'A'
d2['c'] = 'C'

print d1 == d2
```

    dict       : True



```python
print 'OrderedDict:',
d1 = collections.OrderedDict()
d1['a'] = 'A'
d1['b'] = 'B'
d1['c'] = 'C'

d2 = collections.OrderedDict()
d2['b'] = 'B'
d2['a'] = 'A'
d2['c'] = 'C'

print d1 == d2

```

    OrderedDict: False


### 2. defaultdict
普通词典，当你访问没有的键值时，会抛出异常，用`defaultdict`，可以预先给定默认值，尤其默认值是需要做累积或聚合操作的时候(比如计数)。`defaultdict`接受一个参数`default_factory`，该函数负责返回特定的值，可以自定义，也可以用`list`(返回[ ]) `set(返回set())` 或`int(返回0)`，直接上例子说的比较清楚。  

`defaultdict`其实是继承`dict`类后。添加了`__missing__(key)`方法，用于处理`KeyError`异常。


```python
def default_factory():
    return 'This is default string value'
d = collections.defaultdict(default_factory)
print d['foo']
```

    This is default string value


这里没有定义`d['foo']`，但是可以访问，并返回值。下面看点更厉害的！

#### list
把`default_factory`设定为`list`可以方便地把一系列键值对`group`起来。默认会返回空的`list`，下面例子把相同的键`group`在一起。


```python
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(list)
for k, v in s:
    d[k].append(v)
    # simpler and faster than d.setdefault(k, []).append(v)
d.items()
```




    [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]



#### int
计数的时候特别方便，比如要统计每个键值出现多少次。


```python
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(int)
for k, v in s:
    d[k] += 1
d.items()
```




    [('blue', 2), ('red', 1), ('yellow', 2)]




```python
s = 'mississippi'
d = collections.defaultdict(int)
for k in s:
    d[k] += 1
d.items()
```




    [('i', 4), ('p', 2), ('s', 4), ('m', 1)]



#### set
和`list`功能类似，但返回`set()`,剔除了重复元素。


```python
s = [('red', 1), ('blue', 2), ('red', 3), ('blue', 4), ('red', 1), ('blue', 4)]
d = collections.defaultdict(set)
for k, v in s:
    d[k].add(v)
d.items()
```




    [('blue', {2, 4}), ('red', {1, 3})]



### 3. namedtuple
默认的`tuple`是用数字做索引的，而`namedtuple`是可以按名字访问，对`fields`很多，或者创建和使用场景离得比较远的情况，比较有用。


```python
bob = ('Bob', 30, 'male')
print 'Representation:', bob

jane = ('Jane', 29, 'female')
print '\nField by index:', jane[0]

print '\nFields by index:'
for p in [ bob, jane ]:
    print '%s is a %d year old %s' % p
```

    Representation: ('Bob', 30, 'male')
    
    Field by index: Jane
    
    Fields by index:
    Bob is a 30 year old male
    Jane is a 29 year old female


由于不同的`nametuple`不一样，我们要单独定义，同时按`name`访问(依然可以按数字访问)。


```python
# define namedtuple
Person = collections.namedtuple('Person','name age gender')

print 'Type of Person:', type(Person)
bob = Person(name='Bob', age=30, gender='male')
print '\nRepresentation:', bob

bob = Person('Bob',30,'male') # also supported
print 'Representation:', bob

jane = Person(name='Jane', age=29, gender='female')
print '\nField by name:', jane.name
print 'Field by name:', jane[0]
```

    Type of Person: <type 'type'>
    
    Representation: Person(name='Bob', age=30, gender='male')
    Representation: Person(name='Bob', age=30, gender='male')
    
    Field by name: Jane
    Field by name: Jane


### 4. deque
即`double-ended queue`，双向队列，支持任何一侧的`add`和`remove`操作。普通的`stack`和`queue`是`deque`的退化形式。  

当然，`deque`依然是`sequence`，所以一些列表类似的操作也是支持的。


```python
d = collections.deque('abcdefg')
print 'Deque:', d
print 'Length:', len(d)
print 'Left end:', d[0]
print 'Right end:', d[-1]

d.remove('c')
print 'remove(c)', d
```

    Deque: deque(['a', 'b', 'c', 'd', 'e', 'f', 'g'])
    Length: 7
    Left end: a
    Right end: g
    remove(c) deque(['a', 'b', 'd', 'e', 'f', 'g'])


#### populating
往队列`push`元素


```python
import collections

# Add to the right
d = collections.deque()
d.extend('abcdefg') # append with elements from the iterable
print 'extend    :', d
d.append('h')
print 'append    :', d

# Add to the left
d = collections.deque()
d.extendleft('abcdefg')
print 'extendleft:', d
d.appendleft('h')
print 'appendleft:', d
```

    extend    : deque(['a', 'b', 'c', 'd', 'e', 'f', 'g'])
    append    : deque(['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'])
    extendleft: deque(['g', 'f', 'e', 'd', 'c', 'b', 'a'])
    appendleft: deque(['h', 'g', 'f', 'e', 'd', 'c', 'b', 'a'])


#### consuming
从双向队列`pop`元素。


```python
print 'From the right:'
d = collections.deque('abcdefg')
while True:
    try:
        print d.pop(),
    except IndexError:
        break
```

    From the right:
    g f e d c b a



```python
print '\nFrom the left:'
d = collections.deque('abcdefg')
while True:
    try:
        print d.popleft(),
    except IndexError:
        break
```

    
    From the left:
    a b c d e f g


### 5. Counter
计数器，顾名思义。构造器接受以下形式，实现初始化。


```python
print collections.Counter(['a', 'b', 'c', 'a', 'b', 'b'])
print collections.Counter({'a':2, 'b':3, 'c':1})
print collections.Counter(a=2, b=3, c=1)
```

    Counter({'b': 3, 'a': 2, 'c': 1})
    Counter({'b': 3, 'a': 2, 'c': 1})
    Counter({'b': 3, 'a': 2, 'c': 1})


#### update


```python
c = collections.Counter()
print 'Initial :', c

c.update('abcdaab')
print 'Sequence:', c

c.update({'a':1,'d':5}) # increse not replace
print 'Dict    :', c # add to a and d
```

    Initial : Counter()
    Sequence: Counter({'a': 3, 'b': 2, 'c': 1, 'd': 1})
    Dict    : Counter({'d': 6, 'a': 4, 'b': 2, 'c': 1})


#### 访问
访问时候利用和字典一样的`API`。但对于没有的键，不会抛出异常，而是计数为0。


```python
c = collections.Counter('abcdaab')
for letter in 'abcde':
    print '%s : %d' % (letter, c[letter])
```

    a : 3
    b : 2
    c : 1
    d : 1
    e : 0


#### elements
产生包含所有元素的一个迭代器。


```python
c = collections.Counter('China')
c['z'] = 0
print c
print list(c.elements())
```

    Counter({'a': 1, 'C': 1, 'i': 1, 'h': 1, 'n': 1, 'z': 0})
    ['a', 'C', 'i', 'h', 'n']


#### most_common()
返回前n个最常见的。

```python
c = collections.Counter('abcdaab')
c.most_common(2)
```

    [('a', 3), ('b', 2)]

