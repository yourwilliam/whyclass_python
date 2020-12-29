# python电脑使用基础

## 文件系统

### windows资源管理

![-w262](http://ossp.pengjunjie.com/mweb/15592838744620.jpg)

windows的文件系统以分盘分区作为核心。系统可以分为C、D、E盘等等。 每个操作系统都有一个启动盘，主分区。和若干的扩展分区。

window下直接打开我的电脑或者资源管理器可以查看全部的文件内容。

![](http://ossp.pengjunjie.com/mweb/15592845768985.jpg)

### MAC资源管理：

![-w877](http://ossp.pengjunjie.com/mweb/15592840511332.jpg)

![-w348](http://ossp.pengjunjie.com/mweb/15592840804391.jpg) MAC\(Linux\)统一使用单磁盘模式，新的自盘加入需要挂在到磁盘分区中。给所有用户看到的是单一的文件系统，没有多余的盘的概念。

MAC打开finder之后，会默认进入到当前user的目录\(也就是上文的valentine目录\)。需要使用cmd+↑键才能找到当前硬盘的根硬盘。

我们当前用户使用的文件都应该归档于当前登录的user目录下。

## 课程文件初始化

windows用户打开资源管理文件夹之后，在D盘创建youyuLab目录。

![-w768](http://ossp.pengjunjie.com/mweb/15592862590932.jpg)

Mac用户打开Finder后，选择Download文件夹。然后点击 cmd + ↑ 进入到上一层，创建目录youyulab。

文件夹创建完成后，拖动youyulab文件夹到左侧个人收藏中。可以看到个人收藏文件。

![](http://ossp.pengjunjie.com/mweb/15592869433109.jpg)

mac和windows用户： 进去之后首先创建pythontrails目录，第一阶段的课程内容可以放置在这里面，再在里面从创建code目录。

## 命令提示符的使用

windows命令提示符，MAC终端，基本的python命令是通过终端来进行的。在服务器上会经常使用命令控制台，在windows上使用较少。

### windows电脑命令提示符

在windows下可以使用命令提示符\(CMD\)或者powershell。都是直接在window中输入即可。 ![-w1280](http://ossp.pengjunjie.com/mweb/15592836446652.jpg)

![-w978](http://ossp.pengjunjie.com/mweb/15592837712466.jpg)

找到自己的目录使用

![-w551](http://ossp.pengjunjie.com/mweb/15592881352535.jpg)

在其中使用python即可访问

![-w744](http://ossp.pengjunjie.com/mweb/15592881708036.jpg)

### mac使用终端

mac进入终端可以使用 cmd + 空格， 然后输入终端。 或者通过Launchpad-&gt;其他-&gt;终端进入。

![-w472](http://ossp.pengjunjie.com/mweb/15592884164735.jpg)

进入之后输入 `cd /User/你的用户名/youyulab`进入到项目界面，同样输入python即可进入python命令行

