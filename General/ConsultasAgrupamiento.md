______________________________________________________________________
TendaBD
--

1. Seleccionar da táboa artigos as cores e o prezo medio de venda dos artigos de cada cor (con dous decimais).
``` sql
SELECT art_color AS Color, ROUND(AVG(art_pv), 2) AS MediaPrecioVenta,
FROM artigos
WHERE art_color is not null
GROUP BY art_color;
```



2. Seleccionar da táboa artigos as cores e o prezo medio de venda dos artigos de cada cor (con dous decimais), excluíndo aos artigos que teñan un prezo de compra superior a 50 euros. 
``` sql

SELECT art_color AS Color, ROUND(AVG(art_pv), 2) AS MediaPrecioVenta
FROM artigos
WHERE art_color is not null and art_pc <= 50
GROUP BY art_color;
```
	


3. Mostrar as cidades nas que existen clientes e o número de clientes que hai en cada unha delas. Clasificar a saída en orden decrecente polo número de clientes.
```sql
SELECT clt_poboacion as Cidades , count(clt_id) as NumeroCliente
FROM clientes  
GROUP BY clt_poboacion 
ORDER BY NumeroCliente desc

```



4. Mostrar código de artigo, nome de artigo, suma dos importes das vendas de cada artigo sen aplicar o desconto, suma dos importes das vendas de cada artigo despois de aplicar o desconto, e desconto efectuado, para os artigos vendidos entre 1-1-2015 e 25-5-2015.
```sql
SELECT ar.art_codigo AS CodigoArtigo, ar.art_nome AS NomeArtigo SUM(dv.dev_prezo_unitario*dv.dev_cantidade) AS ImporteTotal,
ROUND(SUM(dv.dev_prezo_unitario*dv.dev_cantidade*(1-dv.dev_desconto/100)), 2) 
AS Cobrado, ROUND(sum(dv.dev_prezo_unitario*dv.dev_cantidade (dv.dev_desconto/100)), 2)
AS Descuento
FROM artigos AS ar JOIN detalle_vendas AS dv ON (dev_artigo = art_codigo) JOIN
vendas AS vn ON (ven_id = dev_venda)
WHERE date(vn.ven_data) between "1-1-2015" and "25-5-2015"
GROUP BY CodigoArtigo, NomeArtigo;

```

(ESTA CONSULTA NO FURRULA)


6. Seleccionar da táboa artigos as cores e o prezo medio de venda dos artigos de cada cor, para as cores que teñan o prezo medio maior que 100 euros.
```sql
SELECT artigos.art_color AS ColorArtigo	ROUND(AVG(artigos.art_pv), 2) AS MediaPrecio
FROM artigos
WHERE artigos.art_pv is not null and artigos.art_color is not null
GROUP BY ColorArtigo
HAVING avg(art_pv)>100;
````


7. Mostrar as tendas que fixeron máis de 2 vendas no mes de maio de 2015. Para cada tenda débese mostrar: numero de tenda, número de vendas, número de artigos diferentes vendidos e a suma de unidades vendidas nese período de tempo.
```sql
SELECT ven.ven_tenda as NumeroTenda, COUNT(distinct dv.dev_artigo) as NumeroArtigosVendidos, count(distinct dv.dev_venda) as NumeroVendas
FROM vendas as ven join detalle_vendas as dv on (ven_id = dev_venda)
WHERE MONTH(ven.ven_data) = 5 and YEAR(ven_data)=2015
GROUP BY NumeroTenda
HAVING (NumeroVendas)>2;
```

________________________________________________________________________________________

Traballadores
--


1. Mostrar o número de empregados que utiliza cada extensión telefónica.
```sql
SELECT COUNT(empNumero), empExtension AS extension
FROM empregado
GROUP BY empExtension;
```


2. Mostrar o número de empregados que teñen 0, 1, 2, 3, ... fillos. 
```sql
SELECT COUNT(empNumero) as Numero_Empregados, empFillos as Numero_Fillos_Empregado
FROM empregado
GROUP BY empFillos
ORDER BY empFillos ASC;
```


4. Mostrar o número de departamentos que dependen de cada centro. 

```sql
SELECT COUNT(dpt.depNumero) as NumeroDepartamentos, cn.cenNome nomeCentro
FROM departamento as dpt JOIN centro AS cn ON (depCentro = cenNumero)
GROUP BY cn.cenNumero;
```

5. Seleccionar, para cada departamento, o maior salario, o menor salario e a diferenza que hai entre o salario máis alto e o salario máis baixo. 
```sql
SELECT dpt.depNumero as numeroDepartamento, MAX(em.empSalario) as MaximoSalario, MIN(em.empSalario) as MinimoSalario
FROM departamento as dpt JOIN empregado AS em ON (depNumero  = empDepartamento)
GROUP BY dpt.depNumero;
```


7. Mostrar, para cada departamento, a cantidade que queda do presuposto despois de restar o importe dos salarios e comisións a pagar aos empregados. 
```sql
SELECT dpt.depNumero AS numeroDepartamento, dpt.depNome AS NomeDepartamento,(dpt.depPresuposto - SUM(em.empSalario) - SUM(empComision)) AS RestoPresuposto
FROM departamento AS dpt JOIN empregado AS em ON (depNumero = empDepartamento)
GROUP BY dpt.depNumero , em.empNumero;
```


7. Mostrar número e nome dos departamentos que teñan 5 empregados. 
```sql
SELECT dpt.depNumero AS numeroDepartamento,dpt.depNome AS NomeDepartamento,COUNT(em.empNumero) as NumeroEmpregados
FROM departamento AS dptJOIN empregado AS em ON (depNumero = empDepartamento)GROUP BY dpt.depNumero
HAVING NumeroEmpregados=5;
```



8. Para as extensións telefónicas que son utilizadas por máis dun empregado, mostrar o número de empregados que a comparte.
````sql
SELECT 
em.empExtension as Extension, count(empNumero) as NumeroEmpregados
FROM empregado AS em 
GROUP BY empExtension
HAVING numeroEmpregados>1 ;
```

