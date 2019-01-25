---
layout: post
title:  Mac必备软件
date:   2017-07-22 00:00:00
category: "tool"
keywords: mac,效率,工具
---


Mac上有很多优秀的软件，可以极大地提升效率和工作体验。

## 效率工具

#### Alfred

效率神器，mac绝对必备。可以快速启动程序和全局搜索文件。安装好之后`cmd+space`调用Alfred，输入程序名即可调用程序；打一个空格再输入可以查找文件及文件夹。当然付费版可以自定义workflow，可以组合一连串的操作到一个快捷键。workflow可以整合terminal，浏览器，python程序等等，非常强大。

快速启动程序：

![alfred-launch-app](https://images-1256734305.cos.ap-beijing.myqcloud.com/alfred-launch-app.png)

快速搜索文件或文件夹：

![alfred-open-folder](https://images-1256734305.cos.ap-beijing.myqcloud.com/alfred-open-folder.png)

#### aText

快速输入常用文字片段。经常会输入重复的文字片段，这是时间的极大浪费，就算存储在某个地方，那**打开->查找->复制->粘贴**流程也是非常的麻烦。aText可以给常用的片段定义关键词(可以用固定后缀标识)，比如可以将电话定义为`teltt`，可以将地址定义为`addrtt`等。

#### Keyboard Maestro

录制宏，然后定义快捷键，多步重复操作者的福音。

#### Divvy

分屏软件。当开多个窗口的时候，来回切换很是浪费精力。如果喜欢快捷键，Spectacle也是不错的选择。

#### LightShot

截屏软件。`cmd+shift+9`启动截屏，可以拖动选取范围，可复制到粘贴板，也可以保存为图片。

#### Caffeine

离开电脑几分钟就会锁屏，还要重新解锁。如果不想让电脑锁屏，点一下Caffeine，可以让电脑保持一定时间的不休眠。

![caffeine.png](https://images-1256734305.cos.ap-beijing.myqcloud.com/caffeine.png)

## 知识管理

#### Quiver

代码笔记软件。完美支持Markdown语法，代码、文档可以方便的记录检索。文档里可以添加一个个Cell，在里面写代码片段，下次用的时候可以直接复制。

##### MWeb

Markdown文件编辑工具，相比于Mou和Macdown而言，Mweb有文件层级目录，项目文档、wiki等编辑必备。

#### Reeder

RSS订阅。订阅自己感兴趣的技术博客，Reeder的阅读体验还是很不错的。

#### Zotero

文献图书管理工具。当图书、文献多的时候，管理是个耗时耗力的工作，Zotero是一款很不错的此类开源软件。阳志平老师有很系统的介绍：[Zotero文献管理 - 阳志平的网志](http://www.yangzhiping.com/tech/zotero)。

## 思维工具

##### Workflowy

助力输出工具，[卡片助力输入输出，工具我选 WorkFlowy](https://ishanshan.im/selfedu/HbOutputOwetoWorkFlowy.html)。

## 开发工具

#### Homebrew

> The missing package manager for macOS

自从有了[Homebrew](https://brew.sh/)，大部分软件安装工作都可以通过简单的命令解决，类似于Ubuntu的apt-get。安装需要的软件的时候，可以先用brew搜索，然后通过install命令安装即可。

![brew-seach](https://images-1256734305.cos.ap-beijing.myqcloud.com/brew-search.png)

#### iTerm

更好用的终端。结合[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)，终端使用体验不能更好。

#### Sublime

文本编辑器。好用，轻量级。

#### Navicat

数据库管理。可以连接MySQL, PostgreSQL等主流数据库，用户体验很好。

#### Dash

离线文档。可以在本地方便地查询各种语言的API，同时还能搜索StackOverflow上的问答，开发必备。结合Alfred，不能更方便地查询API。

![dash](https://images-1256734305.cos.ap-beijing.myqcloud.com/dash.png)

## 系统工具

#### AppCleaner

当卸载软件的时候，可能有文件残留，用AppCleaner可以选中默认会残留的文件，一起删除。

#### Bartender

标题栏管理工具。当安装的软件越来越多，电脑上方图标会越来越多，而且很杂，Bartender可以把不常用的隐藏起来，对比开启使用Bartender前后。

没有使用Bartender：

![without-bartender](https://images-1256734305.cos.ap-beijing.myqcloud.com/without-bartender.png)

使用Bartender：

![with-bartender](https://images-1256734305.cos.ap-beijing.myqcloud.com/with-bartender.png)

## 其他

还有很多不是重量级，但依然很赞的应用，也值得一试。

+ Itsycal，日期小工具
+ Flux，护眼小工具
+ Macdown，markdown编辑器
+ SnippetsLab，代码片段管理
+ SourceTree，代码查看，可以看不同版本差异
+ Quicklook，快速查看csv、json的格式的文件
+ Noizio，听歌听腻了，来点白噪音


