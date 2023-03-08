______________________________________________________________________

1. Mostrar os datos de todas as tendas.
``` sql  
SELECT * FROM tendas WHERE 1; 
```

 



2.	Mostrar os nomes de todos os provedores.
``` sql
SELECT prv_nome FROM provedores WHERE 1; 
```
		
	




3.	 Obter a lista das poboacións nas que existen clientes.
``` sql
SELECT clt_poboacion FROM clientes WHERE 1;
```





4. Mostrar o prezo de venda de todos os artigos e o prezo que resultaría despois de aplicarlles un incremento do 10%
```sql
SELECT art_pc as precio, art_pc*0.1+art_pc as precioIncremento FROM artigos WHERE 1;
```





5.	Mostrar o número de cliente, apelidos e nome de todos os clientes de Madrid
```sql

SELECT clt_nome as Nome, clt_apelidos as Apelidos, clt_id as NumeroCliente  
FROM clientes 
WHERE clt_poboacion='Madrid';
```



6. Seleccionar o código, descrición e peso dos artigos que pesen máis de 500 gramos.	

```sql

SELECT art_codigo as CodigoArticulo, art_peso as PesoArticulo, art_nome as NomeArtigo 
FROM artigos 
WHERE art_peso>500;
```




7.	 Seleccionar todos os artigos que teñan prezo de venda superior ou igual ao dobre do prezo de compra.
```sql
	
SELECT art_codigo as CodigoArticulo, art_nome as NomeArtigo 
FROM artigos 
WHERE art_pv>art_pc or art_pv=2*art_pc;
```



8. Seleccionar apelidos, nome, poboación e desconto, de todos clientes de Asturias ou Valencia que teñan un desconto superior ao 2% ou que non teñan desconto.

	``` sql

SELECT clt_nome AS Nome, clt_apelidos AS Apelidos, clt_poboacion AS Poboacion
FROM clientes
WHERE (clt_poboacion = 'Asturias' OR clt_poboacion = 'Valencia') AND (clt_desconto > 2 OR clt_desconto = 0);
```




9.  Seleccionar todos os artigos de cor negra que pesen máis de 5000 gramos
``` sql
SELECT  art_nome as NomeArtigo
FROM artigos
WHERE art_color='negro' and art_peso>5000;
```




10. Obter todos os artigos que non son de cor negra ou que teñan un peso menor ou igual de 5000 gramos, é dicir, obter o resultado complementario da consulta anterior.
``` sql
SELECT art_nome AS NomeArtigo, art_color AS ColorArtigo
FROM artigos
WHERE art_peso <= 5000 AND art_color != 'negro';
```




11. Seleccionar os artigos que son de cor negra e pesan máis de 100 gramos, ou ben son de cor cyan.
``` sql
SELECT art_nome as NomeArtigo, art_color as ColorArtigo
FROM artigos
WHERE art_peso<100 or art_color="cyan";

```



12. Facer unha lista dos artigos que teñan un prezo de compra entre 12 e 18 euros, ambos prezos incluídos. 
``` sql
SELECT art_nome as NomeArtigo, art_pc as PrezoArtigo 
FROM artigos 
WHERE art_pc>=12 and art_pc<=18;
```



13. Mostrar unha lista de artigos de cor negra ou de cor cyan.
``` sql
SELECT art_nome as NomeArtigo, art_color as Color 
FROM artigos 
WHERE art_color = "negro" or art_color="cyan";

```



14. Buscar un cliente do que se descoñece o apelido exacto, pero se sabe que as dúas primeiras letras son 'RO'.
	```SQL
SELECT clt_apelidos as Nome 
FROM clientes 
WHERE clt_apelidos Like 'ro%';
```




15. Buscar clientes que teñan o nome de 5 letras, empezando por 'B' e terminando por 'A'.
``` sql
SELECT clt_nome as Nome 
FROM clientes 
WHERE clt_nome regexp '^b.{3}a$';

```




16. Buscar todos os artigos para os que non se gravou o seu color.
``` sql
SELECT art_color as Color 
FROM artigos 
WHERE art_color is null;
```




17. Clasificar os artigos tendo en conta o seu peso, por orde decrecente.
``` sql
SELECT art_nome as NomeArtigo, art_peso as Peso 
FROM artigos order by art_peso desc;
```



18. Mostrar código de artigo, nome, prezo de compra, prezo de venda e marxe de beneficio (prezo de venda – prezo de compra) dos artigos que teñen un prezo de compra superior a 3000 euros, ordenados pola marxe.		

