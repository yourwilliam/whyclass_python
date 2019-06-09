# Python 基础2 —— files 

File的打开和关闭

通过dash 或者 DevDocs查看open方法

dash:

![-w1280](http://ossp.pengjunjie.com/mweb/15600703236357.jpg)

DevDocs

![-w1280](http://ossp.pengjunjie.com/mweb/15600703454903.jpg)


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

>>>扩展阅读：
>>>[文件部分扩展阅读](https://python3-cookbook.readthedocs.io/zh_CN/latest/chapters/p05_files_and_io.html)

