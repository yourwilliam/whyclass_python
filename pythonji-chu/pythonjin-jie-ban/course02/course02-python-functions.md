# \[course\]02 —— Python Functions

函数定义后是否执行？

空函数的定义方法 pass的使用

函数的返回值？ 什么是函数的返回值

函数的返回值可以包含多个值

> EX18

```python
# this one is like your scripts with argv


def print_two(*args):
    print(args)
    *arg1, arg2 = args
    print(f"arg1: {arg1}, arg2: {arg2} ")


# ok, that *args is actually pointless, we can just do this
def print_two_again(arg1, arg2="333"):
    print(f"arg1: {arg1}, arg2: %{arg2}")


# this just takes one argument
def print_one(arg1):
    print(f"arg1: {arg1}")


# this one takes no arguments
def print_none():
    print("I got nothing.")


print_two("Zed", "Shaw")
print_two_again("Zed", "Shaw")
print_one("First!")
print_none()
```

> EX21

```python
def add(a, b):
    print("ADDING %d + %d" % (a, b))
    return a + b


def complex_print(a, b):
    return a + b, a - b, a * b, a / b


def subtract(a, b):
    print("SUBTRACTING %d - %d" % (a, b))
    return a - b


def multiply(a, b):
    print("MULTIPLYING %d * %d" % (a, b))
    return a * b


def divide(a, b):
    print("DIVIDING %d / %d" % (a, b))
    return a / b


print("Let's do some math with just functions!")

age = add(30, 5)
c1,c2,c3,c4 = complex_print(30, 5)
print(f"{c1},{c2},{c3},{c4}")

height = subtract(78, 4)
weight = multiply(90, 2)
iq = divide(100, 2)

print("Age: %d, Height: %d, Weight: %d, IQ: %d" % (age, height, weight, iq))

# A puzzle for the extra credit, type it in anyway.
print("Here is a puzzle.")

what = add(age, subtract(height, multiply(weight, divide(iq, 2))))

bmi = divide(weight, multiply(height, height))

print("That becomes: ", what, "Can you do it by hand?")
```

### 方法的参数，方法可以有多个参数，也可以不带参数

```python
def f(x, y, z):
    return x + y + z

print(f(1, 3, 2)) # returns 6

def g():
    return 42

print(g()) # returns 42

# Note - the number of arguments provided must match the number of parameters!
print(g(2)) # will crash
print(f(1, 2)) # would also crash if it ran
```

### Builtin Functions

```python
# Some functions are already provided by Python

print("Type conversion functions:")
print(bool(0))   # convert to boolean (True or False)
print(float(42)) # convert to a floating point number
print(int(2.8))  # convert to an integer (int)

print("And some basic math functions:")
print(abs(-5))   # absolute value
print(max(2,3))  # return the max value
print(min(2,3))  # return the min value
print(pow(2,3))  # raise to the given power (pow(x,y) == x**y)
print(round(2.354, 1)) # round with the given number of digits
```

### Module Functions

```python
import math
print(math.factorial(20))  # much better...

# Note that the module name is included before the function name, separated by a .
```

### Variable Scope

外部不能访问在方法内部声明的变量

```python
def f(x):
    print("x:", x)
    y = 5
    print("y:", y)
    return x + y
print(f(4))
print(x) # will crash!
print(y) # would also crash if we reached it!
```

在方法内部定义的变量只能在方法内部使用，它的作用域仅存在于方法内部

```python
def f(x):
    print("In f, x =", x)
    x += 5
    return x

def g(x):
    y = f(x*2)
    print("In g, x =", x)
    z = f(x*3)
    print("In g, x =", x)
    return y + z

print(g(2))

# Another example

def f(x):
    print("In f, x =", x)
    x += 7
    return round(x / 3)

def g(x):
    x *= 10
    return 2 * f(x)

def h(x):
    x += 3
    return f(x+4) + g(x)

print(h(f(1)))
```

在方法外定义的变量\(global scope\)，可以在多个方法中共享

```python
# In general, you should avoid using global variables.
# You will even lose style points if you use them!
# Still, you need to understand how they work, since others
# will use them, and there may also be some very few occasions
# where you should use them, too!

g = 100

def f(x):
    return x + g

print(f(5)) # 105
print(f(6)) # 106
print(g)    # 100

# Another example

def f(x):
    # If we modify a global variable, we must declare it as global.
    # Otherwise, Python will assume it is a local variable.
    global g
    g += 1
    return x + g

print(f(5)) # 106
print(f(6)) # 108
print(g)    # 102
```

### 方法的返回值

基本返回值

```python
def isPositive(x):
    return (x > 0)

print(isPositive(5))  # True
print(isPositive(-5)) # False
print(isPositive(0))  # False
```

方法return之后，方法直接退出，不会执行后续流程

