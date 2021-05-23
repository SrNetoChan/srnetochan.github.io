---

date: 2016-01-28 22:33:52+00:00
title: QGIS Features I long for while using ArcGIS
tags:
- ArcGIS
- Opinion
- QGIS
---

## (aka Features that ArcGIS Desktop users might not know that exists)


From time to time, I read articles comparing ArcGIS vs QGIS. Since many of those articles are created from an ArcGIS user point of view, they invariably lead to biased observations on QGIS lack of features. It's time for a QGIS user perspective, so bare with me on this (a bit) long, **totally and openly biased post**.


<blockquote>"Hello, my name is Alexandre, and I have been using... [QGIS](http://www.qgis.org)"</blockquote>


This is something I would say at an anonymous QGIS user therapy group. I'm willing to attend one of those because being recently and temporally forced to use ArcGIS Desktop again (don't ask!), I really really really miss QGIS in many ways.

There was a time when I have used ArcGIS on the regular basis. I used it until version 9.3.1 and then decided to move away (toward the light) into QGIS (1.7.4 I think). At that time, I missed some (or even many?) ArcGIS features, but I was willing to accept it in exchange for the freedom of the [Open Source](https://en.wikipedia.org/wiki/Open_source) philosophy. Since then, a lot have happened in the QGIS world, and I have been watching it closely. I would expect the same have happened in ArcGIS side, but, as far I can see, it didn't.

I'm using top shelf ArcGIS Desktop Advanced and I'm struggling to do very basic tasks that simply are nonexistent in ArcGIS. So here's my short list of QGIS functionalities that I'm longing for. For those of you that use ArcGIS exclusively, some of this features may catch you by surprise.

**Warning:** For those of you that use ArcGIS exclusively, some of this features may catch you by surprise.


## Transparency control




<blockquote>"ArcGIS have transparency! It's in the Display tab, in the layer's properties dialog!"</blockquote>


Yes, but... you can only set transparency at the layer level. That is, either it's all transparent, or it's not...

In QGIS on the other end, you can set transparency at layer level, feature/symbol level, and color level. You can say that this is being overrated, but check the differences in the following images.

![Transparency_layer_level](/images/2016/01/transparency_layer_level.png)
![Transparency_feature_symbol_level](/images/2016/01/transparency_feature_symbol_level.png)
![Transparency_color_level](/images/2016/01/transparency_color_level.png)


Notice that in QGIS you can set transparency at color level everywhere (or almost everywhere) there is a color to select. This includes annotations (like the ones in the image above), labels and composers items. You can even set transparency in colors by using the RGBA function in an expression! How sweet can that be? :-)

![Screenshot from 2016-01-27 14:12:34](/images/2016/01/screenshot-from-2016-01-27-141234.png)



## Blending modes


This is one of QGIS's pristine jewels. The ability to combine layers the way you would do in almost any design/photo editing software. At layer or at feature level, you can control how they will "interact" with other layers or features below. Besides the normal mode, QGIS offers 12 other blending modes:  Lighten, Screen, Dodge, Darken, Multiply, Burn, Overlay, Soft light, Hard light, Difference, and Subtract. Check [this page](https://en.wikipedia.org/wiki/Blend_modes) to know more about the math behind each one and [this image](http://image.slidesharecdn.com/blendmodesforopengl-140213092122-phpapp02/95/blend-modes-for-opengl-3-638.jpg?cb=1392283377) for some examples

It's not easy to grasp how can this be of any use for cartography before you try it yourself. I had the chance to play around while trying to answer [this question](http://gis.stackexchange.com/a/82815/6191).

![2wph4](/images/2016/01/2wph4.jpg)


A very common application for this functionality is when you want to add shadows to simulate the relief by putting a hill shade on top of other layers. In ArcGIS, you can only control the layer transparency, and the result is always a bit pale. But in QGIS, you can keep the strength of the original colors by using the multiply mode in the hill shade layer.

