# DjangoURL详解

对于高质量的Web 应用来说，使用简洁、优雅的URL 模式是一个非常值得重视的细节。

## Django 如何处理一个请求

当一个用户请求Django 站点的一个页面，下面是Django 系统决定执行哪个Python 代码使用的算法：

1. Django 在 settings.py里面有 `ROOT_URLCONF = 'youyu.urls'`用于配置网站的整体根路由。
2. Django读取python模块并寻找urlpatterns变量，urlpatterns变量由`django.urls.path() and/or django.urls.re_path()`组成
3. Django 依次匹配每个URL 模式，在与请求的URL 匹配的第一个模式停下来。
4. 当url匹配到相应的模式，django将调用相应的view。View是一个简单的python函数。视图传递一下的参数：
   1. 一个HttpRequest实例
   2. 正则表达式参数
   3. url 中的相应匹配参数，可以写入到view的参数列表中。
5. 如果没有任何一个url匹配，django会返回一个异常。

## Path converters

django提供一下类型的path转换符

str - 匹配任意的非空字符串。不包含'/'字符。 int - 匹配0个或者任意个整数，返回int类型 slug - 匹配任意的ASCII 字符和数字。中间空格添加 - 或者 \_ uuid - 匹配UUID格式。 path - 匹配一个非空字符串，包括'/'分隔符。

## slug更新

slug用于更友好的显示blog、单页或者文章后面的url连接。

### 第一步更新slug

将Article模型添加slug字段，然后在url中维护slug解析，最后添加slug\_view

models.py

```python
class Article(BaseSchema):
    STATUS_CHOICES = ((0, 'draft'), (1, 'hidden'), (2, 'publish'))
    title = models.CharField(max_length=100, null=True, blank=True, default='')
    description = models.CharField(max_length=500, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    slug = models.SlugField("slug", unique=True, max_length=255,
                            help_text="Used to build the article's URL.")
    header_image_url = models.URLField("head image url", max_length=511, null=True, blank=True)
    header_image_height = models.PositiveIntegerField(default=75, null=True, blank=True)
    header_image_width = models.PositiveIntegerField(default=75, null=True, blank=True)
    header_image = models.ImageField(upload_to='photos/%Y/%m', height_field='header_image_height',
                                     width_field='header_image_width',
                                     null=True, blank=True)
    status = models.IntegerField(
        "status", db_index=True, choices=STATUS_CHOICES, default=2)
    categories = models.ManyToManyField(
        Category, blank=True, related_name="entries", verbose_name="categories")

    def __unicode__(self):
        return self.title

    def __str__(self):
        return self.title
```

在Article中添加slug字段

urls.py

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:article_id>/', views.blog_single, name='detail'),
    path('<slug:slug>/', views.blog_slug_single, name='detail_slug')
]
```

views.py

```python
def blog_slug_single(request, slug):
    article = get_object_or_404(Article, slug=slug)
    context = {'article': article, }
    return render(request, 'blog/blog_single_rs.html', context)
```

最后记得在admin.py中添加slug维护字段。

在页面使用slug访问遍可以访问到文章。这种模式已经可用了。但是这种模式需要我们手动的指定slug，对于维护文章的时候较复杂。

使用django-uuslug包可以自动的管理slug

#### django-uuslug

第一步安装django-uuslug ， 使用`pip install django-uuslug`

然后在模型中修改默认的保存方法即可

```python
    def save(self, *args, **kwargs):
        self.slug = slugify(self.title)
        super(Article, self).save(*args, **kwargs)
```

将默认的slug替换即可。最后为了方便使用，可以将admin中的slug去除，由系统帮忙生成。

最后我们改掉页面上的连接到slug即可。

