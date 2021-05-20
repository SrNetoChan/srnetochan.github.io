---

date: 2014-04-14 13:35:11+00:00
title: Old map in QGIS
tags:
- QGIS
---

EN | [PT](https://sigsemgrilhetas.wordpress.com/2014/04/14/mapa-envelhecido-aged-map/)


Inspired in a [post](http://anitagraser.com/2013/07/29/vintage-map-design-using-qgis/) by Anita Graser, I've tried to use QGIS to create a [Cascais](http://www.openstreetmap.org/#map=16/38.6967/-9.4156)'s old looking map, as if it have been drawn by hand in a methodical way.


## Defining the styles


I have started by defining the styles for each elements to represent.


### Buildings


To fill the buildings, I have tried to use a color that reminds me the [portuguese roofs](http://olhares.sapo.pt/client/files/foto/big/517/5174082.jpg), similar to the color commonly used in old maps of cities, with a slightly darker outline of the same color.

To give a bit of dimension, a shadow was created beneath, using a "simple fill" with dark colors and using a Offset X,Y. The values were chosen assuming the predominant direction of building's facades, so that the effect could be seen all over the map area.

[![Capturar_4](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_4.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_4.png)[![Capturar_6](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_6.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_6.png)


### Green spaces


For the green spaces, 3 symbol layers were used. One with a green "simple fill". A second one with a thick outline (outline: simple line) in a darker green, and using the new 2.2 [functionality](http://changelog.linfiniti.com/qgis/version/21/#115) that allows one to show outlines only in the polygons inside.

[![Capturar_5](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_5.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_5.png)The last symbol layer is just a tin line of a green even darker than the other two.


### [![Capturar_7](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_7.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_7.png)




### The Sea


For the sea, the same effect as the green spaces was used, but in blues and with the middle outline even thicker.
[![Capturar_8](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_8.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_8.png)


### Roads


In the road, it was used a thick line with a orange pastel color. Some street names labels were created on top of the line using a script font (in have used [Pristina Bold](http://ufonts.com/fonts/pristina.html)). To improve the label readability, a small white buffer with 50% transparency was added.
[![Captura de tela 2014-04-11 17.55.04](http://sigsemgrilhetas.files.wordpress.com/2014/04/captura-de-tela-2014-04-11-17-55-04.png)
![Capturar_9](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_9.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_9.png)


### Beach


In the beaches, besides a simple fill as background, a point patern fill was used with a very small dot.
[![Capturar_11](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_11.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_11.png)[![Capturar_10](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_10.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/capturar_10.png)


## Map composing


Though the map is looking almost done, it's in the print composer that the final touches are given. First, the map sheet is totally covered with an [image of an old papel](http://lostandtaken.com/gallery/antique7.html) (the same used by Anita). A bit of transparency is added (20%), so that the effect is not too strong.

[![Captura de tela 2014-04-14 11.24.53](http://sigsemgrilhetas.files.wordpress.com/2014/04/captura-de-tela-2014-04-14-11-24-53.png)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/captura-de-tela-2014-04-14-11-24-53.png)

Alterwards, the actual map is added, and in the map item properties, the rendering mode is changed from "normal" (by default) to "multiply". This way it looks like if the map was draw directly on the old paper.

![Captura de tela 2014-04-14 11.30.07](http://sigsemgrilhetas.files.wordpress.com/2014/04/captura-de-tela-2014-04-14-11-30-07.png)


After this, it's all about adding a few more labels (the beach and places names), a north arrow and the graphic scale (always using "multiply" rendering mode), and... Voilá, we have a map!

[![mapa_antigo](http://sigsemgrilhetas.files.wordpress.com/2014/04/mapa_antigo.jpg?w=584)
](http://sigsemgrilhetas.files.wordpress.com/2014/04/mapa_antigo.jpg)
