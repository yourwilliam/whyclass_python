# matplotlib基础教程


## 基本绘图

导入matplotlib包

```py
import matplotlib.pyplot as plt
import numpy as np
```

绘制一个最简单的直线图

```py
# 创建一个包含坐标的plt图
fig, ax = plt.subplots()
# 在数据图中展示数据， 第一个数据代表横坐标，第二个数据代表纵坐标
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])
```

![](http://ossp.pengjunjie.com/markdown-img-paste-20200804122650576.png)

### 图表中的重要说明

![](http://ossp.pengjunjie.com/markdown-img-paste-20200804122915774.png)


#### Axes

Axes对象是具有数据空间的图像区域。给定的图形可以包含许多轴，但给定的Axes对象只能在一个图中。轴包含两个(或在3D情况下为三个)Axis对象。Axes类及其成员函数是使用OO接口的主要入口点。


#### Axis

轴对象，在二维图中我们可以看到这个axes 会包含两个axis，X axis 和 Y axis。

#### Artist

### pandas和numpy的数据导入

```py
a = pd.DataFrame(np.random.rand(4, 5), columns = list('abcde'))
print(a)
a_asarray = a.values
print(a_asarray)
```
