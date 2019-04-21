---
layout: post
title:  Python正则表达式实例透析
date:   2016-08-07 00:00:00
category: "python"
keywords: python,re,正则表达式
---


python里的re模块专门处理正则表达式，功能灵活强大。

### `re.search`

经常用`match = re.search(pat, str)`的形式。因为有可能匹配不到，所以`re.search()`后面一般用`if statement`。


```python
str = 'an example word:cat!!'
match = re.search(r'word:\w\w\w', str)
if match:
    print 'found', match.group() ## 'found word:cat'
else:
    print 'did not find'
```

    found word:cat



```python
# re.search return a match object, which contains lots of info
print type(match)
```

    <type '_sre.SRE_Match'>



```python
print match.string # source string
print match.group()
print match.start() # position of w
print match.end() # position of t
print match.endpos # position of last !
print match.span()
```

    an example word:cat!!
    word:cat
    11
    19
    21
    (11, 19)


### `re.match`

`re.match`和`re.search`很相似，只是`re.match`是从字符串的开头开始匹配。


```python
s = 'python tuts'
match = re.match(r'py',s)
if match:
    print(match.group())
```

    py



```python
s = 'python tuts'
match = re.search(r'^py',s)
if match:
    print(match.group())
```

    py


### 常用正则字符意义

- **a, X, 9**,等字符匹配自己, 元字符不匹配自己，因为有特殊意义，比如** . ^ $ * + ? { }[ ] \ | ( )**

- **.** 英文句号，匹配任意字符，不包含'\n'

- **\w** 匹配'word'字符，[a-zA-Z0-9]
- **\W** 匹配非'word'字符
- **\b** 匹配'word'和'non-word'之间边界
- **\s** 匹配单个whitespace字符,space, newline, return, tab, form [\n\r\t\f]
- **\S** 匹配non-whitespace字符
- **\t, \n, \r** 匹配tab, newline, return
- **\d** 匹配数字[0-9]
- **^** 匹配字符串开头
- **$** 匹配字符串结尾

### 重复

‘+’ 一或多次, ‘*’ 零或多次, ‘?’ 零或一次


### 方括号`[]`


```python
# 提取email address
string = 'purple alice-b@gmail.com monkey dishwasher'
match = re.search(r'\w+@\w+', string)
if match:
    print match.group()  ## 'b@google'
```

    b@gmail


`[]`类似于`or`  
Square brackets can be used to indicate a set of chars, so [abc] matches 'a' or 'b' or 'c'.


```python
match = re.search(r'[\w.-]+@[\w.-]+',string)
if match:
    print match.group()
```

    alice-b@gmail.com


### `Group Extraction`圆括号`()`  

有时候需要提取匹配字符的一部分，比如刚才的邮箱，我们可能需要其中的`username`和`hostname`，这时候可以用`()`分别把`username`和`hostname`包起来，就像`r'([\w.-]+)@([\w.-]+)'`,如果匹配成功，那么pattern不改变，只是可以用`match.group(1)`和`match.group(2)`来`username`和`hostname`，`match.group()`结果不变。


```python
string = 'purple alice-b@google.com monkey dishwasher'
match = re.search(r'([\w\.-]+)@([\w\.-]+)',string)
if match:
    # Return subgroup(s) of the match by indices or names.
    print match.group() # or match.group(0)
    print match.group(1)
    print match.group(2)
if match:
    # Return a tuple containing all the subgroups of the match, from 1.
    print match.groups()
```

    alice-b@google.com
    alice-b
    google.com
    ('alice-b', 'google.com')


### `findall` and `groups`

`()`和`findall()`结合，如果包括一或多个`group`，就返回`a list of tuples`。


```python
str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'
tuples = re.findall(r'([\w\.-]+)@([\w\.-]+)', str)
print tuples  # [('alice', 'google.com'), ('bob', 'abc.com')]
for tuple in tuples:
    print tuple[0] # username
    print tuple[1] # host
```

    [('alice', 'google.com'), ('bob', 'abc.com')]
    alice
    google.com
    bob
    abc.com


给`re.search`加`^`之后是一样的。

### `re.sub`

`re.sub(pat, replacement, str)`在str里寻找和pattern匹配的字符串，然后用replacement替换。`replacement`可以包含`\1`或者`\2`来代替相应的`group`，然后实现局部替换。


```python
# replace hostname
str = 'alice@google.com, and bob@abc.com'
#returns new string with all replacements,
# \1 is group(1), \2 group(2) in the replacement
print re.sub(r'([\w\.-]+)@([\w\.-]+)', r'\1@yo-yo-dyne.com', str)
```

    alice@yo-yo-dyne.com, and bob@yo-yo-dyne.com


### 参考

- [google edu](https://developers.google.com/edu/python/regular-expressions)
- [python guru](http://thepythonguru.com/python-regular-expression/)

