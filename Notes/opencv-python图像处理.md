## opencv-python安装

**（1）Windows 下的安装**

opencv 依赖 numpy，先安装好 numpy。

方法一：直接命令法

试试 pip 或 conda 命令安装 `pip install opencv-python`

方法二：下载 whl 文件安装

到官网 <https://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv>，下载相应 Python 版本的 OpenCV 的 whl 文件。如下子的 opencv_python‑3.4.1‑cp36‑cp36m‑win_amd64.whl，然后在 whl 文件所在目录下，使用命令安装即可：

``` 
pip install opencv_python‑3.4.1‑cp36‑cp36m‑win_amd64.whl
```

测试是否安装成功：

``` python
import cv2
```

运行是否报错。

注意：本人在安装 opencv-python 出现了问题，后来换了其他版本的 opencv 解决了，所以怀疑 Python 版本和 opencv-python 版本需要对应。

本人 Python 版本：3.6.4  opencv-python 版本：3.4.1.15

---



## opencv-python 图像处理

### 图像处理代码随记

（1）设置 500x500x3 图像 的 100x100 区域为蓝色：

``` python
import cv2
import numpy as np

ann_img = np.ones((500,500,3)).astype('uint8')
print(ann_img.shape)
ann_img[:100, :100, 0] = 255 # this would set the label of pixel 3,4 as 1

cv2.imwrite( "ann_1.png" ,ann_img )
# print(ann_img)

cv2.imshow("Image", ann_img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

（2）

``` python
import cv2
import numpy as np

img = cv2.imread("./haha.jpg", cv2.IMREAD_COLOR)
print(img.shape)
print(img)
emptyImage = np.zeros(img.shape, np.uint8)
print(emptyImage)
emptyImage2 = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

cv2.imshow("EmptyImage", emptyImage)
cv2.imshow("Image", img)
cv2.imshow("EmptyImage2", emptyImage2)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

### RGB 转为灰度图像

RGB 彩色图像中，一种彩色由R（红色），G（绿色），B（蓝色）三原色按比例混合而成。

图像的基本单元是一个像素，就像一个巨幅电子广告屏上远处看是衣服图像，走近你会看到一个一个的方格，这个方格的颜色是一种，从远处看，觉察不到这个方格的存在。

一个像素需要 3 块表示，分别代表 R，G，B，如果 8 为表示一个颜色，就由 0-255 区分不同亮度的某种原色。

实际中数都是二进制形式的，并且未必按照R，G，B顺序，比如[OpenCV](http://lib.csdn.net/base/opencv)是按照 B,G,R 顺序将三个色值保存在 3 个连续的字节里。

**灰度图像**是用不同饱和度的黑色来表示每个图像点，比如用8位 0-255数字表示“灰色”程度，每个像素点只需要一个灰度值，8位即可，这样一个3X3的灰度图，只需要9个byte就能保存

RGB值和灰度的转换，实际上是人眼对于彩色的感觉到亮度感觉的转换，这是一个心理学问题，有一个公式：

**Grey = 0.299\*R + 0.587\*G + 0.114\*B**

根据这个公式，依次读取每个像素点的 R，G，B 值，进行计算灰度值（转换为整型数），将灰度值赋值给新图像的相应位置，所有像素点遍历一遍后完成转换。

——from：[RGB图像转为灰度图](https://blog.csdn.net/u010312937/article/details/71305714)





