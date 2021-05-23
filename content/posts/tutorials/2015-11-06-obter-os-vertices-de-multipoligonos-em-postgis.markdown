---

date: 2015-11-06 00:49:01+00:00
title: Getting multipolygon vertexes using PostGIS
tags:
- Postgis
---

Today I needed to create a view in [PostGIS](http://postgis.net/) that returned the vertexes of a multi-polygon layer. Besides, I needed that they were numerically ordered starting in 1, and with the respective XY coordinates.

![Screenshot from 2015-11-05 23:58:19](/images/2015/11/screenshot-from-2015-11-05-235819.png)


It seemed to be a trivial task – all I would need was to use the [ST_DumpPoints()](http://postgis.net/docs/ST_DumpPoints.html) function to get all vertexes – if it wasn't for the fact that PostGIS polygons have a duplicate vertex (the last vertex must be equal to the first one) that I have no interess in showing.

After some try-and-fail, I came up with the following query:

[code language="SQL"]
CREATE OR REPLACE VIEW public.my_polygons_vertexes AS
WITH t AS -- Transfor polygons in sets of points
    (SELECT id_polygon,
            st_dumppoints(geom) AS dump
     FROM public.my_polygons),
f AS -- Get the geometry and the indexes from the sets of points
    (SELECT t.id_polygon,
           (t.dump).path[1] AS part,
           (t.dump).path[3] AS vertex,
           (t.dump).geom AS geom
     FROM t)
-- Get all points filtering the last point for each geometry part
SELECT row_number() OVER () AS gid, -- Creating a unique id
       f.id_polygon,
       f.part,
       f.vertex,
       ST_X(f.geom) as x, -- Get point's X coordinate
       ST_Y(f.geom) as y, -- Get point's Y coordinate
       f.geom::geometry('POINT',4326) as geom -- make sure of the resulting geometry type
FROM f
WHERE (f.id_polygon, f.part, f.vertex) NOT IN
      (SELECT f.id_polygon,
              f.part,
              max(f.vertex) AS max
       FROM f
       GROUP BY f.id_polygon,
                f.part);
[/code]

The interesting part occurs in the WHERE clause, basically, from the list of all vertexes, only the ones not included in the list of vertexes with the maximum index by polygon part are showed, that is, the last vertex of each polygon part.

Here's the result:

[![Screenshot from 2015-11-05 23:58:40](/images/2015/11/screenshot-from-2015-11-05-235840.png)
](/images/2015/11/screenshot-from-2015-11-05-235840.png)

The advantage of this approach (using PostGIS) instead of using "Polygons to Lines" and "Lines to points" processing tools is that we just need to change the polygons layer, and save it, to see our vertexes get updated automatically. It's because of this kind of stuff that I love [PostGIS](http://postgis.net/).
