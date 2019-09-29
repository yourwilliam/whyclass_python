# [course] 02 —— Python基础

## Python 基础

### Print

```py
print("hello world!")

```

### Comments and pond characters

```py
# A comment, this is so you can read your program later. # Anything after the # is ignored by python.

print("I could have code like this.") # and the comment after is ignored

# You can also use a comment to "disable" or comment out code: # print("This won't run.")

print("This will run.")
```

### Numbers and Math

```py
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

#### Importing Modules

```py
import math
print(math.factorial(20))
```

导入math模块计算计算阶层

#### Builtin Types 内置类型

```py

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

```py
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


| Category | Operators |
| --- | --- |
| Arithmetic | +, -, *, /, //, **, %, - (unary), + (unary) |
| Relational | <, <=, >=, >, ==, != |
| Assignment | +=, -=, *=, /=, //=, **=, %=, <<=, >>= |
| Logical | and, or, not |

#### Division 除法和整除

```py
print("The / operator does 'normal' float division:")
print(" 5/3  =", ( 5/3))
print()
print("The // operator does integer division:")
print(" 5//3 =", ( 5//3))
print(" 2//3 =", ( 2//3))
print("-1//3 =", (-1//3))
print("-4//3 =", (-4//3))
```

#### The Modulus or Remainder Operator (%) 余数/模

```py
print(" 6%3 =", ( 6%3))
print(" 5%3 =", ( 5%3))
print(" 2%3 =", ( 2%3))
print(" 0%3 =", ( 0%3))
print("-4%3 =", (-4%3))
print(" 3%0 =", ( 3%0))
```

#### Types Affect Semantics

```py
print(3 * 2)
print(3 * "abc")
print(3 + 2)
print("abc" + "def")
print(3 + "def")
```

#### Approximate Values of Floating-Point Numbers

```py
print(0.1 + 0.1 == 0.2)        # True, but...
print(0.1 + 0.1 + 0.1 == 0.3)  # False!
print(0.1 + 0.1 + 0.1)         # prints 0.30000000000000004 (uh oh)
print((0.1 + 0.1 + 0.1) - 0.3) # prints 5.55111512313e-17 (tiny, but non-zero!)
```

#### Equality Testing with almostEqual:

```py
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



###Variables and Names, Format String

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

Format String

### Format String 

