# 街景字符编码识别：
本次项目是datawhale与天池合办的第二场比赛 零基础入门CV赛事- 街景字符编码识别。
竞赛地址：https://tianchi.aliyun.com/competition/entrance/531795/introduction。

## 1.赛题理解
赛题来源自Google街景图像中的门牌号数据集（The Street View House Numbers Dataset, SVHN），并根据一定方式采样得到比赛数据集。训练集数据包括3W张照片，验证集数据包括1W张照片，每张照片包括颜色图像和对应的编码类别和具体位置；为了保证比赛的公平性，测试集A包括4W张照片，测试集B包括4W张照片。

### 字段表
所有的数据（训练集、验证集和测试集）的标注使用JSON格式，并使用文件名进行索引。如果一个文件中包括多个字符，则使用列表将字段进行组合。
Field	Description
top	左上角坐标X
height	字符高度
left	左上角最表Y
width	字符宽度
label	字符编码
注：数据集来源自SVHN，网页链接http://ufldl.stanford.edu/housenumbers/  ，并进行匿名处理和噪音处理，选手使用比赛给定的数据集完成训练。

### 评价标准
评价标准为准确率，选手提交结果与实际图片的编码进行对比，以编码整体识别准确率为评价指标，结果越大越好，具体计算公式如下：
score = 编码识别正确的数量/测试集图片数量

## 2.数据扩增
### 图像读取
图像读取现在比较主流的库主要有Pillow和OpenCV。Pillow是图像处理函式库（PIL)的一个分支。OpenCV在功能上比Pillow更加强大很多，学习成本也高很多。
### 数据扩增
在数据集不够的情况下，数据扩增可以增加训练样本，同时也可以有效缓解模型过拟合现象。使得模型具有更好的泛化能力。
数据扩增的方法有很多，从颜色空间、尺度空间到样本空间，同时根据不同任务数据扩增都有相应的区别。对于图像分类，数据扩增一般不会改变标签。
### 常用数据扩增库
#### torchvision
以torchvison为例，常见的数据扩增方法包括：
transforms.CenterCrop 对图片中心进行剪裁
transforms.ColorJitter 对颜色的对比度、饱和度和零度进行变换
transforms.FiveCrop 对图像四个角和中心进行剪裁得到五分图像
transforms.Grayscale 对图像进行灰度变换
transforms.Pad 使用固定值进行像素填充
transforms.RandomAffine 随机放射变换
transforms.RandomHorizontalFlip 随机水平翻转
transforms.RandomRotation 随机旋转
transforms.RandomVerticalFlip 随机垂直翻转





