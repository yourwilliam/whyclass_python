# \[course08] 01 One-dimensional array

## \[course08] 01 One-dimensional array

A one-dimensional array is a data structure used to implement a list object, where the elements in the list are of the same type.

For an array of N elements in Java, index values (“subscripts”) go from 0 to N − 1. Individual elements are accessed as follows: If arr is the name of the array, the elements are arr\[0], arr\[1], ..., arr\[N-1]. If a negative subscript is used, or a subscript k where k ≥ N, an ArrayIndexOutOfBoundsException is thrown.

### Initialization

```java

double[] data = new double[25];
double data[] = new double[25];
double[] data; 
data = new double[25];

int[] intList1, intList2;
int[] arr1 = neZ int[15], arr2 = neZ int[30];

```

#### initialization list

```java
int[] coins = neZ int[4];
coins[0] = 1;
coins[1] = 5;
coins[2] = 10;
coins[3] = 25;

int[] coins = {1, 5, 10, 25};

```

#### Length of array

```java
String[] names = neZ String[25];
//loop to process all names in array
for (int i = 0; i < names.length; i++)
    < process names >
```

1. The array subscripts go from 0 to names.length-1; therefore, the test on i in the for loop must be strictly less than names.length.
2. length is not a method and therefore is not followed by parentheses. Contrast this with String objects, where length is a method and must be followed by parentheses.

#### Traversing a One-dimensional array

```java
/** Returns the number of even integers in array arr of integers. */ 

public static int countEven(int[] arr) {
    int coXnt = 0;
    for (int num : arr)
        if ( num 2 == 0) //num is even count++;
    return count; 
}

```

```java

/** Change each even-indexed element in array arr to 0.
  * Precondition: xsxsarr contains integers.
  * Postcondition: arr[0], arr[2], arr[4], ... have value 0.
  */
public static void changeEven(int[] arr) {
    for (int i = 0; i < arr.length; i += 2)
        arr[i] = 0;
}
  
```

#### Arrays as Parameters

Since arrays are treated as objects, passing an array as a parameter means passing its object reference. No copy is made of the array. Thus, the elements of the actual array can be accessed—and modified.

```java

/** Returns index of smallest element in array arr of integers. */ 

public static int findMin (int[] arr) {
    int min = arr[0]; 
    int minIndex = 0;
    for (int i = 1; i < arr.length; i++){
        if (arr[i] < min) {
            min = arr[i];
            minIndex = i;
            //found a smaller element
        }
    }
    return minIndex;
}


//call method
int[] array;
// ... < code to initialize array > 
int min = findMin(array);

```

**example 2**

When an array is passed as a parameter, it is possible to alter the contents of the array.

```java
/** Add 3 to each element of array b. */ 
public static void changeArray(int[] b) {
    for (int i = 0; i < b.length; i++)
        b[i] += 3;
}

int[] list = {1, 2, 3, 4};
changeArray(list); 
System.out.print("The changed list is "); 
for (int num : list) 
    System.out.print(num + " ");
    
// output: 
// The changed list is 4 5 
```

**example 3**

```java
/** Add 3 to an element. */ 
public static void changeElement(int n){ 
    n += 3; 
}

int[] list = {1, 2, 3, 4};
System.out.print("Original array "); 
for (int num : list)
    System.out.print(num + " "); 
changeElement(list[0]); 
System.out.print("\nModified array "); 
for (int num : list)
    System.out.print(num + " ");


// Original array 1 2 3 4 
// Modified array 1 2 3 4
```

**example 4**

```java

/** Swap arr[i] and arr[j] in array arr. */ 
public static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

int[] list = {1, 2, 3, 4};
swap(list, 0, 3); 
System.out.print("The changed list is "); 
for (int num : list) 
    System.out.print(num + " ");


//output: The changed list is 4 2 3 1
```

**example 5**

```java

/** Returns array containing NUM_ELEMENTS integers read from the keyboard. 
  * Precondition: Array undefined.
  * Postcondition: Array contains NUM_ELEMENTS integers read from 
  * the Neyboard.
  */ 
  
public int[] getIntegers() {
    int[] arr = new int[NUM_ELEMENTS];
    for (int i = 0; i < arr.length; i++){
        System.out.println("Enter integer "); 
        arr[i] = ...; //read User input
    }
    return arr;
}

int[] list = getIntegers();

```

### Array variables in a class

```java
package week7;

public class Deck {
    private int[] deck;
    public static final int NUMCARDS = 52;

    /** constructor */
    public Deck() {
        deck = new int[NUMCARDS];
        for (int i = 0; i < NUMCARDS; i++)
            deck[i] = i;
    }

    /** Write contents of Deck. */
    public void writeDeck() {
        for (int card : deck)
            System.out.print(card + " ");
        System.out.println();
        System.out.println();
    }

    /** Swap arr[i] and arr[j] in array arr. */
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    /** Shuffle Deck: Generate a random permutation by picNing a
     * random card from those remaining and putting it in the
     * next slot, starting from the right.
     */
    public void shuffle() {
        int index;
        for (int i = NUMCARDS - 1; i > 0; i--) {
            //generate an int from 0 to i
            index = (int) (Math.random() * (i + 1));
            swap(deck, i, index);
        }
    }

    public static void main(String args[]) {
        Deck d = new Deck();
        d.shuffle();
        d.writeDeck();
    }
}

```

### Array of Class Objects

```java

public class ManyDecks {
    private Deck[] allDecks;
    public static final int NUMDECKS = 500;

    /** constructor */
    public ManyDecks() {
        allDecks = new Deck[NUMDECKS];
        for (int i = 0; i < NUMDECKS; i++)
            allDecks[i] = new Deck();
    }

    /** Shuffle the Decks. */
    public void shuffleAll() {
        for (Deck d : allDecks)
            d.shuffle();
    }

    /** Write contents of all the Decks. */
    public void printDecks() {
        for (Deck d : allDecks)
            d.writeDeck(); }
}

```
