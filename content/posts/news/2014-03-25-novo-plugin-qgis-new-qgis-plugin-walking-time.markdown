---

date: 2014-03-25 08:41:42+00:00
title: New QGIS plugin - "Walking time"
---

I have finally "finished" my new plugin. I uses some quotation marks, since I believe that there is still space for a few improvement. This plugin arised with the need to calculate the travel time for the Cascais oficial pedestrian routes, and started as a simple python script. I have then decided to create a graphic interface and publish it as a plugin in the hope that someone else finds it useful.


[![icon_large](/images/2014/03/icon_large.png?w=150)
](/images/2014/03/icon_large.png)**Walking time** is a QGIS python plugin that uses [Tobbler's hiking function](https://en.wikipedia.org/wiki/Tobler's_hiking_function) to estimate the travel time along a line depending on the slope.


The input data required are a vector layer with lines and a raster layer with elevation values ​​(1). One can adjust the base velocity (on flat terrain) according to the type of walking or walker. By default, the value used is 5 km h (2). The plugin update or create fields with estimated time in minutes in forward and in reverse direction (3). One can run the plugin for all elements of the vector layer, or only on selected routes (4).

The plugin can also been used to prepare a network ([graph](https://en.wikipedia.org/wiki/Graph_theory)) to perform network analysis when the use of travel walking time as cost is intended.

[![Captura de tela 2014-03-24 12.12.17-01](/images/2014/03/captura-de-tela-2014-03-24-12-12-17-01.png)
](/images/2014/03/captura-de-tela-2014-03-24-12-12-17-01.png)

QGIS repository: [http://plugins.qgis.org/plugins/walkingtime/](http://plugins.qgis.org/plugins/walkingtime/)

Code: [https://github.com/SrNetoChan/WalkingTime](https://github.com/SrNetoChan/WalkingTime)

Bug report:[ https://github.com/SrNetoChan/WalkingTime/issues](https://github.com/SrNetoChan/WalkingTime/issues)
