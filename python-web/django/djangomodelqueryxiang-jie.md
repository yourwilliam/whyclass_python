# Django Model Query

django 对于model的查询使用较多，会包含在view中做查询。

当前已经使用的如下：

```py
articles = Article.objects.order_by('-updatedAt')
categories = Category.objects.all()
```

## 创建对象

### 使用save()方法可以进行对象的创建

样例：
```py
>>> from blog.models import Blog
>>> b = Blog(name='Beatles Blog', tagline='All the latest Beatles news.')
>>> b.save()
```

在我们的程序中使用做slug部分使用了重写save方法，具体可以查看models.py

```py
def save(self, *args, **kwargs):
    self.slug = slugify(self.title)
    super(Article, self).save(*args, **kwargs)

```

这个例子重写了article的save方法，其中调用uuslug的slugify方法将title的标题字段重写为slug的格式，然后赋值给slug。最后调用父类的save方法来进行保存。

注意这里一定要调用父类的方法进行保存。

## 更新对象

在django中对象的更新是可以直接使用save进行更新的，save部分字段就可以更新。


## 查询对象

### 查询所有对象

```py
# 查询对象并按照时间排序
articles = Article.objects.order_by('-updatedAt')
# 查询所有对象
categories = Category.objects.all()
```

### 根据关键字查询

`filter(**kwargs)`
根据kwargs过滤的内容返回一个QuerySet。

`exclude(**kwargs)`
根据kwargs排除过滤的内容返回一个QuerySet。

我们在查询Article的时候返回所有的对象，但是我们在设计BaseSchema的时候，使用的是软删除的方式，这种查询方法会把已删除的对象也查询出来，我们需要过滤掉deletedAt的对象。修改views.py

```py

def index(request):
    articles = Article.objects.filter(deletedAt=None).order_by('-updatedAt')
    categories = Category.objects.filter(deletedAt=None)
    context = {
        'articles': articles,
        'categories': categories,
    }
    return render(request, 'blog/blog_image_rs.html', context)
```

通过这种模式filter我们可以只查deletedAt字段为None的article。

#### 查看query的相应查询语句

经常我们在使用查询语句的时候，希望看一下最终的sql的查询语句是什么。
比较好的方式是在debug的断点中停住查看，这样更方便调试
![-w1261](media/15586016388125/15591895495754.jpg)


同时我们希望在页面中过只显示publish状态的文章。同样需要添加我们的查询条件

```py
def index(request):
    # articles = Article.objects.order_by('-updatedAt')
    articles = Article.objects.filter(deletedAt=None).filter(status=2).order_by('-updatedAt')
    categories = Category.objects.filter(deletedAt=None)
    context = {
        'articles': articles,
        'categories': categories,
    }
    return render(request, 'blog/blog_image_rs.html', context)

```
这样就能再次过滤我们的状态为publish的文章

同时在修改deletedAt的时候，也记得将admin中的部分修改。 具体可以参考[DjangoAdmin详解](python-web/django/djangoadminxiang-jie.md#admin_list_band)


Chaining filters

我们可以在查询中连接使用filter和exclude 来对结果进行过滤。如下所示

```py
articles = Article.objects.filter(deletedAt=None).filter(status=2).order_by('-updatedAt')
```

## filter lookups

在查询方法filter(), exclude() and get()中，我们可以指定更精准的查询方式，这种方式对应到sql的where方法中。

这种查询方式使用格式`field__lookuptype=value`。

查询方式包含以下几个：

#### exact
An "exact" match。 指定一个精准的匹配。类似 = 的作用

```
Entry.objects.get(id__exact=14)
Entry.objects.get(id__exact=None)
```
匹配
```
SELECT ... WHERE id = 14;
SELECT ... WHERE id IS NULL;
```

#### iexact

支持大小写不敏感的查询，使用之后可以查到当前大小写的。

```
Blog.objects.get(name__iexact='beatles blog')
Blog.objects.get(name__iexact=None)
```

```
SELECT ... WHERE name ILIKE 'beatles blog';
SELECT ... WHERE name IS NULL;
```


#### contains

大小写不敏感的like方式， 使用后可以找到前后包含的内容，同时是大小写不敏感的

```
Entry.objects.get(headline__contains='Lennon')
```

```
SELECT ... WHERE headline LIKE '%Lennon%';
```

#### icontains

大小写不敏感的icontains方式

```
Entry.objects.get(headline__icontains='Lennon')
```
SQL equivalent:
```
SELECT ... WHERE headline ILIKE '%Lennon%';
```

#### in 

在集合中查询 list, tuple, or queryset

```
Entry.objects.filter(id__in=[1, 3, 4])
Entry.objects.filter(headline__in='abc')
```
SQL equivalents:
```
SELECT ... WHERE id IN (1, 3, 4);
SELECT ... WHERE headline IN ('a', 'b', 'c');
```

```py
inner_qs = Blog.objects.filter(name__contains='Cheddar')
entries = Entry.objects.filter(blog__in=inner_qs)
```
这种写法可以使用为in查询

SQL如下

```
SELECT ... WHERE blog.id IN (SELECT id FROM ... WHERE NAME LIKE '%Cheddar%')
```

同时也可以支持对其他外键的支持

```
inner_qs = Blog.objects.filter(name__contains='Ch').values('name')
entries = Entry.objects.filter(blog__name__in=inner_qs)
```


#### gt 

Greater than.

#### gte

Greater than or equal to.

#### lt

Less than.

#### lte

Less than or equal to.

#### startswith

Case-sensitive starts-with.

```py
Entry.objects.filter(headline__startswith='Lennon')
```
SQL equivalent:
```
SELECT ... WHERE headline LIKE 'Lennon%';
```

#### istartswith
Case-insensitive starts-with.

#### endswith
Case-sensitive ends-with.

#### iendswith
Case-insensitive ends-with.

#### range
Range test (inclusive).

```py
import datetime
start_date = datetime.date(2005, 1, 1)
end_date = datetime.date(2005, 3, 31)
Entry.objects.filter(pub_date__range=(start_date, end_date))
```
SQL equivalent:

```
SELECT ... WHERE pub_date BETWEEN '2005-01-01' and '2005-03-31';
```

更多可以参考 [django官方文档filed-lookups部分](https://docs.djangoproject.com/zh-hans/2.2/ref/models/querysets/#field-lookups)


## 属性查询

join查询，SQL中提供丰富的联表join查询。在django中也可以同关系联表查询的模式。可以使用filter方式进行。

```py
Article.objects.filter(categories__title='Ielts')
```

可以用于查询所有目录标题为Ielts的Article

多次联表可以使用多个双下划线


## 复杂的Q查询

前面的filter、exclude可以提供基础的查询模式，更复杂的查询可以使用Q查询来进行

```py
from django.db.models import Q
Q(question__startswith='What')
```

可以提供or查询的能力

```py
Q(question__startswith='Who') | Q(question__startswith='What')
```

等同于SQL

```
WHERE question LIKE 'Who%' OR question LIKE 'What%'
```

多级查询

```py
Poll.objects.get(
    Q(question__startswith='Who'),
    Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6))
)
```
等同于SQL

```
SELECT * from polls WHERE question LIKE 'Who%'
    AND (pub_date = '2005-05-02' OR pub_date = '2005-05-06')
```