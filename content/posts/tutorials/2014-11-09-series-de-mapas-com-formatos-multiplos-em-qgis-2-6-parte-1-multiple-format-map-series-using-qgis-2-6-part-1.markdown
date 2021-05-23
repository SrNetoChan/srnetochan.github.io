---

date: 2014-11-09 23:07:12+00:00
title: Multiple format map series using QGIS 2.6 - Part 1
tags:
- atlas
- Cartography
- Composer
- QGIS
---

As always, the new [QGIS](http://qgis.org) version (QGIS 2.6 Brigthon) brings a vast new [set of features](http://changelog.linfiniti.com/qgis/version/2.6.0/#170) that will allow the user to do more, better and faster than with the earlier version. One of this features is the ability to control some of the composer's items properties with data (for instance, size and position). Something that will allow lots of new interesting usages. In the next posts, I propose to show how to create map series with multiple formats.

In this first post, the goal is that, keeping the page size, the map is created with the most suitable orientation (landscape or portrait) to fit the atlas feature. To exemplify, I will be using the [Alaska's sample dataset](http://docs.qgis.org/2.2/en/docs/user_manual/introduction/getting_started.html#sample-data) to create a map for each of Alaska's regions.

I have started by creating the layout in one of the formats, putting the items in the desired positions.

[![mapa_base_atlas](http://gisunchained.files.wordpress.com/2014/11/mapa_base_atlas.png?w=584)
](http://gisunchained.files.wordpress.com/2014/11/mapa_base_atlas.png)

To control the page orientation with the atlas feature, in the composition tab, I used the following expression in the orientation data defined properties:


    CASE WHEN bounds_width( $atlasgeometry ) >=  bounds_height( $atlasgeometry ) THEN 'landscape' ELSE 'portrait' END


Using the atlas preview, I could verify that the page's orientation changed according to the form of the atlas feature. However, the composition's items did not follow this change and some got even outside the printing area

[![Screenshot from 2014-11-08 23:29:49](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-08-232949.png?w=584)
](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-08-232949.png)

To control both size and position of the composition's items I had in consideration the A4 page size (297 x 210 mm), the map margins ( 20 mm, 5 mm, 10 mm, 5 mm) and the item's reference points.

For the map item, using the upper left corner as reference point, it was necessary to change it's height and width. I knew that the item height was the subtraction of the top and bottom margins (30 mm) from the page height, therefore I used the following expression:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 297 ELSE 210 END) - 30


Likewise, the expression to use in the width was:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 210 ELSE 297 END) - 10


[![Screenshot from 2014-11-09 00:02:15](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-000215.png?w=584)
](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-000215.png)

The rest of the items were always at a relative position of the page without the need to change their size and therefore only needed to control their position. For example, the title was centered at the page's top, and therefore, using the top-center as reference point, all that was needed was the following expression for the X position:

[![Screenshot from 2014-11-09 00:13:17](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-001317.png)
](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-001317.png)


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry)  THEN 297 ELSE 210 END)  / 2.0


[![Screenshot from 2014-11-09 00:30:57](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-003057.png?w=584)
](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-003057.png)

On the other hand, the legend needed to change the position in both X and Y. Using the bottom-right-corner as reference point, the X position expression was:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 297 ELSE 210 END) - 7


And for the Y position:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 210 ELSE 297 END) - 12


[![Screenshot from 2014-11-09 00:47:28](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-004728.png?w=584)
](http://gisunchained.files.wordpress.com/2014/11/screenshot-from-2014-11-09-004728.png)

For the remaining items (North arrow, scalebar, and bottom left text), the expression were similar to the ones already mentioned, and, after setting them for each item, I got a layout that would adapt to both page orientation.

[![output_9](http://gisunchained.files.wordpress.com/2014/11/output_9.png?w=212)
](http://gisunchained.files.wordpress.com/2014/11/output_9.png)

From that point, printing/exporting all (25) maps was one click away.

[![mosaico_regioes](http://gisunchained.files.wordpress.com/2014/11/mosaico_regioes.png)
](http://gisunchained.files.wordpress.com/2014/11/mosaico_regioes.png)

In the [next post](https://gisunchained.wordpress.com/2014/11/18/multiple-format-map-series-using-qgis-2-6-part-2/) of the series, I will try to explain how to create map series where it's the size of the page that change to keep the scale's value of the scale constant.
