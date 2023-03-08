__________________________________________________________________________
TendaBD
----------

1. Seleccionar código e peso dos artigos que teñen o peso máis pequeno que o peso do artigo de código '077WN45'. 
```sql
SELECT 
    art_codigo AS CodigoArtigo, art_peso AS PesoArtigo
FROM
    artigos
WHERE
    art_peso < (SELECT 
            (art_peso)
        FROM
            artigos
        WHERE
            art_codigo = '077WN45')
```


2. Seleccionar código, nome, peso e cor dos artigos da mesma cor que o artigo de código '242C283', e que teñan un peso maior ou igual que o peso medio de todos os artigos. 

```sql
SELECT 
    art_nome AS NomeArtigo,
    art_codigo AS CodigoArtigo,
    art_peso AS PesoArtigo,
    art_color AS ColorArtigo
FROM
    artigos
WHERE
    art_color = (SELECT 
            (art_color)
        FROM
            artigos
        WHERE
            art_codigo = '242C283')
        AND art_peso >= (SELECT 
            (AVG(art_peso))
        FROM
            artigos);
```


3. Seleccionar código da tenda e nome do xerente das tendas nas que se vendeu polo menos unha unidade do artigo de código ' 077WN45'. 
```sql

SELECT 
    td.tda_id AS CodigoTenda,
    em.emp_nome AS NomeXerente,
    td.tda_xerente AS CodigoXerente
FROM
    tendas AS td
        JOIN
    empregados AS em ON (td.tda_xerente = em.emp_id)
WHERE
    td.tda_id IN (SELECT 
            (ven_tenda)
        FROM
            vendas
        WHERE
            ven_id IN (SELECT 
                    (dev_venda)
                FROM
                    detalle_vendas
                WHERE
                    dev_artigo = '077WN45'))
```



4. Mostrar a lista de artigos cun prezo de venda maior que o prezo de venda do artigo máis barato de cor negra. Obter o mesmo resultado nos dous casos seguintes:  Utilizando any.  Utilizando a función min(). 

```sql
SELECT 
    art_nome as NomeArtigo
FROM
    artigos
WHERE
	art_pv >  (SELECT 
            (min(art_pv))
        FROM
            artigos
        WHERE
            art_color like 'Negro')
```
_____________________________________________
```sql
SELECT 
    art_nome as NomeArtigo, art_codigo as codigoArtigo
FROM
    artigos
WHERE
	art_pv > any (SELECT 
            ((art_pv))
        FROM
            artigos
        WHERE
            art_color like 'Negro')
```


5. Seleccionar código de artigo, descrición do artigo e código do provedor para os artigos que subministra o provedor que ten o nome SEAGATE. 

```sql
SELECT 
    art_codigo AS codigoArtigo,
    art_nome AS NomeArtigo,
    art_provedor AS Provedor
FROM
    artigos
WHERE
    art_provedor = (SELECT 
            (prv_id)
        FROM
            provedores
        WHERE
            prv_nome = 'SEAGATE');
```


6. Mostrar información do artigo máis caro, Seleccionando o seu código, nome, prezo de venta e nome do provedor que o subministra. 
```sql
SELECT 
    art_codigo AS codigoArtigo,
    art_nome AS NomeArtigo,
    art_pv as precioArtigo,
    art_provedor AS Provedor,
    prv_nome as nomeProvedor
FROM
    artigos join provedores on (prv_id = art_provedor)
WHERE
    art_pv = (SELECT 
            (max (art_pv))
        FROM
            artigos
```


7. Mostrar nome e prezo de venda dos artigos que teñen un prezo de venda comprendido entre o prezo do artigo '0713242' e a media de prezos de todos os artigos. Os datos deben mostrarse ordenados alfabeticamente polo nome do artigo. 

```sql
SELECT 
    art_codigo AS codigoArtigo,
    art_nome AS NomeArtigo,
    art_pv AS precioArtigo
FROM
    artigos
WHERE
    art_pv BETWEEN (SELECT 
            (art_pv)
        FROM
            artigos
        WHERE
            art_codigo = '0713242') AND (SELECT AVG(art_pv))
```

