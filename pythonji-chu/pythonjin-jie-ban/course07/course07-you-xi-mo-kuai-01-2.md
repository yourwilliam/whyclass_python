# \[course]07 游戏模块01-2

## 添加和删除图形

### 使用List添加删除图形 ，不使用class的形式

```python
from game_graphics import *
from tkinter import *

def appStarted(app):
    app.circleCenters = [ ]

def mousePressed(app, event):
    newCircleCenter = (event.x, event.y)
    app.circleCenters.append(newCircleCenter)

def keyPressed(app, event):
    if (event.key == 'd'):
        if (len(app.circleCenters) > 0):
            app.circleCenters.pop(0)
        else:
            print('No more circles to delete!')

def redrawAll(app, canvas):
    # draw the circles
    for circleCenter in app.circleCenters:
        (cx, cy) = circleCenter
        r = 20
        canvas.create_oval(cx-r, cy-r, cx+r, cy+r, fill='cyan')
    # draw the text
    canvas.create_text(app.width/2, 20,
                       text='Example: Adding and Deleting Shapes')
    canvas.create_text(app.width/2, 40,
                       text='Mouse clicks create circles')
    canvas.create_text(app.width/2, 60,
                       text='Pressing "d" deletes circles')

runApp(width=400, height=400)
```

### 使用class添加

```python
from game_graphics import *
from tkinter import *
import random

class Dot(object):
    def __init__(self, cx, cy):
        self.cx = cx
        self.cy = cy
        # let's add random sizes and colors, too
        # (since it's so easy to store these with each Dot instance)
        colors = ['red', 'orange', 'yellow', 'green', 'blue']
        self.fill = random.choice(colors)
        self.r = random.randint(5, 40)

def appStarted(app):
    app.dots = [ ]

def mousePressed(app, event):
    newDot = Dot(event.x, event.y)
    app.dots.append(newDot)

def keyPressed(app, event):
    if (event.key == 'd'):
        if (len(app.dots) > 0):
            app.dots.pop(0)
        else:
            print('No more circles to delete!')

def redrawAll(app, canvas):
    # draw the circles
    for dot in app.dots:
        canvas.create_oval(dot.cx-dot.r, dot.cy-dot.r,
                           dot.cx+dot.r, dot.cy+dot.r,
                           fill=dot.fill)
    # draw the text
    canvas.create_text(app.width/2, 20,
                       text='Example: Adding and Deleting Shapes')
    canvas.create_text(app.width/2, 40,
                       text='Mouse clicks create circles')
    canvas.create_text(app.width/2, 60,
                       text='Pressing "d" deletes circles')

runApp(width=400, height=400)
```

作业：使用A按钮，来随机添加一个正方形，使用D可以删除

### 通过鼠标选择相应的grid

modelToView 和 viewToModel

