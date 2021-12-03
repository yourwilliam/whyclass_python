# \[course05] Recursion

#### Recursion

#### Example 1 factorial

Given n of 1 or more, return the factorial of n, which is n \* (n-1) \* (n-2) ... 1. Compute the result recursively (without loops).

* factorial(1) → 1
* factorial(2) → 2
* factorial(3) → 6

```python
def factorial(n):
    if n == 1:
        return n
    return n * factorial(n - 1)
```

#### Example 2 fibonacci

The fibonacci sequence is a famous bit of mathematics, and it happens to have a recursive definition. The first two values in the sequence are 0 and 1 (essentially 2 base cases). Each subsequent value is the sum of the previous two values, so the whole sequence is: 0, 1, 1, 2, 3, 5, 8, 13, 21 and so on. Define a recursive fibonacci(n) method that returns the nth fibonacci number, with n=0 representing the start of the sequence.

* fibonacci(0) → 0
* fibonacci(1) → 1
* fibonacci(2) → 1

```python
def fibonacci(n):
    if n == 2:
        return 1
    elif n == 1:
        return 1
    elif n == 0:
        return 0
    return fibonacci(n - 1) + fibonacci(n - 2)
```

#### Example 3 count7

Given a non-negative int n, return the count of the occurrences of 7 as a digit, so for example 717 yields 2. (no loops). Note that mod (%) by 10 yields the rightmost digit (126 % 10 is 6), while divide (/) by 10 removes the rightmost digit (126 / 10 is 12).

* count7(717) → 2
* count7(7) → 1
* count7(123) → 0

```python
def count7(n):
    if n <= 1:
        return 0
    if n % 10 == 7:
        return 1 + count7(n // 10)
    else:
        return count7(n // 10)
```

#### Example 4 changeXY

Given a string, compute recursively (no loops) a new string where all the lowercase 'x' chars have been changed to 'y' chars.

* changeXY("codex") → "codey"
* changeXY("xxhixx") → "yyhiyy"
* changeXY("xhixhix") → "yhiyhiy"

```python
def changeXY(s):
    if len(s) == 0:
        return ""
    if s.startswith("x"):
        return "y" + changeXY(s[1:])
    else:
        return s[0] + changeXY(s[1:])
```

#### Example 5 count11

Given a string, compute recursively (no loops) the number of "11" substrings in the string. The "11" substrings should not overlap.

* count11("11abc11") → 2
* count11("abc11x11x11") → 3
* count11("111") → 1

```python
def count11(s):
    if len(s) <= 1:
        return 0
    if s.startswith("11"):
        return 1 + count11(s[2:])
    else:
        return count11(s[1:])
```

#### Example 6 [array11](https://codingbat.com/prob/p135988)

Given an array of ints, compute recursively the number of times that the value 11 appears in the array. We'll use the convention of considering only the part of the array that begins at the given index. In this way, a recursive call can pass index+1 to move down the array. The initial call will pass in index as 0.

* array11(\[1, 2, 11], 0) → 1
* array11(\[11, 11], 0) → 2
* array11(\[1, 2, 3, 4], 0) → 0

```python
def array11(nums):
    if len(nums) == 0:
        return 0
    if nums[0] == 11:
        return 1 + array11(nums[1:])
    else:
        return array11(nums[1:])
```
