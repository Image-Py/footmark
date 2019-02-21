# Cell Analysis Demo

This is a cell analysis demo using ImagePy. Here is the demo image, we try to extract the cells, and find the connected pairs, and the cells with granules.

![newdoc01](http://idoc.imagepy.org/cell/cell.jpg)

## 1. Open Image

`File > Open`, open your image, or the demo image.

![newdoc01](http://idoc.imagepy.org/cell/01.png)

## 2. Get gray image

`Image > Duplicate`, `Image > Type > 8-bit`, duplicate the original image, rename as cell-gray, and convert to 8-bit gray.

![newdoc01](http://idoc.imagepy.org/cell/02.png)

## 3. Threshold

`Image > Adjust > Threshold` adjust the low threshold to got the cells.

![newdoc01](http://idoc.imagepy.org/cell/03.png)

## 4. Fill holes

`Process > Binary > Fill Holes` fill the inner holes

![newdoc01](http://idoc.imagepy.org/cell/04.png)

## 5. Remove small fragment

`Analysis > Region Analysis > Geometry Filter` we can use the region's properties to filter them, the regions pass the filter would be rendered by front color, others by back color. 'Pass' means pass all the filters, and negative means want the lesser one.

![newdoc01](http://idoc.imagepy.org/cell/05.png)

## 6. Segment the connected pair

`Process > Binary > Binary Watershed`, Use binary watershed to segment the connected cells.

![newdoc01](http://idoc.imagepy.org/cell/06.png)

## 7. Filter the connected cells

`Analysis > Region Analysis > Geometry Filter`, here we select the regions whose eccentricity greater than 1.5. We use 8-connect to ignore the thin segment line. (it is connected in 8-connect)

![newdoc01](http://idoc.imagepy.org/cell/07.png)

## 8. Region Properties

`Analysis > Region Analysis > Geometry Analysis`, here we use 4-connect to calculate every cell's properties.

![newdoc01](http://idoc.imagepy.org/cell/08.png)

## 9. Intensity Analysis

`Analysis > Region Analysis > Intensity Analysis`, the mask only has geometry information, if we want calculate some pixels information, we must calculate with the mask and gray image. **so we need active the mask image, run the intensity analysis, and select the gray image in the parameter dialog.** Here we calculate every region's mass center, mean value, pixels standard, and so on.

![newdoc01](http://idoc.imagepy.org/cell/09.png)

## 10. Find the cell with granules

`Analysis > Region Analysis > Intensity Filter`, like Geometry Filter, We can also filter regions by intensity properties. Here we filter the region with great std, then we get the cells with granules.

![newdoc01](http://idoc.imagepy.org/cell/10.png)

## 11. Lay out images

we can drag and drop images to layout them.

![newdoc01](http://idoc.imagepy.org/cell/11.png)

## 12. Table Statistic

`Table > Statistic > Table Statistic`, we can select some columns by mouse, here the ID is meaningless, then statistic every column.

![newdoc01](http://idoc.imagepy.org/cell/12.png)

## 13. Group Statistic

`Table > Statistic > Group Statistic`, If we import many image as a sequence, we do the geometry and intensity analysis will get a table with a field called **SliceID**. We can use group statistic, and group by **SliceID**, we can got a summarize table.

![newdoc01](http://idoc.imagepy.org/cell/13.png)

## 14. Chart

`Table > Chart > Scatter Chart`, We can draw many chart from table, plot, pie, bar, area and so on. Here we draw a Scatter Chart, select the X,Y Data, If not set the radius column, the size would be radius, If we select a column as radius, the size would be a scale factor for radius columns, If the color column is not set, all circle would be in the color. If the color column is set, the color map would apply for the color column. Here we use area for color column.

![newdoc01](http://idoc.imagepy.org/cell/14.png)

## 15. Generate report

Report is an Excel template, with some note in specific cells. Rename the *.xlsx as *.rpt, then drag and drop on ImagePy's status box (bottom), ImagePy would parse the cell to an dialog, please set the image and table to the right cell mark, then ImagePy will Fill image and table in the marked cell! You can get this [demo template here](https://github.com/Image-Py/IBook/blob/master/menus/IBook/Chapter7%20Binary-Image/Show%20Cell%20Report.rpt). And more about how to build a template please read the [report document](https://github.com/Image-Py/demoplugin/blob/master/doc/report.md).

![newdoc01](http://idoc.imagepy.org/cell/15.png)

We need edit the grid in Excel. We can also add some excel's formula or chart, Then we can print it, or convert it to PDF document.

![newdoc01](http://idoc.imagepy.org/cell/16.png)

## 16. Macros Recorder

`Window > Develop Tool Suit`, We can record all the operation as a macros, then drag and drop on ImagePy's status box below. The command in the macros would run one by one. More about macros please read [the macros document](https://github.com/Image-Py/demoplugin/blob/master/doc/macros.md).

![newdoc01](http://idoc.imagepy.org/cell/17.png)

## 17. Workflow

Add some note to macros, it becomes a work flow. Just read the hint, and click from left to right, everything will be OK! About how to make a workflow, please read [workflow document](https://github.com/Image-Py/demoplugin/blob/master/doc/workflow.md).

![newdoc01](http://idoc.imagepy.org/cell/18.png)

## More Demos

This demo (code, image, macros, workflow and report template) is available in ImagePy's [IBook Plugin](https://github.com/Image-Py/IBook), (`IBook > Chapter 7 > Show Cell ...`) you can use `menu: Plugins > Install > Install Plugins`, then paste `https://github.com/Image-Py/IBook`  to install. Or use the `Plugins > Manager > Plugins Manager` to install (Maybe you need update software first, git pull, or `Plugins > Update Software` for nonprogramers). There are many other demos like this.

![newdoc01](http://idoc.imagepy.org/demoplugin/06.png)