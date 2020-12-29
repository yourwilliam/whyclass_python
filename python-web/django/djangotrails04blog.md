# DjangoTrails04博客建立

## url的能力，新的视图创建

### 1. 创建视图

针对blog业务，可以分为两个主要页面，一个是blog\_list页面，展示所有的blog信息。另一个是blog\_detail页面，展示当前blog的详情页面。

```python
from django.shortcuts import render

# Create your views here.

from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. This is william blog")


def blog_single(request, question_id):
    return HttpResponse("Blog single")
```

### 2. 添加url，绑定视图

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.blog_single, name='detail'),
]
```

其中`<int:question_id>/` 用于配置int型参数的绑定。在View中使用参数question\_id参数进行整体绑定。

## 创建真实View，和模型进行绑定

真实的View，从model模型类获取相应的模型数据，将模型数据按照publish\_time的逆序进行排列。最后统一的保存并写入到前端去。

```python
from django.shortcuts import render

# Create your views here.

from django.http import HttpResponse
from .models import Article


def index(request):
    articles = Article.objects.order_by('-publish_time')
    output = ",".join([q.title for q in articles])
    return HttpResponse(output)


def blog_single(request, question_id):
    return HttpResponse("Hello, world. This is william blog")
```

`python manage.py runserver`来启动web 服务

最后通过页面访问 `http://127.0.0.1:8000/blog/`

## 整理真实HTML视图

上面的方式只适合于写一个简单的页面，是直接返回相关的内容到页面。如果要做复杂的页面，需要导入相关的内容\(HTML\)、样式\(CSS\)、事件和动作\(js\)到相应的页面。然后再通过和后端合作，将数据库中的内容写入到前端形成动态网站。

在django中使用Template和static来整理所有的页面相关内容。

