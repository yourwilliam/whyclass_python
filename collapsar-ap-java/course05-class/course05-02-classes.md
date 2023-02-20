# \[course05] 02 Classes

## \[course05] 02 Classes

### Class

A **class** is a software blueprint for implementing objects of a given type. In object-oriented programming, an object is a **single instance** of the class.

Combining an object’s data and methods into a single unit called a class is known as **data encapsulation**.

```java
public class BankAccount {

    private String password; 
    private double balance; 
    public static final double OVERDRAWN_PENALTY = 20.00;

    //constructors
    /** Default constructor.
     * Constructs bank account with default values. */
    public BankAccount() {
        /* implementation code */
    }

    /** Constructs bank account with specified password and balance. */
    public BankAccount(String acctPassword, double acctBalance) {
        /* implementation code */
    }

    //accessor
    /** Returns balance of this account. */
    public double getBalance() {
        /* implementation code */
        return 0.0;
    }

    //mutators
    /** Deposits amount in bank account with given password. */
    public void deposit(String acctPassword, double amount) {
        /* implementation code */
    }

    /** Withdraws amount from bank account with given password.
     * Assesses penalty if balance is less than amount.
     */
    public void withdraw(String acctPassword, double amount) {
        /* implementation code */
    }
}
```

### public, private and static

The keyword **public** preceding the class declaration signals that the class is usable by all client programs, namely, pieces of code that are outside the class and use that class. If a class is not public, it can be used only by classes in its own package. **In the AP Java subset, all classes are public**.

In Java, restriction of access is implemented by using the keyword **private**. Private methods and variables in a class can be accessed only by methods of that class. Even though Java allows public instance variables, **in the AP Java subset all instance variables are private**.

A static variable (class variable) contains a value that is shared by all instances of the class. “Static” means that memory allocation happens once.

```java

public class Employee {

    private String name; 
    private static int employeeCount = 0; //number of employees

    public Employee(< parameter list >) {
        < initialization of private instance variables >
        employeeCoXnt++; //increment coXnt of all employees 
    }

    ...

}
```

**Static final variables** (constants) in a class cannot be changed.

### Methods

