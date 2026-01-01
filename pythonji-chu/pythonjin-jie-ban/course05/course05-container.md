# \[course]05 —— container

## 1. **Creating Lists**

### **Empty List**

```python
print("Two standard ways to create an empty list:")
a = [ ]
b = list()

print(type(a), len(a), a)
print(type(b), len(b), b)
print(a == b)
```

### **List with One Element (Singleton)**

```python
a = [ "hello" ]
b = [ 42 ]

print(type(a), len(a), a)
print(type(b), len(b), b)
print(a == b)
```

### **List with Multiple Elements**

```python
a = [2, 3, 5, 7]
b = list(range(5))
c = ["mixed types", True, 42]

print(type(a), len(a), a)
print(type(b), len(b), b)
print(type(c), len(c), c)
```

### **Variable-Length List**

```python
n = 10
a = [0] * n # creates a list with n 0s
b = list(range(n))

print(type(a), len(a), a)
print(type(b), len(b), b)
```

## 2. **List Functions and Operations**

```python
a = [ 2, 3, 5, 2 ]
print("a = ", a)
print("len =", len(a))
print("min =", min(a))
print("max =", max(a))
print("sum =", sum(a))

# Create some lists
a = [ 2, 3, 5, 3, 7 ]
b = [ 2, 3, 5, 3, 7 ]   # same as a
c = [ 2, 3, 5, 3, 8 ]   # differs in last element
d = [ 2, 3, 5 ]         # prefix of a

print("a =", a)
print("b =", b)
print("c =", c)
print("d =", d)

print("------------------")
print("a == b", (a == b))
print("a == c", (a == c))
print("a != b", (a != b))
print("a != c", (a != c))

print("------------------")
print("a < c", (a < c))
print("a < d", (a < d))
```

### 3. **Accessing Elements (Indexing and Slicing)**

```python
# Indexing and slicing for lists works the same way as it did for strings!

a = [2, 3, 5, 7, 11, 13]
print("a        =", a)

# Access non-negative indexes
print("a[0]     =", a[0])
print("a[2]     =", a[2])

# Access negative indexes
print("a[-1]    =", a[-1])
print("a[-3]    =", a[-3])

# Access slices a[start:end:step]
print("a[0:2]   =", a[0:2])
print("a[1:4]   =", a[1:4])
print("a[1:6:2] =", a[1:6:2])
```

### 4. **List Mutability and Aliasing**

Unlike strings, lists are **mutable**. This means that they can be changed, without creating a new list. This also forces us to better understand **aliases**, when two variables reference the same value. Aliases are only interesting (and challenging) for mutable values like lists. **Note:** it will be especially helpful to use the Visualize feature in the following examples.

#### **Example:**

```python
# Create a list
a = [ 2, 3, 5, 7 ]

# Create an alias to the list
b = a

# We now have two references (aliases) to the SAME list
a[0] = 42
b[1] = 99
print(a)
print(b)
```

#### **Function Parameters are Aliases:**

```python
def f(a):
    a[0] = 42
a = [2, 3, 5, 7]
f(a)
print(a)

# Note that the parameter alias can still be broken by re-assigning the variable

a = [3, 2, 1]

def foo(a):
     a[0] = 1
     a = [5, 2, 0] # we break the alias here!
     a[0] = 4

foo(a)
print(a)
```

#### **Another Example:**

```python
# Create a list
a = [ 2, 3, 5, 7 ]

# Create an alias to the list
b = a

# Create a different list with the same elements
c = [ 2, 3, 5, 7 ]

# a and b are references (aliases) to the SAME list
# c is a reference to a different but EQUAL list

print("initially:")
print("  a==b  :", a==b)
print("  a==c  :", a==c)
print("  a is b:", a is b) # the is operation tells if two values are aliases, or basic datatypes
print("  a is c:", a is c)

# Now changes to a also change b (the SAME list) but not c (a different list)
a[0] = 42
print("After changing a[0] to 42")
print("  a=", a)
print("  b=", b)
print("  c=", c)
print("  a==b  :", a==b)
print("  a==c  :", a==c)
print("  a is b:", a is b)
print("  a is c:", a is c)
```

