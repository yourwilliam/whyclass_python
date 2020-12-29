# \[course\]08 游戏模块02-2

## 点击游戏，和游戏帮助

1. 游戏的多个模块，可以使用ModelApp来启动，然后里面的每个模块会继承Model。
   1. 一般多个模块的部分，一般会在入口的地方注册每一个model
2. 针对Model模式，我们使用`mode.app.setActiveMode`来激活相应的model，只有被激活的模块才能被显示，以及调用其中相应的方法。这样我们就可以在游戏中增加不同的模块了。
3. 碰撞检测，如何检测到鼠标点击的地方和其中圆圈的地方重合。当mousePressed事件触发时，判断二者的相关关系

```python
from game_graphics import *
from tkinter import *
import random

class SplashScreenMode(Mode):
    def redrawAll(mode, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(mode.width/2, 150, text='This demos a ModalApp!', font=font)
        canvas.create_text(mode.width/2, 200, text='This is a modal splash screen!', font=font)
        canvas.create_text(mode.width/2, 250, text='Press any key for the game!', font=font)

    def keyPressed(mode, event):
        mode.app.setActiveMode(mode.app.gameMode)

class GameMode(Mode):
    def appStarted(mode):
        mode.score = 0
        mode.randomizeDot()

    def randomizeDot(mode):
        mode.x = random.randint(20, mode.width-20)
        mode.y = random.randint(20, mode.height-20)
        mode.r = random.randint(10, 20)
        mode.color = random.choice(['red', 'orange', 'yellow', 'green', 'blue'])
        mode.dx = random.choice([+1,-1])*random.randint(3,6)
        mode.dy = random.choice([+1,-1])*random.randint(3,6)

    def moveDot(mode):
        mode.x += mode.dx
        if (mode.x < 0) or (mode.x > mode.width): mode.dx = -mode.dx
        mode.y += mode.dy
        if (mode.y < 0) or (mode.y > mode.height): mode.dy = -mode.dy

    def timerFired(mode):
        mode.moveDot()

    def mousePressed(mode, event):
        d = ((mode.x - event.x)**2 + (mode.y - event.y)**2)**0.5
        if (d <= mode.r):
            mode.score += 1
            mode.randomizeDot()
        elif (mode.score > 0):
            mode.score -= 1

    def keyPressed(mode, event):
        if (event.key == 'h'):
            mode.app.setActiveMode(mode.app.helpMode)

    def redrawAll(mode, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(mode.width/2, 20, text=f'Score: {mode.score}', font=font)
        canvas.create_text(mode.width/2, 50, text='Click on the dot!', font=font)
        canvas.create_text(mode.width/2, 80, text='Press h for help screen!', font=font)
        canvas.create_oval(mode.x-mode.r, mode.y-mode.r, mode.x+mode.r, mode.y+mode.r,
                           fill=mode.color)

class HelpMode(Mode):
    def redrawAll(mode, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(mode.width/2, 150, text='This is the help screen!', font=font)
        canvas.create_text(mode.width/2, 250, text='(Insert helpful message here)', font=font)
        canvas.create_text(mode.width/2, 350, text='Press any key to return to the game!', font=font)

    def keyPressed(mode, event):
        mode.app.setActiveMode(mode.app.gameMode)

class MyModalApp(ModalApp):
    def appStarted(app):
        app.splashScreenMode = SplashScreenMode()
        app.gameMode = GameMode()
        app.helpMode = HelpMode()
        app.setActiveMode(app.splashScreenMode)
        app.timerDelay = 50

app = MyModalApp(width=500, height=500)
```

## 画布的延展

### 感知上的背景变化

1. 如何批量的创建随机点
2. 中心点不变我们通过参照物的整体的位置变化，让玩家感知上觉得是中心点在变化

