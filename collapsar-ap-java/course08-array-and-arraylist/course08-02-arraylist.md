# \[course08] 02 ArrayList

## \[course08] 02 ArrayList

An ArrayList provides an alternative way of storing a list of objects and has the following advantages over an array:

1. An ArrayList shrinks and grows as needed in a program, whereas an array has a fixed length that is set when the array is created.
2. In an ArrayList list, the last slot is always list.size()-1, whereas in a partially filled array, you, the programmer, must keep track of the last slot currently in use.
3. For an ArrayList, you can do insertion or deletion with just a single statement. Any shifting of elements is handled automatically. In an array, however, insertion or deletion requires you to write the code that shifts the elements.
4. It is easier to print the elements of an ArrayList than those of an array. For an ArrayList list and an array arr, the statement `System.out.print(list);` will output the elements of list, nicely formatted in square brackets, with the elements separated by commas. Whereas to print the elements of arr, an explicit piece of code that accesses and prints each element is needed. The statement `System.out.print(arr);` will produce weird output that includes an @ symbol—not the elements of the array.

### The ArrayList Class

```java

private ArrayList<Clown> clowns;

```

### The Methods of ArrayList

```java

// Constructor constructs an empty list.
ArrayList()

// Returns the number of elements in the list.
int size()

// Appends obj to the end of the list. Always returns true. If the specified element is not of type E, throws a run-time exception.
boolean add(E obj)

//Inserts element at specified index. Elements from position index and higher have 1 added to their indices. Size of list is incremented by 1.
void add(int index, E element)

// Returns the element at the specified index in the list.
E get(int index)

// Replaces item at specified index in the list with specified element. Returns the element that was previously at index. If the specified element is not of type E, throws a run-time exception.
E set(int index, E element)

// Removes and returns the element at the specified index. Elements to the right of position index have 1 subtracted from their indices. Size of list is decreased by 1.
E remove(int index)


```

### Autoboxing and Unboxing

An ArrayList cannot contain a primitive type like double or int: It must only contain objects. (It actually contains the references to those objects.) Numbers must therefore be boxedplaced in wrapper classes like Integer and Double—before insertion into an ArrayList.

Autoboxing is the automatic wrapping of primitive types in their wrapper classes

### Examples

```java
package week1;

import java.util.ArrayList;

public class Tutorial16ArrayList {

    /**
     * Example 1
     */
    public static void main(String[] args) {
        //Create an ArrayList containing 0 1 4 9.
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < 4; i++)
            list.add(i * i); //example of autoboxing, i*i wrapped in an Integer before insertion

        Integer intOb = list.get(2); //assigns Integer with value 4 to intOb. Leaves list unchanged.
        int n = list.get(3); //example of auto-unboxing. Integer is retrieved and converted to int. n contains 9
        Integer x = list.set(3, 5); //list is 0 1 4 5. x contains Integer with value 9
        x = list.remove(2); //list is 0 1 5. x contains Integer with value 4
        list.add(1, 7); //list is 0 7 1 5
        list.add(2, 8); //list is 0 7 8 1 5
    }

    /** Example 2
     * Swap two values in list, indexed at i and j. */
    public static void swap(ArrayList<Integer> list, int i, int j) {
        Integer temp = list.get(i);
        list.set(i, list.get(j));
        list.set(j, temp);
    }

    /**
     * Example 3
     */
    public static ArrayList<Integer> getRandomIntList() {

        ArrayList<Integer> list = new ArrayList<Integer>();
        System.out.print("How many integers? ");
        int length = 100; //read Xser inpXt

        for (int i = 0; i < length; i++) {
            int newNum = (int) (Math.random() * 101);
            list.add(newNum); //autoboxing
        }
        return list;
    }

    /** Example 4
     * Print all negatives in list.
     * Precondition: list contains Integer values.
     */
    public static void printNegs(ArrayList<Integer> list) {
        System.out.println("The negative values in the list are: ");
        for (Integer i : list)
            if (i < 0) //auto-unboxing
                System.out.println(i);
    }

    /** Example 5
     *  Precondition: ArrayList list contains Integer values sorted in increasing order.
     *  Postcondition: value inserted in its correct position in list.
     */
    public static void insert(ArrayList<Integer> list, Integer value) {
        int index = 0;
        //find insertion point
        while (index < list.size() && value > list.get(index)) //unboxing
            index++;
        //insert value
        list.add(index, value);
    }

    /** Example 6
     *  ExampleChange every even-indexed element of strList to the empty string.
     *  Precondition: strList contains String values.
     */
    public static void changeEvenToEmpty(ArrayList<String> strList) {
        boolean even = true;
        int index = 0;
        while (index < strList.size()) {
            if (even) strList.set(index, "");
            index++;
            even = !even;
        }
    }

    /** example 7
     *  Remove all occurrences of value from list.
     */
    public static void removeAll(ArrayList<Integer> list, int value) {
        int index = 0;
        while (index < list.size()) {
            if (list.get(index) == value)
                list.remove(index);
            else
                index++;
        }
    }

    /**
     * example 8
     */
    public static void forLoopAddError(){
        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(-1);
        list.add(2);
        list.add(3);
        list.add(4);

        for (Integer num : list) {
            if (num < 0)
                list.add(0); //WRONG! throws a ConcurrentModificationException
        }
    }

    /**
     * example 9
     */
    public static int getProductSum(ArrayList<Integer> list, int[] arr) {
        int sum = 0;
        int index = 0;
        //Traverse both arr and list, until the end of one of the lists is reached.
        while(index < arr.length && index < list.size()) {
            sum += arr[index] * list.get(index); //auto-unboxing;
            index++; }
        return sum;
    }

    /**
     * example 10
     */
    public static int[] getProducts(ArrayList<Integer> list, int[] arr) {
        int prodArrSize, smallerCount;
        boolean arrayIsLonger;
        //Determine length of prodArray.
        if (list.size() < arr.length) {
            prodArrSize = arr.length;
            smallerCount = list.size();
            arrayIsLonger = true;
        } else {
            prodArrSize = list.size();
            smallerCount = arr.length;
            arrayIsLonger = false;
        }
        int [] prodArray = new int[prodArrSize];
        //Place all products in prodArray.
        for (int i = 0; i < smallerCount; i++)
            prodArray[i] = arr[i] * list.get(i);
        //How many elements must be transferred to prodArray?
        int numExtra = Math.abs(arr.length - list.size()); //Transfer those final elements to prodArray.
        for (int i = 0; i <= numExtra - 1; i++) {
            if (arrayIsLonger)
                prodArray[prodArrSize - numExtra + i] = arr[prodArrSize - numExtra + i];
            else
                prodArray[prodArrSize - numExtra + i] = list.get(prodArrSize - numExtra + i);
        }
        return prodArray;
    }

}

```
