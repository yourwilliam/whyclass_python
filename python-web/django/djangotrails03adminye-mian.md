# DjangoTrails03Admin页面

## 首选创建超级管理员

```bash
(venv) williamtekiMacBook-Pro:youyu valentine$ python manage.py createsuperuser
用户名 (leave blank to use 'valentine'): yourwilliam
电子邮件地址: yourwilliam@gmail.com
Password: 
Password (again): 
Superuser created successfully.
```

## 启动服务器并访问

使用`python manage.py runserver`启动服务器

访问 [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/) 访问管理控制台

![-w1280](http://ossp.pengjunjie.com/mweb/15579872468042.jpg)

## 添加Article 页面

编辑 blog/admin.py文件

```python
from django.contrib import admin

# Register your models here.
from .models import Article

admin.site.register(Article)
```

## 试试添加一个Article对象

