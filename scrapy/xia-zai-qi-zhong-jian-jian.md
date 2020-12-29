# 下载器中间件

下载器中间件是介于Scrapy的request/response处理的钩子框架。 是用于全局修改Scrapy request和response的一个轻量、底层的系统。

## 激活下载器中间件

要激活下载器中间件组件，将其加入到 [DOWNLOADER\_MIDDLEWARES](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES) 设置中。 该设置是一个字典\(dict\)，键为中间件类的路径，值为其中间件的顺序\(order\)。

这里是一个例子:

```text
DOWNLOADER_MIDDLEWARES = {
    'myproject.middlewares.CustomDownloaderMiddleware': 543,
}
```

[DOWNLOADER\_MIDDLEWARES](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES) 设置会与Scrapy定义的 [DOWNLOADER\_MIDDLEWARES\_BASE](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES_BASE) 设置合并\(但不是覆盖\)， 而后根据顺序\(order\)进行排序，最后得到启用中间件的有序列表: 第一个中间件是最靠近引擎的，最后一个中间件是最靠近下载器的。

关于如何分配中间件的顺序请查看 [DOWNLOADER\_MIDDLEWARES\_BASE](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES_BASE) 设置，而后根据您想要放置中间件的位置选择一个值。 由于每个中间件执行不同的动作，您的中间件可能会依赖于之前\(或者之后\)执行的中间件，因此顺序是很重要的。

如果您想禁止内置的\(在 [DOWNLOADER\_MIDDLEWARES\_BASE](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES_BASE) 中设置并默认启用的\)中间件， 您必须在项目的 [DOWNLOADER\_MIDDLEWARES](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES) 设置中定义该中间件，并将其值赋为 `None` 。 例如，如果您想要关闭user-agent中间件:

```text
DOWNLOADER_MIDDLEWARES = {
    'myproject.middlewares.CustomDownloaderMiddleware': 543,
    'scrapy.contrib.downloadermiddleware.useragent.UserAgentMiddleware': None,
}
```

最后，请注意，有些中间件需要通过特定的设置来启用。更多内容请查看相关中间件文档。

## 编写您自己的下载器中间件

编写下载器中间件十分简单。每个中间件组件是一个定义了以下一个或多个方法的Python类:

