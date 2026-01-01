# python基础

## Python Trails 01

### 命令行运行模式：

#### 相应交互模式

windows 打开 powershell , Mac 打开 Terminal。

使用场景: 平时的测试，小功能使用。

#### IDLE 控制台

IDLE： 自带集成开发环境、非商业、初学者使用。

使用场景：简单的小型项目，基本不怎么使用。(可以作为知识点了解一下)

**Mac 使用 python 控制台**

```bash
# 首先通过which命令查询到
williamtekiMacBook-Pro:bin valentine$ which python3
/usr/local/Cellar/python/3.6.4_2/bin//python3

# 进入到相应目录
williamtekiMacBook-Pro:bin valentine$ cd /usr/local/Cellar/python/3.6.4_2/bin/

# 执行并启动IDLE
williamtekiMacBook-Pro:bin valentine$ idle3.6
```

完成之后可以看到IDLE

![-w587](http://ossp.pengjunjie.com/mweb/15597081424792.jpg)

**windows使用IDLE控制台**

开始菜单中直接搜索打开即可。

#### 文件运行模式

使用python命令来运行python脚本。

使用场景： 在真实生产运行环境上使用的方法。当前我们使用pycharm等工具运行python实际上也是包装的使用这种方法运行。同时后面的其他python框架也基本都是使用这种来执行。

运行方法：

windows打开powershell， mac打开terminal。

```bash
# 第一步可以使用cd找到相应的文件目录
williamtekiMacBook-Pro:python_trails01 valentine$ cd /Users/valentine/workspace/python_trails/PythonWeb/code/python_trails01
# 使用python3执行python命令
williamtekiMacBook-Pro:python_trails01 valentine$ python3 trails01.py
Hello World!noyes Hello Again
I like typing this.
This is fun.
Yay! Printing.
I'd much rather you 'not'.
I "said" do not touch this.
I
 said" do not touch this.
```

![-w566](http://ossp.pengjunjie.com/mweb/15597118379478.jpg)

这种模式一定要记住，实际上python的所有执行都是使用的这种方式。

**补充讲解： cd命令**

cd (change directory)

理解方式：在windows或者mac上，我们可以直接使用开始菜单或者快捷方式来运行程序。同时我们也可以打开资源管理器(我的电脑)或者Mac上的Finder，找到运行文件的路径，双击来运行。这种在资源管理器上切换目录的方式可以理解成命令行中的cd模式。

例子： 使用命令行打开软件 windows 下打开powershell，来打开IE浏览器 ![-w609](http://ossp.pengjunjie.com/mweb/15597115469569.jpg)

mac下打开terminal来打开keynote

![-w627](http://ossp.pengjunjie.com/mweb/15597116605483.jpg)

**补充讲解： 服务器操作模式**

我们当前使用的比如 mac、windows 10都是桌面操作系统，这些大家可能比较熟悉。桌面操作系统的优点是用户交互，让用户简便的娱乐和办公。

服务器操作系统更多的是解决文件系统、网络、安全性。

服务器操作系统简要讲述：

[知乎 - 服务器的操作系统有哪些](https://zhuanlan.zhihu.com/p/44189592)

**补充讲解： 远程连接**

前面记得看到多台电脑之间，可以使用远程连接来访问。远程连接其实很多情况下会使用在机房的维护上(如果家里有多台电脑，也可以方便的使用远程连接)。

我们平时使用电脑(PC机)，很多由主机和显示器组成。但是在机房中，主要放置的是服务器(可以理解成台式机的主机部分)。而没有显示器，所以如果要操作这些电脑，实际上会采用远程桌面和远程连接的方式。

远程桌面主要用户针对图形化界面的远程连接协议，远程连接主要用于针对命令行式的用户远程连接协议。

远程连接主要使用几种协议 VNC(主要用户Linux)， RDP(主要用于windows)、SPICE（主要用于虚拟机） 在个人方面RDP 使用较多。

### print 与 终端：

在服务器端操作，实际上非常重要的是人机交互。如上面讲的，如果在桌面操作系统，或者手机操作系统上，我们的交互感官是图形化界面。而在服务器上，我们的交互感官是命令提示符(可以理解成terminal终端)

print方式是python程序用于和用户交互重要的方式。也是服务器维护中使用最多的和终端用户交互方式。

### 方法调用：

方法调用的格式

`方法名(参数,参数名=参数)`

看到这种情况就一定是方法调用。

### 格式化：

MAC ： alt+cmd+L Windows: ctrl+alt+L

## Trails 02

python 注释：

python注释可以使用两种方式：

* `#`单行注释
* """多行注释

## Trails03

数字和Math方法

### 除法

`/`和`//` python3 对于两个整数相除，默认使用会变为浮点型

#### X / Y类型：

在Python2.6或者之前，这个操作对于整数运算会省去小数部分，而对于浮点数运算会保持小数部分；在Python3.0中变成真除法（无论任何类型都会保持小数部分，即使整除也会表示为浮点数形式）。

#### X // Y 类型：

Floor除法：在Python 2.2中新增的操作，在Python2.6和Python3.0中均能使用，这个操作不考虑操作对象的类型，总是省略小数部分，剩下最小的能整除的整数部分。 Floor除法：效果等同于math模块中的floor函数： math.floor(x) ：返回不大于x的整数 所以当运算数是负数时：结果会向下取整。

```python
>>> 5//3   #1.6666666666666667
1
>>> -5//3
-2
```

### `%`运算符

```python
>>> 5%2
1
>>> 5%1.5
0.5
>>> 5%1.2
0.20000000000000018
>>>
```

[浮点数请参考](https://www.zhihu.com/question/25457573)

### 运算符优先级

![](http://ossp.pengjunjie.com/mweb/15597221339886.jpg)

### boolean的运算方式

FALSE: 0 True: 1 (除0以外)

### 补充讲解编码方式：

bit (位)：二进制位

byte (字节)：1个字节等于8个比特（1Byte=8bit）

word（字）：1个字等于4个字节

xx位机的xx位是指字长。这个字和word不一样，是指这种CPU一次能运算的数据长度，32位机就是一次运算32个二进制位，64位机就是一次运算64个二进制位

字节是寻址的最小单位。内存中两个紧挨着的字节，它们的内存地址差1。但是一个字节内的位，就没有地址的概念。你当然也可以定义一种计算机，每个位对应一个内存地址，但是在现代太另类了，估计没有人为你的计算机编程。字是计算机一次处理数据的最大单位。多数情况下，这有几个含义：CPU的寄存器的长度是一个字；CPU一个指令最多从内存中读取的数据量就是一个字；最大的寻址空间，是2^字长（如果一个字是64位，那么最大的寻址空间就是2的64次方）。

#### ASCII 码

8个二进制位，一个字节，128字符编码，第一位为0，只使用后面7位，

#### UTF-8 码

UTF-8是一种变长字节编码方式。对于某一个字符的UTF-8编码，如果只有一个字节则其最高二进制位为0；如果是多字节，其第一个字节从最高位开始，连续的二进制位值为1的个数决定了其编码的位数，其余各字节均以10开头。UTF-8最多可用到6个字节。 如表： 1字节 0xxxxxxx 2字节 110xxxxx 10xxxxxx 3字节 1110xxxx 10xxxxxx 10xxxxxx 4字节 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx 5字节 111110xx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx 6字节 1111110x 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx

[字符编码参考](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

```python
>>> # Python2
>>> a = 'Hello,中国'  # 字节串，长度为字节个数 = len('Hello,')+len('中国') = 6+2*2 = 10
>>> b = u'Hello,中国'  # 字符串，长度为字符个数 = len('Hello,')+len('中国') = 6+2 = 8
>>> c = unicode(a, 'gbk')  # 其实b的定义方式是c定义方式的简写，都是将一个GBK编码的字节串解码（decode）为一个Uniocde字符串
>>> 
>>> print(type(a), len(a))
(<type 'str'>, 10)
>>> print(type(b), len(b))
(<type 'unicode'>, 8)
>>> print(type(c), len(c))
(<type 'unicode'>, 8)
>>>
```

```python
>>> # Python3
>>> a = 'Hello,中国'  # 字节串，长度为字节个数 = len('Hello,')+len('中国') = 6+2*2 = 10
>>> b = u'Hello,中国'  # 字符串，长度为字符个数 = len('Hello,')+len('中国') = 6+2 = 8
>>> c = unicode(a, 'gbk')  # 其实b的定义方式是c定义方式的简写，都是将一个GBK编码的字节串解码（decode）为一个Uniocde字符串
>>> 
>>> print(type(a), len(a))
(<type 'str'>, 8)
>>> print(type(b), len(b))
(<type 'unicode'>, 8)
>>> print(type(c), len(c))
(<type 'unicode'>, 8)
>>>
```

## Trails04

### 何为变量

数学中的变量：

![-w702](http://ossp.pengjunjie.com/mweb/15597251105074.jpg)

Python中的变量：

[python 变量在内存中的表示（变量赋值误区）](https://blog.csdn.net/yj928674542/article/details/76269531) [图解Python变量与赋值](https://foofish.net/python-variable.html) 下面这个以后看 [python基础（5）：深入理解 python 中的赋值、引用、拷贝、作用域](https://my.oschina.net/leejun2005/blog/145911)

### 变量的命名规则

1、模块 模块尽量使用小写命名，首字母保持小写，尽量不要用下划线(除非多个单词，且数量不多的情况)

```python
# 正确的模块名
import decoder
import html_parser

# 不推荐的模块名
import Decoder
```

2、类名 类名使用驼峰(CamelCase)命名风格，首字母大写，私有类可用一个下划线开头

```python
class Farm():
    pass

class AnimalFarm(Farm):
    pass

class _PrivateFarm(Farm):
    pass
```

将相关的类和顶级函数放在同一个模块里. 不像Java, 没必要限制一个类一个模块.

3、函数

函数名一律小写，如有多个单词，用下划线隔开

```python
def run():
    pass

def run_with_env():
    pass
```

私有函数在函数前加一个下划线\_

```
class Person():

    def _private_func():
        pass
```

4、变量名

变量名尽量小写, 如有多个单词，用下划线隔开

```python
if __name__ == '__main__':
    count = 0
    school_name = ''
```

常量采用全大写，如有多个单词，使用下划线隔开

```
MAX_CLIENT = 100
MAX_CONNECTION = 1000
CONNECTION_TIMEOUT = 600
```

5、常量

常量使用以下划线分隔的大写命名

```
MAX_OVERFLOW = 100

Class FooBar:

    def foo_bar(self, print_):
        print(print_)
```

## Trails 05

### 格式化字符串

#### python3的格式化字符串

```python
print('My name is {name}.'.format(name = name))

# 即便是简化的版本
print('My name is {}.'.format(name))
```

#### python3.6提供的格式化字符串方法

```python
>>> name = "Tom"
>>> age = 3
>>> f"His name is {name}, he's {age} years old."
>>> "His name is Tom, he's 3 years old."
```

更细节的格式化字符串参考

[python3 f-string格式化字符串的高级用法](https://mlln.cn/2018/05/19/python3%20f-string%E6%A0%BC%E5%BC%8F%E5%8C%96%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95/) 上面这篇一定要看一下

[Python3.6新的字符串格式化语法](https://imliyan.com/blogs/article/Python3.6%E6%96%B0%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%A0%BC%E5%BC%8F%E5%8C%96%E8%AF%AD%E6%B3%95/)

## Trails 10

![](http://ossp.pengjunjie.com/mweb/15597281180483.jpg)

\a 响铃

## Trails12

### pydoc

Pydoc是python自带的一个文档生成工具，使用pydoc可以很方便的查看类和方法结构

mac 启动pydoc

```bash
(venv) williamtekiMBP:code valentine$ pydoc3.6 -w atexit
wrote atexit.html
(venv) williamtekiMBP:code valentine$ pydoc3.6 -p 5000
Server ready at http://localhost:5000/
Server commands: [b]rowser, [q]uit
server>
```

windows启动pydoc

```bash
python -m pydoc -w atexit   //在当前目录创建atexit.html
python -m pydoc -p 5000    //启动一个Web服务器监听http://localhost:5000/
```

### python sdk

#### [dash](https://kapeli.com/dash)

[dash xclient 下载点](https://xclient.info/s/dash.html)

Dash 是适用于Mac OS平台的软件编程文档管理工具，可以浏览API文档，以及管理代码片段工具。Dash自带了丰富的API文档，涉及各种主流的编程语言和框架。

通过Dash可以浏览API文档，以及管理代码片段工具。Dash自带了丰富的API文档，涉及各种主流的编程语言和框架，包括:ActionScript, Android, C++, CAppuccino, Cocos2D, Cocos3D, Corona, CSS, Django, Groovy, HTML, Java, JavaFX, JavaScript, jQuery, Kobold2D, Lua, MySQL, Node.js, Man Pages, Perl, PHP, Python, Ruby, Ruby on Rails, Scala, Sparrow, SQLite, Unity 3D, WordPress, XSLT, XUL。

利用Dash的代码片段管理功能，你可以把日常使用频繁的代码保存起来，然后为其设置一个独一无二的缩写，这样一来原本需要一遍又一遍的敲击键盘重复录入的繁琐工作，就可以交给Dash来轻松搞定。

缺点： 收费。 不购买VIP也可以使用，但是查每个文件需要等10秒钟（实际上也不是不能忍受）。

![-w1280](http://ossp.pengjunjie.com/mweb/15600695224763.jpg)

#### [DevDocs](https://devdocs.io)

windows上可以使用的Dash的网页版，非常好用的工具。

网页版的API文档工具，也同样集成了非常多的语言和框架接口文档。使用起来非常方便。Mac和Windows用户都可以使用。

![-w1280](http://ossp.pengjunjie.com/mweb/15600696492911.jpg)

## Trails 13

import python给我们预置了很多常用的功能，这些功能以module的形式组织起来，使用import关键字就可以把我们需要的内容导入进来，从而在脚本里使用。

上面的代码里，我们从sys module里导入了argv这个功能。

argv argv的意思是argument variable，这是大多数编程语言里的标准概念。argv里保存了脚本运行时你传入的所有的命令行参数以及脚本名称。看下面的例子

```bash
python something.py first second third # argv = [something.py, first, second, third]
python something.py my_var # argv = [something.py, my_var]
python something.py # argv = [something.py]
```

所以argv里按顺序保存了脚本名称以及各个命令行参数。

注意：命令行参数是以空格分隔的

unpack 简单来说，unpack就是把一组数据按顺序的保存到变量里。看下面的例子

```python
argv = ['something.py', 'first', 'second', 'third']
a, b, c, d = argv # a='something.py' b='first', c=second d='third'
argv = ['something.py', 'my_var']
script, the_var = argv # script='something.py' the_var='my_var'
```

上面的代码里script, case\_id = argv的作用就是把第1个命令行参数赋值给变量case\_id

> > > 基础部分扩展阅读： [数据类型和变量](https://www.liaoxuefeng.com/wiki/1016959663602400/1017063826246112) [字符串和编码](https://www.liaoxuefeng.com/wiki/1016959663602400/1017075323632896) [条件判断](https://www.liaoxuefeng.com/wiki/1016959663602400/1017099478626848)
