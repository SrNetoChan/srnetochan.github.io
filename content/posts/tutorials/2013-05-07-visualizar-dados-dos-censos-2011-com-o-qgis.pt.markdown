---

date: 2013-05-07 22:18:21+00:00
title: Visualizar dados dos Censos 2011 com o QGIS
---

Felizmente parece que algumas coisas vão mudando no nosso país no que toca ao acesso a dados. A Base Geográfica de Referenciação da Informação (BGRI), que outrora foi paga (e bem paga), está agora disponível a todos até ao nível da subsecção estatística e com um total de 122 variáveis dos censos 2011 (organizados por população residente, população presente, famílias, alojamento e edifícios). A [página](http://mapas.ine.pt/download/index2011.phtml) para download, permite descarregar os dados totais para Portugal, ou por regiões e concelhos.

[![Screenshot from 2013-05-03 19:46:54](/images/2013/05/screenshot-from-2013-05-03-194654.png?w=584)
](/images/2013/05/screenshot-from-2013-05-03-194654.png)

O zip descarregado contém diversos ficheiros, nomeadamente um shapefile (shp, shx e dbf) com os poligonos das subsecções estatísticas e um ficheiro de texto (csv) contendo os valores das variáveis dos censos 2011 (assim como  uma nota explicativa das mesmas).

A página de ajuda refere que é possível abrir estes dados recorrendo a software open source, como o [QGIS](http://qgis.org/) ou [gvSIG](http://www.gvsig.org/web/), mas não exemplifica como fazê-lo. A tarefa, embora não seja difícil, obriga a uns quanto passos. Vamos ver quais são.


## Abrir os ficheiros no QGIS




### Dados geográficos (SHP)


Os dados geográficos, ao nível da subsecção estatística, estão guardados no ficheiro _ESRI _S_hapefile_ (*.shp) que abrimos usando o botão _**Adicionar camada vectorial ![add_vector](/images/2013/05/add_vector.png)
  (**_ou através do menu _**camada > adicionar camada > Adicionar camada vectorial...**_). Usando o botão _**pesquisar**_ indique a localização do ficheiro com a extensão "*.shp" (lembre-se que terá de ter opção "Todos os Ficheiros" ou "ESRI Shapefile" para que o ficheiros esteja visível). Para evitar problemas com acentos e cedilhas deve escolher uma _**codificação**_ que suporte os nossos caracteres especiais, nomeadamente o "ISO-8859-1" ou "latin1", que, como podem ver neste [link](https://pt.wikipedia.org/wiki/ISO_8859-1), é essencialmente a mesma coisa)**_._**

![Screenshot from 2016-02-13 14:48:46](/images/2013/05/screenshot-from-2016-02-13-144846.png)

Depois de aberto o ficheiro, há que definir o sistema de coordenadas de referência correcto para a camada, que, tal como podemos ver pelos [metadados](http://mapas.ine.pt/download/metadados/bgri11.html), para portugal continental é o ETRS89/PT-TM06 (EPSG:3763). Isso é feito clicando com botão direito sobre a camada e escolhendo a opção _**Definir SRC da camada**_. A forma mais fácil de encontrar o sistema desejado é introduzir o seu código EPSG no campo do filtro.

![Screenshot from 2016-02-13 14:49:28](/images/2013/05/screenshot-from-2016-02-13-144928.png)



### Dados alfanuméricos (CSV)


Os dados alfanuméricos dos censos 2011 são guardados num ficheiro CSV (_Comma Separated Values_), que não é mais que ficheiros simples de texto em que os valores são separados por vírgulas, ponto-e-vírgulas, ou espaços, e podem ser delimitados, por exemplo, por aspas, e que podem ter ou não uma linha de cabeçalho com os nomes dos campos.

Como se pode ver no excerto abaixo, no nosso caso os valores são  separados por ponto e vírgula, e contêm uma linha de cabeçalho com os nomes dos campos.


    ANO;GEO_COD;GEO_COD_DSG;NIVEL;NIVEL_DSG;N_EDIFICIOS_CLASSICOS;N_EDIFICIOS_CLASSICOS_1OU2;...
    2011;'PT;PT;1;Total Nacional;3544389;3219791;...
    2011;'1;Continente;2;NUT1;3353610;3035969;...
    2011;'17;Lisboa;3;NUT2;448957;322603;...
    2011;'171;Grande Lisboa;4;NUT3;277387;184975;...
    ...


Por omissão, o QGIS (através do [OGR](http://www.gdal.org/ogr/)) lê todos os campos do CSV como sendo do tipo texto (string). No entanto, se quisermos definir explicitamente o tipo de dados de cada campo, podemos usar uma técnica que aprendi com o [Hugo Martins](http://www.linkedin.com/in/hfpmartins). Na mesma pasta, cria-se um ficheiro de texto com o mesmo nome que o csv, mas com a extensão .csvt, e, numa só linha, separado por virgulas e dentro de aspas, especificamos cada um dos tipos de dados dos campos (_integer_, _real_, _string_, _date_ (YYYY-MM-DD), _time_ (HH:MM:SS+nn) e _datetime_ (YYYY-MM-DD HH:MM:SS+nn)).

Para o caso dos ficheiros da BGRI2011, o ficheiro .csvt será qualquer coisa assim.

[code language="text"]&quot;integer&quot;,&quot;string&quot;,&quot;string&quot;,&quot;integer&quot;,&quot;string&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;,&quot;integer&quot;[/code]

Para facilitar, criei um ficheiro csvt com as características necessárias que podem descarregá-lo [aqui](https://dl.dropboxusercontent.com/u/5088211/BGRI2011_PT.csvt). (Nota: o nome do ficheiro terá de ser alterado consoante o nível a que descarregaram a informação, e.g., BGRI2011_PT.csvt --> BGRI2011_1105.csvt.

Depois de preparado o CSVT e de o colocarmos na mesma pasta que o CSV, podemos abrir o CSV no QGIS. Para isso usamos o botão _**Adicionar camada de texto delimitado ![icon_texto_delimitado](/images/2013/05/icon_texto_delimitado.png)
 ****(**_ou através do menu _**camada > adicionar camada > Adicionar camada de texto delimitado...**_). Começamos por indicar a localização do ficheiro usando o botão _**Procurar...**_. Mais uma vez, devemos garantir que usamos uma codificação compatível, a ISO-8859-1. Em formato de ficheiro escolhemos _**Delimitadores personalizados**_ e, como já tínhamos visto anteriormente, seleccionamos a opção _**Ponto e vírgula. **_Seleccionamos a caixa _**Primeiro registo tem nome dos campos **_e escolhemos_** Sem geometria **_em Definição de geometria.

No final da caixa de diálogo podemos ver uma amostra de como ficará o nosso ficheiro dentro do QGIS. Se repararem no campo _GEO_COD_ todos os valores têm antes um apóstrofe (') - penso que colocado propositadamente para obrigar os valores a serem considerados texto em programas como o Excel ou o Calc - de que nos vamos ter de livrar. Para isso, voltamos às opções de _**Delimitadores personalizados**_ e na opção _**Escape**_ colocamos um apóstrofe (') que será ignorado em **todos os campos e respectivos valores** (felizmente, no nosso caso não existem apóstrofes noutros campos, caso contrário teríamos de editar o ficheiro num editor de texto para os salvaguardar) . A caixa de diálogo com todas as opções necessárias deve parecer-se com a imagem abaixo.

![Screenshot from 2016-02-14 01:04:26](/images/2013/05/screenshot-from-2016-02-14-010426.png)



## Unir as tabelas de atributos


Agora que temos as duas camadas no QGIS, já só falta relacionar a componente geográfica à alfanumérica. Uma vez que têm ambas um campo em comum isto pode ser feito através de uma união (virtual). Para isso, temos de abrir as propriedades da camada "geométrica" (botão direito do rato sobre a camada, _**Propriedades**_)  e, no separador **_Uniões_**, adicionar uma nova união clicando no botão ![mActionSignPlus](/images/2013/05/mactionsignplus.png)
. No menu seguinte, é necessário definir a _**Camada a unir**_ a tabela resultante do CSV, o _**Campo a unir**_ como "GEO_COD" e o _**Campo alvo**_ como "BGRI11" (contém o código da subsecção estatística). Podemos ainda definir quais os campos do CSV queremos unir, e que prefixo lhe dar. Para tornar a visualização dos dados mais rápida, aconselha-se a seleccionar a opção de memorizar a camada unida em memória virtual.

![Screenshot from 2016-02-14 15:24:02](/images/2013/05/screenshot-from-2016-02-14-152402.png)


Finalizado o processo, a camada com os dados geográficos tem agora novos campos originários do CSV, tantos quantos os escolhidos,  e precedidos de um prefixo. No meu caso apenas adicionei um campo N_INDIVIDUOS_RESIDENT e usei o prefixo BGRI11_, como se pode constatar na imagem abaixo.

![Screenshot from 2016-02-14 15:26:28](/images/2013/05/screenshot-from-2016-02-14-152628.png)


Assim, torna-se possível usar os dados dos Censos 2011 para efectuar análise espacial, ou simplesmente para criar mapas.

![censos2011_porto](/images/2013/05/censos2011_porto.jpeg)


**Nota:** Neste exemplo trabalhou-se ao nível da subsecção estatística, mas poderia usar-se outro nível de informação desde que combinasse os campos e se dissolvesse os polígonos de antemão.

**Atualizado em: 13 de Fevereiro de 2016**
