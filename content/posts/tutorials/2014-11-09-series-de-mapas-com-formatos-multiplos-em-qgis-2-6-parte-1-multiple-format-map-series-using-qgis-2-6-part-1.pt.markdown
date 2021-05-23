---

date: 2014-11-09 23:07:12+00:00
title: Séries de mapas com formatos múltiplos em QGIS 2.6 - Parte 1
tags:
- atlas
- Cartografia
- Compositor
- QGIS
---

Para não variar, a nova versão do [QGIS](http://qgis.org/pt_PT/site/) (o QGIS 2.6 Brigthon) traz um conjunto alargado de [novas funcionalidades](http://changelog.linfiniti.com/qgis/version/2.6.0/#170) que permitem ao utilizador fazer mais, melhor e mais rápido do que com a versão anterior. Uma das novidades desta versão é a possibilidade de controlar algumas propriedades dos itens do compositor através de dados (por exemplo, o tamanho e a posição). Algo que abre a porta a aplicações bastante interessantes. Nos próximos artigos, proponho-me a mostrar como criar séries de mapas com multiplos formatos.

Neste primeiro artigo, o objectivo é que, mantendo o tamanho da folha, o mapa seja criado com a orientação (paisagem ou retrato) que melhor se adapte à forma do elemento do atlas. Para exemplificar, usei a [amostra de dados do Alaska](http://docs.qgis.org/2.2/en/docs/user_manual/introduction/getting_started.html#sample-data) para criar  um mapa de cada uma das regiões do Alaska.

Em primeiro lugar comecei por criar o meu layout numa dos formatos, colocando vários itens nas posições que desejava.

[![mapa_base_atlas](/images/2014/11/mapa_base_atlas.png?w=584)
](/images/2014/11/mapa_base_atlas.png)

Para  controlar a orientação da folha através do atlas, fui ao separador "Composição" e na opção orientação, usei no botão propriedades definidos por dados a seguinte expressão:


    CASE WHEN bounds_width( $atlasgeometry ) >=  bounds_height( $atlasgeometry ) THEN 'landscape' ELSE 'portrait' END


Usando a opção de pré-visualização do atlas, podemos verificar que a orientação da folha já muda de acordo com a forma do elemento do atlas. No entanto, os itens não acompanham essa mudança e alguns ficam até fora da área de impressão.

[![Screenshot from 2014-11-08 23:29:49](/images/2014/11/screenshot-from-2014-11-08-232949.png?w=584)
](/images/2014/11/screenshot-from-2014-11-08-232949.png)

Para controlar o tamanho e posição dos itens do mapa tive em consideração o tamanho de uma folha A4 (297 x 210 mm), as dimensões das margens do mapa ( 20 mm, 5 mm, 10 mm, 5 mm) e os pontos de referência dos itens.

No caso do item "mapa", usando como ponto de referência o canto superior esquerdo, foi necessário alterar a sua altura e largura. Sabia que a altura do item era é subtracção do tamanho das margens superiores e inferiores (30 mm) da altura folha por isso a expressão a usar foi:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 297 ELSE 210 END) - 30


De forma análoga, a expressão a usar para a largura foi:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 210 ELSE 297 END) - 10


[![Screenshot from 2014-11-09 00:02:15](/images/2014/11/screenshot-from-2014-11-09-000215.png?w=584)
](/images/2014/11/screenshot-from-2014-11-09-000215.png)

Os restantes itens ocupavam sempre uma posição relativa na folha sem que fosse necessário alterar o seu tamanho e por isso tinha apenas de controlar a sua posição. Por exemplo, o título encontrava-se centrado no topo da folha, e portanto, usando como ponto de referência o topo-centro, bastou definir a seguinte expressão para a posição X:

[![Screenshot from 2014-11-09 00:13:17](/images/2014/11/screenshot-from-2014-11-09-001317.png)
](/images/2014/11/screenshot-from-2014-11-09-001317.png)


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry)  THEN 297 ELSE 210 END)  / 2.0


[![Screenshot from 2014-11-09 00:30:57](/images/2014/11/screenshot-from-2014-11-09-003057.png?w=584)
](/images/2014/11/screenshot-from-2014-11-09-003057.png)

Já a legenda exige alterar a posição em X e em Y. Usando como ponto de referência o canto inferior direito, a expressão para a posição em X foi:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 297 ELSE 210 END) - 7


E para a posição em Y:


    (CASE WHEN  bounds_width(  $atlasgeometry ) >=  bounds_height( $atlasgeometry) THEN 210 ELSE 297 END) - 12


[![Screenshot from 2014-11-09 00:47:28](/images/2014/11/screenshot-from-2014-11-09-004728.png?w=584)
](/images/2014/11/screenshot-from-2014-11-09-004728.png)

Para os restantes itens (rosa dos ventos, escala gráfica e texto no canto inferior esquerdo), as expressões a usar eram em tudo similares às já apresentadas, e, após definidas em cada um dos itens, fiquei com o layout preparado para se adaptar às duas orientações da folha.

[![output_9](/images/2014/11/output_9.png?w=212)
](/images/2014/11/output_9.png)

Depois disso, a impressão/exportação de todos os (25) mapas ficou à distância de um só clique.

[![mosaico_regioes](/images/2014/11/mosaico_regioes.png)
](/images/2014/11/mosaico_regioes.png)

No próximo artigo da série, procurarei explicar como criar séries de mapas em que seja o tamanho da folha a adaptar-se de forma a manter uma escala constante.
