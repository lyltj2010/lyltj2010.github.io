---
layout: post
title:  Python处理Json数据
date:   2016-07-30 00:00:00
category: "python"
keywords: python,json
---


JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。易于人阅读和编写。同时也易于机器解析和生成。  

数据格式可以简单地理解为**键值对**的集合（A collection of name/value pairs）。不同的语言中，它被理解为对象（object），纪录（record），结构（struct），字典（dictionary），哈希表（hash table），有键列表（keyed list），或者关联数组 （associative array）。
值的有序列表（An ordered list of values）。在大部分语言中，它被理解为数组（array）。


```python
import json
```

Pyhton的Json模块提供了把内存中的对象序列化的方法。

### `json.dumps`  
`dump`的功能就是把`Python`对象`encode`为json对象，一个编码过程。注意`json`模块提供了`json.dumps`和`json.dump`方法，区别是`dump`直接到文件，而`dumps`到一个字符串，这里的`s`可以理解为`string`。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]
print 'DATA:', repr(data)

data_string = json.dumps(data)
print 'JSON:', data_string
```

    DATA: [{'a': 'A', 'c': 3.0, 'b': (2, 4)}]
    JSON: [{"a": "A", "c": 3.0, "b": [2, 4]}]


查看其类型，发现是`string`对象。


```python
print type(data)
print type(data_string)
```

    <type 'list'>
    <type 'str'>


### `json.dump`
不仅可以把`Python`对象编码为`string`，还可以写入文件。因为我们不能把`Python`对象直接写入文件，这样会报错`TypeError: expected a string or other character buffer object
`，我们需要将其序列化之后才可以。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]
```


```python
with open('output.json','w') as fp:
    json.dump(data,fp)
```


```python
cat output.json
```

    [{"a": "A", "c": 3.0, "b": [2, 4]}]

### `json.loads`
从`Python`内置对象`dump`为`json`对象我们知道如何操作了，那如何从`json`对象`decode`解码为`Python`可以识别的对象呢？是的用`json.loads`方法，当然这个是基于`string`的，如果是文件，我们可以用`json.load`方法。


```python
decoded_json = json.loads(data_string)
```


```python
# 和之前一样，还是list
print type(decoded_json)
```

    <type 'list'>



```python
# 像访问 data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]一样
print decoded_json[0]['a']
```

    A


### `json.load`
可以直接`load`文件。


```python
with open('output.json') as fp:
    print type(fp)
    loaded_json = json.load(fp)
```

    <type 'file'>



```python
# 和之前一样，还是list
print type(decoded_json)
```

    <type 'list'>



```python
# 像访问 data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]一样
print decoded_json[0]['a']
```

    A


### 数据类型对应
`json`和`Python`对象转换过程中，数据类型不完全一致，有对应。

|Python|Json|
|---|---|
|dict|object|
|list,tuple|array|
|str, unicode|string|
|int,long,float|number|
|True|true|
|False|false|
|None|null|

### `json.dumps`常用参数

一些参数，可以让我们更好地控制输出。常见的比如`sort_keys`，`indent`，`separators`，`skipkeys`等。

`sort_keys`名字就很清楚了，输出时字典的是按键值排序的，而不是随机的。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]
print 'DATA:', repr(data)

unsorted = json.dumps(data)
print 'JSON:', json.dumps(data)
print 'SORT:', json.dumps(data, sort_keys=True)
```

    DATA: [{'a': 'A', 'c': 3.0, 'b': (2, 4)}]
    JSON: [{"a": "A", "c": 3.0, "b": [2, 4]}]
    SORT: [{"a": "A", "b": [2, 4], "c": 3.0}]


`indent`就是更个缩进，让我们更好地看清结构。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]
print 'DATA:', repr(data)

print 'NORMAL:', json.dumps(data, sort_keys=True)
print 'INDENT:', json.dumps(data, sort_keys=True, indent=2)
```

    DATA: [{'a': 'A', 'c': 3.0, 'b': (2, 4)}]
    NORMAL: [{"a": "A", "b": [2, 4], "c": 3.0}]
    INDENT: [
      {
        "a": "A", 
        "b": [
          2, 
          4
        ], 
        "c": 3.0
      }
    ]


`separators`是提供分隔符，可以出去白空格，输出更紧凑，数据更小。默认的分隔符是`(', ', ': ')`，有白空格的。不同的`dumps`参数，对应文件大小一目了然。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0 } ]
print 'DATA:', repr(data)
print 'repr(data)             :', len(repr(data))
print 'dumps(data)            :', len(json.dumps(data))
print 'dumps(data, indent=2)  :', len(json.dumps(data, indent=2))
print 'dumps(data, separators):', len(json.dumps(data, separators=(',',':')))
```

    DATA: [{'a': 'A', 'c': 3.0, 'b': (2, 4)}]
    repr(data)             : 35
    dumps(data)            : 35
    dumps(data, indent=2)  : 76
    dumps(data, separators): 29


`json`需要字典的的键是字符串，否则会抛出`ValueError`。


```python
data = [ { 'a':'A', 'b':(2, 4), 'c':3.0, ('d',):'D tuple' } ]

print 'First attempt'
try:
    print json.dumps(data)
except (TypeError, ValueError) as err:
    print 'ERROR:', err

print
print 'Second attempt'
print json.dumps(data, skipkeys=True)
```

    First attempt
    ERROR: keys must be a string
    
    Second attempt
    [{"a": "A", "c": 3.0, "b": [2, 4]}]

