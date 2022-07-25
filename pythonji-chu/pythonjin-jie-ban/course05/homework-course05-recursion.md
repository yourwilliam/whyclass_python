# \[homework] course05 recursion

### 课前作业

下载 [youyulab\_hw\_recursion](https://ossp.pengjunjie.com/mweb/youyulab\_hw\_recursion.py) 和 [youyulab\_recursion\_linter](https://ossp.pengjunjie.com/mweb/youyulab\_recursion\_linter.py) 文件。拷贝到的文件夹中。

其中youyulab\_recursion\_linter文件不需要改动

打开youyulab\_hw\_recursion.py 文件

#### bunnyEars2

We have bunnies standing in a line, numbered 1, 2, ... The odd bunnies (1, 3, ..) have the normal 2 ears. The even bunnies (2, 4, ..) we'll say have 3 ears, because they each have a raised foot. Recursively return the number of "ears" in the bunny line 1, 2, ... n (without loops or multiplication).

```
bunnyEars2(0) → 0
bunnyEars2(1) → 2
bunnyEars2(2) → 5
```

#### sumDigits

Given a non-negative int n, return the sum of its digits recursively (no loops). Note that mod (%) by 10 yields the rightmost digit (126 % 10 is 6), while divide (/) by 10 removes the rightmost digit (126 / 10 is 12).

```
sumDigits(126) → 9
sumDigits(49) → 13
sumDigits(12) → 3
```

#### changePi

Given a string, compute recursively (no loops) a new string where all appearances of "pi" have been replaced by "3.14".

```
changePi("xpix") → "x3.14x"
changePi("pipi") → "3.143.14"
changePi("pip") → "3.14p"

```

#### parenBit

Given a string that contains a single pair of parenthesis, compute recursively a new string made of only of the parenthesis and their contents, so "xyz(abc)123" yields "(abc)".

```
parenBit("xyz(abc)123") → "(abc)"
parenBit("x(hello)") → "(hello)"
parenBit("(xy)1") → "(xy)"
```

#### strCount

Given a string and a non-empty substring sub, compute recursively the number of times that sub appears in the string, without the sub strings overlapping.

```
strCount("catcowcat", "cat") → 2
strCount("catcowcat", "cow") → 1
strCount("catcowcat", "dog") → 0
```
