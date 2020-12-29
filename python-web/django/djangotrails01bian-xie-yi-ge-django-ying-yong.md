# DjangoTrails01编写一个Django 应用

## 创建一个django项目

打开pycharm项目工程，在安装了django的venv下，创建django项目

```bash
$ django-admin startproject youyu
```

执行完成之后可以看到多了一个youyu的文件夹

## 先看到结果

```bash
# 进入到youyu项目目录
$ cd youyu/

# 运行程序
$ python manage.py runserver

# 如果需要其他人可以访问的话，可以使用如下
$ python manage.py runserver 0:8000
```

完成之后可以看到在127.0.0.1:8000上起了我们的web服务，点击之后即可访问

![-w1241](http://ossp.pengjunjie.com/mweb/15579745046709.jpg)

![-w1280](http://ossp.pengjunjie.com/mweb/15579745746022.jpg)

## 看生成文件目录

```bash
youyu/
    manage.py  #管理django项目的命令行工具
    db.sqlite3  #sqlite数据库文件，轻量级数据库
    youyu/ 
        __init__.py  #初始化文件
        settings.py  #Django项目的配置文件
        urls.py  #url声明，类似目录，整理每个目录页面如何响应
        wsgi.py  #项目的运行在 WSGI 兼容的Web服务器上的入口。
```

## 创建 Blog 应用

```bash
youyu valentine$ python manage.py startapp blog
```

可以看到多了文件目录

![-w215](http://ossp.pengjunjie.com/mweb/15579757428922.jpg)

### 添加第一个View页面

在blog/view.py中添加index方法。用于后续调用

```text
from django.shortcuts import render

# Create your views here.

from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. This is MyBlog")
```

### 添加url 解析

在blog目录下新建一个urls.py文件，用于请求的解析

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

在入口的urls中将这个url进行导入 编辑 youyu/urls.py文件

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),  #添加这一行代码
]
```

### 启动服务器查看

```bash
python manage.py runserver
```

