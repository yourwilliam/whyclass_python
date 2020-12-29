# django-tagging

## django 标签

### 安装

安装django-tagging

```text
sudo pip install django-tagging
```

### 添加tagging到环境

* 在setting的INSTALLED\_APPS中添加'tagging'APP

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
    'tagging',
]
```

* 运行 manage.py makemigration
* 运行 manage.py migrate
* 运行工程

### 创建tags

在模型层创建tans，然后

```python
from tagging.fields import TagField

tags = TagField()
```

我们在admin中添加tags

```python
fieldsets = [
        ('basic content', {'fields': ['title', 'description', 'tags', 'content', 'status']}),
        ('banner', {'fields': ['header_image_url', 'header_image']}),
        ('category', {'fields': ['categories', ]}),
    ]
```

## 页面添加tag

### 博客详情页添加tags

在blog详情页我们看到了tags的内容，所以我们可以把此处进行修改

修改blog\_single\_rs.html页面

```python
<ul>
    <li><i class="fa fa-tags"></i> <a href="#">tags: </a></li>
    <li><a href="#">{{article.tags}}</a></li>
</ul>
```

### 列表页面的tags过滤

在列表页添加tags标签，需要两个步骤。首先在view中查询出所有的tags标签，封装到context中。然后再在Template页面中显示相应的内容。

在列表页首先需要显示所有的tags

```python
def index(request):
    articles = Article.objects.order_by('-updatedAt')
    # articles = Article.objects.filter(deletedAt=None).filter(status=2).order_by('-updatedAt')
    categories = Category.objects.filter(deletedAt=None)
    tags = Tag.objects.all()
    context = {
        'articles': articles,
        'categories': categories,
        'tags': tags,
    }
    return render(request, 'blog/blog_image_rs.html', context)
```

在Template中添加所有的tags

```markup
<aside class="widget widget_tag_cloud">
    <h4 class="widget-title">Search by Tags</h4>
    {% for tag in tags%}
        <a href="#" class="ed_btn ed_orange">{{tag.name}}</a>
    {% endfor %}
</aside>
```

### 为tags添加导航

需求：点击tags的按钮的时候，需要展示该Tags下面的所有文章。

1. 建立根据tag来索引文章的view。
2. 为根据tag索引文章的view添加urlpattern。
3. 在列表页添加相应的tag导航。

修改views.py

```python
from tagging.models import Tag


def tag_category(request, tag_name):
    articles = Article.objects.filter(tags=tag_name).filter(deletedAt=None).filter(status=2).order_by(
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

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:article_id>/', views.blog_single, name='detail'),
    path('<slug:slug>/', views.blog_slug_single, name='detail_slug'),
    path('tag/<str:tag_name>/', views.tag_category, name='tag_category')
    path('category/<int:category_id>/', views.category, name='category'),
]
```

修改blog\_image\_rs:

```markup
<aside class="widget widget_tag_cloud">
    <h4 class="widget-title">Search by Tags</h4>
    {% for tag in tags%}
        <a href="/blog/tag/{{tag.name}}" class="ed_btn ed_orange">{{tag.name}}</a>
    {% endfor %}
</aside>
```

详情请参考[django参考文档](http://django-tagging.readthedocs.io/)