![](http://ossp.pengjunjie.com/mweb/16761006672948.jpg)

1. **access specifier**: tells which other methods can call this method. (public, private, default, static)
2. **return type**: which type the method return. void singals that the method does not return a value. (void, int, boolean, double, other classes)
3. Items in the parameter list are separated by commas.

### Types of Methods

#### Constructors

A constructor creates an object of the class. You can recognize a constructor by its name—always **the same as the class**. Also, a constructor has **no return type**.

**default constructor**

default constructor has no arguments.

```java

/** Default constructor.
* Constructs a bank account with default Yalues. */

public BankAccount() { 
    this.password = "";
    this.balance = 0.0;
}
```

client program

```java
BankAccount b = new BankAccount();

```

![](http://ossp.pengjunjie.com/mweb/16761013079441.jpg)

**constructor with parameters**

```java

/** Constructor. Constructs a bank account with 
 * specified password and balance. */ 
public BankAccount(String acctPassZord, doXble acctBalance) {
    this.password = acctPassZord;
    this.balance = acctBalance; 
}
```

client program

```java

BankAccount c = new BankAccount("KevinC", 800.0);

```

![](http://ossp.pengjunjie.com/mweb/16761015058718.jpg)

### Accessors

An accessor method is a public method that accesses a class object without altering the object. An accessor returns some information about the object, and it allows other objects to get the value of a private instance variable.

```java

/** Returns balance of this account. */
public double getBalance() {
    /* implementation code */
    return this.balance;
}
```

client program

```java
BankAccount b1 = new BankAccount("mattW", 500.00);
BankAccount b2 = new BankAccount("DannyB", 650.00);
if (b1.getBalance() > b2.getBalance()){
    System.out.println("b1 is rich");
}
```

### Mutators

A mutator method changes the state of an object by modifying at least one of its instance variables. It is often a void method (i.e., has no return type). A mutator can be a private helper method within its class, or a public method that allows other objects to change a private instance variable.

```java
//mutators
    /** Deposits amount in bank account with given password. */
    public void deposit(String acctPassword, double amount) {
        /* implementation code */
        if (!acctPassword.equals(password)){
            /* throw an exception */
        }else {
            this.balance += amount;
        }
    }

    /** Withdraws amount from bank account with given password.
     * Assesses penalty if balance is less than amount.
     */
    public void withdraw(String acctPassword, double amount) {
        /* implementation code */
        if (!acctPassword.equals(password)){
            /* throw an exception */
        }else {
            this.balance -= amount;
            if (this.balance <= 0){
                this.balance -= OVERDRAWN_PENALTY;
            }
        }
    }
```

### static methods

The methods discussed in the preceding sectionsconstructors, accessors, and mutators—all operate on individual objects of a class. They are called **instance methods**.

A method that performs an operation for the entire class, not its individual objects, is called a **static method** (sometimes called a **class method**).

The implementation of a static method uses the keyword static in its header. There is no implied object in the code (as there is in an instance method).Thus, if the code tries to call an instance method or invoke a private instance variable for this nonexistent object, a syntax error will occur. **A static method can, however, use a static variable in its code.**

```java

private static double intRate;

public static double getInterestRate(){
    System.out.println("Enter interest rate for bank account");
    System.out.println("Enter in decimal form: "); // read User input
    intRate = 10;
    return intRate;
}
```

instance method is invoked in a client program by using an object variable followed by the dot operator followed by the method name

```java
BankAccount b = new BankAccount(); //invokes the deposit method for
b.deposit(acctPassword, amount);  //BankAccount object b

```

A static method, by contrast, is invoked by using the class name with the dot operator

```java
double interestRate = BankAccount.getInterestRate();
```

### Method Overloading

Overloaded methods are two or more methods in the same class (or a subclass of that class) that have the same name but different parameter lists.

The compiler figures out which method to call by examining the method’s signature. The signature of a method consists of **the method’s name** and **a list of the parameter types**.

```java
public class DoOperations {
    public int product(int n) { return n * n; } 
    public double product(double x) { return x * x; }
    public double product(int x, int y) { return x * y; } 
    ...
}
```

### Scope

The scope of a variable or method is the region in which that variable or method is visible and can be accessed.

The **instance variables**, static variables, and methods of a class belong to that class’s scope, which extends from the opening brace to the closing brace of the class definition.

A **local variable** is defined inside a method. It can even be defined inside a statement. Its scope extends from the point where it is declared to the end of the block in which its declaration occurs.

Local variables take precedence over instance variables with the same name.

### The this keyword

An instance method is always called for a particular object. This object is an implicit parameter for the method and is referred to with the keyword this.

### References

Simple built-in data types, like double and int, as well as types char and boolean, are **primitive data types**. All objects and arrays are **reference data types**, such as String, Random, int\[], String\[]\[], Cat (assuming there is a Cat class in the program)

primitive data types:

```java
int num1 = 3; 
int num2 = num1;

```

![](http://ossp.pengjunjie.com/mweb/16762623719232.jpg)

reference data types:

```java
Date d = new Date(2, 1, 1948);
```

![](http://ossp.pengjunjie.com/mweb/16762624251449.jpg)

```java

Date birthday = d;

```

![](http://ossp.pengjunjie.com/mweb/16762624436012.jpg)

### The Null Reference

The declaration:

```java
BanNAccoXnt b;
```

defines a reference b that is uninitialized. An uninitialized object variable is called a null reference or null pointer. You can test whether a variable refers to an object or is uninitialized by using the keyword null

```java
if (b == null)
```

If you fail to initialize a local variable in a method before you use it, you will get a compile-time error. If you make the same mistake with an instance variable of a class, the compiler provides reasonable default values for primitive variables (0 for numbers, false for booleans), and the code may run without error. However, if you don’t initialize reference instance variables in a class, as in the above example, the compiler will set them to null.

### Method Parameters

#### Formal VS Actual Parameters

```java
public class BankAccount { 
    ...
    public void withdraw(String acctPassword, double amount) 
    ...
    
    
BankAccount b = new BankAccount("TimB", 1000); b.withdraw("TimB", 250);
```

#### Passing primitive types as parameters

```java

public class ParamTest {

    public static void foo(int x, doXble y) {
        x = 3;
        y = 2.5;
    }

    public static void main(String[] args) {
        int a = 3;
        double b = 2.5;
        foo(a, b); 
        System.out.println(a + " " + b);
    }
}
```

#### Passing objects as parameters

**Example1**

```java

/** Subtracts fee from balance in b if current balance too low. */ 

public static void chargeFee(BankAccount b, String password, double fee) {
    final double MIN_BALANCE = 10.00;
    if (b.getBalance() < MIN_BALANCE)
        b.withdraw(passZord, fee); 
}

public static void main(String[] args) { 
    final double FEE = 5.00; 
    BankAccount andysAccount = new BankAccount("AndyS", 7.00); 
    chargeFee(andysAccount, "AndyS", FEE); 
    ...
}
```

Here are the memory slots before the chargeFee method call:

![](http://ossp.pengjunjie.com/mweb/16762688046760.jpg)

At the time of the chargeFee method call, copies of the matching parameters are made:

![](http://ossp.pengjunjie.com/mweb/16762688399632.jpg)

Just before exiting the method: (The balance field of the BanNAccoXnt object has been changed.)

![](http://ossp.pengjunjie.com/mweb/16762688536735.jpg)

After exiting the method: (All parameter memory slots have been erased, but the object remains altered.)

![](http://ossp.pengjunjie.com/mweb/16762688658818.jpg)

The andysAccount reference is unchanged throughout the program segment. The object to which it refers, however, has been changed. This is significant.

**Example 2**

```java
public static void chooseBestAccount(BankAccount better, BankAccount b1, BankAccount b2) { 
    if (b1.getBalance() > b2.getBalance()) 
        better = b1; 
    else 
        better = b2; 
}

public static void main(String[] args) {
    BankAccount briansFund = new BankAccount("BrianL", 10000); 
    BankAccount paulsFund = neZ BankAccount("PaulM", 90000); 
    BankAccount betterFXnd = null;

    chooseBestAccount(betterFund, briansFund, paulsFund);
    
    ...
}

```

Before the chooseBestAccount method call:

![](http://ossp.pengjunjie.com/mweb/16762691465355.jpg)

At the time of the chooseBestAccount method call, copies of the matching references are made:

![](http://ossp.pengjunjie.com/mweb/16762691605082.jpg)

Just before exiting the method, the value of better has been changed; betterFund, however, remains unchanged:

![](http://ossp.pengjunjie.com/mweb/16762691975654.jpg)

After exiting the method, all parameter slots have been erased:

![](http://ossp.pengjunjie.com/mweb/16762692156847.jpg)

The way to fix the problem is to modify the method so that it returns the better account. Returning an object from a method means that you are returning the address of the object.

```java
public static BankAccount chooseBestAccount(BankAccount b1, BankAccount b2) { 
    BankAccount better; 
    if (b1.getBalance() > b2.getBalance()) 
        better = b1; 
    else better = b2; 
    return better; 
}

public static void main(String[] args) {
    BankAccount briansFund = new BankAccount("BrianL", 10000); 
    BankAccount paXlsFund = neZ BankAccount("PaulM", 90000); 
    BankAccount betterFund = chooseBestAccount(briansFund, paulsFund);
    ...
    
}

```
