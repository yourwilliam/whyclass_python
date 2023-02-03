# \[pre-homework-java] course02

## \[pre-homework-java] course02

### 课前作业

下载 [CollapsarPreHomeworkWeek1.java](https://ossp.pengjunjie.com/CollapsarPreHomeworkWeek1.java)文件。拷贝到week1的包中。

打开CollapsarPreHomeworkWeek1.java 文件, 运行一下。

在Edit Configuration中设置对应的参数，在VM options内添加`-ea`参数

![](https://ossp.pengjunjie.com/mweb/16327246598595.jpg)

后面执行的时候如果看到Passed 说明用例通过，如果看到异常说明当前用例有问题，需要修改。

![](https://ossp.pengjunjie.com/mweb/16327247126953.jpg)

### 作业内容

#### 1. int\[] hotDogPurchase(int numHotDogs)

Hot dogs are an American tradition. Each year, Americans eat up to 20 Billion hot dogs. A classic hot dog is made up of two components: A frank (the meat) and a bun. Yet, for reasons that mystify mankind, the franks are typically sold in packs of ten and the buns in packs of eight. And, of course, you must buy full packages. Write the function hotdogPurchase(numHotdogs) that takes the total number of hot dogs you want to make, and returns the number of packages of franks and the number of packages of buns you need to purchase. You may assume that the argument, numHotdogs, is a non-negative int and the function returns as ints the smallest number of packages of franks and buns that must be purchased.

For example: hotdogPurchase(50) returns 5, 7. (Meaning 5 packs of franks and 7 packs of buns.). The function need to return an array of int(`return new int[]{num_of_frank, num_of_buns}`).

#### 2. int\[] hotdogExcess(int numHotdogs)

Write the function hotdogExcess(numHotdogs) that takes the total number of hot dogs you want to make (as a non-negative integer) and returns the number of excess franks and buns you will need to purchase. Hint: you may want to use hotDogPurchase, which you just wrote!

For example: hotdogPurchase(50) returns 0, 6.

The function need to return an array of int(`return new int[]{num_of_frank, num_of_buns}`).

#### 3. double distance(int x1, int y1, int x2, int y2)

Write the function distance(x1, y1, x2, y2) that takes four int values x1, y1, x2, y2 that represent the two points (x1, y1) and (x2, y2), and returns the distance between those points as a double.

#### 4. boolean circlesIntersect(int x1, int y1, int r1, int x2, int y2, int r2)

Write the function circlesIntersect(x1, y1, r1, x2, y2, r2) that takes 6 numbers (ints) -- x1, y1, r1, x2, y2, r2 -- that describe the circle centered at (x1,y1) with radius r1, and the circle centered at (x2,y2) with radius r2, and returns True if the two circles intersect and False otherwise.

#### 5. int eggCartons(int eggs)

Write the function eggCartons(eggs) that takes a non-negative integer number of eggs, and returns the smallest integer number of cartons required to hold that many eggs, where a carton may hold up to 12 eggs.

#### 6. boolean isFactor(int f, int n)

Write the function isFactor(f, n) that takes two int values f and n, and returns True if f is a factor of n, and False otherwise. Note that every integer is a factor of 0.

#### 7. boolean isMultiple(int m, int n)

Write the function isMultiple that takes two int values m and n and returns True if m is a multiple of n and False otherwise. Note that 0 is a multiple of every integer including itself. Also, you should make constructive use of the isFactor function you just wrote above.

#### 8. boolean isLegalTriangle(double s1, double s2, double s3)

Write the function isLegalTriangle(s1, s2, s3) that takes three double values representing the lengths of the sides of a triangle, and returns True if such a triangle exists and False otherwise. Note from the triangle inequality that the sum of each two sides must be greater than the third side, and further note that all sides of a legal triangle must be positive. Hint: how can you determine the longest side, and how might that help?

#### 9. boolean isRightTriangle(double x1, double y1, double x2, double y2, double x3, double y3)

Write the function isRightTriangle(x1, y1, x2, y2, x3, y3) that takes 6 double values that represent the vertices (x1,y1), (x2,y2), and (x3,y3) of a triangle, and returns True if that is a right triangle and False otherwise. You may wish to write a helper function, distance(x1, y1, x2, y2), which you might call several times. Also, remember to use almostEqual (instead of ==) when comparing floats.

#### 10. double triangleArea(double s1, double s2, double s3)

Write the function triangleArea(s1, s2, s3) that takes 3 doubles and returns the area of the triangle that has those lengths of its side. If no such triangle exists, return 0. Hint: you will probably wish to use Heron's Formula.

#### 11. double triangleAreaByCoordinates(double x1, double y1, double x2, double y2, double x3, double y3)

Write the function triangleAreaByCoordinates(x1, y1, x2, y2, x3, y3) that takes 6 double values that represent the three points (x1,y1), (x2,y2), and (x3,y3), and returns as a double the area of the triangle formed by those three points. Hint: you should make constructive use of the triangleArea function you just wrote above.
