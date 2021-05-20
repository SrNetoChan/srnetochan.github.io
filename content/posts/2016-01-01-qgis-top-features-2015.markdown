---

date: 2016-01-01 16:16:24+00:00
title: QGIS Top Features 2015
tags:
- QGIS
---

EN | [PT](https://sigsemgrilhetas.wordpress.com/2016/01/02/top-novas-funcionalidades-do-qgis-em-2015/)

With the release of the first long term release (2.8 LTR), and two other stable versions (2.10 and 2.12), **2015 was a great (and busy) year for the QGIS community**, with lots of improvements and new features landing on QGIS source code.

As a balance, I have [asked](https://senhorneto.typeform.com/to/ibwVQz) users to choose wich were their favorite new features during 2015 (from the [visual changelogs](https://www.qgis.org/en/site/forusers/visualchangelogs.html) list). As a result I got the following **Top 5 features list**.

<!-- more -->


## 5 - Python console improvements (2.8)


Since QGIS 2.8, we can drag and drop python scripts into QGIS window and they will be executed automatically. There is also a new a toolbar icon in the plugins toolbar and a shortcut ( `Ctrl-Alt-P`) for quick access to the python console.


![](https://www.qgis.org/en/_images/03be8f30ce341816bd3bcd1a58f3b913ddcea07c.png)





## 4 - Processing new algorithms (2.8)


Also in QGIS 2.8, there were introduced some new algorithms to the processing framework. If you are into spatial analysis this must have done your day (or year).



	  * **Regular points** algorithm
	  * **Symmetrical difference** algorithm
	  * **Vector split** algorithm
	  * **Vector grid** algorithm
	  * **Hypsometric curves** calculation algorithm
	  * **Split lines with lines**
	  * **Refactor fields** attributes manipulation algorithm



![](https://www.qgis.org/en/_images/b2403fae20cd24cfb1883d24e97de6fc51e40c88.png)





## 3 - Show rule-based renderer’s legend as a tree (2.8)


There were introduced a few nice improvements to QGIS legend. Version 2.8 brought us a tree presentation for the rule-based renderer. Better still, each node in the tree can be toggled on/off individually providing for great flexibility in which sublayers get rendered in your map.

![](https://www.qgis.org/en/_images/0d39448aa0893d7a71c5241aa2181750535e62c3.png)



## 2 - Advanced digitizing tools (2.8)


If you ever wished you could digitize lines exactly parallel or at right angles, lock lines to specific angles and so on in QGIS? Since QGIS 2.8 you can! The advanced digitizing tools are a port of the CADinput plugin and adds a new panel to QGIS. The panel becomes active when capturing new geometries or geometry parts.


![Untitled](https://gisunchained.files.wordpress.com/2016/01/untitled.png)





## 1 - Rule-based labeling (2.12)


This was a very awaited feature (at least by me), and it was voted by the majority of users. Since 2.12, you can style features labels using rules. This gives us even more control over placement and styling of labels. Just like the rule based cartographic rendering, label rules can be nested to allow for extremely flexible styling options. For example, you can render labels differently based on the size of the feature they will be rendered into (as illustrated in the screenshot).

![image25](https://www.qgis.org/en/_images/8846f57f0395e7f6b2543a92a5c55b67e8b19923.png)


There were other new features that also made the delight of many users. For example, the Improved/consistent projection selection (2.8), PostGIS provider improvements (2.12), Geometry Checker and Geometry Snapper plugins (2.12), and Multiple styles per layer (2.8).

Don't agree with this list? You can still [cast your votes](https://senhorneto.typeform.com/to/ibwVQz). You can also check the complete results in [here](https://senhorneto.typeform.com/report/ibwVQz/XJgm).

Obviously, this list means nothing at all. I was a mere exercise as with such a diverse QGIS crowd it would be impossible to build a list that would fit us all. Besides, there were many great enhancements, introduced during 2015, that might have fallen under the radar for most users. Check the [visual changelogs](https://www.qgis.org/en/site/forusers/visualchangelogs.html) for a full list of new features.


On my behalf, to all developers, sponsors and general QGIS contributors,





### THANK YOU VERY MUCH FOR YOUR TREMENDOUS WORK!




### I wish you a fantastic (and productive) 2016.
