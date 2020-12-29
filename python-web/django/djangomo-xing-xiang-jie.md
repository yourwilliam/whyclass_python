# Django模型详解

## django 模型

模型准确且唯一的描述了数据。它包含您储存的数据的重要字段和行为。一般来说，每一个模型都映射一张数据库表。

基础：

每个模型都是一个 Python 的类，这些类继承 django.db.models.Model 模型类的每个属性都相当于一个数据库的字段。 利用这些，Django 提供了一个自动生成访问数据库的 API；请参阅 进行查询。

`django model <--> scrapy item <--> java dao dto`

## django 模型基本讲解

### django模型默认属性

#### 1. null

如果设置为 True，当该字段为空时，Django 会将数据库中该字段设置为 NULL。默认为 False 。

#### 2. blank

如果设置为 True，该字段允许为空。默认为 False。

注意该选项与 False 不同， null 选项仅仅是数据库层面的设置，然而 blank 是涉及表单验证方面。如果一个字段设置为 blank=True ，在进行表单验证时，接收的数据该字段值允许为空，而设置为 blank=False 时，不允许为空。

#### 3. choices

使用tuple的list来组成，将作为一个选择器来配置。每个二元组的第一个值会储存在数据库中，而第二个值将只会用于在表单中显示。

对于一个模型实例，要获取该字段二元组中相对应的第二个值，使用 get\_FOO\_display\(\) 方法

```python
YEAR_IN_SCHOOL_CHOICES = [
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
    ('GR', 'Graduate'),
]
```

#### 4. default

该字段的默认值。可以是一个值或者是个可调用的对象，如果是个可调用对象，每次实例化模型时都会调用该对象。

#### 5. help\_text

额外的“帮助”文本，随表单控件一同显示。即便你的字段未用于表单，它对于生成文档也是很有用的。

#### 6. primary\_key

如果设置为 True ，将该字段设置为该模型的主键。

#### 7.unique

如果设置为 True，这个字段的值必须在整个表中保持唯一。

## 模型的继承

django Model的集成和python中的继承完全相同。父类用于定义相同的方法和属性，供子类继承使用。

你只需要决定父类模型是否需要拥有它们的权利（拥有它们的数据表），或者父类仅作为承载仅子类中可见的公共信息的载体。

Django 有三种可用的集成风格。

1. 常见情况下，你仅将父类用于子类公共信息的载体，因为你不会想在每个子类中把这些代码都敲一遍。这样的父类永远都不会单独使用，所以 抽象基类 是你需要的。
2. 若你继承了一个模型（可能来源其它应用），且想要每个模型都有对应的数据表，客官这边请 多表继承。
3. 最后，若你只想修改模型的 Python 级行为，而不是以任何形式修改模型字段， 代理模型 会是你的菜。

### 下面以一个抽象基类为例

代码添加到models中

```python
class BaseSchema(models.Model):
    createdAt = models.DateTimeField("createdAt", auto_now_add=True)
    updatedAt = models.DateTimeField("updatedAt", auto_now=True)
    deletedAt = models.DateTimeField("deletedAt", null=True, default=None)

    class Meta:
        abstract = True

    def delete(self, using=None, keep_parents=False):
        self.deletedAt = timezone.now()
        self.save()
```

这个例子中涉及了两个重要的知识点： Meta设置抽象基类和覆盖模型的`delete()`方法

#### 重写模型默认定义方法

还有一个 模型方法 的集合，包含了一些你可能自定义的数据库行为。尤其是这两个你最有可能定制的方法 save\(\) 和 delete\(\)。

你可以随意地重写这些方法（或其它模型方法）来更改方法的行为。

#### 抽象基类

抽象基类在你要将公共信息放入很多模型时会很有用。编写你的基类，并在 Meta 类中填入 abstract=True。该模型将不会创建任何数据表。当其用作其它模型类的基类时，它的字段会自动添加至子类。

其中BaseSchema定义了一个抽象基类，这个是不需要去实现的类。BaseSchema实现了每个对象的从创建、修改到删除的声明周期管理的抽象基类，所有需要管理对象生命周期的类都可以继承于这个抽象积累获取相应的能力。