### 5. **Copying Lists**

#### **Copy vs Alias**

```python
# Because of aliasing, we have to be careful if we share a reference
# to a list in the same way we might for number or a string,
# by simply setting b = a, like so:

import copy

# Create a list
a = [ 2, 3 ]

# Try to copy it
b = a             # Error!  Not a copy, but an alias
c = copy.copy(a)  # Ok

# At first, things seem ok
print("At first...")
print("   a =", a)
print("   b =", b)
print("   c =", c)

# Now modify a[0]
a[0] = 42
print("But after a[0] = 42")
print("   a =", a)
print("   b =", b)
print("   c =", c)
```

#### **Other ways to copy**

```python
import copy

a = [2, 3]

b = copy.copy(a)
c = a[:]
d = a + [ ]
e = list(a)

a[0] = 42
print(a, b, c, d, e)
```

### 6. **Destructive and Non-destructive Functions**

Because lists are mutable, we can change them in two ways: **destructively** (which modifies the original value directly), and **non-destructively** (which creates a new list and does not modify the original value). This also affects how we write functions that use lists.

#### **Destructive functions**

```
# A destructive function is written to directly change the provided list
# It does not need to return anything, as the caller can access the original list
def fill(a, value):
    for i in range(len(a)):
        a[i] = value

a = [1, 2, 3, 4, 5]
print("At first, a =", a)
fill(a, 42)
print("After fill(a, 42), a =", a)
```

#### **Non-destructive function**

```python
import copy

## First, a quick primer on modifying lists ##
## We'll talk about these more in a bit ##

a = [1, 2, 3, 4]

# .remove() DESTRUCTIVELY removes the given value from the list
a.remove(2)
print(a) # [1, 3, 4]

# .append() DESTRUCTIVELY adds the given value to the end of the list
a.append(70)
print(a) # [1, 3, 4, 70]

## Now, on to NON-DESTRUCTIVE functions! ##

def destructiveRemoveAll(a, value):
    while (value in a):
        a.remove(value)

def nonDestructiveRemoveAll(a, value):
    # Typically, we write non-destructive functions by building a new list
    # instead of changing the original
    result = []
    for element in a:
        if (element != value):
            result.append(element)
    return result # non-destructive functions still need to return!

def alternateNonDestructiveRemoveAll(a, value):
    # We can write the same function by breaking the alias,
    # then using the destructive approach
    a = copy.copy(a)
    destructiveRemoveAll(a, value)
    return a

a = [ 1, 2, 3, 4, 3, 2, 1 ]
print("At first")
print("   a =", a)

destructiveRemoveAll(a, 2)
print("After destructiveRemoveAll(a, 2)")
print("   a =", a)

b = nonDestructiveRemoveAll(a, 3)
print("After b = nonDestructiveRemoveAll(a, 3)")
print("   a =", a)
print("   b =", b)

c = alternateNonDestructiveRemoveAll(a, 1)
print("After c = alternateNonDestructiveRemoveAll(a, 1)")
print("   a =", a)
print("   c =", c)
```

### 7. **Finding Elements**

#### **Check for list membership: in**

```
a = [ 2, 3, 5, 2, 6, 2, 2, 7 ]
print("a      =", a)
print("2 in a =", (2 in a))
print("4 in a =", (4 in a))
```

#### **Check for list non-membership: not in**

```
a = [ 2, 3, 5, 2, 6, 2, 2, 7 ]
print("a          =", a)
print("2 not in a =", (2 not in a))
print("4 not in a =", (4 not in a))
```

#### **Count occurrences in list: list.count(item)**

```
a = [ 2, 3, 5, 2, 6, 2, 2, 7 ]
print("a          =", a)
print("a.count(1) =", a.count(1))
print("a.count(2) =", a.count(2))
print("a.count(3) =", a.count(3))
```

#### **Find index of item: list.index(item) and list.index(item, start)**

