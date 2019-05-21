# Django 插件 django-admin-bootstrapped

[django-admin-bootstrapped github地址](https://github.com/django-admin-bootstrapped/django-admin-bootstrapped)

django 的 admin控制台还是比较方便的，配置化也比较方便管理，但是django-admin 在手机端的体验并不是那么的好。django-admin的各种类型的admin插件比较多。django-admin-bootstrapped 是比较简单的可以

## django-admin-bootstrapped 安装

* `pip install django-admin-bootstrapped` (virtualenv highly suggested)
* 在install_apps 中添加django_admin_bootstrapped。注意需要在django.contrib.admin前添加

```py
INSTALLED_APPS = (
    'django_admin_bootstrapped',
    'django.contrib.admin',

    ...
)
```

## 配置使用bootstrap 3

在installed_app 前添加bootstrapt

```py
INSTALLED_APPS = (
    'django_admin_bootstrapped.bootstrap3',
    'django_admin_bootstrapped',
    'django.contrib.admin',

    ...
)
```


## 其他插件

还可以使用其他插件来美化

[grappelli](https://github.com/sehmaschine/django-grappelli)
一直在更新维护，非常好看的api

[xadmin](https://github.com/sshwsfc/xadmin)
一个中国人写的admin客户端，很久没有维护了

[django-suit](https://github.com/darklow/django-suit/tree/v2)
也是做的比较好的，一年左右没有维护了，手机端适配做得一般般