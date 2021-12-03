# \[course03] 05 Recursion

#### Recursion

A recursive subrouting must:

* hava a base case
* have a general case
* reach the base case after a finite (limited) number of calls to itself

**递归代码的思路**

以Factorial阶层函数为例

**第一步 - 明确你的函数的功能**

先明确的搞清楚函数到底是用来做什么的，函数的主要功能。函数需要传入一个阶层的数。

```
FUNCTION Factorial(n : INTEGER) RETURNS INTEGER 

ENDFUNCTION
```

**第二步 - 寻找递归结束条件**

所谓递归，就是会在函数内部代码中，调用这个函数本身，所以，我们必须要找出递归的结束条件，不然的话，会一直调用自己，进入无底洞。也就是说，我们需要找出当参数为啥时，递归结束，之后直接把结果返回。

阶层函数计算到最后一个1为止

```
FUNCTION Factorial(n : INTEGER) RETURNS INTEGER 
    IF n = 0
        THEN 
            Result ← 1   // This is the base case
    ENDIF 
ENDFUNCTION
```

**第三步 - 找出函数的等价关系式**

第三步我们要不断缩小参数的范围，缩小之后，我们可以通过一些辅助的变量或者操作，使原函数的结果不变。要找到一个等价关系式，每次都可以直接使用等价调用。

```
FUNCTION Factorial(n : INTEGER) RETURNS INTEGER
    IF n = 0
        THEN 
            Result ← 1   // This is the base case
        ELSE
            Result ← n * Factorial(n – 1) // This is the general case
    ENDIF 
    RETURN Result
ENDFUNCTION   
```

**什么是递归**

进一步剖析「递归」，先有「递」再有「归」，「递」的意思是将问题拆解成子问题来解决， 子问题再拆解成子子问题，...，直到被拆解的子问题无需再拆分成更细的子问题（即可以求解），「归」是说最小的子问题解决了，那么它的上一层子问题也就解决了，上一层的子问题解决了，上上层子问题自然也就解决了,....,直到最开始的问题解决,文字说可能有点抽象，那我们就以阶层 f(6) 为例来看下它的「递」和「归」。

在书上的例子上，我们把递称为 base case，归称为 Recursive。

#### Example 1 [factorial](https://codingbat.com/prob/p154669)

Given n of 1 or more, return the factorial of n, which is n \* (n-1) \* (n-2) ... 1. Compute the result recursively (without loops).

* factorial(1) → 1
* factorial(2) → 2
* factorial(3) → 6

```java
public int factorial(int n) {
  if (n == 1){
    return n;
  }
  return n * factorial(n - 1);
}
```

#### Example 2 [fibonacci](https://codingbat.com/prob/p120015)

The fibonacci sequence is a famous bit of mathematics, and it happens to have a recursive definition. The first two values in the sequence are 0 and 1 (essentially 2 base cases). Each subsequent value is the sum of the previous two values, so the whole sequence is: 0, 1, 1, 2, 3, 5, 8, 13, 21 and so on. Define a recursive fibonacci(n) method that returns the nth fibonacci number, with n=0 representing the start of the sequence.

* fibonacci(0) → 0
* fibonacci(1) → 1
* fibonacci(2) → 1

```java
public int fibonacci(int n) {
  if (n == 2){
    return 1;
  }
  else if (n == 1){
    return 1;
  }
  else if (n ==0){
    return 0;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

#### Example 3 [count7](https://codingbat.com/prob/p101409)

Given a non-negative int n, return the count of the occurrences of 7 as a digit, so for example 717 yields 2. (no loops). Note that mod (%) by 10 yields the rightmost digit (126 % 10 is 6), while divide (/) by 10 removes the rightmost digit (126 / 10 is 12).

* count7(717) → 2
* count7(7) → 1
* count7(123) → 0

```java
public int count7(int n) {
  if (n <= 1){
    return 0;
  }
  if (n % 10 == 7){
    return 1 + count7(n/10);
  } else{
    return count7(n/10);
  }
}
```

#### Example 4 [changeXY](https://codingbat.com/prob/p101372)

Given a string, compute recursively (no loops) a new string where all the lowercase 'x' chars have been changed to 'y' chars.

* changeXY("codex") → "codey"
* changeXY("xxhixx") → "yyhiyy"
* changeXY("xhixhix") → "yhiyhiy"

```java
public String changeXY(String str) {
  if (str.length() == 0){
    return "";
  }
  if (str.startsWith("x")){
    return "y" + changeXY(str.substring(1));
  }else{
    return str.substring(0,1) + changeXY(str.substring(1));
  }
}
```

#### Example 5 [count11](https://codingbat.com/prob/p167015)

Given a string, compute recursively (no loops) the number of "11" substrings in the string. The "11" substrings should not overlap.

* count11("11abc11") → 2
* count11("abc11x11x11") → 3
* count11("111") → 1

```java
public int count11(String str) {
  if (str.length() <= 1){
    return 0;
  }
  if (str.startsWith("11")){
    return 1 + count11(str.substring(2));
  }else {
    return count11(str.substring(1));
  }
}
```

#### Example 6 [array11](https://codingbat.com/prob/p135988)

Given an array of ints, compute recursively the number of times that the value 11 appears in the array. We'll use the convention of considering only the part of the array that begins at the given index. In this way, a recursive call can pass index+1 to move down the array. The initial call will pass in index as 0.

* array11(\[1, 2, 11], 0) → 1
* array11(\[11, 11], 0) → 2
* array11(\[1, 2, 3, 4], 0) → 0

```java
public int array11(int[] nums, int index) {
  if (nums.length == index){
    return 0;
  }
  if (nums[index] == 11){
    return 1 + array11(nums, index + 1);
  }else{
    return array11(nums, index + 1);
  }
}
```

**Why use index, how to delete an element in an array?**

```java
import java.util.Arrays;

public class DeleteElementInArray {
    public static int[] deleteElement(int[] arr, int index){
        int[] arr_new = new int[arr.length-1];
        for(int i=0;i<arr_new.length;i++){
            // 判断元素是否越界
            if (index < 0 || index >= arr.length) {
                throw new RuntimeException("元素越界... ");
            }
            if(i<index) {
                arr_new[i] = arr[i];
            }
            else {
                arr_new[i] = arr[i+1];
            }
        }
        return arr_new;
    }

    public static void main(String[] args) {
        int[] arr = {1,2,2,3,4,5,6,7};
        System.out.println(Arrays.toString(deleteElement(arr, 2)));
    }
}
```

**Use ArrayList to rewite:**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Count11ArrayList {
    public static int count11(ArrayList<Integer> arr){
        if (arr.size() == 0){
            return 0;
        }
        if (arr.get(0).equals(11)){
            arr.remove(0);
            return 1 + count11(arr);
        }else{
            arr.remove(0);
            return count11(arr);
        }
    }

    public static void main(String[] args) {
        int[] x = {1,2,11,5,11,11};
        List<Integer> xx = Arrays.stream(x).boxed().collect(Collectors.toList());
        System.out.println(count11(new ArrayList<Integer>(xx)));
    }
}
```
