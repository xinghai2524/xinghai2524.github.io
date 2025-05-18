# 农业项目

# 一    使用飞桨训练yolo11模型

<div style="position: relative; padding-bottom: 56.25%;"><iframe src="https://assets.xinghai.ink/#/videos/1741713152351792/1741713152351792.m3u8" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" frameborder="0" allowfullscreen></iframe></div>



## 1.1    环境配置

**打开浏览器，搜索飞桨**

> ![image-20250310134043152](https://db.xinghai.ink/Typora/1741585247738357.png)
>

**进入飞浆官网，点击项目**

> ![image-20250310134217710](https://db.xinghai.ink/Typora/17415853398377173.png)
>

**选择新建项目**

> ![image-20250310134253997](https://db.xinghai.ink/Typora/17415853766043608.png)
>

选择VSCode

> ![image-20250310134329109](https://db.xinghai.ink/Typora/1741585411398137.png)
>

**接着启动环境**

> ![image-20250310134405260](https://db.xinghai.ink/Typora/17417135098322375.png)

**进入项目**

> ![image-20250311141919848](https://db.xinghai.ink/Typora/1741673964862848.png)

进入之后，在左侧新建一个python文件

> ![image-20250311143223733](https://db.xinghai.ink/Typora/17416747524307811.png)

右键，打开终端

![image-20250311143827084](https://db.xinghai.ink/Typora/17416751097632186.png)

在终端中，使用`pip`下载`ultralytics `

```shell
pip install ultralytics 
```

> ![image-20250311144440741](https://db.xinghai.ink/Typora/17416754830093026.png)

## 1.2    配置YOYO

下载`ultralytics`之后，首先打开YOLO[官网](https://docs.ultralytics.com/modes/train/)

![image-20250311222820203](https://db.xinghai.ink/Typora/1741703305580711.png)

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # load a pretrained model (recommended for training)

# Train the model with 2 GPUs
results = model.train(data="coco8.yaml", epochs=100, imgsz=640, device=[0, 1])
```

复制到Vscode中，将`device`修改成`cpu`，

![image-20250311230220549](https://db.xinghai.ink/Typora/17417053604089417.png)

## 1.3    配置数据集

在工作目录下，使用`wget`命令下载https://db.xinghai.ink/download/agriculture-datasets.tar.gz数据集

```shell
wget https://db.xinghai.ink/download/agriculture-datasets.tar.gz
```

![image-20250311230843941](https://db.xinghai.ink/Typora/1741705727639212.png)

下载好数据集后，使用`tar`命令给数据集进行解压

```shell
tar -zxvf agriculture-datasets.tar.gz
```

解压好后，会得到一个文件夹

![image-20250311231223813](https://db.xinghai.ink/Typora/174170594725083.png)

现在，数据集和yolo都基本配置成功了，为了让yolo能够知道数据集所在的位置，还需要配置一个`yaml`文件,也就是`train`方法里面哪个`coco8.yaml`文件

打开yolo官网,这框起来的就是这个文件的所有内容了，可以在工作目录创建一个`coco8.yaml`文件，然后将下面的内容复制过去

![image-20250311232126104](https://db.xinghai.ink/Typora/17417064891870286.png)

关于配置文件的详解

```yaml

path: ./ # dataset root dir
train: images/train # train images (relative to 'path') 4 images
val: images/test # val images (relative to 'path') 4 images

# Classes
names:
  0: Apple Scab Leaf
  1: Apple leaf
  2: Apple rust leaf
  3: Bell_pepper leaf spot
  4: Bell_pepper leaf
  5: Blueberry leaf
  6: Cherry leaf
  7: Corn Gray leaf spot
  8: Corn leaf blight
  9: Corn rust leaf
  10: Peach leaf
  11: Potato leaf early blight
  12: Potato leaf late blight
  13: Potato leaf
  14: Raspberry leaf
  15: Soyabean leaf
  16: Soybean leaf
  17: Squash Powdery mildew leaf
  18: Strawberry leaf
  19: Tomato Early blight leaf
  20: Tomato Septoria leaf spot
  21: Tomato leaf bacterial spot
  22: Tomato leaf late blight
  23: Tomato leaf mosaic virus
  24: Tomato leaf yellow virus
  25: Tomato leaf
  26: Tomato mold leaf
  27: Tomato two spotted spider mites leaf
  28: grape leaf black rot
  29: grape leaf
```

- path 表示数据集的文件夹所在的路径，但是路径下的数据集文件夹名称必须为`datasets`，
- train 表示在数据集中，训练集图片的路径
- test 表示在数据集中，测试集图片的路径
- names表示图片中的类别标签中，各个数字对应的类别名称

我这里是创建了一个文件，然后将上面的内容复制了过去，记得要复制上面的内容，都是配置好的

![image-20250311232645275](https://db.xinghai.ink/Typora/1741706808243809.png)

返回`tain.py`文件,需要将配置文件了路径改成`绝对路径`,像这样

![image-20250311232927059](https://db.xinghai.ink/Typora/17417069695112383.png)

然后将数据集的名称改成`datasets`

![image-20250311234355684](https://db.xinghai.ink/Typora/1741707837642602.png)

这样，就全部配置成功了

## 1.4    额外配置

这样直接运行也可以，但是会发现，由于没有yolo11n.pt这个预训练模型而需要下载，这个时候，可以直接用`wget`，将https://db.xinghai.ink/db/yolo11n.pt，下载下来，然后指定绝对路径

```shell
wget https://db.xinghai.ink/db/yolo11n.pt
```

![image-20250311234018061](https://db.xinghai.ink/Typora/17417076227376955.png)

然后指定绝对路径

![image-20250311234056857](https://db.xinghai.ink/Typora/17417076605035748.png)

还有一个就是字体，默认没有`Arial.ttf`字体，所以会自动下载，会下载到`~/.config/Ultralytics/Arial.ttf`下，这里使用`wget`命令直接下载到这个目录

切换到这个目录

```shell
cd ~/.config/Ultralytics
```

然后下载

```
wget https://db.xinghai.ink/public/Arial.ttf
```

![image-20250311235551266](https://db.xinghai.ink/Typora/17417085533008769.png)

## 1.5    运行

然后直接运行`train.py` 文件就行

![image-20250311235832095](https://db.xinghai.ink/Typora/1741708714612268.png)

运行的结果会在`runs`文件夹里面

![image-20250311235904955](https://db.xinghai.ink/Typora/17417087475604832.png)
