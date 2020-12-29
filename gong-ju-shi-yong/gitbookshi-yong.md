# Gitbook使用

## 什么是Gitbook？

GitBook \[1\] 是一个基于 Node.js 的命令行工具，可使用 Github/Git 和 Markdown 来制作精美的电子书，GitBook 并非关于 Git 的教程。 GitBook支持输出多种文档格式： ·静态站点：GitBook默认输出该种格式，生成的静态站点可直接托管搭载Github Pages服务上； ·PDF：需要安装gitbook-pdf依赖； ·eBook：需要安装ebook-convert； · 单HTML网页：支持将内容输出为单页的HTML，不过一般用在将电子书格式转换为PDF或eBook的中间过程； ·JSON：一般用于电子书的调试或元数据提取。

## 如何使用gitbook

使用gitbook有两种方法，一种是直接使用gitbook官方提供的服务[gitbook legacy](https://legacy.gitbook.com/)来直接在上面进行制作和管理，完成之后可以直接在云端使用。第二种方案是使用新版本的[gitbook app](https://app.gitbook.com) 结合github来进行发布。同时两种方案最后都可以选择通过gitbook云端和本地来部署gitbook电子书供大家用

在自己的使用，其实比较推荐使用[gitbook app](https://app.gitbook.com) 结合 github的方式，这样更直观。同时在自己的服务器上起一个gitbook自动生成，在github上面配上hook之后实现自动发布，这样在[gitbook客户端](https://legacy.gitbook.com/editor)上直接编写提交后可以在页面自动发布效果。非常省事，还解决了gitbook legacy官方平台的经常莫名其妙的不发布情况。

## GitBook legacy

[gitbook客户端](https://legacy.gitbook.com/editor) 可以在这里下载。直接使用的话在legacy注册账号就能使用。

登陆后上面gitbook.com里面的内容就可以看到同步legacy中的内容。 ![-w501](http://ossp.pengjunjie.com/mweb/15571131843442.jpg)

![-w1232](http://ossp.pengjunjie.com/mweb/15571132366321.jpg)

legacy 比较简单，直接两边使用就可以了。但是在国内使用的时候legacy经常遇到各种各样的问题，无法打开、无法提交、无法发布等等。

## Gitbook APP

现在gitbook官方把legacy很多都升级到APP上了。在gitbook里面可以维护自己的space，来创建不同的gitbook。

登陆gitbook官方[gitbook app](https://app.gitbook.com) 可以注册gitbook的账号，

![-w1230](http://ossp.pengjunjie.com/mweb/15571134087687.jpg)

使用app跟客户端的连接不是很好，上去之后，并不能在客户端里面看到从APP里同步的内容。推测还是因为升级的原因导致只能同步legacy里面的项目。但是新版本的发布会比legacy好很多，所以选择使用哪个版本算是各有取舍了。

使用新版本APP的话，可以创建的时候把gitbook同步到github上，然后使用github来进行管理，同时可以通过github为媒介将项目同步到gitbook客户端上。

首先可以创建自己的组织，这样方便进行管理 ![](http://ossp.pengjunjie.com/mweb/15571145141654.jpg)

然后在自己的组织中可以创建自己的space，免费版的每个organization中只能创建一个public的space。如果不希望给别人看到也可以创建private的。

输入需要创建的名字就可以创建自己的space了

![-w603](http://ossp.pengjunjie.com/mweb/15571146862729.jpg)

后面这一步比较重要，我们是通过github进行同步，所以需要选择github同步来创建space

![-w602](http://ossp.pengjunjie.com/mweb/15571147344486.jpg)

完成后会跳到github去授权，授权完成之后会跳转回来，回到gitbook的项目选择页面

![-w802](http://ossp.pengjunjie.com/mweb/15571148094311.jpg)

可以在github新建一个项目供选择

![-w801](http://ossp.pengjunjie.com/mweb/15571148521889.jpg)

完成之后可以选择相应的分支 ![-w799](http://ossp.pengjunjie.com/mweb/15571148689568.jpg)

下面这步比较重要，如果我们是一个新项目，需要同步数据到github，那么我们需要选择 I write my content on GitBook. 如果我们在github上面已有gitbook的相应同步内容，我们需要导入到app里面的项目中去的话，我们可以选择I write my content on Github。

![-w799](http://ossp.pengjunjie.com/mweb/15571148921477.jpg)

完成后即可同步并创建相应的应用。

### 在gitbook 客户端中导入

创建完成后这个gitbook是在gitbook.com的云端，也可以直接在云端上编辑，但是体验确实不怎么样。我们可以使用gitbook客户端在本地进行编辑。由于gitbook客户端现在还没有同步app.gitbook.com上面的内容。所以我们需要进行导入。

这里主要以mac电脑上的导入方式来配置： 1. 在本地新建文件夹，然后`git clone ****** (刚才的项目地址)`到本地来 2. 在gitbook客户端中选择导入Import来导入相应的项目。 3. 导入完成后在Others里面就可以看到相应的项目了，并且这个项目是使用github同步了的 4. 在使用上传同步的时候，会提示一个提示框，在提示框中输入github的用户名密码后续可以自动进行同步。

![](http://ossp.pengjunjie.com/mweb/15571153087390.jpg)

这样每次在gitbook上面编写，并提交后，在app.gitbook.com上可以看到相应的同步。

此时直接发布gitbook的内容就可以看到更新了，这个就是使用gitbook的服务来发布gitbook文章。但是发现直接使用gitbook发布的几个问题: 1. 访问确实是慢 \(墙的问题，不过还好可以访问\) 2. 手机端访问的时候，很多手机的目录按钮无法点开，所以目录无法使用，基本上就是导致手机不能使用了。

## 在自己的服务器上部署gitbook并发布

在服务器上使用npm遍可以安装gitbook的命令行工具。没有安装npm的话可以使用`apt-get install gitbook`安装一下。

```bash
$ npm install gitbook-cli -g
#安装完成后使用-V可以查看和安装gitbook
$ gitbook -V
```

gitbook常用命令

```text
$ gitbook init # 初始化一个仓库

$ gitbook install # 安装插件

$ gitbook serve [book] # 本地预览
$ gitbook serve --port 8001 # 指定端口

$ gitbook build repository PATH # 输出一个静态网站

$ gitbook pdf book pdf # 生成pdf文件

$ gitbook help # 查看帮助
```

主要的是要记住`gitbook build`

我们将github上面的项目同步过来之后，在目录下直接gitbook build 就可以将gitbook的HTML生成出来了。 最后配上Nginx解析就可以把页面全部整理出来。

### 待完成

1. 配置github hook，每次提交之后脚本自动发布
2. 可以配置[github插件](https://github.com/apps/gitbook-legacy)可以直接在github上集成。

