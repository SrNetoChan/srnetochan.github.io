---

date: 2014-01-15 00:40:09+00:00
title: Mapas de fluxos em QGIS
tags:
- QGIS
---

Hoje surgiu a questão "[Como consigo fazer um mapa em que a sobreposição de símbolos aumente a opacidade?](https://gis.stackexchange.com/questions/82806/how-do-i-make-a-map-where-overlapping-symbols-increase-opacity/82815#82815)". Fiz o meu melhor para descrever como fazê-lo em QGIS, que transcrevo agora para português.

Este tipo de mapas pode ser feito em QGISs usando a uma combinação da transparência e cor dos símbolos e o blending mode dos elementos.

Note-se a diferença entre a transparência e blending mode da camada (que é aplicado a toda a camada) e a transparência do símbolo e blending dos elementos (que acumulam com outros elementos da mesma camada).

Esta opções estão disponíveis em Propriedades da camada > Estilo.

[![testes_opacidade_opcoes](/images/2014/01/testes_opacidade_opcoes.png?w=584)
](/images/2014/01/testes_opacidade_opcoes.png)

Com um valor de transparência do símbolo de 95%, a cor do elemento tornar-se à totalmente opaca quando pelo menos 20 elementos de sobrepuserem. Este número é limitado à sobreposição de 100 elementos(tranparencia 99%).

Usando diferentes modos de blending (como a multiplicação ou a adição) consegues-se obter outros efeitos.

[![Testes_com_opacidade_2](/images/2014/01/testes_com_opacidade_2.png?w=584)
](/images/2014/01/testes_com_opacidade_2.png)

Duplicando a camada, usando diferentes cores (no exemplo abaixo o verde para uma camada e o vermelho para a imediatamente baixo) e usando blending mode dogde,consegue-se obter efeitos ainda mais interessantes.

[![opacity dodge](/images/2014/01/opacity-dodge.png?w=584)
](/images/2014/01/opacity-dodge.png)
