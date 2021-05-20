---

date: 2014-11-18 23:56:51+00:00
title: Séries de mapas com formatos múltiplos em QGIS 2.6 – Parte 2
---

[EN](https://gisunchained.wordpress.com/2014/11/18/multiple-format-map-series-using-qgis-2-6-part-2/) | PT

No [último artigo](http://sigsemgrilhetas.wordpress.com/2014/11/09/series-de-mapas-com-formatos-multiplos-em-qgis-2-6-parte-1-multiple-format-map-series-using-qgis-2-6-part-1/), tentei mostrar como usei o [QGIS 2.6](http://www.qgis.org) para criar séries de mapas cuja orientação da folha se adaptasse à forma do elemento do atlas. Esse método é útil quando a escala final dos mapas não é relevante, ou quando os elementos usados no atlas têm uma dimensão muito semelhante, permitindo a adopção de uma escala única. No entanto, quando é necessário manter a mesma escala de impressão dos mapas e os elementos do atlas apresentam diferenças de extensão, é necessário alterar o tamanho da folha. Nesta segunda parte do artigo, tentarei mostrar como cheguei a uma solução para isso.

Como base usei o mapa criado na 1ª parte do artigo, do qual fiz um duplicado. Para exemplificar o método procurei criar uma série de mapas à escala 1:2.000.000. Uma vez que iria adaptar tanto a altura como a largura da folha aos elementos do atlas, não me precisava de preocupar com a orientação da folha em si e por isso comecei por desactivar as propriedades definidas por dados na opção orientação.

Fiz algumas contas usando a escala, as dimensões do elemento do atlas e as margens definidas anteriormente e e cheguei às seguintes expressões a usar na  largura e altura da folha, respectivamente:


    ((bounds_width( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1 + 10




    ((bounds_height( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1 + 30


Passo a explicar. (bounds_width( $atlasgeometry ) / 2000000.0) é a largura do elemento do atlas representado à escala 1:2.000.000 em unidades do projecto (neste caso metros). Este resultado é multiplicado por 1000 para o converter em milímetros (unidade usada nas definições do compositor). Para que o elemento de atlas não ficasse resvés aos limites do mapa decidi dar 10% de margem em torno do mesmo, o que justifica a multiplicação por 1.1. E por fim adicionei a dimensão das margens do mapa que tinham sido definidas na 1ª parte do artigo (i.e., 20 mm, 5 mm, 10 mm, 5 mm).

[![Screenshot from 2014-11-16 22:58:34](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-225834.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-225834.png)

Como se pode ver pela imagem anterior, após a introdução das expressões nas opções de largura e altura da folha, a sua dimensão já se alterava em função do tamanho do elemento de atlas. No entanto, como seria de esperar, os itens do mapa mantiveram-se teimosamente na mesma posição. Foi por isso necessário alterar as expressões definidas para a dimensão e posição de cada um deles.

Começado pelo tamanho do item de mapa, as expressões a usar na altura e largura não foram difíceis de perceber uma vez que seriam as dimensões da folha menos as margens:


    ((bounds_width( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1




    ((bounds_height( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1


[![Screenshot from 2014-11-16 23:07:43](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-230743.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-230743.png)

Para posicionar correctamente os elementos, bastou substituir nas expressões das opções X e Y os "CASE WHEN ... THEN ... END" que determinavam o tamanho da largura ou altura da folha, pelas expressões descritas anteriormente. Por exemplo, as expressões usadas para a posição da legenda em X e Y:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 297 ELSE 210 END) - 7




    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 210 ELSE 297 END) - 12


Passaram a ser, respectivamente:


    (((bounds_width( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1 + 10) - 7




    (((bounds_height( $atlasgeometry ) / 2000000.0) * 1000.0) * 1.1 + 30) - 12


[![Screenshot from 2014-11-16 23:22:40](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-232240.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-16-232240.png)

Alterando as expressões de posicionamento X e Y dos restantes itens do compositor cheguei à estrutura final.

[![alaska_region_Kenai Peninsula](https://sigsemgrilhetas.files.wordpress.com/2014/11/alaska_region_kenai-peninsula.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/alaska_region_kenai-peninsula.png)

Depois disso, a impressão/exportação de todos os (25) mapas ficou, mais uma vez, à distância de um só clique.

[![mosaico_regioes_fixed](https://sigsemgrilhetas.files.wordpress.com/2014/11/mosaico_regioes_fixed.png)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/mosaico_regioes_fixed.png)

Uma vez que o QGIS permite exportar imagens do compositor georreferenciadas, adicionando-as ao QGIS obtive este resultado interessante.

[![Screenshot from 2014-11-17 00:02:38](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-17-000238.png?w=584)
](https://sigsemgrilhetas.files.wordpress.com/2014/11/screenshot-from-2014-11-17-000238.png)
Como se pode ver pelos resultados, através deste método, podemos obter mapas com formatos bastante estranhos. Por essa razão, na 3ª e última parte deste artigo, procurarei mostrar como criar uma série de mapas com escala fixa, mas usando formatos de folhas standard (A4, A3, A2, A1 e A0).
