# \[course] 01 python环境基础

## python 语言

![](http://ossp.pengjunjie.com/mweb/15696842566098.jpg)

## python环境安装

> 为什么要使用官方安装包？为什么不用[Anaconda](https://www.anaconda.com/distribution/)？
>
> > 1. 学会最基础的环境安装方式，了解最基本的原理，通过手动管理安装包了解python最原生的环境，并学会逐步扩充自己的环境

[官方网站](https://www.python.org/downloads/)

![](http://ossp.pengjunjie.com/mweb/15696855602253.jpg)

> 为什么不使用默认的download？
>
> > 默认的download有可能下载到32位的包，不一定适合使用，最好按照自己的需求选择安装

**安装时一定要勾选Add Python 3.7 to PATH**

![-w653](http://ossp.pengjunjie.com/mweb/15696872532522.jpg)

![-w588](http://ossp.pengjunjie.com/mweb/15696872683691.jpg)

### mac安装

打开terminal, 输入

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

$ brew install python3
```

## pycharm 安装

[pycharm下载路径](https://www.jetbrains.com/pycharm/download/#section=windows)

尽量选择下载professional版本

## 运行python

### 命令行运行模式：

#### 相应交互模式

windows 打开 powershell , Mac 打开 Terminal。

使用场景: 平时的测试，小功能使用。

#### IDLE 控制台

IDLE： 自带集成开发环境、非商业、初学者使用。

使用场景：简单的小型项目，基本不怎么使用。(可以作为知识点了解一下)

**Mac 使用 python 控制台**

```bash
# 首先通过which命令查询到
williamtekiMacBook-Pro:bin valentine$ which python3
/usr/local/Cellar/python/3.6.4_2/bin//python3

# 进入到相应目录
williamtekiMacBook-Pro:bin valentine$ cd /usr/local/Cellar/python/3.6.4_2/bin/

# 执行并启动IDLE
williamtekiMacBook-Pro:bin valentine$ idle3.6
```

完成之后可以看到IDLE

![-w587](http://ossp.pengjunjie.com/mweb/15597081424792.jpg)

**windows使用IDLE控制台**

开始菜单中直接搜索打开即可。

#### 文件运行模式

使用python命令来运行python脚本。

使用场景： 在真实生产运行环境上使用的方法。当前我们使用pycharm等工具运行python实际上也是包装的使用这种方法运行。同时后面的其他python框架也基本都是使用这种来执行。

运行方法：

windows打开powershell， mac打开terminal。

```bash
# 第一步可以使用cd找到相应的文件目录
williamtekiMacBook-Pro:python_trails01 valentine$ cd /Users/valentine/workspace/python_trails/PythonWeb/code/python_trails01
# 使用python3执行python命令
williamtekiMacBook-Pro:python_trails01 valentine$ python3 trails01.py
Hello World!noyes Hello Again
I like typing this.
This is fun.
Yay! Printing.
I'd much rather you 'not'.
I "said" do not touch this.
I
 said" do not touch this.
```

![-w566](http://ossp.pengjunjie.com/mweb/15597118379478.jpg)

这种模式一定要记住，实际上python的所有执行都是使用的这种方式。

**补充讲解： cd命令**

cd (change directory)

理解方式：在windows或者mac上，我们可以直接使用开始菜单或者快捷方式来运行程序。同时我们也可以打开资源管理器(我的电脑)或者Mac上的Finder，找到运行文件的路径，双击来运行。这种在资源管理器上切换目录的方式可以理解成命令行中的cd模式。

例子： 使用命令行打开软件 windows 下打开powershell，来打开IE浏览器 ![-w609](http://ossp.pengjunjie.com/mweb/15597115469569.jpg)

mac下打开terminal来打开keynote

![-w627](http://ossp.pengjunjie.com/mweb/15597116605483.jpg)

**补充讲解： 服务器操作模式**

我们当前使用的比如 mac、windows 10都是桌面操作系统，这些大家可能比较熟悉。桌面操作系统的优点是用户交互，让用户简便的娱乐和办公。

服务器操作系统更多的是解决文件系统、网络、安全性。

服务器操作系统简要讲述：

[知乎 - 服务器的操作系统有哪些](https://zhuanlan.zhihu.com/p/44189592)

### print 与 终端：

在服务器端操作，实际上非常重要的是人机交互。如上面讲的，如果在桌面操作系统，或者手机操作系统上，我们的交互感官是图形化界面。而在服务器上，我们的交互感官是命令提示符(可以理解成terminal终端)

print方式是python程序用于和用户交互重要的方式。也是服务器维护中使用最多的和终端用户交互方式。

### 方法调用：

方法调用的格式

`方法名(参数,参数名=参数)`

看到这种情况就一定是方法调用。

### 格式化：

MAC ： alt+cmd+L Windows: ctrl+alt+L

## Pycharm工程基本使用

### 创建学习文件夹

windows电脑建议在D盘根目录创建youyulab的文件夹，mac电脑建议在`/User/*(你的用户名)/`下创建youyulab文件夹。未来我们将所有的课程内容都可以放入这个文件夹中。

然后在文件夹中创建code目录，放置所有的code文件

#### 创建项目

打开pycharm，新建项目

![-w402](http://ossp.pengjunjie.com/mweb/15697383370825.jpg)

选择create new project，找到之前创建的code目录，点击下面的小三角，打开虚拟环境目录，确保虚拟环境创建成功

![](http://ossp.pengjunjie.com/mweb/15697384279991.jpg)

#### 创建课程文件目录

![](http://ossp.pengjunjie.com/mweb/15697394034584.jpg)

创建文件夹week1

![](http://ossp.pengjunjie.com/mweb/15697394283862.jpg)

创建文件

![](http://ossp.pengjunjie.com/mweb/15697395685813.jpg)

建议为每个功能创建一个文件

#### 运行方式
