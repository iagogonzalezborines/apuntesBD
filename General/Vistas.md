Ejemplo 
--------------

```sql
CREATE OR REPLACE VIEW  empregados_organizacion ( or_nome, or_numero, or_departamento)
as
SELECT empNome, empNumero, empDepartamento
from empregado
where empDepartamento in (select(depNumero) from departamento where depNome like 'ORGANIZACION');
```


Traballadores
--------------

1. Crear unha vista sen CHECK OPTION para os empregados da empresa cos datos: número de empregado, nome, extensión telefónica, número e nome do departamento no que traballa. Utilizar a vista para: 
```sql
CREATE OR REPLACE VIEW empregados_contacto (con_nome , con_numero , con_departamento, con_ext, con_dep, con_dep_nome) AS
    SELECT 
        empNome, empNumero, empDepartamento, empExtension, empDepartamento, depNome
    FROM
        empregado join departamento on depNumero = empDepartamento
```

 Inserir os datos dun empregado no departamento 110. 

```sql
INSERT INTO empregados_contacto (con_nome , con_numero , con_departamento, con_ext)
values('Manrique', 1, 110, 123)
```


 Inserir os datos dun empregado no departamento 5.

```sql
INSERT INTO empregados_contacto (con_nome , con_numero , con_departamento, con_ext)
values('Ggig', 2, 5, 167)
``` 

## Ejercicios práctica
 1. Crear unha vista con CHECK OPTION asociada á táboa departamentos, que realiza as seguintes comprobacións: 
 
	  Existe o empregado que é director.
	 
	  Existe o centro do que depende. 
	 
	  O presuposto está entre 100000 e 2000000 euros. 
	 
	  O tipo de director só admite os valores P ou F. 
	 
	  Utilizar a vista para consultar os datos e comprobar se é posible utilizala con INSERT, DELETE ou UPDATE. 
	 
  
  3. Crear unha vista con CHECK OPTION que permita ver os datos dos empregados que traballan no departamento 111. Utilizar a vista para: 
	 
	  Modificar o número de fillos do empregado 240 que existe na táboa creada pola vista, poñendo 5 fillos. 
	 
	  Modificar o departamento do empregado 240 que existe na táboa creada pola vista, poñendo o departamento 5. 
	 
	  Modificar o número de fillos do empregado 900 que non existe na táboa creada pola vista nin na táboa empregado, poñendo 5 fillos. 
	 
  4. Crear unha vista sen CHECK OPTION que permita mostrar o número, nome e departamento no que traballan os empregados que levan máis de 20 anos traballando na empresa e teñen máis de 2 fillos. Utilizar a vista para:
   
	   Eliminar os datos do empregado 120 que existe na táboa empregado pero non existe na táboa creada pola vista. 
	  
	   Eliminar os datos do empregado 900 que non existe na táboa empregado nin tampouco na táboa creada pola vista. 
	  
	   Eliminar os datos do empregado 260 que existe na táboa creada pola vista.





TendaBD
-----------------

1. Crear unha vista sen CHECK OPTION cos seguintes datos, referidos aos artigos: código e nome do artigo e nome de provedor que o subministra. Utilizar a vista para:
```sql
CREATE OR REPLACE VIEW exercicio1 (art_codigo1 , art_nome1 , art_provedor1) AS
    SELECT 
        art_codigo, art_nome, art_provedor
    FROM
        artigos
            JOIN
        provedores ON art_provedor = prv_id
```

• Inserir os datos do artigo '4065091' que existe na táboa artigos, subministrado polo provedor 1 que existe na táboa de provedores.

```sql
insert into exercicio1 (art_codigo1, art_nome1, art_provedor1)
values ('4065091', 'artigo_novo', 1);
```



2. Crear unha vista sen CHECK OPTION asociada á táboa detalle_vendas que mostra código de artigo e número total de unidades vendidas ordenados por código. Utilizar a vista para consultar os datos e comprobar se é posible utilizala con INSERT, DELETE ou UPDATE.
```sql

CREATE OR REPLACE VIEW ejercicio2 (vistaTotal)
as select dev_artigo, SUM(dev_venda) as total from detalle_vendas
group by dev_artigos

```
3. Crear unha vista con CHECK OPTION que permita ver os datos das vendas realizadas na tenda 30. Utilizar a vista para: 

```sql
CREATE OR REPLACE VIEW ejercicio3Tenda30 (hven_id , hven_empregado , hven_cliente , hven_data) AS
    SELECT 
        hven_id, hven_empregado, hven_cliente, hven_data
    FROM
        hvendas
    WHERE
        hven_tenda = 30 WITH CHECK OPTION
```

• Modificar o cliente da venda 98 que existe na táboa creada pola vista poñendo o cliente 101 que non existe na táboa de clientes. 


```sql
INSERT INTO ejercicio3Tenda30 (hven_id , hven_empregado , hven_cliente , hven_data)
values(98, 1, 101, null)
```


4. Crear unha vista sen CHECK OPTION que permita mostrar código, nome, stock, data de alta e provedor dos artigos dados de alta antes do 1-1-2010, ordenados por provedor, stock (de forma descendente) e código. Utilizar a vista para:

```sql
CREATE OR REPLACE VIEW ejercicio4 (art_codigo4, art_nome4, art_stock4, art_alta4) AS
    SELECT 
        art_codigo, art_nome, art_stock, art_alta
    FROM
        artigos
    WHERE
        art_alta =  1-1-2010;
```


 Eliminar o artigo de código '00112233' que non existe na táboa que crea a vista.

```sql
DELETE  FROM ejercicio4 
where art_codigo4 = '00112233'
```

 Utilizar a vista para eliminar o artigo de código '07735Y4' que existe na táboa que crea a vista e está rexistrada nalgunha venda.

```sql
DELETE  FROM ejercicio4 
where art_codigo4 = '07735Y4'
```

 Utilizar a vista para eliminar o artigo de código '0001122' que existe na táboa que crea a vista e non ten rexistrada ningunha venda.

```sql
DELETE  FROM ejercicio4 
where art_codigo4 = '0001122'
```