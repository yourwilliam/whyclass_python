# Python 基础2 —— files 

File的打开和关闭

通过dash 或者 DevDocs查看open方法

dash:

![-w1280](http://ossp.pengjunjie.com/mweb/15600703236357.jpg)

DevDocs

![-w1280](http://ossp.pengjunjie.com/mweb/15600703454903.jpg)


## 文件的打开方式

* r只读，r+读写，不创建
* w新建只写，w+新建读写，二者都会将文件内容清零（以w方式打开，不能读出。w+可读写）
* w+与r+区别：
    * r+：可读可写，若文件不存在，报错；
    * w+: 可读可写，若文件不存在，创建
    * 说明r+进行了覆盖写。
* 以a,a+的方式打开文件，附加方式打开
* a：附加写方式打开，不可读；a+: 附加读写方式打开

## 文件的操作流程

1. open打开一个文件，获取File句柄
2. 对文件进行read和write操作
3. 关闭文件

## with as 打开文件

```py
# Read the entire file as a single string
with open('somefile.txt', 'rt') as f:
    data = f.read()

# Iterate over the lines of the file
with open('somefile.txt', 'rt') as f:
    for line in f:
        # process line
        ...
```

## seek()

Python 文件 seek() 方法用于移动文件读取指针到指定位置。

## python的文件写入

在下面这里断点一下，看看是否会写入？

![-w533](http://ossp.pengjunjie.com/mweb/15603098999016.jpg)


>>>扩展阅读：
>>>[文件部分扩展阅读](https://python3-cookbook.readthedocs.io/zh_CN/latest/chapters/p05_files_and_io.html)

