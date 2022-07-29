# \[pre-homework]course04

### 课前作业

python 3.9 及以下：

下载 [collapsar\_week3\_linter.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_week3\_linter.py) 和 [collapsar\_pre\_hw\_week3.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_pre\_hw\_week3.py)文件。拷贝到week3的文件夹中。

其中youyulab\_week3\_linter.py文件不需要改动

python 3.10及以上：

[collapsar作业文件](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_week3\_linter.py)

下载 [collapsar\_pre\_hw\_week3.py](https://ossp.pengjunjie.com/collapsar-homework-3-10/collapsar\_pre\_hw\_week3.py)

打开youyulab\_pre\_hw\_week3.py 文件

### 作业内容

#### 1. **rotateString(s, k)**

Write the function rotateString(s, k) that takes a string s and a possibly-negative integer k. If k is non-negative, the function returns the string s rotated k places to the left. If k is negative, the function returns the string s rotated |k| places to the right. So, for example:

```py
assert(rotateString('abcd',  1) == 'bcda')
assert(rotateString('abcd', -1) == 'dabc')
```

#### 2. **applyCaesarCipher(message, shift)**&#x20;

A [Caesar Cipher](https://en.wikipedia.org/wiki/Caesar\_cipher) is a simple cipher that works by shifting each letter in the given message by a certain number. For example, if we shift the message "We Attack At Dawn" by 1 letter, it becomes "Xf Buubdl Bu Ebxo".

Write the function applyCaesarCipher(message, shift) which shifts the given `message` by `shift` letters. You are guaranteed that message is a string, and that shift is an integer between -25 and 25. Capital letters should stay capital and lowercase letters should stay lowercase, and non-letter characters should not be changed. Note that "Z" wraps around to "A". So, for example:

```py
assert(applyCaesarCipher("We Attack At Dawn", 1) == "Xf Buubdl Bu Ebxo")
assert(applyCaesarCipher("zodiac", -2) == "xmbgya")
```

#### 3. **hasBalancedParentheses(s)**

Write the function hasBalancedParentheses, which takes a string and returns True if that code has balanced parentheses and False otherwise (ignoring all non-parentheses in the string). We say that parentheses are balanced if each right parenthesis closes (matches) an open (unmatched) left parenthesis, and no left parentheses are left unclosed (unmatched) at the end of the text. So, for example, "( ( ( ) ( ) ) ( ) )" is balanced, but "( ) )" is not balanced, and "( ) ) (" is also not balanced. Hint: keep track of how many right parentheses remain unmatched as you iterate over the string.

#### 4. **largestNumber(text)**

largestNumber: Write the function largestNumber(text) that takes a string of text and returns the largest int value that occurs within that text, or None if no such value occurs. You may assume that the only numbers in the text are non-negative integers and that numbers are always composed of consecutive digits (without commas, for example). For example:

```py
largestNumber("I saw 3 dogs, 17 cats, and 14 cows!")
```

returns 17 (the int value 17, not the string "17"). And

```py
largestNumber("One person ate two hot dogs!")
```

returns None (the value None, not the string "None").

#### 5. **longestSubpalindrome(s)**

Write the function longestSubpalindrome(s), that takes a string s and returns the longest palindrome that occurs as consecutive characters (not just letters, but any characters) in s. So:

```py
longestSubpalindrome("ab-4-be!!!") 
```

returns "b-4-b". If there is a tie, return the lexicographically larger value -- in Python, a string s1 is lexicographically greater than a string s2 if (s1 > s2). So:

```py
   longestSubpalindrome("abcbce") 
```

returns "cbc", since ("cbc" > "bcb"). Note that unlike the previous functions, this function is case-sensitive (so "A" is not treated the same as "a" here). Also, from the explanation above, we see that longestSubpalindrome("aba") is "aba", and longestSubpalindrome("a") is "a".

#### 6. **collapseWhitespace(s)**

Without using the s.replace() method, write the function collapseWhitespace(s), that takes a string s and returns an equivalent string except that each occurrence of whitespace in the string is replaced by a single space. So, for example, collapseWhitespace("a\t\t\tb\n\nc") replaces the three tabs with a single space, and the two newlines with another single space , returning "a b c". Here are a few more test cases for you:

```py
    assert(collapseWhitespace("a\nb") == "a b")
    assert(collapseWhitespace("a\n   \t    b") == "a b")
    assert(collapseWhitespace("a\n   \t    b  \n\n  \t\t\t c   ") == "a b c ")
```

Once again, do not use s.replace() in your solution.

#### 7. **topScorer(data)**

Write the function topScorer(data) that takes a multi-line string encoding scores as csv data for some kind of competition with players receiving scores, so each line has comma-separated values. The first value on each line is the name of the player (which you can assume has no integers in it), and each value after that is an individual score (which you can assume is a non-negative integer). You should add all the scores for that player, and then return the player with the highest total score. If there is a tie, return all the tied players in a comma-separated string with the names in the same order they appeared in the original data. If nobody wins (there is no data), return None (not the string "None"). So, for example:

```py
data = '''\
Fred,10,20,30,40
Wilma,10,20,30
'''
assert(topScorer(data) == 'Fred')

data = '''\
Fred,10,20,30
Wilma,10,20,30,40
'''
assert(topScorer(data) == 'Wilma')

data = '''\
Fred,11,20,30
Wilma,10,20,30,1
'''
assert(topScorer(data) == 'Fred,Wilma')

assert(topScorer('') == None)
```

Hint: you may want to use both splitlines() and split(',') here!

#### 8. **drawFlagOfQatar(canvas, width, height)**

Write the function drawFlagOfQatar(canvas, width, height) that takes a canvas and its width and height and draws a flag of Qatar: ![](http://ossp.pengjunjie.com/mweb/flagOfQatar.png) Be sure to follow these guidelines:

* The flag must have a thin black border around it.
* The flag must be twice as wide as it is tall, with at least 30 pixels between the edge of the flag and any side of the canvas, and it must be centered in the canvas, and as large as possible given these restrictions.
* The canvas must have the name 'Qatar' in bold, centered at the top.

#### 9. **drawFlagOfTheEU(canvas, width, height)**

Write the function drawFlagOfTheEU(canvas, width, height) that follows the same guidelines as the flag of Qatar above, only now it draws a flag of the European Union: ![](http://ossp.pengjunjie.com/mweb/flagOfTheEU.png) Note that you should use circles instead of stars, and it should say 'European Union' at the top of the canvas.
