# \[course\]07 —— 面向对象编程 01

## 1. **Methods vs Functions**

We call methods using s.f\(\) rather than f\(s\):

```python
s = 'This could be any string!'

print(len(s))     # len is a function

print(s.upper())  # upper is a string method, called using the . notation
                  # we say that we "call the method len on the string s"

print(s.replace('could', 'may')) # some methods take additional arguments
```

See how we get different errors for improperly calling methods vs functions:

```python
n = 123
print(len(n))    # TypeError: object of type 'int' has no len()
                 # This means that len() cannot work properly with int's

n = 123
print(n.upper()) # AttributeError: 'int' object has no attribute 'upper'
                 # This means that there is no method upper() for int's
```

## 2. **Classes and Instances**

* Classes are also called "Types" in Python.
  * For example, these are classes: int, float, str, bool
* Instances are values of a given class or type.
  * For example: 'abc' is a str instance \(also called a string\)

## 3. **Objects and Object-Oriented Programming \(OOP\)**

* Every value in Python is an Object.
  * Every instance is an object, and its type is some class.
  * Every class is an object, too \(its type is **type**!\).
* That is why we call this Object-Oriented Programming
  * We are using objects only a little bit now.
  * Soon we will write our own classes.
  * Then we will add some sophistication to how we write and use classes and objects.
  * Even so, because we are using objects now, **we are already using Object-Oriented Programming \(OOP\)**.

