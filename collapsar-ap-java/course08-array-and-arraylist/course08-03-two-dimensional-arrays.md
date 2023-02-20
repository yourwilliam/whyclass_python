# \[course08] 03 Two dimensional arrays

## \[course08] 03 Two dimensional arrays

A matrix is implemented as an array of rows, where each row is a one-dimensional array of elements.

```
2 6 8 7 
1 5 4 0
9 3 2 8

mat[0] contains {2, 6, 8, 7}

mat[1] contains {1, 5, 4, 0}

mat[2] contains {9, 3, 2, 8}

```

### Declarations

```java
int[][] table;
double[][] matrix = new double[3][4];
String[][] strs = new String[2][5];


// initializer

int[][] mat = { {3, 4, 5},      //row 0
                {6, 7, 8}};     //row 1

```

### Processing a Two-Dimensional Array

```java
for (row = 0; row < mat.length; row++)
    for (col = 0; col < mat[0].length; col++)
        processElements();
        
        
for (col = 0; col < mat[0].length; col++)
    for (row = 0; row < mat.length; row++)
        processElements();
        
        
/** Precondition: mat is initialized with integer values. */
int sum = 0;
for (int r = 0; r < mat.length; r++)
    for (int c = 0; c < mat[r].length; c++)
        sum += mat[r][c];
        
for (int[] row : mat) //for each row array in mat
    for (int element : row) //for each element in this row 
        swm += element;
```

### Two-Dimensional Array as Parameter

```java
/** Returns count of negative values in mat.
 * Precondition: mat is initialized with integers. 
 */
public static int countNegs (int[][] mat) {
    int count = 0;
    for (int[] row : mat)
        for (int num : row) if (num < 0)
            count++;
    return count;
}

/** Returns matrix containing rows
 * cols integers
 * read from the keyboard.
 * Precondition: Number of rows and columns known. */
public static int[][] getMatrix(int rows, int cols) {
    int[][] mat = new int[rows][cols]; //initialize slots
    System.out.println("Enter matrix, one row per line");
    System.out.println();
    //read user input and fill slots
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++)
            mat[r][c] = 5; //read user input
    return mat;
}
```
