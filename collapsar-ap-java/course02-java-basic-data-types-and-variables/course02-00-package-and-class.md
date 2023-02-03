# \[course02] 00 Package and Class

## \[course02] 00 Package and Class

### Two packages used in this course

#### print statements

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

#### TextIO

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

### packages

A typical Java program has **user-defined classes** whose objects interact with those from Java class libraries.

In Java, related classes are grouped into **packages**, many of which are provided with the **compiler**.

```java

import packagename.*;

import packagename.ClassName;

import packagename.subpackagename.ClassName;


import java.util Array;
```

### Basic class

A Java program must have **at least one class**, the one that contains the main method. The Java files that comprise your program are called **source files**.

A compiler converts source code into machine-readable form called **bytecode**.

typical java code:

```java
/*
Program FirstProg.java Start with a comment, giving the program name and a brief description of that the program does.
*/ 

import package1.*; 
import package2.subpackage.ClassName;

public class FirstProg //note that the file name is FirstProg.java 
{
    public static type1 method1(parameter list) {
        < code for method 1 > 
    } 
    public static type2 method2(parameter list) {
        < code for method 2 > 
    }
    ...

    public static void main(String[] args) { 
        < your code > 
    }
}

```

1. All Java methods must be contained in a **class**.
2. The words class, public, static, and void are **reserved words**, alsocalled **keywords**. (This means they have specific uses in Java and **may not be used as identifiers**.)
3. The keyword **public signals** that the class or method is usable outside of the class, whereas private data members or methods are not.
4. The keyword static is used for methods that will not access any objects of a class, such as the methods in the FirstProg class in the example above. This is typically true for all methods in a source file that contains no instance variables. Most methods in Java do operate on objects and are not static. The main method, however, must always be static.
5. The program shown above is a Java application.
