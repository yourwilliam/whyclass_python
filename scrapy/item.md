# Item 

爬取的主要目标就是从非结构性的数据源提取结构性数据，例如网页。 Scrapy提供 Item 类来满足这样的需求。

Item 对象是种简单的容器，保存了爬取到得数据。 其提供了 类似于词典(dictionary-like) 的API以及用于声明可用字段的简单语法。

## 声明Item
Item使用简单的class定义语法以及 Field 对象来声明。例如:

```py
import scrapy

class Product(scrapy.Item):
    name = scrapy.Field()
    price = scrapy.Field()
    stock = scrapy.Field()
    last_updated = scrapy.Field(serializer=str)
```

scrapy的item比django的Model要简单很多，没有很多复杂的字段类型。只有Field()方法即可。 
