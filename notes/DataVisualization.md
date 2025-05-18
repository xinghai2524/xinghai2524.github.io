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
data_17 = np.array([4605.2,4710.3,5168.9,4767.2  ,4947  ,5203,6047.4,5945.5,5219.6,5038.1,5196.3,5698.6])

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

# 第三章

## 3.1    认识图表常用的辅助元素

图表的`辅助元素`是指`除根据数据绘制的图形之外的元素`,常用的辅助元素包括`坐标轴`、`标题`、`图例`、`网格`、`参考线`、`参考区域`、`注释文本`和`表格`

![image-20250122193427563](https://db.xinghai.ink/Typora/17375456770663512.png)

## 3.2    设置坐标轴的标签、刻度线和刻度标签

`matplotlib`提供了设置x轴和y轴标签的方式

**在`matplotlib`中，使用`pyplot`模块的`xlabel()`函数设置x轴的标签**

`xlabel()`构造函数如下

```python
def xlabel(
    xlabel: str,
    fontdict: dict[str, Any] | None = None,
    labelpad: float | None = None,
    *,
    loc: Literal["left", "center", "right"] | None = None,
    **kwargs,
)
```

- xlabel	表示x轴的标签文本 
- fontdict	表示控制标签文本的样式的字典
- labelpad	表示标签与坐标轴边框的距离

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']

x = np.arange(1,6)
y = np.random.randint(1,10,5)

plt.plot(x,y)
plt.xlabel("x轴",labelpad=6)
plt.show()
```

![image-20250123134111038](.DataVisualization_file/image-20250123134111038.png)

**使用`pyplot`的`ylabel()`函数设置y轴的标签**

构造函数如下

```python
def ylabel(
    ylabel: str,
    fontdict: dict[str, Any] | None = None,
    labelpad: float | None = None,
    *,
    loc: Literal["bottom", "center", "top"] | None = None,
    **kwargs,

```

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']

x = np.arange(1,6)
y = np.random.randint(1,10,5)

plt.plot(x,y)
plt.ylabel("y轴",labelpad=6)
plt.show()
```

![image-20250123134326988](https://db.xinghai.ink/Typora/1737611009629191.png)

**使用`pyplot`模块的`xlim()`和`ylim()`函数分别可以设置x轴和y轴的刻度范围**

通常来说，刻度范围是根据图表大小自动设置的，但是可以使用`xlim`手动设置刻度范围,构造函数如下

```python
xlim(left=None, right=None, *, emit=True, auto=False,
                 xmin=None, xmax=None)
```

- left	表示x轴刻度取值区间的左位数
- right	表示x轴刻度取值区间的右位数

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['sans-serif']
x = np.linspace(-1 *np.pi,np.pi)
ysin = np.sin(x)
ycos = np.cos(x)

plt.plot(x,ysin)
plt.show()

plt.plot(x,ysin)
plt.xlim(x.min() * 2,x.max() * 2)
plt.show()
```

![image-20250123200629201](https://db.xinghai.ink/Typora/17376339924326658.png)

![image-20250123200635568](https://db.xinghai.ink/Typora/17376339972583244.png)

**使用`pyplot`模块的`xticks()`和`yticks()`函数设置刻度标签**

构造函数如下

`xlime`是设置刻度的范围，那么`zticks`就是设置具体的x刻度值

```python
def xticks(
    ticks: ArrayLike | None = None,
    labels: Sequence[str] | None = None,
    *,
    minor: bool = False,
    **kwargs
)
```

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.arange(5)

plt.plot(data)

plt.xticks([0,1,2,3,4,4.3,4.7,5])
plt.show()
```

![image-20250127123551392](https://db.xinghai.ink/Typora/17379525549071593.png)

**设置刻度范围和刻度标签**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi,np.pi)
ysin = np.sin(x)
ycos = np.cos(x)

plt.plot(x,ysin)
plt.plot(x,ycos)

plt.xlim(x.min() * 1.5 ,x.max() * 1.5)
plt.xticks([-np.pi,-np.pi/2,0,np.pi / 2,np.pi],[r'$-\pi$',r'$-\pi/2$','$0$',r'$\pi/2$','$\pi$'])

plt.show()
```

![image-20250127133537828](https://db.xinghai.ink/Typora/17379561394687648.png)

<h3>实例 一</h3>

2019中国电影票房排行榜 Top15

|电影名称|总票房（亿元）|电影名称|总票房（亿元）|
| ---- | ---- | ---- | ---- |
|哪吒之魔童降世|48.57|飞驰人生|17.03|
|流浪地球|46.18|烈火英雄|16.70|
|复仇者联盟4：终局之战|42.05|蜘蛛侠：英雄远征|14.01|
|疯狂的外星人|21.83|速度与激情：特别行动|13.84|
|扫毒2：天地对决|12.85|哥斯拉2：怪兽之王|9.27|
|大黄蜂|11.38|阿丽塔：战斗天使|8.88|
|惊奇队长|10.25|银河补习班|8.64|
|比悲伤更悲伤的故事|9.46| | |

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = 'SimHei'
data = np.array([48.57, 46.18, 42.05, 21.83, 17.03, 16.70, 14.01, 13.84, 12.85, 11.38, 10.25, 9.46, 9.27, 8.88, 8.64])
labels = np.array(["哪吒之魔童降世", "流浪地球", "复仇者联盟4：终局之战", "疯狂的外星人", "飞驰人生",
                   "烈火英雄", "蜘蛛侠：英雄远征", "速度与激情：特别行动", "扫毒2：天地对决", "大黄蜂",
                   "惊奇队长", "比悲伤更悲伤的故事", "哥斯拉2：怪兽之王", "阿丽塔：战斗天使", "银河补习班"])

y_data = np.arange(len(data))

plt.barh(y_data,data,height=0.2,color='orange')
plt.yticks(y_data,labels)
plt.xlabel('总票房（亿元）')
plt.ylabel('电影名称')
plt.show()
```

![image-20250127141610248](https://db.xinghai.ink/Typora/17379585723511775.png)

## 3.3    添加图例和标签

使用`pyplot`模块的`title`可以给图表添加标签

```python
title(label,fontdict=None,loc='center',pad=None,**kwargs)
```

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np
plt.rcParams['font.family'] = 'SimHei'
plt.plot(np.arange(5))
plt.title('标签')
plt.show()
```

![image-20250127200903918](https://db.xinghai.ink/Typora/17379797467878153.png)

**使用`pyplot`模块的`legend()`函数可以给图表添加图例**

```
legend(handles,labels,loc,bbox_to_anchor,ncol,title,shadow,fancybox,*args,**kwargs)
```

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np
plt.rcParams['font.family'] = 'SimHei'
plt.plot(np.arange(5))
plt.plot([1,5,2,4,6])
plt.title('标签')
plt.legend(['线条一','线条二'],loc='upper center')
plt.show()
```

![image-20250127213915515](https://db.xinghai.ink/Typora/1737985157485802.png)

<h3>实例 二</h3>

支付宝月账单报告

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.sans-serif'] = ['SimHei']

data = np.array([800 ,100 ,1000,200 ,300 ,200 ,200 ,200 ])
data = data / 3000
labels = np.array(["购物", "人情往来", "餐饮美食", "通信物流", "生活日用", "交通出行", "休闲娱乐", "其他"])

plt.pie(data,autopct='%.2f%%',shadow=True,explode=[0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1],startangle=90,labels=labels)
plt.legend(labels,loc='upper right',bbox_to_anchor=[1.5,1.1])
plt.show()
```

![image-20250127214417102](https://db.xinghai.ink/Typora/17379854587376997.png)

## 3.4    显示网格

**使用`pyplot`模块的`grid()`函数显示网格**

```python
grid(b=None,which='major', axis='both,**kwargs')
```

- b	表示是否显示网格
- which	表示显示网格的类型，支持`major`、`minor`、`both`
- axis	表示显示哪个方向的网格支持`both`、`x`、`y`
- lw	表示网格的宽度

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))

plt.grid(axis='y',linewidth=0.3)

plt.show()
```

![image-20250128131642235](https://db.xinghai.ink/Typora/17380414052812538.png)

<h3>实例 三</h3>

汽车速度与制动距离的关系

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = 'SimHei'
x_speed = np.arange(10,210,10)
y_distance = np.array([
    0.5, 2.0, 4.4, 7.9, 12.3,
    17.7, 24.1, 31.5, 39.9, 49.2,
    59.5, 70.8, 83.1, 96.4, 110.7,
    126.0, 142.2, 159.4, 177.6, 196.8
])
plt.scatter(x_speed,y_distance,s=50,alpha=0.5, linewidths=0.3)
plt.xlabel('速度(km/h)')
plt.ylabel('制动距离(m)')
plt.grid(linewidth=0.3)
```

![image-20250128132831337](https://db.xinghai.ink/Typora/17380421130657723.png)

## 3.5    添加参考线和参考区域

使用axhline()函数添加水平参考线

```python
axhline(y=0,xmin=0,xmax=1linestyle='-',**kwargs)
```

该函数常用的参数含义如下

- y	表示水平参考线的纵坐标
- xmin	表示参考线的起始位置
- ymax	表示水平参考线的结束位置
- linestyle	表示水平参考线的类型

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))

plt.grid(axis='y',linewidth=0.3)
plt.axvline(x=0,ymax=0.9,ymin=0.1,linestyle='--')
plt.axhline(y=0,linestyle='--')
plt.show()
```

![image-20250128150650657](https://db.xinghai.ink/Typora/17380480131767545.png)

**使用`pyplot`模块的`axhspan()`函数添加参考区域**

```python
axhspan(ymin,ymax,xmin=0,xmax=1,**kwargs)
```

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))

plt.grid(axis='y',linewidth=0.3)
plt.legend(['正弦','余弦'])
plt.axvline(x=0,ymax=0.9,ymin=0.1,linestyle='--')
plt.axhline(y=0,linestyle='--')


plt.axvspan(xmin=0.5,xmax=2.0,alpha=0.3)
plt.axhspan(ymin=0.5,ymax=1.0,alpha=0.3)

plt.show()
```

![image-20250128153300790](https://db.xinghai.ink/Typora/1738049582865855.png)

<h3>实例 四</h3>

全校高二年级各班男女英语成绩评估

|班级名称|平均成绩（男生）|平均成绩（女生）|
| ---- | ---- | ---- |
|高二1班|90.5|92.7|
|高二2班|89.5|87.0|
|高二3班|88.7|90.5|
|高二4班|88.5|85.0|
|高二5班|85.2|89.5|
|高二6班|86.6|89.8|

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

men_means = np.array([90.5, 89.5, 88.7, 88.5, 85.2, 86.6])
women_means = np.array([92.7, 87.0, 90.5, 85.0, 89.5, 89.8])

ind = np.arange(len(men_means))
width=0.2
plt.bar(ind-0.1,men_means,width=width,label='男生平均成绩')
plt.bar(ind+0.2,women_means,width=width,label='女生平均成绩')
plt.title('高二各班男生、女生英语平均成绩')

plt.xticks(ind,["高二1班", "高二2班", "高二3班", "高二4班", "高二5班", "高二6班"])
plt.ylabel('分数')

# 参考线
plt.axhline(88.5,linestyle='--',linewidth=1.0,label='全体平均成绩')


plt.legend(loc='lower right')
plt.show()
```

![image-20250128163212354](https://db.xinghai.ink/Typora/17380531350876904.png)

## 3.6    添加注释文本

**使用pyplot模块的`annotate()`函数为图表添加指向型注释文本**

```python
annotate(s, xy, *args, **kwargs)
```

- s	表示注释文本的内容
- xy	表示注释点所在的坐标，接收元组
- xytext	表示注释文本所在的坐标位置
- arrowprops	表示箭头的属性字典

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))

plt.grid(axis='y',linewidth=0.3)
plt.legend(['正弦','余弦'])
plt.axvline(x=0,ymax=0.9,ymin=0.1,linestyle='--')
plt.axhline(y=0,linestyle='--')


plt.axvspan(xmin=0.5,xmax=2.0,alpha=0.3)
plt.axhspan(ymin=0.5,ymax=1.0,alpha=0.3)

plt.annotate('最小值',xy=(-np.pi/2,-1.0), xytext=(-np.pi/2,-0.5),arrowprops={"arrowstyle":'->'})
plt.show()
```

![image-20250128165918791](https://db.xinghai.ink/Typora/17380547616572776.png)

**使用`pyplot`模块的`text()`添加无指向文本标记**

```python
text(x,y,s,fontdict=None,withdash=<deprecated parameter>,**kwargs)
```

- xy	表示注释文本的位置
- s	表示文本的内容
- fontdict	表示控制字体的字典

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))


plt.xlim(x.min() * 1.5, x.max() * 1.5)
plt.xticks([-np.pi,-np.pi / 2,0,np.pi /2, np.pi],[r'$-\pi$',r'$-\pi/2$','0',r'$\pi/2$',r'$\pi$'])



plt.grid(axis='y',linewidth=0.3)
plt.legend(['正弦','余弦'])
plt.axvline(x=0,ymax=0.9,ymin=0.1,linestyle='--')
plt.axhline(y=0,linestyle='--')


plt.axvspan(xmin=0.5,xmax=2.0,alpha=0.3)
plt.axhspan(ymin=0.5,ymax=1.0,alpha=0.3)

plt.annotate('最小值',xy=(-np.pi/2,-1.0), xytext=(-np.pi/2,-0.5),arrowprops={"arrowstyle":'->'})
plt.text(3.10,0.10,'y=sin(x)',bbox={'alpha':0.2})
plt.show()
```

![image-20250129165442197](https://db.xinghai.ink/Typora/17381408855587418.png)

<h3>实例</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(7)
y = np.array([10770, 16780, 24440, 30920, 37670, 48200, 57270])

rects = plt.bar(x,y,width=0.5,tick_label=["FY 2013 ", "FY 2014 ", "FY 2015 ",\
                                   "FY 2016 ", "FY 2017 ", "FY 2018 ", "FY 2019 "])

for i in rects:
    plt.text(i.get_x() + 0.25,i.get_height() + 400,s=i.get_height(),ha='center',va='bottom')
plt.show()
```

![image-20250129170448990](https://db.xinghai.ink/Typora/1738141490964128.png)

## 3.7    添加表格

matplotlib可以添加各种各样的表格

**使用`pyplot`模块的`table()`函数添加自定义表格**

```python
table(
    cellText=None,
    cellColours=None,
    cellLoc="right",
    colWidths=None,
    rowLabels=None,
    rowColours=None,
    rowLoc="left",
    colLabels=None,
    colColours=None,
    colLoc="center",
    loc="bottom",
    bbox=None,
    edges="closed",
    **kwargs,
)
```

- cellText	表示单元格中的数据，是一个二维列表
- cellColours	表示行标题所在单元格的背景颜色
- cellLoc	表示单元格的对其方式
- rowLabels	行标题文本
- colLabels	列标题文本

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False

x = np.linspace(-np.pi,np.pi)
plt.plot(x,np.sin(x))
plt.plot(x,np.cos(x))


plt.xlim(x.min() * 1.5, x.max() * 1.5)
plt.xticks([-np.pi,-np.pi / 2,0,np.pi /2, np.pi],[r'$-\pi$',r'$-\pi/2$','0',r'$\pi/2$',r'$\pi$'])



plt.grid(axis='y',linewidth=0.3)
plt.legend(['正弦','余弦'])
plt.axvline(x=0,ymax=0.9,ymin=0.1,linestyle='--')
plt.axhline(y=0,linestyle='--')


plt.axvspan(xmin=0.5,xmax=2.0,alpha=0.3)
plt.axhspan(ymin=0.5,ymax=1.0,alpha=0.3)

plt.annotate('最小值',xy=(-np.pi/2,-1.0), xytext=(-np.pi/2,-0.5),arrowprops={"arrowstyle":'->'})
plt.text(3.10,0.10,'y=sin(x)',bbox={'alpha':0.2})
plt.table(cellText=[[6,6,6],[8,8,8]],colWidths=[0.1]* 3,rowLabels=['第一行','第二行'],colLabels=['第一列','第二列','第三列'],loc='lower right')
plt.show()
```

![image-20250204132839166](https://db.xinghai.ink/Typora/1738646922873276.png)

<h3>实例 六</h3>

|配料名称|重量（g）|配料名称|重量（g）|
| ---- | ---- | ---- | ---- |
|面粉|250|全麦粉|150|
|酵母|4|苹果酱|250|
|鸡蛋|50|黄油|30|
|盐|4|白糖|20|

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = 'SimHei'

data1 = np.array([250, 150, 4, 250, 50, 30, 4, 20])
data = data1 / data1.sum()
labels = ['面粉', '全麦粉', '酵母', '苹果酱', '鸡蛋', '黄油', '盐', '白糖']
plt.pie(data,autopct="%.2f%%")
plt.legend(labels,loc='upper right',bbox_to_anchor=[1.2,1.1])
plt.table(cellText=[data1],cellLoc='center',colLabels=labels,rowLabels=['重量(g)'],loc='lower center')
plt.show()
```

![image-20250204154653949](https://db.xinghai.ink/Typora/17386552160733707.png)

## 3.8    习题

**在第2章编程题第1题的基础上定制柱形图，具体要求如下：**

- （1）设置y轴的标签为“平均成绩（分）”；

- （2）设置x轴的刻度标签位于两组柱形中间；
- （3）添加标题为“高二男生、女生的平均成绩”；
- （4）添加图例；
- （5）向每个柱形的顶部添加注释文本，标注平均成绩。

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = ['SimHei']

x = np.arange(6)
y1 = [85.5,91,72,59,66,55]
y2 = [94,82,89.5,62,49,53]

label = ['语文','数学','英语','物理','化学','生物']

bar1 = plt.bar(x,y1,width=0.3)
bar2 = plt.bar(x+0.3,y2,width=0.3)

# 第三章
plt.ylabel('平均分')
plt.xticks(np.array([0,1,2,3,4,5]) + 0.15,label)
plt.title('高二男生、女生的平均成绩')
plt.legend(['男生','女生'])
for i in zip(bar1,bar2, y1, y2):
    plt.text(i[0].get_x() + 0.15,i[0].get_height() + 1,i[2],ha='center')
    plt.text(i[1].get_x() + 0.15,i[1].get_height() + 1,i[3],ha='center')

plt.show()
```

![image-20250204171257461](https://db.xinghai.ink/Typora/17386603811572833.png)



**在第2章编程题第2题的基础上定制饼图，具体要求如下：**

- （1）添加标题为“拼多多平台子类目的销售额”；
- （2）添加图例，以两列的形式进行显示;
- （3）添加表格，说明子类目的销售额。

```python
import matplotlib.pyplot as plt
import numpy as np

labels = ['童装', '奶粉辅食', '孕妈专区', '洗护喂养', '宝宝尿裤', '春夏新品', '童车童床', '玩具文娱', '童鞋']
y = np.array([29665 , 3135.4, 4292.4, 5240.9, 5543.4, 5633.8, 6414.5, 9308.1, 10353])
plt.pie(y,radius=1.3,autopct='%.2f%%',pctdistance=0.8,explode=[0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1,0.1],labels=labels)

plt.legend(labels,loc='upper right',bbox_to_anchor=[1.7,1.1],ncol=2)

plt.table(cellText=[y],cellLoc='center',colLabels=labels,rowLabels=['销售额'],loc='lower center',bbox=[0, -0.4,1, 0.2])
plt.show()
```

![image-20250204174408186](https://db.xinghai.ink/Typora/17386622502619655.png)



# 第四章

## 4.1    图表样式概述

`matplotlib`在绘图的过程中会读取存储在本地的配置文件`matplotlibrc`,通过`matplotlibrc`文件中的缺省文件配置信息指定图表元素中的默认样式，完成图表元素的初始设置

**查看配置项**

`matplotlibrc`文件中包含众多配置项，可以通过`rc_params()`查看全部的配置

<h3>示例</h3>

```python
import matplotlib
print(matplotlib.rc_params())
```

![image-20250311153323024](https://db.xinghai.ink/Typora/17416784066206782.png)

**matplotlib的常用配置项**

|配置项|说明|默认值|
| ---- | ---- | ---- |
|lines.color|线条颜色|'C0'|
|lines.linestyle|线条类型|'-'|
|lines.linewidth|线条宽度|1.5|
|lines.marker|线条标记|'None'|
|lines.markeredgecolor|标记边框颜色|'auto'|
|lines.markeredgewidth|标记边框宽度|1.0|
|lines.markerfacecolor|标记颜色|'auto'|
|lines.markersize|标记大小|6.0|
|font.family|系统字体|['sans-serif']|
|font.sans-serif|无衬线字体|['DejaVu Sans', 'Bitstream Vera Sans', 'Computer Modern Sans Serif', 'LucidaGrande', 'Verdana', 'Geneva', 'Lucid', 'Arial', 'Helvetica', 'Avant Garde sans-serif']|
|font.size|字体大小|10.0|
|font.style|字体风格|'normal'|
|axes.unicode_minus|采用Unicode编码的减号|True|
|axes.prop_cycle|属性循环器|cycler('color', ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd', '#8c564b', '#e377c2', '#7f7f7f', '#bcbd22', '#17becf'])|
|figure.constrained_layout.use|使用约束布局|False|

**图表样式修改**

图表样式可以通过两种方式修改：`局部修改和全局修改`

全局修改就是直接修改`matplotlibrc`文件的配置项，此方法用于全局定制的需求（直接修改配置文件），`matplotlibrc`文件主要存在于三个路径，使用`matplotlib_fname()`函数可以查看当前的配置文件所在路径

<h3>示例</h3>

```python
import matplotlib
matplotlib.matplotlib_fname()
```

![image-20250311155629304](https://db.xinghai.ink/Typora/17416797917753582.png)

**局部样式修改**

局部样式修改就是通过代码动态的修改matplotlib配置项，此方法用于满足局部定制的需求

<h3>示例</h3>

```python
import matplotlib.pyplot as plt
# 通过函数的参数配置局部样式
plt.plot([1,2,3],[3,4,5],linewidth=3)
# 通过rcParams 配置局部样式
plt.rcParams['lines.linewidth'] = 3
# 通过
plt.show()
```

![image-20250316160810410](https://db.xinghai.ink/Typora/17421124933498366.png)



## 4.2    使用颜色

`matplotlib`的基础颜色主要有三种表示方式：单词缩写或单词、十六进制或HTML模式、RGB模式

**单词缩写或单词表示的颜色**

支持单词缩写和单词表示的颜色有八种：青色、洋红色、黄色、黑色、红色、绿色、白色、蓝色

|单词缩写|单词|说明|
| ---- | ---- | ---- |
|c|cyan|青色|
|m|magenta|洋红色|
|y|yellow|黄色|
|k|black|黑色|
|r|red|红色|
|g|green|绿色|
|b|blue|蓝色|
|w|white|白色|

<h3>示例</h3>

**使用`colors.cname`字典查看全部的颜色**

```python
from matplotlib import colors
colors.cnames
```

![image-20250311164103181](https://db.xinghai.ink/Typora/17416824660346649.png)

<h3>实例 一</h3>

**两个地区对不同种类图书的采购情况**

|图书种类|地区1（本）|地区2（本）|
| ---- | ---- | ---- |
|家庭|1200|1050|
|小说|2400|2100|
|心理|1800|1300|
|科技|2200|1600|
|儿童|1600|1340|

```python
import numpy as np
import matplotlib.pyplot as plt

y1 = [1200,2400,1800,2200,1600]
y2 = [1050,2100,1300,1600,1340]
x = np.arange(5)
bar_width=0.6
tick_labl= ['家庭','小说','心理','科技','儿童']
fig = plt.figure()
ax = fig.add_subplot(111)
ax.bar(x,y1,color='#FFCC00',width=bar_width,align='center')
ax.bar(x,y2,bottom=y1,color='#B0C4DE',width=bar_width,align='center')
plt.show()
```

![image-20250317181626618](https://db.xinghai.ink/Typora/17422065896059484.png)



## 4.3    选择线型

图表中，每个线条均有不同含义，一般可以设置颜色、宽度、类型来区分线条

| 线型取值 | 说明 | 样式 |
| ---- | ---- | ---- |
| `':'` | 短虚线 | ----------- |
| `'-.'` | 点划线 | — - — . — |
| `'--'` | 长虚线 | – – – – – |
| `'-'` | 实线 | — |

<h3>示例</h3>

**使用`linestyl`或`ls`参数指定先调样式**

```python
plt.plot([1,2,3],[3,4,5],linestyle='--')
plt.show()
plt.plot([1,2,3],[3,4,5],ls='--')
plt.show()
```

![image-20250317232902576](https://db.xinghai.ink/Typora/1742225344817913.png)

![image-20250317232911141](https://db.xinghai.ink/Typora/1742225352891638.png)

<h3>实例 二</h3>

**2017年7月与2019年7月国际外汇市场美元/人民币汇率走势**


|日期|2017年汇率|2019年汇率|
| ---- | ---- | ---- |
|3日 |6.8007|6.8640|
|4日 |6.8007|6.8705|
|5日 |6.8015|6.8697|
|6日 |6.8015|6.8697|
|7日 |6.8060|6.8697|
|8日 |6.8060|6.8881|
|9日 |6.8060|6.8853|
|10日|6.8036|6.8856|
|11日|6.8025|6.8677|
|12日|6.7877|6.8662|
|13日|6.7835|6.8662|
|14日|6.7758|6.8662|
|17日|6.7700|6.8827|
|18日|6.7463|6.8761|
|19日|6.7519|6.8635|
|24日|6.7511|6.8860|
|25日|6.7511|6.8737|
|26日|6.7539|6.8796|
|31日|6.7265|6.8841|

```python
import numpy  as np
import matplotlib.pyplot as plt

plt.rcParams['font.family'] = 'SimHei'

eurcny_2017 = np.array([6.8007,6.8007,6.8015,6.8015,6.8060,6.8060,
                        6.8060,6.8036,6.8025,6.7877,6.7835,6.7758,
                        6.7700,6.7463,6.7519,6.7511,6.7511,6.7539,6.7265])

eurcny_2019 = np.array([6.8640,6.8705,6.8697,6.8697,6.8697,6.8881,
                        6.8853,6.8856,6.8677,6.8662,6.8662,6.8662,
                        6.8827,6.8761,6.8635,6.8860,6.8737,6.8796,6.8841])

date_x = np.array([3,4,5,6,7,8,9,10,11,12,13,14,17,18,19,24,25,26,31])

plt.plot(date_x,eurcny_2017,color='#006374',linewidth=2,label='2017年7月美元/人民币汇率')
plt.plot(date_x,eurcny_2019,color='#8a2e76',ls='--',linewidth=2,label='2019年7月美元/人民币汇率')


plt.title('2017年7月与2019年7月国际外汇市场美元/人民币汇率走势')
plt.xlabel('日期')
plt.ylabel('汇率')
plt.legend()
plt.show()
```

![image-20250317235052441](https://db.xinghai.ink/Typora/1742226654552594.png)



## 4.4    添加数据标记

`mtplotlib`中默认隐藏折线图的书籍标记，数据标记用于强调点的位置，常用于折线图和散点图中

|标记取值|样式|说明|标记取值|样式|说明|
| ---- | ---- | ---- | ---- | ---- | ---- |
|'s'|■|正方形|'x'|✖|叉形|
|'8'|●|八边形|'p'|✚|十字交叉形|
|'>'|▲|右三角|'d'|◇|长菱形|
|'<'|▼|左三角|'D'|◆|正菱形|
|'^'|△|正三角|'H'|♢|六边形1|
|'v'|▽|倒三角|'h'|♤|六边形2|
|'o'|○|圆形|'*'|★|星形|
|'p'|♡|五边形|'+'|＋|加号|
|','|·|像素点|'.'|•|点|
|'1'|☰|下三叉|'2'|☱|上三叉|
|'3'|☲|左三叉|'4'|☴|右三叉|
|'-'|─|水平线|'x'|×|乘号|
|'|'|┃|垂直线|0|─|水平线，位于基线左方|
|1|─|水平线，位于基线右方|2|┐|垂直线，位于基线上方|
|3|└|垂直线，位于基线下方|4|◀|朝左方向键，位于基线右方|
|5|▶|朝右方向键，位于基线左方|6|▲|朝上方向键，位于基线下方|
|7|▼|朝下方向键，位于基线上方|8|◀|朝左方向键，位于基线左方|
|9|▶|朝右方向键，位于基线右方|10|▲|朝上方向键，位于基线上方|
|11|▼|朝下方向键，位于基线下方|  |  |  |

使用`pyplot`的`plot()`或`scatter()`函数时，可以将标记的取值产地给`marker`参数

```python
plt.plot([1,2,3],[3,4,5],marker='*')
```

此外

- `markeredgecolor`或`mec`	表示标记边框的颜色
- `markeredgewidth`或`mew`	表示标记边框的宽度
- `markerfacecolor`或`mfc`	表示标记的填充颜色
- `markerfacecoloralt`或`mfcalt`	表示标记备用的填充颜色
- `markersize`或`ms`	表示标记的大小



<h3>示例</h3>

```python
import matplotlib.pyplot as plt

plt.plot([1,2,3],[3,4,5],ms=20,marker='*',mfc='y')
plt.show()
```

![image-20250318000729257](https://db.xinghai.ink/Typora/17422276516430233.png)

<h3>实例    三</h3>

**标记不同产品各季度的销售额**

|季度|产品A（万元）|产品B（万元）|产品C（万元）|
| ---- | ---- | ---- | ---- |
|第1季度|2144| 853|153|
|第2季度|4617|1214|155|
|第3季度|7674|2414|292|
|第4季度|6666|4409|680|

```python
import matplotlib.pyplot as plt
import numpy as  np

plt.rcParams['font.family'] = 'SimHei'

sale_a = [2144,4617,7674,6666]
sale_b = [ 853,1214,2414,4409]
sale_c = [153,155,292,680]

plt.plot(sale_a, 'D-', sale_b, '^:', sale_c, 's--')

plt.grid(alpha=0.3)
plt.ylabel('销售额(万元)')
plt.xticks(np.arange(len(sale_a)),['第一季度','第二季度','第三季度','第四季度'])
plt.legend(['产品A','产品B','产品C'])
plt.show()
```

![image-20250318002931004](https://db.xinghai.ink/Typora/17422289726917706.png)

## 4.5    设置字体

```python
import matplotlib.pyplot as plt
plt.plot([1,2,3],[3,4,5])
plt.text(1.9, 3.75, 'y=x+2', bbox=dict(facecolor='y'), family='serif', fontsize=18, fontstyle='normal', rotation=-60)
```

![image-20250318003421653](https://db.xinghai.ink/Typora/17422292633445268.png)

<h3>实例 四</h3>

**未来15天的最高气温和最低气温（设置字体样式）**

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = 'Simhei'

x = np.arange(4,19)
y_max = np.array([32,33,33,34,34,31,30,29,30,29,26,23,21,25,31])
y_min = np.array([19,19,20,22,22,21,22,16,18,18,17,14,15,16,16])

plt.plot(x,y_max,marker='o',label='最高温度')
plt.plot(x,y_min,marker='o',label='最低温度')

x_temp = 4

for y_h,y_l in zip(y_max,y_min):
    plt.text(x_temp-0.3,y_h + 0.7,y_h,family='SimHei',fontsize=8,fontstyle='normal')
    plt.text(x_temp-0.3,y_l + 0.7,y_l,family='SimHei',fontsize=8,fontstyle='normal')
    x_temp += 1

plt.title('未来15天的最高气温和最低气温')
plt.xlabel('日期')
plt.ylabel('温度(℃)')
plt.legend()
plt.ylim(0,40)
plt.show()
```

![image-20250318004957662](https://db.xinghai.ink/Typora/17422301995434387.png)

## 4.6    切换主题风格

使用`sttyle.available`可以查看`matplotlib`的所有可用的主题风格

```python
import matplotlib.style as ms

ms.available
```

![image-20250318005528929](https://db.xinghai.ink/Typora/17422305307848701.png)

<h3>示例</h3>

使用`style.use`可以切换主题风

```python
import matplotlib.style as ms
import matplotlib.pyplot as plt
ms.use('seaborn-v0_8-dark')
plt.plot([1,2,3],[3,4,5],ms=20,marker='*',mfc='y')
plt.show()
ms.use('ggplot')
plt.plot([1,2,3],[3,4,5],ms=20,marker='*',mfc='y')
plt.show()
```

![image-20250318005832894](https://db.xinghai.ink/Typora/17422307147713187.png)

![image-20250318005841689](https://db.xinghai.ink/Typora/17422307235466833.png)

## 4.7    填充区域

`matplotlib`中提供多个函数用于填充多边形或区域 `fill()`函数用于填充多边形,`fill_between()`或`fill_betweenx()`用于填充两条水平线或垂直曲线之间的区域



`fill()`函数语法如下

```python
fill(*args,data=None,facecolor,edgecolor,linewidt,**kwargs)
```

- *args	表示x轴坐标和y轴坐标
- facecolor	表示填充的背景颜色
- edgecolor	表示边框的颜色
- linewidth	表示边框的宽度

<h3>示例</h3>

```python
import matplotlib.pyplot as plt

plt.fill([1, 2, 3, 2, 1], [1, 2, 1, 0, 1],'b')
plt.show()
```

![image-20250318092513264](https://db.xinghai.ink/Typora/1742261116373185.png)

**`full_between()`函数语法如下**

```python
fill_between(x, y1, y2, where=None, interpolate=False, setp=None, data=NOne, **kwarg)
```

- x	表示x轴坐标的序列
- y1	第一条曲线的y轴坐标
- y2	第二条曲线的y轴坐标
- where	布尔值序列，表示要填充区域的条件

<h3>实例 五</h3>

**彩色的雪花**（没理解，只有上帝看得懂）

```python
# 05_colorful_snowflakes
import numpy as np
import matplotlib.pyplot as plt


def koch_snowflake(order, scale=10):
    def _koch_snowflake_complex(order):
        if order == 0:
            # 初始三角形
            angles = np.array([0, 120, 240]) + 90
            return scale / np.sqrt(3) * np.exp(np.deg2rad(angles) * 1j)
        else:
            ZR = 0.5 - 0.5j * np.sqrt(3) / 3
            p1 = _koch_snowflake_complex(order - 1)  # 起点
            p2 = np.roll(p1, shift=-1)  # 终点
            dp = p2 - p1  # 连接向量
            new_points = np.empty(len(p1) * 4, dtype=np.complex128)
            new_points[::4] = p1
            new_points[1::4] = p1 + dp / 3
            new_points[2::4] = p1 + dp * ZR
            new_points[3::4] = p1 + dp / 3 * 2
            return new_points

    points = _koch_snowflake_complex(order)
    x, y = points.real, points.imag
    return x, y


x, y = koch_snowflake(order=2)
fig = plt.figure()
ax = fig.add_subplot(111)
ax.fill(x, y, facecolor='lightsalmon', edgecolor='orangered', linewidth=3)
plt.show()
```

![image-20250318125225117](https://db.xinghai.ink/Typora/1742273546971529.png)

## 4.8    习题

**已知2018年、2019年物流行业的快递业务量**

|月份|2018年业务量（亿件）|2019年业务量（亿件）|
| ---- | ---- | ---- |
| 1月|39|45|
| 2月|20|28|
| 3月|40|48|
| 4月|38|49|
| 5月|42|50|
| 6月|43|51|
| 7月|41|50|
| 8月|41|50|
| 9月|45|51|
|10月|48|52|
|11月|52|70|
|12月|50|65|

**第一题**

根据表中2018年、2019年物流行业快递业务量数据绘制图表，具体要求如下：

1. 绘制反映2018年、2019年快递业务量趋势的折线图。
2. 折线图的x轴为月份；y轴为业务量，y轴的标签为“业务量（亿件）”。
3. 代表2018年的折线样式：颜色为“#8B0000”，标记为正三角形，线型为长虚线，线宽为1.5。
4. 代表2019年的折线样式：颜色为“#006374”，标记为长菱形，线型为实线，线宽为1.5。
5. 折线图的主题风格切换为“fivethirtyeight”。

```python
import matplotlib.pyplot as plt
import numpy as np
import matplotlib.style as ms

plt.rcParams['font.family'] = 'SimHei'

y_2018 = [39,20,40,38,42,43,41,41,45,48,52,50]
y_2019 = [45,28,48,49,50,51,50,50,51,52,70,65]
x = np.arange(1,13)

plt.plot(x,y_2018,color='#8B0000',marker='^',ls='--',lw=1.5)
plt.plot(x,y_2019,color='#006374',marker='d',ls='-',lw=1.5)

plt.xlabel('月份')
plt.ylabel('业务量(亿件)')
ms.use('fivethirtyeight')

plt.show()
```

![image-20250318132229261](https://db.xinghai.ink/Typora/17422753510773766.png)



第二题

绘制一个包含正弦曲线和余弦曲线的图表，具体要求如下：

1. 正弦曲线的样式：红色，线宽为1.0。
2. 余弦曲线的样式：蓝色，线宽为1.0，透明度为0.5。
3. x轴的刻度标签为 -π, -π/2, 0, π/2, π。
4. 在x = 1, y = np.cos(1)的位置添加指向型注释文本。
5. 填充|x| < 0.5或cosx > 0.5的区域为绿色，透明度为0.25。

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(-np.pi, np.pi, 0.1)

sinx = np.sin(x)
cosx = np.cos(x)

plt.plot(x, sinx, color='red', linewidth=1.0, label='sin(x)')
plt.plot(x, cosx, color='blue', linewidth=1.0, alpha=0.5, label='cos(x)')

plt.xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi], ['-π', '-π/2', '0', 'π/2', 'π'])
plt.annotate('cos(1)', xy=(1, np.cos(1)), xytext=(1.5, 0.5), arrowprops={"arrowstyle":'->'})
plt.fill_between(x, cosx, where=(np.abs(x) < 0.5) | (cosx > 0.5), color='green', alpha=0.25)

plt.show()
```

![image-20250318144226103](https://db.xinghai.ink/Typora/17422801487492075.png)







# 第五章

matplotlib 可以将整个画布规划成等分布局的`m x n(行 × 列)`的矩阵区域，并按照先行后列的方式对每个区域进行编号（编号从1开始）

## 5.1    绘制固定区域的子图

**绘制单子图**

使用`pyplot`的`subplot()`函数可以在规划好的某个区域中绘制单子图，`subplot()`函数的语法格式如下

```python
subplot(nrows,ncols, index, projection, polar, sharex, sharey, label, **kwargs)
```

该函数常用参数含义如下

- nrows	表示规划区的行数
- ncols	表示规划区的列数
- index	表示规划区的索引
- projection	表示子图的索引类型，可以为 None, aitoff, hammer, lambert, mollweide



<h3>示例</h3>

```python
import matplotlib.pyplot as plt


ax1 = plt.subplot(326)
ax1.plot([1,2,3,4,5])

ax2 = plt.subplot(312)
ax2.plot([1,2,3,4,5])

plt.show()
```

![image-20250404184901444](https://db.xinghai.ink/Typora/17437637446514373.png)

<h3>实例 一</h3>

某工厂产品A与产品B去年的销量额分析

|月份|产品A的销售额（亿元）|产品B的销售额（亿元）|
| ---- | ---- | ---- |
|1|20|17|
|2|28|22|
|3|23|39|
|4|16|26|
|5|29|35|
|6|36|23|
|7|39|25|
|8|33|27|
|9|31|29|
|10|19|38|
|11|21|28|
|12|25|20|

```python
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif'] = "SimHei"
x = np.arange(1,13)
y1 = [20, 28, 23, 16, 29, 36, 39, 33, 31, 19, 21, 25]
y2 = [17, 22, 39, 26, 35, 23, 25, 27, 29, 38, 28, 20]
labels = [f"{i}月" for i in x]

a1 = plt.subplot(211)
a1.plot(x, y1, 'm--o', lw=2, ms=5, label='产品A')
a1.plot(x, y2, 'g--o', lw=2, ms=5, label='产品B')
a1.set_title("产品A 与产品B的销售额", fontsize=11)
a1.set_ylim(10, 45)
a1.set_ylabel('销售额(亿元)')
a1.set_xlabel('月份')

for xy in zip(x, y1, y2):
    a1.annotate(f"{xy[1]}" , xy=(xy[0],xy[1]), xytext=(xy[0]-0.125,xy[1]+1))
    a1.annotate(f"{xy[2]}", xy=(xy[0],xy[2]), xytext=(xy[0]-0.125,xy[2]+1))
a1.legend()

a2 = plt.subplot(223)
a2.pie(y1, radius=1, wedgeprops={'width':0.5}, labels=labels, autopct='%3.1f%%', pctdistance=0.75)
a2.set_title('产品A的销售额 ')

a3 = plt.subplot(224)
a3.pie(y2, radius=1, wedgeprops={'width':0.5}, labels=labels,autopct='%3.1f%%', pctdistance=0.75)
a3.set_title('产品B的销售额 ')

plt.tight_layout()
plt.show()
```

![image-20250415153357482](https://db.xinghai.ink/Typora/17447024467765589.png)





**绘制多子图**

使用`pyplot`的`subplots()`函数可以再规划好的所有区域一次绘制多个子图，`subplots()`函数的语法格式如下

```python
subplots(
    nrows: Literal[1] = ...,
    ncols: Literal[1] = ...,
    *,
    sharex: bool | Literal["none", "all", "row", "col"] = ...,
    sharey: bool | Literal["none", "all", "row", "col"] = ...,
    squeeze: Literal[True] = ...,
    width_ratios: Sequence[float] | None = ...,
    height_ratios: Sequence[float] | None = ...,
    subplot_kw: dict[str, Any] | None = ...,
    gridspec_kw: dict[str, Any] | None = ...,
    **fig_kw
)
```

该函数常用参数含义如下：

- nrows	表示规划区域的行数
- ncols	表示规划区域的列数
- sharex,sharey	表示是否共享子图的x或y轴的坐标



<h3>示例</h3>

```python
import matplotlib.pyplot as plt
fig, ax_arr = plt.subplots(2,2,sharex=True)

ax_arr[1,0].plot([1,2,3,4,5])
```

![image-20250415155251753](https://db.xinghai.ink/Typora/1744703576422973.png)



<h3>实例 二</h3>

部分国家养猫人群比例与养狗人群比例

| 国家     | 养猫人群比例（%） | 养狗人群比例（%） |
| -------- | ----------------- | ----------------- |
| 中国     | 19                | 25                |
| 加拿大   | 33                |  33                |
| 巴西     | 28                | 58                |
| 澳大利亚 |  29                 | 39                |
| 日本     | 14                | 15                |
| 墨西哥   | 24                |  64                |
| 俄罗斯   | 57                |  29                |
| 韩国     | 6                 |  23                |
| 瑞士     | 26                |  22                |
| 土耳其   | 15                |  11                |
| 英国     | 27                |  27                |
| 美国     | 39                |  50                |

```python
import matplotlib.pyplot as plt
import numpy as np
plt.rcParams['font.family'] = "SimHei"

y = np.arange(12)
x1 = [19,33,28,29,14,24,57,6,26,15,27,39]
x2 = [25,33,58,39,15,64,29,23,22,11,27,50]
label = ["中国","加拿大","巴西","澳大利亚","日本","墨西哥","俄罗斯","韩国","瑞士","土耳其","英国","美国"]


def autolabel(ax,rects):
    for rect in rects:
        width = rect.get_width()
        ax.text(width + 2,rect.get_y(),s=width,ha='center',va='bottom')

# 设置画布
fig, (ax1, ax2) = plt.subplots(1,2)
fig.set_figwidth(12)

# 绘制图象
rects1 = ax1.barh(y,x1,tick_label=label,height=0.5,color="#FFA500")
rects2 = ax2.barh(y,x2,tick_label=label,height=0.5,color="#20B2AA")

# 设置ax1图表样式
ax1.set_xlabel('人群比例（%）')
ax1.set_title('部分国家养猫人群比例')
ax1.set_xlim(0,max(x1)+10)
autolabel(ax1,rects1)

# 设置ax2图表样式
ax2.set_xlabel('人群比例（%）')
ax2.set_title('部分国家养狗人群比例')
ax2.set_xlim(0,max(x2)+10)
autolabel(ax2,rects2)
plt.show()
```

![image-20250420161758813](https://db.xinghai.ink/Typora/17451370816257627.png)

## 5.2   绘制自定义区域的子图

**绘制单子图**

使用`pyplot`的`subplot2grid()`函数可以将整个画布规划成非等分布局的区域，并可以在选中的某个区域中绘制单个子图，语法格式如下

```python
subplot2grid(shape,loc,rowspan=1,colspan=1,fig=None,**kwargs)
```

该函数常用参数含义如下

- shape	表示规划的区域结构，它是一个包含两个整形数据的元组，其中第一个元素表示规划区域的行数，第二个元素表示规划区域的列数
- loc	表示选择区域的位置，他是一个包含两个整形数据的元组，第一个表示所在的行数，第二个表示所在的列数
- rowspan	表示向下跨越的行数
- colspan	表示向右跨越的列数
- fig	表示放置子图的列数



<h3>示例</h3>

```python
import matplotlib.pyplot as plt

ax1 = plt.subplot2grid((2,3),(0,2))
ax1.plot([1,2,3,4,5])
ax2 = plt.subplot2grid((2,3),(1,1),colspan=2)
ax2.plot([1,2,3,4,5])

plt.show()
```

![image-20250420164649396](https://db.xinghai.ink/Typora/17451388111841621.png)

<h3>实例 三</h3>

抖音用户地区分布比例和人群增长倍数

| 地区           | 2017年用户比例（%） | 2018年用户比例（%） | 人群增长倍数 |
| -------------- | ------------------- | ------------------- | ------------ |
| 一线城市       | 21                  | 13                  | 51        |
| 二线城市       | 35                  | 32                  | 73        |
| 三线城市       | 22                  | 27                  | 99        |
| 四线及以外     | 19                  | 27                  | 132       |
| 其他国家及地区  | 3                   | 1                   | 45        |

```python
import matplotlib.pyplot as plt

# 数据
labels = ['一线城市', '二线城市', '三线城市', '四线及以外', '其他国家及地区']
data_2017 = [21, 35, 22, 19, 3]
data_2018 = [13, 32, 27, 27, 1]
y = [51, 73, 99, 132, 45]

# 绘制3个子图
ax1 = plt.subplot2grid((3,2),(0,0),rowspan=2,colspan=2)
ax2 = plt.subplot2grid((3,2),(2,0))
ax3 = plt.subplot2grid((3,2),(2,1))

rect1 = ax1.bar([1,2,3,4,5],y,tick_label=labels,color='#20B2AA',width=0.5)
rect3 = ax3.pie(data_2018,radius=1.5,labels=labels,autopct="%.1f%%",colors=['#2F4F4F','#FF0000','#A9A9A9','#FFD700','#B0C4DE'])
rect2 = ax2.pie(data_2017,radius=1.5,labels=labels,autopct="%.1f%%",colors=['#2F4F4F','#FF0000','#A9A9A9','#FFD700','#B0C4DE'])

# 设置图表样式
plt.tight_layout()

for i in rect1:
    height = i.get_height()
    ax1.text(i.get_x()+0.25,height+3,s=f"{height}",ha='center',va='bottom')

ax1.set_title('抖音2018vs2017人群增长倍数')
ax1.set_ylabel('增长倍数')
ax1.set_ylim(0,max(y)+20)
ax1.axhline(75,ls='--',lw=1,color="gray")

ax2.set_title('2017年抖音用户地区分布的比例')
ax3.set_title('2018年抖音用户地区分布的比例')

plt.show()
```

![image-20250420174323010](https://db.xinghai.ink/Typora/17451422048723588.png)



## 5.3    共享子图的坐标轴

当`pyplot`使用`subplots()`函数绘制子图时，可以通过`sharex`或`sharey`参数控制是否共享x轴或者y轴，`sharex`或`sharey`支持`False`或`None`、`True`或`all`、`row`、`col`中任取一值，这些值含义如下

- True或all，表示共享所有子图的x或y轴
- False或None，表示不共享子图的x或y轴
- row表示每一行的子图之间共享x或y轴
- col表示每一列的子图共享x或y轴



<h3>示例</h3>

```python
import numpy as np
import matplotlib.pyplot as plt

x1 = np.linspace(0, 2 *np.pi, 400)
x2 = np.linspace(0.01, 10, 100)
x3 = np.random.rand(10)
x4 = np.arange(0,6,0.5)
y1 = np.cos(x1 ** 2)
y2 = np.sin(x2)
y3 = np.linspace(0,3,10)
y4 = np.power(x4,3)

fig, ax_arr = plt.subplots(2, 2, sharex=True)
ax1 = ax_arr[0, 0]
ax1.plot(x1, y1)
ax2 = ax_arr[0, 1]
ax2.plot(x2, y2)
ax3 = ax_arr[1, 0]
ax3.scatter(x3, y3)
ax4 = ax_arr[1, 1]
ax4.scatter(x4, y4)
plt.show()
```

![image-20250420193825024](https://db.xinghai.ink/Typora/17451491072351182.png)

**共享非相邻子图的坐标轴**

直接将代表子图的变量传给`sharex`或`sharey`传给坐标轴，则可以直接共享坐标轴

```python
import matplotlib.pyplot as plt
import numpy as np

x1 = np.linspace(0, 2 *np.pi, 400)
y1 = np.cos(x1 ** 2)
x2 = np.linspace(0.01, 10, 100)
y2 = np.sin(x2)
ax1 = plt.subplot(221)
ax1.plot(x1, y1)

ax2 = plt.subplot(224, sharex=ax1)
ax2.plot(x2, y2)
plt.show()
```

![image-20250420195248382](https://db.xinghai.ink/Typora/17451499729935334.png)

<h3>实例 四</h3>

某地区全年平均气温与降水量、蒸发的关系

| 月份 | 平均气温（℃） | 降水量（ml） | 蒸发量（ml） |
| ---- | ------------- | ------------ | ------------ |
| 1月  | 2.0           | 2.6          | 2.0          |
| 2月  | 2.2           | 5.9          | 4.9          |
| 3月  | 3.3           | 9.0          | 7.0          |
| 4月  | 4.5           | 26.4         | 23.2         |
| 5月  | 6.3           | 28.7         | 25.6         |
| 6月  | 10.2          | 70.7         | 76.7         |
| 7月  | 20.3          | 175.6        | 135.6        |
| 8月  | 33.4          | 182.2        | 162.2        |
| 9月  | 23.0          | 48.7         | 32.6         |
| 10月 | 16.5          | 18.8         | 20.0         |
| 11月 | 12.0          | 6.0          | 6.4          |
| 12月 | 6.2           | 2.3          | 3.3          |

```python
import matplotlib.pyplot as plt
plt.rcParams['font.family'] = 'SimHei'

data_tem = [2.0,2.2,3.3,4.5,6.3,10.2,20.3,33.4,23.0,16.5,12.0,6.2]
data_precipitation = [2.6,5.9,9.0,26.4,28.7,70.7,175.6,182.2,48.7,18.8,6.0,2.3]
data_evaporaton = [2.0,4.9,7.0,23.2,25.6,76.7,135.6,162.2,32.6,20.0,6.4,3.3]
month_x = [i for i in range(1,13)]

fig, ax = plt.subplots()
bar_ev = ax.bar(month_x, data_evaporaton,color='orange',tick_label=[f"{i}月" for i in range(1,13)])
bar_pre = ax.bar(month_x,data_precipitation,bottom=data_evaporaton,color='green')
ax_right = ax.twinx()
line = ax_right.plot(month_x,data_tem,'o-m')

# 图表样式
ax.set_ylabel('降水量(ml)')
ax.set_title('平均气温与降水量、蒸发量的关系')
ax_right.set_ylabel('气温($^\circ$C)')
plt.legend([bar_ev,bar_pre,line[0]],['蒸发量','降水量','平均气温'],shadow=True,fancybox=True)
plt.show()
```

![image-20250421121325221](https://db.xinghai.ink/Typora/17452088079002676.png)

## 5.4    子图的布局

布局包括约束布局、紧密布局和自定义布局

**约束布局**

使用`subplots()`或`figure()`函数的`contrained_layout`参数或者修改`figure.contrained_layoute.use`配置项即可修改布局

<h3>示例</h3>

```python
import matplotlib.pyplot as plt

fig, axs = plt.subplots(2, 2, constrained_layout=True)
ax1 = axs[0, 0]
ax1.set_title('Title')
ax2 = axs[0, 1]
ax2.set_title('Title')
ax3 = axs[1, 0]
ax3.set_title('Title')
ax4 = axs[1, 1]
ax4.set_title('Title')
plt.show()
```

![image-20250421121937155](https://db.xinghai.ink/Typora/17452091795029948.png)

**紧密布局**

使用`tight_layout()`函数可以实现紧密布局，构造函数如下

```python
tight_layout(pad=1.08, h_pad=None,w_pad=None, rect=None)
```

该函数的参数含义如下

- pad	表示画布边缘与子图边缘之间的空白区一的大小，默认是1.08
- h_pad,w_pad	表示相邻子图之前的空白区域的大小
- rect	表示调整所有子图位置的矩形区域的四元组，默认是(0,0,1,1)



<h3>示例</h3>

```python
import matplotlib.pyplot as plt
fig, axs = plt.subplots(2, 2)
a_one = axs[0, 0]
a_one.set_title('Title')
a_two = axs[0, 1]
a_two.set_title('Title')
a_thr = axs[1, 0]
a_thr.set_title('Title')
a_fou = axs[1, 1]
a_fou.set_title('Title')

plt.tight_layout(pad=0.4, w_pad=1, h_pad=7)
plt.show()
```

![image-20250421155132410](https://db.xinghai.ink/Typora/17452218951378279.png)

**自定义布局**

`matplotlib`的`gridspec`模块是专门用来指定画布中子图的位置的模块，该模块包含一个`GridSpec`类，通过显式创建类对象来自定义画布中子图的布局结构，`GridSpec`类的构造方法的语法格式如下

```python
GridSpec(nrows, ncols figure=None, left=None, bottom=None, right=None,,  top=None, wspace=None, hspace=None, width_rtatios=None,height_ratios=None)
```

该函数常用方法如下

- nrows 	表示行数
- ncols	表示列数
- figure	表示布局的画布
- left，bottom，right，top	表示子图的范围
- wspace	表示子图之间的预留宽度
- hspace	表示子图之间的·预留高度

<h3>示例</h3>

使用`GridSpec`方法

```python
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec
fig2 = plt.figure()
g = gridspec.GridSpec(2,2,figure=fig2,wspace=0.7)
ax1 = fig2.add_subplot(g[0,0])
ax2 = fig2.add_subplot(g[0,1])
ax3 = fig2.add_subplot(g[1,0])
ax4 = fig2.add_subplot(g[1,1])


plt.show()
```

![image-20250421163805707](https://db.xinghai.ink/Typora/17452246877064197.png)

<h3>示例</h3>

使用`add_gridspec`方法

```python
import matplotlib.pyplot as plt

fig3 = plt.figure()
gs = fig3.add_gridspec(3, 3,hspace=0.7,wspace=1)
f3_a1 = fig3.add_subplot(gs[0, :])
f3_a1.set_title('gs[0, :]')
f3_a2 = fig3.add_subplot(gs[1, :-1])
f3_a2.set_title('gs[1, :-1]')
f3_a3 = fig3.add_subplot(gs[1:, -1])
f3_a3.set_title('gs[1:, -1]')
f3_a4 = fig3.add_subplot(gs[-1, 0])
f3_a4.set_title('gs[-1, 0]')
f3_a5 = fig3.add_subplot(gs[-1, -2])
f3_a5.set_title('gs[-1, -2]')

plt.show()
```

![image-20250421163611188](https://db.xinghai.ink/Typora/17452245730371828.png)

<h3>实例 五</h3>

2018上半年某品牌汽车的销售额

| 月份 | 销售额 |
| ---- | ------ |
| 1月  | 2150   |
| 2月  | 1050   |
| 3月  | 1560   |
| 4月  | 1480   |
| 5月  | 1530   |
| 6月  | 1490   |

2018上半年某品牌汽车的销量

| 分公司 | 销量  |
| ------ | ----- |
| 北京   | 83775 |
| 上海   | 62860 |
| 广州   | 59176 |
| 深圳   | 64205 |
| 浙江   | 48671 |
| 山东   | 39968 |

```python
import matplotlib.pyplot as plt
plt.rcParams['font.family'] = 'SimHei'

# 准备数据
x_month = [ f"{i}月" for i in range(1,7)]
y_scales = [2150,1050,1560,1480,1530,1490]
x_citys = ["北京","上海","广州","深圳","浙江","山东"]
y_sale_count = [83775,62860,59176,64205,48671,39968] 

# 子图绘制
fig = plt.figure(constrained_layout=True)
gs = fig.add_gridspec(2,2)
ax1 = fig.add_subplot(gs[0,:])
ax2 = fig.add_subplot(gs[1,0])
ax3 = fig.add_subplot(gs[1,1])

# 绘制图表
ax1.bar(x_month,y_scales,width=0.5,color="#3299CC")
ax2.plot(x_citys,y_sale_count,'m--o',ms=8)
ax3.stackplot(x_citys,y_sale_count,color='#9999FF')

# 图表样式
ax1.set_title('2018年上半年某品牌汽车销售额')
ax1.set_ylabel('销售额（亿元）')
ax2.set_title('分公司某品牌汽车的销量')
ax2.set_ylabel('销量（辆）')
ax3.set_title('分公司某品牌汽车的销量')
ax3.set_ylabel('销量(量)')
plt.show()
```

![image-20250421170301131](https://db.xinghai.ink/Typora/17452261830083168.png)

## 5.5  习题

**第一题**

按照如下要求绘制图表：

- （1）画布被规划为2×3的矩阵区域；
- （2）在编号为3的区域中绘制包含一条正弦曲线的子图；
- （3）在编号为6的区域中绘制包含一条余弦曲线的子图；
- （4）共享两个子图的x轴。

```python
import matplotlib.pyplot as plt
import numpy as np
plt.rcParams['font.family'] = 'SimHei'
plt.rcParams['axes.unicode_minus'] = False

x = np.linspace(-np.pi,np.pi)
cos = np.cos(x)
sin = np.sin(x)

fig = plt.figure(constrained_layout=True)
gs = fig.add_gridspec(2,3)

ax1 = fig.add_subplot(gs[0,0])
ax2 = fig.add_subplot(gs[0,1])
ax3 = fig.add_subplot(gs[0,2])
ax4 = fig.add_subplot(gs[1,0])
ax5 = fig.add_subplot(gs[1,1])
ax6 = fig.add_subplot(gs[1,2])

ax3.plot(x,sin)
ax6.plot(x,cos)


plt.show()
```

![image-20250421172023572](https://db.xinghai.ink/Typora/17452272253026378.png)

**第二题**

```python
import matplotlib.pyplot as plt

fig = plt.figure()
gs = fig.add_gridspec(3,4,hspace=0.3,wspace=0.5)

ax1 = fig.add_subplot(gs[0,:])
ax2 = fig.add_subplot(gs[1,0:2])
ax3 = fig.add_subplot(gs[1,2:4])
ax4 = fig.add_subplot(gs[2,0])
ax4 = fig.add_subplot(gs[2,1:])

plt.show()
```

![image-20250421172649901](https://db.xinghai.ink/Typora/17452276123147497.png)

# 第六章

## 6.1   坐标轴的概述

坐标轴的定制，坐标轴主要包括轴脊，刻度，其中刻度可以分为刻度线和刻度标签，刻度线可以分为主刻度线和次刻度线，坐标轴的各部分均是`matplotlib`类的对象



## 6.2    向任意位置添加坐标轴

`matplotlib`支持向画布的任意位置添加坐标轴系统，同时显示坐标轴，而不再受限于规划区域的限制，pyplot模块可以使用`axes()`函数创建一个`Axes`类的对象，并将对象添加到当前画布中

`axes()`函数的语法格式如下

```python
axes(arg=None,projection=None,polar=False,aspect,frame_no,**kwargs)
```

该函数常用参数如下

- arg支持None,4-tuple参数，None表示添加于画布相同大小的对象，4-tuple是一个4个参数的元组，分别代表坐标轴左侧和底部到坐标轴的位置，宽度和高度
- projection表示坐标轴的类型

<h3>示例</h3>

```python
import matplotlib.pyplot as plt

ax = plt.axes((0.2,0.5,0.3,0.3),projection=None)
ax.plot([1,2,3,4,5])

ax2 = plt.axes((0.6,0.4,0.2,0.2))
ax2.plot([1,2,3,4,5])
plt.show()
```

![image-20250428170253951](https://db.xinghai.ink/Typora/17458309769657264.png)

## 6.3    定制刻度

<h3>实例 一</h3>

| 时间  | 风速（km/h） |
| ----- | ------------ |
| 00:00 | 7            |
| 02:00 | 9            |
| 04:00 | 11           |
| 06:00 | 14           |
| 08:00 | 8            |
| 10:00 | 15           |
| 12:00 | 22           |
| 14:00 | 11           |
| 16:00 | 10           |
| 18:00 | 11           |
| 20:00 | 11           |
| 22:00 | 13           |
| 00:00 | 8            |

```python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.dates import DateFormatter, HourLocator

plt.rcParams['font.family'] = 'SimHei'
x_date = pd.date_range("2019-10-24","2019-10-25",freq='2h')
y_data = [7,9,11,14,8,15,22,11,10,11,11,13,8]

fig = plt.figure()
ax = fig.add_axes((0.0,0.0,1.0,1.0))
ax.plot(x_date,y_data,'->',ms=8,mfc="#FF9900")
ax.set_title("深圳市24小时的平均风速")
ax.set_xlabel("时间")
ax.set_ylabel("平均风速(km/h)")


ax.xaxis.set_major_formatter(DateFormatter("%H:%M"))
ax.xaxis.set_major_locator(HourLocator(interval=2))
ax.tick_params(direction='in',length=6,width=2,labelsize=12)
ax.xaxis.set_tick_params(rotation=45)
```

![image-20250428173137963](https://db.xinghai.ink/Typora/17458326999429324.png)



## 6.4   隐藏轴脊



<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import matplotlib.patches as mpathes
polygon = mpathes.RegularPolygon((0.5,0.5),6,radius=0.2,color='g')
ax = plt.axes((0.3,0.3,0.5,0.5))
ax.add_patch(polygon)
ax.axis(False)
plt.show()
```

![image-20250428174140339](https://db.xinghai.ink/Typora/17458333022351987.png)





`matplotlib`只需要访问`spines`熟悉获取轴脊，然后使用`set_color()`方法将颜色改成`None`即可

<h3>示例</h3>

```python]
import matplotlib.pyplot as plt
import matplotlib.patches as mpathes
polygon = mpathes.RegularPolygon((0.5,0.5),6,radius=0.2,color='g')
ax = plt.axes((0.3,0.3,0.5,0.5))
ax.add_patch(polygon)

ax.spines['top'].set_color('None')
ax.spines['left'].set_color('None')
ax.spines['right'].set_color('None')
ax.yaxis.set_ticks_position('none')
ax.set_yticklabels([])

plt.show()
```

![image-20250428174517831](https://db.xinghai.ink/Typora/17458335197060444.png)

<h3>实例 二</h3>

```python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.dates import DateFormatter, HourLocator

plt.rcParams['font.family'] = 'SimHei'
x_date = pd.date_range("2019-10-24","2019-10-25",freq='2h')
y_data = [7,9,11,14,8,15,22,11,10,11,11,13,8]

fig = plt.figure()
ax = fig.add_axes((0.0,0.0,1.0,1.0))
ax.plot(x_date,y_data,'->',ms=8,mfc="#FF9900")
ax.set_title("深圳市24小时的平均风速")
ax.set_xlabel("时间")
ax.set_ylabel("平均风速(km/h)")


ax.xaxis.set_major_formatter(DateFormatter("%H:%M"))
ax.xaxis.set_major_locator(HourLocator(interval=2))
ax.tick_params(direction='in',length=6,width=2,labelsize=12)
ax.xaxis.set_tick_params(rotation=45)
ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')
plt.show()
```

![image-20250428174707130](https://db.xinghai.ink/Typora/1745833628887215.png)

## 6.5    移动轴脊

`Spine`类中提供了一个设置轴脊位置的`set_position()`方法，该方法的构造函数如下

```python
set_position(self,position)
```



<h3>示例</h3>

```python
import matplotlib.pyplot as plt
import matplotlib.patches as mpathes
polygon = mpathes.RegularPolygon((0.5,0.5),6,radius=0.2,color='y')
ax = plt.axes((0.3,0.3,0.5,0.5))
ax.add_patch(polygon)

ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')

ax.spines['left'].set_position(('data',0.5))
ax.spines['bottom'].set_position(('data',0.5))
plt.show()
```

![image-20250428175315502](https://db.xinghai.ink/Typora/17458339973824642.png)



<h3>实例 三</h3>

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.family'] = 'SimHei'
plt.rcParams['axes.unicode_minus'] = False
x_data = np.linspace(-2 * np.pi, 2 * np.pi,100)
sin = np.sin(x_data)
cos = np.cos(x_data)

fig = plt.figure()
ax = fig.add_axes((0.2,0.2,0.7,0.7))
ax.plot(x_data,sin,label='正弦曲线')
ax.plot(x_data,cos,label='余弦曲线')
ax.legend()
ax.set_xlim(-2*np.pi,2*np.pi)
ax.set_xticks(
    [-2*np.pi,-3 * np.pi/2,-1*np.pi,-1*np.pi/2,0,np.pi/2,np.pi,3*np.pi/2,np.pi*2],
    ["$-2\pi$","$-3\pi/2$","$-\pi$","$-\pi/2$","$0$","$\pi/2$","$\pi$","$3\pi/2$","$2\pi$"]
    )
ax.set_yticks([-1.0,-0.5,0.0,0.5,1])

ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
ax.spines['left'].set_position(("data",0))
ax.spines['bottom'].set_position(("data",0))
plt.show()
```

![image-20250428182529853](https://db.xinghai.ink/Typora/17458359316435883.png)



## 6.6 习题

### 五、编程题
已知某股票一周内收盘价如表6 - 7所示。

| 周日期 | 收盘价（单位：元） |
| ------ | ------------------ |
| 周一   | 44.98              |
| 周二   | 45.02              |
| 周三   | 44.32              |
| 周四   | 41.05              |
| 周五   | 42.08              |
| 周六   | —                  |
| 周日   | —                  |

根据表6 - 7的数据绘制一个折线图，具体要求如下。
（1）在距画布顶部0.2、左侧0.2的位置上添加一个宽度为0.5、高度为0.5的绘图区域。
（2）x轴的刻度标签为周日期。 
（3）刻度线样式调整：方向朝内，宽度为2。 
（4）隐藏坐标轴的上轴脊、右轴脊。 



```python
import matplotlib.pyplot as plt

x = ['周一','周二','周三','周四','周五']
y = [44.98,45.02,44.32,41.05,42.08]

fig = plt.figure()
ax = fig.add_axes((0.2,0.2,0.5,0.5))
ax.plot(x,y)

ax.set_xlim(-0.5,6)
ax.set_xticks([0,1,2,3,4,5,6],['周一','周二','周三','周四','周五','周六','周日'])
ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')
ax.tick_params(direction='in',width=2)

plt.show()
```

![image-20250428183848533](https://db.xinghai.ink/Typora/1745836730572837.png)






# 第七章

3d图形不想学，略。。。。





# 第八章



# 第九章



# 总结



<div style="color:#e96900;float:right;"><sub style="background-color:#f8f8f8;font-weight:600;">2025年01月18日</sub></div>