8. Obter a lista de provedores que subministran como mínimo un artigo de cor negra. 

```sql
SELECT 
    prv_id AS idProvedor, prv_nome AS nomeProvedor
FROM
    provedores
WHERE
    prv_id IN (SELECT 
            (art_provedor)
        FROM
            artigos
        WHERE
            art_color = 'negro')
```


9. Mostrar identificador de cliente, apelidos e nome na mesma columna separados por coma, para os clientes que só teñen unha venda. O resultado estará ordenado polo identificador do cliente. 

```sql
SELECT 
    clt_nome AS nomeCliente, clt_id as idCliente
FROM
    clientes
WHERE
    clt_id IN (SELECT (ven_cliente) from vendas group by ven_cliente having count(ven_id)>1 )
```

10. Mostrar identificador e nome dos clientes que fixeron algunha compra despois do día en que o cliente número 6 fixo a súa última compra. 
```sql

SELECT 
    clt_nome AS nomeCliente, clt_id AS idCliente
FROM
    clientes
WHERE
    clt_ultima_venda > (SELECT 
            (clt_ultima_venda)
        FROM
            clientes
        WHERE
            clt_id = 6)  
```


11. Mostrar os nomes dos xerentes das tendas nas que se fixo algunha venta. 


```sql
SELECT 
    emp_nome AS nomeXerente
FROM
    empregados
WHERE
    emp_id IN (SELECT 
            (tda_xerente)
        FROM
            tendas
        WHERE
            tda_id IN (SELECT 
                    (ven_tenda)
                FROM
                    vendas
                GROUP BY ven_id
                HAVING COUNT(ven_id) = 1))
```


12. Importe total das vendas que se fixeron ao cliente LEANDRO FERREIRO BENITEZ 

```sql
SELECT 
    ROUND(SUM(dev_prezo_unitario * dev_cantidade * (1 - dev_desconto / 100)),
            2) AS total
FROM
    detalle_vendas
        JOIN
    vendas v ON detalle_vendas.dev_venda = v.ven_id
WHERE
    ven_cliente IN (SELECT 
            clt_id
        FROM
            clientes
        WHERE
            clt_nome = 'LEANDRO'
                AND clt_apelidos = 'FERREIRO BENITEZ');
```


___________________________________________________

Traballadores
-------------------

7. Seleccionar o nome e número de departamento dos empregados que pertenzan a un departamento cun presuposto comprendido entre os presupostos dos departamentos 122 e 121 (incluídos). Os datos deben mostrarse ordenados de menor a maior polo número do departamento. 


```sql
SELECT 
    depNome AS NomeDepartamento, depNumero AS NumeroDepartamento
FROM
    departamento
WHERE
    depPresuposto >= (SELECT 
            (depPresuposto)
        FROM
            departamento
        WHERE
            depNumero = 122)
        AND depPresuposto <= (SELECT 
            (depPresuposto)
        FROM
            departamento
        WHERE
            depNumero = 121)
ORDER BY depNumero ASC; 
```


8. Mostrar o número de departamento e o número de empregados dos departamentos que teñen un presuposto anual superior a 36000 euros. 


```sql
SELECT 
    empDepartamento AS NumeroDepartamento,
    COUNT(empNumero) AS numeroEmpregados
FROM
    empregado
WHERE
    empDepartamento IN (SELECT 
            (depNumero)
        FROM
            departamento
        WHERE
            depPresuposto > 36000)
GROUP BY empDepartamento;
```


9. Mostrar nome de departamento e de empregado para os empregados que traballan nalgún departamento que dependa do centro 'SEDE CENTRAL'. Os datos mostraranse ordenados por departamento e nome de empregado. 


```sql
SELECT 
    empDepartamento AS NumeroDepartamento,
    empNome AS NomeEmpregado
FROM
    departamento
        JOIN
    empregado ON empDepartamento = depNumero
WHERE
    empDepartamento IN (SELECT 
            (depNumero)
        FROM
            departamento
        WHERE
            depCentro IN (SELECT 
                    (cenNumero)
                FROM
                    centro
                WHERE
                    cenNome = 'SEDE CENTRAL'));
```

