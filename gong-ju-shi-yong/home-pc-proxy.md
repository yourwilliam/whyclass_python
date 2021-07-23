# 内网穿透

## 内网穿透

### 使用场景

1. 想在外面使用ipad来访问家里的台式机，进行一些基本的远程办公的时候。
2. 平时不想带厚重的笔记本，但是在外面又想在外面方便的访问。
3. 开发一些临时的Web服务，还没有部署但是又想让别人方便的访问。

### 什么叫内网穿透

如果在家里安装了一台Nas服务器，或者在家里的电脑上配置了一个Web服务器，但是这台服务器在外网是不能够访问的。

主要原因大家也知道，主要是当前我们在使用的电信网络使用了NAT的模式，家用电脑会有多个家庭使用共享的IP地址，所以家用上网都会是一个动态的IP地址，很有可能会随时改变，无法绑定到一个地址上，这样就导致了无法从公网访问家用电脑上的服务。

如何解决这种问题呢，以前使用的是动态域名的方式，通过本地定时请求动态域名，隔一段时间通过家用电脑更新DNS服务上接口，来绑定动态域名。这种方案是最简单也是最廉价的方法，只需要有一个域名就可以了。但是这种方案还是有一个时间段，如果刚好卡在时间段里面，就要等到下一个时间点更新才能访问。

当前使用较多的一种方式是直接使用反向代理。如果有一台公网的服务器，那么可以把这台服务器作为服务端，通过反向代理映射到家用端就可以了。

### 使用FRP来部署

当前使用较多的是使用frp来进行内网穿透。

frp的GitHub地址：

[frp github](https://github.com/fatedier/frp)

[frp 软件下载地址](https://github.com/fatedier/frp/releases)

具体程序逻辑如下

![](https://ossp.pengjunjie.com/mweb/16270100504729.jpg)

#### 服务器端配置

记得先开启一下服务器的安全组，否则安全组被关闭了外网是无法被访问的

![](https://ossp.pengjunjie.com/mweb/16270105569907.jpg)

这里图片中开启的是7000-7500端口，由于系统使用的是7500端口作为admin，所以将这些端口都打开了。但是实际上为了服务器安全，可以没有必要开这么多端口。但是如果减少端口的话，比如7000-7050，就需要修改在frps.ini服务器端的配置上将dashboard配置到其他的端口。

frp 里面包含两个程序 frps和frpc， 从命名就可以看出来，frps是用于服务器端的，frpc是用于客户端的，在不同的端可以启用不同的服务。

```text
# frps.ini
[common]
bind_port = 7000
token = 1234567

dashboard_user = ****
dashboard_pwd = ****
dashboard_port = 7010
```

然后 vps 上启动 frps：

```text
.\frps -c frps.ini

# 服务器端后台启动可以使用
nohup .\frps -c frps.ini &
```

#### 客户端配置

然后再家中内网服务器上编辑 frpc.ini 配置，token需要保持一致，服务器端建立添加一下token，这样会有一些加密，否则其他人也可以使用你的7000端口了。

```text
# frpc.ini
[common]
server_addr = 202.115.8.1
server_port = 7000
token = 1234567

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 3389
remote_port = 7001
```

客户端配置的token要和服务器端一致，否则没法连接。客户端的local\_port用于本地的服务端口，remote\_port用于服务器端配置的服务端口。

local\_port可以配置22，3389，80，8080这些，为了对应不同的服务。 服务端需要配置在你刚才在安全组打开的端口范围内，这样对应的本地端口就可以映射到远程了。

然后内网服务器启动 frpc：

```text
frpc -c /usr/local/etc/frpc.ini
```

#### 使用

如果你配置的是3389 ，那么你在远程的时候就远程连接服务器的IP加上端口7001就可以访问你的电脑的远程连接了。

### 多服务映射

如果你想映射家里电脑的多个服务，那么可以在客户端配置多个端口映射

```text
# frpc.ini
[common]
server_addr = 202.115.8.1
server_port = 7000
token = 1234567

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 221

[https]
type = tcp
local_ip = 192.168.1.3
local_port = 443
remote_port = 8443
```

### 将客户端配置为电脑自启动服务

之前启动的方式在windows下面必须要在powershell下执行才能启动着等待远程使用，非常不方便，最好的方式还是配置成服务的形式，并配置自动启动更方便。

首先在客户端创建一个bat文件，将运行的内容写到bat中

注意这里要写绝对目录，不然后续服务启动的时候会找不到路径

```text
# frpc.bat
C:\User\**\...\frpc.exe -c C:\User\**\...\frpc.ini
```

然后使用nssm来进行windows的服务配置

nssm 安装地址： [http://www.nssm.cc/](http://www.nssm.cc/)

![](https://ossp.pengjunjie.com/mweb/16270180284532.jpg)

![](https://ossp.pengjunjie.com/mweb/16270180340583.jpg)

我是 64 位电脑，所以使用 cmd 终端进入 E:\desktop\development\nssm-2.24\win64\(如果你们是 32 位可以选择 E:\desktop\development\nssm-2.24\win32\)

进入后输入 nssm install 服务名\(自己随便写\)

![](https://ossp.pengjunjie.com/mweb/16270180534129.jpg)

点击回车后，会出现弹框， 选择你想要的路径，点击需要的.exe 或。bat 程序。

完成之后就可以在服务中看到了。

如果想删除的话，使用 `sc.exe delete *****(服务名)`可以删除服务。删除后关闭服务，然后再打开就没有了

首次配置的话，需要手动去服务中启动一下。下次电脑重启就会自动启动了。

### 其他

更多详细的配置可以参考知乎这一篇

[https://zhuanlan.zhihu.com/p/57477087](https://zhuanlan.zhihu.com/p/57477087)

