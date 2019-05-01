# Spider

## Spider

Spider类定义了如何爬取某个\(或某些\)网站。包括了爬取的动作\(例如:是否跟进链接\)以及如何从网页的内容中提取结构化数据\(爬取item\)。 换句话说，Spider就是您定义爬取的动作及分析某个网页\(或者是有些网页\)的地方。

class scrapy.Spider是最基本的类，所有编写的爬虫必须继承这个类。

主要用到的函数及调用顺序为：

**init**\(\) : 初始化爬虫名字和start\_urls列表

start\_requests\(\) 调用make\_requests\_from url\(\):生成Requests对象交给Scrapy下载并返回response

parse\(\) : 解析response，并返回Item或Requests（需指定回调函数）。Item传给Item pipline持久化 ， 而Requests交由Scrapy下载，并由指定的回调函数处理（默认parse\(\)\)，一直进行循环，直到处理完所有的数据为止。

