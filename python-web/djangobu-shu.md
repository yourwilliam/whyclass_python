# 网站初始化部署和展示

## 1. 域名购买

国内推荐[阿里云域名](https://wanwang.aliyun.com/)

优势：阿里云购买可以在一个平台搞定域名、主机等各种服务，适合长期在国内并把服务架设到国内的个人。
劣势：所有域名网站都需要备案，备案比较麻烦，且周期大概在15天到一个月。但是比国外买域名在国内备案稍微简单一些。

国外推荐[godaddy](https://sg.godaddy.com/zh)

链接显示的是新加坡主站，也可以选择其他国际站点。

优势：在国外用比较方便，结合国外的服务器，不需要备案可以直接上线，操作起来更方便，可以随时购买随时使用。
劣势：最好有信用卡，支付起来会比较方便。如果想在国内使用，备案会比较复杂。

## 2. 服务器购买

国内推荐：
[阿里云服务器](https://www.aliyun.com/product/ecs?spm=5176.8142029.388261.92.e9396d3eHJUQ0E)

可以作为第一选择

注册登陆后，进入控制台，在ecs中购买

如果只使用django和mysql的话，直接使用1v1G的服务器足够使用。带宽选择1M的限额带宽。足够平时的小型网站使用

![](http://ossp.pengjunjie.com/mweb/15602194880455.jpg)

![](http://ossp.pengjunjie.com/mweb/15602195379747.jpg)


![](http://ossp.pengjunjie.com/mweb/15602195159529.jpg)


AWS： 

如果买国外的域名可以直接使用AWS进行部署，这样就都不需要国内的备案。建议在国外长待的可以使用这种方式。如果主要访问为国内用户的话，AWS会出现国内访问较慢，以及时常的国内访问抽风的情况。

AWS的服务器的优势是使用最小配置，需要绑定信用卡，绑定信用卡首年免费。

Heroku：

heroku采用容器模型进行配置，是国外现在非常流行的方式。


## 域名备案

以下以阿里云模式作为介绍

在国内的所有网站都需要做域名备案，在阿里鱼的备案中心可以直接做备案。



![-w1279](http://ossp.pengjunjie.com/mweb/15602209408019.jpg)

我们可以使用个人性质进行备案。需要使用身份证进行备案。

![-w1032](http://ossp.pengjunjie.com/mweb/15602209881607.jpg)

备案后需要上传个人手持身份证照片和备案背景墙照片。

## 服务器配置

### 整体配置架构
![](http://ossp.pengjunjie.com/mweb/15602251299814.jpg)

在服务器端部署和安装涉及到Nginx、uWSGI、python、django、mysql、Git等环境。

### 登陆服务器

登陆阿里云控制台可以看到我们的ecs服务器。也可以看到公网
![](http://ossp.pengjunjie.com/mweb/15602224776793.jpg)


![-w1024](http://ossp.pengjunjie.com/mweb/15602255089403.jpg)


使用ssh访问

```sh
williamtekiMacBook-Pro:~ valentine$ ssh root@47.110.156.109
root@47.110.156.109's password:
Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-48-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 * Ubuntu's Kubernetes 1.14 distributions can bypass Docker and use containerd
   directly, see https://bit.ly/ubuntu-containerd or try it now with

     snap install microk8s --classic

Welcome to Alibaba Cloud Elastic Compute Service !

Last login: Tue Jun 11 12:01:11 2019
```

### python的安装

Ubuntu默认安装了python2.7和python3.6，可以在命令控制台使用python测试相应的版本。
![-w324](http://ossp.pengjunjie.com/mweb/15602273609236.jpg)

### mysql的安装

后台使用mysql。所以我们需要安装mysql

安装前执行`apt-get update`来更新服务器包配置

```sh
root@iZbp1gkjjwb0uadqq8s47uZ:~# apt-get update
Get:1 http://mirrors.cloud.aliyuncs.com/ubuntu bionic InRelease [242 kB]
Get:2 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security InRelease [88.7 kB]
Get:4 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/universe Sources [9051 kB]
Get:5 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/main Sources [829 kB]
Get:6 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/main amd64 Packages [1019 kB]
Get:7 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/main i386 Packages [1007 kB]
Get:8 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/main Translation-en [516 kB]
Get:9 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/universe amd64 Packages [8570 kB]
Get:10 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/universe i386 Packages [8531 kB]
Get:11 http://mirrors.cloud.aliyuncs.com/ubuntu bionic/universe Translation-en [4941 kB]
Get:12 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/universe Sources [244 kB]
Get:13 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/main Sources [276 kB]
Get:14 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/main i386 Packages [533 kB]
Get:15 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/main amd64 Packages [641 kB]
Ign:16 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/main Translation-en
Get:17 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/universe amd64 Packages [949 kB]
Get:18 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/universe i386 Packages [936 kB]
Ign:19 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/universe Translation-en
Get:20 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/universe Sources [130 kB]
Get:21 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/main Sources [97.1 kB]
Get:22 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/main amd64 Packages [382 kB]
Get:23 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/main i386 Packages [289 kB]
Ign:24 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/main Translation-en
Get:25 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/universe i386 Packages [252 kB]
Get:26 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/universe amd64 Packages [257 kB]
Ign:27 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/universe Translation-en
Get:16 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/main Translation-en [237 kB]
Get:19 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-updates/universe Translation-en [280 kB]
Get:24 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/main Translation-en [137 kB]
Get:27 http://mirrors.cloud.aliyuncs.com/ubuntu bionic-security/universe Translation-en [145 kB]
Fetched 40.7 MB in 8s (4854 kB/s)
Reading package lists... Done
```

安装 mysql 服务

```sh
# 安装mysql服务
sudo apt-get install mysql-server
# 安装客户端
sudo apt install mysql-client
# 安装依赖
sudo apt install libmysqlclient-dev
# 检查状态
sudo netstat -tap | grep mysql
```

mysql的默认安装是不带密码的，所以可以直接登陆进去，这时我们需要给默认的root用户带上密码，减少安全隐患和方便后续登陆。

设置root账号的密码：

直接在控制台输入mysql进入mysql 管理控制台

```sh
root@iZbp1gkjjwb0uadqq8s47uZ:~# mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.26-0ubuntu0.18.04.1 (Ubuntu)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> update mysql.user set authentication_string=PASSWORD('123456'), plugin='mysql_native_password' where user='root';
Query OK, 1 row affected, 1 warning (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 1

mysql> flush privileges
    -> ;
Query OK, 0 rows affected (0.00 sec)

```

修改了密码之后，登陆方式需要修改成

```sh
mysql -u root -p
```

默认的mysql为了安全起见是不配置远程登陆的，但是我们在开发等环境时往往需要使用远程登陆，所以我们可以配置mysql的远程连接。

```sh
# 修改配置文件，注释掉bind-address = 127.0.0.1
$ sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

# 保存退出，然后进入mysql服务，执行授权命令：
$ mysql -uroot -p

mysql> grant all on *.* to root@'%' identified by '123456' with grant option;
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
$ sudo /etc/init.d/mysql restart

```

最后使用navicat 测试登陆mysql

![-w502](http://ossp.pengjunjie.com/mweb/15602313875545.jpg)


### Git的安装和配置

```sh
root@iZbp1gkjjwb0uadqq8s47uZ:~# apt-get install git

#进入到opt目录
root@iZbp1gkjjwb0uadqq8s47uZ:~# cd /opt

# 克隆项目到服务器
root@iZbp1gkjjwb0uadqq8s47uZ:/opt# git clone http://git.yuketang.net/yourwilliam/youyulab-web.git

```

### 安装virtualenv

```sh
#安装pip3
root@iZbp1gkjjwb0uadqq8s47uZ:/opt/youyulab-web# apt install python3-pip

#创建venv
root@iZbp1gkjjwb0uadqq8s47uZ:/opt/youyulab-web# virtualenv -p /usr/bin/python3.6 venv

#切换到virtualenv虚拟环境
root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# source venv/bin/activate
(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web#

#安装依赖包
(venv) root@iZbp1gkjjwb0uadqq8s47uZ:/opt/youyulab-web# pip install -r requirements.txt

#安装包依赖
(venv) root@iZbp1gkjjwb0uadqq8s47uZ:/opt/youyulab-web# python manage.py makemigrations
No changes detected

#生成依赖关系
(venv) root@iZbp1gkjjwb0uadqq8s47uZ:/opt/youyulab-web# python manage.py migrate
```

最后在数据库中就可以看到这些文件了

![-w320](http://ossp.pengjunjie.com/mweb/15602428622805.jpg)


最后可以使用python manage.py runserver 来启动测试

#### 生成static文件

在settings.py中添加配置 `STATIC_ROOT = 'static/'`

再执行`python3 manage.py collectstatic` 来生成静态文件

### 配置nginx

```sh
#切换到非virtualenv环境
(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# deactivate

# 安装uwsgi
root@iZbp1gkjjwb0uadqq8s47uZ:~# pip3 install uwsgi

#安装nginx
sudo apt-get install nginx

```

配置uwsgi
创建uwsgi_youyulab.ini文件

```sh
-- Support: http://www.ubuntu.com/support
--
[uwsgi]
chdir = /opt/youyulab-web
home = /opt/youyulab-web/venv
module = youyu.wsgi:application
#wsgi-file = /opt/destiny/destiny-core/django_uwsgi.py

master = true
processes = 2
enable-threads = true

# use unix socket because it is more secure and faster than TCP socket
socket = %(chdir)/uwsgi/uwsgi-destiny.sock
status = %(chdir)/uwsgi/uwsgi-destiny.status
pidfile = %(chdir)/uwsgi/uwsgi-destiny.pid
daemonize = %(chdir)/uwsgi/uwsgi.log


chmod-socket = 662
vacuum = true
die-on-term = true

logto = %(chdir)/uwsgi/uwsgi-destiny.log

env = LANG=en_US.UTF-8
env = LC_ALL=en_US.UTF-8
env = PYTHONIOENCODING=UTF-8
~
```

启动uwsgi

```
#切换到venv环境
root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# source venv/bin/activate

(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# uwsgi --ini uwsgi_youyulab.ini
[uWSGI] getting INI configuration from uwsgi_youyulab.ini
```

可以通过日志查看启动日志信息

```
(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# vi uwsgi/uwsgi.log
```


设置nginx配置文件:

`vi /etc/nginx/conf.d/youyulab.conf`

```sh
server {
    listen   80;
    charset utf-8;
    server_name  lab.yuketang.net;
    access_log  /var/log/nginx/destiny/access.log;
    error_log   /var/log/nginx/destiny/error.log;

    proxy_http_version 1.1;
    proxy_set_header Connection "";

    location / {

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        include uwsgi_params;
        uwsgi_pass_request_body on;
        uwsgi_pass_request_headers on;
        uwsgi_pass  unix:/opt/youyulab-web/uwsgi/uwsgi-destiny.sock;
        uwsgi_read_timeout 1800;
        uwsgi_send_timeout 300;
        proxy_connect_timeout 600;
        proxy_read_timeout 600;
        sendfile        on;
        client_max_body_size 20M;
        keepalive_timeout  0;
    }


    location /static/ {
        alias /opt/youyulab-web/static/;
    }
}

```


```sh
# 完成后需要创建nginx日志目录地址
root@iZuf67ehbr4ubh7ress6u8Z:~# mkdir /var/log/nginx/destiny/

# 完成后重启nginx
root@iZuf67ehbr4ubh7ress6u8Z:~# service nginx restart
```

这些生成后配置域名解析

![](http://ossp.pengjunjie.com/mweb/15602646544484.jpg)

![](http://ossp.pengjunjie.com/mweb/15602647464868.jpg)

![](http://ossp.pengjunjie.com/mweb/15602649573574.jpg)


![-w1032](http://ossp.pengjunjie.com/mweb/15602456432748.jpg)

完成后等待配置完毕，访问即可。

直接访问会出现如下问题，是由于没有加入到allowed_hosts中的原因。
![](http://ossp.pengjunjie.com/mweb/15602652303800.jpg)

修改如下

修改django的 settings.py文件

```sh
root@iZuf67ehbr4ubh7ress6u8Z:~# vi /opt/youyulab-web/youyu/settings.py

```

```py
ALLOWED_HOSTS = ["lab.yuketang.net"]
```

重启uwsgi即可

```sh
root@iZuf67ehbr4ubh7ress6u8Z:~# ps -ef|grep uwsgi
root      7456     1  0 22:48 ?        00:00:00 uwsgi --ini uwsgi_youyulab.ini
root      7458  7456  0 22:48 ?        00:00:00 uwsgi --ini uwsgi_youyulab.ini
root      7459  7456  0 22:48 ?        00:00:00 uwsgi --ini uwsgi_youyulab.ini
root      7702  7530  0 23:02 pts/1    00:00:00 grep --color=auto uwsgi
root@iZuf67ehbr4ubh7ress6u8Z:~# kill -9 7456

#切换到virtualenv环境
root@iZuf67ehbr4ubh7ress6u8Z:~# cd /opt/youyulab-web/
root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# source venv/bin/activate
(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web# uwsgi --ini uwsgi_youyulab.ini
#启动uwsgi
[uWSGI] getting INI configuration from uwsgi_youyulab.ini
(venv) root@iZuf67ehbr4ubh7ress6u8Z:/opt/youyulab-web#
```

![](http://ossp.pengjunjie.com/mweb/15602456864082.jpg)
