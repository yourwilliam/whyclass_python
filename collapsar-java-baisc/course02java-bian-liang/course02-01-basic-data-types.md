# \[course02] 01 Basic Data Types

### Variables

A name used in this way—to refer to data stored in memory—is called a variable.

In Java, the only way to get data into a variable—that is, into the box that the variable names—is with an assignment statement. An assignment statement takes the form:

```
variable = expression;
```

### Types

There are eight so-called primitive types built into Java. The primitive types are named **byte**, **short**, **int**, **long**, **float**, **double**, **char**, and **boolean**.

![](https://ossp.pengjunjie.com/mweb/16378235011427.jpg)

The first four types hold integers (whole numbers such as 17, -38477, and 0). The four integer types are distinguished by the ranges of integers they can hold.

The float and double types hold real numbers (such as 3.6 and -145.99). Again, the two real types are distinguished by their range and accuracy.

A variable of type char holds a single character from the Unicode character set.

* short corresponds to two bytes (16 bits). Variables of type short have values in the range -32768 to 32767.
* int corresponds to four bytes (32 bits). Variables of type int have values in the range -2147483648 to 2147483647.
* long corresponds to eight bytes (64 bits). Variables of type long have values in the range -9223372036854775808 to 9223372036854775807.

The float data type is represented in four bytes of memory, using a standard method for encoding real numbers. The maximum value for a float is about 10 raised to the power 38. A float can have about 7 significant digits. (So that 32.3989231134 and 32.3989234399 would both have to be rounded off to about 32.398923 in order to be stored in a variable of type float.) A double takes up 8 bytes, can range up to about 10 to the power 308, and has about 15 significant digits. Ordinarily, you should stick to the double type for real values.

A variable of type char occupies two bytes in memory. The value of a char variable is a single character such as A, \*, x, or a space character. Values of type char are closely related to integer values, since a character is actually stored as a 16-bit integer code number.

```java
// "e" means "10 to the power."

public class Exponents {
  public static void main(String[] args) {
    // Uppercase and lowercase 'e' are the same:
    float expFloat = 1.39e-43f;
    expFloat = 1.39E-43f;
    System.out.println(expFloat);
    double expDouble = 47e47d; // 'd' is optional
    double expDouble2 = 47e47; // Automatically double
    System.out.println(expDouble);
  }
} /* Output:
1.39E-43
4.7E48
*///:~
```

### Literals

![](https://ossp.pengjunjie.com/mweb/16378235673967.jpg)

A data value is stored in the computer as a sequence of bits. In the computer's memory, it doesn't look anything like a value written on this page.

For example, to type a value of type char in a program, you must surround it with a pair of single quote marks, such as 'A', '\*', or 'x'. The character and the quote marks make up a literal of type char. Without the quotes, A would be an identifier and \* would be a multiplication operator.

```
ch = 'A';
```

#### escape character

In particular, a tab is represented as '\t', a carriage return as '\r', a linefeed as '\n', the single quote character as ''', and the backslash itself as '\\'.

#### Numeric literals

* there are the obvious literals such as 317 and 17.42.
* real numbers can be represented in an exponential form such as 1.3e12 or 12.3737e-108. The "e12" and "e-108" represent powers of 10, so that 1.3e12 means 1.3 times 1012 and 12.3737e-108 means 12.3737 times 10-108.
* "1.2F" stands for 1.2 considered as a value of type float.
* You can make a literal of type long by adding "L" as a suffix.
* In Java, a hexadecimal literal begins with 0x or 0X, as in 0x45 or 0xFF7A.
* numeric literals can include the underscore character ("\_"), which can be used to separate groups of digits. For example, the integer constant for two billion could be written 2\_000\_000\_000, which is a good deal easier to decipher than 2000000000.

#### Char

hexadecimal numbers can also be used in character literals to represent arbitrary Unicode characters. The character literal '\u00E9' represents the Unicode character that is an "e" with an acute accent.

#### Boolean

two literals: true and false.

```java
import static net.mindview.util.Print.*;

public class Literals {
  public static void main(String[] args) {
    int i1 = 0x2f; // Hexadecimal (lowercase)
    print("i1: " + Integer.toBinaryString(i1));
    int i2 = 0X2F; // Hexadecimal (uppercase)
    print("i2: " + Integer.toBinaryString(i2));
    int i3 = 0177; // Octal (leading zero)
    print("i3: " + Integer.toBinaryString(i3));
    char c = 0xffff; // max char hex value
    print("c: " + Integer.toBinaryString(c));
    byte b = 0x7f; // max byte hex value
    print("b: " + Integer.toBinaryString(b));
    short s = 0x7fff; // max short hex value
    print("s: " + Integer.toBinaryString(s));
    long n1 = 200L; // long suffix
    long n2 = 200l; // long suffix (but can be confusing)
    long n3 = 200;
    float f1 = 1;
    float f2 = 1F; // float suffix
    float f3 = 1f; // float suffix
    double d1 = 1d; // double suffix
    double d2 = 1D; // double suffix
    // (Hex and Octal also work with long)
  }
} /* Output:
i1: 101111
i2: 101111
i3: 1111111
c: 1111111111111111
b: 1111111
s: 111111111111111
*///:~
```

### double

#### Never use == with doubles

```java
double x = Math.sqrt(2.0);
double y = x * x;
if (y == 2.0) {
    System.out.println("sqrt(2) * sqrt(2) is 2");
} else {
    System.out.println("sqrt(2) * sqrt(2) “ + “is not 2. It is " + y);
}
```

#### Test if doubles are close

```java
public static boolean almostEqual(double x, double y) {
    double tolerance = 1E-15;
    return Math.abs(x - y) < tolerance;
}
```

### String and String Literals

String is a type, but not a primitive type; it is in fact the name of a class, and we will return to that aspect of strings

* A value of type String is a sequence of characters.
* The double quotes are part of the literal; they have to be typed in the program.
* A string can contain any number of characters, even zero.
* There is a big difference between the String "A" and the char 'A'.

### Variables in Programs

A variable can be used in a program only if it has first been **declared**. A **variable declaration statement** is used to declare one or more variables and to give them names. When the computer executes a variable declaration, it **sets aside memory for the variable** and **associates the variable's name with that memory**.

Good programming style is to declare only one variable in a declaration statement, unless the variables are closely related in some way.

```java
int numberOfStudents;
String name;
double x, y;        
boolean isFinished;
char firstInitial, middleInitial, lastInitial;
```

declare include a comment with each variable declaration

```java
double principal;    // Amount of money invested.
double interestRate; // Rate as a decimal, not percentage.
```

* Variables declared inside a subroutine are called **local variables** for that subroutine. They exist only inside the subroutine, while it is running, and are completely inaccessible from outside.
* Variable declarations can occur anywhere inside the subroutine, as long as each variable is declared before it is used in any way.
* Declare important variables at the beginning of the subroutine, and use a comment to explain the purpose of each variable.

```java
/**
 * This class implements a simple program that
 * will compute the amount of interest that is
 * earned on $17,000 invested at an interest
 * rate of 0.027 for one year.  The interest and
 * the value of the investment after one year are
 * printed to standard output.
 */
 
public class Interest {
   
   public static void main(String[] args) {
   
       /* Declare the variables. */
   
       double principal;     // The value of the investment.
       double rate;          // The annual interest rate.
       double interest;      // Interest earned in one year.
       
       /* Do the computations. */
       
       principal = 17000;
       rate = 0.027;
       interest = principal * rate;   // Compute the interest.
       
       principal = principal + interest;
             // Compute value of investment after one year, with interest.
             // (Note: The new value replaces the old value of principal.)
             
       /* Output the results. */
             
       System.out.print("The interest earned is $");
       System.out.println(interest);
       System.out.print("The value of the investment after one year is $");
       System.out.println(principal);
                      
   } // end of main()
      
} // end of class Interest
```

### Java Operators

#### Arithmetic Operators

**+, -, \*, /**

* \+(addition), -(subtraction), \*(multiplication), /(division)
* These operations can be used on values of any numeric type: byte, short, int, long, float, or double.
* If this operators are used in char, treated as integers in this context; a char is converted into its Unicode code number when it is used with an arithmetic operator.
* If your program tells the computer to combine two values of different types, the computer will convert one of the values from one type to another. This is called a type conversion.

**type conversion**

![](https://ossp.pengjunjie.com/mweb/16378234366932.jpg)

**Widening conversion preserves magnitude**

* Widening conversions convert data to another type that has the same or more bits of storage.
* short to int, long (safe)
* int to long (safe)
* int to float, double (magnitude the same but can lose precision)

**Narrowing conversion can lose information**

* Narrowing conversions convert data to another type that has the fewer bits of storage!
* int, long to short
  * Keeps low order bits only (can loose magnitude and sign)!
* double or float to any integer type
  * Rounds towards 0, then keeps low order bits
  * Or largest/smallest value (lose magnitude)!

**Promotion is widening conversion done automatically**

When a Java operator is applied to operands of different types, Java does a widening conversion automatically, known as a promotion.

Example:

* 2.2 \* 2 evaluates to 4.4
* 1.0 / 2 evaluates to 0.5
* double x = 2; assigns 2.0 to x
* "count = " + 4 evaluates to "count = 4"

**Type casting tells Java to convert one type to another.**

Uses:

* Convert an int to a double to force floating-point division.
* Truncate a double to an int.

Examples:

* int total = 17;
* double average = (double) total / 5
* int feet = (int) (28.3 / 12.0)

**Type casting applies to only operand immediately to its right.**

Type casting has high precedence and is evaluated right to left.

![](https://ossp.pengjunjie.com/mweb/16384795139849.jpg)

**Modulus %**

%(Modulus): computing the remainder when one number is divided by another.

% is not quite the same as the usual mathematical "modulus" operator, since if one of A or B is negative, then the value of A % B will be negative.

#### Increment and Decrement

\++(increment operator)

\--(decrement operator)

These operators can be used on variables belonging to any of the numerical types and also on variables of type char.

* `y = x++` the value assigned to y is the old value of x
* `y = ++x` ++x is defined to be the new value of x
* `x = x++` does not change the value of x

The same with --

```java
counter  =  counter + 1;
goalsScored  =  goalsScored + 1;

counter++;
goalsScored++;

counter--;
goalsScored--;
```

```java
import static net.mindview.util.Print.*;

public class AutoInc {
    public static void main(String[] args) {
        int i = 1;
        print("i : " + i); 
        print("++i : " + ++i); // Pre-increment
        print("i++ : " + i++); // Post-increment
        print("i : " + i);
        print("--i : " + --i); // Pre-decrement
        print("i-- : " + i--); // Post-decrement
        print("i : " + i);
    }
}
```

#### Relational Operators

Relational operators are used to test whether two values are equal, whether one value is greater than another, and so forth.

```
A == B       Is A "equal to" B?
A != B       Is A "not equal to" B?
A < B        Is A "less than" B?
A > B        Is A "greater than" B?
A <= B       Is A "less than or equal to" B?
A >= B       Is A "greater than or equal to" B?
```

you cannot do with the relational operators <, >, <=, and >= is to use them to compare values of type String or Object. The == operator checks whether two objects are stored in the same memory location, rather than whether they contain the same value. You should compare strings using subroutines such as equals() and compareTo()

```java
public class Equivalence {
    public static void main(String[] args) {
        Integer n1 = Integer.valueOf(47);
        Integer n2 = Integer.valueOf(47);
        System.out.println(n1 == n2);
        System.out.println(n1 != n2);

        Integer n3 = new Integer(47);
        Integer n4 = new Integer(47);
        System.out.println(n3 == n4);
        System.out.println(n3 != n4);
        System.out.println(n3.equals(n4));
    }
}
```

#### Boolean Operators

* &&(and)
* ||(or)
* !(not)

```java
import java.util.*;
import static net.mindview.util.Print.*;

public class Bool {
    public static void main(String[] args) {
        Random rand = new Random(47);
        int i = rand.nextInt(100);
        int j = rand.nextInt(100);
        print("i = " + i);
        print("j = " + j);
        print("i > j is " + (i > j));
        print("i < j is " + (i < j));
        print("i >= j is " + (i >= j));
        print("i <= j is " + (i <= j));
        print("i == j is " + (i == j));
        print("i != j is " + (i != j));
        // Treating an int as a boolean is not legal Java:
        // ! print("i && j is " + (i && j));
        // ! print("i || j is " + (i || j));
        // ! print("!i is " + !i);

        print("(i < 10) && (j < 10) is " + ((i < 10) && (j < 10)) );

        print("(i < 10) || (j < 10) is " + ((i < 10) || (j < 10)) );
    }
}/* Output:
i = 58
j = 55
i > j is true
i < j is false
i >= j is true
i <= j is false
i == j is false
i != j is true
(i < 10) && (j < 10) is false
(i < 10) || (j < 10) is false
*///:~
```

The operators && and || are said to be short-circuited versions of the boolean operators. This means that the second operand of && or || is not necessarily evaluated.

```java
package group.collapsar.java.basic.week2;
import static net.mindview.util.Print.*;

public class ShortCircuit {
    static boolean test1(int val) {
        print("test1(" + val + ")");
        print("result: " + (val < 1));
        return val < 1;
    }

    static boolean test2(int val) {
        print("test2(" + val + ")");
        print("result: " + (val < 2));
        return val < 2;
    }

    static boolean test3(int val) {
        print("test3(" + val + ")");
        print("result: " + (val < 3));
        return val < 3;
    }
    public static void main(String[] args) {
        boolean b = test1(0) && test2(2) && test3(2);
        print("expression is " + b);
    }
}
```

#### Conditional Operator

`boolean-expression ? expression1 : expression2`

```java
next = (N % 2 == 0) ? (N/2) : (3*N+1);
```

```java
public class ConditionalOperator {
    public static void main(String[] args) {
        int a = 3, b = 5;
        int max = 0;
        if (a > b) {
            max = a;
        } else {
            max = b;
        }

        int new_max = a > b ? a : b;
        int new_min = a < b ? a : b;
        int new_1_min = a > b ? b : a;
    }
}
```

#### Assignment Operators and Type Conversion

\= is really an operator in the sense that an assignment can itself be used as an expression or as part of a more complex expression.

```java
if ( (A=B) == 0 )...
//don't do things like that
```

**Type cast**

```java
int A;
double X;
short B;
A = 17;
X = A;    // OK; A is converted to a double
B = A;    // illegal; no automatic conversion
          //       from int to short
```

#### >>>

```java
// Test of unsigned right shift.
import static net.mindview.util.Print.*;

public class URShift {
  public static void main(String[] args) {
    int i = -1;
    print(Integer.toBinaryString(i));
    i >>>= 10;
    print(Integer.toBinaryString(i));
    long l = -1;
    print(Long.toBinaryString(l));
    l >>>= 10;
    print(Long.toBinaryString(l));
    short s = -1;
    print(Integer.toBinaryString(s));
    s >>>= 10;
    print(Integer.toBinaryString(s));
    byte b = -1;
    print(Integer.toBinaryString(b));
    b >>>= 10;
    print(Integer.toBinaryString(b));
    b = -1;
    print(Integer.toBinaryString(b));
    print(Integer.toBinaryString(b>>>10));
  }
} /* Output:
11111111111111111111111111111111
1111111111111111111111
1111111111111111111111111111111111111111111111111111111111111111
111111111111111111111111111111111111111111111111111111
11111111111111111111111111111111
11111111111111111111111111111111
11111111111111111111111111111111
11111111111111111111111111111111
11111111111111111111111111111111
1111111111111111111111
*///:~
```

#### Precedence Rules

```java
public class Precedence {
    public static void main(String[] args) {
        int x = 1, y = 2, z = 3;
        int a = x + y - 2/2 + z;
        int b = x + (y - 2)/(2 + z);
        System.out.println("a = " + a + " b = " + b);
    }
}
```

![](https://ossp.pengjunjie.com/mweb/16378240492144.jpg)

![](https://ossp.pengjunjie.com/mweb/16378237086332.jpg)
