# Scrapy生产部署

大家对于scrapy的管理主要倾向于在写scrapy上，但是很多人没有去控制如何对scrapy进行部署和使用。使用scrapyd可以很好地对各种爬虫进行管理。如果加上scrapyd-web就能更好的对爬虫进行控制和可视化。下面就分别的记录两个爬虫的使用和配置。

## scrapyd的安装和使用

scrapyd分为两个端，服务器端安装scrapyd，客户端安装scrapyd-client。然后在客户端进行爬虫的编写，完成后发布到服务器端即可。

### 1. 服务器端scrapyd的安装和使用

服务器端的scrapyd的安装可以在virtualenv下使用。

新建virtualenv的环境，然后使用pip安装 scrapyd即可。

```bash
#记得要安装Twisted，否则的话后面使用client部署会报错
pip3 install Twisted==18.9.0

pip3 install scrapyd
```

报错 `<span>builtins.AttributeError</span>: <span>'int' object has no attribute 'splitlines'</span>` 如果看到这个报错就说明需要安装Twisted

安装好之后，在venv环境下面执行 scrapyd就可以启动。但是这里注意需要修改几个配置

搜索default\_scrapyd.conf文件，在venv目录下。然后修改bind\_address 到0.0.0.0，这样才能保证外部输入

![](http://ossp.pengjunjie.com/mweb/15558365147525.jpg)

也可以在服务器端使用命令后台来开启scrapyd进程

```text
#使用后台进程启动
setsid scrapyd

#停止进程使用kill
```

### 2. 安装scrapy-client端

在本地安装scrapy-client ，`pip isntall scrapy-client`

安装完成后，在自己的scrapy工程目录下，执行

```bash
scrapyd-deploy -l
```

会生成一个scrapy.cfg文件。修改成如下配置

```text
[settings]
default = ieltsOnlineSpider.settings

[deploy:IeltsOnline]
url = http://121.41.8.92:6800/
project = ieltsOnlineSpider
```

完成之后就可以发布到服务器端了

```text
# 将爬虫部署到服务器端
1$ scrapyd-deploy IeltsOnline -p ieltsOnlineSpider

#查看部署情况
scrapyd-deploy -L IeltsOnline

#查看远程部署情况
1curl http://121.41.8.92:6800/listprojects.json

#远程启动爬虫
1$ curl http://121.41.8.92:6800/schedule.json  -d project=ieltsOnlineSpider -d spider=ielts_online
{"node_name": "iZ23b233aiuZ", "status": "ok", "jobid": "bab498fe641311e993c900163e0c780f"}
```

可以在浏览器端查询爬虫的情况

`http://121.41.8.92:6800/jobs`

在日志中可以查看到爬虫的运行情况 `http://121.41.8.92:6800/logs`

```bash
#删除一个爬虫
1curl http://119.75.216.20:6800/delproject.json -d project=<project>
```

### 配置生产环境的scrapyd

在生产环境上如果直接开启6800端口，那么任何人都可以到你的服务器上面发布scrapy任务了，这样肯定没有安全性保障，所以需要配置相应的nginx鉴权来保证用户鉴权

安装`sudo apt-get install apache2-utils`

```bash
sudo htpasswd -c /etc/nginx/htpasswd/user.htpasswd exampleuser
New password:
Re-type new password:
Adding password for user exampleuser
```

配置 nginx.conf

```text
server {
    listen 6801;
    location / {
        proxy_pass http://127.0.0.1:6800/;
        auth_basic "Restricted";
        auth_basic_user_file /etc/nginx/htpasswd/user.htpasswd;
    }
}
```

重载nginx `service nginx reload`

注意这里需要修改非6800端口，否则两个端口就冲突了。

修改scrapy的配置文件 `venv/lib/python3.6/site-packages/scrapyd/default_scrapyd.conf`

```text
bind_address = 127.0.0.1
```

记得这里一定要修改为127.0.0.1，这样就可以放置外网的访问scrapyd，而只能通过nginx进行访问了。

配置完成后重启scrapyd就可以生效了。再次访问的时候就可以

最后重新配置scrapydweb。

scrapyd可以配置成公网的，方便外部访问

```text
SCRAPYD_SERVERS = [
    '121.41.8.92:6801',
    # 'username:password@localhost:6801#group',
    #('username', 'password', 'localhost', '6801', 'group'),
]
```

配置的时候最后使用第三个元组的形式将配置项导入。然后访问的时候即可使用

## scrapydweb的使用

```bash
pip3 install scrapyd

#在这里可以修改scrapydweb的相关配置参数
vi venv/lib/python3.6/site-packages/scrapydweb/default_settings.py
```

### 基本配置

scrapydweb 的配置文件中有许多需要配置的内容，安装完成后scrapydweb会自动的将配置文件拷贝到项目目录。可以通过查看

安装完成后会在项目目录下自动配置`scrapydweb_settings_v8.py`文件

```text
# The default is '0.0.0.0'.
SCRAPYDWEB_BIND = '0.0.0.0'
# Accept connections on the specified port, the default is 5000.
SCRAPYDWEB_PORT = 5000

# The default is False, set it to True to enable basic auth for web UI.
ENABLE_AUTH = True
# In order to enable basic auth, both USERNAME and PASSWORD should be non-empty strings.
USERNAME = '*******'
PASSWORD = '*******'

#这里需要配置项目路径
SCRAPY_PROJECTS_DIR = '/root/scrapydweb/projects/'

#这里需要配置项目的日志路径，这里配置scrapyd的parseLog目录
SCRAPYD_LOGS_DIR = '/opt/scrapyd/logs'
```

### 配置nginx解析

```text
server {
    listen 80;
    server_name ******;

    location / {
        proxy_pass http://127.0.0.1:5000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass_request_body on;
        client_max_body_size 100m;
    }
}
```

完成后即可实现远程登录

## 远程发布及使用

scrapydweb支持多种远程提交到远程服务器

最简单的方法还是直接在本地scrapy项目的地方使用命令行进行上传

```bash
# 将爬虫部署到服务器端
1$ scrapyd-deploy IeltsOnline -p ieltsOnlineSpider

#查看部署情况
scrapyd-deploy -L IeltsOnline
```

每次deploy之后在服务器端会有一个版本信号，在后面调用的时候可以针对这个版本进行run

## 待完成部分

* [ ] 代理怎么使用
* [ ] 将数据保存到数据库，先使用mysql
* [ ] 版本的控制管理， [这个帖子可以将git的版本和scrapyd进行集成](https://ox0spy.github.io/post/python/scrapyd/)

参考blog

> [【Python实战】用Scrapyd把Scrapy爬虫一步一步部署到腾讯云上，有彩蛋](https://juejin.im/post/5b0b87796fb9a009e405d12c) [python – 我们如何配置scrapyd以将virtualenv用于项目？](https://codeday.me/bug/20190405/886820.html) [如何在Ubuntu上通过Nginx设置HTTP认证](https://segmentfault.com/a/1190000003793613) [scrapyd和scrapyd-client使用教程](https://ox0spy.github.io/post/python/scrapyd/) [使用Scrapyd部署爬虫](https://www.jianshu.com/p/f0077adb74bb) [官方教程平台](https://github.com/my8100/files/blob/master/scrapydweb/README_CN.md) [scrapydweb-github项目](https://github.com/my8100/files/tree/master/scrapydweb) [scrapyd官方说明文档](https://scrapyd.readthedocs.io)

