# Light Microscopy Australia 2019

## 简介

[ImagePy](https://github.com/Image-Py/imagepy) 是基于Python开发的开源图像处理框架，采用wxpython界面基础，基于Numpy为核心图像数据结构，pandas为核心表格数据结构，可以方便的接入scipy.ndimage, scikit-image, simpleitk, opencv等算法库进行插件扩展。

![newdoc01](http://idoc.imagepy.org/imgs/newdoc01.png)

<div align=center>Overview, mouse measurement, geometric transformation, filtering, segmentation, counting, etc.</div><br>

## 论文

[ImagePy: an open-source, Python-based and platform-independent software package for bioimage analysis](https://academic.oup.com/bioinformatics/article/34/18/3238/4989871)



## 功能特性

1. 软件具有友好的用户操作界面
2. 能读取，保存多种图像数据格式
3. 支持ROI设定，绘图，测量等鼠标操作
4. 能完成图像滤波，形态学运算等常规操作
5. 可以很好的完成一些分割，区域计数，几何测量，密度分析相关的工作
6. 可以对分析结果进行数据筛选，过滤，统计，绘图等相关工作

*但更为重要的是 ImagePy 不仅是一个界面应用程序，还是一个插件系统，可以方便的对其进行功能扩展*



## 与ImageJ的异同

ImagePy 从名字，到界面风格，到功能，甚至一些设计思想都很大程度的借鉴了ImageJ。包括插件加载与解析为菜单的方式，工具栏设计，参数对话框生成都与 ImageJ 类似，也同样实现了ROI，宏录制等功能。

![newdoc02](http://idoc.imagepy.org/imgs/newdoc02.png)

<div align=center>'Windows > Windows Style' can switch to ImageJ style</div><br>

**但 ImagePy 并不是一个 Python 版的 ImageJ，它们有如下区别**

1. 开发语言不同，

   语言这是最基本的差别，或许不太严谨的讲，在图像处理领域，Python 比 Java 更具优势。相对于Java，Python更加简单医学，更容易与C/C++混编，在科学计算领域有更丰富的类库。当然 ImageJ2 对 Python 有了不错的支持，但 ImagePy 可以更为直接的操作 Numpy，pandas。这意味着 scipy.ndimage, opencv-python, scikit-image, SimpleITK 等各个基于 Numpy 的图像处理库可以毫无阻力的接入 ImagePy。

2. 开发者友好性

   ImageJ2 相对 ImageJ1 做了相当程度的重构，对UI和功能做了解耦，扩展性大大增强。但开发的复杂性也有所提高。而 ImagePy 开发，在适当的插件模板上进行参数配置，然后操作核心数据结构 (Numpy/Pandas) 即可。ImagePy基础功能中多数的插件代码都在10几行甚至10行以内。[以常用滤波器为例](https://github.com/Image-Py/imagepy/blob/master/imagepy/menus/Process/Filters/classic_plgs.py)

3. 纯粹的连接器

   ImageJ 做的是搭建一个生态系统，imglib为核心，并连接Python，Matlab，OpenCV 等多种语言或工具。而 ImagePy 定位为纯粹的连接器，搭建生态环境是Numpy 的工作，ImagePy 只为 Numpy，Pandas 提供展示及交互环境，连接开发者与终端用户。

   

   这主要体现在：

   * ImagePy 不包含任何算法，也极力反对开发者将算法写入插件，算法只针对问题，只基于Numpy，Pandas等通用数据结构，不依赖 ImagePy，而 ImagePy 单方面的尽可能为算法提供交互环境。

   * ImageJ 自成体系的宏，以及 Headless 模式，提供了很大应用灵活性。但 ImagePy 作为纯粹的连接器，并不支持这些，ImagePy 的宏是标准 json，只起到功能串联的作用，并不能实现其他逻辑。而对于 Headless 则是完全不支持。原因很简单，ImagePy 只提供交互，而交互在 Headless 下交互毫无意义。但只要一切开发以算法为核心，不把算法卷入 ImagePy，个人倾向于，必要时，我们自己动手来写真正的 Python 代码，那并不比写宏或headless复杂多少，并且真正能做到每一个细节都可控。

     

## 应用示例

ImagePy 作为处理框架，提供的多数是基础功能。当然也与高校或科研机构合作过一些系统性应用项目，比如使`Unet网络对高频摄像机下的震荡的液面进行捕获`，`细胞轮廓的复杂几何参数描述` 等，但由于一些原因，这些项目的代码或数据不能够开源，这里选用一个`海冰遥感影像分析`的例子进行展示，由于部分高分影像无法开源，这里只是部分功能。

**高分辨率影像分割** [Github](https://github.com/Image-Py/seaice)

采用滤波，梯度提取，局部极值，分水岭，区域分析，灰度分析，聚类等方法，区分冰与水，并对冰进行分块。

![](http://idoc.imagepy.org/ice/30.gif)

<div align=center>高分辨率影像分割</div><br>

**低分辨率冰缘线交互式提取**

使用 GrabCut 方法，对图像进行交互式分割，如不满意可以撤销操作，并对掩膜进行修补，再次计算。

![](http://idoc.imagepy.org/ice/7.png)

<div align=center>交互式冰与水分割</div><br>

**通过地理参考进行配准，冰区生长对比**

通过 tif 自带的地理坐标系，对图像进行配准，结合上述的提取冰区方法，并对多期进行叠加分析，得到生长情况。

![](http://idoc.imagepy.org/ice/21.png)

<div align=center>多期配准与生长分析</div><br>

**通过雷达影像计算水流速度**

使用ORB描述子对每一张进行特征的提取，并计算每个层间的仿射矩阵，得到连续变换关系，算出流速，转速。

![](http://idoc.imagepy.org/ice/36.gif)

<div align=center>通过雷达影像计算水流</div><br>

## 未来研发计划

**为机器学习提供更好的支持：**机器学习是当下非常热门的学科，以后也会越来越多的应用到各个领域，ImagePy 希望为机器学习打造一个更好的环境，包括图像标记，模型选择，结构参数设定，训练，代价函数的表格与图表，预测等。我想这并不会太复杂，因为目前多数的机器学习库也支持 Numpy，并且储了结构参数设定之外，也无非各种图像，鼠标交互，表格与图表，这些都是 ImagePy 已经具备的。我希望从 [DeepLabCut](https://github.com/AlexEMG/DeepLabCut), [ilastik](https://github.com/ilastik/ilastik) 着手。

**集成显微镜控制：**希望做一个显微镜控制应用，把数据采集，硬件调整，软件分析的过程缩短，关于显微镜，有著名的 [MicroManager](https://github.com/micro-manager/micro-manager)，但它并没有提供一个高级的Python API，不知道是否有其他的实现，或者各个显微镜厂商是否有意愿出一套类似于 Direct Show的通用标准。

**Web 版的 ImagePy：**用 [bokeh](https://bokeh.pydata.org/en/latest/) 做展示，做一套基于Web的应用，但工作量巨大，并且 ROI 编辑等功能对 js 功力要求太高。并且目前看来，wxpython也并没什么不好，除了Linux下安装会遇到些许麻烦。



## 贡献

**为现有功能编写操作手册**

为ImagePy里的功能编写说明，用户可以在使用过程中随时查看，具体请参阅 [操作手册编写](https://github.com/Image-Py/demoplugin/blob/master/doc/document.md)

![14](http://idoc.imagepy.org/demoplugin/31.png)

<div align=center>view doc from plugin tree view</div><br>

**开发插件**

如果你希望将你的算法做成 ImagePy 插件，这里是一个[插件演示项目](https://github.com/Image-Py/demoplugin)，里面讲解了各种插件的作用和编写方法。编写完成后，还可以通过项目的github地址来安装插件，也可以将你的插件发布到ImagePy，即可从插件管理器中安装。

![06](http://idoc.imagepy.org/demoplugin/06.png)

<div align=center>Plugins Manager</div><br>

**完善框架**

ImagePy 作为纯粹的连通器，致力于更好的为算法提供交互环境，如果你觉得有什么新特性需要添加，请在Github 上发 Pull Request。当然在添加新特性之前，最好先发起一个Issue，以确保新特性的确需要，并且以最优雅的方式实现。



## 社区

ImagePy 是 [image.sc](https://forum.image.sc/) 的合作伙伴，任何使用，开发上遇到的问题，可以在上面讨论。