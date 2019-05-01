# Pipeline

## 使用pipeline

当Item在Spider中被收集之后，它将会被传递到Item Pipeline，这些Item Pipeline组件按定义的顺序处理Item。

每个Item Pipeline都是实现了简单方法的Python类，比如决定此Item是丢弃而存储。以下是item pipeline的一些典型应用：

验证爬取的数据\(检查item包含某些字段，比如说name字段\) 查重\(并丢弃\) 将爬取结果保存到文件或者数据库中

### 1. 编写pipeline

```python
class ReadingJsonPipeline(object):

    def __init__(self):
        self.file = open('reading_page1.json', 'w')

    def process_item(self, item, spider):
        content = json.dumps(dict(item), ensure_ascii=False) + "\n"
        self.file.write(content)
        return item

    def close_spider(self, spider):
        self.file.close()
```

注意process\_item 一定要返回item,否则后面的链就会断掉。

### 2. 启用pipeline

为了启用Item Pipeline组件，必须将它的类添加到 settings.py文件ITEM\_PIPELINES 配置。 分配给每个类的整型值，确定了他们运行的顺序，item按数字从低到高的顺序，通过pipeline，通常将这些数字定义在0-1000范围内（0-1000随意设置，数值越低，组件的优先级越高）

```text
ITEM_PIPELINES = {
    'ieltsOnlineSpider.pipelines.ReadingJsonPipeline': 300,
}
```

### 3. 启动爬虫

scrapy crawl ielts\_online