同时设置delete方法，针对对象的软删除`.delete`方法覆盖基类`models.Model`的删除方法。所以对象在删除的时候不会直接从数据库中删除对象，而是通过设置deleteAt字段判断对象的删除标识。可以看到在Delete方法的最后使用的是`save()`，而不是del\(\)

最后修改我们需要使用的对象继承抽象基类即可。

```python
class Article(BaseSchema):
    title = models.CharField(max_length=100, null=True, blank=True, default='')
    description = models.CharField(max_length=500, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    banner = models.URLField()
```

article 中可以删除掉之前配置的时间相关的字段。同时在admin.py中也修改一下相关的字段。

Django 在安装 Meta 属性前，对抽象基类的 Meta 做了一个调整——设置 abstract=False。这意味着抽象基类的子类不会自动地变成抽象类。当然，你可以继承一个抽象基类创建另一个抽象基类。你只需记住显示地设置 abstract=True。

有时候变更模型之后，新的模型跟老的数据库字段会有一定的冲突。因为一些新增的字段有一些非空约束等，需要对老的数据中添加这些字段的默认值。如果老的数据不重要的话，最简单的解决方法是：

1. 删除掉migrations里面除**init**.py的所有文件
2. 删除掉sqllite数据库文件\(其他数据库直接删库也可以\)

## 模型字段

### 枚举选择类型

所有文章需要文章状态，使用元组来创建不同的文章状态。数据库中设置整形的状态类型，页面上可以查看相应的显示类型。具体生成后可以查看admin获取

```python
#修改model.py文件
class Article(BaseSchema):
    STATUS_CHOICES = ((0, 'draft'), (1, 'hidden'), (2, 'publish'))
    title = models.CharField(max_length=100, null=True, blank=True, default='')
    description = models.CharField(max_length=500, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    banner = models.URLField()
    status = models.IntegerField(
        "status", db_index=True, choices=STATUS_CHOICES, default=2)
```

修改admin.py文件将status添加到fields中去。

```python
#修改admin.py文件
class AritcleAdmin(admin.ModelAdmin):
    fields = ['title', 'description', 'content', 'banner', 'status']
    list_display = ('title', 'description', 'content', 'banner', 'status', 'createdAt', 'updatedAt')
    list_filter = ['createdAt', 'updatedAt']
    search_fields = ['title', 'description']
```

添加完成后执行 `python manage.py makemigrations` 和 `python manage.py migrate`

## Image 和 Url类型

### Image 管理

Image目录用于做对象模型中图片的上传和下载管理。Django 提供ImageField来管理模型中的图像字段。在admin中提供Image的上传和显示功能。

Image 字段定义如下

```python
class ImageField(upload_to=None, height_field=None, width_field=None, max_length=100, **options)
```

ImageFiled 继承于 FileField\(后面我们会详细讲解FileField\)。

**upload\_to**

upload\_to 字段记录Image类型存储的位置。 可以使用`upload_to='photos/%Y/%m'`这种模式来将media存储到一个记录时间的文件夹中，方便后续管理。

**height\_field**

height\_field 可以将图像的长度字段存储到相应的字段中。系统会帮助自动的进行存储。

**width\_field**

height\_field 可以将图像的宽度字段存储到相应的字段中。系统会帮助自动的进行存储。

其中的这两个字段可以定义到其他的字段中去。 这么做的好处是方便后续做相应的读取使用。

> 使用Image字段的时候，需要安装Pillow包，使用pip install Pillow

#### 相应代码

```python
class Article(BaseSchema):
    STATUS_CHOICES = ((0, 'draft'), (1, 'hidden'), (2, 'publish'))
    title = models.CharField(max_length=100, null=True, blank=True, default='')
    description = models.CharField(max_length=500, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    header_image_url = models.URLField("head image url", max_length=511, null=True, blank=True)
    header_image_height = models.PositiveIntegerField(default=75)
    header_image_width = models.PositiveIntegerField(default=75)
    header_image = models.ImageField(upload_to='photos/%Y/%m', height_field='header_image_height',
                                     width_field='header_image_width',
                                     null=True, blank=True)
    status = models.IntegerField(
        "status", db_index=True, choices=STATUS_CHOICES, default=2)
```

