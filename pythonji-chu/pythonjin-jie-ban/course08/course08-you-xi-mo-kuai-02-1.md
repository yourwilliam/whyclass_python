# \[course]08 游戏模块02-1

这部分游戏主要跟图像和滚动相关，是对图像的一个衍生

## 使用自定义类来创建

和之前的不同，这次使用自定义类来进行创建，通过继承APP来创建。

```python
from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        self.counter = 0

    def keyPressed(self, event):
        self.counter += 1

    def redrawAll(self, canvas):
        canvas.create_text(self.width/2, self.height/2,
                           text=f'{self.counter} keypresses', font='Arial 30 bold')

MyApp(width=400, height=400)
```

## 使用定义的快捷键

绑定模块中自定义的快捷键来进行操作 在game\_graphics中的\_keyPressedWrapper定义了相应的内容

```python
from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        self.counter = 0

    def timerFired(self):
        self.counter += 1

    def redrawAll(self, canvas):
        canvas.create_text(200,  50, text='Keyboard Shortcut Demo')
        canvas.create_text(200, 100, text='Press control-p to pause/unpause')
        canvas.create_text(200, 150, text='Press control-s to save a snapshot')
        canvas.create_text(200, 200, text='Press control-q to quit')
        canvas.create_text(200, 250, text='Press control-x to hard exit')
        canvas.create_text(200, 300, text=f'{self.counter}')

MyApp(width=400, height=400) # quit still runs next one, exit does not
MyApp(width=600, height=600)
```

## 记录数遍跟踪信息

相关键盘和鼠标的事件 keyPressed、keyReleased 键盘的相应操作 mousePressed、mouseReleased 鼠标的点击和释放 mouseMoved 鼠标移动 mouseDragged 鼠标拖动 sizeChanged 窗口大小变换

```python
from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self): 
        self.messages = ['appStarted']

    def appStopped(self):
        self.messages.append('appStopped')
        print('appStopped!')

    def keyPressed(self, event):
        self.messages.append('keyPressed: ' + event.key)

    def keyReleased(self, event):
        self.messages.append('keyReleased: ' + event.key)

    def mousePressed(self, event):
        self.messages.append(f'mousePressed at {(event.x, event.y)}')

    def mouseReleased(self, event):
        self.messages.append(f'mouseReleased at {(event.x, event.y)}')

    def mouseMoved(self, event):
        self.messages.append(f'mouseMoved at {(event.x, event.y)}')

    def mouseDragged(self, event):
        self.messages.append(f'mouseDragged at {(event.x, event.y)}')

    def sizeChanged(self):
        self.messages.append(f'sizeChanged to {(self.width, self.height)}')

    def redrawAll(self, canvas):
        font = 'Arial 20 bold'
        canvas.create_text(self.width/2,  30, text='Events Demo', font=font)
        n = min(10, len(self.messages))
        i0 = len(self.messages)-n
        for i in range(i0, len(self.messages)):
            canvas.create_text(self.width/2, 100+50*(i-i0),
                               text=f'#{i}: {self.messages[i]}',
                               font=font)

MyApp(width=600, height=600)
```

## 控制输入事件

控制输入事件，绑定输入内容

```python
# This demos app.getUserInput(prompt) and app.showMessage(message)

from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        self.message = 'Click the mouse to enter your name!'

    def mousePressed(self, event):
        name = self.getUserInput('What is your name?')
        if (name == None):
            self.message = 'You canceled!'
        else:
            self.showMessage('You entered: ' + name)
            self.message = f'Hi, {name}!'

    def redrawAll(self, canvas):
        font = 'Arial 24 bold'
        canvas.create_text(self.width/2,  self.height/2,
                           text=self.message, font=font)

MyApp(width=500, height=300)
```

## 图片控制

### 输入图片的几种方式

输入图片的几种方式： 1. 直接通过本地图片 2. 通过线上的图片链接 3. 通过跳转图片链接

使用loadImage 来读入图片 使用scaleImage来改变图片的大小

```python
# This demos loadImage and scaleImage from a url

from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        #url = '11.jpg'
        #url = 'http://hbimg.b0.upaiyun.com/341920a3c7ad84de5c8e8945b35c1957b90f81ae31c3e-uxvEFE_fw658'
        url = 'https://www.mtyyw.com/wp-content/uploads/2015/06/Fight-Club.jpg'
        self.image1 = self.loadImage(url)
        self.image2 = self.scaleImage(self.image1, 2/3)

    def redrawAll(self, canvas):
        canvas.create_image(200, 300, image=ImageTk.PhotoImage(self.image1))
        canvas.create_image(500, 300, image=ImageTk.PhotoImage(self.image2))

MyApp(width=700, height=600)
```

