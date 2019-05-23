# Django admin详解

当前在和model一起修改admin 样式如下

```py

from django.contrib import admin

# Register your models here.
from .models import Article, Category


class CategoryAdmin(admin.ModelAdmin):
    fields = ('title', 'slug', 'description')
    list_display = ('title', 'slug')


class ArticleAdmin(admin.ModelAdmin):
    fields = ['title', 'description', 'content', 'status', 'header_image_url', 'header_image', 'categories']
    list_display = ('title', 'description', 'content', 'status', 'createdAt', 'updatedAt')
    list_filter = ['createdAt', 'updatedAt']
    search_fields = ['title', 'description']


admin.site.register(Article, ArticleAdmin)
admin.site.register(Category, CategoryAdmin)

```

通过 admin.site.register(Article, ArticleAdmin) 注册 Article 模型，Django 能够构建一个默认的表单用于展示。通常来说，你期望能自定义表单的外观和工作方式。你可以在注册模型时将这些设置告诉 Django。

默认配置样式如下

![](http://ossp.pengjunjie.com/mweb/15585937788289.jpg)

下面我们来一步一步优化样式

##优化将field分为不同的区间来修改

对于拥有数十个字段的表单来说，为表单选择一个直观的排序方法就显得你的针很细了。

说到拥有数十个字段的表单，你可能更期望将表单分为几个字段集：

```py
from django.contrib import admin

# Register your models here.
from .models import Article, Category


class CategoryAdmin(admin.ModelAdmin):
    fields = ('title', 'slug', 'description')
    list_display = ('title', 'slug')


class ArticleAdmin(admin.ModelAdmin):
    fieldsets = [
        ('basic content', {'fields': ['title', 'description', 'content', 'status']}),
        ('banner', {'fields': ['header_image_url', 'header_image']}),
        ('category', {'fields': ['categories',]}),
    ]
    list_display = ('title', 'description', 'content', 'status', 'createdAt', 'updatedAt')
    list_filter = ['createdAt', 'updatedAt']
    search_fields = ['title', 'description']

admin.site.register(Article, ArticleAdmin)
admin.site.register(Category, CategoryAdmin)

```

可以使用fieldsets将相同的部分分组整理起来，在输入的时候会更清楚

如图展示如下

![](http://ossp.pengjunjie.com/mweb/15585938894166.jpg)

## 多对多关系优化

这种模式的多对多关系看起来比较简单， 有时候比较难看清楚具体的选择情况，可以提供更方便的管理方式。

```
from django.contrib import admin

# Register your models here.
from .models import Article, Category


class CategoryAdmin(admin.ModelAdmin):
    fields = ('title', 'slug', 'description')
    list_display = ('title', 'slug')


class ArticleAdmin(admin.ModelAdmin):
    fieldsets = [
        ('basic content', {'fields': ['title', 'description', 'content', 'status']}),
        ('banner', {'fields': ['header_image_url', 'header_image']}),
        ('category', {'fields': ['categories',]}),
    ]
    list_display = ('title', 'description', 'content', 'status', 'createdAt', 'updatedAt')
    list_filter = ['createdAt', 'updatedAt']
    search_fields = ['title', 'description']
    filter_horizontal = ('categories',)


admin.site.register(Article, ArticleAdmin)
admin.site.register(Category, CategoryAdmin)

```

添加filter_horizontal可以优化具体的表现形式。

![](http://ossp.pengjunjie.com/mweb/15585940198573.jpg)


这种方式的显示会直观很多。


## list_display

list_display用来展示列表页面内容

![](http://ossp.pengjunjie.com/mweb/15585944599164.jpg)

同时list_display可以包含Model的相关方法来获取更加丰富的展示。详情可以参考django文档


## list_filter

list_filter负责配置右侧的过滤组件。
```py
    list_filter = ['categories','createdAt', 'updatedAt']
```

显示结果

![](http://ossp.pengjunjie.com/mweb/15585946510712.jpg)


## search_filter 

在列表的顶部增加一个搜索框。当输入待搜项时，Django 将搜索 question_text 字段。你可以使用任意多的字段——由于后台使用 LIKE 来查询数据，将待搜索的字段数限制为一个不会出问题大小，会便于数据库进行查询操作。

现在是给你的修改列表页增加分页功能的好时机。默认每页显示 100 项。变更页分页, 搜索框, 过滤器, 日期层次结构, 和 列标题排序 均以你期望的方式合作运行。

```py
    search_fields = ['title', 'description']
```