添加相应的字段之后，需要配置好media路径，否则写入和查看的时候不能使用。django提供media来配置所有的图片和文件上传路径。在settings.py中可以配置上传路径，在urls.py中可以配置查看路径。

```python
#在settings.py文件中添加这两行
MEDIA_ROOT = BASE_DIR + '/blog/media'
MEDIA_URL = '/media/'
```

```python
#在urls.py文件中可以添加相应的静态文件访问路径
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

最后将相关的字段添加到admin.py的管理模块中去。

```python
#admin.py管理文件
from django.contrib import admin

# Register your models here.
from .models import Article

class AritcleAdmin(admin.ModelAdmin):
    fields = ['title', 'description', 'content', 'status','header_image_url', 'header_image']
    list_display = ('title', 'description', 'content', 'status', 'createdAt', 'updatedAt')
    list_filter = ['createdAt', 'updatedAt']
    search_fields = ['title', 'description']

admin.site.register(Article, AritcleAdmin)
```

启动服务器后就可以看到Image配置成功了。可以看到相应的图片提交目录和图片访问目录如下。

![](http://ossp.pengjunjie.com/mweb/15585903495580.jpg)

## 关联关系

显然，关系型数据库的强大之处在于各表之间的关联关系。 Django 提供了定义三种最常见的数据库关联关系的方法：一对多，多对多，一对一。

### manytomany 多对多关系

我们让blog页面的category和blog article拥有多对多关系。即一个article可以属于多个category，一个category可以拥有多个不同的article。

多对多关系的定义。

我们先定义category模型

```python
class Category(BaseSchema):
    title = models.CharField("title", max_length=255)
    slug = models.SlugField("slug", unique=True, max_length=255,
                            help_text="Used to build the catagory's URL.")
    description = models.TextField("description", blank=True)

    def __unicode__(self):
        return self.title
```

添加了一个**unicode**\(self\)方法，unicode\(\)方法是在一个对象上调用unicode\(\)时被调用的。因为Django的数据库后端会返回Unicode字符串给model属性，所以我们通常会给自己的model写一个unicode\(\)方法。

slug是用于后续我们如果不使用id进行页面索引，我们就可以使用slut来进行文章和目录的索引。

下面在article添加外键字段

```python
class Article(BaseSchema):
    STATUS_CHOICES = ((0, 'draft'), (1, 'hidden'), (2, 'publish'))
    title = models.CharField(max_length=100, null=True, blank=True, default='')
    description = models.CharField(max_length=500, null=True, blank=True, default='')
    content = models.TextField(null=True, blank=True, default='')
    header_image_url = models.URLField("head image url", max_length=511, null=True, blank=True)
    header_image_height = models.PositiveIntegerField(default=75)
    header_image_width = models.PositiveIntegerField(default=75)
    header_image = models.ImageField(upload_to='photos/%Y/%m', height_field='header_image_height',
                                     width_field='header_image_width',
                                     null=True, blank=True)
    status = models.IntegerField(
        "status", db_index=True, choices=STATUS_CHOICES, default=2)
    categories = models.ManyToManyField(
        Category, blank=True, related_name="entries", verbose_name="categories")

    def __unicode__(self):
        return self.title
```

可以看到我们添加了`models.ManyToManyField`字段。

添加到这里外键关系遍添加完成了。然后我们执行`python manage.py makemigrations` 和`python manage.py migrate`即可发布完成。

**配置admin.py 来管理配置**

最简单的配置如下，可以直接在ArticleAdmin中加入categories即可。

```python
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

但是这种方式展示及使用起来极为不方便，我们可以针对此进行修改。

在category和article的模型中添加str方法可以解决这个问题

```python
    def __str__(self):
        return self.title
```

`__str__()`方法用于在显示模型的时候显示str。

如果定义了unicode\(\)方法但是没有定义str\(\)方法，Django会自动提供一个str\(\)方法调用unicode\(\)方法，然后把结果转换为UTF-8编码的字符串对象。在实际开发中，建议：只定义unicode\(\)方法，需要的话让Django来处理字符串对象的转换。

在django 2中这种方式被修改了。

