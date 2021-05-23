---

date: 2014-06-24 16:21:00+00:00
title: Please use the "IN" operador
tags:
- QGIS
- SQL
---

It's not the [first time](https://gis.stackexchange.com/questions/103019/using-the-rule-based-styling-case-condition-to-get-results-for-each-grid-cell-fr) I see people that, to select feature by their fields values, use expressions like this:

[code language="SQL"]"field" = 'value1' OR "field" = 'value2' OR "field" = 'value3' [OR ...][/code]

A more practical and pretty way of doing this is by using the **IN** operator instead.

[code language="SQL"]"field" IN ('value1','value2','value3'[,...])[/code]

This operator is available in almost every GIS software I know. In [QGIS](http://www.qgis.org/en/site/), it can be used even if there isn't a small little button to click.
![Captura de tela 2014-04-23 16.50.40](/images/2014/04/captura-de-tela-2014-04-23-16-50-40.png)


In fact, this is an abbreviation of what is used in SQL, where the operator is used in the WHERE statement:

[code language="SQL"]
SELECT *
FROM parks
WHERE "tipo" IN ('PI','CM','PJ');
[/code]

