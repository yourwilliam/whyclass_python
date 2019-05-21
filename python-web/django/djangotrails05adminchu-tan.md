# Django Trails 05 

## admin控制面板的配置

之前配置的admin控制面板 

```py
from django.contrib import admin

# Register your models here.
from .models import Article

admin.site.register(Article)

```

## list_display

在控制面板发现几个问题，list页面的时候看不到文章具体内容，不好寻找。

list_display 用于控制列表页面显示出来的具体属性，方便用户配置和修改。

```py
from django.contrib import admin

# Register your models here.
from .models import Article

class AritcleAdmin(admin.ModelAdmin):
    fields = ['title', 'description', 'content', 'banner']
    list_display = ('title', 'description', 'content', 'banner', 'publish_time', 'last_modify_time')

admin.site.register(Article, AritcleAdmin)

```

把不需要的字段删除掉试试看。


### list_filter 

list_filter 用于在右侧添加过滤栏目，方便快速过滤和寻找

```py
list_filter = ['publish_time']
```

### search_fields

search_fields 用于搜索关键信息

```py
    search_fields = ['title', 'description']

```

