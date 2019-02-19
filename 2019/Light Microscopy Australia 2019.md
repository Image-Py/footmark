# Light Microscopy Australia 2019

## Abstract

[ImagePy](https://github.com/Image-Py/imagepy) is an open source image processing framework written in Python. Its UI interface, image data structure and table data structure are wxpython-based, Numpy-based and pandas-based respectively. Furthermore, it supports any plug-in based on Numpy and pandas, which can talk easily between scipy.ndimage, scikit-image, simpleitk, opencv and other image processing libraries.

![newdoc01](http://idoc.imagepy.org/imgs/newdoc01.png)

<div align=center>Overview, mouse measurement, geometric transformation, filtering, segmentation, counting, etc.</div><br>

## Article 

[ImagePy: an open-source, Python-based and platform-independent software package for bioimage analysis](https://academic.oup.com/bioinformatics/article/34/18/3238/4989871)



## ImagePy: 

1. has a user-friendly interface 
2. can IO a variety of image formats 
3. supports ROI settings, drawing, measurement and other mouse operations  
4. can perform image filtering, morphological operations and other routine operations. 

5. can perform image segmentation, area counting, geometric measurement and density analysis. 
6. is able to perform data selection, filtering, statistical analysis and other operations related to the parameters extracted from the image.  

**More importantly, ImagePy is not just a UI software, it's a pluggable framwork that allows extensibility.**



## Motivation & Goal

### Open Source 

Python is a simple, elegant, powerful language, and has very rich third-party libraries for scientific computing. Numpy-based libraries such as scipy, scikit-image, scikit-learn and other scientific computing libraries have brought great convenience to scientific research. What more, these libraries are all open-source program, all programmers share, use and build them together. But I think **it is a large waste that only programmers share these!** So ImagePy devotes to building a light tool, which can wrap Numpy-based algorithm to build friendly tools easily. Then more users, even non-programmer can benefit from Python and Numpy-based libraries.

### Developer Friendly

ImagePy can interact with Numpy and pandas directly. This means all Numpy-based image processing packages such as scipy.ndimage, opencv-python, scikit-image, can all be effortlessly been integrated in ImagePy. Many functionalities can be implemented within less then ten lines of code. One can take [classical filters](https://github.com/Image-Py/imagepy/blob/master/imagepy/menus/Process/Filters/classic_plgs.py) as an example

### Pure Connector

ImagePy is not a algorithm libaries, doesn't contain any algorithms, and we are extremly against putting the algorithms into plugin, All algorithms should be problem specific, that only depends on common data structures such as Numpy or Pandas, but not ImagePy. ImagePy should and will only provide the interactive environment for algorithms. ImagePy supports a json style macros, but only aims to link functionalities, not to perform other logical operations. And ImagePy does not support `headless`, because we think, python and Numpy are convenient enough!

### Salute ImageJ

ImagePy is largely inspired by ImageJ, including its name, its UI style, its functionalities and the software design. More specifically, the way of loading and creating the menu, toolkit bar and parameter dialog. And there is a **IJ Style UI**, you can use `Windows > Windows Style` to switch.

![newdoc02](http://idoc.imagepy.org/imgs/newdoc02.png)

<div align=center>`Windows > Windows Style` can switch to ImageJ style</div><br>



**More specifically: **

ImagePy doesn't contain any algorithms. Further more, we are extremly against putting the algorithms into plugin. All algorithms should be problem specific, that only depends on common data structures such as Numpy or Pandas, but not ImagePy. ImagePy should and will only provide the interactive environment for algorithms.

The macro and headless mode from ImageJ have provided great extensibility of ImageJ. However, as a connector, ImagePy doesn't support these functionalities. The macro of ImagePy is standarized on json and only aims to link functionalities, but not to perform other logical operations. As for headless mode, ImagePy does not support it at all. Part of the reason has been previously explained. ImagePy only ensures the interactive exploration of image data. However, in headless mode, the interaction is meaningless. From our perspective, one algorithm should be pure and no UI dependancy should be involved. Therefore, we think one should write real Python code when needed, such as for batch processing, which is not much harder than writing macros or using headless mode. As a benefit of doing this, one can have total control of every detail of its pipeline.


## Demostrations 

ImagePy as an image processing framework, mostly provides basic operations. Some more advanced projects have been previously conducted with different universities and research institues, such as the capturing of vibrating liquid surface using Unet on images from high-frequency camera; the description complexe geometrical parameters of cell contours _etc._.  However, for some reason, the data or the code of these projects can not be open sourced. In this part, we choose to use some examples from the [Sea Ice RS Image Analysis](https://github.com/Image-Py/seaice) project for demostration.

**High-res image segmentation**

Operations such as, filtering, gradiant extraction, local maxima, watersheding, area analysis, gray level analysis and clustering are performed to classify ice and water, the ice are futher fragmented.

![](http://idoc.imagepy.org/ice/30.gif)

<div align=center>High-res image segmentation</div><br>

**Interactive ice edge extraction with low-res images**

The `GrabCut` is implemented to perform interactive segmentation. Undo and re-calculation of the segmentation mask is supported if the result is unsatisfied.

![](http://idoc.imagepy.org/ice/7.png)

<div align=center>Interactive ice/water segmentation</div><br>

**Alignment with geological information and ice growth area analysis**

Align images with geological coordinates saved in tif files. Then combine it with ice area extraction described above to overlay multiple timepoints in order to evaluate ice area growth. 

![](http://idoc.imagepy.org/ice/21.png)

<div align=center>Multiple timepoint overlay and ice growth analysis</div><br>

**Water flow speed estimation with RADAR images**

Use ORB descriptor to extract features from every image. The transformation matrix are calculated from each timepoint, then the flow speed roration speed can be estimated from the consecutive time-serie images.

![](http://idoc.imagepy.org/ice/36.gif)

<div align=center>Water flow speed estimation with RADAR images</div><br>

## Future plans

**Better support for Machine learning：** Machine learning has been heated up recently and will be largely deployed in image processing domain. ImagePy wants to build a more friendly environment for machine learning users, including image tagging, model selection, parameter setting, training, cost function report, prediction _etc._ Since most of the machine learning packages are powered by Numpy, we think the implementation is quite foreseeable. An advantage of ImagePy is that it has already several functionalities in place such as image, mouse interaction, charts and tables. The only missing part is model parameter setting. We will start with [DeepLabCut](https://github.com/AlexEMG/DeepLabCut) and [ilastik](https://github.com/ilastik/ilastik).

**Microscope control：** We are planning to intergrate a microscope control part into ImagePy. This will shorten the image analysis pipeline that are made of data collection, hardware tuning, software analysis. The well-known [MicroManager](https://github.com/micro-manager/micro-manager), was on top of our list. However, it is written in C, wrapped by Java, and does not provide a high-level API for Python. We have no idea whether there is other implementation, or the microscope manufacture are trying to build a standard such as Direct Show.

**Web-based ImagePy：** [bokeh](https://bokeh.pydata.org/en/latest/) shall be used for all displays, that in turn allows web-based image processing. But the large amount of work and the lack of javascript skill in the team holds us back. Fortunately, wxpython provides already what we need, except the installation under Linux may needs some trouble shooting.



## Contributions

**Documentation writing**

Write plugin documentations for ImagePy, so that users can see it while using it, more details can be found [here](https://github.com/Image-Py/demoplugin/blob/master/doc/document.md)

![14](http://idoc.imagepy.org/demoplugin/31.png)

<div align=center>view doc from plugin tree view</div><br>

**Plugin development**

If you want your algorithm to be a part of ImagePy, this is [the demo](https://github.com/Image-Py/demoplugin) to start with. Inside this demo, diffrent kind of plugins and their functions are introduced. Once compiled, it can either be installed using Github address or be published in ImagePy, so that it can also been installed via plugin manager.

![06](http://idoc.imagepy.org/demoplugin/06.png)

<div align=center>Plugins Manager</div><br>

**Framework improvement**

ImagePy as a connector, focus on making better interactive environment for algorithms. If any other feature that you think is useful, please address issues on Github to ensure that it's really needed and suitable in ImagePy. Once confirmed and the plugin been elegantly written, all PRs are welcomed. 


## Community 

ImagePy and [image.sc](https://forum.image.sc/) are partners. Any issues concerning ImagePy can be discussed on this forum.
