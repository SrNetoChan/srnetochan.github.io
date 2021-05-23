---
date: 2013-04-24 15:47:11+00:00
title: Definir a representação de pixeis sem valor em mosaicos de imagens VRT
tags:
- gdal
- tutorial
---

Como está muito bem descrito neste [artigo](http://blog.viasig.com/2010/01/mosaicos-de-imagens-em-mapserver-com-gdal/) do Duarte Carreira, a criação de catálogos virtuais (vrt) e respectivas pirâmides (overviews) usando o [GDAL](http://www.gdal.org/), permite facilitar e melhorar a performance de visualização de mosaicos de imagens.

Usando o comando [gdalbuildvrt](http://www.gdal.org/gdalbuildvrt.html) para criar o catálogo virtual, as áreas sem valor (NoData) são, por defeito, substituídas pelo valor 0. Em certos caso, o efeito pode não ser o mais desejável.


    gdalbuildvrt mosaico1.vrt --optfile listadeimagens.txt


[![mosaico1_fundo](images/2013/04/mosaico1_fundo.jpg?w=584)
](images/2013/04/mosaico1_fundo.jpg)

No entanto, através dos parâmetros **-hidenodata** e **-srcnonata,** é possível definir outros valores para os pixeis sem valor. Por exemplo, no comando seguinte escolhi os valores RGB [255, 255, 255] (branco). E o resultado foi uma imagem com o "fundo" branco.


    gdalbuildvrt mosaico2.vrt -hidenodata -srcnodata "255 255 255" --optfile listadeimagens.txt


[![mosaico2_fundo](images/2013/04/mosaico2_fundo.jpg?w=584)
](images/2013/04/mosaico2_fundo.jpg)

Se pretendermos que pixeis sem valor não sejam representados, podemos usar o parâmetro **-addalpha**,  tornando-os transparentes.


    gdalbuildvrt mosaico3.vrt -hidenodata -addalpha --optfile listadeimagens.txt


[![mosaico3](images/2013/04/mosaico3.jpg?w=584)
](images/2013/04/mosaico3.jpg)
