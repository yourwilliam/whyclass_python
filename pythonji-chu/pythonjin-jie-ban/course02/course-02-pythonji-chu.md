# \[course] 02 —— Python基础

## Python 基础

### Print

```python
print("hello world!")
```

### Comments and pond characters

> EX02

两种注释方法，`#`注释和`"""`注释

`#`用于单行注释

`"""`用于三行注释

```python
# A comment, this is so you can read your program later. # Anything after the # is ignored by python.

print("I could have code like this.") # and the comment after is ignored

# You can also use a comment to "disable" or comment out code: # print("This won't run.")

print("This will run.")
```

### Numbers and Math

> (EX03)

```python
print("I will now count my chickens:")

print("Hens", 25 + 30 / 6) 
print("Roosters", 100 - 25 * 3 % 4) 
print("Now I will count the eggs:") 
print(3 + 2 + 1 - 5 + 4 % 2 - 1 / 4 + 6) 
print("Is it true that 3 + 2 < 5 - 7?") 
print(3 + 2 < 5 - 7) 
print("What is 3 + 2?", 3 + 2) 
print("What is 5 - 7?", 5 - 7) 
print("Oh, that's why it's False.")

print("How about some more.")

print("Is it greater?", 5 > -2) 
print("Is it greater or equal?", 5 >= -2) 
print("Is it less or equal?", 5 <= -2)
```

#### 除法

`/`和`//` python3 对于两个整数相除，默认使用会变为浮点型

```python
print("The / operator does 'normal' float division:")
print(" 5/3  =", ( 5/3))
print()
print("The // operator does integer division:")
print(" 5//3 =", ( 5//3))
print(" 2//3 =", ( 2//3))
print("-1//3 =", (-1//3))
print("-4//3 =", (-4//3))
```

**X / Y类型：**

在Python2.6或者之前，这个操作对于整数运算会省去小数部分，而对于浮点数运算会保持小数部分；在Python3.0中变成真除法（无论任何类型都会保持小数部分，即使整除也会表示为浮点数形式）。

**X // Y 类型：**

Floor除法：在Python 2.2中新增的操作，在Python2.6和Python3.0中均能使用，这个操作不考虑操作对象的类型，总是省略小数部分，剩下最小的能整除的整数部分。 Floor除法：效果等同于math模块中的floor函数： math.floor(x) ：返回不大于x的整数 所以当运算数是负数时：结果会向下取整。

```python
>>> 5//3   #1.6666666666666667
1
>>> -5//3
-2
```

#### The Modulus or Remainder Operator (%) 余数/模

```python
print(" 6%3 =", ( 6%3))
print(" 5%3 =", ( 5%3))
print(" 2%3 =", ( 2%3))
print(" 0%3 =", ( 0%3))
print("-4%3 =", (-4%3))
print(" 3%0 =", ( 3%0))
```

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

#### 浮点数计算相等

```python
print(0.1 + 0.1 == 0.2)        # True, but...
print(0.1 + 0.1 + 0.1 == 0.3)  # False!
print(0.1 + 0.1 + 0.1)         # prints 0.30000000000000004 (uh oh)
print((0.1 + 0.1 + 0.1) - 0.3) # prints 5.55111512313e-17 (tiny, but non-zero!)
```

#### 浮点数近似相等计算方式：

```python
print("The problem....")
d1 = 0.1 + 0.1 + 0.1
d2 = 0.3
print(d1 == d2)                # False (never use == with floats!)

print()
print("The solution...")
epsilon = 10**-10
print(abs(d2 - d1) < epsilon)  # True!

print()
print("Once again, using a useful helper function, almostEqual:")

def almostEqual(d1, d2):
    epsilon = 10**-10
    return (abs(d2 - d1) < epsilon)

d1 = 0.1 + 0.1 + 0.1
d2 = 0.3
print(d1 == d2)            # still False, of course
print(almostEqual(d1, d2)) # True, and now packaged in a handy reusable function!
```

#### Importing Modules

```python
import math
print(math.factorial(20))
```

导入math模块计算计算阶层

#### Builtin Types 内置类型

基本数据类型和container类型

```python
import math
def f():
    print("This is a user-defined function")
    return 42

print("Some basic types in Python:")
print(type(2))           # int
print(type(2.2))         # float
print(type(2 < 2.2))     # bool (boolean)
print(type(type(42)))    # type

print("#####################################################")

print("And some other types we may see later in the course...")
print(type("2.2"))       # str (string or text)
print(type([1,2,3]))     # list
print(type((1,2,3)))     # tuple
print(type({1,2}))       # set
print(type({1:42}))      # dict (dictionary or map)
print(type(2+3j))        # complex  (complex number)
```

#### Builtin Constants 内置常量

```python
print("Some builtin constants:")
print(True)
print(False)
print(None)

print("And some more constants in the math module:")
import math
print(math.pi)
print(math.e)
```

#### Builtin Operators 内置运算符

| Category   | Operators                                    |
| ---------- | -------------------------------------------- |
| Arithmetic | +, -, _, /, //, \*_, %, - (unary), + (unary) |
| Relational | <, <=, >=, >, ==, !=                         |
| Assignment | +=, -=, _=, /=, //=, \*_=, %=, <<=, >>=      |
| Logical    | and, or, not                                 |

#### 类型将会影响计算方式

为什么我们要强调python中的Types数据类型，因为不同的类型使用方法不同，将会决定我们的计算方式。

```python
print(3 * 2)
print(3 * "abc")
print(3 + 2)
print("abc" + "def")
print(3 + "def")
```
