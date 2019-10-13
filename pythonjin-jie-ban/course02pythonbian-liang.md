# [course]02——Python变量

###Variables and Names, Format String

> EX04

```py
cars = 100 
space_in_a_car = 4.0 
drivers = 30 
passengers = 90 
cars_not_driven = cars - drivers 
cars_driven = drivers 
carpool_capacity = cars_driven * space_in_a_car average_passengers_per_car = passengers / cars_driven

print("There are", cars, "cars available.") 
print("There are only", drivers, "drivers available.") 
print("There will be", cars_not_driven, "empty cars today.") 
print("We can transport", carpool_capacity, "people today.") 
print("We have", passengers, "to carpool today.") 
print("We need to put about", average_passengers_per_car, "in each car.")

print(f"Let's talk about {my_name}.") 
print(f"He's {my_height} inches tall.")
total = my_age + my_height + my_weight 
print(f"If I add {my_age}, {my_height}, and {my_weight} I get {total}.")
```

什么是变量

Python中的变量：

[python 变量在内存中的表示（变量赋值误区）](https://blog.csdn.net/yj928674542/article/details/76269531)
[图解Python变量与赋值](https://foofish.net/python-variable.html)
下面这个以后看
[python基础（5）：深入理解 python 中的赋值、引用、拷贝、作用域](https://my.oschina.net/leejun2005/blog/145911)

### 变量的命名规则

变量的命名规则 —— 请查看python cheatsheet

1、模块
模块尽量使用小写命名，首字母保持小写，尽量不要用下划线(除非多个单词，且数量不多的情况)

```py
# 正确的模块名
import decoder
import html_parser

# 不推荐的模块名
import Decoder
```

2、类名
类名使用驼峰(CamelCase)命名风格，首字母大写，私有类可用一个下划线开头

```py
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

```py
def run():
    pass

def run_with_env():
    pass
```

私有函数在函数前加一个下划线_

```
class Person():

    def _private_func():
        pass
```

4、变量名

变量名尽量小写, 如有多个单词，用下划线隔开

```py
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

### 格式化字符串

#### python3的格式化字符串

```py
print('My name is {name}.'.format(name = name))

# 即便是简化的版本
print('My name is {}.'.format(name))
```

#### python3.6提供的格式化字符串方法

```py
>>> name = "Tom"
>>> age = 3
>>> f"His name is {name}, he's {age} years old."
>>> "His name is Tom, he's 3 years old."
```

更细节的格式化字符串参考

[python3 f-string格式化字符串的高级用法](https://mlln.cn/2018/05/19/python3%20f-string%E6%A0%BC%E5%BC%8F%E5%8C%96%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95/)
上面这篇一定要看一下

[Python3.6新的字符串格式化语法](https://imliyan.com/blogs/article/Python3.6%E6%96%B0%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%A0%BC%E5%BC%8F%E5%8C%96%E8%AF%AD%E6%B3%95/)