```python
# SideScroller1:

from game_graphics import *
from tkinter import *
import random

class SideScroller1(App):
    def appStarted(self):
        self.scrollX = 0
        self.dots = [(random.randrange(self.width),
                      random.randrange(60, self.height)) for _ in range(50)]

    def keyPressed(self, event):
        if (event.key == "Left"):    self.scrollX -= 5
        elif (event.key == "Right"): self.scrollX += 5

    def redrawAll(self, canvas):
        # draw the player fixed to the center of the scrolled canvas
        cx, cy, r = self.width/2, self.height/2, 10
        canvas.create_oval(cx-r, cy-r, cx+r, cy+r, fill='cyan')

        # draw the dots, shifted by the scrollX offset
        for (cx, cy) in self.dots:
            cx -= self.scrollX  # <-- This is where we scroll each dot!!!
            canvas.create_oval(cx-r, cy-r, cx+r, cy+r, fill='lightGreen')

        # draw the x and y axes
        x = self.width/2 - self.scrollX # <-- This is where we scroll the axis!
        y = self.height/2
        canvas.create_line(x, 0, x, self.height)
        canvas.create_line(0, y, self.width, y)

        # draw the instructions and the current scrollX
        x = self.width/2
        canvas.create_text(x, 20, text='Use arrows to move left or right')
        canvas.create_text(x, 40, text=f'app.scrollX = {self.scrollX}')

SideScroller1(width=300, height=300)
```

### 感知上的物体变化

1. 中央player移动，到边界时移动背景内容，感受背景变化

```python
# SideScroller2:

# Now with a scroll margin, so player does not stay fixed
# at the center of the scrolled canvas, and we only scroll
# if the player's center (in this case) gets closer than the
# margin to the left or right edge of the canvas.

from game_graphics import *
from tkinter import *
import random

class SideScroller2(App):
    def appStarted(self):
        self.scrollX = 0
        self.scrollMargin = 50
        self.playerX = self.width//2 # player's center
        self.dots = [(random.randrange(self.width),
                      random.randrange(60, self.height)) for _ in range(50)]

    def makePlayerVisible(self):
        # scroll to make player visible as needed
        if (self.playerX < self.scrollX + self.scrollMargin):
            self.scrollX = self.playerX - self.scrollMargin
        if (self.playerX > self.scrollX + self.width - self.scrollMargin):
            self.scrollX = self.playerX - self.width + self.scrollMargin

    def movePlayer(self, dx, dy):
        self.playerX += dx
        self.makePlayerVisible()

    def keyPressed(self, event):
        if (event.key == "Left"):    self.movePlayer(-5, 0)
        elif (event.key == "Right"): self.movePlayer(+5, 0)

    def redrawAll(self, canvas):
        # draw the player, shifted by the scrollX offset
        cx, cy, r = self.playerX, self.height/2, 10
        cx -= self.scrollX # <-- This is where we scroll the player!!!
        canvas.create_oval(cx-r, cy-r, cx+r, cy+r, fill='cyan')

        # draw the dots, shifted by the scrollX offset
        for (cx, cy) in self.dots:
            cx -= self.scrollX  # <-- This is where we scroll each dot!!!
            canvas.create_oval(cx-r, cy-r, cx+r, cy+r, fill='lightGreen')

        # draw the x and y axes
        x = self.width/2 - self.scrollX # <-- This is where we scroll the axis!
        y = self.height/2
        canvas.create_line(x, 0, x, self.height)
        canvas.create_line(0, y, self.width, y)

        # draw the instructions and the current scrollX
        x = self.width/2
        canvas.create_text(x, 20, text='Use arrows to move left or right')
        canvas.create_text(x, 40, text=f'app.scrollX = {self.scrollX}')

SideScroller2(width=300, height=300)
```

### 触碰游戏

1. getWallHit 碰撞检测
2. 积分

