# \[course\]03 —— Python循环

> EX32

```python
the_count = [1, 2, 3, 4, 5]
fruits = ['apples', 'oranges', 'pears', 'apricots']
change = [1, 'pennies', 2, 'dimes', 3, 'quarters']

# this first kind of for-loop goes through a list

p = 0
# 迭代  iterator
for number in the_count:
    print("This is count %d" % number)

print(number)
print(p)

# same as above
for fruit in fruits:
    print("A fruit of type: %s" % fruit)

# also we can go through mixed lists too
#  notice we have to use %r since we don't know what's in it
for i in change:
    print("I got %r" % i)

# we can also build lists, first start with an empty one
elements = []

# then use the range function to do 0 to 5 counts
for i in range(0, 6):
    print("Adding %d to the list." % i)
    # append is a function that lists understand
    elements.append(i)
    print(elements)

# now we can print them out too
for i in elements:
    print("Element was: %d" % i)

index = 0

while index < len(elements):
    print(elements[index])
    index += 1
```

> EX33

```python
i = 0
numbers = []

while i < 6:
    print("At the top i is %d" % i)
    numbers.append(i)

    i = i + 2
    if i == 4:
        continue
    print("Numbers now: ", numbers)
    print("At the bottom i is %d" % i)

print("The numbers: ")

for num in numbers:
    print(num)
```

## 1. **for循环和range**

