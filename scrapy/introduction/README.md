# Install

## MAC安装scrapy

mac电脑在virtualenv中直接安装即可

```bash
pip install scrapy
```

## Windows 安装Scrapy

在windows中也可以使用pip来安装

* Python 2 / 3
* 升级pip版本：pip install --upgrade pip
* 通过pip 安装 Scrapy 框架pip install Scrapy

在windows安装中总会报一个错 `visual c++ build tools 2017 is required`

解决方法，这个包的问题主要出在Twist包上，在pip中的Twist包需要依赖visual c++环境，下载包非常大，而且很难找到相应的包，解决方案是手动安装一下Twist包

[twisted下载地址](https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted)

下载完之后在virtualenv的环境下pip安装指定的这个文件即可

```bash
pip install Twisted-19.2.0-cp37-cp37m-win32.whl
```

