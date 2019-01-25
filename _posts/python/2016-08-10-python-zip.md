---
layout: post
title:  Python zip模块
date:   2016-08-10 00:00:00
category: "python"
keywords: python,zip
---


python里有专门处理压缩文件的包zipfile，可以进行压缩、解压等各种常见操作。

#### 判断是否是`ZIP`文件

用`zipfile.is_zipfile`判断。


```python
import zipfile
```


```python
print(zipfile.is_zipfile('samples/archive.zip'))
```

    True

---
`ZipFile`可以直接操作`ZIP`，支持读取数据以及对其修改。

#### 读取文件信息

`List`出来archive文件里内容，用**namelist** 和 **infolist**方法。返回`list of filenames`或`list of ZipInfo instances`。


```python
import zipfile
zf = zipfile.ZipFile('samples/archive.zip','r')
```


```python
# list filenames
for name in zf.namelist():
    print name,
```

    a.txt b.txt c.txt



```python
# list file infomation
for info in zf.infolist():
    print info.filename, info.date_time, info.file_size
```

    a.txt (2016, 7, 15, 0, 5, 58) 2
    b.txt (2016, 7, 15, 0, 6, 8) 2
    c.txt (2016, 7, 15, 0, 6, 14) 2


#### 提取数据`read()`

用`read()`方法，以`filename`作为参数，以`string`形式返回数据。


```python
zf = zipfile.ZipFile('samples/archive.zip')
for filename in zf.namelist():
    # can use other than namelist,['there.txt','notthere.txt']
    try:
        data = zf.read(filename) # extract use read()
    except KeyError:
        print "Error: Did not find %s in zip file" % filename
    else:
        print filename, ':',
        print repr(data)
```

    a.txt : 'a\n'
    b.txt : 'b\n'
    c.txt : 'c\n'


#### 解压数据`extract()`


```python
zf = zipfile.ZipFile('samples/archive.zip','r')
# Extract a member from the archive to the current working directory
zf.extract('a.txt') # you may want to specify path param

# Extract all members from the archive to the current working directory
zf.extractall() # you may want to specify path param
```

#### 压缩数据

创建新的`zip`文件，只需要初始化一个新的`ZipFile`即可，用`w`模式，要添加数据，用`write()`方法即可。


```python
print('creating archive')
zf = zipfile.ZipFile('zipfile_write.zip',mode='w')
try:
    print('adding readme.txt')
    zf.write('readme.txt')
finally:
    print('closing')
    zf.close()
```

    creating archive
    adding readme.txt
    closing


但是默认没有只是打包，没有压缩数据，如果压缩，需要用`zlib`模块。默认压缩模式`zipfile.ZIP_STORED`，可以改变为`zipfile.ZIP_DEFLATED`。


```python
# try to change compression type
try:
    import zlib
    compression = zipfile.ZIP_DEFLATED
except:
    compression = zipfile.ZIP_STORED

modes = {zipfile.ZIP_DEFLATED: 'deflated', zipfile.ZIP_STORED: 'stored'}
print('creating archive')
zf = zipfile.ZipFile('zipfile_write_compression.zip',mode='w')
try:
    print('adding README.txt with compression mode'+ str(modes[compression]))
    zf.write('readme.txt',compress_type=compression)
finally:
    print('closing')
    zf.close()
```

    creating archive
    adding README.txt with compression modedeflated
    closing


### Ref:

- [Effbot](http://effbot.org/librarybook/zipfile.htm)  
- [Python Module of the Week](http://bioportal.weizmann.ac.il/course/python/PyMOTW/PyMOTW/docs/zipfile/index.html)

