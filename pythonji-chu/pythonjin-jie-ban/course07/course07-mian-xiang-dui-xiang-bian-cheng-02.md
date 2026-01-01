# \[course]07 —— 面向对象编程02

## 1. **Writing Classes**

```python
# Create our own class:
class Dog(object):
    # a class must have a body, even if it does nothing, so we will
    # use 'pass' for now...
    pass

# Create instances of our class:
d1 = Dog()
d2 = Dog()

# Verify the type of these instances:
print(type(d1))             # Dog (actually, class '__main__.Dog')
print(isinstance(d2, Dog))  # True

# Set and get properties (aka 'fields' or 'attributes') of these instances:
d1.name = 'Dot'
d1.age = 4
d2.name = 'Elf'
d2.age = 3
print(d1.name, d1.age) # Dot 4
print(d2.name, d2.age) # Elf 3
```

## 2. **Writing Constructors**

* Constructors let us pre-load our new instances with properties.
* This lets us write code like so:

```python
d1 = Dog('fred', 4) # now d1 is a Dog instance with name 'fred' and age 4
```

* We would like to write our constructor like this:

```python
def constructor(dog, name, age):
    # pre-load the dog instance with the given name and age:
    dog.name = name
    dog.age = age
```

* Unfortunately, Python does not use 'constructor' as the constructor name. Instead, it uses '**init**' (sorry about that), like so:

```python
def __init__(dog, name, age):
    # pre-load the dog instance with the given name and age:
    dog.name = name
    dog.age = age
```

* Also, unfortunately, while we could name the instance 'dog' like we did, standard convention requires that we name it 'self' (sorry again), like so:

```python
def __init__(self, name, age):
    # pre-load the dog instance with the given name and age:
    self.name = name
    self.age = age
```

* Finally, we place this method inside the class and we have a constructor that we can use, like so:

```python
class Dog(object):
    def __init__(self, name, age):
        # pre-load the dog instance with the given name and age:
        self.name = name
        self.age = age

# Create instances of our class, using our new constructor
d1 = Dog('Dot', 4)
d2 = Dog('Elf', 3)

print(d1.name, d1.age) # Dot 4
print(d2.name, d2.age) # Elf 3
```

## 5. **Writing Methods**

* Start with a function:

```python
class Dog(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Here is a function we will turn into a method:
def sayHi(dog):
    print(f'Hi, my name is {dog.name} and I am {dog.age} years old!')

d1 = Dog('Dot', 4)
d2 = Dog('Elf', 3)

sayHi(d1) # Hi, my name is Dot and I am 4 years old!
sayHi(d2) # Hi, my name is Elf and I am 3 years old!
```

* Turn the function into a method, and the function call into a method call, like this:

```python
class Dog(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # Now it is a method (simply by indenting it inside the class!)
    def sayHi(dog):
        print(f'Hi, my name is {dog.name} and I am {dog.age} years old!')

d1 = Dog('Dot', 4)
d2 = Dog('Elf', 3)

# Notice how we change the function calls into method calls:

d1.sayHi() # Hi, my name is Dot and I am 4 years old!
d2.sayHi() # Hi, my name is Elf and I am 3 years old!
```

* Finally, use `self`, as convention requires:

```python
class Dog(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # Now we are using self, as convention requires:
    def sayHi(self):
        print(f'Hi, my name is {self.name} and I am {self.age} years old!')

d1 = Dog('Dot', 4)
d2 = Dog('Elf', 3)

# Notice how we change the function calls into method calls:

d1.sayHi() # Hi, my name is Dot and I am 4 years old!
d2.sayHi() # Hi, my name is Elf and I am 3 years old!
```

* Methods can take additional parameters, like so:

```python
class Dog(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # This method takes a second parameter -- times
    def bark(self, times):
        print(f'{self.name} says: {"woof!" * times}')

d = Dog('Dot', 4)

d.bark(1) # Dot says: woof!
d.bark(4) # Dot says: woof!woof!woof!woof!
```

* Methods can also set properties, like so:

```python
class Dog(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.woofCount = 0   # we initialize the property in the constructor!

    def bark(self, times):
        # Then we can set and get the property in this method
        self.woofCount += times
        print(f'{self.name} says: {"woof!" * times} ({self.woofCount} woofs!)')

d = Dog('Dot', 4)

d.bark(1) # Dot says: woof!
d.bark(4) # Dot says: woof!woof!woof!woof!
```

## 6. **Advantages of Classes and Methods**

* **Encapsulation**
  *   **Organizes code**

      &#x20; A class includes the data and methods for that class.
  *   **Promotes intuitive design**

      &#x20; Well-designed classes should be _intuitive_, so the data and methods in the class match commonsense expectations.
  * **Restricts access**
    * `len` is a function, so we can call `len(True)` (which crashes)
    * `upper` is a method on strings but not booleans, so we cannot even call `True.upper()`
*   **Polymorphism**

    &#x20; Polymorphism: the same method name can run different code based on type, like so:

```python
class Dog(object):
    def speak(self):
        print('woof!')

class Cat(object):
    def speak(self):
        print('meow!')

for animal in [ Dog(), Cat() ]:
    animal.speak() # same method name, but one woofs and one meows!
```