```python
def isPositive(x):
    print("Hello!")   # runs
    return (x > 0)
    print("Goodbye!") # does not run ("dead code")

print(isPositive(5))  # prints Hello, then True
```

方法如果没有return，默认会返回None

```python
def f(x):
    x + 42

print(f(5)) # None
```

```python
def f(x):
    result = x + 42

print(f(5)) # None
```

## 下面是作业中会用到的部分

### 方法组合

在方法内可以调用其他的方法，从而形成方法的组合

```python
def f(w):
    return 10*w

def g(x, y):
    return f(3*x) + y

def h(z):
    return f(g(z, f(z+1)))

print(h(1)) # hint: try the "visualize" feature
```

### Helper Functions

```python
# We commonly write functions to solve problems.
# We can also write functions to store an action that is used multiple times!
# These are called helper functions.

def onesDigit(n):
    return n%10

def largerOnesDigit(x, y):
    return max(onesDigit(x), onesDigit(y))

print(largerOnesDigit(134, 672)) # 4
print(largerOnesDigit(132, 674)) # Still 4
```

### 作业中出现的方法，帮助使用的

```python
# There are a few functions from modules you'll definitely want to use in the assignments

# First: the built-in round function has confusing behavior when rounding 0.5.
# Use our function roundHalfUp to fix this.

def roundHalfUp(d):
    # Round to nearest with ties going away from zero.
    # You do not need to understand how this function works.
    import decimal
    rounding = decimal.ROUND_HALF_UP
    return int(decimal.Decimal(d).to_integral_value(rounding=rounding))

print(round(0.5)) # This evaluates to 0 - what!
print(round(1.5)) # And this will be 2 - so confusing!
print(roundHalfUp(0.5)) # Now this will always round 0.5 up (to 1)
print(roundHalfUp(1.5)) # This still rounds up too!

# Second: when comparing floats, == doesn't work quite right.
# Use almostEqual to compare floats instead

print(0.1 + 0.1 == 0.2) # True, but...
d1 = 0.1 + 0.1 + 0.1
d2 = 0.3
print(d1 == d2) # False!
print(d1)       # prints 0.30000000000000004 (uh oh)
print(d1 - d2)  # prints 5.55111512313e-17 (tiny, but non-zero!)
# Moral: never use == with floats!

# Python includes a builtin function math.isclose(), but that function
# has some confusing behavior when comparing values close to 0.
# Instead, let's just make our own version of isclose:

def almostEqual(x, y):
    return abs(x - y) < 10**-9

# This will now work properly!
print(almostEqual(0, 0.0000000000001))
print(almostEqual(d1, d2))
```

### 测试方法

出现错误的用例

```python
def onesDigit(n):
    return n%10

def testOnesDigit():
    print("Testing onesDigit()...", end="")
    assert(onesDigit(5) == 5)
    assert(onesDigit(123) == 3)
    assert(onesDigit(100) == 0)
    assert(onesDigit(999) == 9)
    print("Passed!")

testOnesDigit() # Passed!  Why is this bad?
```

正确的用例版本

```python
def onesDigit(n):
    return n%10

def testOnesDigit():
    print("Testing onesDigit()...", end="")
    assert(onesDigit(5) == 5)
    assert(onesDigit(123) == 3)
    assert(onesDigit(100) == 0)
    assert(onesDigit(999) == 9)
    assert(onesDigit(-123) == 3) # Added this test
    print("Passed!")

testOnesDigit() # Crashed!  So the test function worked!
```

## 函数的扩充阅读和讲解

## 函数的定义

函数定义后是否执行？

空函数的定义方法 pass的使用

函数的返回值？ 什么是函数的返回值

函数的返回值可以包含多个值

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的新的坐标：

```python
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
import math语句表示导入math包，并允许后续代码引用math包里的sin、cos等函数。
```

然后，我们就可以同时获得返回值：

```python
>>> x, y = move(100, 100, 60, math.pi / 6)
>>> print(x, y)
151.96152422706632 70.0
```

但其实这只是一种假象，Python函数返回的仍然是单一值：

```python
>>> r = move(100, 100, 60, math.pi / 6)
>>> print(r)
(151.96152422706632, 70.0)
```

原来返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

## 函数的调用

## 函数的参数

### 默认参数

使用=定义默认参数

```python
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```

### 可变参数

