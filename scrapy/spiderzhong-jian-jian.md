Spider中间件(Middleware) 
Spider中间件是介入到Scrapy的spider处理机制的钩子框架，您可以添加代码来处理发送给 [Spiders](spiders.html#topics-spiders) 的response及spider产生的item和request。

## 激活spider中间件 

要启用spider中间件，您可以将其加入到 [SPIDER_MIDDLEWARES](settings.html#std:setting-SPIDER_MIDDLEWARES) 设置中。 该设置是一个字典，键位中间件的路径，值为中间件的顺序(order)。

样例:

```
SPIDER_MIDDLEWARES = {
    'myproject.middlewares.CustomSpiderMiddleware': 543,
}
```

[SPIDER_MIDDLEWARES](settings.html#std:setting-SPIDER_MIDDLEWARES) 设置会与Scrapy定义的 [SPIDER_MIDDLEWARES_BASE](settings.html#std:setting-SPIDER_MIDDLEWARES_BASE) 设置合并(但不是覆盖)， 而后根据顺序(order)进行排序，最后得到启用中间件的有序列表: 第一个中间件是最靠近引擎的，最后一个中间件是最靠近spider的。

关于如何分配中间件的顺序请查看 [SPIDER_MIDDLEWARES_BASE](settings.html#std:setting-SPIDER_MIDDLEWARES_BASE) 设置，而后根据您想要放置中间件的位置选择一个值。 由于每个中间件执行不同的动作，您的中间件可能会依赖于之前(或者之后)执行的中间件，因此顺序是很重要的。

如果您想禁止内置的(在 [SPIDER_MIDDLEWARES_BASE](settings.html#std:setting-SPIDER_MIDDLEWARES_BASE) 中设置并默认启用的)中间件， 您必须在项目的 [SPIDER_MIDDLEWARES](settings.html#std:setting-SPIDER_MIDDLEWARES) 设置中定义该中间件，并将其值赋为 `None` 。 例如，如果您想要关闭off-site中间件:

```
SPIDER_MIDDLEWARES = {
    'myproject.middlewares.CustomSpiderMiddleware': 543,
    'scrapy.contrib.spidermiddleware.offsite.OffsiteMiddleware': None,
}
```

最后，请注意，有些中间件需要通过特定的设置来启用。更多内容请查看相关中间件文档。

## 编写您自己的spider中间件

编写spider中间件十分简单。每个中间件组件是一个定义了以下一个或多个方法的Python类:

* /class/ `scrapy.contrib.spidermiddleware.` `SpiderMiddleware` (#scrapy.contrib.spidermiddleware.SpiderMiddleware)
	* `process_spider_input` ( /response/, /spider/ ) (#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_input)
	* 当response通过spider中间件时，该方法被调用，处理该response。

	* [process_spider_input()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_input) 应该返回 `None` 或者抛出一个异常。

	* 如果其返回 `None` ，Scrapy将会继续处理该response，调用所有其他的中间件直到spider处理该response。

	* 如果其跑出一个异常(exception)，Scrapy将不会调用任何其他中间件的 [process_spider_input()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_input) 方法，并调用request的errback。 errback的输出将会以另一个方向被重新输入到中间件链中，使用 [process_spider_output()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_output) 方法来处理，当其抛出异常时则带调用 [process_spider_exception()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_exception) 。

	* 参数:

		* *response* ( [Response](request-response.html#scrapy.http.Response) 对象) – 被处理的response
		* *spider* ( [Spider](spiders.html#scrapy.spider.Spider) 对象) – 该response对应的spider

	* `process_spider_output` ( /response/, /result/, /spider/ )(#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_output)
	* 当Spider处理response返回result时，该方法被调用。

	* [process_spider_output()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_output) 必须返回包含 [Request](request-response.html#scrapy.http.Request) 或 [Item](items.html#scrapy.item.Item) 对象的可迭代对象(iterable)。

	* 参数:

		* *response* ( [Response](request-response.html#scrapy.http.Response) 对象) – 生成该输出的response
		* *result* (包含 [Request](request-response.html#scrapy.http.Request) 或 [Item](items.html#scrapy.item.Item) 对象的可迭代对象(iterable)) – spider返回的result
		* *spider* ( [Spider](spiders.html#scrapy.spider.Spider) 对象) – 其结果被处理的spider

	* `process_spider_exception` ( /response/, /exception/, /spider/ ) (#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_exception)
	* 当spider或(其他spider中间件的) [process_spider_input()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_input) 跑出异常时， 该方法被调用。

	* [process_spider_exception()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_exception) 必须要么返回 `None` ， 要么返回一个包含 [Response](request-response.html#scrapy.http.Response) 或 [Item](items.html#scrapy.item.Item) 对象的可迭代对象(iterable)。

	* 如果其返回 `None` ，Scrapy将继续处理该异常，调用中间件链中的其他中间件的 [process_spider_exception()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_exception) 方法，直到所有中间件都被调用，该异常到达引擎(异常将被记录并被忽略)。

	* 如果其返回一个可迭代对象，则中间件链的 [process_spider_output()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_output) 方法被调用， 其他的 [process_spider_exception()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_exception) 将不会被调用。

	* 参数:

		* *response* ( [Response](request-response.html#scrapy.http.Response) 对象) – 异常被抛出时被处理的response
		* *exception* ( [Exception](http://docs.python.org/library/exceptions.html#exceptions.Exception) 对象) – 被跑出的异常
		* *spider* ( [Spider](spiders.html#scrapy.spider.Spider) 对象) – 抛出该异常的spider

	* `process_start_requests` ( /start_requests/, /spider/ ) (#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_start_requests)
	* 0.15 新版功能.

	* 该方法以spider 启动的request为参数被调用，执行的过程类似于 [process_spider_output()](#scrapy.contrib.spidermiddleware.SpiderMiddleware.process_spider_output) ，只不过其没有相关联的response并且必须返回request(不是item)。

	* 其接受一个可迭代的对象( `start_requests` 参数)且必须返回另一个包含 [Request](request-response.html#scrapy.http.Request) 对象的可迭代对象。

	* 注解

	* 当在您的spider中间件实现该方法时， 您必须返回一个可迭代对象(类似于参数start_requests)且不要遍历所有的 `start_requests` 。 该迭代器会很大(甚至是无限)，进而导致内存溢出。 Scrapy引擎在其具有能力处理start request时将会拉起request， 因此start request迭代器会变得无限，而由其他参数来停止spider( 例如时间限制或者item/page记数)。

	* 参数:

		* *start_requests* (包含 [Request](request-response.html#scrapy.http.Request) 的可迭代对象) – start requests
		* *spider* ( [Spider](spiders.html#scrapy.spider.Spider) 对象) – start requests所属的spider

## 内置spider中间件参考手册

本页面介绍了Scrapy自带的所有spider中间件。关于如何使用及编写您自己的中间件，请参考 [spider middleware usage guide](#topics-spider-middleware).

关于默认启用的中间件列表(及其顺序)请参考 [SPIDER_MIDDLEWARES_BASE](settings.html#std:setting-SPIDER_MIDDLEWARES_BASE) 设置。

### DepthMiddleware

* /class/ `scrapy.contrib.spidermiddleware.depth.` `DepthMiddleware` [¶](#scrapy.contrib.spidermiddleware.depth.DepthMiddleware)
* DepthMiddleware是一个用于追踪每个Request在被爬取的网站的深度的中间件。 其可以用来限制爬取深度的最大深度或类似的事情。

* [DepthMiddleware](#scrapy.contrib.spidermiddleware.depth.DepthMiddleware) 可以通过下列设置进行配置(更多内容请参考设置文档):

	* [DEPTH_LIMIT](settings.html#std:setting-DEPTH_LIMIT) - 爬取所允许的最大深度，如果为0，则没有限制。
	* [DEPTH_STATS](settings.html#std:setting-DEPTH_STATS) - 是否收集爬取状态。
	* [DEPTH_PRIORITY](settings.html#std:setting-DEPTH_PRIORITY) - 是否根据其深度对requet安排优先级

### HttpErrorMiddleware 

* /class/ `scrapy.contrib.spidermiddleware.httperror.` `HttpErrorMiddleware` (#scrapy.contrib.spidermiddleware.httperror.HttpErrorMiddleware)
* 过滤出所有失败(错误)的HTTP response，因此spider不需要处理这些request。 处理这些request意味着消耗更多资源，并且使得spider逻辑更为复杂。

根据 [HTTP标准](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) ，返回值为200-300之间的值为成功的resonse。

如果您想处理在这个范围之外的response，您可以通过 spider的 `handle_httpstatus_list` 属性或 [HTTPERROR_ALLOWED_CODES](#std:setting-HTTPERROR_ALLOWED_CODES) 设置来指定spider能处理的response返回值。

例如，如果您想要处理返回值为404的response您可以这么做:

```
class MySpider(CrawlSpider):
    handle_httpstatus_list = [404]
```

[Request.meta](request-response.html#scrapy.http.Request.meta) 中的 `handle_httpstatus_list` 键也可以用来指定每个request所允许的response code。

不过请记住，除非您知道您在做什么，否则处理非200返回一般来说是个糟糕的决定。

更多内容请参考: [HTTP Status Code定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).

#### HttpErrorMiddleware settings 

##### HTTPERROR_ALLOWED_CODES 

默认: `[]`

忽略该列表中所有非200状态码的response。

##### HTTPERROR_ALLOW_ALL

默认: `False`

忽略所有response，不管其状态值。

### OffsiteMiddleware 

* /class/ `scrapy.contrib.spidermiddleware.offsite.` `OffsiteMiddleware` [¶](#scrapy.contrib.spidermiddleware.offsite.OffsiteMiddleware)
* 过滤出所有URL不由该spider负责的Request。

* 该中间件过滤出所有主机名不在spider属性 [allowed_domains](spiders.html#scrapy.spider.Spider.allowed_domains) 的request。

* 当spide返回一个主机名不属于该spider的request时， 该中间件将会做一个类似于下面的记录:

```
DEBUG: Filtered offsite request to 'www.othersite.com': <GET http://www.othersite.com/some/page.html>
```

* 为了避免记录太多无用信息，其将对每个新发现的网站记录一次。因此，例如， 如果过滤出另一个 `[www.othersite.com](http://www.othersite.com)` 请求，将不会有新的记录。 但如果过滤出 `[someothersite.com](http://someothersite.com)` 请求，仍然会有记录信息(仅针对第一次)。

* 如果spider没有定义 [allowed_domains](spiders.html#scrapy.spider.Spider.allowed_domains) 属性，或该属性为空， 则offsite 中间件将会允许所有request。

* 如果request设置了 `dont_filter` 属性， 即使该request的网站不在允许列表里，则offsite中间件将会允许该request。

### RefererMiddleware 

* /class/ `scrapy.contrib.spidermiddleware.referer.` `RefererMiddleware` (#scrapy.contrib.spidermiddleware.referer.RefererMiddleware)
* 根据生成Request的Response的URL来设置Request `Referer` 字段。

#### RefererMiddleware settings

##### REFERER_ENABLED 

0.15 新版功能.

默认: `True`

是否启用referer中间件。

### UrlLengthMiddleware

* /class/ `scrapy.contrib.spidermiddleware.urllength.` `UrlLengthMiddleware` (#scrapy.contrib.spidermiddleware.urllength.UrlLengthMiddleware)
* 过滤出URL长度比URLLENGTH_LIMIT的request。

* [UrlLengthMiddleware](#scrapy.contrib.spidermiddleware.urllength.UrlLengthMiddleware) 可以通过下列设置进行配置(更多内容请参考设置文档):

	* [URLLENGTH_LIMIT](settings.html#std:setting-URLLENGTH_LIMIT) - 允许爬取URL最长的长度.