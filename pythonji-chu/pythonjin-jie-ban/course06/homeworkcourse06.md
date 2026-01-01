# \[homework]course06

## 课前作业

下载 [youyulab\_week5\_linter.py](http://ossp.pengjunjie.com/youyulab_week5_linter.py) 和 [youyulab\_hw\_week5.py](http://ossp.pengjunjie.com/youyulab_hw_week5.py)文件。拷贝到week5的文件夹中。

其中youyulab\_week5\_linter.py文件不需要改动

打开youyulab\_pre\_hw\_week5.py 文件

## 作业内容

说明： week5的作业需要自己写测试用例。

### 1. **getPairSum(lst, target)**

Write the function getPairSum(lst, target) that takes a list of integers and a target value (also an integer), and if there is a pair of numbers in the given list that add up to the given target number, returns that pair as a tuple; otherwise, it returns None. If there is more than one valid pair, you can return any of them. For example:

```python
getPairSum([1], 1) == None
getPairSum([5, 2], 7) in [ (5, 2), (2, 5) ]
getPairSum([10, -1, 1, -8, 3, 1], 2) in [ (10, -8), (-8, 10), (-1, 3), (3, -1), (1, 1) ]
getPairSum([10, -1, 1, -8, 3, 1], 10) == None
```

A naive solution would be to check every possible pair in the list. That runs in O(N\*\*2). To get full credit for the problem, your solution must run in no worse than O(N) time.

### 2. **containsPythagoreanTriple(lst)**

Write the function containsPythagoreanTriple(lst) that takes a list of positive integers and returns True if there are 3 values (a, b, c) anywhere in the list such that (a, b, c) form a Pythagorean Triple `(where a**2 + b**2 == c**2)`. So \[1, 3, 6, 2, 5, 1, 4] returns True because of `(3,4,5): 3**2 + 4**2 == 5**2\`. \[1, 3, 6, 2, 1, 4] returns False, because it contains no triple.

A naive solution would be to check every possible triple (a, b, c) in the list. That runs in `O(N**3)`. To get full credit for the problem, your solution must run in no worse than `O(N**2)` time.

### 3. **movieAwards(oscarResults)**

Write the function movieAwards(oscarResults) that takes a set of tuples, where each tuple holds the name of a category and the name of the winning movie, then returns a dictionary mapping each movie to the number of the awards that it won. For example, if we provide the set:

```javascript
{ 
("Best Picture", "Green Book"), 
("Best Actor", "Bohemian Rhapsody"),
("Best Actress", "The Favourite"),
("Film Editing", "Bohemian Rhapsody"),
("Best Original Score", "Black Panther"),
("Costume Design", "Black Panther"),
("Sound Editing", "Bohemian Rhapsody"),
("Best Director", "Roma")
}
```

the program should return:

```javascript
{ 
"Black Panther" : 2,
"Bohemian Rhapsody" : 3,
"The Favourite" : 1,
"Green Book" : 1,
"Roma" : 1
}
```

**Note 1:** Remember that sets are unordered! For the example above, the returned set may be in a different order than what we have shown, and that is ok.

**Note 2:** Regarding efficiency, your solution needs to run faster than the naive solution using lists instead of some other appropriate, more-efficient data structures.

### 4. **friendsOfFriends(d)**

Background: we can create a dictionary mapping people to sets of their friends. For example, we might say:

```javascript
d = { }
d["jon"] = set(["arya", "tyrion"])
d["tyrion"] = set(["jon", "jaime", "pod"])
d["arya"] = set(["jon"])
d["jaime"] = set(["tyrion", "brienne"])
d["brienne"] = set(["jaime", "pod"])
d["pod"] = set(["tyrion", "brienne", "jaime"])
d["ramsay"] = set()
```

With this in mind, write the nondestructive function friendsOfFriends(d) that takes such a dictionary mapping people to sets of friends and returns a new dictionary mapping all the same people to sets of their friends-of-friends. For example, since Tyrion is a friend of Pod, and Jon is a friend of Tyrion, Jon is a friend-of-friend of Pod. This set should exclude any direct friends, so Jaime does not count as a friend-of-friend of Pod (since he is simply a friend of Pod) despite also being a friend of Tyrion's. Additionally, a person cannot be a friend or a friend-of-friend of themself.

Thus, in this example, friendsOfFriends should return:

```javascript
{
 'tyrion': {'arya', 'brienne'}, 
 'pod': {'jon'}, 
 'brienne': {'tyrion'}, 
 'arya': {'tyrion'}, 
 'jon': {'pod', 'jaime'}, 
 'jaime': {'pod', 'jon'}, 
 'ramsay': set()
}
```

**Note 1:** you may assume that everyone listed in any of the friend sets also is included as a key in the dictionary.

**Note 2:** you may **not** assume that if Person1 lists Person2 as a friend, Person2 will list Person1 as a friend! Sometimes friendships are only one-way. =(

**Note 3:** regarding efficiency, your solution needs to run faster than the naive solution using lists instead of some other appropriate, more-efficient data structures.
