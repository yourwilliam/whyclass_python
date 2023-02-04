# \[pre-homework-java] course 04

### 作业说明

下载 [CollapsarPreHomeworkWeek3](https://ossp.pengjunjie.com/mweb/CollapsarPreHomeworkWeek3.java) 文件。拷贝到week3的包中。

打开CollapsarPreHomeworkWeek3.java 文件, 运行一下。

在Edit Configuration中设置对应的参数，在VM options内添加`-ea`参数

![](https://ossp.pengjunjie.com/mweb/16327246598595.jpg)

后面执行的时候如果看到Passed 说明用例通过，如果看到异常说明当前用例有问题，需要修改。

![](https://ossp.pengjunjie.com/mweb/16327247126953.jpg)

### 作业内容

#### 1. **rotateString(s, k)**

Write the function rotateString(s, k) that takes a string s and a possibly-negative integer k. If k is non-negative, the function returns the string s rotated k places to the left. If k is negative, the function returns the string s rotated |k| places to the right. So, for example:

```java
 assert (rotateString("abcde", 0).equals("abcde"));
 assert (rotateString("abcde", 1).equals("bcdea"));
 assert (rotateString("abcde", 2).equals("cdeab"));
```

#### 2. **applyCaesarCipher(message, shift)**&#x20;

A [Caesar Cipher](https://en.wikipedia.org/wiki/Caesar\_cipher) is a simple cipher that works by shifting each letter in the given message by a certain number. For example, if we shift the message "We Attack At Dawn" by 1 letter, it becomes "Xf Buubdl Bu Ebxo".

Write the function applyCaesarCipher(message, shift) which shifts the given `message` by `shift` letters. You are guaranteed that message is a string, and that shift is an integer between -25 and 25. Capital letters should stay capital and lowercase letters should stay lowercase, and non-letter characters should not be changed. Note that "Z" wraps around to "A". So, for example:

```java
assert (applyCaesarCipher("We Attack At Dawn", 1).equals("Xf Buubdl Bu Ebxo"));
assert (applyCaesarCipher("1234", 6).equals("1234"));
```

#### 3. **hasBalancedParentheses(s)**

Write the function hasBalancedParentheses, which takes a string and returns True if that code has balanced parentheses and False otherwise (ignoring all non-parentheses in the string). We say that parentheses are balanced if each right parenthesis closes (matches) an open (unmatched) left parenthesis, and no left parentheses are left unclosed (unmatched) at the end of the text. So, for example, "( ( ( ) ( ) ) ( ) )" is balanced, but "( ) )" is not balanced, and "( ) ) (" is also not balanced. Hint: keep track of how many right parentheses remain unmatched as you iterate over the string.

#### 4. **largestNumber(text)**

largestNumber: Write the function largestNumber(text) that takes a string of text and returns the largest int value that occurs within that text, or None if no such value occurs. You may assume that the only numbers in the text are non-negative integers and that numbers are always composed of consecutive digits (without commas, for example). For example:

```java
assert (largestNumber("I saw 3 dogs, 17 cats, and 14 cows!") == 17);
```

returns 17 (the int value 17, not the string "17").

#### 5. **longestSubpalindrome(s)**

Write the function longestSubpalindrome(s), that takes a string s and returns the longest palindrome that occurs as consecutive characters (not just letters, but any characters) in s. So:

```java
assert (longestSubpalindrome("ab-4-be!!!").equals("b-4-b"));
```

returns "b-4-b". If there is a tie, return the lexicographically larger value -- in Python, a string s1 is lexicographically greater than a string s2 if (s1 > s2). So:

```java
   longestSubpalindrome("abcbce") 
    
```

returns "cbc", since ("cbc" > "bcb"). Note that unlike the previous functions, this function is case-sensitive (so "A" is not treated the same as "a" here). Also, from the explanation above, we see that longestSubpalindrome("aba") is "aba", and longestSubpalindrome("a") is "a".

#### 6. **collapseWhitespace(s)**

Without using the s.replace() method, write the function collapseWhitespace(s), that takes a string s and returns an equivalent string except that each occurrence of whitespace in the string is replaced by a single space. So, for example, collapseWhitespace("a\t\t\tb\n\nc") replaces the three tabs with a single space, and the two newlines with another single space , returning "a b c". Here are a few more test cases for you:

```java
assert (collapseWhitespace("a\nb").equals("a b") );
assert (collapseWhitespace("a\n   \t    b").equals("a b"));
assert (collapseWhitespace("a\n   \t    b  \n\n  \t\t\t c   ").equals("a b c "));
```

Once again, do not use s.replace() in your solution.

#### 7. **topScorer(data)**

Write the function topScorer(data) that takes a multi-line string encoding scores as csv data for some kind of competition with players receiving scores, so each line has comma-separated values. The first value on each line is the name of the player (which you can assume has no integers in it), and each value after that is an individual score (which you can assume is a non-negative integer). You should add all the scores for that player, and then return the player with the highest total score. If there is a tie, return all the tied players in a comma-separated string with the names in the same order they appeared in the original data. So, for example:

```java
String data = "Fred,10,20,30,40\nWilma,10,20,30";
assert (topScorer(data).equals("Fred"));

data = "Fred,10,20,30\nWilma,10,20,30,40";
assert (topScorer(data).equals("Wilma"));

data = "Fred,11,20,30\n Wilma,10,20,30,1";
assert (topScorer(data).equals("Fred,Wilma"));
```
