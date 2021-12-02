# \[sourse05] 04 Searching and Sorting

### Searching

```java
/**
 * Searches the array A for the integer N.  If N is not in the array,
 * then -1 is returned.  If N is in the array, then the return value is
 * the first integer i that satisfies A[i] == N.
 */
static int find(int[] A, int N) {
      
   for (int index = 0; index < A.length; index++) {
      if ( A[index] == N ) 
         return index;  // N has been found at this index!
   }
   
   // If we get this far, then N has not been found
   // anywhere in the array.  Return a value of -1.
   
   return -1;
   
}
```

### Binary Search

```java
/**
 * Searches the array A for the integer N.
 * Precondition:  A must be sorted into increasing order.
 * Postcondition: If N is in the array, then the return value, i,
 *    satisfies A[i] == N.  If N is not in the array, then the
 *    return value is -1.
 */
static int binarySearch(int[] A, int N) {
      
    int lowestPossibleLoc = 0;
    int highestPossibleLoc = A.length - 1;
    
    while (highestPossibleLoc >= lowestPossibleLoc) {
       int middle = (lowestPossibleLoc + highestPossibleLoc) / 2;
       if (A[middle] == N) {
                 // N has been found at this index!
          return middle;
       }
       else if (A[middle] > N) {
                 // eliminate locations >= middle
          highestPossibleLoc = middle - 1;
       }
       else {
                 // eliminate locations <= middle
          lowestPossibleLoc = middle + 1;   
       }
    }
    
    // At this point, highestPossibleLoc < LowestPossibleLoc,
    // which means that N is known to be not in the array.  Return
    // a -1 to indicate that N could not be found in the array.
 
    return -1;
  
}
```

### Insertion Sort

![](https://ossp.pengjunjie.com/mweb/16383966184392.jpg)

```java
static void insertionSort(int[] A) {
      // Sort the array A into increasing order.
      
   int itemsSorted; // Number of items that have been sorted so far.

   for (itemsSorted = 1; itemsSorted < A.length; itemsSorted++) {
         // Assume that items A[0], A[1], ... A[itemsSorted-1] 
         // have already been sorted.  Insert A[itemsSorted]
         // into the sorted part of the list.
         
      int temp = A[itemsSorted];  // The item to be inserted.
      int loc = itemsSorted - 1;  // Start at end of list.
      
      while (loc >= 0 && A[loc] > temp) {
         A[loc + 1] = A[loc]; // Bump item from A[loc] up to loc+1.
         loc = loc - 1;       // Go on to next location.
      }
      
      A[loc + 1] = temp; // Put temp in last vacated space.
   }
}
```

### Selection Sort

```java
static void selectionSort(int[] A) {
      // Sort A into increasing order, using selection sort
      
   for (int lastPlace = A.length-1; lastPlace > 0; lastPlace--) {
         // Find the largest item among A[0], A[1], ...,
         // A[lastPlace], and move it into position lastPlace 
         // by swapping it with the number that is currently 
         // in position lastPlace.
         
      int maxLoc = 0;  // Location of largest item seen so far.
      
      for (int j = 1; j <= lastPlace; j++) {
         if (A[j] > A[maxLoc]) {
               // Since A[j] is bigger than the maximum we've seen
               // so far, j is the new location of the maximum value
               // we've seen so far.
            maxLoc = j;  
         }
      }
      
      int temp = A[maxLoc];  // Swap largest item with A[lastPlace].
      A[maxLoc] = A[lastPlace];
      A[lastPlace] = temp;
      
   }  // end of for loop
   
}
```
