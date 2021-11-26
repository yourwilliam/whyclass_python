# \[course03] 04 switch case

### Base switch case

A switch statement allows you to test the value of an expression and, depending on that value, to jump directly to some location within the switch statement. Only expressions of certain types can be used. The value of the expression can be one of the primitive integer types **int**, **short**, or **byte**. It can be the primitive **char** type. It can be **String**. Or it can be an **enum** type. In particular, note that the expression **cannot be a double or float value**.

```java
switch (expression) {
   case constant-1:
      statements-1
      break;
   case constant-2:
      statements-2
      break;
      .
      .   // (more cases)
      .
   case constant-N:
      statements-N
      break;
   default:  // optional default case
      statements-(N+1)
} // end of switch statement

//same as 

if (expression == constant-1) { // but use .equals for String!!
    statements-1
} 
else if (expression == constant-2) { 
    statements-2
} 
    .
    .
    .
else if (expression == constant-N) { 
    statements-N
} 
else {
    statements-(N+1)
}
```

### example : menus

```java
String units;       // Unit of measurement, entered by user.
double measurement; // A numerical measurement, input by the user.
double inches;      // The same measurement, converted into inches.

/* Read the user's unit of measurement. */

System.out.println("What unit of measurement does your input use?");
System.out.print("Legal responses: inches, feet, yards, or miles : ");
units = TextIO.getln().toLowerCase();

/* Read user's measurement and convert to inches. */

System.out.print("Enter the number of " + units + ":  ");
measurement = TextIO.getlnDouble();

switch ( units ) {
   case "inches":
       inches = measurement;
       break;          
   case "feet":
       inches = measurement * 12;
       break;          
   case "yards":
       inches = measurement * 36;
       break;          
   case "miles":
       inches = measurement * 12 * 5280;
       break;
   default:
       System.out.println("Wait a minute!  Illegal unit of measure!  I quit!");
       System.exit(1);          
} // end switch
```

### Enum in switch statements

```java
enum Season { SPRING, SUMMER, FALL, WINTER }

switch ( currentSeason ) {
   case WINTER:    // ( NOT Season.WINTER ! )
      System.out.println("December, January, February");
      break;
   case SPRING:
      System.out.println("March, April, May");
      break;
   case SUMMER:
      System.out.println("June, July, August");
      break;
   case FALL:
      System.out.println("September, October, November");
      break;
}
```
