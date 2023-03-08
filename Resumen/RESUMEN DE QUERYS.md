
1.   --CONSULTA COMUN--
```sql  
SELECT (Lo que quieres) FROM (Tabla) WHERE (Condición);
```


## Uniendo tablas

Las dos valen para lo mismo, es importante recordar que el uso de las subconsultas es mejor cuando la consulta es mas corta ya que al hacer subconsultas se utillizan bastantes lineas de sql y por lo tanto siempre es mejor simplificar a la hora de hacer las querys por lo cual usar el JOIN en una consulta mas larga siempre es mejor

2. --CONSULTA MULTITABLA--
	``` sql  
SELECT (Lo que quieres)  FROM (tabla) join (tabla) on (igualtabla1=igualtabla2) WHERE (condicion); 
```
[[JOIN CHEATSHEET]]

3. --SUBCONSULTAS--
	``` sql  
SELECT (Lo que quieres)  FROM (tabla) WHERE igualtabla1 IN (SELECT(igualtabla2) FROM (tabla) WHERE (condicion)) ; 
```


## Agrupando por dato, consultas group by

Estas consultas buscan agrupar por cierto dato

Ejemplo:

``` sql

SELECT art_color AS Color, ROUND(AVG(art_pv), 2) AS MediaPrecioVenta
FROM artigos
WHERE art_color is not null and art_pc <= 50
GROUP BY art_color;
```

En este caso aparece el precio medio de venta por color de articulo, estamos mostrando los datos que parten de cierto dato como en este caso es el color. 
La consulta nos da el precio medio de venta de los articulos por color.
``` sql 
GROUP BY
```

4. --AGRUPAMIENTO--
	``` sql

SELECT (Lo que quieres) AS (Alias), (Dato que viene del primero) AS (Alias)
FROM (Tabla)
WHERE (Condicion)
GROUP BY (Lo que quieres);
```
En este caso podemos utilizxar funciones como ROUND, AVG, SUM etc... ya que solo estamos buscando por una row y los datos que vamos a ver son unicos ya que estamos haciendo para cada uno del primer select usando el GROUP BY 
[[FUNCIONES CHEATSHEET]]

