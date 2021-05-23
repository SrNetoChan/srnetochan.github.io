---

date: 2014-06-24 16:21:00+00:00
title: Por favor, use o operador "IN"
tags:
- QGIS
- SQL
---

Já não é a [primeira vez](https://gis.stackexchange.com/questions/103019/using-the-rule-based-styling-case-condition-to-get-results-for-each-grid-cell-fr) que vejo pessoas que para seleccionarem elementos pelos valores dos seus atributos, usam expressões como

[code language="SQL"]"field" = 'value1' OR "field" = 'value2' OR "field" = 'value3' [OR ...][/code]

Uma forma mais prática e bonita de o fazer é usar o operador** IN**.

[code language="SQL"]"field" IN ('value1','value2','value3'[,...])[/code]

Este operador existe em quase todos os softwares SIG que conheço. No [QGIS](http://www.qgis.org/pt_PT/site/), pode ser usado mesmo quando não existe um botãozinho para clicar.

![Captura de tela 2014-04-23 16.50.40](images/2014/04/captura-de-tela-2014-04-23-16-50-40.png)


Na verdade, trata-se de uma abreviatura do que é usado em SQL, onde o operador é usado na expressão WHERE.

[code language="SQL"]
SELECT *
FROM parks
WHERE "tipo" IN ('PI','CM','PJ');
[/code]

