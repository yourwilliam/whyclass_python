# Django Template详解

在修改Model之后先把之前的页面模板更新

```html
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
```

由于修改了更新时间和头部图片，所以我们修改头部图片。使用`.url`可以获取到图像的全部链接地址。

singlt.html也同样的修改。

## category部分升级

view.py
```py
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

```py
<aside class="widget widget_categories">
    <h4 class="widget-title">Search Categories</h4>
    <ul>
        {% for category in categories %}
            <li><a href="#"><i class="fa fa-chevron-right"></i>{{category.title}}</a></li>
        {% endfor %}
    </ul>
</aside>
```