```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

### 关键字参数

```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```

### 可变参数

在Python函数中，还可以定义可变参数。顾名思义，可变参数就是传入的参数个数是可变的，可以是1个、2个到任意个，还可以是0个。

我们以数学题为例子，给定一组数字a，b，c……，请计算a2 + b2 + c2 + ……。

要定义出这个函数，我们必须确定输入的参数。由于参数个数不确定，我们首先想到可以把a，b，c……作为一个list或tuple传进来，这样，函数可以定义如下：

```text
def calc(numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

但是调用的时候，需要先组装出一个list或tuple：

```text
>>> calc([1, 2, 3])
14
>>> calc((1, 3, 5, 7))
84
```

如果利用可变参数，调用函数的方式可以简化成这样：

```text
>>> calc(1, 2, 3)
14
>>> calc(1, 3, 5, 7)
84
```

所以，我们把函数的参数改为可变参数：

```text
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`号。在函数内部，参数`numbers`接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数：

```text
>>> calc(1, 2)
5
>>> calc()
0
```

如果已经有一个list或者tuple，要调用一个可变参数怎么办？可以这样做：

```text
>>> nums = [1, 2, 3]
>>> calc(nums[0], nums[1], nums[2])
14
```

这种写法当然是可行的，问题是太繁琐，所以Python允许你在list或tuple前面加一个`*`号，把list或tuple的元素变成可变参数传进去：

```text
>>> nums = [1, 2, 3]
>>> calc(*nums)
14
```

`*nums`表示把`nums`这个list的所有元素作为可变参数传进去。这种写法相当有用，而且很常见。

### 关键字参数

可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。请看示例：

```text
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```

函数`person`除了必选参数`name`和`age`外，还接受关键字参数`kw`。在调用该函数时，可以只传入必选参数：

```text
>>> person('Michael', 30)
name: Michael age: 30 other: {}
```

也可以传入任意个数的关键字参数：

```text
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```

关键字参数有什么用？它可以扩展函数的功能。比如，在`person`函数里，我们保证能接收到`name`和`age`这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。

和可变参数类似，也可以先组装出一个dict，然后，把该dict转换为关键字参数传进去：

```text
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, city=extra['city'], job=extra['job'])
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

当然，上面复杂的调用可以用简化的写法：

```text
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

`**extra`表示把`extra`这个dict的所有key-value用关键字参数传入到函数的`**kw`参数，`kw`将获得一个dict，注意`kw`获得的dict是`extra`的一份拷贝，对`kw`的改动不会影响到函数外的`extra`。

### 命名关键字参数

对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。至于到底传入了哪些，就需要在函数内部通过`kw`检查。

仍以`person()`函数为例，我们希望检查是否有`city`和`job`参数：

```text
def person(name, age, **kw):
    if 'city' in kw:
        # 有city参数
        pass
    if 'job' in kw:
        # 有job参数
        pass
    print('name:', name, 'age:', age, 'other:', kw)
```

但是调用者仍可以传入不受限制的关键字参数：

```text
>>> person('Jack', 24, city='Beijing', addr='Chaoyang', zipcode=123456)
```

如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收`city`和`job`作为关键字参数。这种方式定义的函数如下：

```text
def person(name, age, *, city, job):
    print(name, age, city, job)
```

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

调用方式如下：

```text
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`了：

```text
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错：

```text
>>> person('Jack', 24, 'Beijing', 'Engineer')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: person() takes 2 positional arguments but 4 were given
```

由于调用时缺少参数名`city`和`job`，Python解释器把这4个参数均视为位置参数，但`person()`函数仅接受2个位置参数。

命名关键字参数可以有缺省值，从而简化调用：

```text
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
```

由于命名关键字参数`city`具有默认值，调用时，可不传入`city`参数：

```text
>>> person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer
```

使用命名关键字参数时，要特别注意，如果没有可变参数，就必须加一个`*`作为特殊分隔符。如果缺少`*`，Python解释器将无法识别位置参数和命名关键字参数：

```text
def person(name, age, city, job):
    # 缺少 *，city和job被视为位置参数
    pass
```

### 参数组合

在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。

比如定义一个函数，包含上述若干种参数：

```text
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
```

在函数调用的时候，Python解释器自动按照参数位置和参数名把对应的参数传进去。

```text
>>> f1(1, 2)
a = 1 b = 2 c = 0 args = () kw = {}
>>> f1(1, 2, c=3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> f1(1, 2, 3, 'a', 'b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
>>> f2(1, 2, d=99, ext=None)
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None}
```

最神奇的是通过一个tuple和dict，你也可以调用上述函数：

```text
>>> args = (1, 2, 3, 4)
>>> kw = {'d': 99, 'x': '#'}
>>> f1(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': '#'}
>>> args = (1, 2, 3)
>>> kw = {'d': 88, 'x': '#'}
>>> f2(*args, **kw)
a = 1 b = 2 c = 3 d = 88 kw = {'x': '#'}
```

所以，对于任意函数，都可以通过类似`func(*args, **kw)`的形式调用它，无论它的参数是如何定义的。

虽然可以组合多达5种参数，但不要同时使用太多的组合，否则函数接口的可理解性很差。

> > > 阅读文档: [廖雪峰的python教程，整个函数部分](https://www.liaoxuefeng.com/wiki/1016959663602400/1017105145133280) [python3-cockbook第七章函数](https://python3-cookbook.readthedocs.io/zh_CN/latest/c07/p01_functions_that_accept_any_number_arguments.html)

