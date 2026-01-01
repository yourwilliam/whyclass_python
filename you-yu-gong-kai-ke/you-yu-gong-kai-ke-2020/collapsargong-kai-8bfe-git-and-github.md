# Collapsar公开课-Git\&Github

## 版本控制

### 问题

1. 我们经常在修改word的时候，后面的修改保存后，如果修改出现问题，前面的内容就再也找不回了
2. 在开发代码的时候，有时改了一些东西导致无法运行，但是因为保存了想退回去又无法退回。文件多了更不知道怎么退回了。
3. 代码由多人维护，多人开发时如何维护？

### 什么是版本控制

版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。

如果你是位图形或网页设计师，可能会需要保存某一幅图片或页面布局文件的所有修订版本（这或许是你非常渴望拥有的功能），采用版本控制系统（VCS）是个明智的选择。 有了它你就可以将选定的文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态，你可以比较文件的变化细节，查出最后是谁修改了哪个地方，从而找出导致怪异问题出现的原因，又是谁在何时报告了某个功能缺陷等等。 使用版本控制系统通常还意味着，就算你乱来一气把整个项目中的文件改的改删的删，你也照样可以轻松恢复到原先的样子。 但额外增加的工作量却微乎其微。

#### 本地版本控制

![](http://ossp.pengjunjie.com/mweb/15960872710305.jpg)

#### 集中化的版本控制

![](http://ossp.pengjunjie.com/mweb/15960873161915.jpg)

#### 分布式版本控制系统

![](http://ossp.pengjunjie.com/mweb/15960873540255.jpg)

## Git

### git简史

同生活中的许多伟大事物一样，Git 诞生于一个极富纷争大举创新的年代。

Linux 内核开源项目有着为数众多的参与者。 绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 这就迫使 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds）基于使用 BitKeeper 时的经验教训，开发出自己的版本系统。 他们对新的系统制订了若干目标：

速度

简单的设计

对非线性开发模式的强力支持（允许成千上万个并行开发的分支）

完全分布式

有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）

自诞生于 2005 年以来，Git 日臻成熟完善，在高度易用的同时，仍然保留着初期设定的目标。 它的速度飞快，极其适合管理大项目，有着令人难以置信的非线性分支管理系统

### 什么是Git

#### 直接记录快照，而非差异比较

Git 和其它版本控制系统（包括 Subversion 和近似工具）的主要差别在于 Git 对待数据的方法。 从概念上来说，其它大部分系统以文件变更列表的方式存储信息，这类系统（CVS、Subversion、Perforce、Bazaar 等等） 将它们存储的信息看作是一组基本文件和每个文件随时间逐步累积的差异 （它们通常称作 基于差异（delta-based） 的版本控制）。

![](http://ossp.pengjunjie.com/mweb/15960875809895.jpg)

Git 不按照以上方式对待或保存数据。反之，Git 更像是把数据看作是对小型文件系统的一系列快照。 在 Git 中，每当你提交更新或保存项目状态时，它基本上就会对当时的全部文件创建一个快照并保存这个快照的索引。 为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 快照流。

![](http://ossp.pengjunjie.com/mweb/15960876711978.jpg)

#### 近乎所有操作都是本地执行

和其他操作不同，可以在脱网的时候在本地修改，其他系统做不到这点，在脱网的时候无法提交会导致不能协同

#### 三种状态

Git 有三种状态，你的文件可能处于其中之一： 已提交（committed）、已修改（modified） 和 已暂存（staged）。

* 已修改表示修改了文件，但还没保存到数据库中。
* 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
* 已提交表示数据已经安全地保存在本地数据库中。

![](http://ossp.pengjunjie.com/mweb/15960878128023.jpg)

## 安装git

### mac操作系统

在 Mac 上安装 Git 有多种方式。 最简单的方法是安装 Xcode Command Line Tools。

有的mac系统直接执行git是存在的。

如果你想安装更新的版本，可以使用二进制安装程序。 官方维护的 macOS Git 安装程序可以在 Git 官方网站下载，网址为 [https://git-scm.com/download/mac](https://git-scm.com/download/mac)。

### windows安装

在 Windows 上安装 Git 也有几种安装方法。 官方版本可以在 Git 官方网站下载。 打开 [https://git-scm.com/download/win，下载会自动开始。](https://git-scm.com/download/win%EF%BC%8C%E4%B8%8B%E8%BD%BD%E4%BC%9A%E8%87%AA%E5%8A%A8%E5%BC%80%E5%A7%8B%E3%80%82) 要注意这是一个名为 Git for Windows 的项目（也叫做 msysGit），和 Git 是分别独立的项目；更多信息请访问 [http://msysgit.github.io/。](http://msysgit.github.io/%E3%80%82)

## git的使用

### 克隆仓库

克隆仓库是最简单的也是我们平时使用得最多的

```bash
$ git clone https://github.com/libgit2/libgit2
```

### 初始化仓库

初始化仓库可以在git.yuketang.net上初始化一个项目来查看

```bash
$ git init
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```

### 远程仓库

```bash
# 从远端克隆仓库
$ git clone https://github.com/schacon/ticgit
# 查看远端仓库
$ git remote -v
# 添加远程仓库
$ git remote add pb https://github.com/paulboone/ticgit
# 
$ git fetch <remote>
$ git pull
```

这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

如果你使用 clone 命令克隆了一个仓库，命令会自动将其添加为远程仓库并默认以 “origin” 为简写。 所以，git fetch origin 会抓取克隆（或上一次抓取）后新推送的所有工作。 必须注意 git fetch 命令只会将数据下载到你的本地仓库——它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。

如果你的当前分支设置了跟踪远程分支（阅读下一节和 Git 分支 了解更多信息）， 那么可以用 git pull 命令来自动抓取后合并该远程分支到当前分支。 这或许是个更加简单舒服的工作流程。默认情况下，git clone 命令会自动设置本地 master 分支跟踪克隆的远程仓库的 master 分支（或其它名字的默认分支）。 运行 git pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

### 分支

#### 创建分支

```bash
$ git branch testing
```

![](http://ossp.pengjunjie.com/mweb/15960937275830.jpg)

那么，Git 又是怎么知道当前在哪一个分支上呢？ 也很简单，它有一个名为 HEAD 的特殊指针。 请注意它和许多其它版本控制系统（如 Subversion 或 CVS）里的 HEAD 概念完全不同。 在 Git 中，它是一个指针，指向当前所在的本地分支（译注：将 HEAD 想象为当前分支的别名）。 在本例中，你仍然在 master 分支上。 因为 git branch 命令仅仅 创建 一个新分支，并不会自动切换到新分支中去。

HEAD 指向当前所在的分支。

![](http://ossp.pengjunjie.com/mweb/15960937904257.jpg)

#### 分支切换

```bash
$ git checkout testing
```

![](http://ossp.pengjunjie.com/mweb/15960938445558.jpg)

那么，这样的实现方式会给我们带来什么好处呢？ 现在不妨再提交一次：

```
$ vim test.rb
$ git commit -a -m 'made a change'
```

![](http://ossp.pengjunjie.com/mweb/15960939548577.jpg)

Figure 15. HEAD 分支随着提交操作自动向前移动

如图所示，你的 `testing` 分支向前移动了，但是 `master` 分支却没有，它仍然指向运行 `git checkout` 时所指的对象。 这就有意思了，现在我们切换回 `master` 分支看看：

```
$ git checkout master
```

![](http://ossp.pengjunjie.com/mweb/15960939835712.jpg)

Figure 16. 检出时 HEAD 随之移动

这条命令做了两件事。 一是使 HEAD 指回 `master` 分支，二是将工作目录恢复成 `master` 分支所指向的快照内容。 也就是说，你现在做修改的话，项目将始于一个较旧的版本。 本质上来讲，这就是忽略 `testing` 分支所做的修改，以便于向另一个方向进行开发。

**创建新分支的同时切换过去** 通常我们会在创建一个新分支后立即切换过去，这可以用 `git checkout -b <newbranchname>` 一条命令搞定。

> 更多内容请参考[官方文档](https://git-scm.com/book/en/v2)

## Pycharm如何集成git

## github 如何获取知识

### awesome github

github的awesome是专门用来收集某个语言或者工具的相关知识的整理汇总贴，在这上面其实可以找到很多的该类相关的知识，我们在学习每个语言之前，可以去整理一下awesome相关的知识

[awesome list](https://github.com/sindresorhus/awesome#readme)

同时我们在学习不同语言的时候，也可以找到相关的awesome知识，可以直接在github上面搜索

比如微信小程序 [awesome-wechat-weapp](https://github.com/justjavac/awesome-wechat-weapp)

django [awesome-django](https://github.com/wsvincent/awesome-django)

### 相关开源项目

相关开源项目可以通过关键字在github中搜索

搜索方法： 1. 分解关键字 2. 看排序 3. 检查更新情况 4. 查看issue

也可以通过OpenChina 开源中国来找一些比较有名的开源项目

## 有鱼git

没开通可以开通一下

[https://git.yuketang.net](https://git.yuketang.net)

使用过程： 1. 将代码克隆到本地 2. 自己建立分支 3. 分支提交，并提出合并请求
