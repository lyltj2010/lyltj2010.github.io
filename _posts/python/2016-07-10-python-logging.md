---
layout: post
title:  Python Logging模块
date:   2016-07-10 00:00:00
category: "python"
keywords: python,日志,python日志
---


python的Logging模块专门提供日志相关的功能。

### Quick Start

导入模块后直接`logging.waring()`，`logging.error()`简单粗暴地调用即可。默认的`level`是`DEBUG`，所以`warning`会打印出信息，`info`级别更低，不会输出信息。如果你不知道`level`等参数的意义请后面解释，淡定，继续往下看。  

如果不特别配置，`logging`模块将日志打印到屏幕上(stdout)。


```python
#!/usr/local/bin/python
# -*- coding:utf-8 -*-
import logging
logging.warning('Watch out!')  # print message to console
logging.info('I told you so')  # will not print anything
```

### `Log`写入文件

更常见的情形是把信息记录在`log`文件里。需要用`logging.basicConfig()`设置文件名以及`level`等参数，常见的`level`见下表。  

|Level|Value|Usage|
|---|---|---|
|CRITICAL|50|严重错误，表明程序已不能继续运行了|
|ERROR|40|严重的问题，程序已不能执行一些功能了|
|WARNING|30|有意外，将来可能发生问题，但依然可用|
|INFO|20|证明事情按预期工作|
|DEBUG|10|详细信息，调试问题时会感兴趣。|  

如果设置`level`为`INFO`，那么`DEBUG`级别的信息就不会输出。常见的函数接口有`debug()`, `info()`, `warning()`, `error()` and `critical()`，分别对应`log`不同严重级别的信息。  

注意把下面代码写入脚本（直接在`terminal`里不会生成文件），比如`test_log.py`。


```python
import logging
logging.basicConfig(filename='example.log',level=logging.DEBUG,filemode='w')
# filemode = 'w' 每次运行，重写log
logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
```


```python
cat example.log
```

    DEBUG:root:This message should go to the log file
    INFO:root:So should this
    WARNING:root:And this, too


### 改变`Log`输出格式  

通过`format`参数，可以定制写入`log`文件的格式。


```python
import logging
logging.basicConfig(format='%(levelname)s:%(message)s',level=logging.DEBUG)
logging.debug('This message should appear on the console')
logging.info('So should this')
logging.warning('And this, too')
```

DEBUG:This message should appear on the console  
INFO:So should this  
WARNING:And this, too  

### 记录时间

通过`datafmt`参数，可以格式化输出`log`的时间。


```python
import logging
logging.basicConfig(format='%(asctime)s %(message)s',datefmt='%m/%d/%Y %I:%M:%S %p')
logging.warning('is when this event was logged.')
```

07/16/2016 12:10:35 AM is when this event was logged.

### 更丰富的`Log`控制

上面的代码大部分是利用默认配置，其实我们自定义更多。比如把输出到`terminal`和`log.txt`文件里。  

首先理解几个概念是有用的。  
- `Logger` 记录器，暴露了应用程序代码能直接使用的接口。
- `Handler` 处理器，将（记录器产生的）日志记录发送至合适的目的地。
- `Filter` 过滤器，提供了更好的粒度控制，它可以决定输出哪些日志记录。
- `Formatter` 格式化器，指明了最终输出中日志记录的布局。


首先，创建一个`logger`，记录器，然后给其添加不同的`handler`，输出到不同的渠道，比如下面这个例子就会生成`log.txt`文件，并同时输出在`terminal`里。


```python
import logging
# create logger with name
# if not specified, it will be root
logger = logging.getLogger('my_logger')
logger.setLevel(logging.DEBUG)

# create a handler, write to log.txt
# logging.FileHandler(self, filename, mode='a', encoding=None, delay=0)
# A handler class which writes formatted logging records to disk files.
fh = logging.FileHandler('log.txt')
fh.setLevel(logging.DEBUG)

# create another handler, for stdout in terminal
# A handler class which writes logging records to a stream
sh = logging.StreamHandler()
sh.setLevel(logging.DEBUG)

# set formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
fh.setFormatter(formatter)
sh.setFormatter(formatter)

# add handler to logger
logger.addHandler(fh)
logger.addHandler(sh)

# log it
logger.debug('Debug')
logger.info('Info')
```

    2016-07-18 21:43:14,648 - my_logger - DEBUG - Debug
    2016-07-18 21:43:14,650 - my_logger - INFO - Info


### Ref:

- [官方文档](https://docs.python.org/2.7/howto/logging.html)
- [Python Module of the Week](https://pymotw.com/2/logging/)
- [Good logging practice in python](http://victorlin.me/posts/2012/08/26/good-logging-practice-in-python)