### 输出图片的大小

```python
from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        url = '11.jpg'
        self.image1 = self.loadImage(url)
        self.image2 = self.scaleImage(self.image1, 2/3)

    def drawImageWithSizeBelowIt(self, canvas, image, cx, cy):
        canvas.create_image(cx, cy, image=ImageTk.PhotoImage(image))
        imageWidth, imageHeight = image.size
        msg = f'Image size: {imageWidth} x {imageHeight}'
        canvas.create_text(cx, cy + imageHeight/2 + 20,
                           text=msg, font='Arial 20 bold')

    def redrawAll(self, canvas):
        self.drawImageWithSizeBelowIt(canvas, self.image1, 200, 300)
        self.drawImageWithSizeBelowIt(canvas, self.image2, 500, 300)

MyApp(width=700, height=600)
```

## 图片转换

transpose : Transpose image (flip or rotate in 90 degree steps)

```python
def transpose(self, method):
"""
Transpose image (flip or rotate in 90 degree steps)

:param method: One of :py:attr:`PIL.Image.FLIP_LEFT_RIGHT`,
  :py:attr:`PIL.Image.FLIP_TOP_BOTTOM`, :py:attr:`PIL.Image.ROTATE_90`,
  :py:attr:`PIL.Image.ROTATE_180`, :py:attr:`PIL.Image.ROTATE_270`,
  :py:attr:`PIL.Image.TRANSPOSE` or :py:attr:`PIL.Image.TRANSVERSE`.
:returns: Returns a flipped or rotated copy of this image.
"""
```

```python
# This demos using transpose to flip an image

from game_graphics import *
from tkinter import *
from PIL import Image  # <-- need to do this after tkinter import

class MyApp(App):
    def appStarted(self):
        url = '11.jpg'
        self.image1 = self.loadImage(url)
        self.image2 = self.image1.transpose(Image.FLIP_LEFT_RIGHT)

    def redrawAll(self, canvas):
        canvas.create_image(200, 300, image=ImageTk.PhotoImage(self.image1))
        canvas.create_image(500, 300, image=ImageTk.PhotoImage(self.image2))

MyApp(width=700, height=600)
```

## 截屏和保存图片

```python
from game_graphics import *
from tkinter import *

class MyApp(App):
    def appStarted(self):
        self.image = None

    def keyPressed(self, event):
        if (event.key == 'g'):
            snapshotImage = self.getSnapshot()
            self.image = self.scaleImage(snapshotImage, 0.4)
        elif (event.key == 's'):
            self.saveSnapshot()

    def redrawAll(self, canvas):
        canvas.create_text(350, 20, text='Press g to getSnapshot')
        canvas.create_text(350, 40, text='Press s to saveSnapshot')
        canvas.create_rectangle(50, 100, 250, 500, fill='cyan')
        if (self.image != None):
            canvas.create_image(525, 300, image=ImageTk.PhotoImage(self.image))

MyApp(width=700, height=600)
```

## Spritesheets 雪碧图

雪碧图用于游戏中的角色运动。

```python
# This demos sprites using Pillow/PIL images
# See here for more details:
# https://pillow.readthedocs.io/en/stable/reference/Image.html

# This uses a spritestrip from this tutorial:
# https://www.codeandweb.com/texturepacker/tutorials/how-to-create-a-sprite-sheet

from game_graphics import *
from tkinter import *


class MyApp(App):
    def appStarted(self):
        url = 'black_bird.jpg'
        spritestrip = self.loadImage(url)
        self.sprites = []
        first_shift_x = 40
        first_shift_y = 100
        for i in range(8):
            sprite = spritestrip.crop(
                (0 + 115 * i + first_shift_x, first_shift_y, 115 + 115 * i + first_shift_x, first_shift_y + 130))
            self.sprites.append(sprite)
        self.spriteCounter = 0

    def timerFired(self):
        self.spriteCounter = (1 + self.spriteCounter) % len(self.sprites)

    def redrawAll(self, canvas):
        sprite = self.sprites[self.spriteCounter]
        canvas.create_image(200, 200, image=ImageTk.PhotoImage(sprite))


MyApp(width=400, height=400)
```

作业： 制作自己的雪碧图人物，可以在网上随便的搜索相应的图片模板
