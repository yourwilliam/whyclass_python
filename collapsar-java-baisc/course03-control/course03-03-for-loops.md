# \[course03] 03 for loops

### For Loops

while loops general form

```java
initialization
while ( continuation-condition ) {
    statements
    update
}
```

```java
years = 0;  // initialize the variable years
while ( years < 5 ) {   // condition for continuing loop

    interest = principal * rate;    //
    principal += interest;          // do three statements
    System.out.println(principal);  //
    
    years++;   // update the value of the variable, years
}

// the same as 

for ( years = 0;  years < 5;  years++ ) {
   interest = principal * rate;
   principal += interest;
   System.out.println(principal);
}
```

syntax:

```java
for ( initialization; continuation-condition; update )
     statement

//with block 

for ( initialization; continuation-condition; update ) {
     statements
}
```

![](https://ossp.pengjunjie.com/mweb/16379507320345.jpg)

```java
for ( N = 1 ;  N <= 10 ;  N++ )
   System.out.println( N );
   
for ( N = 0 ;  N < 10 ;  N++ )
   System.out.println( N );
   
for ( N = 10 ;  N >= 1 ;  N-- )
   System.out.println( N );      

for ( i=1, j=10;  i <= 10;  i++, j-- ) {
   System.out.printf("%5d", i); // Output i in a 5-character wide column.
   System.out.printf("%5d", j); // Output j in a 5-character column.
   System.out.println();       //     and end the line.
}

// Print out the alphabet on one line of output.
char ch;  // The loop control variable; 
          //       one of the letters to be printed.
for ( ch = 'A';  ch <= 'Z';  ch++ )
    System.out.print(ch);
System.out.println();
```

### examples: how many different letters were found

```java
import group.collapsar.java.basic.TextIO;

/**
 * This program reads a line of text entered by the user.
 * It prints a list of the letters that occur in the text,
 * and it reports how many different letters were found.
 */
public class ListLetters {

    public static void main(String[] args) {

        String str;  // Line of text entered by the user.
        int count;   // Number of different letters found in str.
        char letter; // A letter of the alphabet.

        System.out.println("Please type in a line of text.");
        str = TextIO.getln();

        str = str.toUpperCase();

        count = 0;
        System.out.println("Your input contains the following letters:");
        System.out.println();
        System.out.print("   ");
        for ( letter = 'A'; letter <= 'Z'; letter++ ) {
            int i;  // Position of a character in str.
            for ( i = 0; i < str.length(); i++ ) {
                if ( letter == str.charAt(i) ) {
                    System.out.print(letter);
                    System.out.print(' ');
                    count++;
                    break;
                }
            }
        }

        System.out.println();
        System.out.println();
        System.out.println("There were " + count + " different letters.");

    } // end main()

} // end class ListLetters
```

### example : Demonstrates "for" loop by listing

```java
// Demonstrates "for" loop by listing
// all the lowercase ASCII letters.

public class ListCharacters {
  public static void main(String[] args) {
    for(char c = 0; c < 128; c++)
      if(Character.isLowerCase(c))
        System.out.println("value: " + (int)c +
          " character: " + c);
  }
} /* Output:
value: 97 character: a
value: 98 character: b
value: 99 character: c
value: 100 character: d
value: 101 character: e
value: 102 character: f
value: 103 character: g
value: 104 character: h
value: 105 character: i
value: 106 character: j
...
*///:~
```

### ForEach syntax

foreach syntax means that you don’t have to create an int to count through a sequence of items—the foreach produces each item for you, automatically.

```java
import java.util.*;

public class ForEachFloat {
  public static void main(String[] args) {
    Random rand = new Random(47);
    float f[] = new float[10];
    for(int i = 0; i < 10; i++)
      f[i] = rand.nextFloat();
    for(float x : f)
      System.out.println(x);
  }
} /* Output:
0.72711575
0.39982635
0.5309454
0.0534122
0.16020656
0.57799757
0.18847865
0.4170137
0.51660204
0.73734957
*///:~
```

```java
import static net.mindview.util.Range.*;
import static net.mindview.util.Print.*;

public class ForEachInt {
  public static void main(String[] args) {
    for(int i : range(10)) // 0..9
      printnb(i + " ");
    print();
    for(int i : range(5, 10)) // 5..9
      printnb(i + " ");
    print();
    for(int i : range(5, 20, 3)) // 5..20 step 3
      printnb(i + " ");
    print();
  }
} /* Output:
0 1 2 3 4 5 6 7 8 9
5 6 7 8 9
5 8 11 14 17
*///:~
```

```java
public class ForEachString {
  public static void main(String[] args) {
    for(char c : "An African Swallow".toCharArray() )
      System.out.print(c + " ");
  }
} /* Output:
A n   A f r i c a n   S w a l l o w
*///:~
```

```java
import static net.mindview.util.Range.*;
import static net.mindview.util.Print.*;

public class ForEachInt {
  public static void main(String[] args) {
    for(int i : range(10)) // 0..9
      printnb(i + " ");
    print();
    for(int i : range(5, 10)) // 5..9
      printnb(i + " ");
    print();
    for(int i : range(5, 20, 3)) // 5..20 step 3
      printnb(i + " ");
    print();
  }
} /* Output:
0 1 2 3 4 5 6 7 8 9
5 6 7 8 9
5 8 11 14 17
*///:~
```
