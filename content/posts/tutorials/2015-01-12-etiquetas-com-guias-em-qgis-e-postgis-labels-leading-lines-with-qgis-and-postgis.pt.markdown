---

date: 2015-01-12 08:00:41+00:00
title: Etiquetas com guias em QGIS e Postgis
---

Recentemente tive necessidade de colocar etiquetas de texto em elementos com geometrias muito próximas, fazendo com que as mesmas colidissem umas com as outras.

![Capturar_3](images/2015/01/capturar_3-e1420735767497.png?w=584)


Controlando a posição das etiquetas através dos dados (para configurar rapidamente a camada usei o plugin "[layer to labeled layer](https://plugins.qgis.org/plugins/toLabeledLayer/)") e usando a ferramenta do qgis para mover as etiquetas, foi relativamente fácil reposicioná-las de forma a que todas coubessem no mapa sem se sobreporem. Porém, em certos casos, tornou-se difícil perceber a que elemento cada uma correspondia.

![Capturar_2](images/2015/01/capturar_2-e1420735797114.png?w=584)


Precisava de criar "linhas de guia" que, sempre que necessário, ligassem o elemento e a respectiva etiqueta. Conhecia a existência de outro excelente plugin, chamado “[Easy Custom Labeling](https://plugins.qgis.org/plugins/EasyCustomLabeling/)” do [Regis Haubourg](https://plugins.qgis.org/plugins/author/Regis%2520Haubourg%2520%2528Agence%2520de%2520l%2527eau%2520Adour%2520Garonne%2529/), que fazia o que eu pretendia, mas como criava um duplicado da camada original significava que a mesma não seria actualizada quando a camada original fosse editada.

Uma vez que os dados estavam guardados numa base de dados PostgreSQL/Postgis, decidi criar uma consulta que me devolvesse uma camada com as linhas de guia. Usei a seguinte consulta no gestor de bases de dados:

[code language="SQL"]
SELECT
  gid,
  label,
  ST_Makeline(St_setSRID(ST_PointOnSurface(geom),27493), St_setSRID(St_Point(x_label::numeric, y_label::numeric),27493))
FROM
  epvu.sgev
WHERE
  x_label IS NOT NULL AND
  y_label IS NOT NULL AND
  NOT ST_Within(ST_Makeline(St_setSRID(ST_PointOnSurface(geom),27493), St_setSRID(St_Point(x_label::numeric, y_label::numeric),27493)),geom))[/code]

Esta consulta cria uma linha composta pelo centro (interno) do polígono e a coordenada do ponto para a qual a etiqueta foi movida. A última condição da cláusula WHERE garante que a linha só é criada se a coordenada da etiqueta não estiver dentro do polígono.

[![Capturar_1](images/2015/01/capturar_1-e1420735837615.png?w=584)
](images/2015/01/capturar_1-e1420735837615.png)

Com a camada resultante carregada no meu projecto, basta-me mover as etiquetas e gravar a edição da camada original para que a respectiva linha de guia apareça.

[![guidelines](images/2015/01/guidelines1.gif)
](images/2015/01/guidelines1.gif)
