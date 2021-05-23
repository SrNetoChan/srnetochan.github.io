---

date: 2015-02-23 23:44:33+00:00
title: Hack to adjust map symbols location in QGIS
tags:
- Cartography
- Hint
- QGIS
---

Now and then I get too many map symbols (points) in the same place, and I thought how nice it would be if we could drag n' drop them around without messing with their geometries position, just like we do with labels. That thought gave me an idea for a cool hack.

Choose your point layer and start by creating two new fields called symbX and symbY (Type: Decimal number; Size: 20; Precision: 5). Now go the layer properties and in the Style tab edit your symbol. **For each level of your symbol** select "map units" as the offset units, and set the following expression in the offset data define properties option:

[code]

CASE WHEN symbX IS NOT NULL AND symbY IS NOT NULL THEN
    tostring($x - symbX) + ',' + tostring($y - symbY)
ELSE
    '0,0'
END

[/code]

[![Screenshot from 2015-02-22 18:18:43](/images/2015/02/screenshot-from-2015-02-22-181843.png)
](/images/2015/02/screenshot-from-2015-02-22-181843.png)

Be aware that, if your coordinates have negative values, you need to adapt the code. E.g., If you have negative values in X you should use "tostring(symbX -$x)" instead.

Now, temporarly  label your layer with a small convenient text (I used a centered '+' (plus sign) with a white buffer) and set its coordinates to data defined using the symbX and symbY Fields.

[![Screenshot from 2015-02-22 22:42:07](/images/2015/02/screenshot-from-2015-02-22-224207.png?w=660)
](/images/2015/02/screenshot-from-2015-02-22-224207.png)

From this point on, when you use the move label tool, not only the label position change but also the actual symbol! Pretty cool, isn't it?

[![anim](/images/2015/02/anim.gif)
](/images/2015/02/anim.gif)

Notice that the features geometries are not changed during the process. Also, remember that in this case you can also [add leading lines](/images/2015/01/12/etiquetas-com-guias-em-qgis-e-postgis-labels-leading-lines-with-qgis-and-postgis/) to connect the symbols to the original position of the points.
