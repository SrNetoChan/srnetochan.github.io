---

date: 2013-12-03 23:09:47+00:00
title: Triggers para que vos quero...
tags:
- Postgis
- trigger
---

Há já algum tempo que queria estudar a funcionalidade de triggers em [PostgreSQL](http://www.postgresql.org/). A grosso modo, tinha ideia que permitiam executar comandos de forma automática, sempre que se alterasse determinada tabela, mas desconhecia os mecanismos para o fazer. Uma das aplicações que me veio à ideia foi a de usar triggers para manter actualizado atributos geométricos como a área ou o comprimento. Quando editamos de elementos que contêm atributos relacionados com as dimensões, forma ou localização das suas geometrias (área, perímetro, comprimento), é muito fácil esquecermo-nos de os actualizar depois da edição. Se mais tarde usarmos esses atributos para realizar alguma análise, este esquecimento pode levar a resultados errados.Como exemplo, vou criar um trigger para actualizar os atributos "área", "latitude" e "longitude" de uma tabela de polígonos.A primeira coisa a fazer é criar uma função que execute o que pretendemos. No caso em questão, usei a seguinte:

    CREATE OR REPLACE FUNCTION update_geometry_fields()
    RETURNS trigger;
    $BODY$
    DECLARE
    lat_long TEXT;
    BEGIN
    -- Cálculo da área da geometria
    NEW.area = st_area(NEW.geom);

    -- Cálculo da latitude e longitude do centroíde da geometria em graus minutos e segundos
    lat_long := ST_AsLatLonText(st_transform(st_centroid(NEW.geom), 4326));
    NEW.latitude = split_part(lat_long,' ',1);
    NEW.longitude = split_part(lat_long,' ',2);

    RETURN NEW;
    END;
    $BODY$
    LANGUAGE plpgsql VOLATILE

Depois, é necessário criar o trigger que despolete a função:

    CREATE TRIGGER update_epvu_sgev_geom_fields
    BEFORE INSERT OR UPDATE OF geom
    ON epvu.sgev
    FOR EACH ROW
    EXECUTE PROCEDURE update_geometry_fields();

O trigger, quando lido em inglês, é bastante simples de entender. Antes de inserir uma linha nova, ou actualizar a geometria (geom) de uma linha existente da tabela "epvu.sgev", executa a função update_geometry_fields() De notar que a criação do triggers (e respectivas funções) pode ter variações. Em primeiro lugar, os triggers podem ser despoletados antes ou depois de um INSERT, DELETE ou UPDATE numa tabela. Em segundo, podem executar a função sobre toda a tabela ou apenas nas linhas em questão. Para ilustrar estas diferenças, mais um exemplo. Com o objectivo de optimizar a impressão em mapas no [QGIS](www.qgis.org), através da nova funcionalidade de [atlas](http://docs.qgis.org/testing/en/docs/user_manual/print_composer/print_composer.html#atlas-generation) do print composer, criei uma consulta para agregar vários polígonos com base num atributo ("codigo") e me determinasse se os multi-polígonos resultantes encaixava melhor numa folha ao alto ou deitado. Na tentativa de tornar o processo mais rápido, pensei em gravar a consulta como tabela mantê-la actualizada sempre que alguma alteração pertinente ocorresse através de um trigger. A função a usar no trigger era pouco mais que a consulta em si:

    CREATE OR REPLACE FUNCTION epvu.refresh_geom_paginas_prestadores()
    RETURNS trigger AS
    $BODY$
    BEGIN
    TRUNCATE epvu.geom_paginas_prestadores restart identity;
    INSERT INTO epvu.geom_paginas_prestadores (codigo, formato, geom)
    (WITH g as
    (SELECT (st_union(st_makevalid(geom))) AS geom,
        codigo
     FROM
        epvu.sgev
     GROUP BY codigo
    )
    SELECT
        g.codigo,
        CASE WHEN abs(ST_XMax(g.geom)-ST_XMin(g.geom)) > abs(ST_YMax(g.geom)-ST_YMin(g.geom)) THEN
            'Landscape'
        ELSE
            'Portrait'
        END as formato,
        st_multi(g.geom) as geom
    FROM g);
    RETURN NEW;
    END;
    $BODY$
    LANGUAGE plpgsql VOLATILE

Neste caso, a função deve ser despoletada sempre que forem feitas alterações à tabela que usada na consulta (epvu.sgev) e que possam alterar os seus resultados. Assim, sempre que haja introdução (INSERT) ou eliminação (DELETE) de registos, ou que sejam alterados (UPDATE) os campos da geometria (geom) e "codigo", o trigger executa uma única vez a função descrita acima:

    CREATE TRIGGER actualiza_paginas_update
    AFTER INSERT OR UPDATE OF geom, codigo OR DELETE
    ON epvu.sgev
    FOR EACH STATEMENT

**Nota**: Depois de alguns teste, cheguei à conclusão que, dado o número reduzido de registos que tinha, era mais rápido usar uma VIEW. Continuo no entanto a achar que, este tipo de triggers podem ser úteis para pre-processar consultas mais exigentes. Para mais informação sobre o uso de triggers, a [documentação do PostgreSQL](http://www.postgresql.org/docs/9.3/static/sql-createtrigger.html) é um excelente ponto de partida.



