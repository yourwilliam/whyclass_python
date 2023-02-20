# \[course07] 01 Object class

## \[course07] 01 Object class

### The universal superclass

Object is a direct or indirect superclass of every other class.

![](http://ossp.pengjunjie.com/mweb/16766935617626.jpg)

#### toString() method

```java

SavingsAccount s = new SavingsAccount(500); System.out.println(s);

```

examples:

```java
public class OrderedPair {
    private double x; 
    private double y;
    

    //constructors and other methods ...

    /** Returns this OrderedPair in String form. */ 
    public String toString() { 
        return "(" + x + "," + y + ")"; 
    }
}
```

**Note**

1. The + sign is a concatenation operator for strings
2. Array objects are unusual in that they do not have a toString method. To print the elements of an array, the array must be traversed and each element must explicitly be printed.

#### equal() method

```java

public boolean equals(Object other)
```

```java

Date d1 = new Date(2021, Calendar.JANUARY, 14);
Date d2 = d1;
Date d3 = new Date(2021, Calendar.JANUARY, 14);

System.out.println(d1 == d2);
System.out.println(d1 == d3);

System.out.println(d1.equals(d2));
System.out.println(d1.equals(d3));
```

Do not use == to test objects for equality. Use the equals method.

**Note**

1. The default implementation of equals is equivalent to the == relation for objects: In the Date example above, the test if (d1 == d2) returns trXe; the test if (d1 == d3) returns false.
2. The operators <, >, and so on are not used for objects (reference types) in Java. To compare objects, you must use either the equals method or define a compareTo method for the class.
