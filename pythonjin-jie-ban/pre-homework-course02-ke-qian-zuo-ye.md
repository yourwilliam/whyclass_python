# [pre-homework] course02 课前作业

## 
下载 [youyulab_week1_linter.py](http://ossp.pengjunjie.com/youyulab_week1_linter.py) 和 [youyulab_pre_hw_week1.py](http://ossp.pengjunjie.com/youyulab_pre_hw_week1.py)文件。拷贝到week1的文件夹中。

其中youyulab_week1_linter.py文件不需要改动

打开youyulab_pre_hw_week1.py 文件


## 作业内容

### 1. hotdogPurchase(numHotdogs) 
Hot dogs are an American tradition. Each year, Americans eat up to 20 Billion hot dogs. A classic hot dog is made up of two components: A frank (the meat) and a bun. Yet, for reasons that mystify mankind, the franks are typically sold in packs of ten and the buns in packs of eight. And, of course, you must buy full packages. Write the function hotdogPurchase(numHotdogs) that takes the total number of hot dogs you want to make, and returns the number of packages of franks and the number of packages of buns you need to purchase. You may assume that the argument, numHotdogs, is a non-negative int and the function returns as ints the smallest number of packages of franks and buns that must be purchased.

For example:
  hotdogPurchase(50) returns 5, 7. (Meaning 5 packs of franks and 7 packs of buns.)


### 2. hotdogExcess(numHotdogs)
Write the function hotdogExcess(numHotdogs) that takes the total number of hot dogs you want to make (as a non-negative integer) and returns the number of excess franks and buns you will need to purchase. Hint: you may want to use hotDogPurchase, which you just wrote!

For example:
  hotdogPurchase(50) returns 0, 6.
  
### 3. distance(x1, y1, x2, y2)
Write the function distance(x1, y1, x2, y2) that takes four int or float values x1, y1, x2, y2 that represent the two points (x1, y1) and (x2, y2), and returns the distance between those points as a float.

### 4. circlesIntersect(x1, y1, r1, x2, y2, r2)
Write the function circlesIntersect(x1, y1, r1, x2, y2, r2) that takes 6 numbers (ints or floats) -- x1, y1, r1, x2, y2, r2 -- that describe the circle centered at (x1,y1) with radius r1, and the circle centered at (x2,y2) with radius r2, and returns True if the two circles intersect and False otherwise.

### 5. eggCartons(eggs)
Write the function eggCartons(eggs) that takes a non-negative integer number of eggs, and returns the smallest integer number of cartons required to hold that many eggs, where a carton may hold up to 12 eggs.

### 6. isFactor(f, n)
Write the function isFactor(f, n) that takes two int values f and n, and returns True if f is a factor of n, and False otherwise. Note that every integer is a factor of 0.

### 7. isMultiple(m,n)
Write the function isMultiple that takes two int values m and n and returns True if m is a multiple of n and False otherwise. Note that 0 is a multiple of every integer including itself. Also, you should make constructive use of the isFactor function you just wrote above.

### 8. isLegalTriangle(s1, s2, s3)
Write the function isLegalTriangle(s1, s2, s3) that takes three int or float values representing the lengths of the sides of a triangle, and returns True if such a triangle exists and False otherwise. Note from the triangle inequality that the sum of each two sides must be greater than the third side, and further note that all sides of a legal triangle must be positive. Hint: how can you determine the longest side, and how might that help?

### 9. isRightTriangle(x1, y1, x2, y2, x3, y3)
Write the function isRightTriangle(x1, y1, x2, y2, x3, y3) that takes 6 int or float values that represent the vertices (x1,y1), (x2,y2), and (x3,y3) of a triangle, and returns True if that is a right triangle and False otherwise. You may wish to write a helper function, distance(x1, y1, x2, y2), which you might call several times. Also, remember to use almostEqual (instead of ==) when comparing floats.

### 10. triangleArea(s1, s2, s3)
Write the function triangleArea(s1, s2, s3) that takes 3 floats and returns the area of the triangle that has those lengths of its side. If no such triangle exists, return 0. Hint: you will probably wish to use Heron's Formula.

### 11. triangleAreaByCoordinates(x1, y1, x2, y2, x3, y3)
Write the function triangleAreaByCoordinates(x1, y1, x2, y2, x3, y3) that takes 6 int or float values that represent the three points (x1,y1), (x2,y2), and (x3,y3), and returns as a float the area of the triangle formed by those three points. Hint: you should make constructive use of the triangleArea function you just wrote above.