* /class/ `scrapy.contrib.downloadermiddleware.` `DownloaderMiddleware` \(\#scrapy.contrib.downloadermiddleware.DownloaderMiddleware\)
  * `process_request` \( /request/, /spider/ \)\(\#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process\_request\)
  * 当每个request通过下载中间件时，该方法被调用。
  * [process\_request\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_request) 必须返回其中之一: 返回 `None` 、返回一个 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象、返回一个 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象或raise [IgnoreRequest](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/exceptions.html#scrapy.exceptions.IgnoreRequest) 。
  * 如果其返回 `None` ，Scrapy将继续处理该request，执行其他的中间件的相应方法，直到合适的下载器处理函数\(download handler\)被调用， 该request被执行\(其response被下载\)。
  * 如果其返回 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象，Scrapy将不会调用 /任何/ 其他的 [process\_request\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_request) 或 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 方法，或相应地下载函数； 其将返回该response。 已安装的中间件的 [process\_response\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_response) 方法则会在每个response返回时被调用。
  * 如果其返回 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象，Scrapy则停止调用 process\_request方法并重新调度返回的request。当新返回的request被执行后， 相应地中间件链将会根据下载的response被调用。
  * 如果其raise一个 [IgnoreRequest](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/exceptions.html#scrapy.exceptions.IgnoreRequest) 异常，则安装的下载中间件的 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 方法会被调用。如果没有任何一个方法处理该异常， 则request的errback\( `Request.errback` \)方法会被调用。如果没有代码处理抛出的异常， 则该异常被忽略且不记录\(不同于其他异常那样\)。
  * 参数:
    * _request_ \( [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象\) – 处理的request
    * _spider_ \( [Spider](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/spiders.html#scrapy.spider.Spider) 对象\) – 该request对应的spider
  * `process_response` \( /request/, /response/, /spider/ \) \(\#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process\_response\)
  * [process\_request\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_request) 必须返回以下之一: 返回一个 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象、 返回一个 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象或raise一个 [IgnoreRequest](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/exceptions.html#scrapy.exceptions.IgnoreRequest) 异常。
  * 如果其返回一个 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) \(可以与传入的response相同，也可以是全新的对象\)， 该response会被在链中的其他中间件的 [process\_response\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_response) 方法处理。
  * 如果其返回一个 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象，则中间件链停止， 返回的request会被重新调度下载。处理类似于 [process\_request\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_request) 返回request所做的那样。
  * 如果其抛出一个 [IgnoreRequest](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/exceptions.html#scrapy.exceptions.IgnoreRequest) 异常，则调用request的errback\( `Request.errback` \)。 如果没有代码处理抛出的异常，则该异常被忽略且不记录\(不同于其他异常那样\)。
  * 参数:
    * _request_ \( [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象\) – response所对应的request
    * _response_ \( [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象\) – 被处理的response
    * _spider_ \( [Spider](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/spiders.html#scrapy.spider.Spider) 对象\) – response所对应的spider
  * `process_exception` \( /request/, /exception/, /spider/ \) \(\#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process\_exception\)
  * 当下载处理器\(download handler\)或 [process\_request\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_request) \(下载中间件\)抛出异常\(包括 [IgnoreRequest](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/exceptions.html#scrapy.exceptions.IgnoreRequest) 异常\)时， Scrapy调用 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 。
  * [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 应该返回以下之一: 返回 `None` 、 一个 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象、或者一个 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象。
  * 如果其返回 `None` ，Scrapy将会继续处理该异常，接着调用已安装的其他中间件的 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 方法，直到所有中间件都被调用完毕，则调用默认的异常处理。
  * 如果其返回一个 [Response](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Response) 对象，则已安装的中间件链的 [process\_response\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_response) 方法被调用。Scrapy将不会调用任何其他中间件的 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 方法。
  * 如果其返回一个 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象， 则返回的request将会被重新调用下载。这将停止中间件的 [process\_exception\(\)](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.DownloaderMiddleware.process_exception) 方法执行，就如返回一个response的那样。
  * 参数:
    * _request_ \(是 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象\) – 产生异常的request
    * _exception_ \( `Exception` 对象\) – 抛出的异常
    * _spider_ \( [Spider](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/spiders.html#scrapy.spider.Spider) 对象\) – request对应的spider

## 内置下载中间件参考手册

本页面介绍了Scrapy自带的所有下载中间件。关于如何使用及编写您自己的中间件，请参考 [downloader middleware usage guide](xia-zai-qi-zhong-jian-jian.md#topics-downloader-middleware).

关于默认启用的中间件列表\(及其顺序\)请参考 [DOWNLOADER\_MIDDLEWARES\_BASE](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_MIDDLEWARES_BASE) 设置。

### CookiesMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.cookies.` `CookiesMiddleware` \(\#scrapy.contrib.downloadermiddleware.cookies.CookiesMiddleware\)
* 该中间件使得爬取需要cookie\(例如使用session\)的网站成为了可能。 其追踪了web server发送的cookie，并在之后的request中发送回去， 就如浏览器所做的那样。

以下设置可以用来配置cookie中间件:

* [COOKIES\_ENABLED](xia-zai-qi-zhong-jian-jian.md#std:setting-COOKIES_ENABLED)
* [COOKIES\_DEBUG](xia-zai-qi-zhong-jian-jian.md#std:setting-COOKIES_DEBUG)

  **单spider多cookie session**

0.15 新版功能.

Scrapy通过使用 [cookiejar](xia-zai-qi-zhong-jian-jian.md#std:reqmeta-cookiejar) Request meta key来支持单spider追踪多cookie session。 默认情况下其使用一个cookie jar\(session\)，不过您可以传递一个标示符来使用多个。

例如:

```text
for i, url in enumerate(urls):
    yield scrapy.Request("http://www.example.com", meta={'cookiejar': i},
        callback=self.parse_page)
```

需要注意的是 [cookiejar](xia-zai-qi-zhong-jian-jian.md#std:reqmeta-cookiejar) meta key不是”黏性的\(sticky\)”。 您需要在之后的request请求中接着传递。例如:

```text
def parse_page(self, response):
    # do some processing
    return scrapy.Request("http://www.example.com/otherpage",
        meta={'cookiejar': response.meta['cookiejar']},
        callback=self.parse_other_page)
```

#### COOKIES\_ENABLED

默认: `True`

是否启用cookies middleware。如果关闭，cookies将不会发送给web server。

#### COOKIES\_DEBUG

默认: `False`

如果启用，Scrapy将记录所有在request\( `Cookie` 请求头\)发送的cookies及response接收到的cookies\( `Set-Cookie` 接收头\)。

下边是启用 [COOKIES\_DEBUG](xia-zai-qi-zhong-jian-jian.md#std:setting-COOKIES_DEBUG) 的记录的样例:

```text
2011-04-06 14:35:10-0300 [diningcity] INFO: Spider opened
2011-04-06 14:35:10-0300 [diningcity] DEBUG: Sending cookies to: <GET http://www.diningcity.com/netherlands/index.html>
        Cookie: clientlanguage_nl=en_EN
2011-04-06 14:35:14-0300 [diningcity] DEBUG: Received cookies from: <200 http://www.diningcity.com/netherlands/index.html>
        Set-Cookie: JSESSIONID=B~FA4DC0C496C8762AE4F1A620EAB34F38; Path=/
        Set-Cookie: ip_isocode=US
        Set-Cookie: clientlanguage_nl=en_EN; Expires=Thu, 07-Apr-2011 21:21:34 GMT; Path=/
2011-04-06 14:49:50-0300 [diningcity] DEBUG: Crawled (200) <GET http://www.diningcity.com/netherlands/index.html> (referer: None)
[...]
```

### DefaultHeadersMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.defaultheaders.` `DefaultHeadersMiddleware` \(\#scrapy.contrib.downloadermiddleware.defaultheaders.DefaultHeadersMiddleware\)
* 该中间件设置 [DEFAULT\_REQUEST\_HEADERS](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DEFAULT_REQUEST_HEADERS) 指定的默认request header。

### DownloadTimeoutMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.downloadtimeout.` `DownloadTimeoutMiddleware` \(\#scrapy.contrib.downloadermiddleware.downloadtimeout.DownloadTimeoutMiddleware\)
* 该中间件设置 [DOWNLOAD\_TIMEOUT](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOAD_TIMEOUT) 指定的request下载超时时间.

### HttpAuthMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.httpauth.` `HttpAuthMiddleware` \(\#scrapy.contrib.downloadermiddleware.httpauth.HttpAuthMiddleware\)
* 该中间件完成某些使用 [Basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication) \(或者叫HTTP认证\)的spider生成的请求的认证过程。
* 在spider中启用HTTP认证，请设置spider的 `http_user` 及 `http_pass` 属性。
* 样例:

```text
from scrapy.contrib.spiders import CrawlSpider

class SomeIntranetSiteSpider(CrawlSpider):

    http_user = 'someuser'
    http_pass = 'somepass'
    name = 'intranet.example.com'

    # .. rest of the spider code omitted ...
```

### HttpCacheMiddleware [¶](xia-zai-qi-zhong-jian-jian.md#module-scrapy.contrib.downloadermiddleware.httpcache)

* /class/ `scrapy.contrib.downloadermiddleware.httpcache.` `HttpCacheMiddleware`\(\#scrapy.contrib.downloadermiddleware.httpcache.HttpCacheMiddleware\)
* 该中间件为所有HTTP request及response提供了底层\(low-level\)缓存支持。 其由cache存储后端及cache策略组成。
* Scrapy提供了两种HTTP缓存存储后端:
  * [Filesystem storage backend \(默认值\)](xia-zai-qi-zhong-jian-jian.md#httpcache-storage-fs)
  * [DBM storage backend](xia-zai-qi-zhong-jian-jian.md#httpcache-storage-dbm)

您可以使用 [HTTPCACHE\_STORAGE](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_STORAGE) 设定来修改HTTP缓存存储后端。 您也可以实现您自己的存储后端。

Scrapy提供了两种了缓存策略:

* [RFC2616策略](xia-zai-qi-zhong-jian-jian.md#httpcache-policy-rfc2616)
* [Dummy策略\(默认值\)](xia-zai-qi-zhong-jian-jian.md#httpcache-policy-dummy)

您可以使用 [HTTPCACHE\_POLICY](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_POLICY) 设定来修改HTTP缓存存储后端。 您也可以实现您自己的存储策略。

#### Dummy策略\(默认值\)

该策略不考虑任何HTTP Cache-Control指令。每个request及其对应的response都被缓存。 当相同的request发生时，其不发送任何数据，直接返回response。

Dummpy策略对于测试spider十分有用。其能使spider运行更快\(不需要每次等待下载完成\)， 同时在没有网络连接时也能测试。其目的是为了能够回放spider的运行过程， /使之与之前的运行过程一模一样/ 。

使用这个策略请设置:

* [HTTPCACHE\_POLICY](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_POLICY) 为 `scrapy.contrib.httpcache.DummyPolicy`

#### RFC2616策略

该策略提供了符合RFC2616的HTTP缓存，例如符合HTTP Cache-Control， 针对生产环境并且应用在持续性运行环境所设置。该策略能避免下载未修改的数据\(来节省带宽，提高爬取速度\)。

实现了:

* 当 `no-store` cache-control指令设置时不存储response/request。
* 当 `no-cache` cache-control指定设置时不从cache中提取response，即使response为最新。
* 根据 `max-age` cache-control指令中计算保存时间\(freshness lifetime\)。
* 根据 `Expires` 指令来计算保存时间\(freshness lifetime\)。
* 根据response包头的 `Last-Modified` 指令来计算保存时间\(freshness lifetime\)\(Firefox使用的启发式算法\)。
* 根据response包头的 `Age` 计算当前年龄\(current age\)
* 根据 `Date` 计算当前年龄\(current age\)
* 根据response包头的 `Last-Modified` 验证老旧的response。
* 根据response包头的 `ETag` 验证老旧的response。
* 为接收到的response设置缺失的 `Date` 字段。 目前仍然缺失:
* `Pragma: no-cache` 支持 [http://www.mnot.net/cache\_docs/\#PRAGMA](http://www.mnot.net/cache_docs/#PRAGMA)
* `Vary` 字段支持 [http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html\#sec13.6](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.6)
* 当update或delete之后失效相应的response [http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html\#sec13.10](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.10)
* ... 以及其他可能缺失的特性 .. 使用这个策略，设置:
* [HTTPCACHE\_POLICY](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_POLICY) 为 `scrapy.contrib.httpcache.RFC2616Policy`

#### Filesystem storage backend \(默认值\)

文件系统存储后端可以用于HTTP缓存中间件。

使用该存储端，设置:

* [HTTPCACHE\_STORAGE](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_STORAGE) 为 `scrapy.contrib.httpcache.FilesystemCacheStorage` 每个request/response组存储在不同的目录中，包含下列文件:
* `request_body` - the plain request body
* `request_headers` - the request headers \(原始HTTP格式\)
* `response_body` - the plain response body
* `response_headers` - the request headers \(原始HTTP格式\)
* `meta` - 以Python `repr()` 格式\(grep-friendly格式\)存储的该缓存资源的一些元数据。
* `pickled_meta` - 与 `meta` 相同的元数据，不过使用pickle来获得更高效的反序列化性能。

目录的名称与request的指纹\(参考 `scrapy.utils.request.fingerprint` \)有关，而二级目录是为了避免在同一文件夹下有太多文件 \(这在很多文件系统中是十分低效的\)。目录的例子:

```text
/path/to/cache/dir/example.com/72/72811f648e718090f041317756c03adb0ada46c7
```

#### DBM storage backend

0.13 新版功能.

同时也有 [DBM](http://en.wikipedia.org/wiki/Dbm) 存储后端可以用于HTTP缓存中间件。

默认情况下，其采用 [anydbm](http://docs.python.org/library/anydbm.html) 模块，不过您也可以通过 [HTTPCACHE\_DBM\_MODULE](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_DBM_MODULE) 设置进行修改。

使用该存储端，设置:

* [HTTPCACHE\_STORAGE](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_STORAGE) 为 `scrapy.contrib.httpcache.DbmCacheStorage`

#### LevelDB storage backend [¶](xia-zai-qi-zhong-jian-jian.md#leveldb-storage-backend)

0.23 新版功能.

A [LevelDB](http://code.google.com/p/leveldb/) storage backend is also available for the HTTP cache middleware.

This backend is not recommended for development because only one process can access LevelDB databases at the same time, so you can’t run a crawl and open the scrapy shell in parallel for the same spider.

In order to use this storage backend:

* set [HTTPCACHE\_STORAGE](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_STORAGE) to `scrapy.contrib.httpcache.LeveldbCacheStorage`
* install [LevelDB python bindings](http://pypi.python.org/pypi/leveldb) like `pip install leveldb`

#### HTTPCache中间件设置 [¶](xia-zai-qi-zhong-jian-jian.md#httpcache)

[HttpCacheMiddleware](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.httpcache.HttpCacheMiddleware) 可以通过以下设置进行配置:

**HTTPCACHE\_ENABLED**

0.11 新版功能.

默认: `False`

HTTP缓存是否开启。

在 0.11 版更改: 在0.11版本前，是使用 [HTTPCACHE\_DIR](xia-zai-qi-zhong-jian-jian.md#std:setting-HTTPCACHE_DIR) 来开启缓存。

**HTTPCACHE\_EXPIRATION\_SECS**

默认: `0`

缓存的request的超时时间，单位秒。

超过这个时间的缓存request将会被重新下载。如果为0，则缓存的request将永远不会超时。

在 0.11 版更改: 在0.11版本前，0的意义是缓存的request永远超时。

**HTTPCACHE\_DIR**

默认: `'httpcache'`

存储\(底层的\)HTTP缓存的目录。如果为空，则HTTP缓存将会被关闭。 如果为相对目录，则相对于项目数据目录\(project data dir\)。更多内容请参考 [默认的Scrapy项目结构](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/commands.html#topics-project-structure) 。

**HTTPCACHE\_IGNORE\_HTTP\_CODES**

0.10 新版功能.

默认: `[]`

不缓存设置中的HTTP返回值\(code\)的request。

**HTTPCACHE\_IGNORE\_MISSING**

默认: `False`

如果启用，在缓存中没找到的request将会被忽略，不下载。

**HTTPCACHE\_IGNORE\_SCHEMES**

0.10 新版功能.

默认: `['file']`

不缓存这些URI标准\(scheme\)的response。

**HTTPCACHE\_STORAGE**

默认: `'scrapy.contrib.httpcache.FilesystemCacheStorage'`

实现缓存存储后端的类。

**HTTPCACHE\_DBM\_MODULE**

0.13 新版功能.

默认: `'anydbm'`

在 [DBM存储后端](xia-zai-qi-zhong-jian-jian.md#httpcache-storage-dbm) 的数据库模块。 该设定针对DBM后端。

**HTTPCACHE\_POLICY**

0.18 新版功能.

默认: `'scrapy.contrib.httpcache.DummyPolicy'`

实现缓存策略的类。

### HttpCompressionMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.httpcompression.` `HttpCompressionMiddleware` [¶](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.httpcompression.HttpCompressionMiddleware)
* 该中间件提供了对压缩\(gzip, deflate\)数据的支持。

#### HttpCompressionMiddleware Settings

**COMPRESSION\_ENABLED**

默认: `True`

Compression Middleware\(压缩中间件\)是否开启。

### ChunkedTransferMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.chunked.` `ChunkedTransferMiddleware` \(\#scrapy.contrib.downloadermiddleware.chunked.ChunkedTransferMiddleware\)
* 该中间件添加了对 [chunked transfer encoding](http://en.wikipedia.org/wiki/Chunked_transfer_encoding) 的支持。

### HttpProxyMiddleware

0.8 新版功能.

* /class/ `scrapy.contrib.downloadermiddleware.httpproxy.` `HttpProxyMiddleware` \(\#scrapy.contrib.downloadermiddleware.httpproxy.HttpProxyMiddleware\)
* 该中间件提供了对request设置HTTP代理的支持。您可以通过在 [Request](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request) 对象中设置 `proxy` 元数据来开启代理。
* 类似于Python标准库模块 [urllib](http://docs.python.org/library/urllib.html) 及 [urllib2](http://docs.python.org/library/urllib2.html) ，其使用了下列环境变量:
  * `http_proxy`
  * `https_proxy`
  * `no_proxy`

### RedirectMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.redirect.` `RedirectMiddleware` \(\#scrapy.contrib.downloadermiddleware.redirect.RedirectMiddleware\)
* 该中间件根据response的状态处理重定向的request。

通过该中间件的\(被重定向的\)request的url可以通过 [Request.meta](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request.meta) 的 `redirect_urls` 键找到。

[RedirectMiddleware](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.redirect.RedirectMiddleware) 可以通过下列设置进行配置\(更多内容请参考设置文档\):

* [REDIRECT\_ENABLED](xia-zai-qi-zhong-jian-jian.md#std:setting-REDIRECT_ENABLED)
* [REDIRECT\_MAX\_TIMES](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-REDIRECT_MAX_TIMES)

  如果 [Request.meta](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request.meta) 包含 `dont_redirect` 键，则该request将会被此中间件忽略。

#### RedirectMiddleware settings

**REDIRECT\_ENABLED**

0.13 新版功能.

默认: `True`

是否启用Redirect中间件。

**REDIRECT\_MAX\_TIMES**

默认: `20`

单个request被重定向的最大次数。

### MetaRefreshMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.redirect.` `MetaRefreshMiddleware` \(\#scrapy.contrib.downloadermiddleware.redirect.MetaRefreshMiddleware\)
* 该中间件根据meta-refresh html标签处理request重定向。

[MetaRefreshMiddleware](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.redirect.MetaRefreshMiddleware) 可以通过以下设定进行配置 \(更多内容请参考设置文档\)。

* [METAREFRESH\_ENABLED](xia-zai-qi-zhong-jian-jian.md#std:setting-METAREFRESH_ENABLED)
* `METAREFRESH_MAXDELAY`

  该中间件遵循 [RedirectMiddleware](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.redirect.RedirectMiddleware) 描述的 [REDIRECT\_MAX\_TIMES](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-REDIRECT_MAX_TIMES) 设定， [dont\_redirect](xia-zai-qi-zhong-jian-jian.md#std:reqmeta-dont_redirect) 及 [redirect\_urls](xia-zai-qi-zhong-jian-jian.md#std:reqmeta-redirect_urls) meta key。

#### MetaRefreshMiddleware settings

**METAREFRESH\_ENABLED**

0.17 新版功能.

默认: `True`

Meta Refresh中间件是否启用。

**REDIRECT\_MAX\_METAREFRESH\_DELAY**

默认: `100`

跟进重定向的最大 meta-refresh 延迟\(单位:秒\)。

### RetryMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.retry.` `RetryMiddleware` \(\#scrapy.contrib.downloadermiddleware.retry.RetryMiddleware\)
* 该中间件将重试可能由于临时的问题，例如连接超时或者HTTP 500错误导致失败的页面。

爬取进程会收集失败的页面并在最后，spider爬取完所有正常\(不失败\)的页面后重新调度。 一旦没有更多需要重试的失败页面，该中间件将会发送一个信号\(retry\_complete\)， 其他插件可以监听该信号。

[RetryMiddleware](xia-zai-qi-zhong-jian-jian.md#scrapy.contrib.downloadermiddleware.retry.RetryMiddleware) 可以通过下列设定进行配置 \(更多内容请参考设置文档\):

* [RETRY\_ENABLED](xia-zai-qi-zhong-jian-jian.md#std:setting-RETRY_ENABLED)
* [RETRY\_TIMES](xia-zai-qi-zhong-jian-jian.md#std:setting-RETRY_TIMES)
* [RETRY\_HTTP\_CODES](xia-zai-qi-zhong-jian-jian.md#std:setting-RETRY_HTTP_CODES)

  关于HTTP错误的考虑:

如果根据HTTP协议，您可能想要在设定 [RETRY\_HTTP\_CODES](xia-zai-qi-zhong-jian-jian.md#std:setting-RETRY_HTTP_CODES) 中移除400错误。 该错误被默认包括是由于这个代码经常被用来指示服务器过载\(overload\)了。而在这种情况下，我们想进行重试。

如果 [Request.meta](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/request-response.html#scrapy.http.Request.meta) 包含 `dont_retry` 键， 该request将会被本中间件忽略。

#### RetryMiddleware Settings

**RETRY\_ENABLED**

0.13 新版功能.

默认: `True`

Retry Middleware是否启用。

**RETRY\_TIMES**

默认: `2`

包括第一次下载，最多的重试次数

**RETRY\_HTTP\_CODES**

默认: `[500, 502, 503, 504, 400, 408]`

重试的response 返回值\(code\)。其他错误\(DNS查找问题、连接失败及其他\)则一定会进行重试。

### RobotsTxtMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.robotstxt.` `RobotsTxtMiddleware` \(\#scrapy.contrib.downloadermiddleware.robotstxt.RobotsTxtMiddleware\)
* 该中间件过滤所有robots.txt eclusion standard中禁止的request。
* 确认该中间件及 [ROBOTSTXT\_OBEY](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-ROBOTSTXT_OBEY) 设置被启用以确保Scrapy尊重robots.txt。
* 警告
* 记住, 如果您在一个网站中使用了多个并发请求， Scrapy仍然可能下载一些被禁止的页面。这是由于这些页面是在robots.txt被下载前被请求的。 这是当前robots.txt中间件已知的限制，并将在未来进行修复。

### DownloaderStats

* /class/ `scrapy.contrib.downloadermiddleware.stats.` `DownloaderStats` \(\#scrapy.contrib.downloadermiddleware.stats.DownloaderStats\)
* 保存所有通过的request、response及exception的中间件。
* 您必须启用 [DOWNLOADER\_STATS](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/settings.html#std:setting-DOWNLOADER_STATS) 来启用该中间件。

### UserAgentMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.useragent.` `UserAgentMiddleware` \(\#scrapy.contrib.downloadermiddleware.useragent.UserAgentMiddleware\)
* 用于覆盖spider的默认user agent的中间件。
* 要使得spider能覆盖默认的user agent，其 `user_agent` 属性必须被设置。

### AjaxCrawlMiddleware

* /class/ `scrapy.contrib.downloadermiddleware.ajaxcrawl.` `AjaxCrawlMiddleware` \(\#scrapy.contrib.downloadermiddleware.ajaxcrawl.AjaxCrawlMiddleware\)
* 根据meta-fragment html标签查找 ‘AJAX可爬取’ 页面的中间件。查看 [https://developers.google.com/webmasters/ajax-crawling/docs/getting-started](https://developers.google.com/webmasters/ajax-crawling/docs/getting-started) 来获得更多内容。
* 注解
* 即使没有启用该中间件，Scrapy仍能查找类似于 `'http://example.com/!#foo=bar'` 这样的’AJAX可爬取’页面。 AjaxCrawlMiddleware是针对不具有 `'!#'` 的URL，通常发生在’index’或者’main’页面中。

#### AjaxCrawlMiddleware设置

**AJAXCRAWL\_ENABLED**

0.21 新版功能.

默认: `False`

AjaxCrawlMiddleware是否启用。您可能需要针对 [通用爬虫](https://github.com/yourwilliam/whyclass_python/tree/d24463376b112278a67bcdc9fde23c4ca399a069/scrapy/broad-crawls.html#topics-broad-crawls) 启用该中间件。

