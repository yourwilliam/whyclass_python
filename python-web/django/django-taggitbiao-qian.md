# django-taggit标签

## 安装 django-taggit

```bash
pip install django-taggit -i https://mirrors.aliyun.com/pypi/simple
```

## 添加模型

在 `setting.py` 中添加引入taggit app

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
    'taggit',
]
```

在`models.py`中添加tag字段

```python
class Article(BaseSchema):
    title = models.CharField(max_length=1023, null=True, blank=True, default='')
    description = models.CharField(max_length=2047, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    slug = models.SlugField("slug", max_length=255,
                            help_text="Used to build the article's URL.")
    banner = models.URLField(null=True, blank=True)
    header_image_height = models.PositiveIntegerField(default=75)
    header_image_width = models.PositiveIntegerField(default=75)
    header_image = models.ImageField(upload_to='photos/%Y/%m', height_field='header_image_height',
                                     width_field='header_image_width',
                                     null=True, blank=True)
    categories = models.ManyToManyField(
        Category, blank=True, related_name="entries", verbose_name="categories")
    tags = TaggableManager()

    def __unicode__(self):
        return self.title

    def __str__(self):
        return self.title
```

添加完成之后重新发布模型

```bash
python manage.py makemigrations
python manage.py migrate
```

## 在admin中添加模型

```python
class ArticleAdmin(admin.ModelAdmin):
    # fields = ["title", "description", "banner","content","header_image","categories"]
    fieldsets = [
        ('basic content', {"fields": ["title", "slug", "description", "content", "tag"]}),
        ('图片', {"fields": ["banner", "header_image"]}),
        ('category', {"fields": ["categories"]})
    ]
    list_display = ["title", "description", "updatedAt"]
    list_filter = ['updatedAt']
    search_fields = ['title', 'description']
    filter_horizontal = ('categories',)

    def get_queryset(self, request):
        qs = super(ArticleAdmin, self).get_queryset(request)
        qs = qs.filter(deletedAt=None)
        return qs
```

## 在前台显示tags

