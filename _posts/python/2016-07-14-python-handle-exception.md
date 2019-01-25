---
layout: post
title:  Python异常处理
date:   2016-07-14 00:00:00
category: "python"
keywords: python,python异常处理,exception
---


异常处理是写出健壮程序的必备步骤。

### 1.1 基本语法  

把可能抛出异常(出错)的语句放在`try`的`block`里，然后用`except`去扑捉(预判)可能的异常类型，如果异常类型match，就执行`except`模块。

```python
try:
    # write some code
    # that might throw exception
except <ExceptionType>:
    # Exception handler, alert the user
```

比如读取一个不存在的文件会引起`IOError`，我们就可以提前加以处理。


```python
try:
    f = open('nofile.txt', 'r')
    print f.read()
    f.close()
except IOError:
    print 'file not found'
```

    file not found


> 执行流程是这样的：
1. First statement between `try`  and `except`  block are executed.
2. If no exception occurs then code under `except`  clause will be skipped.
3. If file don’t exists then exception will be raised and the rest of the code in the `try`  block will be skipped
4. When exceptions occurs, if the exception type matches exception name after `except`  keyword, then the code in that `except`  clause is executed.

### 1.2 扑获更多异常类型

```python
try:
    <body>
except <ExceptionType1>:
    <handler1>
except <ExceptionTypeN>:
    <handlerN>
except:
    <handlerExcept>
else:
    <process_else>
finally:
    <process_finally>
```

1. `except`类似于`elif`，当`try`出现异常时，挨个匹配`except`里的异常类型，如果匹配，执行；若果没有匹配，执行不指定异常类型的`except`。  

2. `else`只有在`try`执行时没有异常的时候执行。  

3. `finally`不管`try`模块是否有异常抛出，都执行。

### 1.3 例子


```python
num1, num2 = 1,0
try:
    result = num1 / num2
    print("Result is", result)

except ZeroDivisionError:
    print("Division by zero is error !!")

except:
    print("Wrong input")

else:
    print("No exceptions")

finally:
    print("This will execute no matter what you input")
```

    Division by zero is error !!
    This will execute no matter what you input


## 2. 抛出异常

用`raise`语句抛出自己的异常。`raise ExceptionClass('Your argument')`


```python
def enterage(age):
    if age < 0:
        raise ValueError("Only positive integers are allowed")

    if age % 2 == 0:
        print("age is even")

try:
    num = int(input("Enter your age: "))
    enterage(num)
except ValueError:
    print 'Only positive integers are allowd'
except:
    print 'Something went wrong'
```

    Enter your age: -3
    Only positive integers are allowd


异常参考图，更多异常类型参见[官方文档](https://docs.python.org/2/library/exceptions.html)。  
![exception](http://upload-images.jianshu.io/upload_images/310441-8ce0e0edb7391428.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3. 操作异常

有时候我们希望能把异常对象传递给一个变量，也非常方便实现。  

```python
try:
    # this code is expected to throw exception
except ExceptionType as ex:
    # code to handle exception
```


```python
try:
    number = int(input("Enter a number: "))
    print "The number entered is", number

except NameError as ex:
    print "Exception:", ex
```

    Enter a number: one
    Exception: name 'one' is not defined



