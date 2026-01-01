# Xpath爬虫写法优化

* 默认的写法：&#x20;
  * 直接从浏览器复制xpath
  * title: `//*[@id="set-container-1"]/h2`   content: `//*[@id="set-container-1"]/div[3]`
  * 问题：
    1. 这样写只能搜索一个内容，不能批量把多篇文章拷下来
* 批量优化写法一：
  * 往上层找到批量查询的id再往底层找
  * title：`//*[@id="slpit-two"]/div[1]/div/h2/text()`  content:`//*[@id="slpit-two"]/div[1]/div/div[3]`
  * 问题：
    1. 这样写读起来教简单，并且可以搜索出多个列表
    2. 由于通过div的层级关系来进行搜索，在搜索多篇文章或者不同的页面的时候，可能会存在中间层级混乱之后导致查询内容失败的问题，导致无法获取内容。
* 批量优化写法二：
  * 往上层找到批量查询的id，然后再往下层逐步去查询不变的class找到我们想要的内容
  * title:`//*[@id="slpit-two"]//h2[@class="subtitle"]`      content: `//*[@id="slpit-two"]//div[@class="passage-content"]`
  * 问题：
    1. 这样写可以直接找到下面的class属性，一般各个网站会使用class作为样式的定义，一般按照class的样式来搜索会更加精准
    2. 使用`//` 双下划线来进行下面的所有判断，对层级的依赖更小，防止网站的变化