[range方法](https://devdocs.io/python~3.7/library/functions#range)的使用，第一个参数指定开始，第二个参数指定到哪里结束\(&lt;\)

```python
# A for loop repeats an action a specific number of times
# based on the provided range
def sumFromMToN(m, n):
    total = 0
    # note that range(x, y) includes x but excludes y
    for x in range(m, n+1):
        total += x
    return total

print(sumFromMToN(5, 10) == 5+6+7+8+9+10)
```

**不使用range的计算方式**

```python
def sumFromMToN(m, n):
    return sum(range(m, n+1))

print(sumFromMToN(5, 10) == 5+6+7+8+9+10)

# And we can even do this with a closed-form formula,
# which is the fastest way, but which doesn't really
# help us demonstrate loops.  :-)

def sumToN(n):
    # helper function
    return n*(n+1)//2

def sumFromMToN_byFormula(m, n):
    return (sumToN(n) - sumToN(m-1))

print(sumFromMToN_byFormula(5, 10) == 5+6+7+8+9+10)
```

**如果range只写一个参数则默认从0开始**

```python
def sumToN(n):
    total = 0
    # range defaults the starting number to 0
    for x in range(n+1):
        total += x
    return total

print(sumToN(5) == 0+1+2+3+4+5)
```

Copy Visualize Run

**range的第三个参数代表步长\(step\)**

```python
def sumEveryKthFromMToN(m, n, k):
    total = 0
    # the third parameter becomes a step
    for x in range(m, n+1, k):
        total += x
    return total

print(sumEveryKthFromMToN(5, 20, 7) == (5 + 12 + 19))
```

**计算m到n之间的奇数之和**

```python
# We can also change the step by changing the inside of the loop
def sumOfOddsFromMToN(m, n):
    total = 0
    for x in range(m, n+1):
        if (x % 2 == 1):
            total += x
    return total

print(sumOfOddsFromMToN(4, 10) == sumOfOddsFromMToN(5,9) == (5+7+9))
```

**使用步长来计算**

```python
# Here we will range in reverse
# (not wise in this case, but instructional)
def sumOfOddsFromMToN(m, n):
    total = 0
    for x in range(n, m-1, -1):
        if (x % 2 == 1):
            total += x
    return total

print(sumOfOddsFromMToN(4, 10) == sumOfOddsFromMToN(5,9) == (5+7+9))
```

## 2. **循环嵌套**

循环可以嵌套使用，在循环嵌套的时候更要注意两次循环的次数

```python
# We can put loops inside of loops to repeat actions at multiple levels
# This prints the coordinates
def printCoordinates(xMax, yMax):
    for x in range(xMax+1):
        for y in range(yMax+1):
            print("(", x, ",", y, ")  ", end="")
        print()

printCoordinates(4, 5)
```

**使用循环来写`*`**

```python
def printStarRectangle(n):
    # print an nxn rectangle of asterisks
    for row in range(n):
        for col in range(n):
            print("*", end="")
        print()

printStarRectangle(5)
```

```python
# What would this do? Be careful and be precise!

def printMysteryStarShape(n):
    for row in range(n):
        print(row, end=" ")
        for col in range(row):
            print("*", end=" ")
        print()

printMysteryStarShape(5)
```

## 3. **while循环**

```python
# use while loops when there is an indeterminate number of iterations

def leftmostDigit(n):
    n = abs(n)
    while (n >= 10):
        n = n//10
    return n

print(leftmostDigit(72658489290098) == 7)
```

**Example: nth positive integer with some property**

```python
# eg: find the nth number that is a multiple of either 4 or 7
def isMultipleOf4or7(x):
    return ((x % 4) == 0) or ((x % 7) == 0)

def nthMultipleOf4or7(n):
    found = 0
    guess = -1
    while (found <= n):
        guess += 1
        if (isMultipleOf4or7(guess)):
            found += 1
    return guess

print("Multiples of 4 or 7: ", end="")
for n in range(15):
    print(nthMultipleOf4or7(n), end=" ")
print()
```

**Misuse: While loop over a fixed range**

```python
# sum numbers from 1 to 10
# note:  this works, but you should not use "while" here.
#        instead, do this with "for" (once you know how)
def sumToN(n):
    # note: even though this works, it is bad style.
    # You should do this with a "for" loop, not a "while" loop.
    total = 0
    counter = 1
    while (counter <= n):
        total += counter
        counter += 1
    return total

print(sumToN(5) == 1+2+3+4+5)
```

## 4.  **break 和 continue**

break： 结束当前循环 continue： 跳出当次循环，继续执行下一次循环

```python
# continue, break, and pass are three keywords used in loops
# in order to change the program flow
for n in range(200):
    if (n % 3 == 0):
        continue # skips rest of this pass
    elif (n == 8):
        break # skips rest of entire loop
    else:
        pass # does nothing! pass is a placeholder, not needed here
    print(n, end=" ")
print()
```

Copy Visualize Run

**while true循环的跳出**

```python
# Note- this is advanced content, as it uses strings. It's okay
# to not fully understand the content below.
def readUntilDone():
    linesEntered = 0
    while (True):
        response = input("Enter a string (or 'done' to quit): ")
        if (response == "done"):
            break
        print("  You entered: ", response)
        linesEntered += 1
    print("Bye!")
    return linesEntered

linesEntered = readUntilDone()
print("You entered", linesEntered, "lines (not counting 'done').")
```

## 5. **素数**

使用循环来求素数

```python
# Note: there are faster/better ways.  We're just going for clarity and simplicity here.
def isPrime(n):
    if (n < 2):
        return False
    for factor in range(2,n):
        if (n % factor == 0):
            return False
    return True

# And take it for a spin
for n in range(100):
    if isPrime(n):
        print(n, end=" ")
print()
```

**更快的查询素数的方式**

```python
# Note: this is still not the fastest way, but it's a nice improvement.
def fasterIsPrime(n):
    if (n < 2):
        return False
    if (n == 2):
        return True
    if (n % 2 == 0):
        return False
    maxFactor = round(n**0.5)
    for factor in range(3,maxFactor+1,2):
        if (n % factor == 0):
            return False
    return True

# And try out this version:
for n in range(100):
    if fasterIsPrime(n):
        print(n, end=" ")
print()
```

**验证**

```python
def isPrime(n):
    if (n < 2):
        return False
    for factor in range(2,n):
        if (n % factor == 0):
            return False
    return True

def fasterIsPrime(n):
    if (n < 2):
        return False
    if (n == 2):
        return True
    if (n % 2 == 0):
        return False
    maxFactor = round(n**0.5)
    for factor in range(3,maxFactor+1,2):
        if (n % factor == 0):
            return False
    return True

# Verify these are the same
for n in range(100):
    assert(isPrime(n) == fasterIsPrime(n))
print("They seem to work the same!")

# Now let's see if we really sped things up
import time
bigPrime = 499 # Try 1010809, or 10101023, or 102030407
print("Timing isPrime(",bigPrime,")", end=" ")
time0 = time.time()
print(", returns ", isPrime(bigPrime), end=" ")
time1 = time.time()
print(", time = ",(time1-time0)*1000,"ms")

print("Timing fasterIsPrime(",bigPrime,")", end=" ")
time0 = time.time()
print(", returns ", fasterIsPrime(bigPrime), end=" ")
time1 = time.time()
print(", time = ",(time1-time0)*1000,"ms")
```

## 6.  **计算第n个素数**

```python
def isPrime(n):
    if (n < 2):
        return False
    if (n == 2):
        return True
    if (n % 2 == 0):
        return False
    maxFactor = round(n**0.5)
    for factor in range(3,maxFactor+1,2):
        if (n % factor == 0):
            return False
    return True

# Adapt the "nth" pattern we used above in nthMultipleOf4or7()

def nthPrime(n):
    found = 0
    guess = 0
    while (found <= n):
        guess += 1
        if (isPrime(guess)):
            found += 1
    return guess

# and let's see a list of the primes
for n in range(10):
    print(n, nthPrime(n))
print("Done!")
```

