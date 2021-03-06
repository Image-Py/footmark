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

ImagePy is not a algorithm libraries,  it doesn't contain any algorithms, and we are extremely against putting the algorithms into plugin, All algorithms should be problem specific, that only depends on common data structures such as Numpy or Pandas, but not ImagePy. ImagePy should and will only provide the interactive environment for algorithms. ImagePy supports a json style macros, but only aims at link functionalities, not to perform other logical operations. And ImagePy does not support `headless`, because we think, python and Numpy are convenient enough!

### Salute ImageJ

ImagePy,including its name,UI style,functionalities and the software design, is largely inspired by ImageJ. More specifically, it is the way of loading and creating the menu, toolkit bar and parameter dialog. And there is a **IJ Style UI**, you can use `Windows > Windows Style` to switch.

![newdoc02](http://idoc.imagepy.org/imgs/newdoc02.png)

<div align=center>`Windows > Windows Style` can switch to ImageJ style</div><br>


## Demostrations 

ImagePy as an image processing framework, mostly provides basic operations. Some more advanced projects have been previously conducted with different universities and research institutes, such as the capturing of vibrating liquid surface using Unet on images from high-frequency camera; the description complex geometrical parameters of cell contours _etc._.  However, for some reason, the data or the code of these projects can not be open sourced. In this part, we choose two demos. First one is a simple but classical [Cell Image Segment And Region Analysis](Cell%20Analysis%20Demo.md) for live demo, Second one is [Sea Ice RS Image Analysis](https://github.com/Image-Py/seaice). But the real HD RS data with coordinate can not be open sourced too, so just have a look.

**Cells segment and region analysis**

This is a simple but classical demo, here we use ImagePy to threshold the cells, and segment the connected cells using watershed, then do region analysis, filter the region with eccentricity greater than 1.5 (connected pairs). And statistic the pixels of every region, filter region has standard deviation more than 30 (cells with granules).

![newdoc01](http://idoc.imagepy.org/cell/11.png)

<div align=center>Cells Analysis</div><br>

**Generate Report from excel template**

User can design their Excel template, and add tags in a particular cell and save the template. change the suffix to `rpt`, you can get the report plugin of ImagePy, ImagePy will parse the template to a parameter dialog, we can set image or table, then ImagePy will fill the cell automatically.

![newdoc01](http://idoc.imagepy.org/cell/16.png)

<div align=center>Generate report by fill the result to a excel template</div><br>

**High-res image segmentation**

Operations such as, filtering, gradient extraction, local maximum, watershed, area analysis, gray level analysis and clustering are performed to classify ice and water, the ice are further fragmented.

![](http://idoc.imagepy.org/ice/30.gif)

<div align=center>High-res image segmentation</div><br>

**Interactive ice edge extraction with low-res images**

Use OpenCV's `GrabCut` to perform interactive segmentation. Undo and re-calculation of the segmentation mask is supported if the result is unsatisfied.

![](http://idoc.imagepy.org/ice/7.png)

<div align=center>Interactive ice/water segmentation</div><br>

**Alignment with geological information and ice growth area analysis**

Align images with geological coordinates saved in tif files. Then combine it with ice area extraction described above to overlay multiple time points in order to evaluate ice area growth. 

![](http://idoc.imagepy.org/ice/21.png)

<div align=center>Multiple timepoint overlay and ice growth analysis</div><br>

**Water flow speed estimation with RADAR images**

Use ORB descriptor to extract features from every image. The transformation matrix are calculated from each time point, then the Velocity rate and rotation speed of the flow can be estimated from the consecutive time-series images. We also give a implements with [pystackreg](https://pystackreg.readthedocs.io).

![](http://idoc.imagepy.org/ice/36.gif)

<div align=center>Water flow speed estimation with RADAR images</div><br>

## Future plans

**Better support for Machine learning** Machine learning has been heated up recently and will be largely deployed in image processing domain. ImagePy wants to build a more friendly environment for machine learning users, including image tagging, model selection, parameter setting, training, cost function report, prediction _etc._ Since most of the machine learning packages are powered by Numpy, we think the implementation is quite foreseeable. An advantage of ImagePy is that it has already several functionalities in place such as image, mouse interaction, charts and tables. The only missing part is model parameter setting. We will start with [DeepLabCut](https://github.com/AlexEMG/DeepLabCut) and [ilastik](https://github.com/ilastik/ilastik).

**Microscope control** We are planning to integrate a microscope control part into ImagePy. This will shorten the image analysis pipeline that are made of data collection, hardware tuning, software analysis. The well-known [MicroManager](https://github.com/micro-manager/micro-manager), was on top of our list. However, it is written in C, wrapped by Java, and does not provide a high-level API for Python. We have no idea whether there is other implementation, or the microscope manufacture are trying to build a standard such as Direct Show? Which defines all the interfaces about camera, light, and the motion platform needed, then the implemented in SDK, even give a blank implement if not support.

**Web-based ImagePy** [bokeh](https://bokeh.pydata.org/en/latest/) shall be used for all displays, that in turn allows web-based image processing. But the large amount of work and the lack of javascript skill in the team holds us back. Fortunately, wxpython provides already what we need, except the installation under Linux may needs some trouble shooting.



## Contributions

**Documentation writing**

Write plugin documentations for ImagePy, so that users can see document while using the function, more details can be found [here](https://github.com/Image-Py/demoplugin/blob/master/doc/document.md)

![14](http://idoc.imagepy.org/demoplugin/31.png)

<div align=center>view doc from plugin tree view</div><br>

**Plugin development**

If you want your algorithm to be a part of ImagePy, this is [the demo](https://github.com/Image-Py/demoplugin) to start with. Inside this demo, diffrent kind of plugins and their functions are introduced. Once compiled, it can either be installed using Github address or be published in ImagePy, so that it can also been installed via plugin manager.

![06](http://idoc.imagepy.org/demoplugin/06.png)

<div align=center>Plugins Manager</div><br>

**Framework improvement**

ImagePy as a connector, focus on making better interactive environment for algorithms. If any other feature that you think is useful, please address issues on Github to ensure that it's really needed and suitable in ImagePy. Once confirmed, all PRs are welcomed. 


## Community 

ImagePy is [image.sc](https://forum.image.sc/) 's partner. Any issues concerning ImagePy can be discussed on this forum.