---

date: 2013-12-20 15:35:42+00:00
title: Dissolver polígonos em Postgres\Postgis
tags:
- Postgis
---

Trata-se de um cenário muito recorrente em análise espacial. Tendo uma camada\tabela composta por diversos polígonos, queremos "juntá-los" de acordo com valores distintos de um ou mais atributos (exemplo: de uma camada com os limites de freguesias, queremos obter os concelhos, ou, da COS ao 3º nível, obter o 2º ou o 1º)

Este artigo tem como objectivo mostrar como fazê-lo em Postgres\Postgis.


## Tabela de exemplo


Como exemplo vou usar uma tabela como o seguinte formato:

[code language="SQL"]
CREATE TABLE tabela_1
    (gid serial PRIMARY KEY,
     campo1 character varying(128),
     campo2 integer,
     geom geometry(MultiPolygon,27493);
[/code]

[![tabela1_original_tabela](images/2013/12/tabela1_original_tabela.png)
](images/2013/12/tabela1_original_tabela.png)

[![tabela1_original](images/2013/12/tabela1_original.png?w=584)
](images/2013/12/tabela1_original.png)



# Dissolver todos os polígonos


Em primeiro lugar podemos simplesmente agregar todos os elementos num multi-polígono único. Para tal usamos a função [ST_Union()](http://postgis.refractions.net/docs/ST_Union.html).

[code language="SQL"]
SELECT
    ST_Union(t.geom) as geom
FROM
    tabela_1 as t;
[/code]

[![tabela1_union](images/2013/12/tabela1_union.png?w=584)
](images/2013/12/tabela1_union.png)



# Separar polígonos que não sejam contíguos


Se por outro lado não quisermos que o resultado apresente multi-polígonos usamos a função [ST_Dump()](http://postgis.refractions.net/docs/ST_Dump.html) recolhendo o campo da geometria.

[code language="SQL"]
SELECT
    (ST_Dump(ST_Union(t.geom))).geom as geom
FROM
    tabela_1 as t;
[/code]

[![tabela1_union_dump](images/2013/12/tabela1_union_dump.png?w=584)
](images/2013/12/tabela1_union_dump.png)



# Dissolver polígonos com base em valores dos campos


Se quisermos dissolver os polígonos que tenham valores iguais num ou mais campos, basta incluí-los na cláusula GROUP BY. Se quisermos que esses campos apareçam no resultado (geralmente queremos) há que referi-los no início do SELECT.

[code language="SQL"]
SELECT
    campo1,
    campo2,
    (ST_Dump(ST_Union(t.geom))).geom as geom
FROM
    tabela_1 as t
GROUP BY
    campo1,
    campo2;
[/code]

[![tabela1_union_by_value](images/2013/12/tabela1_union_by_value.png?w=584)
](images/2013/12/tabela1_union_by_value.png)

**Nota 1:** Para quem prefere usar interfaces gráficos, preencher formulários e clicar em botões, o uso de SQL para fazer este tipo de operações pode parecer demasiado complicado e até um pouco retrógrado. Mas uma coisa garanto, com alguma prática as dificuldades iniciais são ultrapassadas e os benefícios que se retiram deste tipo de abordagem são muito recompensadores.

**Nota 2:** Visualizar o resultado deste tipos consultas de agregação (que usam a cláusula GROUP BY) no QGIS pode ser desafiante, este [artigo](http://wp.me/p3kcmy-5p) explica como ultrapassar essa dificuldade.
