## INNER JOIN

Este join nos permite unir dos tablas en un campo en especial
```sql
SELECT * FROM ARTIST AS ART
INNER JOIN ALBUM AS ALB
ON ART.ARTIST_ID = ALB.ARTIST_ID;
```
En este ejemplo unimos el propio ID de un artista con el ID del artista que aparece en la tabla ALBUM. 


## SELF JOIN

Estos se usan para comparar valores en una tabla a otros valores en esa misma tabla mediante la union de diferentes partes de la tabla 
```sql
SELECT
  alb1.artist_id,
  alb1.title AS alb1_title,
  alb2.title AS alb2_title
FROM album as alb1
INNER JOIN album as alb2
ON alb1.artist_id = alb2.album_id;
```

## LEFT JOIN

Devuelve todas las filas de la tabla de la izquierda y las filas coincidentes de la tabla de la derecha. Si no se encuentran filas que coincidan en la tabla de la derecha, se utilizan NULL.

```sql
SELECT *
FROM ARTIST AS ART
LEFT JOIN ALBUM AS ALB
ON ART.ARTIST_ID = ALB.ALBUM_ID;

```

## _Pro tip_:
Es buena opcion utilizar alias para las tablas definiendo este alias en la clausula FROM y luego utilizando este alias antes del campo en uso con un punto entre ambos como se muestra en el ejemplo anterior.