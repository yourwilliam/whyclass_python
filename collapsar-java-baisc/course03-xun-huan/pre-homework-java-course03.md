# \[pre-homework-java]course03

## \[pre-homework] course03

### 作业说明

下载 [CollapsarPreHomeworkWeek2](https://ossp.pengjunjie.com/mweb/CollapsarPreHomeworkWeek2.java) 文件。拷贝到week2的包中。

打开CollapsarHomeworkWeek1.java 文件, 运行一下。

在Edit Configuration中设置对应的参数，在VM options内添加`-ea`参数

![](https://ossp.pengjunjie.com/mweb/16327246598595.jpg)

后面执行的时候如果看到Passed 说明用例通过，如果看到异常说明当前用例有问题，需要修改。

![](https://ossp.pengjunjie.com/mweb/16327247126953.jpg)

### 作业内容

#### 1. **digitCount(n)** &#x20;

Write the function digitCount(n) that takes a possibly-negative int and returns the number of digits in it. So, digitCount(12323) returns 5, digitCount(0) returns 1, and digitCount(-111) returns 3. One way you could do this would be to return len(str(abs(n))), but you cannot do that, since you may not use strings here! This can be solved with logarithms, but seeing as this is "loops week", you should instead simply repeatedly remove the ones digit until you cannot.

#### 2. **gcd(m, n)** &#x20;

\[Note: to receive any credit, you must solve this problem using Euclid's algorithm, and by no other means. In particular, do not just loop through all integers less than min(m,n) and find the common factors that way -- it is much too slow!] According to Euclid, the greatest common divisor, or gcd, can be found like so:

```java
gcd(x,y) == gcd(y, x%y)
```

We can use that to quickly find gcd's. For example:

```java
gcd(270,250) == gcd(250, 20) # 270 % 250 == 20
             == gcd(20, 10) # 250 % 20 == 10
             == gcd(10, 0) # 20 % 10 == 0
```

When we get to gcd(x,0), the answer is x. So gcd(270, 250) is 10. With this in mind, write the function gcd(x,y) that takes two positive integers x and y and returns their gcd using Euclid's gcd algorithm.

#### 3. **hasConsecutiveDigits(n)**&#x20;

Write the function hasConsecutiveDigits(n) that takes a possibly- negative int value n and returns True if that number contains two consecutive digits that are the same, and False otherwise.

#### 4. **mostFrequentDigit(n)**

Write the function mostFrequentDigit(n), that takes a non-negative integer n and returns the digit from 0 to 9 that occurs most frequently in it, with ties going to the smaller digit.

#### 5. **nthAdditivePrime(n)**  &#x20;

Write the function nthAdditivePrime(n) that takes a non-negative int n and returns the nth Additive Prime, which is a prime number such that the sum of its digits is also prime. For example, 113 is prime and 1+1+3==5 and 5 is also prime, so 113 is an Additive Prime.

#### 6. **nthPalindromicPrime(n)**

Write the function nthPalindromicPrime(n). See [here](https://en.wikipedia.org/wiki/Palindromic\_prime) for details. So nthPalindromicPrime(0) returns 2, and nthPalindromicPrime(10) returns 313.

#### 7. **isRotation(x, y)**

Write the function isRotation(x, y) that takes two non-negative integers x and y, both guaranteed to not contain any 0's, and returns True if x is a rotation of the digits of y and False otherwise. For example, 3412 is a rotation of 1234. Any number is a rotation of itself.

#### 8. **carrylessAdd(x, y)**

First, you may wish to read the first page (page 44) from [here](http://www.maa.org/sites/default/files/pdf/upload\_library/2/Applegate-2013.pdf) about Carryless Arithmetic. Or, just understand that carryless addition is what it sounds like -- regular addition, only with the carry from each column ignored. So, for example, if we carryless-ly add 8+7, we get 5 (ignore the carry). And if we add 18+27, we get 35 (still ignore the carry). With this in mind, write the function carrylessAdd(x, y) that takes two non-negative integers x and y and returns their carryless sum. As the paper demonstrates, carrylessAdd(785, 376) returns 51.
