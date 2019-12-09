# [Game Project]flappy bird 游戏

## 背景知识

### 1. 物体上升和下落

为了做出和现实感觉一致的上升和下落的感觉，我们需要在物体的上升和下落的情况下使用重力加速度，公式`V=gt`，其中g是重力，t是下落的时间

## 开发流程

![flappy_story](http://ossp.pengjunjie.com/mweb/flappy_story.jpg)

### 1. 基础框架，显示多个页面

基本框架包含三个对象，背景图片Background、管道Pipe和小鸟Bird。页面模型包含三个，开始页模型SplashScreenMode、游戏页模型GameMode、帮助也模型HelpMode和结束页模型EndMode。

不同模型之间通过按键来触发

```py
from game_graphics import *
from tkinter import *

class Bird(object):
    def __init__(self, mode):
        pass


class Background(object):
    def __init__(self, mode):
        pass


class Pipe(object):
    def __init__(self, mode):
        pass

class SplashScreenMode(Mode):
    def appStarted(self):
        pass

    def redrawAll(self, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(self.width / 2, 150, text='Welcome to Black Bird', font=font)
        canvas.create_text(self.width / 2, 250, text='Press Space key for the game!', font=font)

    def timerFired(self):
        pass


    def keyPressed(self, event):
        if event.key == 'Space':
            self.app.setActiveMode(self.app.gameMode)


class GameMode(Mode):
    def appStarted(self):
        pass

    def timerFired(self):
        pass

    def mousePressed(self, event):
        pass

    def keyPressed(self, event):
        if event.key == 'h':
            self.app.setActiveMode(self.app.helpMode)

    def redrawAll(self, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(20, 20, text=f'start game', font=font)


class HelpMode(Mode):
    def redrawAll(mode, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(mode.width / 2, 150, text='This is the help screen!', font=font)
        canvas.create_text(mode.width / 2, 250, text='(Insert helpful message here)', font=font)
        canvas.create_text(mode.width / 2, 350, text='Press any key to return to the game!', font=font)

    def keyPressed(mode, event):
        mode.app.setActiveMode(mode.app.gameMode)


class EndMode(Mode):
    def appStarted(self):
        pass

    def redrawAll(self, canvas):
        font = 'Arial 26 bold'
        canvas.create_text(self.width / 2, 150, text='Game Over', font=font)
        canvas.create_text(self.width / 2, 250, text=f'Your score is : {self.score}', font=font)
        canvas.create_text(self.width / 2, 350, text='Press Space to restart to the game!', font=font)

    def keyPressed(self, event):
        if event.key == "Space":
            # 游戏重新开始
            self.app.gameMode = GameMode()
            self.app.setActiveMode(self.app.gameMode)


class MyModalApp(ModalApp):
    def appStarted(app):
        app.splashScreenMode = SplashScreenMode()
        app.gameMode = GameMode()
        app.helpMode = HelpMode()
        app.endMode = EndMode()
        app.setActiveMode(app.splashScreenMode)
        app.timerDelay = 33


app = MyModalApp(width=400, height=600)

```

### 开始页基本流程

#### 1. 导入bird图片，导入background图片

```py
bird_image = mode.loadImage(url)
sprite_strip = mode.scaleImage(bird_image, image_scale)
```

使用loadImage和scaleImage来导入图片并动态变化图片。并展示在开始页上

#### 2. 使用SpriteSheet形成可飞行的小鸟和自动滚动的背景。

小鸟图和背景图可以自己去寻找，小鸟图直接使用spritesheets来进行制作即可。

背景图可以使用两种方式，一种依然使用雪碧图，另外一种可以让图片的位置不停的变动来模拟滚动的场景。

完成效果

![-w185](http://ossp.pengjunjie.com/mweb/15758792514436.jpg)

### 游戏页基本流程

#### 1. 小鸟跳跃行为

模拟小鸟正常时的自由落体掉落，按空格键进行向上跳跃

#### 2. 小鸟跳出屏幕判断结束

小鸟跳珠屏幕的判断，如何切换到EndMode状态。EndMode状态如何切换到开始游戏状态

#### 3. 添加水管

添加移动的水管，由于水管很多，可以使用list来存储所有水管内容。

简单的水管模式，使用同X轴，上下排列。

#####3.1 导入上下排列的水管

做一个固定的上下排列的水管，中间使用distance来测距

##### 3.2 让水管在x轴负向移动

让水管在X轴移动

##### 3.3 自动生成水管和自动去除水管

可以按照固定的时间生成水管

在水管的X周为负数之后可以去除水管

#### 4. 碰撞检测

将bird和pipes进行碰撞检测

检测为true之后结束游戏

![-w187](http://ossp.pengjunjie.com/mweb/15758803965320.jpg)

####5. 结束页面

![-w186](http://ossp.pengjunjie.com/mweb/15758804300509.jpg)


## 代码优化

## 游戏扩展作业

1. 将游戏的最高积分永久保存下来
2. 游戏结束之后，可以要求输入用户名，并保存排行榜
3. 添加吃豆豆加分模式
4. 设置多种不同的游戏难度，再开始菜单进行选择


##其他扩展游戏

### 下100层
![](http://ossp.pengjunjie.com/mweb/15758805831432.jpg)

### 子弹躲避
![](http://ossp.pengjunjie.com/mweb/15758806249629.jpg)

###飞机大战

![](http://ossp.pengjunjie.com/mweb/15758808375371.jpg)

### 其他游戏