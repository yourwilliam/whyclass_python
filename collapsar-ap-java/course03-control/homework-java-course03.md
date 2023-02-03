# \[homework-java] course03

### 作业说明

下载 [CollapsarHomeworkWeek2](https://ossp.pengjunjie.com/mweb/CollapsarHomeworkWeek2.java) 文件。拷贝到week2的包中。

打开CollapsarHomeworkWeek2.java 文件, 运行一下。

在Edit Configuration中设置对应的参数，在VM options内添加`-ea`参数

![](https://ossp.pengjunjie.com/mweb/16327246598595.jpg)

后面执行的时候如果看到Passed 说明用例通过，如果看到异常说明当前用例有问题，需要修改。

![](https://ossp.pengjunjie.com/mweb/16327247126953.jpg)

### 作业

#### **1. nthSmithNumber(n)**

Write the function nthSmithNumber that takes a non-negative int n and returns the nth Smith number, where a Smith number is a composite (non-prime) the sum of whose digits are the sum of the digits of its prime factors (excluding 1). Note that if a prime number divides the Smith number multiple times, its digit sum is counted that many times. For example, 4 equals 2\*\*2, so the prime factor 2 is counted twice, thus making 4 a Smith Number.

#### **2. playPig()**

First, read about the dice game Pig [here](https://en.wikipedia.org/wiki/Pig\_\(dice\_game\)). Then, write the function playPig(), that allows two players to play the game Pig. You will want to use random.randint(1,6) to randomly choose a number between 1 and 6 inclusive. Grading criteria:

* Your game must enforce the basic rules of Pig.
* Your game should not use any graphics. This is a console-based game.
* Your game should use the input(prompt) function to get user input.
* Your game should print enough information to make the game reasonably fun and usable.

As with the previous creative problem, be thoughtful but don't overthink this. Any reasonably fun, playable game of Pig will do fine here. Have fun!

#### **3. Code Writing: nthHappyPrime**

Write the function nthHappyPrime(n) that finds the nth happy prime. Prime we know already, but what is a happy number? To find out, read the first paragraph on [the Wikipedia page](https://en.wikipedia.org/wiki/Happy\_number). For our purposes, we can simplify the process of finding a happy number by saying that a cycle which reaches 1 indicates a happy number, while a cycle which reaches 4 indicates a number that is unhappy. To solve this problem, you'll want to use isPrime and write three other functions:

* **sumOfSquaresOfDigits**

Write the function sumOfSquaresOfDigits(n) which takes a non-negative integer and returns the sum of the squares of its digits. For example, 123 would become 1^2 + 2^2 + 3^2 = 1 + 4 + 9 = 14. You **must** work with the number input directly instead of casting it to a string! Even if the linter allows your code, we will also check for this requirement in AutoLab!

* **isHappyNumber**

Write the function isHappyNumber(n) which takes a possibly-negative integer and returns True if it is happy and False otherwise. Note that all numbers less than 1 are not happy.

* **nthHappyPrime**

A happy prime is a number that is both happy and prime. Write the function nthHappyPrime(n) which takes a non-negative integer and returns the nth happy prime number (where the 0th happy prime number is 7).

#### **4. Code Writing: printNumberTriangle(n)**

Instead of returning a value, in this function you'll be printing out results. Write the function printNumberTriangle that takes one non-negative integer, n, and prints out a number triangle based on n. For example, given the number 4, this function would print out

```
1
21
321
4321
```
