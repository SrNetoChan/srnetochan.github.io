---

date: 2015-02-10 23:34:49+00:00
title: Calculate polygon centroid's coordinates
tags:
- Hint
- QGIS
---

EN | [PT](https://sigsemgrilhetas.wordpress.com/2015/02/10/calcular-coordenadas-do-centroide-de-poligonos-calculate-polygon-centroids-coordinates/)


I had the need to add columns with the coordinates of polygons centroids. I came up with the following expressions to calculate X e Y, respectively:

[code]
xmin(centroid($geometry))
ymin(centroid($geometry))
[/code]

The expression seems quite simple, but it toke me some time before I realize that, not having a x(geometry) and y(geometry) functions, I could use the xmin() and ymin() to get the coordinates of the polygons centroids. Since this wasn't the first time I had to use this expressions, this post will work as a reminder for the future.
