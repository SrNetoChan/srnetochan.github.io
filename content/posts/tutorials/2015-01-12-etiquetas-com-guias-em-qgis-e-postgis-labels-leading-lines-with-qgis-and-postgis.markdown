---

date: 2015-01-12 08:00:41+00:00
title: Labels leading lines with QGIS and Postgis
tags:
- Cartography
- Hint
- Postgis
- QGIS
---

Recently I had the need to add labels to features with very close geometries, resulting in their collision.

![Capturar_3](http://gisunchained.files.wordpress.com/2015/01/capturar_3-e1420735767497.png?w=584)


Using data-defined override for label's position (I have used[ layer to labeled layer](https://plugins.qgis.org/plugins/toLabeledLayer/) plugin to set this really fast) and the QGIS tool to move labels, it was quite easy to relocate them to better places. However, in same cases, it was difficult to understand to which geometry they belonged.

![Capturar_2](http://gisunchained.files.wordpress.com/2015/01/capturar_2-e1420735797114.png?w=584)


I needed some kind of leading lines to connect, whenever necessary, label and feature. I knew another great plugin called "[Easy Custom Labeling](https://plugins.qgis.org/plugins/EasyCustomLabeling/)", by [Regis Haubourg](https://plugins.qgis.org/plugins/author/Regis%2520Haubourg%2520%2528Agence%2520de%2520l%2527eau%2520Adour%2520Garonne%2529/), that did what I needed, but it would create a memory duplicate of the original layer, wish meant that any edition on the original layer wouldn't be updated in the labels.

Since the data were stored in a PostgreSQL/Postgis database, I have decided to create a query that would return a layer with leading lines. I used the following query in DB manager:

[code language="SQL"]
SELECT
  gid,
  label,
  ST_Makeline(St_setSRID(ST_PointOnSurface(geom),27493), St_setSRID(St_Point(x_label::numeric, y_label::numeric),27493))
FROM
  epvu.sgev
WHERE
  x_label IS NOT NULL AND
  y_label IS NOT NULL AND
  NOT ST_Within(ST_Makeline(St_setSRID(ST_PointOnSurface(geom),27493), St_setSRID(St_Point(x_label::numeric, y_label::numeric),27493)),geom))[/code]

This query creates a line by using the feature centroid as starting point and the label coordinate as end point. The last condition on the WHERE statement assures that the lines are only created for labels outside the feature.

[![Capturar_1](http://gisunchained.files.wordpress.com/2015/01/capturar_1-e1420735837615.png?w=584)
](http://gisunchained.files.wordpress.com/2015/01/capturar_1-e1420735837615.png)

With the resulting layer loaded in my project, all I need is to move my labels and save the edition (and press refresh) to show a nice leading line.

[![guidelines](http://gisunchained.files.wordpress.com/2015/01/guidelines1.gif)
](http://gisunchained.files.wordpress.com/2015/01/guidelines1.gif)
