# github markdown blog 

## 安装Git

Git安装指南可以参考廖雪峰的博客

[安装Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

## 注册github用户

github用户直接注册就可以，此步骤不在这里过多讨论

## 配置github 页面

进入到自己的主页之后需要创建一个代码仓库

![](http://ossp.pengjunjie.com/mweb/15648456758933.jpg)

创建代码仓库的时候，特别注意，使用特定的名字  username.github.io 

![](http://ossp.pengjunjie.com/mweb/15648457915019.jpg)

下载模板

很多网站提供了丰富的jekyll模板，其中包含**[jekyllthemes.org](http://jekyllthemes.org/)**也可以快速的去找到很多的jekyll主题。

选中一个之后，Homepage一般是该站的github地址源码。其中demo是其他做的可以查看的示范站，Download是下载相关的代码。

我们找主题去做blog的时候，尽量的去找代码中有blog的，同时在源码中有_posts文件夹的主题。这样更好的修改为blog。

![](http://ossp.pengjunjie.com/mweb/15648531200228.jpg)



创建gitblog目录。我们将自己的代码内容下载到自己管理目录中。

![-w339](http://ossp.pengjunjie.com/mweb/15648461957047.jpg)

git clone下载到本地

![](http://ossp.pengjunjie.com/mweb/15648462374539.jpg)


```shell
#首先一定要进入到创建的gitbook目录
$ cd gitbook
$ git clone https://github.com/yourwilliam/yourwilliam.github.io.git
Cloning into 'yourwilliam.github.io'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
```

将模板中的文件拷贝到目录下

![](http://ossp.pengjunjie.com/mweb/15648464133872.jpg)

将所有文件拷贝到我们clone后生成的项目文件夹之后，我们可以将这些新增的文件提交到代码仓库中去。

```sh
$ cd yourwilliam.github.io/
$ git add .
$ git commit -m 'initial'
$ git push origin master
```

提交之后我们刷新github的网页可以看到这个项目中的数据已经添加了。我们再使用其中的settings，来确保网站的正常发布

![](http://ossp.pengjunjie.com/mweb/15648468840503.jpg)


在settings的中可以查看Github Pages是否是published，如果是的表示所有配置完毕

![](http://ossp.pengjunjie.com/mweb/15648474193329.jpg)

查看页面，为什么会这样？ —— 是不是CSS未加载。如何定位这个问题
![](http://ossp.pengjunjie.com/mweb/15648474781433.jpg)



更新_config.yml，来修改网站未自己相关的知识内容

```md

# Site settings
title: william blog
description: 'william blog - a github blog center'
url: 'http://yourwilliam.github.io'
baseurl: '/'
# google_analytics: 'UA-XXXXXX-X'
# disqus_shortname: 'your-disqus-name'

author:
  name: 'william'
  email: yourwilliam@gmail.com
  twitter_username: yourwilliam
  facebook_username: yourwilliam
  github_username:  yourwilliam
  linkedin_username:  yourwilliam

```

更新github

```sh
$ git add .
$ git commit 'modify config'
$ git push origin master
```


提交后刷新即可

![](http://ossp.pengjunjie.com/mweb/15648477192031.jpg)

## 制作blog修改方式

打开typora, 选择右下角的打开文件夹，找到前面的_posts文件夹，导入即可

![](http://ossp.pengjunjie.com/mweb/15648504826891.jpg)

未来所有的blog文件夹都在这个地方，也是在这个地方修改

文章修改后，可以再次上传，即可以完成更新

```sh
$ git add .
$ git commit 'modify config'
$ git push origin master
```


### 解决blog图片问题

默认的在typora添加图片之后，typora会生成一个asset文件夹，然后将图片放入其中，同时会将文章中的图片引入到这个地址。如果按照默认的方式提交到github上，文章中会无法显示图片。

修改默认的图片指向方式

修改_config.yml文件，将让文章只显示单层目录。
```markdown
permalink: /:title/
```

然后修改typora配置，让图片自动保存在images目录中。

首先在images文件夹下创建一个blog文件夹

![](http://ossp.pengjunjie.com/mweb/15648512771182.jpg)

然后修改typora配置

![](http://ossp.pengjunjie.com/mweb/15648514117688.jpg)

在图片插入中选择 **复制到制定路径** ， 然后在下面使用相对路径(千万不要使用绝对路径)，相对路径输入`../images/blog`

tips:

这里的路径模式很重要，根据不同的jekyll模板，我们可能会对路径做不同的调整，需要知道整个的模板原理才能自行修改

**这里修改之后要特别注意，其他的文件夹也会沿用这种模式。**


修改好之后，所有粘贴到typora中的图片都能自动的发布到git上去。

## 如何更新blog

前面已经将typora的整个编辑模式和配置修改完毕，我们现在可以继续添加自己的blog了。

![](http://ossp.pengjunjie.com/mweb/15648520256039.jpg)

将markdown的文件内容导入到文章中，或者直接在typora中写相应的blog。注意文章中的图片信息，如果是觉得路径的话，需要修改为相对路径（这种建议可以批量替换）

![](http://ossp.pengjunjie.com/mweb/15648523384339.jpg)

文章内容整理完毕之后我们可以添加文件头，文件头特别重要，相应的内容都使用文件头来记录。一定需要填写。

![](http://ossp.pengjunjie.com/mweb/15648524522347.jpg)


完成后我们做下一步，修改文件名，文件名很重要，需要按照相应的规则填写，我们将文件名修改为

这几行的具体说明：

#### 什么是 YAML ？

YAML 指的是一个文件的头信息。你可以用它来定义这篇文章的写作时间、标题、引用图片等等。每个文章都必须要有头信息才能被模版正确地读取。

头信息的内容被夹在两行 --- 之间，你需要将它放在整个文章的最上方。每个模版对于 YAML 的定义不同。一般在你的模版中的 _post 文件夹中一定有几篇预置的文章。用文本编辑器打开它，你就能看到你所需要的头信息了，比如说我的模版：

```html
layout: post
title: 'Jekyll + Github = 简单搭建一个个人博客'
subtitle: ‘轻量化静态博客搭建指南’
date: 2018-08-08
categories: Jekyll+GitHub
cover: '../../../assets/img/Jekyll-header.jpg'
tags: Jekyll Github Gitee Markdown HTML JavaScript
```
不同的模版参数的格式都不同，不过以我的为例，其中这些参数有以下作用：

layout：选定一个模版文件，一般不需要改
title：文章的标题名
subtitle：文章的小标题
date：文章的时间
catagories：文章的分类，不同分类可用空格分割
cover：文章的封面图片位置
tags：文章的标签。类似于catagories，可以分的更细一些

![](http://ossp.pengjunjie.com/mweb/15648525254639.jpg)

修改完成后提交查看相应效果

```sh
$ git add .
$ git commit '提交提一篇文章'
$ git push origin master
```


![](http://ossp.pengjunjie.com/mweb/15648528105374.jpg)


## 好处

1. 由于git的版本管理特性，你永远不会丢失你的blog内容。
2. 由于Git的版本特性，你可以经常使用，方便的回复到某个需要的版本节点
3. markdown写作的blog，方便转换到其他的方式提交的blog
4. jekyll的模板类型比较丰富，可以快速的修改自己的样式
5. 这样你可以平时使用typora来写整理自己的笔记，整理完之后直接同步到github上面展示。

## 遗留问题

1. 工具是提升效率的，一定要养成使用工具提升效率的好习惯。
2. 有HTML经验的可以修改一下这个模板，改成自己更喜欢的模式
3. 使用这中工具是否可以形成一个自己的链接中心
4. 自己买一个域名，使用@标签来讲域名跳转到你的blog页面
    1. 在百度站长提交一个索引来索引你的网站
5. **坚持写——坚持写——坚持写**
6. 学习之后是否可以用其他的样式模板，来改写成jekyll模板

> 参考文章
> [Jekyll + Github = 简单搭建一个个人博客](https://my.oschina.net/u/3729927/blog/1930704)