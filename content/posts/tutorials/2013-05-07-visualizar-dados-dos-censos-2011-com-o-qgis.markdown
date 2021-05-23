---

date: 2013-05-07 22:18:21+00:00
title: Visualizar dados dos Censos 2011 com o QGIS
---

Felizmente parece que algumas coisas vão mudando no nosso país no que toca ao acesso a dados. A Base Geográfica de Referenciação da Informação (BGRI), que outrora foi paga (e bem paga), está agora disponível a todos até ao nível da subsecção estatística e com um total de 122 variáveis dos censos 2011 (organizados por população residente, população presente, famílias, alojamento e edifícios). A [página](http://mapas.ine.pt/download/index2011.phtml) para download, permite descarregar os dados totais para Portugal, ou por regiões e concelhos.

[![Screenshot from 2013-05-03 19:46:54](/images/2013/05/screenshot-from-2013-05-03-194654.png?w=584)
](/images/2013/05/screenshot-from-2013-05-03-194654.png)

O zip descarregado contém diversos ficheiros, nomeadamente um shapefile (shp, shx e dbf) com os poligonos das subsecções estatísticas e um ficheiro de texto (csv) contendo os valores das variáveis dos censos 2011 (assim como  uma nota explicativa das mesmas).

A página de ajuda refere que é possível abrir estes dados recorrendo a software open source, como o [QGIS](http://qgis.org/) ou [gvSIG](http://www.gvsig.org/web/), mas não exemplifica como fazê-lo. A tarefa, embora não seja difícil, obriga a uns quanto passos. Vamos ver quais são.

**Preparar o CSV**

Por alguma razão (provavelmente para, ao abrir como folha de cálculo, impor o tipo string), no ficheiros csv, todos os valores do campo GEO_COD contêm um apóstrofo (') no início, que impossibilitam a ligação aos dados geográficos, sendo necessário eliminá-los. Para este tipo de tarefas uso geralmente o editor de texto [Geany](http://www.geany.org/), mas  pode ser feito em qualquer editor de texto através da funcionalidade "substituir", deixando o campo "substituir por" vazio. Felizmente só este campo contém apóstrofos, sendo portanto possível eliminá-los de uma só vez em todo o documento.

[![Captura de ecra de 2013-05-05 12:37:55](/images/2013/05/captura-de-ecra-de-2013-05-05-123755.png?w=584)
](/images/2013/05/captura-de-ecra-de-2013-05-05-123755.png)

Por defeito, o QGIS (através do [OGR](http://www.gdal.org/ogr/)) lê todos os campos do csv como sendo do tipo texto (string). No entanto, se quisermos definir explicitamente o tipo de dados de cada campo, podemos usar uma técnica que aprendi com o [Hugo Martins](http://www.linkedin.com/in/hfpmartins). Na mesma pasta, basta criar um ficheiro de texto com o mesmo nome que o csv, mas com a extensão .csvt, e numa só linha, separado por virgulas e dentro de aspas, especificamos cada um dos tipos de dados dos campos (Integer, Real, String, Date (YYYY-MM-DD), Time (HH:MM:SS+nn) e DateTime (YYYY-MM-DD HH:MM:SS+nn)).

Para o caso dos ficheiros da BGRI2011, o ficheiro .csvt será qualquer coisa assim.

[code language="text"]"integer","string","string","integer","string","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer","integer"[/code]

Abrir os ficheiros no QGIS

A abertura dos ficheiros no QGIS pode ser feita usando o botão "Adicionar nova camada vectorial". Para evitar problemas com acentos e cedilhas devemos escolher a codificação "latin1". Através do botão exibir, chegamos a outro menu onde podemos indicar a localização dos ficheiros. Depois de escolher como tipo de ficheiro "Todos os ficheiros", podemos seleccionar o 'shp' e o 'csv' ao mesmo tempo (pressionando o Ctrl) e terminando por clicar em "Abrir" nos dois menus.

[![abrir_ficheiros_bgri](/images/2013/05/abrir_ficheiros_bgri1.png?w=584)
](/images/2013/05/abrir_ficheiros_bgri1.png)Depois de abertos os ficheiros, há que definir o sistema de coordenadas de referência correcto para a camada dos dados geográficos, que, tal como podemos ver pelos [metadados](http://mapas.ine.pt/download/metadados/bgri11.html), para portugal continental é o ETRS89/PT-TM06 (EPSG:3763). Isso é feito clicando com botão direito sobre a camada e escolhendo "Set Layer CRS". A forma mais fácil de encontrar o sistema desejado é introduzir o seu código EPSG no campo do filtro.

[![definir_crs](/images/2013/05/definir_crs.png?w=584)
](/images/2013/05/definir_crs.png)


# Unir as tabelas de atributos


Já só falta relacionar as duas camadas. Para isso devemos ir às propriedades da camada dos polígonos (botão direito do rato sobre a camada),  e no separador união(_joins)_, adicionar uma nova união. No menu seguinte há que definir como  camada a unir a tabela resultante do csv, o campo a unir como "geo_cod" e o campo alvo como "bgri11" (contém o código da subsecção estatística).

[![ligação dos dados](/images/2013/05/ligac3a7c3a3o-dos-dados.png?w=584)
](/images/2013/05/ligac3a7c3a3o-dos-dados.png)

Se abrirmos a tabela de atributos da camada de polígonos, podemos verificar que contém todas as variáveis dos censos 2011, que podemos usar para produzir mapas temáticos.

[![Densidade_populacional](/images/2013/05/densidade_populacional.png?w=584)
](/images/2013/05/densidade_populacional.png)

**Nota**: "bgri11" é o campo que detém o código da subsecção estatistica, mas poderia usar-se outro nível de informação desde que combinasse os campos e se dissolvesse os polígonos de antemão.
