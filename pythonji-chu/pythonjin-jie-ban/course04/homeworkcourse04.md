# \[homework]course04

### 课前作业

python 3.9及以下：

下载 [collapsar\_week3\_linter.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_week3\_linter.py) 和 [collapsar\_hw\_week3.py](https://ossp.pengjunjie.com/collapsar-homework-3-9/collapsar\_hw\_week3.py)文件。拷贝到week3的文件夹中。

其中youyulab\_week3\_linter.py文件不需要改动

python 3.10 及以上：

下载 [collapsar\_hw\_week3.py](https://ossp.pengjunjie.com/collapsar-homework-3-10/collapsar\_hw\_week3.py)

打开youyulab\_hw\_week3.py 文件

### 作业内容

#### 1. **patternedMessage(message, pattern)**&#x20;

Write the function patternedMessage(message, pattern) that takes two strings, a message and a pattern, and returns a string produced by replacing the non-whitespace characters in the pattern with the non-whitespace characters in the message. As a first example:

![-w472](http://ossp.pengjunjie.com/mweb/15751829941769.jpg)

Here, the message is "Go Pirates!!!" and the pattern is a block of asterisks with a few missing in the middle. Notice how the whitespace in the pattern is preserved, but the whitespace in the message is removed. Also, note that any leading or trailing newlines in the pattern are removed.

Here is another example:

![-w517](http://ossp.pengjunjie.com/mweb/15751830169164.jpg)

Hint: While you may solve this how you wish, our sample solution did not use replace in any way. Instead, we started with the empy string, and built up the result character by character. How did we determine the next character? Using both the message and the pattern in some way...

Here are two more straightforward examples:

```py
assert(patternedMessage("abc def",   "***** ***** ****")   ==
       "abcde fabcd efab")
assert(patternedMessage("abc def", "\n***** ***** ****\n") == 
       "abcde fabcd efab")
```

And here is one last example, just for fun:

```py
patternedMessage("Go Steelers!",
"""
                          oooo$$$$$$$$$$$$oooo
                      oo$$$$$$$$$$$$$$$$$$$$$$$$o
                   oo$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$o         o$   $$ o$
   o $ oo        o$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$o       $$ $$ $$o$
oo $ $ '$      o$$$$$$$$$    $$$$$$$$$$$$$    $$$$$$$$$o       $$$o$$o$
'$$$$$$o$     o$$$$$$$$$      $$$$$$$$$$$      $$$$$$$$$$o    $$$$$$$$
  $$$$$$$    $$$$$$$$$$$      $$$$$$$$$$$      $$$$$$$$$$$$$$$$$$$$$$$
  $$$$$$$$$$$$$$$$$$$$$$$    $$$$$$$$$$$$$    $$$$$$$$$$$$$$  '$$$
   '$$$'$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$     '$$$
    $$$   o$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$     '$$$o
   o$$'   $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$       $$$o
   $$$    $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$' '$$$$$$ooooo$$$$o
  o$$$oooo$$$$$  $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$   o$$$$$$$$$$$$$$$$$
  $$$$$$$$'$$$$   $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$     $$$$'
 ''''       $$$$    '$$$$$$$$$$$$$$$$$$$$$$$$$$$$'      o$$$
            '$$$o     '$$$$$$$$$$$$$$$$$$'$$'         $$$
              $$$o          '$$'$$$$$$'           o$$$
               $$$$o                                o$$$'
                '$$$$o      o$$$$$$o'$$$$o        o$$$$
                  '$$$$$oo     '$$$$o$$$$$o   o$$$$'
                     '$$$$$oooo  '$$$o$$$$$$$$$'
                        '$$$$$$$oo $$$$$$$$$$
                                '$$$$$$$$$$$
                                    $$$$$$$$$$$$
                                     $$$$$$$$$$'
                                      '$$$'
""")
```

```
Returns this:
```

```
                          GoSteelers!GoSteeler
                      s!GoSteelers!GoSteelers!GoS
                   teelers!GoSteelers!GoSteelers!GoS         te   el er
   s ! Go        Steelers!GoSteelers!GoSteelers!GoSteel       er s! GoSt
ee l e rs      !GoSteeler    s!GoSteelers!    GoSteelers       !GoSteel
ers!GoSte     elers!GoSt      eelers!GoSt      eelers!GoSt    eelers!G
  oSteele    rs!GoSteele      rs!GoSteele      rs!GoSteelers!GoSteeler
  s!GoSteelers!GoSteelers    !GoSteelers!G    oSteelers!GoSt  eele
   rs!GoSteelers!GoSteelers!GoSteelers!GoSteelers!GoSteel     ers!
    GoS   teelers!GoSteelers!GoSteelers!GoSteelers!GoSteelers     !GoSt
   eele   rs!GoSteelers!GoSteelers!GoSteelers!GoSteelers!GoSt       eele
   rs!    GoSteelers!GoSteelers!GoSteelers!GoSteelers!Go Steelers!GoSteele
  rs!GoSteelers  !GoSteelers!GoSteelers!GoSteelers!GoS   teelers!GoSteelers
  !GoSteelers!G   oSteelers!GoSteelers!GoSteelers!Go     Steel
 ers!       GoSt    eelers!GoSteelers!GoSteelers!G      oSte
            elers     !GoSteelers!GoSteelers!         GoS
              teel          ers!GoSteel           ers!
               GoSte                                elers
                !GoSte      elers!GoSteele        rs!Go
                  Steelers     !GoSteelers!   GoStee
                     lers!GoSte  elers!GoSteeler
                        s!GoSteele rs!GoSteel
                                ers!GoSteele
                                    rs!GoSteeler
                                     s!GoSteeler
                                      s!GoS
```

**Hint:** You will almost surely want to print strings to help you debug here, but whitespace can be quite tricky in this problem. So... Instead of using `print(s)` in your debugging, use `print(repr(s))`. That way, you can easily see the whitespace. This can make a **huge** difference in how long this problem takes! We highly recommend using this advice.

#### 2. **encodeRightLeftRouteCipher(message,rows)**

Background: A right-left route cipher is a fairly simple way to encrypt a message. It takes two values, some plaintext and a number of rows, and it first constructs a grid with that number of rows and the minimum number of columns required, writing the message in successive columns. For example, if the message is WEATTACKATDAWN, with 4 rows, the grid would be:

```
        W T A W
        E A T N
        A C D
        T K A
```

We will assume the message only contains uppercase letters. We'll fill in the missing grid entries with lowercase letters starting from z and going in reverse (wrapping around if necessary), so we have:

```
        W T A W
        E A T N
        A C D z
        T K A y
```

Next, we encrypt the text by reading alternating rows first to the right ("WTAW"), then to the left ("NTAE"), then back to the right ("ACDz"), and back to the left ("yAKT"), until we finish all rows. We precede these values with the number of rows itself in the string. So the encrypted value for the message WEATTACKATDAWN with 4 rows is "4WTAWNTAEACDzyAKT".

With this in mind, write the function encodeRightLeftRouteCipher that takes an all-uppercase message and a positive integer number of rows, and returns the encoding as just described.

Here are a few more examples to consider:

```py
assert(encodeRightLeftRouteCipher("WEATTACKATDAWN",4) == "4WTAWNTAEACDzyAKT")
assert(encodeRightLeftRouteCipher("WEATTACKATDAWN",3) == "3WTCTWNDKTEAAAAz") 
assert(encodeRightLeftRouteCipher("WEATTACKATDAWN",5) == "5WADACEAKWNATTTz") 
 
```

Be sure to take the time to fully understand each of those examples!

**Hint:** the grid described above is only conceptual. Your code will never actually construct a 2-dimensional grid (especially as you may not yet use lists!). Instead, you should use a clever scheme of indexing the message string where you translate a row and column into a single index into the message string.

**More complete hint:** let's do this example in a bit more detail, and we'll even provide an idea or two on how to simplify solving this:

```py
assert(encodeRightLeftRouteCipher("WEATTACKATDAWN",3) == "3WTCTWNDKTEAAAAz") 
   
```

1. **Find the dimensions of the conceptual 2d grid** Since len('WEATTACKATDAWN') is 14, and we have 3 rows, we need math.ceil(14/3) or 5 columns.
2. **Pad the string** We need 3\*5, or 15 letters. We have 14. We have to add one. So we now have 'WEATTACKATDAWNz'
3. **Imagine the conceptual 2d grid** We do not create this part. We just imagine it. But this is the 2d grid we imagine:

```
W T C T W
E T K D N
A A A A z
```

1. **Label your rows and cols** To be sure we are visualizing the grid properly, let's add row and col labels, like so:

```
           col0  col1  col2  col3  col4
    row0:    W     T     C     T     W
    row1:    E     T     K     D     N
    row2:    A     A     A     A     z
    
```

1. **Label the padded string with row, col, and i** Let's use these row and col labels, but write them over the padded string (instead of the conceptual 2d grid). We'll also include the index i, like so:

```
        row:  0  1  2  0  1  2  0  1  2  0  1  2  0  1  2
        col:  0  0  0  1  1  1  2  2  2  3  3  3  4  4  4
        i:    0  1  2  3  4  5  6  7  8  9 10 11 12 13 14
              W  E  A  T  T  A  C  K  A  T  D  A  W  N  z
    
```

1. **Find a function f(row,col) --> i** Look at the patterns in the row, col, and i in the table we just made. See if you can find a function f(row, col) that takes any row and col (in the conceptual 2d grid) and returns the corresponding index i (in the padded string). Also, name this function something better than f.

* Hint: from the table above, we see that the K is in row 1 and column 2, and the K is at index 7 in the padded string, so... `f(1,2) == 7`
* Hint: see how the row in the table above repeats: 0, 1, 2, 0, 1, 2,... What does this have to do with the fact that we have 3 total rows?

1. **Now, traverse the 2d grid top-to-bottom, left-to-right** This step is not required, but it is super helpful. As only a temporary measure, we will solve a slightly easier version of the problem: we will simply ignore that every other row goes right-to-left. We'll make every row go left-to-right just for now. So use two loops, one going over every row, and inside that, one going over every column. For each row,col pair, use your function f() that you just wrote (and renamed) to find the index in the padded string. Remember that this was the conceptual grid:

```
WTCTW
ETKDN
AAAAz
```

```
And so, when you are done with this step, you should have a string like this (which, again, is not the real solution, since we always go left-to-right):
```

```
WTCTWETKDNAAAAz
```

1. **Now alternate left-to-right and right-to-left** Now make every-other-row go the other way. So the second row will change from ETKDN to NDKTE, like so:

```
WTCTWNDKTEAAAAz
```

1. **Add the rows as a prefix** Easy enough:

```
3WTCTWNDKTEAAAAz
```

1. **Return that string** We are done. To remind ourselves, here was the test case:

```
assert(encodeRightLeftRouteCipher("WEATTACKATDAWN",3) == "3WTCTWNDKTEAAAAz") 
```

#### 3.**decodeRightLeftRouteCipher(message)**

Write the function decodeRightLeftRouteCipher, which takes an encoding from the previous problem and runs it in reverse, returning the plaintext that generated the encoding. For example, decodeRightLeftRouteCipher("4WTAWNTAEACDzyAKT") returns "WEATTACKATDAWN".

#### 4.**drawSimpleTortoiseProgram(program, canvas, width, height)**

In addition to the Tkinter which we all know and love, Python usually comes with another graphics package called "Turtle Graphics", which you can read about [here](https://docs.python.org/2/library/turtle.html). We will definitely not be using turtle graphics in this problem (and you may not do so in your solution!), but we will instead implement a small turtle-like (or maybe turtle-inspired) graphics language of our own. We'll call it Tortoise Graphics.

First, we need to understand how Tortoise Graphics programs work. Your tortoise starts in the middle of the screen, heading to the right. You can direct your tortoise with the following commands:

* **color name** Set the drawing color to the given name, which is entered without quotes, and which can be "red", "blue", "green", or any other color that Tkinter understands. It can also be "none", meaning to not draw.
* **move n** Move n pixels straight ahead, where n is a non-negative integer, while drawing a 4-pixel-wide line in the current drawing color. If the drawing color is "none", just move straight ahead without drawing (that is, just change the tortoise's location).
* **left n** Turn n degrees to the left, without moving, where n is a non-negative integer.
* **right n** Turn n degrees to the right, without moving, where n is a non-negative integer. Commands are given one-per-line. Lines can also contain comments, denoted by the hash sign (#), and everything from there to the end-of-line is ignored. Blank lines and lines containing only whitespace and/or comments are also ignored.

With this in mind, write the function drawSimpleTortoiseProgram(program, canvas, width, height) that takes a program as specified above and runs it, displaying it in the given canvas of the given width and height. Your function should also display the tortoise program in that window, in a 10-point font, in gray text, running down the left-hand side of the window (say 10 pixels from the left edge). Don't worry if the program is longer than can fit in the window (no need to scroll or otherwise deal with this). Also, you are not responsible for any syntax errors or runtime errors in the tortoise program.

Note that the starter code includes the helpful function runDrawSimpleTortoiseProgram(program, width, height) that creates a window and a canvas and then calls drawSimpleTortoiseProgram(program, canvas, width, height).

For example, this call:

```py
runDrawSimpleTortoiseProgram("""
# This is a simple tortoise program
color blue
move 50

left 90

color red
move 100

color none # turns off drawing
move 50

right 45

color green # drawing is on again
move 50

right 45

color orange
move 50

right 90

color purple
move 100
""", 300, 400)
```

produces this result in a 300x400 window: ![](http://ossp.pengjunjie.com/mweb/hw4-tortoise1.png)

And this call:

```py
runDrawSimpleTortoiseProgram("""
# Y
color red
right 45
move 50
right 45
move 50
right 180
move 50
right 45
move 50
color none # space
right 45
move 25

# E
color green
right 90
move 85
left 90
move 50
right 180
move 50
right 90
move 42
right 90
move 50
right 180
move 50
right 90
move 43
right 90
move 50  # space
color none
move 25

# S
color blue
move 50
left 180
move 50
left 90
move 43
left 90
move 50
right 90
move 42
right 90
move 50
""", 500, 500)
```

produces this result in a 500x500 window: ![](http://ossp.pengjunjie.com/mweb/hw4-tortoise2.png)

#### 5. **drawNiceRobot(canvas, width, height)**

Write a function drawNiceRobot(canvas, width, height) that (you guessed it!) draws a nice robot! This is not meant to be very difficult. We just want to see some really cool robots while grading your homework. Your function must make a drawing using Tkinter that meets the following criteria:

1. Easily identifiable as a robot
2. Includes at least 10 shapes total, including at least one oval, one rectangle, one non-rectangular polygon, and one line
3. Uses at least 4 colors
4. Resizes with the canvas. (You may assume that the canvas will always resize proportionally, and you may change the starting proportions in the test case if you want to)Do not use anything we haven't learned in class or in the notes through Week 3! No extra files, no importing anything other than Tkinter. Have fun!
