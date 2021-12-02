# \[course05] 03 ArrayList

### ArrayList and Parameterized Types

```java
ArrayList<String> namelist;

namelist = new ArrayList<String>();

ArrayList<Player> playerList = new ArrayList<Player>();

//in java 10 or later
var playlerList = new ArrayList<Player>();
```

[ArrayList](https://devdocs.io/openjdk\~11/java.base/java/util/arraylist)

* list.size() — This function returns the current size of the list, that is, the number of items currently in the list. The only valid positions in the list are numbers in the range 0 to list.size()-1. Note that the size can be zero. A call to the default constructor new ArrayList() creates a list of size zero.
* list.add(obj) — Adds an object onto the end of the list, increasing the size by 1. The parameter, obj, can refer to an object of type T, or it can be null.
* list.get(N) — This function returns the value stored at position N in the list. The return type of this function is T.  N must be an integer in the range 0 to list.size()-1. If N is outside this range, an error of type IndexOutOfBoundsException occurs. Calling this function is similar to referring to A\[N] for an array, A, except that you can't use list.get(N) on the left side of an assignment statement.
* list.set(N, obj) — Assigns the object, obj, to position N in the ArrayList, replacing the item previously stored at position N. The parameter obj must be of type T. The integer N must be in the range from 0 to list.size()-1. A call to this function is equivalent to the command A\[N] = obj for an array A.
* list.clear() — Removes all items from the list, setting its size to zero.
* list.remove(N) — For an integer, N, this removes the N-th item in the ArrayList. N must be in the range 0 to list.size()-1. Any items in the list that come after the removed item are moved up one position. The size of the list decreases by 1.
* list.remove(obj) — If the specified object occurs somewhere in the list, it is removed from the list. Any items in the list that come after the removed item are moved up one position. The size of the ArrayList decreases by 1. If obj occurs more than once in the list, only the first copy is removed. If obj does not occur in the list, nothing happens; this is not an error.
* list.indexOf(obj) — A function that searches for the object, obj, in the list. If the object is found in the list, then the first position number where it is found is returned. If the object is not found, then -1 is returned.

### method

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites); 
        System.out.println(sites.get(1));  // get element
        sites.set(2, "Wiki"); 
        System.out.println(sites); 
        sites.remove(3);
        System.out.println(sites); 
        System.out.println(sites.size());
        
        for (int i = 0; i < sites.size(); i++) {
            System.out.println(sites.get(i));
        }
        
        for (String i : sites) {
            System.out.println(i);
        }
        

    }
}
```

### Programming with ArrayList

```java
import textio.TextIO;
import java.util.ArrayList;

/**
 * Reads a list of non-zero numbers from the user, then prints
 * out the input numbers in the reverse of the order in which
 * the were entered.  There is no limit on the number of inputs.
 */
public class ReverseWithArrayList {
    
    public static void main(String[] args) {
        ArrayList<Integer> list;
        list = new ArrayList<Integer>();
        System.out.println("Enter some non-zero integers.  Enter 0 to end.");
        while (true) {
            System.out.print("? ");
            int number = TextIO.getlnInt();
            if (number == 0)
                break;
            list.add(number);
        }
        System.out.println();
        System.out.println("Your numbers in reverse are:");
        for (int i = list.size() - 1; i >= 0; i--) {
            System.out.printf("%10d%n", list.get(i));
        }
    }

}
```

### ArrayList interface

![](https://ossp.pengjunjie.com/mweb/16383953307324.jpg)
