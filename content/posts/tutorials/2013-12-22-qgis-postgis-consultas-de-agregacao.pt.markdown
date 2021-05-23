---

date: 2013-12-22 17:43:50+00:00
title: 'QGIS + Postgis: Consultas de agregação '
---

Quando através de uma consulta SQL a uma base de dados postgres\postgis se procede a uma agregação (através do uso da cláusula GROUP BY) é quase certo perder a chave primária da tabela original (geralmente o gid). No entanto, para visualizar o resultado de consultas SQL em QGIS é necessário que exista um campo com valores inteiros distintos para usar como identificadores únicos. Assim, para ultrapassar este contratempo, há que criar uma coluna com essas características.

Essa coluna pode ser feita usando a função ROW_NUMBER(), da seguinte forma:

[code language="SQL"]
WITH r as (SELECT
               campo1,
               (ST_Dump(ST_Union(t.geom))).geom as geom
           FROM
               tabela_1 as t
           GROUP BY
               campo1)
SELECT
    ROW_NUMBER() OVER() as id,
    r.*
FROM r;
[/code]

Copiando toda para a expressão na janela SQL do DB Manager (Base de dados > Gestor BD > Janela SQL), é possível usar o campo id como identificador único.

[![QGIS_Janela_SQL](/images/2013/12/qgis_janela_sql1.png?w=584)
](/images/2013/12/qgis_janela_sql1.png)

[![AgregacaoSQL_Qgis](/images/2013/12/agregacaosql_qgis.png?w=584)
](/images/2013/12/agregacaosql_qgis.png)

