# \[course04] 01 Build-in Subrouting and Functions

### static

static members of the class.

```java
public static void main(String[] args){
...
}
```

When a class contains a static variable or subroutine, the name of the class is part of the full name of the variable or subroutine.

### Exit

```java
System.exit(0);
```

Calling System.exit will terminate the program and shut down the Java Virtual Machine. You could use it if you had some reason to terminate the program before the end of the main routine.

### Math

[Dev docs Math](https://devdocs.io/openjdk\~11/java.base/java/lang/math)

import math method:

* `Math.abs(x)`
* `Math.sin(x)`, `Math.cos(x)`, and `Math.tan(x)`
* `Math.asin(x)`, `Math.acos(x)`, and `Math.atan(x)`
* `Math.exp(x)`, `Math.log(x)`
* `Math.pow(x,y)`
* `Math.floor(x)`, `Math.ceil(x)`, `Math.round(x)`
* `Math.random`

```java
/**
 * This program performs some mathematical computations and displays the
 * results.  It also displays the value of the constant Math.PI.  It then 
 * reports the number of seconds that the computer spent on this task.
 */
public class TimedComputation {

    public static void main(String[] args) {

        long startTime; // Starting time of program, in nanoseconds.
        long endTime;   // Time when computations are done, in nanoseconds.
        long compTime;  // Run time in nanoseconds.
        double seconds; // Time difference, in seconds.

        startTime = System.nanoTime();

        double width, height, hypotenuse;  // sides of a triangle
        width = 42.0;
        height = 17.0;
        hypotenuse = Math.sqrt( width*width + height*height );
        System.out.print("A triangle with sides 42 and 17 has hypotenuse ");
        System.out.println(hypotenuse);

        System.out.println("\nMathematically, sin(x)*sin(x) + "
                + "cos(x)*cos(x) - 1 should be 0.");
        System.out.println("Let's check this for x = 100:");
        System.out.print("      sin(100)*sin(100) + cos(100)*cos(100) - 1 is: ");
        System.out.println( Math.sin(100)*Math.sin(100) 
                + Math.cos(100)*Math.cos(100) - 1 );
        System.out.println("(There can be round-off errors when" 
                + " computing with real numbers!)");

        System.out.print("\nHere is a random number:  ");
        System.out.println( Math.random() );

        System.out.print("\nThe value of Math.PI is ");
        System.out.println( Math.PI );

        endTime = System.nanoTime();
        compTime = endTime - startTime;
        seconds = compTime / 1000000000.0;

        System.out.print("\nRun time in nanoseconds was: ");
        System.out.println(compTime);
        System.out.println("(This is probably not perfectly accurate!");
        System.out.print("\nRun time in seconds was:  ");
        System.out.println(seconds);

    } // end main()

} // end class TimedComputation
```

* Random object
* Random methods:
  * nextInt()
  * nextFloat()
  * nextLong()
  * nextDouble()
  * nextInt()

```java
package group.collapsar.java.basic.week2;

import java.util.*;
import static net.mindview.util.Print.*;

public class MathOps {
    public static void main(String[] args) {
        // Create a seeded random number generator:
        Random rand = new Random(47);
        int i, j, k; // Choose value from 1 to 100:
        j = rand.nextInt(100) + 1;
        print("j : " + j);
        k = rand.nextInt(100) + 1;
        print("k : " + k);
        i = j + k;
        print("j + k : " + i);
        i = j - k;
        print("j - k : " + i);
        i = k / j;
        print("k / j : " + i);
        i = k * j;
        print("k * j : " + i);
        i = k % j;
        print("k % j : " + i);
        j %= k;
        print("j %= k : " + j); // Floating-point number tests:
        float u, v, w; // Applies to doubles, too
        v = rand.nextFloat();
        print("v : " + v);
        w = rand.nextFloat();
        print("w : " + w);
        u = v + w;
        print("v + w : " + u);
        u = v - w;
        print("v - w : " + u);
        u = v * w;
        print("v * w : " + u);
        u = v / w;
        print("v / w : " + u); // The following also works for char, // byte, short, int, long, and double:
        u += v;
        print("u += v : " + u);
        u -= v;
        print("u -= v : " + u);
        u *= v;
        print("u *= v : " + u);
        u /= v;
        print("u /= v : " + u);
    }
}
```

use the round( ) methods in java.lang.Math

```java
// Rounding floats and doubles.
import static net.mindview.util.Print.*;

public class RoundingNumbers {
  public static void main(String[] args) {
    double above = 0.7, below = 0.4;
    float fabove = 0.7f, fbelow = 0.4f;
    print("Math.round(above): " + Math.round(above));
    print("Math.round(below): " + Math.round(below));
    print("Math.round(fabove): " + Math.round(fabove));
    print("Math.round(fbelow): " + Math.round(fbelow));
  }
} /* Output:
Math.round(above): 1
Math.round(below): 0
Math.round(fabove): 1
Math.round(fbelow): 0
*///:~
```

### Time functions

`System.currentTimeMillis()`

```java
/**
 * This program performs some mathematical computations and displays the
 * results.  It also displays the value of the constant Math.PI.  It then 
 * reports the number of seconds that the computer spent on this task.
 */
public class TimedComputation {

    public static void main(String[] args) {

        long startTime; // Starting time of program, in nanoseconds.
        long endTime;   // Time when computations are done, in nanoseconds.
        long compTime;  // Run time in nanoseconds.
        double seconds; // Time difference, in seconds.

        startTime = System.nanoTime();

        double width, height, hypotenuse;  // sides of a triangle
        width = 42.0;
        height = 17.0;
        hypotenuse = Math.sqrt( width*width + height*height );
        System.out.print("A triangle with sides 42 and 17 has hypotenuse ");
        System.out.println(hypotenuse);

        System.out.println("\nMathematically, sin(x)*sin(x) + "
                + "cos(x)*cos(x) - 1 should be 0.");
        System.out.println("Let's check this for x = 100:");
        System.out.print("      sin(100)*sin(100) + cos(100)*cos(100) - 1 is: ");
        System.out.println( Math.sin(100)*Math.sin(100) 
                + Math.cos(100)*Math.cos(100) - 1 );
        System.out.println("(There can be round-off errors when" 
                + " computing with real numbers!)");

        System.out.print("\nHere is a random number:  ");
        System.out.println( Math.random() );

        System.out.print("\nThe value of Math.PI is ");
        System.out.println( Math.PI );

        endTime = System.nanoTime();
        compTime = endTime - startTime;
        seconds = compTime / 1000000000.0;

        System.out.print("\nRun time in nanoseconds was: ");
        System.out.println(compTime);
        System.out.println("(This is probably not perfectly accurate!");
        System.out.print("\nRun time in seconds was:  ");
        System.out.println(seconds);

    } // end main()

} // end class TimedComputation
```
