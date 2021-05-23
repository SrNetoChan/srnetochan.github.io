---

date: 2015-11-06 00:49:29+00:00
title: Obter os vértices de multipolígonos usando PostGIS
tags:
- Postgis
---

Hoje precisei criar uma _view_ em [PostGIS](http://postgis.net/) que me devolvesse os vértices de uma camada de multipolígonos. Para além disso, precisava que os mesmos viessem ordenados numericamente começando em 1, e com as respectivas coordenadas XY.

[![Screenshot from 2015-11-05 23:58:19](/images/2015/11/screenshot-from-2015-11-05-235819.png)
](/images/2015/11/screenshot-from-2015-11-05-235819.png)

A tarefa parecia-me trivial – bastaria usar a função [ST_DumpPoints()](http://postgis.net/docs/ST_DumpPoints.html) para obter os vértices – não fosse o facto dos polígonos em postGIS terem um vértice repetido (obrigatoriamente o último vértice tem de ser igual primeiro) que não me interessava mostrar.

Depois de algumas tentativas, cheguei à seguinte _query_:

[code language="SQL"]
CREATE OR REPLACE VIEW public.my_polygon_vertexes AS
WITH t AS -- Transformar os polígonos em sets de pontos
    (SELECT id_polygon,
            st_dumppoints(geom) AS dump
     FROM public.my_polygons),
f AS -- Tirar geometria e indices dos sets de pontos
    (SELECT t.id_polygon,
           (t.dump).path[1] AS part,
           (t.dump).path[3] AS vertex,
           (t.dump).geom AS geom
     FROM t)
-- Obter todos os pontos filtrando o último ponto de cada parte das geometrias
SELECT row_number() OVER () AS gid, -- Criar um identificador único
       f.id_polygon,
       f.part,
       f.vertex,
       ST_X(f.geom) as x, -- extra: obter a coordenada X do ponto
       ST_Y(f.geom) as y, -- extra: obter a coordenada Y do ponto
       f.geom::geometry('POINT',4326) as geom -- garantir o tipo de geometria
FROM f
WHERE (f.id_polygon, f.part, f.vertex) NOT IN
      (SELECT f.id_polygon,
              f.part,
              max(f.vertex) AS max
       FROM f
       GROUP BY f.id_polygon,
                f.part);
[/code]

A parte interessante ocorre na cláusula WHERE, basicamente, da listagem total de vértices, são escolhidos apenas os que não se encontram numa lista de vértices com o valor de índice máximo do vértice por polígono e por parte, ou seja, o último vértice que cada parte de cada polígono.

Eis o resultado:

[![Screenshot from 2015-11-05 23:58:40](/images/2015/11/screenshot-from-2015-11-05-235840.png)
](/images/2015/11/screenshot-from-2015-11-05-235840.png)

A vantagem desta abordagem (via PostGIS) em vez de usar a ferramenta "Polígonos  para linhas", seguida de "Linhas para Ponto" é que basta alterar a minha camada de polígonos, e gravá-la, para ver os vértices a serem actualizados automaticamente. É nestas coisas que adoro o [Postgis](http://postgis.net/).
