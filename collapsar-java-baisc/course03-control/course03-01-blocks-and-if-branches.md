# \[course03] 01 Blocks and If Branches

### Blocks

The block is the simplest type of structured statement. Its purpose is simply to group a sequence of statements into a single statement. The format of a block is:

```java
{
     statements
}
```

Java is what is called a free-format language. There are no syntax rules about how the language has to be arranged on a page. So, for example, you could write an entire block on one line if you want. But as a matter of good programming style, you should lay out your program on the page in a way that will make its structure as clear as possible.

```java
{
   System.out.print("The answer is ");
   System.out.println(ans);
}
  
 
{  // This block exchanges the values of x and y
   int temp;      // A temporary variable for use in this block.
   temp = x;      // Save a copy of the value of x in temp.
   x = y;         // Copy the value of y into x.
   y = temp;      // Copy the value of temp into y.
}
```

### The Basic If Statement

An if statement tells the computer to take one of two alternative courses of action, depending on whether the value of a given boolean-valued expression is true or false.

```java
if ( boolean-expression )
    statement1
else
    statement2
```

![](https://ossp.pengjunjie.com/mweb/16379470254041.jpg)

```java
if ( boolean-expression ) {
    statements
}
else {
    statements
}
```

or

```java
if ( boolean-expression ) {
    statements
}
```

exchanges the value of two variables, x and y, but only if x is greater than y to begin with.

```java
if ( x > y ) {
    int temp;      // A temporary variable for use in this block.
    temp = x;      // Save a copy of the value of x in temp.
    x = y;         // Copy the value of y into x.
    y = temp;      // Copy the value of temp into y.
}
```

an example of an if statement that includes an else part

```java
if ( years > 1 ) {  // handle case for 2 or more years
    System.out.print("The value of the investment after ");
    System.out.print(years);
    System.out.print(" years is $");
}
else {  // handle case for 1 year
    System.out.print("The value of the investment after 1 year is $");
}  // end of if statement
System.out.printf("%1.2f", principal);  // this is done in any case
```

examples:

```java
import static net.mindview.util.Print.*;

public class IfElse {
  static int result = 0;
  static void test(int testval, int target) {
    if(testval > target)
      result = +1;
    else if(testval < target)
      result = -1;
    else
      result = 0; // Match
  }
  public static void main(String[] args) {
    test(10, 5);
    print(result);
    test(5, 10);
    print(result);
    test(5, 5);
    print(result);
  }
} /* Output:
1
-1
0
*///:~
```

### Multiway Branching

```java
if (boolean-expression-1)
     statement-1
else
     if (boolean-expression-2)
         statement-2
     else
         statement-3


//almost always written in the format

if (boolean-expression-1)
     statement-1
else if (boolean-expression-2)
     statement-2
else
     statement-3
     
```

```java
if (test-1)
     statement-1
else if (test-2)
     statement-2
else if (test-3)
     statement-3
  .
  . // (more cases)
  .
else if (test-N)
     statement-N
else
     statement-(N+1)
```

![](https://ossp.pengjunjie.com/mweb/16379514595604.jpg)

### example

```java
//TODO remember to change the textio
import textio.TextIO;

/**
 * This program will convert measurements expressed in inches,
 * feet, yards, or miles into each of the possible units of
 * measure.  The measurement is input by the user, followed by
 * the unit of measure.  For example:  "17 feet", "1 inch", or
 * "2.73 mi".  Abbreviations in, ft, yd, and mi are accepted.
 * The program will continue to read and convert measurements
 * until the user enters an input of 0.
 */
 public class LengthConverter {
 
    public static void main(String[] args) {
       
       double measurement;  // Numerical measurement, input by user.
       String units;        // The unit of measure for the input, also
                            //    specified by the user.
       
       double inches, feet, yards, miles;  // Measurement expressed in
                                           //   each possible unit of
                                           //   measure.
       
       System.out.println("Enter measurements in inches, feet, yards, or miles.");
       System.out.println("For example:  1 inch    17 feet    2.73 miles");
       System.out.println("You can use abbreviations:   in   ft  yd   mi");
       System.out.println("I will convert your input into the other units");
       System.out.println("of measure.");
       System.out.println();
       
       while (true) {
          
          /* Get the user's input, and convert units to lower case. */
          
          System.out.print("Enter your measurement, or 0 to end:  ");
          measurement = TextIO.getDouble();
          if (measurement == 0)
             break;  // Terminate the while loop.
          units = TextIO.getlnWord();            
          units = units.toLowerCase();  // convert units to lower case
          
          /* Convert the input measurement to inches. */
          
          if (units.equals("inch") || units.equals("inches") 
                                          || units.equals("in")) {
              inches = measurement;
          }
          else if (units.equals("foot") || units.equals("feet") 
                                          || units.equals("ft")) {
              inches = measurement * 12;
          }
          else if (units.equals("yard") || units.equals("yards") 
                                           || units.equals("yd")) {
              inches = measurement * 36;
          }
          else if (units.equals("mile") || units.equals("miles") 
                                             || units.equals("mi")) {
              inches = measurement * 12 * 5280;
          }
          else {
              System.out.println("Sorry, but I don't understand \"" 
                                                   + units + "\".");
              continue;  // back to start of while loop
          }
          
          /* Convert measurement in inches to feet, yards, and miles. */
          
          feet = inches / 12;
          yards = inches / 36;
          miles = inches / (12*5280);
          
          /* Output measurement in terms of each unit of measure. */
          
            System.out.println();
            System.out.println("That's equivalent to:");
            System.out.printf("%14.5g inches%n", inches);
            System.out.printf("%14.5g feet%n", feet);
            System.out.printf("%14.5g yards%n", yards);
            System.out.printf("%14.5g miles%n", miles);
            System.out.println();
       
       } // end while
       
       System.out.println();
       System.out.println("OK!  Bye for now.");
       
    } // end main()
    
 } // end class LengthConverter
```
