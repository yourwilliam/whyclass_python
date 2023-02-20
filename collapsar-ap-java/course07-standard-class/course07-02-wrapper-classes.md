# \[course07]02 Wrapper classes

## \[course07]02 Wrapper classes

A wrapper class takes either an existing object or a value of primitive type, “wraps” or “boxes” it in an object, and provides a new set of methods for that type.

### Integer class

```java
// Constructs an Integer object from an int. (Boxing.)
Integer(int value)

//Returns the value of this Integer as an int. (Unboxing.)
int intValue()

//A constant equal to the minimum value represented by an int or Integer.
Integer.MIN_VALUE

//A constant equal to the maximum value represented by an int or Integer.
Integer.MAX_VALUE

```

example:

```java
Integer a = new Integer(10);
int b = a.intValue();
System.out.println(Integer.MIN_VALUE);
System.out.println(Integer.MAX_VALUE);
```

### Double class

```java
//Constructs a Double object from a double. (Boxing.)
Double(double value)

//Returns the value of this Double as a double. (Unboxing.)
double doubleValue()

```

**Note**

1. The compareTo and equals methods for the Integer and Double classes are no longer part of the AP Java subset. This is probably because the later versions of Java make extensive use of autoboxing and auto-unboxing.
2. Integer and Double objects are immutable. This means there are no mutator methods in the classes.

### Autoboxing and Unboxing

Autoboxing is the automatic conversion that the Java compiler makes between primitive types and their corresponding wrapper classes. This includes converting an int to an Integer and a double to a Double.

```java
Integer intOb = 3; //3 is boxed

ArrayList<Integer> list = new ArrayList<Integer>();
list.add(4); //4 is boxed
```

Unboxing is the automatic conversion that the Java compiler makes from the wrapper class to the primitive type. This includes converting an Integer to an int and a Double to a double.

```java
Integer intOb1 = 9; 
Integer intOb2 = 8;

public static int sum (int num1, int num2) { 
    return num1 + num2; 
}

System.out.println(sum(intOb1, intOb2)); //intOb1 and intOb2 are unboxed
```

### comparison of wrapper class objects

Unboxing is often used in the comparison of wrapper objects of the same type. But it’s trickier than it sounds. Don’t use == to test Integer objects! You may get surprising results.

```java
Integer intOb1 = 4; //boxing
Integer intOb2 = 4; //boxing
System.out.println(intOb1 == intOb2);   //true

Integer intOb3 = 4; //boxing
Integer intOb4 = new Integer(4);
System.out.println(intOb3 == intOb4); // false

Integer intOb5 = 4;
int intOb6 = 4;
System.out.println(intOb5 == intOb6);  //true

Integer intOb7 = 4; //boxing
Integer intOb8 = new Integer(4); //boxing
System.out.println(intOb7.intValue() == intOb8.intValue()); // true

Integer intOb9 = 4;
Integer intOb10 = 8;
System.out.println(intOb9 < intOb10); // true

Integer intOb11 = 4;
int n = 8;
System.out.println(intOb11 < n);  // true

```
