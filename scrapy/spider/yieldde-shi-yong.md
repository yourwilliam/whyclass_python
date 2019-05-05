# scrapy yield的使用

scrapy 使用yield可以指定返回的内容

```py
# 发送新的url请求加入待爬队列，并调用回调函数 self.parse
yield scrapy.Request(url, callback = self.parse)

# 将获取的数据交给pipeline
yield item

```

所以使用Request的时候也可以指定其他的callback，这样就可以定义不同的通道了

> 1. 因为使用的yield，而不是return。parse函数将会被当做一个生成器使用。scrapy会逐一获取parse方法中生成的结果，并判断该结果是一个什么样的类型；
> 2. 如果是request则加入爬取队列，如果是item类型则使用pipeline处理，其他类型则返回错误信息。
> 3. scrapy取到第一部分的request不会立马就去发送这个request，只是把这个request放到队列里，然后接着从生成器里获取；
> 4. 取尽第一部分的request，然后再获取第二部分的item，取到item了，就会放到对应的pipeline里处理；
> 5. parse()方法作为回调函数(callback)赋值给了Request，指定parse()方法来处理这些请求 scrapy.Request(url, callback=self.parse)
> 6. Request对象经过调度，执行生成 scrapy.http.response()的响应对象，并送回给parse()方法，直到调度器中没有Request（递归的思路）
> 7. 取尽之后，parse()工作结束，引擎再根据队列和pipelines中的内容去执行相应的操作；
> 8. 程序在取得各个页面的items前，会先处理完之前所有的request队列里的请求，然后再提取items。
> 7. 这一切的一切，Scrapy引擎和调度器将负责到底。


##不同类型的item进入不同的pipeline

```py
from items import AspiderItem, BspiderItem, CspiderItem
 
class myspiderPipeline(object):
    def __init__(self):
        pass
 
    def process_item(self, item, spider):
        if isinstance(item, AspiderItem):
            pass
        elif isinstance(item, BspiderItem):
            return item
        elif isinstance(item, CspiderItem):
            print item
            return item

  转自——https://blog.csdn.net/weixin_38859557/article/details/86220472 