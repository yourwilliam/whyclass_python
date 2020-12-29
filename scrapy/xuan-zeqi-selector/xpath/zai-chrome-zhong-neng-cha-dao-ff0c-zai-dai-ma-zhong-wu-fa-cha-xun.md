# 在chrome中能查到，在代码中无法查询

xpath在使用的时候，在chrome上调试可以找到元素，但是在代码中查出来是一个空的，情况如下：

chrome查看情况 ![-w340](http://ossp.pengjunjie.com/mweb/15572084334174.jpg)

代码debug的结果 ![-w457](http://ossp.pengjunjie.com/mweb/15572088966188.jpg)

两边写的也没有问题。

## 定位方式

在发现代码中没有找出来的时候，一般可以这几步来定位：

### 1. 使用chrome的$x\(\)来定位

首先在chrome的console面板下使用$x\(\)来定位是否存在问题。如果chrome中就无法显示出来，说明xpath本身写的就有问题，如果有，那么就说明xpath是没有问题的

![-w630](http://ossp.pengjunjie.com/mweb/15572090194621.jpg)

### 2. 使用pycharm的console来定位

同样的xpath打断点，通过console来定位，查看是否有，如果这里没有就说明xpath没有取到 ![-w1208](http://ossp.pengjunjie.com/mweb/15572090825234.jpg)

### 3. 查看原因

response.xpath\(\)的原理是针对response.body中的内容进行xpath的，chrome的xpath是通过展示出来的html来进行xpath的。这二者有时候是会有差别的，实际上有些网页的dom并不在response.body中，是通过javascript生成的dom，所以有时候查询不到。

很多时候在chrome的Elements里面的内容跟使用response中的html内容是有区别的，因为部分的HTML是由javascript生成的，所以在response做xpath的时候根本就看不到。

可以通过查看response.body 看到获取过来的html元素。更方便看的话也可以在chrome里面查看。 在Network页签中的Network处可以查看到相应的返回HTML 元素 ![-w632](http://ossp.pengjunjie.com/mweb/15572093287862.jpg)

从这里就可以看到和页面上的div的class属性是不一样的，所以可以知道实际上是通过javascript后续渲染出来的，所以在代码中这样查找找不到。所以我们需要改写

## 备注

很多时候在页面抓取的时候，需要仔细分析一下页面的组成。

有很多网页的数据是通过请求来获取的，在XHR中可以查看，如果这种接口获取json的格式，爬取起来会比xpath更简单，所以每个爬取的网页需要根据具体问题具体分析。

