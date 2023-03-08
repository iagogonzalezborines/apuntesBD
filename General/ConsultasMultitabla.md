________________________________________________________________________________________

TendaBD
----------
1. Seleccionar a información de todos os artigos negros, xunto cos artigos que pesan máis de 5000 gramos.
```sql
SELECT ar.art_nome as Nome, ar.art_peso as Peso ,ar.art_numero as Numero 
FROM artigos as ar join provedores as pr
```



2. Seleccionar os artigos de cor negra e mostrar o seu número, nome e peso, así como o nome do provedor.
```sql 
SELECT artigos.art_nome as Nome, artigos.art_peso as Peso, artigos.art_codigo as Numero, provedores.prv_nome as provedor 
FROM artigos inner join provedores on (provedores.prv_id = art_provedor) 
WHERE art_color = "negro";

```



3. Seleccionar para todos os apelidos, nome e o nome da provincia na que residen. Os dous primeiros díxitos do código postal (clt_cp) corresponden ao código da provincia na que reside o cliente. Ordenar o resultado polo nome da provincia, e dentro da provincia, polos apelidos e nome, alfabeticamente.
```sql
SELECT cl.clt_nome as Nome, cl.clt_poboacion as Provincia, pr.pro_nome as Provincia, cl.clt_cp as CodPost 
FROM clientes as cl join provincias as pr on left((cl.clt_cp), 2) = pr.pro_id
WHERE 1 order by pr.pro_nome;
```




4. Mostrar para cada venda: nome e apelidos do cliente, día, mes, e ano da venda (cada un nunha columna).
```sql
SELECT clientes.clt_nome as Nome, clientes.clt_apelidos as Apellidos, DAY(vn.ven_data) as Dia,  MONTH(vn.ven_data) as Mes, YEAR(vn.ven_data) as Año 
FROM clientes join vendas as vn on (vn.ven_cliente=clientes.clt_id)

```

