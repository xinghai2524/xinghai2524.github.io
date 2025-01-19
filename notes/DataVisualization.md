<div class="container">

# Python数据可视化</div>

# 第一章

​	随着大数据时代的到来，各行各业产生的数据呈指数级增长，为了从海量的数据中智能的<sup>**[1]**</sup>获取有价值的信息,数据可视化技术越来越收到人们的关注

## 1.1    数据可视化概述

​	数据可视化有着非常久远的历史，在远古时期，人类的祖先通过画图的方式记录对周围生活环境的认知，随着社会的发展，已经能够灵活的运用柱形图，折线图的展示数据

​	研究表明80%的人能够记得所看到的事物，而只有20%的人能记得所阅读的文字，因此相较于文字类型的数据，人眼对图形的敏感度更高，记忆时间更久

​	数据可视化是借助图形话的手段将一组数据以图形的方式表示，并利用数据分析和开发工具发现其中未知信息的数据处理过程，数据可视化是一个抽象的过程，它将一个不易描述的事物形成一个可感知的过程，即数据从数据空间到图形空间的映射

![无标题-2025-01-05-0645](https://db.xinghai.ink/Typora/1736741213460559.png)

## 1.2    常见的数据可视化方式

通常所说的数据可视化指的是狭义上的数据可视化方式，即将数据以图表的方式进行呈现，而图表是数据可视化最基础的应用，下列介绍常用的图表

**折线图**
折线图是将数据标注成点，并通过直线将这些点按照某种顺序连接而成。它以折线的形式反映事物某个维度的变化趋势，常用于展示时间序列数据的变化

**柱形图**
柱形图使用矩形的长度或高度表示数据大小，通常用于比较不同类别之间的数值大小。柱形图可分为垂直柱形图和水平柱形图

**条形图**
条形图是柱形图的变体，其矩形条通常是水平的，适合在分类标签较长时使用，以便提高可读性

**堆积图**
堆积图是柱形图的一种，表示数据的分布构成。每一列表示总体，各部分堆叠在一起，反映其在总体中的占比

**直方图**
直方图用于展示数据分布的频率，横轴为数据范围（分组），纵轴为频数或频率。它常用于展示连续数据的分布特征

**箱型图**
箱型图（Boxplot）用于显示数据的分布及其离散程度，包括中位数、上下四分位数、最大值、最小值以及异常值等信息

**饼图**
饼图通过将数据分割成扇形区域来表示每个部分占整体的比例，适合表现百分比和比例分布

**散点图**
散点图以二维平面上的点表示数据，横纵坐标分别表示两个变量，常用于观察变量之间的关系或分布趋势

**气泡图**
气泡图是散点图的扩展，每个点不仅表示二维数据，还通过点的大小（气泡的面积）表示第三个变量的值

**误差棒图**
误差棒图在数据点或柱形图上添加误差棒，用于表示数据的不确定性或变化范围，常用于科学研究和实验数据展示

**雷达图**
雷达图（Spider Chart）用于展示多维数据，每个维度以放射状的轴表示，数据点通过多边形连接，适合对比多个对象的综合特性

**统计地图**
统计地图将数据与地理信息结合，利用颜色或图形在地图上展示数据的空间分布或变化趋势

**3D 图表**
3D 图表通过三维展示数据，包括 3D 柱形图、3D 曲面图、3D 散点图等。它提供立体效果，适合展示复杂数据关系，但需注意避免过度复杂导致难以解读

常见的数据的数据可视化库包括 `matplotlib` `seaborn` `ggplot` `pygal` `pyecharts`

尽管python再matplotlib库的基础上封装了很多轻量级的数据可视化库，掌握基础库matplotlib既可以了解数据可视化的底层原理，也可以具备快速学习其他数据可视化库的能力

## 1.3    matplotlib安装

```cmd
pip install matplotlib
```

## 1.4    使用matplotlib绘制图表

**使用面对对象的方式绘制**

```python
from matplotlib import pyplot as plt
import numpy as np

data = np.array([1,2,3,4,5])
fig = plt.figure()
ax = fig.add_subplot(111)
ax.plot(data)
plt.show()
```

- 首先导入了matplotlib中的pyplot模块，然后将模块设置成plt别名，将numpy设置成np为别名
- 创建了包含了五个元素的数组，data
- 然后创建画布对象`fig`
- 在画布中，划分一行一列，然后在第一块区域中绘制坐标轴，相当于画纸`ax = fig.add_subplot(111)`
- 然后在坐标轴中将数组`data`绘制成折线图

**效果**

![image-20250113143242442](https://db.xinghai.ink/Typora/17367499652908306.png)

**使用pyplot函数，快速绘制图表**

```python
from matplotlib import pyplot as plt
import numpy as np

data = np.array([1,2,3,4,5])
plt.plot(data)
plt.show()
```

- 首先导入matplotlib的pyplot模块，并设置为plt别名，导入numpy模块，设置np别名
- 创建包含五个元素的数组data
- 然后使用plt的plot函数直接将data绘制成图表
- 最后用plt.show显示图表

**效果**

![image-20250113143242442](.DataVisualization_file/17367499652908306.png)

在上面的方法中没有创建画布，那图表就会被绘制在默认的画布中，在使用plt.show方法之前所有的plot方法都会被绘制在同一个画布当中，例如

```python
import numpy as np
from matplotlib import pyplot as plt

data = np.array([1,2,3,4,5])
plt.plot(data)

data1 = np.array([1,3,2,4,6])
plt.plot(data1)

plt.show()
```

![image-20250113144638563](https://db.xinghai.ink/Typora/17367508197771184.png)

## 1.5     绘制三角函数

```python
from matplotlib import pyplot as plt
import numpy as np

data = np.linspace(-1 * np.pi,np.pi)

sin = np.sin(data)
cos = np.cos(data)

plt.plot(sin)
plt.plot(cos)

plt.show()
```

![image-20250113145101351](https://db.xinghai.ink/Typora/17367510645843458.png)

- linspace函数会生成两个数之间品均分布的若干个数据组成的数组
- 然后将数组计算得出sin和cos
- 最后使用plot方法绘制图表

# 第二章

目标：掌握matplotlib的绘制函数，并能够绘制简单的图表

## 2.1    绘制折线图

使用`pyplot`的`plot()`函数可以快速的绘制折线图。plot()函数的语法格式如下所示

```python
polot(x, y, scalex=True, scaley=True, data=None, label=None, *args, **kwargs)
```

常用参数如下：

- x:	x表示x轴的数据
- y: 	y表示y轴的数据
- fmt:	表示快速设置线条样式的格式字符串
- label:	表示图列的标签的图例

<h3>示例</h3>

**通过`plot`函数绘制折线图**

```python
import numpy as np
import matplotlib.pyplot as plt

y = np.array([1,2,3,4,5])	# 设置y轴
x = np.array([0.1,0.2,0.3,0.4,0.5])	# 设置x轴
plt.plot(x, y)	# 绘制折线图
plt.show()	# 显示图片
```

![image-20250118122551602](https://db.xinghai.ink/Typora/1737174355812834.png)

**多次调用plot()函数来绘制具有多个线条的折线图**

```python
import matplotlib.pyplot as plt

plt.plot([1,2,3],[4,5,9])
plt.plot([1,2,3],[5,6,8])
plt.show()
```

![image-20250118125019918](https://db.xinghai.ink/Typora/1737175822086033.png)

**调用`plot()`时，通过传入二维数组，绘制多个折线图**

```python
import matplotlib.pyplot as plt

plt.plot([1,2,3,4],[[1, 5, 1, 7],[2, 9, 5, 6],[3, 1, 2, 4],[4, 7, 6, 9]])
plt.show()
```

![image-20250118134045623](https://db.xinghai.ink/Typora/17371790944568663.png)

**通过传入多组数据来绘制多个线条的折线图**

语法

```
matplotlib.pyplot.plot(x1,y1,x2,y2,x3,y3......)
```

示例

```
import matplotlib.pyplot as plt
import numpy as np
data = np.linspace(-1 * np.pi,np.pi)
sin = np.sin(data)
cos = np.cos(data)

plt.plot(data,cos,data,sin)
plt.show()
```

![image-20250118134449283](https://db.xinghai.ink/Typora/17371790919302194.png)

<h3>实例 一</h3>

**未来15天最高气温和最低气温**

|日期|9月4日|9月5日|9月6日|9月7日|9月8日|9月9日|9月10日|9月11日|9月12日|9月13日|9月14日|9月15日|9月16日|9月17日|9月18日|
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|最高气温|32|33|33|34|34|31|30|29|30|29|26|23|21|25|31|
|最低气温|19|19|20|22|22|21|22|16|18|18|17|14|15|16|16|

 根据表中的数据，将`日期`这一行作为x轴，将`最高气温`和`最低气温`两行作为y轴的数据，使用plot()函数绘制反应最高气温和最低气温变化趋势的折线图

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(4,19)

y_max = np.array([32,33,33,34,34,31,30,29,30,29,26,23,21,25,31])
y_min = np.array([19,19,20,22,22,21,22,16,18,18,17,14,15,16,16])
plt.plot(x,y_max,x,y_min)
plt.show()
```

![image-20250118141636488](https://db.xinghai.ink/Typora/17371810436125047.png)

## 2.2    绘制柱形图或堆积柱形图

使用`pyplot`的`bar()`函数可以快速绘制柱形图或堆积柱形图，`bar()`函数的语法如下图所示

```python
bar(x, height, width=0.8, bottom=None, align='center', data=None, tick_label=None, xerr=None, yerr=None, error_kw=None, **kwargs )
```

该函数常用的参数含义如下

- x:	表示柱形图的x坐标值
- height:	表示柱形图的高度,y轴的坐标值
- width:	表示柱形图的宽度
- bottom:	表示柱形图底部y轴坐标的坐标值
- align:	表示柱形的对齐方式，有center和edge两个取值，center表示将柱形与刻度线对其，edge表示将柱形的左边与刻度对其
- tick_label:	表示柱形对应的刻度标签

<h3>示例</h3>

**利用`bar()`函数绘制简单的柱形图**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(5)
y = np.array([10,8,7,11,13])

plt.bar(x,y,tick_label=['a','b','c','d','e'],width=0.3)
```

![image-20250118165631162](https://db.xinghai.ink/Typora/17371905942185874.png)

**使用`bar`绘制有多柱组的柱形图**

其原理就是绘制两次柱形图，而第二次的x会比第一次的大一个宽度的距离

```python
import matplotlib.pyplot as plt
import numpy as np

# 设置x和y1，y2的值
x = np.arange(5)
y1 = np.array([10, 8, 7, 11, 13])
y2 = np.array([9, 6, 5, 10, 12])
bar_width = 0.3

# 绘制柱形图，柱组1和柱组2
plt.bar(x, y1, width=bar_width,tick_label=['a','b','c','d','e'])
plt.bar(x+bar_width, y2, width=bar_width)
# 显示图片
plt.show()
```

![image-20250118171259175](https://db.xinghai.ink/Typora/17371915832610464.png)

**使用`pyplot`的`bar`函数绘制图标时，可以给bottom参数传值的方式，让柱形图绘制在先前图像的的柱形上方**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(5)
y1 = np.array([10, 8, 7, 11, 13])
y2 = np.array([9, 6, 5, 10, 12])
bar_width = 0.3

plt.bar(x,y1,tick_label=['a', 'b', 'c', 'd', 'e'], width=0.3)
plt.bar(x,y2,bottom=y1,width=0.3)
plt.show()
```

![image-20250118172109651](https://db.xinghai.ink/Typora/17371920750424798.png)

**可以通过设置xerr和yerr的方式为图形添加误差棒**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(5)
y1 = np.array([10, 8, 7, 11, 13])
y2 = np.array([9, 6, 5, 10, 12])
bar_width = 0.3

# 设置误差棒
error = [2, 1, 2.5, 2, 1.5]

plt.bar(x,y1,tick_label=['a', 'b', 'c', 'd', 'e'], width=0.3)
plt.bar(x,y2,bottom=y1,width=0.3,yerr=error)
plt.show()
```

![image-20250118174047231](https://db.xinghai.ink/Typora/1737193249520281.png)

<h3>实例 二</h3>

2013-2019财年淘宝和天猫平台的GMV

|  财年   | GMV（亿元） |
| :-----: | :---------: |
| FY2013  |    10770    |
| FY 2014 |    16780    |
| FY 2015 |    24440    |
| FY 2016 |    30920    |
| FY 2017 |    37670    |
| FY 2018 |    48200    |
| FY 2019 |    57270    |

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(7)
y = np.array([10770, 16780, 24440, 30920, 37670, 48200, 57270])

plt.bar(x,y,width=0.3,tick_label=["FY 2013 ", "FY 2014 ", "FY 2015 ",\
                                   "FY 2016 ", "FY 2017 ", "FY 2018 ", "FY 2019 "])
plt.show()
```

![image-20250118180525868](https://db.xinghai.ink/Typora/1737194728018449.png)

## 2.3    绘制条形图或堆积图形

使用`barh()`函数绘制条形图或堆积条形图

函数的语法如下所示

```python
barh(y,width,height=.8,left=None,align='center',*,**kwargs)
```

该函数常用的参数含义如下：

- y:	表示条形的y坐标值
- width:	表示条形的宽度，也就是x坐标值
- height:	表示条形的高度
- left:	条形左侧的x坐标

<h3>示例</h3>

**使用`barh()`绘制条形图**

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.arange(5)
x1 = np.array([10,8,7,11,13])
plt.barh(y,x1,height=0.3,tick_label=['a','b','c','d','e'])
plt.show()
```

![image-20250118203416918](https://db.xinghai.ink/Typora/1737203658837036.png)

**使用pyplot的`barh()`绘制多组条形的条形图**

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.arange(5)
x1 = np.array([10,8,7,11,13])
x2 = np.array([9,6,5,10,12])
plt.barh(y,x1,height=0.3,tick_label=['a','b','c','d','e'])
plt.barh(y+0.3,x2,height=0.3)
plt.show()
```

![image-20250118203625208](https://db.xinghai.ink/Typora/17372037868785605.png)

**使用left参数，在上一个条形的右方绘制新的条形图**

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.arange(5)
x1 = np.array([10,8,7,11,13])
x2 = np.array([9,6,5,10,12])
plt.barh(y,x1,height=0.3,tick_label=['a','b','c','d','e'])
plt.barh(y,x2,height=0.3,left=x1)
plt.show()
```

![image-20250118203809928](https://db.xinghai.ink/Typora/17372038918645954.png)

**使用xerr的方式添加误差棒**

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.arange(5)
x1 = np.array([10,8,7,11,13])
x2 = np.array([9,6,5,10,12])

error = [2, 1, 2.5, 2, 1.5]

plt.barh(y,x1,height=0.3,tick_label=['a','b','c','d','e'])
plt.barh(y,x2,height=0.3,left=x1,xerr=error)
plt.show()
```

![image-20250118204300795](https://db.xinghai.ink/Typora/17372041831924047.png)

<h3>实例 三</h3>

各商品种类的网购替代率

|商品种类|替代率|
|--|--|
|家政、家教、保姆等生活服务|95.9%|
|飞机票、火车票|95.1%|
|家具|93.5%|
|手机、手机配件|92.4%|
|计算机及其配套产品|89.3%|
|汽车用品|89.2%|
|通信充值、游戏充值|86.5%|
|个人护理用品|86.3%|
|书报杂志及音像制品|86.0%|
|餐饮、旅游、住宿|85.6%|
|家用电器|85.4%|
|食品、饮料、烟酒、保健品|83.5%|
|家庭日杂用品|82.6%|
|保险、演出票务|81.6%|
|服装、鞋帽、家用纺织品|79.8%|
|数码产品|76.5%|
|其他商品和服务|76.3%|
|工艺品、收藏品|67.0%|

```

```

<div style="color:#e96900;float:right;"><sub style="background-color:#f8f8f8;font-weight:600;">2025年01月18日</sub></div>