```python
# SideScroller3:

# Now with walls that track when you run into them (but
# ignore while you are still crossing them).

from game_graphics import *
from tkinter import *

class SideScroller3(App):
    def appStarted(self):
        self.scrollX = 0
        self.scrollMargin = 50
        self.playerX = self.scrollMargin
        self.playerY = 0
        self.playerWidth = 10
        self.playerHeight = 20
        self.walls = 5
        self.wallPoints = [0]*self.walls
        self.wallWidth = 20
        self.wallHeight = 40
        self.wallSpacing = 90 # wall left edges are at 90, 180, 270,...
        self.currentWallHit = -1 # start out not hitting a wall

    def getPlayerBounds(self):
        # returns absolute bounds, not taking scrollX into account
        (x0, y1) = (self.playerX, self.height/2 - self.playerY)
        (x1, y0) = (x0 + self.playerWidth, y1 - self.playerHeight)
        return (x0, y0, x1, y1)

    def getWallBounds(self, wall):
        # returns absolute bounds, not taking scrollX into account
        (x0, y1) = ((1+wall) * self.wallSpacing, self.height/2)
        (x1, y0) = (x0 + self.wallWidth, y1 - self.wallHeight)
        return (x0, y0, x1, y1)

    def getWallHit(self):
        # return wall that player is currently hitting
        # note: this should be optimized to only check the walls that are visible
        # or even just directly compute the wall without a loop
        playerBounds = self.getPlayerBounds()
        for wall in range(self.walls):
            wallBounds = self.getWallBounds(wall)
            if (self.boundsIntersect(playerBounds, wallBounds) == True):
                return wall
        return -1

    def boundsIntersect(self, boundsA, boundsB):
        # return l2<=r1 and t2<=b1 and l1<=r2 and t1<=b2
        (ax0, ay0, ax1, ay1) = boundsA
        (bx0, by0, bx1, by1) = boundsB
        return ((ax1 >= bx0) and (bx1 >= ax0) and
                (ay1 >= by0) and (by1 >= ay0))

    def checkForNewWallHit(self):
        # check if we are hitting a new wall for the first time
        wall = self.getWallHit()
        if (wall != self.currentWallHit):
            self.currentWallHit = wall
            if (wall >= 0):
                self.wallPoints[wall] += 1

    def makePlayerVisible(self):
        # scroll to make player visible as needed
        if (self.playerX < self.scrollX + self.scrollMargin):
            self.scrollX = self.playerX - self.scrollMargin
        if (self.playerX > self.scrollX + self.width - self.scrollMargin):
            self.scrollX = self.playerX - self.width + self.scrollMargin

    def movePlayer(self, dx, dy):
        self.playerX += dx
        self.playerY += dy
        self.makePlayerVisible()
        self.checkForNewWallHit()

    def sizeChanged(self):
        self.makePlayerVisible()

    def mousePressed(self, event):
        self.playerX = event.x + self.scrollX
        self.checkForNewWallHit()

    def keyPressed(self, event):
        if (event.key == "Left"):    self.movePlayer(-5, 0)
        elif (event.key == "Right"): self.movePlayer(+5, 0)
        elif (event.key == "Up"):    self.movePlayer(0, +5)
        elif (event.key == "Down"):  self.movePlayer(0, -5)

    def redrawAll(self, canvas):
        # draw the base line
        lineY = self.height/2
        lineHeight = 5
        canvas.create_rectangle(0, lineY, self.width, lineY+lineHeight,fill="black")

        # draw the walls
        # (Note: should optimize to only consider walls that can be visible now!)
        sx = self.scrollX
        for wall in range(self.walls):
            (x0, y0, x1, y1) = self.getWallBounds(wall)
            fill = "orange" if (wall == self.currentWallHit) else "pink"
            canvas.create_rectangle(x0-sx, y0, x1-sx, y1, fill=fill)
            (cx, cy) = ((x0+x1)/2 - sx, (y0 + y1)/2)
            canvas.create_text(cx, cy, text=str(self.wallPoints[wall]))
            cy = lineY + 5
            canvas.create_text(cx, cy, text=str(wall), anchor=N)

        # draw the player
        (x0, y0, x1, y1) = self.getPlayerBounds()
        canvas.create_oval(x0 - sx, y0, x1 - sx, y1, fill="cyan")

        # draw the instructions
        msg = "Use arrows to move, hit walls to score"
        canvas.create_text(self.width/2, 20, text=msg)

SideScroller3(width=300, height=300)
```

