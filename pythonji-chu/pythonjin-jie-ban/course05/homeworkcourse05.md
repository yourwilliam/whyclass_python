# \[homework]course05

### 课前作业

python 3.9及以下：

下载 [collapsar\_week4\_linter.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar_week4_linter.py) 和 [collapsar\_hw\_week4.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar_hw_week4.py)文件。拷贝到week3的文件夹中。

其中youyulab\_week3\_linter.py文件不需要改动

python 3.10及以上：

下载 [collapsar\_hw\_week4.py](https://ossp.pengjunjie.com/collapsar-homework-3-10/collapsar_hw_week4.py)

打开youyulab\_pre\_hw\_week3.py 文件

### 作业内容

#### 1. **Look and Say Numbers**&#x20;

First, read about look-and-say numbers [here](https://en.wikipedia.org/wiki/Look-and-say_sequence).

Second, write the non-destructive function lookAndSay(lst) that takes a list of numbers and returns a list of numbers that results from "reading off" the initial list using the look-and-say method, using tuples for each (count, value) pair. For example:

```py
assert(lookAndSay([]) == [])
assert(lookAndSay([1, 1, 1]) == [(3, 1)])
assert(lookAndSay([-1, 2, 7]) == [(1, -1), (1, 2), (1, 7)])
assert(lookAndSay([3, 3, 8, -10, -10, -10]) == [(2, 3), (1, 8), (3, -10)])
assert(lookAndSay([3, 3, 8, 3, 3]) == [(2, 3), (1, 8), (2, 3)])
```

**Hint:** you'll want to keep track of the current number and how many times it has been seen.

Finally, write the non-destructive function inverseLookAndSay(lst) that does the inverse of the function lookAndSay, turning tuples of count and value into a single list. In general, inverseLookAndSay(lookAndSay(lst)) == lst. So for example:

```py
assert(inverseLookAndSay([(2, 3), (1, 8), (3, -10)]) == [3, 3, 8, -10, -10, -10])
```

#### 2.**Non-destructive and Destructive removeRepeats(lst)**

In this problem, you will write one function two ways: non-destructively and destructively. The function is removeRepeats(lst), which removes any repeating elements from a given list. For example:

```py
assert(removeRepeats([1, 3, 5, 3, 3, 2, 1, 7, 5]) == [1, 3, 5, 2, 7])
```

First, write nondestructiveRemoveRepeats(lst), which implements the function non-destructively. This function should not change the provided list, and should return a new list with no repeating elements.

Then, write destructiveRemoveRepeats(lst), which implements the function destructively. This function should modify the provided list to not have any repeating elements, and should not return at all.

**Note: Do not use sets in this problem, even if you know how to use them.**

#### 3. **bestScrabbleScore(dictionary, letterScores, hand)**

Background: in a Scrabble-like game, players each have a hand, which is a list of lowercase letters. There is also a dictionary, which is a list of legal words (all in lowercase letters). And there is a list of letterScores, which is length 26, where letterScores\[i] contains the point value for the ith character in the alphabet (so letterScores\[0] contains the point value for 'a'). Players can use some or all of the tiles in their hand and arrange them in any order to form words. The point value for a word is 0 if it is not in the dictionary; otherwise it is the sum of the point values of each letter in the word, according to the letterScores list (pretty much as it works in actual Scrabble).

In case you are interested, here is a list of the actual letterScores for Scrabble:

```py
letterScores = [
#  a, b, c, d, e, f, g, h, i, j, k, l, m,
   1, 3, 3, 2, 1, 4, 2, 4, 1, 8, 5, 1, 3,
#  n, o, p, q, r, s, t, u, v, w, x, y, z
   1, 1, 3,10, 1, 1, 1, 1, 4, 4, 8, 4,10
]
```

Note that your function must work for any list of letterScores that is provided by the caller.

With this in mind, write the function bestScrabbleScore(dictionary, letterScores, hand) that takes 3 lists -- dictionary (a list of lowercase words), letterScores (a list of 26 integers), and hand (a list of lowercase characters) -- and finds the highest-scoring word in the dictionary that can be formed by some arrangement of some set of letters in the hand.

* If there is only one highest-scoring word, return it and its score in a tuple.
* If there are multiple highest-scoring words, return a tuple with two elements: a list of all the highest-scoring words in the order they appear in the dictionary, then the score.
* If no highest-scoring word exists (ie, if no legal words can be formed from the hand), return None instead of a tuple. The dictionary in this problem is a list of words, and thus not a true Python dictionary (which we haven't taught you and you may not use in this assignment)! It is OK to loop through the dictionary, even if the dictionary we provide is large.

**Note:** You should definitely write helper functions for this problem! In fact, try to think of at least two helper functions you could use before writing any code at all.

**Another Note:** You may not use itertools for this problem! In fact, you should not create permutations of the letters at all, and if you do, your solution will probably time out on Autolab. There's a much simpler way to find all the legal words you can create...
