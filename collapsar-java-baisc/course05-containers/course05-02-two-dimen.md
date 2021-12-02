# \[course05] 02 Two-dimen

### Declare and initialize

```java
int[][] A;
A = new int[3][4];

int[][]  A  =  {  {  1,  0, 12, -1 },
                  {  7, -3,  2,  5 },
                  { -5, -2,  2, -9 }
               };

A  =  new int[][] {  {  1,  0, 12, -1 },
                     {  7, -3,  2,  5 },
                     { -5, -2,  2, -9 }
                  };
```

### The truth about 2D arrays

Java does not actually have two-dimensional arrays. In a true 2D array, all the elements of the array occupy a continuous block of memory, but that's not true in Java.

a 2D array is really an array of pointers, where each pointer can refer to a one-dimensional array.

![](https://ossp.pengjunjie.com/mweb/16383919545390.jpg)

![](https://ossp.pengjunjie.com/mweb/16383919286018.jpg)

```java
/**
 * Represents symmetric n-by-n matrices of real numbers.
 */
public class SymmetricMatrix {
    
    private double[][] matrix;  // A triangular matrix to hold the data.
    
    /**
     * Creates an n-by-n symmetric matrix in which all entries are 0.
     */
    public SymmetricMatrix(int n) {
        matrix = new double[n][];
        for (int i = 0; i < n; i++)
            matrix[i] = new double[i+1];
    }
    
    /**
     * Returns the matrix entry at position (row,col).  (If row < col,
     * the value is actually stored at position (col,row).)
     */
    public double get( int row, int col ) {
        if (row >= col)
            return matrix[row][col];
        else
            return matrix[col][row];
    }
    
    /**
     * Sets the value of the matrix entry at (row,col).  (If row < col,
     * the value is actually stored at position (col,row).)
     */
    public void set( int row, int col, double value ) {
        if (row >= col)
            matrix[row][col] = value;
        else
            matrix[col][row] = value;
    }
    
    /**
     * Returns the number of rows and columns in the matrix.
     */
    public int size() {
        return matrix.length;  // The size is the number of rows.
    }

} // end class SymmetricMatrix
```