```python
from game_graphics import *
from tkinter import *

def appStarted(app):
    app.rows = 4
    app.cols = 8
    app.margin = 5 # margin around grid
    app.selection = (-1, -1) # (row, col) of selection, (-1,-1) for none

def pointInGrid(app, x, y):
    # return True if (x, y) is inside the grid defined by app.
    return ((app.margin <= x <= app.width-app.margin) and
            (app.margin <= y <= app.height-app.margin))

def getCell(app, x, y):
    # aka "viewToModel"
    # return (row, col) in which (x, y) occurred or (-1, -1) if outside grid.
    if (not pointInGrid(app, x, y)):
        return (-1, -1)
    gridWidth  = app.width - 2*app.margin
    gridHeight = app.height - 2*app.margin
    cellWidth  = gridWidth / app.cols
    cellHeight = gridHeight / app.rows

    # Note: we have to use int() here and not just // because
    # row and col cannot be floats and if any of x, y, app.margin,
    # cellWidth or cellHeight are floats, // would still produce floats.
    row = int((y - app.margin) / cellHeight)
    col = int((x - app.margin) / cellWidth)

    return (row, col)

def getCellBounds(app, row, col):
    # aka "modelToView"
    # returns (x0, y0, x1, y1) corners/bounding box of given cell in grid
    gridWidth  = app.width - 2*app.margin
    gridHeight = app.height - 2*app.margin
    columnWidth = gridWidth / app.cols
    rowHeight = gridHeight / app.rows
    x0 = app.margin + col * columnWidth
    x1 = app.margin + (col+1) * columnWidth
    y0 = app.margin + row * rowHeight
    y1 = app.margin + (row+1) * rowHeight
    return (x0, y0, x1, y1)

def mousePressed(app, event):
    (row, col) = getCell(app, event.x, event.y)
    # select this (row, col) unless it is selected
    if (app.selection == (row, col)):
        app.selection = (-1, -1)
    else:
        app.selection = (row, col)

def redrawAll(app, canvas):
    # draw grid of cells
    for row in range(app.rows):
        for col in range(app.cols):
            (x0, y0, x1, y1) = getCellBounds(app, row, col)
            fill = "orange" if (app.selection == (row, col)) else "cyan"
            canvas.create_rectangle(x0, y0, x1, y1, fill=fill)
    canvas.create_text(app.width/2, app.height/2 - 15, text="Click in cells!",
                       font="Arial 26 bold", fill="darkBlue")

runApp(width=400, height=400)
```

## 自己运动的方块

```python
from game_graphics import *
from tkinter import *


def appStarted(app):
    app.squareLeft = app.width // 2
    app.squareTop = app.height // 2
    app.squareSize = 25
    app.dx = 10
    app.dy = 15
    app.isPaused = False
    app.timerDelay = 50  # milliseconds


def keyPressed(app, event):
    if (event.key == "p"):
        app.isPaused = not app.isPaused
    elif (event.key == "s"):
        doStep(app)


def timerFired(app):
    if (not app.isPaused):
        doStep(app)


def doStep(app):
    # Move horizontally
    app.squareLeft += app.dx

    # Check if the square has gone out of bounds, and if so, reverse
    # direction, but also move the square right to the edge (instead of
    # past it). Note: there are other, more sophisticated ways to
    # handle the case where the square extends beyond the edges...
    if app.squareLeft < 0:
        # if so, reverse!
        app.squareLeft = 0
        app.dx = -app.dx
    elif app.squareLeft > app.width - app.squareSize:
        app.squareLeft = app.width - app.squareSize
        app.dx = -app.dx

    # Move vertically the same way
    app.squareTop += app.dy
    if app.squareTop < 0:
        # if so, reverse!
        app.squareTop = 0
        app.dy = -app.dy
    elif app.squareTop > app.height - app.squareSize:
        app.squareTop = app.height - app.squareSize
        app.dy = -app.dy


def redrawAll(app, canvas):
    # draw the square
    canvas.create_rectangle(app.squareLeft,
                            app.squareTop,
                            app.squareLeft + app.squareSize,
                            app.squareTop + app.squareSize,
                            fill="yellow")
    # draw the text
    canvas.create_text(app.width / 2, 20,
                       text="Pressing 'p' pauses/unpauses timer")
    canvas.create_text(app.width / 2, 40,
                       text="Pressing 's' steps the timer once")


runApp(width=400, height=150)
```

## 贪食蛇

