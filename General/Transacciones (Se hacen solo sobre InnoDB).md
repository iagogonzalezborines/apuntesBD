________________________________________________________________________________________
Ejemplos
------------

1. 

```sql
BEGIN;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (4, "cuarto", null);
ROLLBACK;
SELECT * FROM tbl_ProbaTransaccions;
```
___________________________________________________

2. 

```sql
BEGIN;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (4, "cuarto", null);
SELECT * FROM tbl_ProbaTransaccions;
```

(cae la conexión*)

-No se agregan los datos 
___________________________________________________
3. 

```sql
BEGIN;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (4, "cuarto", null);
COMMIT;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (5, "quinto", null);
COMMIT;
SELECT * FROM tbl_ProbaTransaccions;
```

__________________________________________________
-*Término* _SAVEPOINT_: Perminte nombrar un paso

4. 

```sql
START TRANSACTION;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (6, "sexto", null);
savepoint UNO;
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (7, "septimo", null);
INSERT INTO tbl_ProbaTransaccions (id, s, si) VALUES (8, "octavo", null);
ROLLBACK TO UNO;
SELECT * FROM tbl_ProbaTransaccions;
```
_________________________________________________
-*Término* _LOCK TABLES_: Permite limitar la alteración de las tablas.

- READ / WRITE ---> (INSERT, UPDATE, DELETE)

-*Término* _UNLOCK TABLES_: Desbloquea todas las tablas al mismo tiempo.

-**HAY TIPOS DE BLOQUEO**: PÁG 9 de Transaccions.pdf

Para trabajar con el LOCK debemos crear mas usuarios 

```sql
CREATE USER 'usuario1'@'localhost' IDENTIFIED BY 'usuario1'; 
CREATE USER 'usuario2'@'localhost' IDENTIFIED BY 'usuario2'; 
CREATE USER 'usuario3'@'localhost' IDENTIFIED BY 'usuario3'; 
SELECT * FROM mysql.user; 
GRANT ALL ON bd_ProbaTransaccions.* TO 'usuario1'@'localhost'; 
GRANT ALL ON bd_ProbaTransaccions.* TO 'usuario2'@'localhost'; 
GRANT ALL ON bd_ProbaTransaccions.* TO 'usuario3'@'localhost';
```