[caption id="attachment_1809" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:24:38](/images/2016/01/screenshot-from-2016-01-27-152438.png)
Hypsometry original colors[/caption]

[caption id="attachment_1806" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:25:45](/images/2016/01/screenshot-from-2016-01-27-152545.png)
Hypsometry colors paled by transparent hill shade[/caption]

[caption id="attachment_1805" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:24:45](/images/2016/01/screenshot-from-2016-01-27-152445.png)
Hypsometry original colors with the hill shade using QGIS multiply blending[/caption]

You can also use blending modes in the print composer items, allowing you to combine them with other items and textures. This gives you the opportunity to make [more "artistic" things](https://gisunchained.wordpress.com/2014/04/14/mapa-envelhecido-aged-map/) without the need to go post-processing in a design software.


## Colour Picker Menu


Controlling color is a very important deal for a cartographer and QGIS allow you to control it like the professional you are. You can select your colours using many different interfaces. Interfaces that you might recognize from software like Inkscape, Photoshop, Gimp and others alike.

[gallery ids="1570,1569,1568" type="rectangular"]

My favorite one is the color picker. Using color picker, you can pick colors from anywhere on your screen, either from QGIS itself or outside. This is quite handy and productive when you are trying to use a color from your map, it's legend, a [COLOURlovers](http://www.colourlovers.com/) palette or a company logo.

[caption id="attachment_1571" align="alignnone" width="862"]![anim](/images/2016/01/anim.gif)
Picking a color from outside QGIS[/caption]

You can also copy/paste colors between dialogs, save and import color palettes, and you can even name a color and [use it in a variable](http://nyalldawson.net/2015/12/exploring-variables-in-qgis-pt-2-project-management/). With all this available for free, it's hard to swallow Windows color selector :(.

[gallery ids="1555,1554" type="rectangular" orderby="rand"]


### Vector symbols renderers "powertools"


In ArcGIS, you have a few fancy ways to symbol your vector layers. You got: _Single symbol_, _Unique values_, _Unique values many fields_... and so on. At the first glance, you may think that QGIS lacks some of them. Believe me, it doesn't! In fact, QGIS offers much more flexibility when you need to symbol your layers.

For starters, it allows you to use fields or expressions on any of the symbols renderers, while ArcGIS only allows the use of fields. Powered by hundreds of functions and the ability to create your owns in python, what you can do with the expression builder has no limits. This means, for instance, that you can combine, select, recalculate, normalize an infinite number of fields to create your own "values" (not to mention that you can tweak your values labels, making it ideal to create the legend).

[caption id="attachment_1580" align="alignnone" width="825"]![Screenshot from 2016-01-20 22:34:54](/images/2016/01/screenshot-from-2016-01-20-223454.png)
QGIS Graduated renderer using an expression to calculate population density[/caption]

And then, in QGIS, you have the special (and kinda very specific) renderers, that make you say "wooooh". Like the _Inverted polygons_ that allow you to fill the the outside of polygons (nice to mask other features), the _Point displacement_ to show points that are too close to each others, and the _Heatmap_ that will transform, ON-THE-FLY, all your points in a layer into a nice heatmap without the need to convert them to raster (and that will update as soon as you, or anyone else, edits the point features).

[caption id="attachment_1583" align="alignnone" width="777"]![Screenshot from 2016-01-20 22:58:44](/images/2016/01/screenshot-from-2016-01-20-225844.png)
Inverted Polygon Renderer masking the outside of an interest area[/caption]

But I have left the best to the end. The "One rendered to Rule them all", the _Rule-based_ symbols. With the rule-based renderer, you can add several rules, group them in a tree structure, and set each one with a desired symbol. This gives QGIS users full control of their layer's symbols, and, paired with expression builder and data-defined properties, opens the door to many wonderful applications.

[caption id="attachment_1589" align="alignnone" width="869"]![rulesymbol_ng_line](/images/2016/01/rulesymbol_ng_line.png)
Rule-based renderer[/caption]


## Atlas


One of my favorite (and missed) features in QGIS is the Map Composer's Atlas. I know that ArcGIS has its own "Atlas", the Data Driven Pages, but frankly, it's simply not the same.

I believe you know the basic functionally that both software allow. You create a map layout and choose a vector layer as coverage, and it will create an output panned or zoomed for each of the layer's feature. You can also add some labels that will change according to the layers attributes.

**But in QGIS, things go a little bit further...**

Basically, you can use coverage layer's attributes and geometry anywhere you can use an expression. And, in QGIS, expressions are everywhere. That way, most layers and map composer items properties can be controlled by a single coverage layer.

With the right configuration, while iterating over the atlas coverage features, you can,  [choose what feature to show and what features to hide](http://nathanw.net/2013/12/02/waiting-for-qgis-2-2-highlighting-current-atlas-feature/), [change a theme color for your map](http://nathanw.net/2014/09/23/qgis-atlas-on-non-geometry-tables/), [rotate and resize your page acording to the feature size](https://gisunchained.wordpress.com/2014/11/09/series-de-mapas-com-formatos-multiplos-em-qgis-2-6-parte-1-multiple-format-map-series-using-qgis-2-6-part-1/), [choose a specific logo to came along with your map](http://nyalldawson.net/2013/04/a-neat-trick-in-qgis-2-0-images-in-atlas-prints/), and much more. Once again, the sky is the limit.

[caption id="attachment_535" align="aligncenter" width="506"]![mosaico_regioes_fixed](/images/2014/11/mosaico_regioes_fixed.png)
Auto-resized maps that fits the coverage features at specific scale using atlas[/caption]

So, if you pair **Atlas** it with QGIS **data-defined properties**,** rule-based symbols** and **expressions**, ArcGIS Data Driven Pages are no match. You don't think so? Try to answer [this question](http://gis.stackexchange.com/questions/174817/feature-label-visibility-based-on-spatial-relationship-to-index-feature-using-da?atw=1) then.

**Tip:** If you really want to leverage your map production, using [Spatialite](https://www.gaia-gis.it/gaia-sins/) or [Postgis ](http://postgis.net/)databases you can create the perfect atlas coverage layers from views that fit your needs. No data redundancy and they are always updated.


## Label and Style dialogs


This one is more of a User Experience thing than an actual feature, but you won't imagine how refreshing it is to have all Style and Labels options in two single dialogs (with several tabs, of course).

Using the symbol menu in ArcGIS makes me feel like if I'm in the [Inception movie](http://www.imdb.com/title/tt1375666/), at some point in time, I no longer know where the hell am I. For example, to apply a dashed outline in a fill symbol I needed to open 5 different dialogs, and then go back clicking OK, OK, OK, OK ...

[caption id="attachment_1244" align="aligncenter" width="1499"]![Capture](/images/2016/01/capture.jpg)
ArcGIS "Inception" symbol settings[/caption]

In QGIS, once in the properties menu, every setting is (almost) one click way. And you just need to press OK (or Apply ) once to see the result!

[caption id="attachment_1561" align="alignnone" width="907"]![Screenshot from 2016-01-20 21:51:33](/images/2016/01/screenshot-from-2016-01-20-215133.png)
QGIS Style setting[/caption]

As an extra, you can copy/paste styles from one layer to another, making styling several layers even faster. And now you say:


<blockquote>"Don't be silly! In ArcGIS you can import symbols from other layers too."</blockquote>


Symbols? yes. Labels? No! And if you had lots of work setting your fancy labels, having to do the exact same/similar thing in another layer, it will make you wanna cry... I did.

(I think I will leave the **multiple styles per layer vs data frames** comparison for another time)


## WFS




<blockquote>"Say what?!!"</blockquote>


Yup, that's it, ArcGIS Desktop lacks support for [WFS OGC standard](http://www.opengeospatial.org/standards/wfs) unless you buy an extra extension: The [Data Interoperability Extention](http://www.esri.com/software/arcgis/extensions/datainteroperability/pricing).

In a GIS world that, more and more, is evolving towards [Open Data](https://en.wikipedia.org/wiki/Open_data), [Open Standards](https://en.wikipedia.org/wiki/Open_standard) and [OGC Web Services](http://www.opengeospatial.org/standards/owc), this reveals a very mercantile approach by ESRI. If I were an ESRI customer, I would feel outraged. <sarcasm>Or maybe not... maybe I would thank the opportunity to yet invest some more money in it's really advanced features...<\sarcasm>

In QGIS, like everything else, WFS is absolutely free (as in freedom, not free beer). All you need to do is add the WFS server's URL, and you can add all the layers you want, with the absolute sure that they are as updated as you can get.

![Screenshot from 2016-01-20 21:58:54](/images/2016/01/screenshot-from-2016-01-20-215854.png)


Fortunately for ArcGIS users with a low budget, they can easily make a request for a layer using the internet browser :-P.


    http://giswebservices.massgis.state.ma.us/geoserver/wfs?request=GetFeature&service=wfs&version=1.0.0&typename=massgis:GISDATA.TOWNS_POLY&outputformat=SHAPE-ZIP


Or they can simply use QGIS to download it. But, in both cases, be aware that the layers won't update themselves by magic.


## Expression builder


I have already mentioned the use of expressions several times, but for those of you that do not know the expression Builder, I though I end my post with one of my all time favourite features in QGIS.

I do not know enough of ArcGIS expression builder to really criticize it. But, AFAIK, you can use it to create labels and to populate a field using the field calculator. I know that there are many functions that you can use (I have used just a few) but they are not visible to the common user (you probably need to consult the ArcGIS Desktop Help to know them all). And you can create your own functions in VBScript, Python, and JsScript.

![Capture](/images/2016/01/capture2.jpg)


On QGIS side, like I said before, the Expression Builder can be used almost everywhere, and this makes it very convenient for many different purposes. In terms of functions, you have hundreds of functions right there in the builder's dialog, with the corresponding syntax help, and some examples. You also have the fields and values like in ArcGIS, and you even have a "recent expressions" group for re-using recent expressions with no the need to remember prior expression.

![Capture](/images/2016/01/capture3.jpg)


Besides, you can create your own functions using Python (no VBScript or JsScript). For this purpose, you have a separate tab with a function editor. The editor have code highlighting and save your functions in your user area, making it available for later use (even for other QGIS sessions).

![Capture](/images/2016/01/capture4.jpg)



## Conclusion


These are certainly not the only QGIS features that I miss, and they are probably not the most limiting ones (for instance, not being able to fully work with Spatialite and Postgis databases will make, for sure, my life miserable in the near future), but they were the ones I noticed right away when I (re)open ArcGIS for the first time.

I also feel that, based on the QGIS current development momentum, with each QGIS Changelog, the list will grow very fast. And although I haven't tested ArcGIS Pro, I don't think ESRI will be able to keep the pace.

"Are there things I still miss from ArcGIS?" Sure. I miss CMYK color support while exporting maps, for instance. But not as much as I miss QGIS now. Besides, I know that those will be addressed sooner or later.

In the end, I kinda enjoyed the opportunity to go back to ArcGIS, as it reinforced the way I think about QGIS. It's all about freedom! Not only the freedom to use the software (that I was already aware) but also the freedom to control software itself and it's outputs. Maintaining the users friendliness for new users, a lot have been done to make power users life easier, and they feel very pleased with it (at least I am).


<blockquote>

>
> All this being said, the winner is... QGIS!!
>
>
</blockquote>




### The End




#### (of a very biased post)