```python
from game_graphics import *
from tkinter import *
import random

def appStarted(app):
    app.rows = 10
    app.cols = 10
    app.margin = 5 # margin around grid
    app.timerDelay = 250
    initSnakeAndFood(app)
    app.waitingForFirstKeyPress = True

def initSnakeAndFood(app):
    app.snake = [(0,0)]
    app.direction = (0, +1) # (drow, dcol)
    placeFood(app)
    app.gameOver = False

# getCellBounds from grid-demo.py
def getCellBounds(app, row, col):
    # aka 'modelToView'
    # returns (x0, y0, x1, y1) corners/bounding box of given cell in grid
    gridWidth  = app.width - 2*app.margin
    gridHeight = app.height - 2*app.margin
    x0 = app.margin + gridWidth * col / app.cols
    x1 = app.margin + gridWidth * (col+1) / app.cols
    y0 = app.margin + gridHeight * row / app.rows
    y1 = app.margin + gridHeight * (row+1) / app.rows
    return (x0, y0, x1, y1)

def keyPressed(app, event):
    if (app.waitingForFirstKeyPress):
        app.waitingForFirstKeyPress = False
    elif (event.key == 'r'):
        initSnakeAndFood(app)
    elif app.gameOver:
        return
    elif (event.key == 'Up'):      app.direction = (-1, 0)
    elif (event.key == 'Down'):  app.direction = (+1, 0)
    elif (event.key == 'Left'):  app.direction = (0, -1)
    elif (event.key == 'Right'): app.direction = (0, +1)
    # elif (event.key == 's'):
        # this was only here for debugging, before we turned on the timer
        # takeStep(app)

def timerFired(app):
    if app.gameOver or app.waitingForFirstKeyPress: return
    takeStep(app)

def takeStep(app):
    (drow, dcol) = app.direction
    (headRow, headCol) = app.snake[0]
    (newRow, newCol) = (headRow+drow, headCol+dcol)
    if ((newRow < 0) or (newRow >= app.rows) or
        (newCol < 0) or (newCol >= app.cols) or
        ((newRow, newCol) in app.snake)):
        app.gameOver = True
    else:
        app.snake.insert(0, (newRow, newCol))
        if (app.foodPosition == (newRow, newCol)):
            placeFood(app)
        else:
            # didn't eat, so remove old tail (slither forward)
            app.snake.pop()

def placeFood(app):
    # Keep trying random positions until we find one that is not in
    # the snake. Note: there are more sophisticated ways to do this.
    while True:
        row = random.randint(0, app.rows-1)
        col = random.randint(0, app.cols-1)
        if (row,col) not in app.snake:
            app.foodPosition = (row, col)
            return

def drawBoard(app, canvas):
    for row in range(app.rows):
        for col in range(app.cols):
            (x0, y0, x1, y1) = getCellBounds(app, row, col)
            canvas.create_rectangle(x0, y0, x1, y1, fill='white')

def drawSnake(app, canvas):
    for (row, col) in app.snake:
        (x0, y0, x1, y1) = getCellBounds(app, row, col)
        canvas.create_oval(x0, y0, x1, y1, fill='blue')

def drawFood(app, canvas):
    if (app.foodPosition != None):
        (row, col) = app.foodPosition
        (x0, y0, x1, y1) = getCellBounds(app, row, col)
        canvas.create_oval(x0, y0, x1, y1, fill='green')

def drawGameOver(app, canvas):
    if (app.gameOver):
        canvas.create_text(app.width/2, app.height/2, text='Game over!',
                           font='Arial 26 bold')
        canvas.create_text(app.width/2, app.height/2+40,
                           text='Press r to restart!',
                           font='Arial 26 bold')

def redrawAll(app, canvas):
    if (app.waitingForFirstKeyPress):
        canvas.create_text(app.width/2, app.height/2,
                           text='Press any key to start!',
                           font='Arial 26 bold')
    else:
        drawBoard(app, canvas)
        drawSnake(app, canvas)
        drawFood(app, canvas)
        drawGameOver(app, canvas)

runApp(width=400, height=400)
```

作业： 1. 增加游戏难度选择 1. normal:保持原本 2. hard:地图扩大1倍，游戏速度增加1倍 3. hell:地图扩大2倍，游戏速度增加2倍 2. 游戏结束后给出分数 3. 将最高分数进行记录，结束后显示 1. 只在运行时保存，运行结束后清零 2. 一直保存 4. 一次多加几个Food
