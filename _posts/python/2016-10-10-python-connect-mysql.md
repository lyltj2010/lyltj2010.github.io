---
layout: post
title:  Python操作数据库
date:   2016-10-10 00:00:00
category: "python"
keywords: python,database,mysql
---


前几天数据库课程的一个小project，需要接入MySQL数据库，导入数据，写了个[脚本](https://github.com/lyltj2010/MusicDB/blob/master/get_data/write_to_db.py)，做简单的CRUD操作，用Python实现，简单地记录一下。

#### 依赖
可以用MySQL-python来连MySQL，安装很简单，`pip install MySQL-python`，然后在脚本里引入`import MySQLdb`即可。有不止一个库实现类似的功能，API大同小异。

#### 连接
首先要做的是链接数据库，当然要确保你MySQL Server是安装运行的，用[homebrew](http://brew.sh/)安装的话`brew install mysql`。  

链接数据库之后，会返回一个cursor，主要通过这个cursor执行SQL语句，操作数据库。比如有一个数据库叫MusicDB，链接的函数如下。

```python
import MySQLdb
def connect_db():
    """Connect database and return db and cursor"""
    db = MySQLdb.connect(host="localhost",user='root',
                     	 passwd='PASSWD'',db="MusicDB")
    cursor = db.cursor()
    return db, cursor
```

当然如果想确认下有没有链接成功的话，可以用如下代码。  

```python
db, cursor = connect_db()
cursor.execute("SELECT VERSION()")
data = cursor.fetchone()
print "Database version : %s " % data
db.close()
```

运行脚本，如果看到类似这样的输出`Database version : 5.0.45`，表明就ok了。

#### 检查表的存在
有时候可能需要不知一次修改数据库的表，不想直接在terminal里写sql，想直接修改脚本，重新跑一下，直接删除表，需要看下表是否存在。MySQL里有个表information_schema.tables包含数据库表的信息。

```python
def table_exists(table_name):
    """Check table existence base on table name"""
    db, cursor = connect_db()
    cursor.execute("SELECT * FROM information_schema.tables \
                   WHERE table_name = '%s'" % table_name)
    nrows = int(cursor.rowcount); db.close()
    return False if nrows == 0 else True
```

#### 创建表
链接数据库，定义个`CREATE TABLE`语句，执行即可，具体table里有哪些字段，当然是根据实际情况喽。这里的例子是歌手信息，比如有名字，他的网址，以及播放次数。

```python
def create_table_artist():
	 # Connect database
    db, cursor = connect_db()
    sql = """CREATE TABLE artist(
             name CHAR(50) NOT NULL,
             url CHAR(80),
             playcount INT)"""
    if not table_exists('artist'):
        cursor.execute(sql)
    # remember to disconnect from server
    db.close()
```

#### 删除表
当然了，删除表不是一个常见的操作，不过偶然可能用到。

```python
def drop_table(table_name):
    db, cursor = connect_db()
    if table_exists(table_name):
        sql = """DROP TABLE %s""" % table_name
        cursor.execute(sql)
    db.close()
```

#### 插入INSERT
我们从外部读入数据之后，可以把这些数据插入到数据库中，具体的toy数据开心用啥就用啥喽。插入数据的时候，如果数据不符合创建表时候的定义，就会抛出错误，我们需要简单地处理下。如果try成功了，那就`db.commit()`将改变写入到数据库，如果try失败，那就`db.rollback()`回来。记得要**`db.commit()`**哦，要不然那个表总是一行数据都没有。

```python
def insert_into_artist():
    artists = load_json('artists.json')       
    db, cursor = connect_db()
    sql = """INSERT INTO artist(name, url, playcount)
           VALUES ('%s',  '%s', '%d')"""
    for a in artists:
        try:
        	  # remember to convert playcount to integer
            tp = (a['name'], a['url'], int(a['playcount']))
            cursor.execute(sql % tp)
            db.commit()
        except:
            db.rollback()
    db.close()
```

#### 删除DELETE
删除操作也很类似，定义sql语句，execute即可，如果失败就rollback回来。如果表里一个字段是其他表的Foreign Key的话，直接删除这条记录就会抛出错误，所以需要考虑下这种异常情况。

```python
def delete_artist(artist):
	db, cursor = connect_db()
	sql = "DELETE FROM artist WHERE name='%s'" % artist
	try:
		cursor.execute(sql)
   		db.commit()
   	except:
   		db.rollback()
   	db.close()	
```

#### 更新UPDATE
比如每次有人播放一首歌，我们想把这个歌手的播放次数加一，可以用`UPDATE`语句实现。

```python
def update_artist(artist):
	db, cursor = connect_db()
	sql = "UPDATE artist SET playcount = playcount + 1 WHERE name='%s'" % artist
	try:
		cursor.execute(sql)
   		db.commit()
   	except:
   		db.rollback()
   	db.close()	
```

#### 查找SELECT
这个稍微复杂点，主要的API有`fetchone()`，`fetchall()`和`rowcount`。比如想找出播放次数大于十万的所有歌手，可以这样实现。

```python
def top_artists():
	db, cursor = connect_db()
	sql = "SELECT * FROM artist WHERE playcount > '%d' " % 100000
	try:
		cursor.execute(sql)
		return cursor.fetchall()
	execept:
		print("Error in fetching data")
	db.close()

results = top_artists()
for row in results:
	name = row[0]
	print(name)	
```

