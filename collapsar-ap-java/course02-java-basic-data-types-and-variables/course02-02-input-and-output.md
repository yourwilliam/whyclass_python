# \[course02] 02 Input and Output

## \[course02] 02 Input and Output

#### input

```java
import java.util.Scanner;

public class ForgetfulMachine {
    public static void main( String[] args ) {
        Scanner keyboard = new Scanner(System.in);

        System.out.println( "What city is the capital of France?" );
        String nextStr = keyboard.next();
        System.out.println("Your answer: " + nextStr);

        System.out.println( "What is 6 multiplied by 7?" );
        int nextInt = keyboard.nextInt();
        System.out.println("Your answer: " + nextInt);

        System.out.println( "Enter a number between 0.0 and 1.0." );
        double nextDouble = keyboard.nextDouble();
        System.out.println("Your answer: " + nextDouble);

        System.out.println( "Is there anything else you would like to say?" );
        String nextStr1 = keyboard.next();
        System.out.println("Your answer: " + nextStr1);

    }
}
```

[Devdocs Scanner](https://devdocs.io/openjdk\~11/java.base/java/util/scanner)

#### Output

```java

public static void main(String[] args) {
    System.out.print("Hot");
    System.out.println("dog");

    System.out.println("Hot");
    System.out.println("Hot");

    System.out.println(7 + 3);

    System.out.println(7 == 2 + 5);

    int x = 27;
    System.out.println(x);
    System.out.println("Value of x is " + x);
}

```
