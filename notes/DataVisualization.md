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

![image-20250113143242442](https://db.xinghai.ink/Typora/17374505608254879.png)

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

```python
import matplotlib.pyplot as plt
import numpy as np


plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False  # 处理负号显示问题
labels = [" 家政、家教、保姆等生活服务", " 飞机票、火车票", " 家具", " 手机、手机配件",\
          " 计算机及其配套产品", " 汽车用品", " 通信充值、游戏充值", " 个人护理用品",\
          " 书报杂志及音像制品", " 餐饮、旅游、住宿", " 家用电器", " 食品、饮料、烟酒、保健品", \
          " 家庭日杂用品", " 保险、演出票务", " 服装、鞋帽、家用纺织品", " 数码产品", \
          " 其他商品和服务", " 工艺品、收藏品"]

x = np.array([0.959, 0.951, 0.935, 0.924, 0.893, 0.892, 0.865, 0.863, 0.86 ,\
       0.856, 0.854, 0.835, 0.826, 0.816, 0.798, 0.765, 0.763, 0.67 ])
y = np.arange(18)


plt.barh(y,x,height=0.6,tick_label=labels)
plt.show()
```

![image-20250119124613268](https://db.xinghai.ink/Typora/17372619755405967.png)

## 2.4    绘制堆积面积图

使用`pyplot`的`stackplot()`函数可以快速绘制堆积面积图，`stackplot()`函数的句法格式如下

```python
stackplot(x, y, labels=(), baseline='zero', data=None, *args, **kwargs)
```

该函数常用的参数含义如下

- x	表示x轴的数据，可以是一维数组
- y	表示y轴的数据，可以是二维数组或一维数组序列
- labels	表示每组折现及填充区域的标签
- baseline	表示计算基线的方式，包括zero，sym wiggle

<h3>示例</h3>

使用`stackplot()`函数绘制由三条折现及下方填充区域堆叠的堆积面积图

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(6)
y1 = np.array([1, 4, 3, 5, 6, 7])
y2 = np.array([1, 3, 4, 2, 7, 6])
y3 = np.array([3, 4, 3, 6, 5, 5])

# 下面两个都可以
plt.stackplot(x,y1,y2,y3)
# plt.stackplot(x,[y1,y2,y3])

plt.show()
```

![image-20250119125916323](https://db.xinghai.ink/Typora/17372627580364785.png)

<h3>实例 四</h3>

**物流公司物流费用统计**

|月份|A公司| B公司| C公司|
|----|----|----|----|
|1|198|203|185|
|2|215|203|205|
|3|245|236|226|
|4|222|236|199|
|5|200|269|238|
|6|236|216|200|
|7|201|298|250|
|8|253|333|209|
|9|236|301|246|
|10|200|349|219|
|11|266|360|253|
|12|290|368|288|

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(1,13)
y_a = np.array([198, 215, 245, 222, 200, 236, 201, 253, 236, 200, 266, 290])
y_b = np.array([203, 203, 236, 236, 269, 216, 298, 333, 301, 349, 360, 368])
y_c = np.array([185, 205, 226, 199, 238, 200, 250, 209, 246, 219, 253, 288])

plt.stackplot(x,y_a,y_b,y_c)
plt.show()
```

![image-20250119133044456](https://db.xinghai.ink/Typora/1737264647415256.png)

## 2.5    绘制直方图

使用`pyplot`的`hist()`函数可以绘制直方图，`hist()`函数的语法格式如下

```python
def hist(
    x: ArrayLike | Sequence[ArrayLike],
    bins: int | Sequence[float] | str | None = None,
    range: tuple[float, float] | None = None,
    density: bool = False,
    weights: ArrayLike | None = None,
    cumulative: bool | float = False,
    bottom: ArrayLike | float | None = None,
    histtype: Literal["bar", "barstacked", "step", "stepfilled"] = "bar",
    align: Literal["left", "mid", "right"] = "mid",
    orientation: Literal["vertical", "horizontal"] = "vertical",
    rwidth: float | None = None,
    log: bool = False,
    color: ColorType | Sequence[ColorType] | None = None,
    label: str | Sequence[str] | None = None,
    stacked: bool = False,
    *,
    data=None,
    **kwargs,
)
```

该函数常用的参数含义如下

- x	表示x轴的数据
- bins	表示矩形条的个数，默认为10
- range	表示数据的范围
- cumulative	表示是否计算累计频数或频率
- histtype	表示直方图的类型，
- align	表示矩形条边界的对其方式

<h3>示例</h3>

绘制一个具有8个矩形条填充的线条直方图

```python
import matplotlib.pyplot as plt
import numpy as np
scores = np.random.randint(0,100,50)

plt.hist(scores,bins=8,histtype='stepfilled')
plt.show()
```

![image-20250119145431755](https://db.xinghai.ink/Typora/17372696738160198.png)

<h3>实例 五</h3>

人脸识别的灰度直方图

```python
import matplotlib.pyplot as plt
import numpy as np

random_state = np.random.RandomState(19680801)
random_x = random_state.randn(1000)

plt.hist(random_x,bins=25)
plt.show()
```

![image-20250119145922404](https://db.xinghai.ink/Typora/17372699647649877.png)

## 2.6    绘制 饼图或圆环图

使用`pie()`函数绘制饼图或者圆环图，该函数语法如下

```python
pie(
    x: ArrayLike,
    explode: ArrayLike | None = None,
    labels: Sequence[str] | None = None,
    colors: ColorType | Sequence[ColorType] | None = None,
    autopct: str | Callable[[float], str] | None = None,
    pctdistance: float = 0.6,
    shadow: bool = False,
    labeldistance: float | None = 1.1,
    startangle: float = 0,
    radius: float = 1,
    counterclock: bool = True,
    wedgeprops: dict[str, Any] | None = None,
    textprops: dict[str, Any] | None = None,
    center: tuple[float, float] = (0, 0),
    frame: bool = False,
    rotatelabels: bool = False,
    *,
    normalize: bool = True,
    hatch: str | Sequence[str] | None = None,
    data=None,
)
```

<h3>示例</h3>

**使用`pie()`函数绘制简单的饼图**

> - x	表示数据
> - labels	表示数据对应的标签和文本
> - autopct	表示控制图形显示的数值字符串，可以通过格式指定显示小数点后几位
> - radius	表示半径，半径越大，图像越大

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.array([20,50,10,15,30,55])
label = np.array(['A','B','C','D','E','F'])

plt.pie(data,labels=label,autopct='%.2f%%',radius=1.5)
plt.show()
```

![image-20250119152832217](https://db.xinghai.ink/Typora/17372717141331823.png)

**使用`pie()`函数绘制圆环图**

> - pctdistance		用来控制数值距离圆心的距离默认是0.6
> - wedgeprops	用来设置属性，例如width可以控制楔形的宽度

```python
import numpy as np
import matplotlib.pyplot as plt

data = np.array([20,50,10,15,30,55])
label = np.array(['A','B','C','D','E','F'])

plt.pie(data,labels=label,autopct='%.2f%%',radius=1.5,pctdistance=0.8,wedgeprops={'width':0.65})
plt.show()
```

![image-20250119154612415](https://db.xinghai.ink/Typora/1737272774477938.png)



**`shoadow`表示是否绘制阴影，`frame`表示是否绘制图框**

![image-20250119160939872](https://db.xinghai.ink/Typora/1737274181774736.png)

<h3>实例 六</h3>

支付宝月账单报告

|分类|金额（元）|
|--|--|
|购物|800|
|人情往来|100|
|餐饮美食|1000|
|通信物流|200|
|生活日用|300|
|交通出行|200|
|休闲娱乐|200|
|其他|200|
|总支出|3000|

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.sans-serif'] = ['SimHei']

data = np.array([800 ,100 ,1000,200 ,300 ,200 ,200 ,200 ])
data = data / 3000
labels = np.array(["购物", "人情往来", "餐饮美食", "通信物流", "生活日用", "交通出行", "休闲娱乐", "其他"])

plt.pie(data,autopct='%.2f%%',shadow=True,explode=[0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1],startangle=90,labels=labels)
plt.show()
```

![image-20250119162303670](https://db.xinghai.ink/Typora/17372765961017027.png)

## 2.7    绘制散点图或气泡图

使用`scatter()`函数可以绘制散点图或气泡图,基本语法如下

```python
scatter(
    x: float | ArrayLike,
    y: float | ArrayLike,
    s: float | ArrayLike | None = None,
    c: ArrayLike | Sequence[ColorType] | ColorType | None = None,
    marker: MarkerType | None = None,
    cmap: str | Colormap | None = None,
    norm: str | Normalize | None = None,
    vmin: float | None = None,
    vmax: float | None = None,
    alpha: float | None = None,
    linewidths: float | Sequence[float] | None = None,
    *,
    edgecolors: Literal["face", "none"] | ColorType | Sequence[ColorType] | None = None,
    plotnonfinite: bool = False,
    data=None,
    **kwargs,
)
```

- x,y	表示数据点的位置
- s	表示数据点的大小
- c	表示数据点的颜色
- marker	表示数据点的形状，默认为圆形
- cmap	表示数据点颜色的映射表，仅当c为浮点数时生效
- norm	表示数据亮度，取值为0~1
- alpha	表示透明度

<h3>示例</h3>

**使用`scatter()`绘制一个散点图**

```python
import matplotlib.pyplot as plt
import numpy as np

num = 50
x = np.random.rand(num)
y = np.random.rand(num)

plt.scatter(x,y)
plt.show()
```

![image-20250119170518797](https://db.xinghai.ink/Typora/17372775210338879.png)

**通过设置`s`参数控制点大小绘制气泡图**

```python
import matplotlib.pyplot as plt
import numpy as np

num = 50
x = np.random.rand(num)
y = np.random.rand(num)

plt.scatter(x,y,s=(np.random.rand(num) * 30)**2,alpha=0.5)
plt.show()
```

![](https://db.xinghai.ink/Typora/1737277601072146.png)



<h3>实例 七</h3>

车速与制动距离的关系

|车速（km/h）|制动距离（m）|车速（km/h）|制动距离（m）|
|----|----|----|----|
|10|0.5|110|59.5|
|20|2.0|120|70.8|
|30|4.4|130|83.1|
|40|7.9|140|96.4|
|50|12.3|150|110.7|
|60|17.7|160|126.0|
|70|24.1|170|142.2|
|80|31.5|180|159.4|
|90|39.9|190|177.6|
|100|49.2|200|196.8|

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(10,210,10)
y = np.array([0.5  , 2.0  , 4.4  , 7.9  , 12.3 , 17.7 , 24.1 , 31.5 , 39.9 , 49.2 , 59.5 , 70.8 , 83.1 , 96.4 , 110.7, 126.0, 142.2, 159.4, 177.6, 196.8])

plt.scatter(x,y,s=50,alpha=0.5)
plt.show()
```

![image-20250119172430981](https://db.xinghai.ink/Typora/1737278672871719.png)

## 2.8    绘制箱型图

使用`boxplot()`绘制箱型图，构造函数如下

```python
boxplot(
    x: ArrayLike | Sequence[ArrayLike],
    notch: bool | None = None,
    sym: str | None = None,
    vert: bool | None = None,
    whis: float | tuple[float, float] | None = None,
    positions: ArrayLike | None = None,
    widths: float | ArrayLike | None = None,
    patch_artist: bool | None = None,
    bootstrap: int | None = None,
    usermedians: ArrayLike | None = None,
    conf_intervals: ArrayLike | None = None,
    meanline: bool | None = None,
    showmeans: bool | None = None,
    showcaps: bool | None = None,
    showbox: bool | None = None,
    showfliers: bool | None = None,
    boxprops: dict[str, Any] | None = None,
    tick_labels: Sequence[str] | None = None,
    flierprops: dict[str, Any] | None = None,
    medianprops: dict[str, Any] | None = None,
    meanprops: dict[str, Any] | None = None,
    capprops: dict[str, Any] | None = None,
    whiskerprops: dict[str, Any] | None = None,
    manage_ticks: bool = True,
    autorange: bool = False,
    zorder: float | None = None,
    capwidths: float | ArrayLike | None = None,
    label: Sequence[str] | None = None,
    *,
    data=None,
)
```



**使用`boxplot()`函数绘制一个箱型图**

> - x	绘制箱型图的数据
> - menline	是否用横跨箱体的先条标出中位数
> - patch_artist	是否填充箱体的颜色
> - showfliers	是否显示异常值
> - widths	表示箱体的宽度

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.randn(100)
plt.boxplot(data,meanline=True,widths=0.3,patch_artist=True,showfliers=False)
plt.show()
```

![image-20250120230127690](https://db.xinghai.ink/Typora/17373852911877167.png)

<h3>实例 八</h3>

2017年和2018年全国发电量统计

| 月份 | 2018年发电量（亿千瓦·时） | 月份 | 发电量（亿千瓦·时） |
| ---- | ------------------------- | ---- | ------------------- |
| 1月  | 5200                      | 1月  | 4605.2              |
| 2月  | 5254.5                    | 2月  | 4710.3              |
| 3月  | 5283.4                    | 3月  | 4767.2              |
| 4月  | 5107.8                    | 4月  | 4947                |
| 5月  | 5443.3                    | 5月  | 5203                |
| 6月  | 5550.6                    | 6月  | 6047.4              |
| 7月  | 6400.2                    | 7月  | 6047.4              |
| 8月  | 6404.9                    | 8月  | 5945.5              |
| 9月  | 5483.1                    | 9月  | 5219.6              |
| 10月 | 5330.2                    | 10月 | 5038.1              |
| 11月 | 5543                      | 11月 | 5196.3              |
| 12月 | 6199.9                    | 12月 | 5698.6              |

> vert	表示是否将箱型图垂直摆放，默认为True

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
data_18 = np.array([5200  ,5254.5,5283.4,5107.8,5443.3,5550.6,6400.2,6404.9,5483.1,5330.2,5543  ,6199.9])
data_17 = np.array([4605.2,4710.3,4767.2,4947  ,5203  ,6047.4,6047.4,5945.5,5219.6,5038.1,5196.3,5698.6])

# 绘制箱型图
plt.boxplot([data_18,data_17],tick_labels=('2018年','2017年'),meanline=True,widths=0.5,vert=False,patch_artist=True)
plt.show()
```

![image-20250120234859367](https://db.xinghai.ink/Typora/1737388141344926.png)

## 2.9    绘制雷达图

使用`pyplot`的`polar()`函数可以快速绘制雷达图

```python
polar(theta, r, **kwargs)
```

> theta	表示每个数据点所在的射线与极径的夹角
>
> r	表示每个数据点到原点的距离



| 用户 | 研究型（I） | 艺术型（A） | 社会型（S） | 企业型（E） | 传统型（C） | 现实型（R） |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 用户1 | 0.40 | 0.32 | 0.35 | 0.30 | 0.30 | 0.88 |
| 用户2 | 0.85 | 0.35 | 0.30 | 0.40 | 0.40 | 0.30 |
| 用户3 | 0.43 | 0.89 | 0.30 | 0.28 | 0.22 | 0.30 |
| 用户4 | 0.30 | 0.25 | 0.48 | 0.85 | 0.45 | 0.40 |
| 用户5 | 0.20 | 0.38 | 0.87 | 0.45 | 0.32 | 0.28 |
| 用户6 | 0.34 | 0.31 | 0.38 | 0.40 | 0.92 | 0.28 |

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
data = np.array([[0.40, 0.32, 0.35, 0.30, 0.30, 0.88],
[0.85, 0.35, 0.30, 0.40, 0.40, 0.30],
[0.43, 0.89, 0.30, 0.28, 0.22, 0.30],
[0.30, 0.25, 0.48, 0.85, 0.45, 0.40],
[0.20, 0.38, 0.87, 0.45, 0.32, 0.28],
[0.34, 0.31, 0.38, 0.40, 0.92, 0.28]])

# 计算出圆的平分6份的各个角度
angles = np.linspace(0,2 * np.pi, 6, endpoint=False)
# 在末尾添加一位和首位相同的数
angles = np.concatenate((angles,[angles[0]])) 
data = np.concatenate((data,[data[0]]))

rradar_labels = ['研究型','艺术型','社会型','企业型','传统型','现实型','研究型']

plt.polar(angles,data)
plt.fill(angles,data,alpha=0.25)
plt.thetagrids(angles * 180/np.pi,labels=rradar_labels)
plt.show()
```

![image-20250121130203582](https://db.xinghai.ink/Typora/17374357269873056.png)



## 2.10    绘制误差棒

**使用`errorbar()`绘制误差棒**

```python
errorbar(
    x: float | ArrayLike,
    y: float | ArrayLike,
    yerr: float | ArrayLike | None = None,
    xerr: float | ArrayLike | None = None,
    fmt: str = "",
    ecolor: ColorType | None = None,
    elinewidth: float | None = None,
    capsize: float | None = None,
    barsabove: bool = False,
    lolims: bool | ArrayLike = False,
    uplims: bool | ArrayLike = False,
    xlolims: bool | ArrayLike = False,
    xuplims: bool | ArrayLike = False,
    errorevery: int | tuple[int, int] = 1,
    capthick: float | None = None,
    *,
    data=None,
    **kwargs,
)
```

该函数常用的参数含义如下

- x，y	表示数据点位置
- xerr，yerr	表示数据点的误差
- fmt	表示数据点的标记样式
- ecolor	表示误差棒的颜色
- elinewidth	表示误差棒的宽度]
- capsize	误差帮横跨栏的长度
- capthick	误差棒横跨栏的厚度

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(5)
y = (25, 32, .4, 20, 25)
y_offset = (3, 5, 2, 3, 3)

plt.errorbar(x,y,yerr=y_offset,capsize=3,capthick=2)
plt.show()
```

![image-20250121131931482](https://db.xinghai.ink/Typora/17374367733609188.png)

<h3>实例 十</h3>

4个树种不同季节的细根生物量

|季节|马尾松|樟树|杉木|桂花|
|--|--|--|--|--|
|春季|2.04±0.16|1.69±0.27|4.65±0.34|3.39±0.23|
|夏季|1.57±0.08|1.61±0.14|4.99±0.32|2.33±0.23|
|秋季|1.63±0.10|1.64±0.14|4.94±0.29|4.10±0.39|

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(3)

y1 = np.array([2.04,1.57,1.63])
y2 = np.array([1.69,1.61,1.64])
y3 = np.array([4.65,4.99,4.94])
y4 = np.array([3.39,2.33,4.10])

plt.rcParams['font.family'] = ['SimHei']

error1 = [0.16,0.08,0.10]
error2 = [0.27,0.14,0.14]
error3 = [0.34,0.32,0.29]
error4 = [0.23,0.23,0.39]

plt.bar(x,y1,width=0.2)
plt.bar(x + 0.2,y2,width=0.2,tick_label=['春季','夏季','秋季'])
plt.bar(x + 0.4,y3,width=0.2)
plt.bar(x + 0.6,y4,width=0.2)

plt.errorbar(x,y1,yerr=error1,capsize=3,elinewidth=2,fmt='k,')
plt.errorbar(x + 0.2,y2,yerr=error2,capsize=3,elinewidth=2,fmt='k,')
plt.errorbar(x + 0.4,y3,yerr=error3,capsize=3,elinewidth=2,fmt='k,')
plt.errorbar(x + 0.6,y4,yerr=error4,capsize=3,elinewidth=2,fmt='k,')

plt.show()
```

![image-20250121170817063](https://db.xinghai.ink/Typora/17374505003753402.png)

## 2.11   习题

高二男生、女生各科的平均成绩

| 学科 | 平均成绩（男） | 平均成绩（女） |
| ---- | -------------- | -------------- |
| 语文 | 85.5           | 94             |
| 数学 | 91             | 82             |
| 英语 | 72             | 89.5           |
| 物理 | 59             | 62             |
| 化学 | 66             | 49             |
| 生物 | 55             | 53             |

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']

x = np.arange(6)
y1 = np.array([85.5,91,72,59,66,55])
y2 = np.array([94,82,89.5,62,49,53])

label = ['语文','数学','英语','物理','化学','生物']

plt.bar(x,y1,width=0.3,tick_label=label)
plt.bar(x+0.3,y2,width=0.3)
plt.show()
```

![image-20250121173654354](https://db.xinghai.ink/Typora/1737452216222738.png)

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']

x = np.arange(6)
y1 = np.array([85.5,91,72,59,66,55])
y2 = np.array([94,82,89.5,62,49,53])

label = ['语文','数学','英语','物理','化学','生物']

plt.bar(x,y1,width=0.3,tick_label=label)
plt.bar(x,y2,bottom=y1,width=0.3)
plt.show()
```

![image-20250121173738065](https://db.xinghai.ink/Typora/17374522620839047.png)

|子类目|销售额（亿元）|
|--|--|
|童装|29665|
|奶粉辅食|3135.4|
|孕妈专区|4292.4|
|洗护喂养|5240.9|
|宝宝尿裤|5543.4|
|春夏新品|5633.8|
|童车童床|6414.5|
|玩具文娱|9308.1|
|童鞋|10353|

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.array([29665 , 3135.4, 4292.4, 5240.9, 5543.4, 5633.8, 6414.5, 9308.1, 10353])
plt.pie(y,radius=1.3,autopct='%.2f%%',pctdistance=0.8,explode=[0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1])
plt.show()
```

![image-20250121174551124](https://db.xinghai.ink/Typora/17374527529996457.png)

<div style="color:#e96900;float:right;"><sub style="background-color:#f8f8f8;font-weight:600;">2025年01月18日</sub></div>

