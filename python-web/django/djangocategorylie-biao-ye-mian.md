# Django category列表页面

前面讲述过在列表页面展示category，这一节主要讲解如何点击category跳转到相应的category下的文章列表

主要过程分为：

1. 添加category过滤的view
2. 修改url
3. 在页面Template中添加url

修改 views.py

```py
def category(request, category_id):
    articles = Article.objects.filter(categories__id=category_id).filter(deletedAt=None).filter(status=2).order_by(
        '-updatedAt')
    categories = Category.objects.filter(deletedAt=None)
    tags = Tag.objects.all()
    context = {
        'articles': articles,
        'categories': categories,
        'tags': tags,
    }
    return render(request, 'blog/blog_image_rs.html', context)
```

修改urls.py

```py
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:article_id>/', views.blog_single, name='detail'),
    path('<slug:slug>/', views.blog_slug_single, name='detail_slug'),
    path('category/<int:category_id>/', views.category, name='category'),
]
```

修改blog_image_rs.html文件

```html
<aside class="widget widget_categories">
    <h4 class="widget-title">Search Categories</h4>
    <ul>
        {% for category in categories %}
        <li><a href="/blog/category/{{category.id}}"><i class="fa fa-chevron-right"></i>{{category.title}}</a></li>
        {% endfor %}
    </ul>
</aside>
```



最后修改完成页面之后，发现category列表下面的blog点击之后不能访问，其访问的url是http://127.0.0.1:8000/blog/category/1/4。 这里明显无法解析，我们需要修改article的地址为绝对地址，修改如下

```html
<div class="ed_blog_item ed_bottompadder50">
    {% if article.header_image%}
    <div class="ed_blog_image">
        <a href="/blog/{{article.id}}"><img src="{{article.header_image.url}}"
                                        alt="blog image"/></a>
    </div>
    {% endif %}
    <div class="ed_blog_info">
        <h2><a href="/blog/{{article.id}}">{{article.title}}</a></h2>
        <ul>
            <li><a href="#"><i class="fa fa-user"></i> james marco</a></li>
            <li><a href="#"><i class="fa fa-clock-o"></i> {{article.updatedAt}}</a></li>
            <li><a href="#"><i class="fa fa-comment-o"></i> 4 comments</a></li>
        </ul>
        <p class="ed_bottompadder10">{{article.description|default:''}}</p>
        <a href="/blog/{{article.id}}" class="btn ed_btn ed_orange">read more</a>
    </div>
</div>
```