# django分页

当blog中的article内容很多的时候，可能会一页加载很多的内容给客户，这样可能会造成客户加载时间很长的情况，这是我们需要分页显示。

其实我们在很多地方已经看过导航条了，比如bilibili.com的导航条

![-w741](http://ossp.pengjunjie.com/mweb/15596402708721.jpg)


同样我们也给我们的blog加上分页导航。

django的当前版本已经自带了导航模块，我们可以使用django的导航模块即可。



```py
from django.core.paginator import Paginator



def index(request):
    # articles = Article.objects.order_by('-updatedAt')
    articles = Article.objects.filter(deletedAt=None).filter(status=2).order_by('-updatedAt')
    categories = Category.objects.filter(deletedAt=None)
    tags = Tag.objects.all()

    # 分页
    paginator = Paginator(articles, 5)
    page = request.GET.get('page')
    if not page:
        page = 1

    articles = paginator.get_page(page)

    context = {
        'articles': articles,
        'categories': categories,
        'tags': tags,
    }
    return render(request, 'blog/blog_image_rs.html', context)
```

第二步修改Template页面：

```html
<div class="ed_blog_bottom_pagination">
    <div class="row">
        <nav>
            <ul class="pagination">
                {% if articles.has_previous %}
                    <li><a href="?page=1">1</a></li>
                    <li><a href="?page={{articles.previous_page_number}}">previous</a></li>
                {% endif %}

                <li class="active"><a href="#">{{articles.number}}</a></li>

                {% if articles.has_next %}
                    <li><a href="?page={{articles.next_page_number}}">next</a></li>
                    <li><a href="?page={{articles.paginator.num_pages}}">last</a></li>
                {% endif %}
            </ul>
        </nav>
    </div>
</div>
```

