# Hog+SVM实现目标检测

- 方向梯度直方图（Histogram of Oriented Gradient，Hog）特征是一种再计算机视觉和图像处理中用来进行`物体检测`的`特征描述子`
- 它通过计算和统计图象局部区域的梯度直方图来构建特征
- Hog特征和SVM分类器已经被广泛应用于图像识别中



## Hog的实现过程

- 灰度化，将图像看作一个xyz的三维图像
- 采用Gamma校正法对输入图像进行颜色空间的标准化（归一化）
- 计算图像的每个像素的梯度（包括大小和方向）
- 将图像划分成小cells，小的单元
- 统计每个cell的梯度直方图，不同梯度的个数，得到cells的描述子
- 将每几个cell组成一个block，得到block的描述子
- 将图像image内的所有block的HOG特征descriptor串联起来，就可以得到HOG特征，该特征向量就是用来目标检测或分来的特征

示例代码

```python
import cv2
import numpy as np

def is_inside(o,i):
	ox, oy, ow, oh = o
	ix, iy, iw, ih = i
	return ox >ix and oy > iy and ox + ow < ix + iw and oy + oh < iy + ih

# 对人体绘制颜色框
def draw_person(image,person):
    x, y, w, h = person
    cv2.rectangle(img, (x, y), (x + w, y + h), (0,255,255), 2)

img = cv2.imread("people.jpg")
hog = cv2.HOGDescriptor() # 启动检测对象
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector()) # 指定检测器为人体
found, w = hog.detectMultiScale(img, 0.1, (1, 1)) # 加载并检测图像
print(found)
print(w)


```

