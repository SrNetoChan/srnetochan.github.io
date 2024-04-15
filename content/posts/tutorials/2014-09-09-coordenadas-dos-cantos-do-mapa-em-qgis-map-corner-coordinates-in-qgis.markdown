---

date: 2014-09-09 23:05:51+00:00
title: Map corner coordinates in QGIS
tags:
- Cartography
- python
- QGIS
- tutorial
---

Some time ago in the [qgis-pt mailing list](http://osgeo-org.1560.x6.nabble.com/QGIS-pt-f5128248.html), someone asked [how to show the coordinates of a map corners using QGIS](http://osgeo-org.1560.x6.nabble.com/QGIS-Layout-coordenadas-nos-4-cantos-do-mapa-tt5140019.html). Since this features wasn't available (yet), I have tried to reach a automatic solution, but without success,  After some thought about it and after reading a [blog post](http://nathanw.net/2012/11/10/user-defined-expression-functions-for-qgis/) by [Nathan Woodrow](http://nathanw.net/aboutme.html), it came to me that the solution could be creating a user defined function for the expression builder to be used in labels in the map.

Closely following the blog post instructions, I have created a file called **userfunctions.py** in the  **.qgis2/python** folder and, with [a help](http://osgeo-org.1560.x6.nabble.com/How-to-get-Composer-s-name-title-using-Python-td5160691.html) from [Nyall Dawson](http://nyalldawson.net/) I wrote the following code.

[code language="Python"]
```
from qgis.utils import qgsfunction, iface
from qgis.core import QGis

@qgsfunction(2,"python")
def map_x_min(values, feature, parent):
 """
 Returns the minimum x coordinate of a map from
 a specific composer.
 """
 composer_title = values[0]
 map_id = values[1]
 composers = iface.activeComposers()
 for composer_view in composers():
  composer_window = composer_view.composerWindow()
  window_title = composer_window.windowTitle()
  if window_title == composer_title:
   composition = composer_view.composition()
   map = composition.getComposerMapById(map_id)
   if map:
    extent = map.currentMapExtent()
    break
 result = extent.xMinimum()
 return result
``` 
[/code]

After running the command **import userfunctions** in the python console  (Plugins > Python Console), it was already possible to use the  **map_x_min()** function (from the python category) in an expression to get the minimum X value of the map.

![Screenshot from 2014-09-09 16^%29^%29](/images/2014/09/screenshot-from-2014-09-09-162929.png?w=584)


All I needed now was to create the other three functions,  **map_x_max()**, **map_y_min()** and** map_y_max()**.  Since part of the code would be repeated, I have decided to put it in a function called **map_bound()**, that would use the print composer title and map id as arguments, and return the map extent (in the form of a QgsRectangle).

[code language="Python"]

from qgis.utils import qgsfunction, iface
from qgis.core import QGis

def map_bounds(composer_title, map_id):
 """
 Returns a rectangle with the bounds of a map
 from a specific composer
 """
 composers = iface.activeComposers()
 for composer_view in composers:
  composer_window = composer_view.composerWindow()
  window_title = composer_window.windowTitle()
  if window_title == composer_title:
   composition = composer_view.composition()
   map = composition.getComposerMapById(map_id)
   if map:
    extent = map.currentMapExtent()
    break
 else:
  extent = None

 return extent
 
 [/code]

With this function available, I could now use it in the other functions to obtain the map X and Y minimum and maximum values, making the code more clear and easy to maintain. I also add some mechanisms to the original code to prevent errors.

[code language="Python"]

@qgsfunction(2,"python")
def map_x_min(values, feature, parent):
 """
 Returns the minimum x coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_x_min(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_x_min('my pretty map', 0) -> -12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.xMinimum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_x_max(values, feature, parent):
 """
 Returns the maximum x coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_x_max(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_x_max('my pretty map', 0) -> 12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.xMaximum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_y_min(values, feature, parent):
 """
 Returns the minimum y coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_y_min(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_y_min('my pretty map', 0) -> -12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.yMinimum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_y_max(values, feature, parent):
 """
 Returns the maximum y coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_y_max(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_y_max('my pretty map', 0) -> 12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.yMaximum()
 else:
  result = None

 return result
 
 [/code]

The functions became available to the expression builder in the "Python" category (could have been any other name) and the functions descriptions are formatted as help texts to provide the user all the information needed to use them.

![Screenshot from 2014-09-09 15^%39^%19](/images/2014/09/screenshot-from-2014-09-09-153919.png?w=584)


Using the created functions, it was now easy to put the corner coordinates in labels near the map corners. Any change to the map extents is reflected in the label, therefore quite useful to use with the atlas mode.

[![Screenshot from 2014-09-09 15^%40^%27](/images/2014/09/screenshot-from-2014-09-09-154027.png?w=584)
](/images/2014/09/screenshot-from-2014-09-09-154027.png)

The functions result can be used with other functions. In the following image, there is an expression to show the coordinates in a more compact way.

[![Screenshot from 2014-09-09 15^%43^%55](/images/2014/09/screenshot-from-2014-09-09-154355.png?w=584)
](/images/2014/09/screenshot-from-2014-09-09-154355.png)

There was a setback... For the functions to become available, it was necessary to manually import them in each QGIS session. Not very practical. Again with Nathan's [help](http://osgeo-org.1560.x6.nabble.com/How-to-import-a-user-defined-expression-functions-on-QGIS-start-up-td5159062.html), I found out that it's possible to import python modules at QGIS startup by putting a **startup.py** file with the import statements in the **.qgis2/python** folder. In my case, this was enough.

[code language="Python"]

import userfunctions

[/code]

I was pretty satisfied with the end result. The ability to create your own functions in expressions demonstrates once more how easy it is to customize QGIS and create your own tools. I'm already thinking in more applications for this amazing functionality.

[![UT 9 - Qta da Peninha - Vegetação potencial](/images/2014/09/ut-9-qta-da-peninha-vegetac3a7c3a3o-potencial.jpg?w=584)
](/images/2014/09/ut-9-qta-da-peninha-vegetac3a7c3a3o-potencial.jpg)

You can download the Python files with the functions [HERE](https://www.dropbox.com/s/b0ejc7216eboach/user_functions.zip?dl=0). Just unzip both files to the .qgis2/python folder, and restart QGIS, and the functions should become available.

**Disclaimer: **I'm not an English native speaker, therefore I apologize for any errors, and I will thank any advice on how to improve the text.