10. Mostrar número de empregados e suma dos salarios, comisións e fillos, para os departamentos nos que existe algún empregado cun salario base mensual maior de 2000 euros. 


```sql
SELECT 
    COUNT(empNumero) AS NumeroEmpregados,
    SUM(empSalario) AS TotalSalario,
    SUM(ifnull(empComision, 0)) AS TotalComision,
    SUM(empFillos) AS TotalFillos,
    depNumero AS NumeroDepartamento
FROM
    empregado
        JOIN
    departamento ON empDepartamento = depNumero
WHERE
    depNumero IN (SELECT 
            (empDepartamento)
        FROM
            empregado
        WHERE
            empSalario > 2000)
            group by depNumero;
```


11. Mostrar o nome de todos os directores de departamento ordenados polo número de departamento. Resolver a consulta: • con subconsultas. • sen subconsultas. 


```sql
SELECT 
    empNome AS NomeDirector
FROM
    empregado
WHERE
    empNumero IN ((SELECT 
            (depDirector)
        FROM
            departamento))
            order by empDepartamento;
```
_________________________________

```sql
SELECT 
    empNome AS NomeDirector, depNome AS Departamento
FROM
    empregado
        JOIN
    departamento ON empNumero = depDirector
ORDER BY depNumero;
```



12. Mostrar os nomes dos directores de departamentos que dependen dun centro de traballo que ten un nome que empeza pola letra 'S'. Resolver a consulta: • con subconsultas. • sen subconsultas. 

```sql
SELECT 
    empNome AS NomeDirector, depNome AS Departamento
FROM
    empregado
        JOIN
    departamento ON empNumero = depDirector
WHERE
    depCentro IN (SELECT 
            (cenNumero)
        FROM
            centro
        WHERE
            cenNome REGEXP '^S');

```

13. A empresa decide gratificar aos directores en funcións incrementando o seu salario base un 5%. Mostrar ordenados alfabeticamente, os nomes destes empregados, o seu salario, a gratificación que lle corresponde, e o salario final que resulta de sumarlle a nova gratificación ao salario. Resolver a consulta: • con subconsultas. • sen subconsultas. 


```sql
SELECT 
    empNome AS NomeDirector, empSalario as Salario, (empSalario * 0.5) as Gratificacion, (empSalario + (empSalario * 0.5)) as SalarioFinal
FROM
    empregado
        JOIN
    departamento ON empNumero = depDirector
order by empNome;
```
____________________________________

```sql
SELECT 
    empNome AS NomeDirector,
    empSalario AS Salario,
    (empSalario * 0.5) AS Gratificacion,
    (empSalario + (empSalario * 0.5)) AS SalarioFinal
FROM
    empregado
WHERE
    empNumero IN (SELECT 
            (depDirector)
        FROM
            departamento)
ORDER BY empNome;
```


14. Mostrar nome e salario dos empregados co salario base maior cá media dos soldos dos directores que están en funcións. 

```sql
SELECT 
    empNome AS Nome, empSalario AS Salario
FROM
    empregado
WHERE
    empSalario > (SELECT 
            (AVG(empSalario))
        FROM
            empregado
                JOIN
            departamento ON empNumero = depDirector)
```


15. Mostrar nome e salario+comisións dos empregados do centro “RELACIÓN CON CLIENTES ” que gañan máis de 1500 euros entre salario e comisións, ordenados por departamento, salario+comisión e nome. 


```sql
SELECT 
    empNome AS Nome, empSalario+ifnull(empComision, 0) AS 'Salario+Comision'
FROM
    empregado join departamento on empDepartamento = depNumero
WHERE
    depCentro > (SELECT 
            (cenNome)
        FROM
            centro
               WHERE cenNome = 'RELACION CON CLIENTES ') and empSalario > 1500;
```




16. Mostrar os nomes dos empregados que traballan no mesmo departamento que Lavinia Sanz ou Cesar Pons.



```sql
SELECT 
    empNome AS Nome
FROM
    empregado
WHERE
    empDepartamento IN (SELECT 
            (empDepartamento)
        FROM
            empregado
        WHERE
            empNome LIKE 'SANZ, LAVINIA'
                OR empNome LIKE 'PONS, CESAR')
```