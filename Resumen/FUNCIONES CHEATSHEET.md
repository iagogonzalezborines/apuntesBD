

AVG

Devuelve el valor promedio de la columna especificada

`SELECT AVG(marks) from students where subject = ‘English’;`

MIN

Devuelve el valor más pequeño de la columna especificada

`SELECT MIN(price) from product WHERE product_category = ‘shoes’;`

MAX

Devuelve el valor más grande de la columna especificada

`SELECT MAX(quantity), product_name from inventory;`

COUNT

Devuelve el número de filas que satisfacen la consulta

Muestra un número total de registros en la tabla de empleados.  
  
`SELECT COUNT(*) from employee;`  
  
Mostrar el número de empleados cuyo salario es mayor a 20000  
  
`SELECT COUNT(*) from employee where salary > 20000;`

SUM

Devuelve la suma de los valores de la columna numérica especificada

`SELECT SUM(marks) from students where subject = ‘English’;`


## En otros aspectos...

Podemos usar ROUND para redondear 
``` sql
SELECT ROUND(Dato u Operacion, (Decimales que queremos)) FROM (Tabla) WHERE 1; 
```

TRUNCATE para truncar