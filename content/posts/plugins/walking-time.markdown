---

date: 2014-03-25 08:41:42+00:00
title: Walking time
menu:
  sidebar:
    name: Walking time
    identifier: walking-time
    parent: plugins
    weight: 20
hero: /images/posts_hero/walking_time.png
---

The **Walking time** is a QGIS python plugin that uses Tobbler’s hiking function to estimate the travel time along a line depending on the slope.

The input data required are a vector layer with lines and a raster layer with elevation values ​​(1). One can adjust the base velocity (on flat terrain) according to the type of walking or walker. By default, the value used is 5 km h (2). The plugin update or create fields with estimated time in minutes in forward and in reverse direction (3). One can run the plugin for all elements of the vector layer, or only on selected routes (4).

The plugin can also been used to prepare a network (graph) to perform network analysis when the use of travel walking time as cost is intended.

Captura de tela 2014-03-24 12.12.17-01

QGIS repository: http://plugins.qgis.org/plugins/walkingtime/

Code: https://github.com/SrNetoChan/WalkingTime

Bug report: https://github.com/SrNetoChan/WalkingTime/issues

### Instalation

The plugin is available in the oficial QGIS plugins repository. Therefore, just go to **Plugins > Manage and install plugins** and search for “Walking Time”. Since the plugin is experimental, make sure you have the **Show also experimental plugins** option selected in the **Settings** tab.