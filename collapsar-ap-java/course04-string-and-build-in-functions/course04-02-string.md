# \[course04] 02 String

## \[course04] 02 String

### Strings

String is a class, and a value of type String is an object. That object contains data, namely the sequence of characters that make up the string. It also contains subroutines. All of these subroutines are in fact functions.

```java
String advice;
advice = "Seize the day!";

String day = "new day";
String username = new String("Joh");
username = "Harry";

```

```java
System.out.print("The number of characters in ");
System.out.print("the string \"Hello World\" is ");
System.out.println( "Hello World".length() );
```

* String is not a primitive type, but a class/type
* String variables store references to memory addresses
* Strings are immutable! That is, you cannot change a string, but you can assign a new string to a variable.
* A string cannot span more than one line

### Java escape sequence

![](http://ossp.pengjunjie.com/mweb/16378312181359.jpg)

### String is a sequence of (unicode) characters

When we declare a variable of type String, it does not create an object. `String founder;`

To create an object we use the new operator:

```java
founder = new String("Carnegie"); 
```

Strings have a shortcut way of creating them:

```java
String founder2 = "Mellon"; 
```

difference the two types

### Object vs Primitive Data

![](http://ossp.pengjunjie.com/mweb/16378315081520.jpg)

[devdocs java](https://devdocs.io/openjdk\~11/java.base/java/lang/string)

* `s1.equals(s2)`
* `s1.equalsIgnoreCase(s2)`
* `s1.length()`
* `s1.charAt(N)`
* `s1.substring(N,M)`and `s1.substring(N)`
* `s1.indexOf(s2)` and s1.lastIndexOf(x)
* `s1.compareTo(s2)` and `s1.compareToIgnoreCase(s2)`
* `s1.toUpperCase()` and `s1.toLowerCase()`
* `s1.trim()`

#### immutable feature of String

```java
public static void main(String[] args) {
    String s="Sachin";
    s.concat(" Tendulkar");//concat() method appends the string at the end
    System.out.println(s);//will print Sachin because strings are immutable objects

    String newS = s.concat(" Tendulkar");
    System.out.println(newS);
}
```

#### The concatenation operator

```java
public static void main(String[] args) {
    int fiYe = 5;

    String state = "HaZaii-";

    String tvShow = state + five + "-0"; //tvShow has value "HaZaii-5-0"

    System.out.println(tvShow);

    int x = 3, y = 4;

    //String sXm = x + y; //error: can’t assign int 7 to String

    Date d1 = new Date(8, 2, 1947);
    Date d2 = new Date(2, 17, 1948);
    String s = "My birthday is " + d2;

    //String s2 = d1 + d2;   //error: + not defined for objects
    String s3 = d1.toString() + d2.toString();
    System.out.println(s3);

}
```

#### use equals to compare String

```java
public static void main(String[] args) {

    String a1 = "hello";
    String a2 = "hello";
    System.out.println(a1 == a2);

    String b1 = new String("hello");
    String b2 = new String("hello");
    System.out.println(b1 == b2);


    String s1 = "hello";
    String s2 = "world";
    String s3 = "helloworld";
    String s4 = s1 + s2;
    System.out.println(s3 == s4);
    System.out.println(System.identityHashCode(s3));
    System.out.println(System.identityHashCode(s4));

    String s5= s1;

    System.out.println(s1 == s5);
    System.out.println(System.identityHashCode(s1));
    System.out.println(System.identityHashCode(s5));

    s1 = s1+s2;
    System.out.println(s1 == s3);
    System.out.println(System.identityHashCode(s1));
    System.out.println(System.identityHashCode(s3));

    System.out.println(s1.equals(s3));
    String str1 = "HOT";
    String str2 = "HOTEL";
    String str3 = "dog";

    System.out.println(str1.compareTo(str2));
    System.out.println(str1.compareTo(str3));
}
```

[String pool](https://www.cnblogs.com/Andya/p/14067618.html)

### Substring

[substring](https://devdocs.io/openjdk\~11/java.base/java/lang/string#substring\(int\))

### Replacing Characters

[replace](https://devdocs.io/openjdk\~11/java.base/java/lang/string#replace\(char,char\))

### Compare the lexicographical order of two strings

[compareTo](https://devdocs.io/openjdk\~11/java.base/java/lang/string#compareTo\(java.lang.String\))

### Enums

An enum is a type that has a fixed list of possible values, which is specified when the enum is created.

```java
public class EnumDemo {
 
       // Define two enum types -- remember that the definitions
       // go OUTSIDE the main() routine!
  
    enum Day { SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY }
      
    enum Month { JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC }
     
    public static void main(String[] args) {
       
         Day tgif;     // Declare a variable of type Day.
         Month libra;  // Declare a variable of type Month.
       
         tgif = Day.FRIDAY;    // Assign a value of type Day to tgif.
         libra = Month.OCT;    // Assign a value of type Month to libra.
           
         System.out.print("My sign is libra, since I was born in ");
         System.out.println(libra);   // Output value will be:  OCT
         System.out.print("That's the ");
         System.out.print( libra.ordinal() );
         System.out.println("-th month of the year.");
         System.out.println("   (Counting from 0, of course!)");
         
         System.out.print("Isn't it nice to get to ");
         System.out.println(tgif);   // Output value will be:  FRIDAY
          
         System.out.println( tgif + " is the " + tgif.ordinal() 
                                            + "-th day of the week.");
    }
   
}

```

### Multiline Strings

""" text blocks, this is only supported in Java 15

```java
String poem = """ 
    As I was walking down the stair,
       I met a man who wasn't there.
    He wasn't there again today.
       I wish, I wish he'd go away!""";
```

Java 8 multiline Strings

```java
String poem = "As I was walking down the stair,\n"
    + "   I met a man who wasn't there.\n"
    + "He wasn't there again today.\n"
    + "   I wish, I wish he'd go away!\n";
```

### Letter Counter

#### Java Version

```java
import java.util.Scanner;

public class LetterCounter1 {
    
    // Asks the user for a message and then prints the
    // number of times each letter appears in the message
    public static void main(String[] args) {
        
        String alphabet = "abcdefghijklmnopqrstuvwxyz";
         // or String alphabet = new String("abcdefghijklmnopqrstuvwxyz");
        
        System.out.println("Enter a message.");
        
        // Get the input from the user using Scanner 
        Scanner keyboard = new Scanner(System.in);
        String message = keyboard.nextLine().toLowerCase();
        
        // loop through each letter in the alphabet
        // and print the count of it in message
        for (int i = 0; i < 26; i++) {
            char letter = alphabet.charAt(i);
            int numLetters = count(letter, message);
            if (numLetters > 0) {
                System.out.println(letter + " " + numLetters);
            }
        }        
    }
    
    // Returns the number of times ch occurs in the text
    public static int count(char ch, String text) {
        
        // loop through each character in the message 
        // and see if it is the same as ch
        int counter = 0;
        for (int i = 0; i < text.length(); i++) {
            
            if (text.charAt(i) == ch) {
                counter++;
            }           
        }
        
        return counter;
        
    }
}
```

#### Python Version

```python
# Asks the user for a message and then prints the
# number of times each letter appears in the message

def letter_counter():

    alphabet = "abcdefghijklmnopqrstuvwxyz"
    message = input("Enter a message.\n")

    for i in range(26):
        letter = alphabet[i]
        numLetters = count(letter, message)
        if numLetters > 0:
            print(letter + " " + str(numLetters))
        

def count(ch, text):
    counter = 0
    
    for i in range(len(text)):
        if text[i] == ch:
            counter = counter + 1
            
    return counter


letter_counter()
    
```

### String demo

```java
public class StringDemo {
    
    public static void main(String[] args) {
        String s = "a";
        System.out.println("s = \""+ s + "\"");
        System.out.println("s.length: " + s.length());
        System.out.println();

        s = "ab";
        System.out.println("s = \""+ s + "\"");       
        System.out.println(" s.charAt(0): " + s.charAt(0));
        System.out.println(" (int)s.charAt(0): " + (int)s.charAt(0));
        System.out.println(" s.length: " + s.length());
        System.out.println();
     
        s = "";
        System.out.println("s = \""+ s + "\"");    
        System.out.println(" s.length: " + s.length());
        System.out.print(" s.length == 0 ");        
        System.out.println(s.length() == 0);
        System.out.print(" s == null ");    
        System.out.println(s == null);
        System.out.println();
       
        s = null;
        System.out.println(" s = null ");
        System.out.print(" s == null ");
        System.out.println(s == null);
        //System.out.print("s.length: " );
        //System.out.println(s.length());
        //int i = null;
        System.out.println();
                
        s = "hello world";
        System.out.println("s = \""+ s + "\"\ns.contains(\"lo\":) ");
        System.out.println(s.contains("lo"));
        System.out.println();
        
        // comparisons
        System.out.println("compareTo: ");
        System.out.println("word vs work " + "word".compareTo("work"));
        System.out.println("word vs words " + "word".compareTo("words"));
        System.out.println("word vs wor " + "word".compareTo("wor"));
        System.out.println("word equals work " + "word".equals("work"));
        System.out.println();
      
        // equality
        String ab = "ab";
        String cd = "cd";
        String s1 = "abcd";
        String s2 = ab + cd;
        String s3 = "ab" + "cd";
        String s4 = "ab".concat("cd");
        // Note that s1, s2, s3, and s4 all hold the characters "abcd"
        System.out.println("See how equals works as expected for ALL of them:");
        System.out.println(s1.equals(s2));
        System.out.println(s1.equals(s3));
        System.out.println(s1.equals(s4));
        System.out.println();
        System.out.println("But == only works as expected for SOME of them:");
        System.out.println(s1 == s2);
        System.out.println(s1 == s3);
        System.out.println(s1 == s4);
        // Moral of the story: Do NOT use "==" with Strings -- the results are unpredictable!
        System.out.println();
      
        // a pattern using concat to build a result string
        // CAUTION - do NOT use if you're constructing a LOT of Strings!
        // Once we start using Objects, I will show you a better way...
        String result = "";
        for (int i = 0; i < 10; i++) {
            result += "Margaret";
        }
        System.out.println(result);

    }
 }

```
