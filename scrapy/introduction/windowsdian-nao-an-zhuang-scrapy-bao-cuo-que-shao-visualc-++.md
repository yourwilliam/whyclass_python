# windows电脑安装scrapy的问题

windows电脑在安装scrapy的时候，可能需要依赖Twisted包，这个包直接使用pip安装的时候会要求依赖Microsoft buildtools Visual C++ 14.0 up，但是这个东西在build tools里又总是很难找到，解决方法是可以直接安装下载的包，这样就不会出现这个依赖了，下载地址

https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted

下载后执行pip install 这个文件就可以了。