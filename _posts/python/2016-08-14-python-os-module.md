---
layout: post
title:  Python os模块实例
date:   2016-08-14 00:00:00
category: "python"
keywords: python,os
---


os模块操作文件、路径，是python比较常用的一个库。

```python
# I use jupyter notebook to create some file
!touch foo.txt
!echo Hello > foo.txt
!cat foo.txt
```

    Hello



```python
# rename file
os.rename('foo.txt','bar.txt')
!cat bar.txt
```

    Hello



```python
# remove file
os.remove('bar.txt')
```

### 改变目录


```python
# current dir
print os.getcwd() # current working directory
```

    /Users/yongle/OMOOC2py/cheat



```python
# go down
os.chdir('img')
print os.getcwd()

# go back up
os.chdir(os.pardir) #or simply os.chdir('..')
print os.getcwd()
```

    /Users/yongle/OMOOC2py/cheat/img
    /Users/yongle/OMOOC2py/cheat


### 遍历目录`listdir`


```python
# listdir
!touch a.txt b.txt
for file in os.listdir('.'):
    # os.listdir() return a list
    if file.endswith('.txt'):
        print file
```

    a.txt
    b.txt


### 遍历`os.walk`


```python
os.chdir('doc')
```


```python
# Directory tree generator.
# For each dir in the dir tree rooted at top (including top
# itself, but excluding '.' and '..'), yields a 3-tuple
# dirpath, dirnames, filenames
for dirpath, dirnames, filenames in os.walk('.'):
    print dirnames
    print filenames
    break # only one level needed, or just use listdir
```

    ['folder1', 'folder2']
    ['.DS_Store', 'a.txt', 'b.txt']


### 增删目录

##### 单层目录


```python
# make a dir, one level, no duplication allowed
os.mkdir('test')
```


```python
# remove a dir, one level, not empty will raise OSError
os.rmdir('test') 
```

##### 多层目录 


```python
# make dirs, multipul level
os.makedirs('test/mulitiple/levels')
```


```python
# remove all empty directories above it, ensure empty
os.removedirs('test/mulitiple/levels')
```

##### 非空目录


```python
# remove non empty dir, ust a new module shutil.rmtree
# copy function is also useful
import shutil
```


```python
# copy a.txt to backup folder
# or just shutil.copy('a.txt','backup/')
# use shutil.copytree to copy a folder like cp -r
os.mkdir('backup')
shutil.copy('a.txt',os.path.join('backup','a_backup.txt'))
```


```python
# remove non empty folder
shutil.rmtree('backup/')
```

### os.path模块


```python
# is a dir or not
print(os.path.isdir('img'))
print(os.path.isdir('a.txt'))
```

    True
    False



```python
# is a file or not
print(os.path.isfile('img'))
print(os.path.isfile('a.txt'))
```

    False
    True



```python
# determine the presence of path(a file or dir); os.path.lexists?
print(os.path.exists('img'))
print(os.path.exists('a.txt'))
print(os.path.exists('none_exist.txt'))
```

    True
    True
    False



```python
# Join two or more pathname components, inserting '/' as needed.
# If any component is an absolute path, 
# all previous path components will be discarded.
print(os.path.join('/Users','john'))
print(os.path.join('/Users','/john'))
print(os.path.join('/Users','john','a.txt'))
```

    /Users/john
    /john
    /Users/john/a.txt



```python
# split a pathname. Returns "(head, tail)" 
# where "tail" is everything after the final slash.
os.path.split('/Users/john/a.txt')
```




    ('/Users/john', 'a.txt')




```python
# split the extension from a pathname
os.path.splitext('/Users/john/a.txt')
```




    ('/Users/john/a', '.txt')




```python
# determine the size of a path(file or dir)
os.path.getsize('a.txt')
```




    0

