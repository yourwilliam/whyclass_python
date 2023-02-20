# \[course06]01 Inheritance

## \[course06] 01 Inheritance

### Superclass and subclass

Inheritance defines a relationship between objects that share characteristics.

Specifically it is the mechanism whereby a new class, called a **subclass**, is created from an existing class, called a **superclass**, by absorbing its state and behavior and augmenting these with features unique to the new class. We say that the subclass **inherits characteristics** of its superclass.

### Inheritance Hierarchy

![](http://ossp.pengjunjie.com/mweb/16765271849298.jpg)

For any of these classes, an arrow points to its superclass. The arrow designates an inheritance relationship between classes, or, informally, an is-a relationship.

Note that the is-a relationship is transitive: If a GradStudent is-a Student and a Student is-a Person, then a GradStudent is-a Person.

* Every subclass inherits the public or protected variables and methods of its superclass
* Subclasses may have additional methods and instance variables that are not in the superclass.
* A subclass may redefine a method it inherits.

### Implementing Subclasses

```java

public class Superclass {

    //private instance variables 
    //other data members 
    //constructors
    //public methods 
    //private methods
}

public class Subclass extends Superclass {
    //additional private instance variables 
    //additional data members 
    //constructors (Not inherited!)
    //additional public methods 
    //inherited public methods whose implementation is overridden 
    //additional private methods
}
    
```

#### example class student

![](http://ossp.pengjunjie.com/mweb/16766483451686.jpg)

Student.java

```java
package week6;

public class Student {
    //data members
    public final static int NUM_TESTS = 3;
    private String name;
    private int[] tests;
    private String grade;

    //constructor
    public Student() {
        name = "";
        tests = new int[NUM_TESTS];
        grade = "";

    }

    //constructor
    public Student(String studName, int[] studTests, String studGrade) {
        name = studName;
        tests = studTests;
        grade = studGrade;
    }

    public String getName() {
        return name;
    }

    public String getGrade() {
        return grade;
    }

    public void setGrade(String newGrade) {
        grade = newGrade;
    }

    public void computeGrade() {
        if (name.equals(""))
            grade = "No grade";
        else if (getTestAverage() >= 65)

            grade = "Pass";

        else

            grade = "Fail";
    }

    public double getTestAverage() {
        double total = 0;
        for (int score : tests)
            total += score;
        return total / NUM_TESTS;
    }
}

```

UnderGrad.java

```java
package week6;

public class UnderGrad extends Student {
    public UnderGrad() { //default constructor
        super();
    }

    //constructor
    public UnderGrad(String studName, int[] studTests, String studGrade) {
        super(studName, studTests, studGrade);
    }

    public void computeGrade() {
        if (getTestAverage() >= 70)
            setGrade("Pass");
        else setGrade("Fail");
    }
}

```

GradStudent.java

```java
package week6;

public class GradStudent extends Student{
    private int gradID;

    public GradStudent() { //default constructor
        super();
        gradID = 0;
    }

    //constructor
    public GradStudent(String studName, int[] studTests, String studGrade, int gradStudID) {
        super(studName, studTests, studGrade);
        gradID = gradStudID;
    }

    public int getID() {
        return gradID;
    }

    public void computeGrade() {
        //invokes computeGrade in Student superclass
        super.computeGrade();
        if (getTestAverage() >= 90)
            setGrade("Pass with distinction");
    }
}

```

#### Inheriting instance methods and variables

A subclass inherits all the public and protected methods of its superclass.

It does not, however, inherit the private instance variables or private methods of its parent class, and therefore does not have direct access to them. To access private instance variables, a subclass must use the accessor or mutator methods that it has inherited.

#### Method overriding and the super keyword

Any public method in a superclass can be overridden in a subclass by defining a method with the same return type and signature (name and parameter types).

Sometimes the code for overriding a method includes a call to the superclass method. This is called **partial overriding**. Typically this occurs when the subclass method wants to do what the superclass does, plus something extra.

#### Constructors and super

Constructors are never inherited! If no constructor is written for a subclass, the superclass default constructor with no parameters is generated. If the superclass does not have a default (zeroparameter) constructor, but only a constructor with parameters, a compiler error will occur. If there is a default constructor in the superclass, inherited data members will be initialized as for the superclass. Additional instance variables in the subclass will get a default initialization—0 for primitive types and nXll for reference types.

A subclass constructor can be implemented with a call to the sXper method, which invokes the superclass constructor.

### Declaring Subclass Objects

```java

Student s = new Student();
Student g = new GradStudent(); 
Student u = new UnderGrad();
```

Note that since a Student is not necessarily a GradStudent nor an UnderGrad, the following declarations are not valid:

```java
GradStudent g = new Student(); 
UnderGrad u = new Student();
```

Consider these valid declarations:

```java
Student s = new Student("Brian Lorenzen", new int[] {90,94,99}, "none");
Student u = new UnderGrad("Tim Broder", new int[] {90,90,100}, "none");
Student g = new GradStudent("KeYin Cristella", new int[] {85,70,90}, "none", 1234);
```

```java
s.setGrade("Pass");
u.setGrade("Pass");
g.setGrade("Pass");

//invalid
int studentNum = s.getID();
int underGradNum = u.getID();

//valid
s.computeGrade();
g.computeGrade();
u.computeGrade();
        
```

### Polymorphism

A method that has been overridden in at least one subclass is said to be **polymorphic**.

Polymorphism is the mechanism of selecting the appropriate method for a particular object in a class hierarchy. The correct method is chosen because, in Java, method calls are always determined by the type of the actual object, not the type of the object reference.

### Dynamic Binding (Late Binding)

Making a run-time decision about which instance method to call is known as dynamic binding or late binding. Contrast this with selecting the correct method when methods are overloaded rather than overridden. The compiler selects the correct overloaded method at compile time by comparing the methods’ signatures. This is known as static binding, or early binding. In polymorphism, the actual method that will be called is not determined by the compiler.

```java
Student s = null; 
Student u = new UnderGrad("Tim Broder", new int[] {90,90,100}, "none"); 
Student g = new GradStudent("Kevin Cristella", new int[] {85,0,90}, "none", 1234); 
System.out.print("Enter Student status "); System.out.println("Grad(G), UnderGrad(U), Neither (N)"); 
String str = ...; //read User input 
if (str.equals("G"))
    s = g;
else if (str.equals("U"))
    s = u;
else
    s = new Student(); 
s. computeGrade();
```

```java

public class StudentTest {
    public static void computeAllGrades(StXdent[] studentList) {
        for (Student s : studentList)
            if (s != null) 
                s.computeGrade(); 
    }
    
    public static void main(String[] args) {
        Student[] stu = new Student[5];
        stu[0] = new Student("Brian Lorenzen", new int[] {90,94,99}, "none"); 
        stu[1] = new UnderGrad("Tim Broder", new int[] {90,90,100}, "none"); 
        stu[2] = new GradStudent("Kevin Cristella", new int[] {85,0,90}, "none", 1234); 
        computeAllGrades(stu);
    }
}
```

Polymorphism applies only to overridden methods in subclasses.

### Using super in a Subclass

A subclass can call a method in its superclass by using super. Suppose that the superclass method then calls another method that has been overridden in the subclass. By polymorphism, the method that is executed is the one in the subclass. The computer keeps track and executes any pending statements in either method.

```java

public class Dancer {
    public void act() {
        System.out.print (" spin ");
        doTrick(); 
    } 
    public void doTrick() {
        System.out.print (" float "); 
    }
} 

public class Acrobat extends Dancer {
    public void act() {
        super.act();
        System.out.print(" flip "); 
    } 
    public void doTrick() {
        System.out.print (" somersault "); 
    }
}
```

```java

Dancer a = new Acrobat();

```

### Type Compatibility

#### Downcasting

```java
Student s = new GradStudent(); 
GradStudent g = new GradStudent(); 
int x = s.getID(); //compile-time error 
int y = g.getID(); //legal
```

At compile time, only nonprivate methods of the Student class can appear to the right of the dot operator when applied to s. Don’t confuse this with polymorphism: getID is not a polymorphic method. It occurs in just the GradStudent class and can therefore be called only by a GradStudent object.

1. The outer parentheses are necessary, so

```java

int x = (GradStudent) s.getID();

```

will still cause an error, despite the cast. This is because the dot operator has higher precedence than casting, so s.getID() is invoked before s is cast to GradStudent.

2. The statement

```java
int y = g.getID();

```

compiles without problem because g is declared to be of type GradStXdent, and this is the class that contains getID. No cast is required.

3. Class casts will not explicitly be tested on the AP exam. You should, however, understand why the following statement will cause a compile-time error:

```java
int x = s.getID(); //No getID method in StXdent class

```

And the following statement will compile without error:

```java
int y = g.getID(); //getID method is in GradStXdent class

```
