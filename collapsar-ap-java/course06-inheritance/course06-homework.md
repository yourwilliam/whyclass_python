# \[course06] homework

## \[course06] homework

### Q1 Make a class

The Book class is used to store information about a book. A partial Book class definition is shown.

```java
public class Book {

/** The title of the book */ 
private String title;

/** The price of the book */ 
private double price;

/** Creates a new Book with given title and price */ public Book(String bookTitle, double bookPrice) { 
    /* implementation not shown */ 
}

/** Returns the title of the book */ 
public String getTitle() { 
    return title; 
}

/** Returns a string containing the title and price of the Book */ 
public String getBookInfo() { 
    return title + " - " + price; 
}

// There may be instance variables, constructors, and methods that are not shown.

}
```

You will write a class `Textbook`, which is a subclass of `Book`.

A `Textbook` has an edition number, which is a positive integer used to identify different versions of the book. The `getBookInfo` method, when called on a `Textbook`, returns a string that also includes the edition information, as shown in the example.

Information about the book title and price must be maintained in the `Book` class. Information about the edition must be maintained in the `Textbook` class.

The `Textbook` class contains an additional method, `canSubstituteFor`, which returns true if a `Textbook` is a valid substitute for another `Textbook` and returns `false` otherwise. The current `Textbook` is a valid substitute for the `Textbook` referenced by the parameter of the `canSubstituteFor` method if the two `Textbook` objects have the same title and if the edition of the current `Textbook` is greater than or equal to the edition of the parameter.

The following table contains a sample code execution sequence and the corresponding results. The code execution sequence appears in a class other than Book or Textbook.

![](http://ossp.pengjunjie.com/mweb/16771335462124.jpg)

Write the complete Textbook class. Your implementation must meet all specifications and conform to the examples shown in the preceding table.

### Q2 restaurant table

The class SingleTable represents a table at a restaurant.

```java
public class SingleTable {

/** Returns the number of seats at this table. The value is always greater than or equal to 4. */ 
public int getNumSeats() { 
    /* implementation not shown */ 
}

/** Returns the height of this table in centimeters. */ 
public int getHeight() { 
    /* implementation not shown */ 
}

/** Returns the quality of the view from this table. */ 
public double getViewQuality() { 
    /* implementation not shown */
}

/** Sets the quality of the view from this table to value . */ 
public void setViewQuality(double value) { 
    /* implementation not shown */ }

// There may be instance variables, constructors, and methods that are not shown.

}
```

At the restaurant, customers can sit at tables that are composed of two single tables pushed together. You will write a class CombinedTable to represent the result of combining two `SingleTable` objects, based on the following rules and the examples in the chart that follows.

* A `CombinedTable` can seat a number of customers that is two fewer than the total number of seats in its two `SingleTable` objects (to account for seats lost when the tables are pushed together).
* A `CombinedTable` has a desirability that depends on the views and heights of the two single tables. If the two single tables of a `CombinedTable` object are the same height, the desirability of the `CombinedTable` object is the average of the view qualities of the two single tables.
* If the two single tables of a `CombinedTable` object are not the same height, the desirability of the `CombinedTable` object is 10 units less than the average of the view qualities of the two single tables.

Assume SingleTable objects t1, t2, and t3 have been created as follows.

* `SingleTable` t1 has 4 seats, a view quality of 60.0, and a height of 74 centimeters.
* `SingleTable` t2 has 8 seats, a view quality of 70.0, and a height of 74 centimeters.
* `SingleTable` t3 has 12 seats, a view quality of 75.0, and a height of 76 centimeters.

The chart contains a sample code execution sequence and the corresponding results.

![](http://ossp.pengjunjie.com/mweb/16771342948525.jpg)

The last line of the chart illustrates that when the characteristics of a `SingleTable` change, so do those of the `CombinedTable` that contains it.

Write the complete `CombinedTable` class. Your implementation must meet all specifications and conform to the examples shown in the preceding chart.
