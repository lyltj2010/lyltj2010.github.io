---
layout: post
title:  Python glob匹配文件
date:   2016-07-17 00:00:00
category: "python"
keywords: python,glob
---


`glob`的应用场景是要寻找一系列（符合特定规则）文件名。  

`glob`模块是最简单的模块之一，内容非常少。用它可以查找符合特定规则的文件路径名。查找文件只用到三个匹配符：”`*`”, “`?`”, “`[]`”。   

- ”*”匹配0个或多个字符；  
- ”?”匹配单个字符；
- ”[ ]”匹配指定范围内的字符，如：[0-9]匹配数字。

假设以下例子目录是这样的。  
`dir`  
`dir/file.txt`  
`dir/file1.txt`  
`dir/file2.txt`  
`dir/filea.txt`  
`dir/fileb.txt`  
`dir/subdir`  
`dir/subdir/subfile.txt`  

### 匹配所有文件

可以用`*`匹配任意长度字节。`glob.glob`比较常用，返回一个`list`，也可用`glob.iglob`返回生成器。


```python
import glob
for name in glob.glob('dir/*'):
    print name
```

    dir/file.txt
    dir/file1.txt
    dir/file2.txt
    dir/filea.txt
    dir/fileb.txt
    dir/subdir


### 匹配子目录文件

可以指定子目录名称，也可以用通配符代替，不显示指定。


```python
print 'Named explicitly:'
for name in glob.glob('dir/subdir/*'):
    print '\t', name

print 'Named with wildcard:'
for name in glob.glob('dir/*/*'):
    print '\t', name
```

    Named explicitly:
    	dir/subdir/subfile.txt
    Named with wildcard:
    	dir/subdir/subfile.txt


### 单字节通配符匹配

除了`*`以外，还有`?`匹配单个字符。比如下面这个例子，匹配以`file`开头，以`.txt`结尾，中间是任一字符的文件。


```python
for name in glob.glob('dir/file?.txt'):
    print name
```

    dir/file1.txt
    dir/file2.txt
    dir/filea.txt
    dir/fileb.txt


### 字符区间匹配[0-9]

比如匹配后缀前是数字的文件。


```python
for name in glob.glob('dir/*[0-9].*'):
    print name
```

    dir/file1.txt
    dir/file2.txt


### Ref:

- [官方文档](https://docs.python.org/2/library/glob.html)
- [Python Module of the Week](https://pymotw.com/2/glob/)