[html原始文件下载链接](http://ossp.pengjunjie.com/YouyuLab_src_static.zip)

```bash
youyulab/
    blog_single_rs.html
    blog_image_rs.html
    css/
    js/
    fonts/
    images/
```

下载的文件目录如下，实际上大多数的web相关内容也都会整理成这样的文档结构。其中HTML对应页面相关内容，下面的四个文件夹一般对应网站的静态文件内容。所以我们可以将html文件对应到Template中，将其他四个文件夹内容对应到static内容。

### 1. 创建static文件

在blog app文件夹下创建static文件夹，再在static文件夹下创建blog文件夹。这里使用blog命名实际上是需要和blog app 的文件夹同名（后面会具体讲述原因）。最后我们将所有的静态四个文件夹拷入目录即可。

![-w173](http://ossp.pengjunjie.com/mweb/15584184210983.jpg)

### 2. 创建template

在blog下创建Template文件夹，同样在Template文件夹下创建blog文件夹。和static一样这里使用blog命名是需要和blog app的文件夹同名。 最后我们将html文件拷入。

![-w214](http://ossp.pengjunjie.com/mweb/15584186278805.jpg)

### 3. 修改View测试

完成之后修改View做一下测试。

blog/view.py

```python
from django.shortcuts import render

# Create your views here.

from django.http import HttpResponse
from .models import Article
from django.template import loader


def index(request):
    articles = Article.objects.order_by('-publish_time')
    output = ",".join([q.title for q in articles])
    template = loader.get_template('blog/blog_image_rs.html')

    context = {
        'articles': articles,
    }
    return HttpResponse(template.render(context, request))


def blog_single(request, question_id):
    return HttpResponse("Hello, world. This is william blog")
```

### 测试

完成后使用`python manage.py runserver`进行测试

访问`http://127.0.0.1:8000/blog/`

可以看到HTML访问页面出来了。但是是一个只有HTML没有样式的页面。接下来我们修改样式文件的引入。

### 4. 修改static文件引入

使用了Django的Template模型之后，对于静态文件的引入不能在使用HTML的文件引入方式，需要遵循django的设计方式。这里通过修改Template下的HTML文件修改。

修改blog\_image\_rs.html文件 最上面添加\`

\`

```markup
{% load static %}
<!DOCTYPE html>
<!--[if IE 8]> <html lang="en" class="ie8 no-js"> <![endif]-->
<!--[if IE 9]> <html lang="en" class="ie9 no-js"> <![endif]-->
<!--[if !IE]><!-->
<html lang="en">
<!--<![endif]-->
```

下面对于引入的静态文件进行修改

css文件修改这里

```markup
<!--srart theme style -->
<link href="{% static 'blog/css/main.css'%}" rel="stylesheet" type="text/css"/>
<!-- end theme style -->
<!-- favicon links -->
<link rel="shortcut icon" type="image/png" href="{% static 'blog/images/header/favicon.png' %}" />
</head>
```

js文件修改

```markup
<!--main js file start--> 
<script type="text/javascript" src="{% static 'blog/js/jquery-1.12.2.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/bootstrap.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/modernizr.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/owl.carousel.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/smooth-scroll.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/revel/jquery.themepunch.tools.min.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/revel/jquery.themepunch.revolution.min.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/revel/revolution.extension.layeranimation.min.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/revel/revolution.extension.navigation.min.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/revel/revolution.extension.slideanims.min.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/countto/jquery.countTo.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/plugins/countto/jquery.appear.js' %}"></script>
<script type="text/javascript" src="{% static 'blog/js/custom.js' %}"></script>
<!--main js file end-->
```

修改完之后在`python manage.py runserver`运行一下可以看到相应的样式已经找到

### 5. 修改将后台数据写入Template

首先找到html中的生成blog的部分。

![-w500](http://ossp.pengjunjie.com/mweb/15584201936792.jpg)

从页面可以看到每个ed\_blog\_item 指定了一个blog列表项。这里就是我们要的内容

在Template中修改，获取后端所有数据

```markup
{% for article in articles %}
                    <div class="ed_blog_item ed_bottompadder50">
                        <div class="ed_blog_image">
                            <a href="blog_single.html"><img src="{{article.banner}}" alt="blog image" /></a>
                        </div>
                        <div class="ed_blog_info">
                            <h2><a href="blog_single.html">{{article.title}}</a></h2>
                            <ul>
                                <li><a href="#"><i class="fa fa-user"></i> james marco</a></li>
                                <li><a href="#"><i class="fa fa-clock-o"></i> {{article.last_modify_time}}</a></li>
                                <li><a href="#"><i class="fa fa-comment-o"></i> 4 comments</a></li>
                            </ul>
                            <p class="ed_bottompadder10">{{article.description}}</p>
                            <a href="blog_single.html" class="btn ed_btn ed_orange">read more</a>
                        </div>
                    </div>
                    {% endfor %}
```

修改这一段，再讲其他的静态数据删掉。 完成之后在运行一下看看效果 后台添加几篇文章试试看

## 改改detail详情页试试看

修改 view

```python
def blog_single(request, article_id):
    article = get_object_or_404(Article, pk=article_id)
    return render(request, 'blog/blog_single_rs.html', {'article': article})
```

修改url

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:article_id>/', views.blog_single, name='detail'),
]
```

修改HTML Template static

修改html

```markup
<div class="ed_blog_item ed_bottompadder50">
                        <div class="ed_blog_image_rs">
                            <img src="{{article.banner}}" alt="blog image" />
                        </div>
                    <div class="ed_blog_info">
                        <h2>{{article.title}}</h2>
                        <ul>
                            <li><a href="#"><i class="fa fa-user"></i> james marco</a></li>
                            <li><a href="#"><i class="fa fa-clock-o"></i> {{article.last_modify_time}}</a></li>
                            <li><a href="#"><i class="fa fa-comment-o"></i> 4 comments</a></li>
                        </ul>
                        <p>{{article.content}}</p>
                    </div>
```

