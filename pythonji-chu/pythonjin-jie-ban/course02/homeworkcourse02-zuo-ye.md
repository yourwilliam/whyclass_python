# \[homework]course02 作业

## \[homework]course02 作业

\##TODO 记得修改路径

python 3.9及以下：

下载 [collapsar\_week1\_linter.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_week1\_linter.py) 和 [collapsar\_hw\_week1\_work.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_hw\_week1\_work.py)文件。拷贝到week1的文件夹中。

python 3.10 及以上:

下载 [collapsar\_hw\_week1\_work.py](https://ossp.pengjunjie.com/collapsar-homework-3-10/collapsar\_hw\_week1\_work.py)

其中collapsar\_week1\_linter.py文件不需要改动

打开collapsar\_pre\_hw\_week1.py 文件

### 作业

#### 1. **Code Writing: isEvenPositiveInt**

Write the function isEvenPositiveInt(n) which, given a value n, returns True if it is even, positive, and an integer, and False otherwise.

#### 2. **nearestOdd(n)**

Write the function nearestOdd(n) that takes an int or float n, and returns as an int value the nearest odd number to n. In the case of a tie, return the smaller odd value. Note that the result must be an int, so nearestOdd(13.0) is the int 13, and not the float 13.0.

Hint: Remember that the built-in round function works in surprising ways. Instead of round(n), you should use roundHalfUp(n) from this week's notes. That said, there are good ways to solve this problem without using rounding at all, if you prefer.

#### 3. **Code Writing: getTheCents(n)**

Write the function getTheCents(n) which takes a value n (which represents a payment in US dollars) and returns the number of cents in the payment. For example, if n is 2.45, the function should return 45. If n is an int, the function should return 0, as it has 0 cents; if it isn't a number, it should return None, because a non-number payment make no cents (ha!). If the payment has partial cents (for example, 3.953), it should be rounded up to the nearest cent (in this example, 96 cents).

#### 4. **isPerfectSquare(n)**

Write the function isPerfectSquare(n) that takes a possibly-non-int value, and returns True if it is an int that is a perfect square (that is, if there exists an integer m such that m\*\*2 == n), and False otherwise. Do not crash on non-ints nor on negative ints.

#### 5. **numberOfPoolBalls(rows)**

Pool balls are arranged in rows where the first row contains 1 pool ball and each row contains 1 more pool ball than the previous row. Thus, for example, 3 rows contain 6 total pool balls (1+2+3). With this in mind, write the function numberOfPoolBalls(rows) that takes a non-negative int value, the number of rows, and returns another int value, the number of pool balls in that number of full rows. For example, numberOfPoolBalls(3) returns 6. We will not limit our analysis to a "rack" of 15 balls. Rather, our pool table can contain an unlimited number of rows. For this problem and the next, you should research Triangular Numbers.

#### 6. **numberOfPoolBallRows(balls)**

This problem is the inverse of the previous problem. Write the function numberOfPoolBallRows(balls) that takes a non-negative int number of pool balls, and returns the smallest int number of rows required for the given number of pool balls. Thus, numberOfPoolBallRows(6) returns 3. Note that if any balls must be in a row, then you count that row, and so numberOfPoolBallRows(7) returns 4 (since the 4th row must have a single ball in it).

#### 7. **colorBlender(rgb1, rgb2, midpoints, n)**

This problem implements a color blender, inspired by [this tool](https://meyerweb.com/eric/tools/color-blend/#:::hex). In particular, we will use it with integer RGB values (it also does hex values and RGB% values, but we will not use those modes). Note that RGB values contain 3 integers, each between 0 and 255, representing the amount of red, green, and blue respectively in the given color, where 255 is "entirely on" and 0 is "entirely off".

For example, consider [this case](https://meyerweb.com/eric/tools/color-blend/#DC143C:BDFCC9:3:rgbd). Here, we are combining crimson (rgb(220, 20, 60)) and mint (rgb(189, 252, 201)), using 3 midpoints, to produce this palette (using our own numbering convention for the colors, starting from 0, as the tool does not number them):

color0: rgb(220, 20, 60) color1: rgb(212, 78, 95) color2: rgb(205, 136, 131) color3: rgb(197, 194, 166) color4: rgb(189, 252, 201)

There are 5 colors in the palette because the first color is crimson, the last color is mint, and the middle 3 colors are equally spaced between them.

So we could ask: if we start with crimson and go to mint, with 3 midpoints, what is color #1? The answer then would be rgb(212, 78, 95).

One last step: we need to represent these RGB values as a single integer. To do that, we'll use the first 3 digits for red, the next 3 for green, the last 3 for blue, all in base 10 (decimal, as you are accustomed to). Hence, we'll represent crimson as the integer 220020060, and mint as the integer 189252201.

With all that in mind, write the function colorBlender(rgb1, rgb2, midpoints, n), which takes two integers representing colors encoded as just described, a non-negative integer number of midpoints, and a non-negative integer n, and returns the nth color in the palette that the tool creates between those two colors with that many midpoints. If n is out of range (too small or too large), return None.

For example, following the case above: colorBlender(220020060, 189252201, 3, 1) returns 212078095

Hints: RGB values must be ints, not floats. Also, remember to use roundHalfUp(n) instead of round(n) when calculating midpoint colors.

#### 8. **Bonus/Optional: bonusPlayThreeDiceYahtzee(dice)**

In this exercise, we will write a simplified form of the dice game [Yahtzee](https://en.wikipedia.org/wiki/Yahtzee). In this version, the goal is to get 3 matching dice, and if you can't do that, then you hope to at least get 2 matching dice. The game is played like so:

1. Roll 3 dice.
2. If you do not have 3 matching dice:
   1. If you have 2 matching dice (a pair), keep the pair and roll one die to replace the third die.
   2. Otherwise, if you have no matching dice, keep the highest die and roll two dice to replace the other two dice.
3. Repeat step 2 one more time.
4. Finally, compute your score like so:
   1. If you have 3 matching dice, your score is 20 + the sum of the matching dice.
      * So if you have 4-4-4, your score is 20+4+4+4, or 32.
   2. If you only have 2 matching dice, your score is 10 + the sum of the matching dice.
      * So if you have 4-4-3, your score is 10+4+4, or 18.
   3. If you have no matching dice, your score is the highest die.
      * So if you have 4-3-2, your score is just 4.

Our goal is to write some Python code that plays this game. It's a large task, so we will use **top-down design** and break it up into smaller, more manageable pieces. So we'll first write some **helper functions** that do part of the work, and then those helper functions will make our final function much easier to write.

Also note: we will represent a hand of 3 dice as a single 3-digit integer. So the hand 4-3-2 will be represented by the integer 432. With that, let's start writing some code. Be sure to write your functions in the same order as given here, since later functions will make use of earlier ones!

1. **handToDice(hand)** Write the (very short) function handToRolls(hand) that takes a hand, which is a 3-digit integer, and returns 3 values, each of the 3 dice in the hand. For example:

```py
assert(handToDice(123) == (1,2,3))
assert(handToDice(214) == (2,1,4))
assert(handToDice(422) == (4,2,2))
```

**Hint:** You might find // and % useful here, and also getKthDigit.

1. **diceToOrderedHand(a, b, c)** Write the function diceToOrderedHand(a, b, c) that takes 3 dice and returns them in a hand, which is a 3-digit integer. However, even if the dice are unordered, the resulting hand must be ordered so that the largest die is on the left and smallest die is on the right. For example:

```py
assert(diceToOrderedHand(1,2,3) == 321)
assert(diceToOrderedHand(6,5,4) == 654)
assert(diceToOrderedHand(1,4,2) == 421)
assert(diceToOrderedHand(6,5,6) == 665)
assert(diceToOrderedHand(2,2,2) == 222)
```

**Hint:** You can use max(a,b,c) to find the largest of 3 values, and min(a,b,c) to find the smallest.

1. **playStep2(hand, dice)**

This is the most complicated part. Write the function playStep2(hand, dice) that plays step 2 as explained above. This function takes a hand, which is a 3-digit integer, and it also takes dice, which is an integer containing all the future rolls of the dice. For example, if dice is 5341, then the next roll will be a 1, then the roll after that will be a 4, then a 3, and finally a 5. Note that in a more realistic version of this game, instead of hard-coding the dice in this way, we'd probably use a random-number generator.

With that, the function plays step2 of the given hand, using the given dice to get the next rolls as needed. At the end, the function returns the new hand, but it has to be ordered, and the function also returns the resulting dice (which no longer contain the rolls that were just used).

For example:

```py
assert(playStep2(413, 2312) == (421, 23))
```

Here, the hand is 413, and the future dice rolls are 2312. What happens? Well, there are no matching dice in 413, so we keep the highest die, which is a 4, and we replace the 1 and the 3 with new rolls. Since new rolls come from the right (the one's digit), those are 2 and 1. So the new hand is 421. It has to be sorted, but it already is. Finally, the dice was 2312, but we used 2 digits, so now it's just 23. We return the hand and the dice, so we return (421, 23).

Here are some more examples. Be sure you carefully understand them:

```py
assert(playStep2(413, 2345) == (544, 23))
assert(playStep2(544, 23) == (443, 2))
assert(playStep2(544, 456) == (644, 45))
```

**Hint:** You may wish to use handToDice(hand) at the start to convert the hand into the 3 individual dice. **Hint:** Then, you may wish to use diceToOrderedHand(a, b, c) at the end to convert the 3 dice back into a sorted hand. **Hint:** Also, remember to use % to get the one's digit, and use //= to get rid of the one's digit.

1. **score(hand)** Almost there... Now write the function score(hand) that takes a 3-digit integer hand, and returns the score for that hand as explained in step4 above. For example:

```py
assert(score(432) == 4)
assert(score(532) == 5)
assert(score(443) == 10+4+4)
assert(score(633) == 10+3+3)
assert(score(333) == 20+3+3+3)
assert(score(555) == 20+5+5+5)
```

**Hint:** The structure of this function is actually quite similar to the previous function.

1. **bonusPlayThreeDiceYahtzee(dice)** Ok, we've made it to the last function: bonusPlayThreeDiceYahtzee(dice), the function that actually earns the 2.5 bonus points! This function takes one value, the dice with all the rolls for a game of 3-Dice Yahtzee. The function plays the game -- it does step1 and gets the first 3 dice (from the right), then it does step2 twice (by calling playStep2, which you already wrote), and then it computes the score (by calling score, which you already wrote). The function should return two values -- the resulting hand and the score for that hand. For example:

```py
assert(bonusPlayThreeDiceYahtzee(2312413) == (432, 4))
assert(bonusPlayThreeDiceYahtzee(2315413) == (532, 5))
assert(bonusPlayThreeDiceYahtzee(2345413) == (443, 18))
assert(bonusPlayThreeDiceYahtzee(2633413) == (633, 16))
assert(bonusPlayThreeDiceYahtzee(2333413) == (333, 29))
assert(bonusPlayThreeDiceYahtzee(2333555) == (555, 35))
```

#### 9. **Bonus/Optional: bonusFindIntRootsOfCubic(a,b,c,d)**

Write the function bonusFindIntRootsOfCubic(a,b,c,d) that takes the int or float coefficients a, b, c, d of a cubic equation of this form: ![-w174](http://ossp.pengjunjie.com/mweb/15709476372038.jpg)

You are guaranteed the function has 3 real roots, and in fact that the roots are all integers. Your function should return these 3 roots in increasing order. How does a function return multiple values? Like so: return root1, root2, root3 To get started, you'll want to read about Cardano's cubic formula here (great stuff!). Then, from that page, use this formula:

![-w443](http://ossp.pengjunjie.com/mweb/15709476112477.jpg)

where:

![-w319](http://ossp.pengjunjie.com/mweb/15709476250993.jpg)

This isn't quite as simple as it seems, because your solution for x will not only be approximate (and not exactly an int, so you'll have to do something about that), but it may not even be real! Though the solution is real, the intermediate steps may include some complex values, and in these cases the solution will include a (possibly-negligibly-small) imaginary value. So you'll have to convert from complex to real (try c.real if c is complex), and then convert from real to int.

Great, now you have one root. What about the others? Well, we can divide the one root out and that will leave us with a quadratic equation, which of course is easily solved. A brief, clear explanation of this step is provided [here](https://en.wikipedia.org/wiki/Cubic\_function#Factorization). Don't forget to convert these to int values, too!

So now you have all three int roots. Great job! All that's left is to sort them. Now, if this were later in the course, you could put them in a list and call a built-in function that will sort for you. But it's not, so you can't. Instead, figure out how to sort these values using the limited built-in functions and arithmetic available this week. Then just return these 3 values and you're done.
