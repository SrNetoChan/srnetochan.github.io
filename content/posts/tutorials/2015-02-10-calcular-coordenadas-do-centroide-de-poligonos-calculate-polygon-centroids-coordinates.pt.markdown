---

date: 2015-02-10 23:34:49+00:00
title: Calcular coordenadas do centroide de polígonos
---

[EN](https://gisunchained.wordpress.com/2015/02/10/calcular-coordenadas-do-centroide-de-poligonos-calculate-polygon-centroids-coordinates/) | PT

Tive necessidade de, numa camada de polígonos, adicionar colunas à tabela de atributos com as coordenadas dos centroides das geometria. Cheguei às seguintes expressões para calcular as coordenadas X e Y, respectivamente:

[code]
xmin(centroid($geometry))
ymin(centroid($geometry))
[/code]

A expressão parece bastante banal, mas ainda demorei a perceber que, não existindo funções x(geometry) e y(geometry), podia usar as funções xmin() e ymin() para obter as coordenadas dos centroides dos polígonos. Uma vez que esta não foi a primeira vez que precisei de usar estas expressões, fica agora o registo para não me voltar a esquecer.
