# \[course03] 02 While Loops

### The Basic While Loop

A while loop is used to repeat a given statement over and over. Of course, it's not likely that you would want to keep repeating it forever. That would be an infinite loop, which is generally a bad thing

```java
while (boolean-expression)
     statement
     
// with block

while (boolean-expression) {
    statements
}
```

![](https://ossp.pengjunjie.com/mweb/16379470189559.jpg)

When the computer comes to a while statement, it evaluates the boolean-expression, which yields either true or false as its value. If the value is false, the computer skips over the rest of the while loop and proceeds to the next command in the program. If the value of the expression is true, the computer executes the statement or block of statements inside the loop.

example : a while loop that simply prints out the numbers 1, 2, 3, 4, 5

```java
int number;   // The number to be printed.
number = 1;   // Start with 1.
while ( number < 6 ) {  // Keep going as long as number is < 6.
    System.out.println(number);
    number = number + 1;  // Go on to the next number.
}
System.out.println("Done!");
```

### The do...while Statement

```java
do
    statement
while ( boolean-expression );

//with block
do {
    statements
} while ( boolean-expression );
```

example:

```java
boolean wantsToContinue;  // True if user wants to play again.
do {
   Checkers.playGame();
   System.out.print("Do you want to play again? ");
   Scanner keyboard = new Scanner(System.in);
   wantsToContinue = keyboard.nextBoolean();
} while (wantsToContinue == true);
```

do while and while do

```java
do {
    doSomething
} while ( boolean-expression );

//has exactly the same effect as

doSomething
while ( boolean-expression ) {
    doSomething
}

while ( boolean-expression ) {
    doSomething
} 

// can be replaced by

if ( boolean-expression ) {
   do {
       doSomething
   } while ( boolean-expression );
}
```

### break and continue

When the computer executes a **break** statement in a loop, it will immediately jump out of the loop.

```java
while (true) {  // looks like it will run forever!
   System.out.print("Enter a positive number: ");
   N = TextIO.getlnInt();
   if (N > 0)   // the input value is OK, so jump out of loop
      break;
   System.out.println("Your answer must be > 0.");
}
// continue here after break
```

The continue statement is related to break, but less commonly used. A continue statement tells the computer to skip the rest of the current iteration of the loop. However, instead of jumping out of the loop altogether, it jumps back to the beginning of the loop and continues with the next iteration

### example

```java
// Demonstrates the while loop.

public class WhileTest {
  static boolean condition() {
    boolean result = Math.random() < 0.99;
    System.out.print(result + ", ");
    return result;
  }
  public static void main(String[] args) {
    while(condition())
      System.out.println("Inside 'while'");
    System.out.println("Exited 'while'");
  }
} /* (Execute to see output) *///:~
```
