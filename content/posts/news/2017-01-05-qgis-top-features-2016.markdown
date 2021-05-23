---

date: 2017-01-05 01:51:21+00:00
title: QGIS Top Features 2016
tags:
- QGIS
---

A year ago I have asked QGIS's community what were their favourite QGIS new features from 2015 and published [this blog post](https://gisunchained.wordpress.com/2016/01/01/qgis-top-features-2015/). This year I decided to ask it again. In 2016, we add the release of the second long-term release (2.14 LTR), and two other stable versions (2.16 and 2.18).

**2016 was again very productive year for the QGIS community**, with lots of improvements and new features landing on QGIS source code, not to speak of all the work already in place for QGIS 3. This is a great assurance of the project's vitality.

As a balance, I have [asked](https://senhorneto.typeform.com/to/iEeJye) users to choose wich were their favorite new features during 2016 (from the [visual changelogs](https://www.qgis.org/en/site/forusers/visualchangelogs.html) list). As a result, I got the following **Top 5 features list**.


## 5 – Paste a style to multiple selected layers or to all layers in a legend group (2.14)


This is a productivity functionaly that I just realized that existed now, with so many people voting on it. If copy/paste styles was, in my opinion, a killer feature, being able to use it in multiple layers or even a group is just great.

![screenshot-from-2017-01-05-00-25-39](https://gisunchained.files.wordpress.com/2017/01/screenshot-from-2017-01-05-00-25-39.png)






## 4 – fTools plugin has been replaced with Processing algorithms (2.16)


While checking the Vector Menu, the tools seem the same as previous version, but it's when you open them that you understand the difference. All vector tools, provided until now by the fTools core plugin, were replaced by equivalent processing Algoritms. For the users it means easier access to more functionality, like running the tools in batch mode, or getting outputs as temporary layers. Besides some of the tools have been improved.

![screenshot-from-2017-01-05-00-54-17](https://gisunchained.files.wordpress.com/2017/01/screenshot-from-2017-01-05-00-54-17.png)





## 3 – Virtual layers (2.14)


This is definitly one of my favourite new features, and it seems I'm not alone. With virtual layers you can run SQL queries using the layers loaded in the project, even when the layers are not stored in a relational database. We are not talking about WHERE statments to filter data, with this you can do real SQL queries, with spatial analysis, aggregations, and so on. Besides, virtual layers will act as VIEWs and any changes to any of the input layers will automatically update the layer.

![Screenshot from 2017-01-05 01-12-10.png](https://gisunchained.files.wordpress.com/2017/01/screenshot-from-2017-01-05-01-12-10.png)



## 2 – Speed and memory improvements (2.14)


It's no surprise that speed and memory improvements we one of the most voted features. Lots of improvements were made for loading and managing large datasets, and this have a tremendous impact in all users. According to the changelog, zoom is faster, selecting features is faster, updating attributes on selected features is faster, and it consumes less memory. So don't be afraid to put QGIS to the test.


## 1 – Trace digitising tool (2.14)


If you do lots of digitising, you better look into this new feaure that landed on QGIS 2.14. It allows you to digitize new feature by using other layers boundaries. Besides the quality improvement of layers topology, this can make digitizing almost feel pleasing and fast! Just click the first point, move your mouse around other features edged to pick up more vertex.

![screenshot-from-2017-01-05-01-42-33](https://gisunchained.files.wordpress.com/2017/01/screenshot-from-2017-01-05-01-42-33.png)




There were other new features that also made the delight of many users. For example, several improvements on the labeling, Georeference outputs (eg PDF) from composer (2.16), Filter legend by expression (2.14), 2.5D Renderer. Personally, the Style docker made my day/year. But you can check the [full results of the survey](https://senhorneto.typeform.com/report/iEeJye/XC7D), if you like.

Obviously, this list means nothing at all. All new features were of tremendous value, and will be useful for thousands (yes thousands) of people. It was a mere exercise as, with such a diverse QGIS crowd, it would be impossible to build a list that would fit us all. Besides, there were many great enhancements, introduced during 2016, that might have fallen under the radar for most users. Check the [visual changelogs](https://www.qgis.org/en/site/forusers/visualchangelogs.html) for a full list of new features.


On my behalf, to all developers, sponsors, and general QGIS contributors, once again





### THANK YOU VERY MUCH FOR YOUR TREMENDOUS WORK!




### I wish you a fantastic 2017.
