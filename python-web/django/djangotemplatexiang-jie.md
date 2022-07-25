# DjangoTemplate详解

在修改Model之后先把之前的页面模板更新

```markup
{% raw %}
{% for article in articles %}
<div class="ed_blog_item ed_bottompadder50">
    <div class="ed_blog_image">
        <a href="./{{article.id}}"><img src="{{article.header_image.url}}" alt="blog image"/></a>
    </div>
    <div class="ed_blog_info">
        <h2><a href="./{{article.id}}">{{article.title}}</a></h2>
        <ul>
            <li><a href="#"><i class="fa fa-user"></i> james marco</a></li>
            <li><a href="#"><i class="fa fa-clock-o"></i> {{article.updatedAt}}</a></li>
            <li><a href="#"><i class="fa fa-comment-o"></i> 4 comments</a></li>
        </ul>
        <p class="ed_bottompadder10">{{article.description}}</p>
        <a href="./{{article.id}}" class="btn ed_btn ed_orange">read more</a>
    </div>
</div>
{% endfor %}
{% endraw %}
```

由于修改了更新时间和头部图片，所以我们修改头部图片。使用`.url`可以获取到图像的全部链接地址。

singlt.html也同样的修改。

## category部分升级

view.py

```python
def index(request):
    articles = Article.objects.order_by('-updatedAt')
    categories = Category.objects.all()
    context = {
        'articles': articles,
        'categories': categories,
    }
    return render(request, 'blog/blog_image_rs.html', context)
```

修改view.py，添加category到返回模板中去。

在修改模板内容

```python
<aside class="widget widget_categories">
    <h4 class="widget-title">Search Categories</h4>
    <ul>
        {% raw %}
{% for category in categories %}
            <li><a href="#"><i class="fa fa-chevron-right"></i>{{category.title}}</a></li>
        {% endfor %}
{% endraw %}
    </ul>
</aside>
```

## Template if,else 判断

在Template模板中，可以包含判断块，其中和python语言类似，包含 if, elif 和 else

```python
{% raw %}
{% if athlete_list %}
    Number of athletes: {{ athlete_list|length }}
{% elif athlete_in_locker_room_list %}
    Athletes should be out of the locker room soon!
{% else %}
    No athletes.
{% endif %}
{% endraw %}
```

在我们的例子中，由于Model设计的时候，header\_image可以为空，可以测试下，在admin中如果将header\_image设置为空的话，会发生什么事情？

这时候可以使用 if else来判断

blog\_image\_rs.html

```markup
<div class="ed_blog_all_item">
{% raw %}
{% for article in articles %}
<div class="ed_blog_item ed_bottompadder50">
    {% if article.header_image%}
    <div class="ed_blog_image">
        <a href="./{{article.id}}"><img src="{{article.header_image.url}}"
                                        alt="blog image"/></a>
    </div>
    {% endif %}
{% endraw %}
    <div class="ed_blog_info">
```

这样可以在没有图片的时候，不显示图片的内容。仔细想想为什么要把if,else块写在外面。

同时可以把另外一个修改了 blog\_single\_rs.html

```markup
<div class="ed_blog_item ed_bottompadder50">
    {% raw %}
{% if article.header %}
    <div class="ed_blog_image_rs">
        <img src="{{article.header_image.url}}" alt="blog image" />
    </div>
    {% endif %}
{% endraw %}
<div class="ed_blog_info">
```

思考和研究： 如果在if中有and 和 or怎么写？

## Template filter 过滤器

举个例子： 如果在admin中，将article的description中的数据清除，保存，在查看image\_rs页面。

在某些值为None的情况下，由于Model中设置可以为none，那么就需要在前端页面给默认值。

```markup
<p class="ed_bottompadder10">{{article.description|default:''}}</p>
```

使用如上的过滤器就可以设置为空时候的默认值

django支持其他种类的过滤器

### default

如果变量为FALSE或者为空，就会使用default后面的值。否则变量会使用自己的值

```python
{{ value|default:"nothing" }}
```

### length

针对String和list类型，会返回值的长度

```python
{{ value|length }}
```

filesizeformat

将文件的大小格式化为更加可读的形式，比如(i.e. '13 KB', '4.1 MB', '102 bytes', etc.)

```python
{{ value|filesizeformat }}
```

## template safe (HTML安全退出模式)

当前我们在content存的是文章内容，那么如果我们需要对文章的内容做一些特别的分段、粗体、超链接、斜体等该如何处理呢？

我们可以在content中直接存入HTML来解决上面的问题，可以测试一下在content中直接存入HTML会发生什么情况。

![-w856](http://ossp.pengjunjie.com/mweb/15590276717134.jpg)

![-w568](http://ossp.pengjunjie.com/mweb/15590276825057.jpg)

所以页面也直接显示了带标签的内容，那么我们如何使页面上可以直接显示HTML解析后的内容呢。

使用safe标签可以解决以上问题。

```markup
<p>{{article.content|safe}}</p>
```

如果不希望使用这种包裹方式，可以直接使用div