**Example**

```
a = [ 2, 3, 5, 2, 6, 2, 2, 7 ]
print("a            =", a)
print("a.index(6)   =", a.index(6))
print("a.index(2)   =", a.index(2))
print("a.index(2,1) =", a.index(2,1))
print("a.index(2,4) =", a.index(2,4))
```

**Problem: crashes when item is not in list**

```
a = [ 2, 3, 5, 2 ]
print("a          =", a)
print("a.index(9) =", a.index(9)) # crashes!
print("This line will not run!")
```

**Solution: use (item in list)**

```
a = [ 2, 3, 5, 2 ]
print("a =", a)
if (9 in a):
    print("a.index(9) =", a.index(9))
else:
    print("9 not in", a)
print("This line will run now!")
```

### 8. **Adding Elements**   video

#### **Destructively (Modifying Lists)**

**Add an item with list.append(item)**

```python
a = [ 2, 3 ]
a.append(7)
print(a)
```

**Add a list of items with list += list2 or list.extend(list2)**

```python
a = [ 2, 3 ]
a += [ 11, 13 ]
print(a)
a.extend([ 17, 19 ])
print(a)
```

**Insert an item at a given index**

```python
a = [ 2, 3, 5, 7, 11 ]
a.insert(2, 42)  # at index 2, insert 42
print(a)
```

#### **Non-Destructively (Creating New Lists)**

**Add an item with list1 + list2**

```python
a = [ 2, 3 ]
b = a + [ 13, 17 ]
print(a)
print(b)
```

**Insert an item at a given index (with list slices)**

```python
a = [ 2, 3 ]
b = a[:2] + [5] + a[2:]
print(a)
print(b)
```

#### **Destructive vs Non-Destructive Example**

```python
print("Destructive:")
a = [ 2, 3 ]
b = a
a += [ 4 ]
print(a)
print(b)

print("Non-Destructive:")
a = [ 2, 3 ]
b = a
a = a + [ 4 ] # this overwrites a, but not the alias of b
print(a)
print(b)
```

### 9. **Removing Elements**

#### **Destructively (Modifying Lists)**

**Remove an item with list.remove(item)**

```python
a = [ 2, 3, 5, 3, 7, 6, 5, 11, 13 ]
print("a =", a)

a.remove(5)
print("After a.remove(5), a=", a)

a.remove(5)
print("After another a.remove(5), a=", a)
```

**Remove an item at a given index with list.pop(index)**

```python
a = [ 2, 3, 4, 5, 6, 7, 8 ]
print("a =", a)

item = a.pop(3)
print("After item = a.pop(3)")
print("   item =", item)
print("   a =", a)

item = a.pop(3)
print("After another item = a.pop(3)")
print("   item =", item)
print("   a =", a)

# Remove last item with list.pop()
item = a.pop()
print("After item = a.pop()")
print("   item =", item)
print("   a =", a)
```

#### **Non-Destructively (Creating New Lists)**

**Remove an item at a given index (with list slices)**

```python
a = [ 2, 3, 5, 3, 7, 5, 11, 13 ]
print("a =", a)

b = a[:2] + a[3:]
print("After b = a[:2] + a[3:]")
print("   a =", a)
print("   b =", b)
```

### 10. **Looping Over Lists**

#### **Looping with a normal for loop:**

```python
a = [ 2, 3, 5, 7 ]
print("Here are the items in a with their indexes:")
for index in range(len(a)):
    print("a[", index, "] =", a[index])
```

#### **Looping with a for each loop**

```python
# Lists and strings are both iterable types.
# This means that we can iterate (loop) over them directly!
a = [ 2, 3, 5, 7 ]
print("Here are the items in a:")
for item in a:
    print(item)
```

#### **Hazard: modifying inside a for loop**

```python
# IMPORTANT: don't change a list inside a for loop! The indexes will behave unpredictably.
# This isn't a problem for strings because they aren't mutable.
a = [ 2, 3, 5, 3, 7 ]
print("a =", a)

# Failed attempt to remove all the 3's
for index in range(len(a)):
    if (a[index] == 3):  # this eventually crashes!
        a.pop(index)

print("This line will not run!")
```

