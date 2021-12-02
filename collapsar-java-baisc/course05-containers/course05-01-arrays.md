# \[course05] 01 Arrays

A data structure consists of a number of data items chunked together so that they can be treated as a unit. An array is a data structure in which the items are arranged as a numbered sequence, so that each individual item can be referred to by its position number.

* The number of items in an array is called the **length** of the array.
* The type of the individual items in an array is called the **base type** of the array.
* And the position number of an item in an array is called the **index** of that item.
* The items in an array—really, the individual variables that make up the array—are more often referred to as the **elements** of the array.

The base type of an array can be any Java type.

```java
//declare
String[] namelist;
int[] A;
double[] prices;

//assignment
namelist = new String[1000];
A = new int[5];
prices = new double[100];
```

![](https://ossp.pengjunjie.com/mweb/16383871987220.jpg)

### declare and initialize

```java
double[] myList = {1.9, 2.9, 3.4, 3.5};
int[] arr = new int[]{3, 1, 2, 6, 4, 2};
String[][] str = new String[3][4];
```

* Arrays are uniform, fixed length, and have no methods
* Every element of an array must be the same type.
  * We will see how to get around that restriction later
* You can make arrays of primitives values or objects.
* The length of an array is determined when it is first created and cannot grow or shrink

### Arrays and For Loops

find the largest number in the array A

```java
double max;  // The largest number seen so far.
max = A[0];   // At first, the largest number seen is A[0].
int i;
for ( i = 1; i < A.length; i++ ) {
    if (A[i] > max) {
       max = A[i];
    }
}
// at this point, max is the largest item in A
```

average the non-zero elements

```java
double total;    // The sum of the non-zero numbers in the array.
int count;       // The number of non-zero numbers.
double average;  // The average of the non-zero numbers.
int i;
total = 0;
count = 0;
for ( i = 0; i < A.length; i++ ) {
    if ( A[i] != 0 ) {
        total = total + A[i];  // Add element to the total
        count = count + 1;     //      and count it.
    }
}
if (count == 0) {
    System.out.println("There were no non-zero elements.");
}
else {
    average = total / count;  // Divide by number of items
    System.out.printf("Average of %d elements is %1.5g%n",
                            count, average);
}
```

### Random Access

birthday problem: Suppose that there are N people in a room. What's the chance that there are two people in the room who have the same birthday? (That is, they were born on the same day in the same month, but not necessarily in the same year.) Most people severely underestimate the probability. We will actually look at a different version of the question: Suppose you choose people at random and check their birthdays. How many people will you check before you find one who has the same birthday as someone you've already checked? Of course, the answer in a particular case depends on random factors, but we can simulate the experiment with a computer program and run the program several times to get an idea of how many people need to be checked on average.

To simulate the experiment, we need to keep track of each birthday that we find. There are 365 different possible birthdays. (We'll ignore leap years.) For each possible birthday, we need to keep track of whether or not we have already found a person who has that birthday. The answer to this question is a boolean value, true or false. To hold the data for all 365 possible birthdays, we can use an array of 365 boolean values:

```java
boolean[] used; 
used = new boolean[365];
```

For this problem, the days of the year are numbered from 0 to 364. The value of used\[i] is true if someone has been selected whose birthday is day number i. Initially, all the values in the array are false. (Remember that this is done automatically when the array is created.) When we select someone whose birthday is day number i, we first check whether used\[i] is true. If it is true, then this is the second person with that birthday. We are done. On the other hand, if used\[i] is false, we set used\[i] to be true to record the fact that we've encountered someone with that birthday, and we go on to the next person. Here is a program that carries out the simulated experiment (of course, in the program, there are no simulated people, only simulated birthdays):

```java
/**
 * Simulate choosing people at random and checking the day of the year they 
 * were born on.  If the birthday is the same as one that was seen previously, 
 * stop, and output the number of people who were checked.
 */
public class BirthdayProblem {

   public static void main(String[] args) {

       boolean[] used;  // For recording the possible birthdays
                        //   that have been seen so far.  A value
                        //   of true in used[i] means that a person
                        //   whose birthday is the i-th day of the
                        //   year has been found.

       int count;       // The number of people who have been checked.

       used = new boolean[365];  // Initially, all entries are false.
   
       count = 0;

       while (true) {
             // Select a birthday at random, from 0 to 364.
             // If the birthday has already been used, quit.
             // Otherwise, record the birthday as used.

          int birthday;  // The selected birthday.
          birthday = (int)(Math.random()*365);
          count++;

          System.out.printf("Person %d has birthday number %d%n", count, birthday);

          if ( used[birthday] ) {  
                // This day was found before; it's a duplicate.  We are done.
             break;
          }

          used[birthday] = true;

       } // end while

       System.out.println();
       System.out.println("A duplicate birthday was found after " 
                                             + count + " tries.");
   }

} // end class BirthdayProblem
```

### Partially Full Arrays

a program that reads positive integers entered by the user and stores them for later processing. The program stops reading when the user inputs a number that is less than or equal to zero. The input numbers can be kept in an array, numbers, of type int\[]. Let's say that no more than 100 numbers will be input. Then the size of the array can be fixed at 100. But the program must keep track of how many numbers have actually been read and stored in the array. For this, it can use an integer variable. Each time a number is stored in the array, we have to count it; that is, value of the counter variable must be incremented by one. One question is, when we add a new item to the array, where do we put it? Well, if the number of items is count, then they would be stored in the array in positions number 0, 1, ..., (count-1). The next open spot would be position number count, so that's where we should put the new item.

```java
import textio.TextIO;

public class ReverseInputNumbers {

   public static void main(String[] args) {
   
     int[] numbers;  // An array for storing the input values.
     int count;      // The number of numbers saved in the array.
     int num;        // One of the numbers input by the user.
     int i;          // for-loop variable.
     
     numbers = new int[100];   // Space for 100 ints.
     count = 0;                // No numbers have been saved yet.
     
     System.out.println("Enter up to 100 positive integers; enter 0 to end.");
     
     while (true) {   // Get the numbers and put them in the array.
        System.out.print("? ");
        num = TextIO.getlnInt();
        if (num <= 0) {
              // Zero marks the end of input; we have all the numbers.
           break;
        }
        numbers[count] = num;  // Put num in position count.
        count++;  // Count the number
     }
     
     System.out.println("\nYour numbers in reverse order are:\n");
     
     for ( i = count - 1; i >= 0; i-- ) {
         System.out.println( numbers[i] );
     }
     
   } // end main();
   
}  // end class ReverseInputNumbers
```

### Two-dimensional Arrays

![](https://ossp.pengjunjie.com/mweb/16383883136574.jpg)

```java
int[][]  A;
A  =  new int[5][7];

int row, col;  // loop-control-variables for accessing rows and columns in A
for ( row = 0; row < 5; row++ ) {
    for ( col = 0; col < 7; col++ ) {
        System.out.printf( "%7d",  A[row][col] );
    }
    System.out.println();
}
```

```java
double decemberProfit;
int storeNum;
decemberProfit = 0.0;
for ( storeNum = 0; storeNum < 25; storeNum++ ) {
   decemberProfit += profit[storeNum][11];
}
```

### For-each loops

```java
for (int i = 0; i < namelist.length; i++) {
    System.out.println( namelist[i] );
}

for ( String name : namelist ) {
    System.out.println( name );
}

```

```java
int sum = 0;   // This will be the sum of all the positive numbers in A.
for ( int item : A ) {
   if (item > 0)
      sum = sum + item;
}
```

```java
int[] intList = new int[10];
for ( int item : intList ) {   // INCORRECT! DOES NOT MODIFY THE ARRAY!
   item = 17;
}
```

### Some Standard Array Methods

#### Arrays

[Arrays Devdocs](https://devdocs.io/openjdk\~11/java.base/java/util/arrays)

```java
playerList[k] = playerList[playerCt-1];
playerCt--;
if ( playerCt < playerList.length/4 ) {
        // More than 3/4 of the spaces are empty. Cut the array size in half.
    playerList = Arrays.copyOf( playerList, playerList.length/2 );
}
```

* Arrays.fill( array, value ) — Fill an entire array with a specified value. The type of value must be compatible with the base type of the array. For example, assuming that numlist is an array of type double\[], then Arrays.fill(numlist,17) will set every element of numlist to have the value 17.
* Arrays.fill( array, fromIndex, toIndex, value ) — Fills part of the array with value, starting at index number fromIndex and ending with index number toIndex-1. Note that toIndex itself is not included.
* Arrays.toString( array ) — A function that returns a String containing all the values from array, separated by commas and enclosed between square brackets. The values in the array are converted into strings in the same way they would be if they were printed out.
* Arrays.sort( array ) — Sorts the entire array. To sort an array means to rearrange the values in the array so that they are in increasing order. This method works for arrays of String and arrays of primitive type values (except for boolean, which would be kind of silly). But it does not work for all arrays, since it must be meaningful to compare any two values in the array, to see which is "smaller." We will discuss array-sorting algorithms in [Section 7.4](https://math.hws.edu/javanotes/c7/s4.html).
* Arrays.sort( array, fromIndex, toIndex ) — Sorts just the elements from array\[fromIndex] up to array\[toIndex-1]
* Arrays.binarySearch( array, value ) — Searches for value in the array. The array **must already be sorted** into increasing order. This is a function that returns an int. If the value is found in the array, the return value is the index of an element that contains that value. If the value does not occur in the array, the return value is -1. We will discuss the binary search algorithm in [Section 7.4](https://math.hws.edu/javanotes/c7/s4.html).

### Arrays reference

#### Arrays as parameters

![](https://ossp.pengjunjie.com/mweb/16384771195137.jpg)

#### Arrays as Parameters

![](https://ossp.pengjunjie.com/mweb/16384771632100.jpg)

#### The array reference is copied to the parameter

![](https://ossp.pengjunjie.com/mweb/16384775168009.jpg)

#### An array parameter is an alias

![](https://ossp.pengjunjie.com/mweb/16384775492293.jpg)

#### Changes to an array in a method are visible outside the method!

![](https://ossp.pengjunjie.com/mweb/16384785670102.jpg)

#### The null reference

![](https://ossp.pengjunjie.com/mweb/16384787979203.jpg)
