# \[course02] 00 package

### print statements

```java
System.out.println("Rather a lot to type");
```

```java
import java.util.*;
import static net.mindview.util.Print.*;

public class HelloDate {
    //: operators/HelloDate.java

    public static void main(String[] args) {
        print("Hello, it’s: ");
        print(new Date());
    }
}
```

[net.mindview.util.jar](https://ossp.pengjunjie.com/mweb/net.mindview.util.jar)

add the root directory of that code tree to your computer’s CLASSPATH environment variable.

### TextIO

```java
import group.collapsar.java.basic.TextIO;

/**
 * A program that reads an integer that is typed in by the
 * user and computes and prints the square of that integer.
 */
public class PrintSquare {

    public static void main(String[] args) {

        int userInput;  // The number input by the user.
        int square;     // The userInput, multiplied by itself.

        System.out.print("Please type a number: ");
        userInput = TextIO.getlnInt();
        square = userInput * userInput;

        System.out.println();
        System.out.println("The number that you entered was " + userInput);
        System.out.println("The square of that number is " + square);
        System.out.println();

    } // end of main()

} //end of class PrintSquare
```

where is textio.TextIO

[TextIO](https://ossp.pengjunjie.com/mweb/TextIO.java)

add the file to package and import the class auto.
