---

date: 2014-09-09 23:05:51+00:00
title: Coordenadas dos cantos do mapa em QGIS
tags:
- Cartografia
- python
- QGIS
- tutorial
---

[EN](https://gisunchained.wordpress.com/2014/09/09/coordenadas-dos-cantos-do-mapa-em-qgis-map-corner-coordinates-in-qgis/) | PT


## O desafio


Em tempos na [lista de discussão do qgis-pt](http://osgeo-org.1560.x6.nabble.com/QGIS-pt-f5128248.html) alguém perguntou como [dispor as coordenadas dos cantos do mapa](http://osgeo-org.1560.x6.nabble.com/QGIS-Layout-coordenadas-nos-4-cantos-do-mapa-tt5140019.html) no [QGIS](http://www.qgis.org). Não estando (ainda) disponível tal funcionalidade, tentei chegar sem sucesso a uma solução que fosse de certa forma automática. Depois de remoer a ideia, e de ler [um artigo](http://nathanw.net/2012/11/10/user-defined-expression-functions-for-qgis/) do [Nathan Woodrow](http://nathanw.net/aboutme.html), achei que a solução poderia passar por criar uma função para o construtor de expressões que pudesse ser usada em etiquetas no mapa.


##  A solução


Seguindo as indicações do referido artigo, comecei por criar um ficheiro **userfunctions.py**, que gravei na pasta **.qgis2/python **e, com [uma ajuda](http://osgeo-org.1560.x6.nabble.com/How-to-get-Composer-s-name-title-using-Python-td5160691.html) do [Nyall Dawson](http://nyalldawson.net/), escrevi o seguinte código.

[code language="Python"]
from qgis.utils import qgsfunction, iface
from qgis.core import QGis

@qgsfunction(2,"python")
def map_x_min(values, feature, parent):
 """
 Returns the minimum x coordinate of a map from
 a specific composer.
 """
 composer_title = values[0]
 map_id = values[1]
 composers = iface.activeComposers()
 for composer_view in composers():
  composer_window = composer_view.composerWindow()
  window_title = composer_window.windowTitle()
  if window_title == composer_title:
   composition = composer_view.composition()
   map = composition.getComposerMapById(map_id)
   if map:
    extent = map.currentMapExtent()
    break
 result = extent.xMinimum()
 return result
[/code]

Depois de correr o comando **import userfunctions** na consola python (Módulos > Consola python), já conseguia usar a função **map_x_min()** (disponível na categoria python) numa expressão para obter o valor mínimo em X.

![Screenshot from 2014-09-09 16^%29^%29](http://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-162929.png?w=584)

Bastava então criar as restantes funções **map_x_max()**, **map_y_min()** e** map_y_max()**. Como parte do código seria repetida, decidi encapsulá-lo na função **map_bound()** que recebesse como argumentos o título do compositor de impressão e o id do mapa e me devolvesse a extensão do mesmo (sob a forma de um QgsRectangle).

[code language="Python"]
from qgis.utils import qgsfunction, iface
from qgis.core import QGis

def map_bounds(composer_title, map_id):
 """
 Returns a rectangle with the bounds of a map
 from a specific composer
 """
 composers = iface.activeComposers()
 for composer_view in composers:
  composer_window = composer_view.composerWindow()
  window_title = composer_window.windowTitle()
  if window_title == composer_title:
   composition = composer_view.composition()
   map = composition.getComposerMapById(map_id)
   if map:
    extent = map.currentMapExtent()
    break
 else:
  extent = None

 return extent[/code]

Com essa função disponível podia usá-la internamente nas funções para devolver cada um dos mínimos e máximos em X e Y, tornando o código mais compacto e fácil de manter. Adicionei ainda ao código original alguns mecanismos para evitar erros.

[code language="Python"]
@qgsfunction(2,"python")
def map_x_min(values, feature, parent):
 """
 Returns the minimum x coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_x_min(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_x_min('my pretty map', 0) -> -12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.xMinimum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_x_max(values, feature, parent):
 """
 Returns the maximum x coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_x_max(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_x_max('my pretty map', 0) -> 12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.xMaximum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_y_min(values, feature, parent):
 """
 Returns the minimum y coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_y_min(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_y_min('my pretty map', 0) -> -12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.yMinimum()
 else:
  result = None

 return result

@qgsfunction(2,"python")
def map_y_max(values, feature, parent):
 """
 Returns the maximum y coordinate of a map from a specific composer.
 Calculations are in the Spatial Reference System of the project.
<h2>Syntax</h2>
map_y_max(composer_title, map_id)
<h2>Arguments</h2>
composer_title - is string. The title of the composer where the map is.
 map_id - integer. The id of the map.
<h2>Example</h2>
map_y_max('my pretty map', 0) -> 12345.679

 """
 composer_title = values[0]
 map_id = values[1]
 map_extent = map_bounds(composer_title, map_id)
 if map_extent:
  result = map_extent.yMaximum()
 else:
  result = None

 return result[/code]

As funções ficaram disponíveis no construtor de expressões na categoria "Python" (podia ter-lhe dado outro nome qualquer) e as descrições das funções são transformadas em textos de ajuda para fornecer ao utilizador informação de como utilizar as funções.

![Screenshot from 2014-09-09 15^%39^%19](http://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-153919.png?w=584)


Usando as funções recentemente criadas, foi fácil posicionar etiquetas  junto dos cantos do mapa com as coordenadas dos mesmos. Qualquer alteração à extensão do mapa, reflecte-se nas etiquetas, podendo por isso ser usadas convenientemente com a funcionalidade de atlas.

[![Screenshot from 2014-09-09 15^%40^%27](http://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-154027.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-154027.png)

O resultado destas funções pode ser usado com outras. Na imagem seguinte apresenta-se uma expressão para apresentar as coordenadas de forma mais compacta.

[![Screenshot from 2014-09-09 15^%43^%55](http://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-154355.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/09/screenshot-from-2014-09-09-154355.png)

Havia um senão... Para as funções ficarem disponíveis, seria necessário importá-las manualmente em cada utilização do QGIS. Algo que não era prático. Novamente com a [ajuda](http://osgeo-org.1560.x6.nabble.com/How-to-import-a-user-defined-expression-functions-on-QGIS-start-up-td5159062.html) do Nathan, fiquei a saber que podemos importar módulos Python no arranque do QGIS colocando na pasta **.qgis2/python** um ficheiro com o nome **startup.py** com os comandos de importação. Para o meu caso bastou o seguinte.

[code language="Python"]
import userfunctions
[/code]


## Conclusões


Fiquei bastante satisfeito com o resultado. A possibilidade do utilizador criar as usas próprias funções para usar em expressões vem mais uma vez demonstrar como é fácil personalizar e criar as minhas próprias ferramentas para QGIS. Já estou a matutar em mais aplicações para estar fantástica funcionalidade.

[![UT 9 - Qta da Peninha - Vegetação potencial](http://sigsemgrilhetas.files.wordpress.com/2014/09/ut-9-qta-da-peninha-vegetac3a7c3a3o-potencial.jpg?w=584)
](http://sigsemgrilhetas.files.wordpress.com/2014/09/ut-9-qta-da-peninha-vegetac3a7c3a3o-potencial.jpg)

Os ficheiros Python com as funções criadas podem ser descarregados [AQUI](https://www.dropbox.com/s/b0ejc7216eboach/user_functions.zip?dl=0). Basta descompactar os dois ficheiros para a pasta **.qgis2/python** e reiniciar o QGIS, e as funções devem ficar disponíveis.
