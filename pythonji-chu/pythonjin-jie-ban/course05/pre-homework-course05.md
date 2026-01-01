# \[pre-homework] course05

## 课前作业

下载 [youyulab\_week4\_linter.py](http://ossp.pengjunjie.com/youyulab_week4_linter.py) 和 [youyulab\_pre\_hw\_week4.py](http://ossp.pengjunjie.com/youyulab_pre_hw_week4.py)文件。拷贝到week3的文件夹中。

其中youyulab\_week3\_linter.py文件不需要改动

打开youyulab\_pre\_hw\_week3.py 文件

## 作业内容

### 1. **alternatingSum(a)**

Write the function alternatingSum(a) that takes a list of numbers and returns the alternating sum (where the sign alternates from positive to negative or vice versa). For example, alternatingSum(\[5,3,8,4]) returns 6 (that is, 5-3+8-4). If the list is empty, return 0.

### 2. **median(a)**

Write the non-destructive function median(a) that takes a list of ints or floats and returns the median value, which is the value of the middle element, or the average of the two middle elements if there is no single middle element. If the list is empty, return None.

### 3. **isSorted(a)**

Write the function isSorted(a) that takes a list of numbers and returns True if the list is sorted (either smallest-first or largest-first) and False otherwise. Your function must only consider each value in the list once (so, in terms of big-oh, which we will learn soon, it runs in O(n) time, where n=len(a)), and so in particular you may not sort the list.

### 4. **smallestDifference(a)**

Write the function smallestDifference(a) that takes a list of integers and returns the smallest absolute difference between any two integers in the list. If the list is empty, return -1. For example:

```python
      assert(smallestDifference([19,2,83,6,27]) == 4)
```

The two closest numbers in that list are 2 and 6, and their difference is 4.

### 5. **lookAndSay(a)**

First, you can read about look-and-say numbers [here](https://en.wikipedia.org/wiki/Look-and-say_sequence). Then, write the function lookAndSay(a) that takes a list of numbers and returns a list of numbers that results from "reading off" the initial list using the look-and-say method, using tuples for each (count, value) pair. For example:

```python
      lookAndSay([]) == []
      lookAndSay([1,1,1]) == [(3,1)]
      lookAndSay([-1,2,7]) == [(1,-1),(1,2),(1,7)]
      lookAndSay([3,3,8,-10,-10,-10]) == [(2,3),(1,8),(3,-10)]
      lookAndSay([3,3,8,3,3,3,3]) == [(2,3),(1,8),(4,3)]
```

### 6. **inverseLookAndSay(a)**

Write the function inverseLookAndSay(a) that does the inverse of the previous problem, so that, in general:

```python
      inverseLookAndSay(lookAndSay(a)) == a
```

```
Or, in particular:
```

```python
      inverseLookAndSay([(2,3),(1,8),(3,-10)]) == [3,3,8,-10,-10,-10]
```

#### 7. **multiplyPolynomials(p1, p2)**

Background: we can represent a polynomial as a list of its coefficients. For example, \[2, 3, 0, 4] could represent the polynomial 2x3 + 3x2 + 4. With this in mind, write the function multiplyPolynomials(p1, p2) which takes two lists representing polynomials as just described, and returns a third list representing the polynomial which is the product of the two. For example, multiplyPolynomials(\[2,0,3], \[4,5]) represents the problem `(2x**2 + 3)(4x + 5)`, and: `(2x**2 + 3)(4x + 5) = 8x**3 + 10x**2 + 12x + 15` And so this returns the list \[8, 10, 12, 15].

### 8. **nondestructiveRemoveRepeats(L)**

Write the function nondestructiveRemoveRepeats(L), which takes a list L and nondestructively returns a new list in which any repeating elements in L are removed. For example:

```python
    assert(nondestructiveRemoveRepeats([1, 3, 5, 3, 3, 2, 1, 7, 5]) ==[1, 3, 5, 2, 7])
```

```
Also:
```

```python
    L = [1, 3, 5, 3, 3, 2, 1, 7, 5]
    assert(nondestructiveRemoveRepeats(L) == [1, 3, 5, 2, 7])
    assert(L == [1, 3, 5, 3, 3, 2, 1, 7, 5]) # nondestructive!
```

Note that the values in the resulting list occur in the order they appear in the original list, but each occurs only once in the result. Also, since this is a nondestructive function, it returns the resulting list.

### 9. **destructiveRemoveRepeats(L)**

Write the function destructiveRemoveRepeats(L), which implements the same function destructively. Thus, this function should directly modify the provided list to not have any repeating elements. Since this is a destructive function, it should not return any value at all (so, implicitly, it should return None). For example:

```python
    L = [1, 3, 5, 3, 3, 2, 1, 7, 5]
    destructiveRemoveRepeats(L)
    assert(L == [1, 3, 5, 2, 7]) # destructive!
```
