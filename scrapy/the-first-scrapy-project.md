# The first scrapy project

## 第一个爬虫项目

## 创建项目

在开始爬取之前，必须创建一个新的Scrapy项目。

```text
scrapy startproject ielts_online_spider
```

## 制作爬虫

生成一个爬虫

```python
scrapy genspider ielts_online "ieltsonlinetests.com"
```

将start\_urls的值修改为需要爬取的第一个url

```python
    start_urls = ['https://ieltsonlinetests.com/ielts-recent-actual-test-answers-vol-6-reading-practice-test-1/solution']
```

修改parse\(\)方法

```python
    def parse(self, response):
        filename = "reading_page1.html"
        open(filename, 'w').write(str(response.body))
```

然后运行一下看看，在mySpider目录下执行：

```bash
scrapy crawl ielts_online
```

查看HTML文件可以看到已经写出

## 取爬虫数据

### 构建自己的spider存储对象

打开mySpider目录下的items.py

Item 定义结构化数据字段，用来保存爬取到的数据，有点像Python中的dict，但是提供了一些额外的保护减少错误。

可以通过创建一个 scrapy.Item 类， 并且定义类型为 scrapy.Field的类属性来定义一个Item（可以理解成类似于ORM的映射关系）。

接下来，创建一个ItcastItem 类，和构建item模型（model）。

```python
class ArticalItem(scrapy.Item):
    title = scrapy.Field()
    content = scrapy.Field()
```

### 取数据

取出所有的文章，然后遍历逐步的写入到文章的内容中去

```python
# -*- coding: utf-8 -*-
import scrapy
from ieltsOnlineSprider.items import ArticalItem


class IeltsOnlineSpider(scrapy.Spider):
    name = 'ielts_online'
    allowed_domains = ['ieltsonlinetests.com']
    start_urls = ['https://ieltsonlinetests.com/ielts-recent-actual-test-answers-vol-6-reading-practice-test-1/solution']

    def parse(self, response):
        items = []

        for each in response.xpath('//*[@id="slpit-two"]/div[1]/div'):
            item = ArticalItem()

            title = each.xpath('h2/text()').extract()
            content = each.xpath('div[3]').extract()

            item['title'] = title
            item['content'] = content

            items.append(item)

        return items
```

### 执行测试

直接使用returns的时候，可以将return的内容写到不同的类型的文件中去。

```bash
# json格式，默认为Unicode编码
scrapy crawl ielts_online -o reading_page1.json

# json lines格式，默认为Unicode编码
scrapy crawl ielts_online -o reading_page1.jsonl

# csv 逗号表达式，可用Excel打开
scrapy crawl ielts_online -o reading_page1.csv

# xml格式
scrapy crawl ielts_online -o reading_page1.xml
```