``` sql
SELECT art_nome as NomeArtigo, art_codigo as codigoArtigo, art_pc as precioCompra, art_pv as precioVenta, (art_pv-art_pc) as Beneficio 
FROM artigos;
```




19. Clasificar nome, provedor, stock e peso dos artigos que teñen un peso menor ou igual de 1000 gramos, por orde crecente do provedor. Cando os provedores coincidan, deben clasificarse polo stock en orde decrecente.
``` sql
SELECT art_nome AS NomeArtigo, art_stock AS Stock, art_provedor AS provedor, art_peso AS Peso
FROM artigos
WHERE art_peso <= 1000
ORDER BY art_provedor ASC , art_stock DESC;
```




20. Seleccionar nome e apelidos dos clientes que teñan un apelido que empece por 'F' e remate por 'Z'.
``` sql
SELECT clt_apelidos as Apelido 
FROM clientes 
where clt_apelidos regexp '^f z$';

```





21. Seleccionar todos os artigos que leven a palabra LED, en maiúsculas, na súa descrición.
``` sql
SELECT art_nome 
FROM artigos 
WHERE art_nome like '%led%';
```




22. Seleccionar todos os artigos que teñan unha descrición que empece por 'CABI', sen diferenciar maiúsculas de minúsculas.
``` sql
SELECT art_nome 
FROM artigos 
WHERE art_nome like 'cabi%';
```




23. Seleccionar os clientes que teñan un apelido que empece pola letra 'a' ou pola letra 'f'
``` sql
SELECT clt_apelidos as Apelidos 
FROM clientes 
WHERE clt_apelidos like 'a%' or clt_apelidos like '%f';

```




24.  Seleccionar os clientes que teñan un apelido que non empece por 'a','b','c' ou 'd'.
 ``` sql
SELECT clt_apelidos as Apelidos 
FROM clientes 
WHERE clt_apelidos like 'a%' or clt_apelidos like 'd%' or clt_apelidos like 'b%' or clt_apelidos like 'c%';
```





25. Seleccionar os artigos que teñan un prezo de venta que remata en .00.
``` sql
SELECT art_pv as PrecioVenta, art_nome as NomeArtigo 
FROM  artigos where art_pv like'%.00';
```



26. Seleccionar os clientes que teñen un nome que teña exactamente 5 carácteres. 
``` sql
SELECT clt_nome as nome from clientes where clt_nome like '_____';	

```


27. Mostrar apelidos e nome dos clientes da tenda, nunha mesma columna separados por unhacoma, e o número de letras que ten o nome dos clientes.
 ``` sql

SELECT concat (clt_nome, ", ",clt_apelidos) as NomeApelidos, char(clt_nome) as "Numero de letras en nombre" 
FROM clientes;
```



28. Mostrar nomes e apelidos dos clientes en minúscula.
``` sql
SELECT LOWER(clt_nome) AS nome, LOWER(clt_apelidos) AS apelidos
FROM clientes
WHERE 1;
```




30. Mostrar todas as vendas que se fixeron no mes actual en calquera ano.
``` sql
SELECT ven_id as IdVenta, ven_data as fechaVenta 
FROM vendas 
WHERE MONTH(ven_data)=curdate();
```



31. Mostrar número, nome e prezo de venda (redondeado, sen decimais) dos artigos de cor negra.
	``` sql
SELECT art_codigo as CodigoArtigo, round(art_pv) as PrecioVenta, art_color as color 
FROM artigos
WHERE art_color like "negro";
```



32. Calcular a media dos pesos de todos os artigos.
``` sql
SELECT avg(art_peso) as mediaPeso 
FROM artigos;
```



33. Calcular a media do peso, o marxe máximo ( máxima diferenza entre o prezo de venda e o prezo de compra) e a diferenza que se dá entre o maior prezo de venda e o menor prezo de compra. Estes cálculos terán que facerse para aqueles artigos que teñan descrito a cor cun valor distinto do NULL.
``` sql

SELECT avg(art_peso) as mediaPeso, MAX(art_pv - art_pc) diferemnciaMAXPrecioVentaPrecioCompra, (max(art_pv)-min(art_pc)) as DiferenciaMaxVentaMinCompra 
FROM artigos;
```




34. Contar o número de cores distintas que existen na táboa de artigos.
``` sql
SELECT COUNT(art_color) 
FROM artigos;
```


35. Mostrar nome e cor dos artigos. Se a cor é descoñecida, débese mostrar o texto ‘DESCOÑECIDO´
``` sql	
SELECT art_nome as NomeArtigo, ifnull(art_color, 'Desconocido') as Color 
FROM artigos;
```