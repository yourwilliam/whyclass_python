# Django Model Query

django 对于model的查询使用较多，会包含在view中做查询。

当前已经使用的如下：

```py
articles = Article.objects.order_by('-updatedAt')
categories = Category.objects.all()
```

## 创建对象

### 使用save()方法可以进行对象的创建

```py
>>> from blog.models import Blog
>>> b = Blog(name='Beatles Blog', tagline='All the latest Beatles news.')
>>> b.save()
```

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

