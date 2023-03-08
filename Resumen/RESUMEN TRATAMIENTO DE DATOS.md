1. --INSERT-- 
	Nos ayuda a insertar nuevos dtos en las tablas y se hace de la siguiente forma:
	```sql
INSERT INTO (tabla) ((campo1), (campo2), (campo3))
values (valor1, valor2, valor3)
```
	Es importante recalcar que el valor introducido tiene que coincidir con el tipo de dato especificado en el campo y que los valores no agregados adoptan el valor default dado.



2.  --DELETE--
	Vale para eliminar datos de la tabla
```sql
DELETE FROM (Tabla) 
WHERE (Condicion);
```

Borra todos los datos de la row en la cual se cumple la condicion

	 
	 
	


3. --UPDATE-- 
	Nos sirve para actualizar datos ya introducidos
```sql
UPDATE (Tabla)
SET 
    (Campo) = (Nuevo Valor)
WHERE
    (Condicion);
```

