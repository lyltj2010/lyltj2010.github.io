---
layout: post
title:  很赞的开源小工具
date:   2017-08-26 00:00:00
category: "tool"
keywords: 开源,open source,效率,小工具
---

最近整理了一些在用的，感觉还不错的开源小工具，有的仅适用MacOS，但多数跨平台。

#### Homebrew

[Homebrew — The missing package manager for macOS](https://brew.sh/)，Mac上非常好用的包管理工具，很多常见的安装都可以通过`brew install app`或者`brew cask install app`直接安装，类似apt-get。

![brew-seach](https://images-1256734305.cos.ap-beijing.myqcloud.com/brew-search.png)

#### Oh My Zsh

如果你经常用命令行，那+ [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)绝对是必须的工具，因为

> Oh My Zsh will not make you a 10x developer...

不管是自动纠错、目录切换、命令补全、参数补全、强大的alias，用起来都很顺手。

![oh-my-zsh.png](https://images-1256734305.cos.ap-beijing.myqcloud.com/oh-my-zsh.png)

#### tldr

当简单查询某条命令如何使用时，用man查看简直是噩梦，实在太长了，Too Long Don't Read!

![man](https://images-1256734305.cos.ap-beijing.myqcloud.com/man.png)

而[tldr: Simplified and community-driven man pages](https://github.com/tldr-pages/tldr)可以快速get到、回忆起命令的常见用法。对比一下：

![tldr](https://images-1256734305.cos.ap-beijing.myqcloud.com/tldr-tar.png)

#### Autojump

有时候cd到某个目录要好几层，用[Autojump: A cd command that learns](https://github.com/wting/autojump)可以一步到位，安装之后，第一次需要手动cd，以后就可以`j longdir`即可。

![autojump](https://images-1256734305.cos.ap-beijing.myqcloud.com/autojump.png)

#### Copy as Markdown

对于经常用Markdown写文档的人来说，复制网页链接之后还要插入到`[]()`里，实在麻烦。[Copying Link, Image and Tab(s) as Markdown](https://github.com/chitsaou/copy-as-markdown)解决这个头疼的问题。

![copy-as-markdown](https://images-1256734305.cos.ap-beijing.myqcloud.com/copy-as-markdown.png)

#### Github Hovercard

经常混迹于Github人士会浏览无数的Repo，有时候只想大致看看Repo的信息，又懒惰打开那个网页。此时[Github Hovercard](https://github.com/Justineo/github-hovercard)是你的不二之选。

![github-hovercard](https://images-1256734305.cos.ap-beijing.myqcloud.com/github-hovercard.png)

只需要把鼠标悬停在仓库链接即可。

#### Octotree

想看看Github上开源的代码，又不想一层层目录点下去，此时[Octotree: Code tree for GitHub](https://github.com/buunguyen/octotree)正好解决这个难题。

![Octotree](https://images-1256734305.cos.ap-beijing.myqcloud.com/octotree.png)

#### OctoLinker

在Github上的代码，经常会看到`import ...`，习惯了IDE的你，是不是忍不住跳到那个类？[OctoLinker](https://github.com/OctoLinker/browser-extension)满足你的这个需求。

![octo-linker](https://images-1256734305.cos.ap-beijing.myqcloud.com/octo-linker.png)

也支持Python。

#### Go2Shell

Mac下，想直接在某个文件夹下打开Terminal，咋办？去Terminal里打开实在是太麻烦了，试试[Go2Shell](http://zipzapmac.com/Go2Shell)。集成在Finder里之后，一点即可。

#### Web Clipper

看到一篇好文章，保存链接不放心，怕链接失效；复制粘贴太麻烦。用[Evernote Web Clipper](https://evernote.com/products/webclipper/)，直接保存富文本格式的文章，还只能去除广告，好用。

![web-clipper](https://images-1256734305.cos.ap-beijing.myqcloud.com/web-clipper.png)

#### Json Viewer

![json-viewer](https://images-1256734305.cos.ap-beijing.myqcloud.com/json-viewer.png)

在浏览器上返回的Json文件，如果没有格式化太难看清其结构，利用[Json Viewer](https://github.com/tulios/json-viewer)插件，就明了多了。

#### jq

如果在终端想看结果化的json，可以用[jq](https://stedolan.github.io/jq/)。

> jq is a lightweight and flexible command-line JSON processor.


#### csvkit

如果你做数据分析，这个命令行工具[csvkit](https://github.com/wireservice/csvkit/tree/1.0.2)你一定喜欢。《Data Science at Command Line》一书推荐，很好用。

#### Quicklook

工作中会遇到各种各样格式的文件，比如代码、Json、csv、Excel、markdown文档等。很多时候只想看大概信息，就是quicklook一下，不想打开编辑，这时候[Quicklook Plugins: List of useful Quick Look plugins for developers](https://github.com/sindresorhus/quick-look-plugins)特别好用，官网上有很丰富的例子。

![quicklook-markdown](https://images-1256734305.cos.ap-beijing.myqcloud.com/quicklook-markdown.png)

#### 本地wiki

如果你需要写wiki page，类似如下图的文档。

![ollum-wiki](https://images-1256734305.cos.ap-beijing.myqcloud.com/gollum-wiki.png)

用[gollum: A simple, Git-powered wiki with a sweet API and local frontend.](https://github.com/gollum/gollum)吧，基于Ruby on Rails的一个框架，简单易用。