#### **Also Hazard: modifying inside a for-each loop**

```python
# If we remove items in a for-each loop, the loop won't crash,
# but it won't behave as we would expect either!

a = [3, 3, 2, 3, 4]
for item in a:       # this won't reach every item in the list!
    if (item == 3):
      a.remove(item)
print(a) # should be [2, 4], but there's still a 3 in there!
```

#### **Better: modifying inside a while loop**

```python
# Modify the list in a while loop instead of a for loop,
# to control how indexes 

a = [ 2, 3, 5, 3, 7 ]
print("a =", a)

# Successful attempt to remove all the 3's
index = 0
while (index < len(a)):
    if (a[index] == 3):
        a.pop(index)
    else:
        index += 1

print("This line will run!")
print("And now a =", a)
```

### 11. **List Methods: Sorting and Reversing**

Lists have many built-in methods. It's common for these methods to be implemented both destructively and non-destructively.

#### **Destructively with list.sort() or list.reverse()**

```python
a = [ 7, 2, 5, 3, 5, 11, 7 ]
print("At first, a =", a)
a.sort()
print("After a.sort(), a =",a)

a = [ 2, 3, 5, 7 ]
print("Here are the items in reverse:")
a.reverse()
for item in a:
    print(item)
print(a)
```

#### **Non-Destructively with sorted(list) and reversed(list)**

```python
a = [ 7, 2, 5, 3, 5, 11, 7 ]
print("At first")
print("   a =", a)
b = sorted(a)
print("After b = sorted(a)")
print("   a =", a)
print("   b =", b)

a = [ 2, 3, 5, 7 ]
print("Here are the items in reverse:")
for item in reversed(a):
    print(item)
print(a)
```

#### **More list methods**

For most list methods, see [this](https://docs.python.org/3/library/stdtypes.html#typesseq-mutable) table and [this](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) list of list methods.

### 12. **Tuples (Immutable Lists)**

Tuples are exactly like lists, except they are **immutable**. We cannot change the values of a tuple.

#### **Tuple syntax**

```python
t = (1, 2, 3)
print(type(t), len(t), t)

a = [1, 2, 3]
t = tuple(a)
print(type(t), len(t), t)
```

#### **Tuples are immutable**

```python
t = (1, 2, 3)
print(t[0])

t[0] = 42    # crash!
print(t[0])
```

#### **Parallel (tuple) assignment**

```
(x, y) = (1, 2)
print(x)
print(y)

# tuples are useful for swapping!
(x, y) = (y, x)
print(x)
print(y)
```

#### **Singleton tuple syntax**

```python
t = (42)
print(type(t), t*5)

t = (42,) # use a comma to force the type
print(type(t), t*5)
```

### 13. **List Comprehensions**

List comprehensions are a handy way to create lists using simple loops all in one line.

```
# Long way
a = []
for i in range(10):
    a.append(i)
print(a)

# Short way
a = [i for i in range(10)]
print(a)

# We can also add conditionals at the end (but keep it simple!)
a = [(i*100) for i in range(20) if i%5 == 0]
print(a)
```

### 14.**Converting Between Lists and Strings**

```python
# use list(s) to convert a string to a list of characters
a = list("wahoo!")
print(a)  # prints: ['w', 'a', 'h', 'o', 'o', '!']

# use s1.split(s2) to convert a string to a list of strings delimited by s2
a = "How are you doing today?".split(" ")
print(a) # prints ['How', 'are', 'you', 'doing', 'today?']

# use "".join(a) to convert a list of characters to a single string
print("".join(a))  # prints: Howareyoudoingtoday?

# "".join(a) also works on a list of strings (not just single characters)
a = ["parsley", "is", "gharsley"] # by Ogden Nash!
print("".join(a))  # prints: parsleyisgharsley
print(" ".join(a)) # prints: parsley is gharsley
```
