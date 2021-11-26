# \[course02] 02 functions

### Subroutine Definitions

```java
modifiers  return-type  subroutine-name  ( parameter-list ) {
    statements
}
```

The **statements** between the braces, { and }, in a subroutine definition make up the body of the subroutine.

The **modifiers** that can occur at the beginning of a subroutine definition are words that set certain characteristics of the subroutine, such as whether it is static or not. The modifiers that you've seen so far are "static" and "public". There are only about a half-dozen possible modifiers altogether.

If the subroutine is a **function**, whose job is to compute some value, then the **return-type** is used to specify the type of value that is returned by the function. It can be a type name such as String or int or even an array type such as double\[]. If the subroutine is not a function, then the return-type is replaced by the special value void, which indicates that no value is returned. The term **"void"** is meant to indicate that the return value is empty or non-existent.

**parameter-list**. Parameters are part of the interface of a subroutine. They represent information that is passed into the subroutine from outside, to be used by the subroutine's internal computations.

```java
public static void playGame() {
    // "public" and "static" are modifiers; "void" is the 
    // return-type; "playGame" is the subroutine-name; 
    // the parameter-list is empty.
    . . .  // Statements that define what playGame does go here.
}

int getNextN(int N) {
    // There are no modifiers; "int" is the return-type;
    // "getNextN" is the subroutine-name; the parameter-list 
    // includes one parameter whose name is "N" and whose 
    // type is "int".
    . . .  // Statements that define what getNextN does go here.
}

static boolean lessThan(double x, double y) {
    // "static" is a modifier; "boolean" is the
    // return-type; "lessThan" is the subroutine-name; 
    // the parameter-list includes two parameters whose names are 
    // "x" and "y", and the type of each of these parameters 
    // is "double".
    . . .  // Statements that define what lessThan does go here.
}
```

### Calling Subroutines

When you define a subroutine, all you are doing is telling the computer that the subroutine exists and what it does. The subroutine doesn't actually get executed until it is called.

```java
playGame();
```

Since playGame() is a public method, it can also be called from other classes, but in that case, you have to tell the computer which class it comes from. Since playGame() is a static method, its full name includes the name of the class in which it is defined.

```java
Poker.playGame();
```

### Subroutines in Programs

```java
import textio.TextIO;

public class GuessingGame {

   public static void main(String[] args) {
      System.out.println("Let's play a game.  I'll pick a number between");
      System.out.println("1 and 100, and you try to guess it.");
      boolean playAgain;
      do {
         playGame();  // call subroutine to play one game
         System.out.print("Would you like to play again? ");
         playAgain = TextIO.getlnBoolean();
      } while (playAgain);
      System.out.println("Thanks for playing.  Goodbye.");
   } // end of main()            
   
   static void playGame() {
       int computersNumber; // A random number picked by the computer.
       int usersGuess;      // A number entered by user as a guess.
       int guessCount;      // Number of guesses the user has made.
       computersNumber = (int)(100 * Math.random()) + 1;
                // The value assigned to computersNumber is a randomly
                //    chosen integer between 1 and 100, inclusive.
       guessCount = 0;
       System.out.println();
       System.out.print("What is your first guess? ");
       while (true) {
          usersGuess = TextIO.getInt();  // Get the user's guess.
          guessCount++;
          if (usersGuess == computersNumber) {
             System.out.println("You got it in " + guessCount
                     + " guesses!  My number was " + computersNumber);
             break;  // The game is over; the user has won.
          }
          if (guessCount == 6) {
             System.out.println("You didn't get the number in 6 guesses.");
             System.out.println("You lose.  My number was " + computersNumber);
             break;  // The game is over; the user has lost.
          }
          // If we get to this point, the game continues.
          // Tell the user if the guess was too high or too low.
          if (usersGuess < computersNumber)
             System.out.print("That's too low.  Try again: ");
          else if (usersGuess > computersNumber)
             System.out.print("That's too high.  Try again: ");
       }
       System.out.println();
   } // end of playGame()
               
} // end of class GuessingGame
```

### Member Variables

A class can include other things besides subroutines. In particular, it can also include variable declarations. Of course, you can declare variables inside subroutines. Those are called **local variables**. However, you can also have variables that are not part of any subroutine. To distinguish such variables from local variables, we call them **member variables**, since they are members of a class. Another term for them is **global variable**.

#### member variables

```java
static String usersName;
public static int numberOfPlayers;
private static double velocity, time;
```

```java
import textio.TextIO;

public class GuessingGame2 {
 
    static int gamesPlayed;   // The number of games played.
    static int gamesWon;      // The number of games won.
 
    public static void main(String[] args) {
       gamesPlayed = 0;
       gamesWon = 0;  // This is actually redundant, since 0 is 
                      //                 the default initial value.
       System.out.println("Let's play a game.  I'll pick a number between");
       System.out.println("1 and 100, and you try to guess it.");
       boolean playAgain;
       do {
          playGame();  // call subroutine to play one game
          System.out.print("Would you like to play again? ");
          playAgain = TextIO.getlnBoolean();
       } while (playAgain);
       System.out.println();
       System.out.println("You played " + gamesPlayed + " games,");
       System.out.println("and you won " + gamesWon + " of those games.");
       System.out.println("Thanks for playing.  Goodbye.");
    } // end of main()            
    
    static void playGame() {
        int computersNumber; // A random number picked by the computer.
        int usersGuess;      // A number entered by user as a guess.
        int guessCount;      // Number of guesses the user has made.
        gamesPlayed++;  // Count this game.
        computersNumber = (int)(100 * Math.random()) + 1;
                 // The value assigned to computersNumber is a randomly
                 //    chosen integer between 1 and 100, inclusive.
        guessCount = 0;
        System.out.println();
        System.out.print("What is your first guess? ");
        while (true) {
           usersGuess = TextIO.getInt();  // Get the user's guess.
           guessCount++;
           if (usersGuess == computersNumber) {
              System.out.println("You got it in " + guessCount
                      + " guesses!  My number was " + computersNumber);
              gamesWon++;  // Count this win.
              break;       // The game is over; the user has won.
           }
           if (guessCount == 6) {
              System.out.println("You didn't get the number in 6 guesses.");
              System.out.println("You lose.  My number was " + computersNumber);
              break;  // The game is over; the user has lost.
           }
           // If we get to this point, the game continues.
           // Tell the user if the guess was too high or too low.
           if (usersGuess < computersNumber)
              System.out.print("That's too low.  Try again: ");
           else if (usersGuess > computersNumber)
              System.out.print("That's too high.  Try again: ");
        }
        System.out.println();
    } // end of playGame()
                
} // end of class GuessingGame2
```
