# \[course\]07 游戏模块01-1

## 安装准备

拷贝[game\_graphics](course07-you-xi-mo-kuai-01.md)文件到week5文件夹中。

安装依赖包：

```text
pip install pillow -i https://mirrors.aliyun.com/pypi/simple
pip install pyscreenshot -i https://mirrors.aliyun.com/pypi/simple
pip install requests -i https://mirrors.aliyun.com/pypi/simple
```

[Pillow](https://pillow.readthedocs.io/en/stable/): 用于图像处理的基本的包，包含对图像处理的一些基本的操作 [pyscreenshot](https://pyscreenshot.readthedocs.io/en/latest/): 是一个 Python 的模块，用来对屏幕进行截屏并拷贝到 PIL or Pillow 图像对象中。这是一个纯 Python 库，支持跨平台。 [requests](https://cn.python-requests.org/zh_CN/latest/): Requests 唯一的一个非转基因的 Python HTTP 库，人类可以安全享用。

## EX1 —— 基本操作入门

```python
from game_graphics import *
from tkinter import *

def appStarted(app):
    """
    app启动时设置一个变量
    :param app:
    :return:
    """
    app.counter = 0

def keyPressed(app, event):
    """
    监控键盘操作，每次键盘操作会调用这个方法
    :param app:
    :param event:
    :return:
    """
    app.counter += 1

def redrawAll(app, canvas):
    """
    屏幕会不停的进行重绘
    :param app:
    :param canvas:
    :return:
    """
    canvas.create_text(app.width/2, app.height/2,
                       text=f'{app.counter} keypresses', font='Arial 30 bold')

runApp(width=400, height=400)
```

## MVC

![](http://ossp.pengjunjie.com/mweb/15757031072429.jpg)

MVC是三个单词的首字母缩写，它们是Model（模型）、View（视图）和Controller（控制）。

这个模式认为，程序不论简单或复杂，从结构上看，都可以分成三层。

1. 最上面的一层，是直接面向最终用户的**"视图层"（View）**。它是提供给用户的操作界面，是程序的外壳。用于界面设计人员进行图形界面设计。
2. 最底下的一层，是核心的**"数据层"（Model）**，也就是程序需要操作的数据或信息。程序员编写程序应有的功能（实现算法等等）、数据库专家进行数据管理和数据库设计\(可以实现具体的功能\)。
3. 中间的一层，就是**"控制层"（Controller）**，它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

这三层是紧密联系在一起的，但又是互相独立的，每一层内部的变化不影响其他层。每一层都对外提供接口（Interface），供上面一层调用。这样一来，软件就可以实现模块化，修改外观或者变更数据都不用修改其他层，大大方便了维护和升级。

类似function、class，MVC又是更深一层次的抽象，在我们的程序越来越复杂化之后，我们需要更深入的去对代码进行抽象。MVC涉及到更深一层次的解耦，我们不再是把所有的内容包含在一起，而是逐步的去进行解耦，把程序之间的耦合解开，让我们在编程的时候更清楚的知道不同的内容放在不同的地方，这种编程思维的转化更有利于我们开发更大型的代码。同时在多人合作的项目中，这种模式更加有利于我们在多人间共享开发。

当前game\_graphics的MVC解析，在上面的例子中：

1. `app.counter`就是我们的**模型层**，用来存储键盘按键的次数
2. `redrawAll`方法是我们的**视图层**，用来绘制图形化界面
3. `keyPressed`是我们的**控制层**，用来控制键盘、鼠标、时间和其他的模型

同时，在这个例子中需要注意： 1. 不需要去手动调用`redrawAll`和`keyPressed`，系统会在相应事件触发的时候去自动调用他 2. 不要尝试去用`keyPressed`来调用`redrawAll`。我们在每个层来解决自己的事情，中间使用模型去传递。 3. 不要尝试在`redrawAll`中去修改`app.counter`中的值。同样的我们在视图层只做显示，而不要去做对模型的任何操作。

## EX2

这个样例我们要测试所有的键盘按键返回的具体值是什么，在下面案例之前，我们考虑三个问题： 1. 这个样例的M、V、C三个模型分别是什么？ 2. 如何控制？ 3. 代码结构是什么样的？

```python
# Note: Tkinter uses event.keysym for some keys, and event.char
# for others, and it can be confusing how to use these properly.
# Instead, cmu_112_graphics replaces both of these with event.key,
# which simply works as expected in all cases.

from game_graphics import *
from tkinter import *


def appStarted(app):
    app.message = 'Press any key'


def keyPressed(app, event):
    app.message = f"event.key == '{event.key}'"


def redrawAll(app, canvas):
    canvas.create_text(app.width / 2, 40, text=app.message, font='Arial 30 bold')

    keyNamesText = '''Here are the legal event.key names:
                      * Keyboard key labels (letters, digits, punctuation)
                      * Arrow directions ('Up', 'Down', 'Left', 'Right')
                      * Whitespace ('Space', 'Enter', 'Tab', 'Backspace')
                      * Other commands ('Delete', 'Escape')'''

    y = 80
    for line in keyNamesText.splitlines():
        canvas.create_text(app.width / 2, y, text=line.strip(), font='Arial 20')
        y += 30


runApp(width=600, height=400)
```

## 使用键盘操控移动

### EX3 使用键盘的左右键来移动圆点

```python
from game_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def keyPressed(app, event):
    if (event.key == 'Left'):
        app.cx -= 10
    elif (event.key == 'Right'):
        app.cx += 10

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Move dot with left and right arrows')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

作业： 如何添加上下移动？

### ex4 判断边界，让圆点不移出画面

```python
# This version bounds the dot to remain entirely on the canvas

from game_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def keyPressed(app, event):
    if (event.key == 'Left'):
        app.cx -= 10
        if (app.cx - app.r < 0):
          app.cx = app.r
    elif (event.key == 'Right'):
        app.cx += 10
        if (app.cx + app.r > app.width):
          app.cx = app.width - app.r

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Move dot with left and right arrows')
    canvas.create_text(app.width/2, 40,
                       text='See how it is bounded by the canvas edges')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

### EX5 让圆点从另一侧出现

```python
# This version wraps around, so leaving one side enters the opposite side

from game_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def keyPressed(app, event):
    if (event.key == 'Left'):
        app.cx -= 10
        if (app.cx + app.r <= 0):
          app.cx = app.width + app.r
    elif (event.key == 'Right'):
        app.cx += 10
        if (app.cx - app.r >= app.width):
          app.cx = 0 - app.r

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Move dot with left and right arrows')
    canvas.create_text(app.width/2, 40,
                       text='See how it uses wraparound on the edges')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

### EX6 在x轴和y轴方向移动

```python
# This version moves in both x and y dimensions.

from game_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def keyPressed(app, event):
    if (event.key == 'Left'):    app.cx -= 10
    elif (event.key == 'Right'): app.cx += 10
    elif (event.key == 'Up'):    app.cy -= 10
    elif (event.key == 'Down'):  app.cy += 10

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Move dot with up, down, left, and right arrows')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

作业： 如何类似ex5一样，在整个画板上循环移动

## EX7 跟随鼠标点击移动

```python
from cmu_112_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def mousePressed(app, event):
    app.cx = event.x
    app.cy = event.y

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Move dot with mouse presses')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

作业：如何跟随鼠标移动 \(Tips:使用mouseMoved\)

## EX8 根据时间移动

```python
from game_graphics import *
from tkinter import *

def appStarted(app):
    app.cx = app.width/2
    app.cy = app.height/2
    app.r = 40

def timerFired(app):
    app.cx -= 10
    if (app.cx + app.r <= 0):
        app.cx = app.width + app.r

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='Watch the dot move!')
    canvas.create_oval(app.cx-app.r, app.cy-app.r,
                       app.cx+app.r, app.cy+app.r,
                       fill='darkGreen')

runApp(width=400, height=400)
```

作业： 如何在x=y的斜线上移动

## MVC中不要在view中修改models

```text
from cmu_112_graphics import *
from tkinter import *

def appStarted(app):
    app.x = 0

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='This has an MVC Violation!')

    app.x = 10 # This is an MVC Violation!
               # We cannot change the model from the view (redrawAll)

runApp(width=400, height=400)
```

**同样，不要在view中修改模型，即使是List**

```text
# Since this version modifies a mutable value in the model,
# the exception does not occur immediately on the line of the change,
# but only after redrawAll has entirely finished.

from cmu_112_graphics import *
from tkinter import *

def appStarted(app):
    app.L = [ ]

def redrawAll(app, canvas):
    canvas.create_text(app.width/2, 20,
                       text='This also has an MVC Violation!')

    app.L.append(42) # This is an MVC Violation!
                     # We cannot change the model from the view (redrawAll)

runApp(width=400, height=400)
```

