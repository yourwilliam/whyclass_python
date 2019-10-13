# [course]03 —— 画图

后面使用的标准画图插件可以直接参考 [tkinter类库](https://anzeljg.github.io/rin2/book2/2405/docs/tkinter/index.html) 

### 1. **创建一个空的canvas**
    
在draw方法中什么都不写，就可以创建一个空的画板

```py
from tkinter import *

def draw(canvas, width, height):
    pass # replace with your drawing code!

def runDrawing(width=300, height=300):
    root = Tk()
    root.resizable(width=False, height=False) # prevents resizing window
    canvas = Canvas(root, width=width, height=height)
    canvas.configure(bd=0, highlightthickness=0)
    canvas.pack()
    draw(canvas, width, height)
    root.mainloop()
    print("bye!")

runDrawing(400, 200)
```

**Result:**
![](media/15709505190826/graphics-emptyCanvas.png)

### 2. **Canvas坐标系**
 
 canvas的坐标系是从左上角开始计算的，向右记为x轴增加，向下记为y轴增加

![](media/15709505190826/graphics-coords.png)


### 3. **Draw a Line**

画直线，直线使用开始点和结束点来定义。

```py
def draw(canvas, width, height):
    # create_line(x1, y1, x2, y2) draws a line from (x1, y1) to (x2, y2)
    canvas.create_line(25, 50, width/2, height/2)
```

**Result:**
![](media/15709505190826/graphics-line.png)