_____________________________________________________________________________________
TendaBD
----------


1. Executar a seguinte sentenza, analizar os erros que provocan, e indicar as medidas que se deberían de adoptar para manter a integridade e consistencia dos datos.


```SQL
insert into clientes ( clt_id, clt_cif, clt_apelidos, clt_nome, clt_enderezo, clt_cp, clt_poboacion, clt_pais, clt_alta) values (92, '33956665D','Varela Montero','Luisa','Rua Vella, 5-2º', '15006', 'Coruña',73,curdate()); 
```

- /*El clt_id se repite, además es autoincremental
insert into clientes (clt_cif, clt_apelidos, clt_nome, clt_enderezo, clt_cp, clt_poboacion, clt_pais, clt_alta) 
values ('33956665D','Varela Montero','Luisa','Rua Vella, 5-2º', '15006', 'Coruña',73,curdate());



2. Executar a seguinte sentenza, analizar os erros que provocan, e indicar as medidas que se deberían de adoptar para manter a integridade e consistencia dos datos. 
```SQL
insert into clientes ( clt_cif, clt_apelidos, clt_nome, clt_enderezo, clt_cp, clt_poboacion, clt_pais, clt_alta) values ('16137107P','Nuñez Castro','Maria','Rua Nova, 22 - 5º','27001', 'Lugo',73,curdate()); 
```



- /*El cif se repetía por lo tanto igual se está buscando actualizar la información o el cif es un error

```SQL
insert into clientes ( clt_cif, clt_apelidos, clt_nome, clt_enderezo, clt_cp, clt_poboacion, clt_pais, clt_alta) 
values (_null_,'Nuñez Castro','Maria','Rua Nova, 22 - 5º','27001', 'Lugo',73,curdate()); 
```



3. Executar a seguinte sentenza, analizar os erros que provocan, e indicar as medidas que se deberían de adoptar para manter a integridade e consistencia dos datos.. 


```SQL
insert into vendas (ven_tenda, ven_empregado, ven_cliente, ven_data, ven_factura) values (24,null,55,now(),null); 
```

- /*El empregado no puede ser null, se tiene que añadir un empleado que exista ya que es una fk

```SQL
insert into vendas (ven_tenda, ven_empregado, ven_cliente, ven_data, ven_factura) 
values (24,_8_,55,now(),null);
``` 

4. Executar a seguinte sentenza, analizar os erros que provocan, e indicar as medidas que se deberían de adoptar para manter a integridade e consistencia dos datos. 
```SQL

insert into vendas (ven_tenda, ven_empregado, ven_cliente, ven_data, ven_factura) values (24,10,155,now(),null); 
```

- /*Se está haciendo referencia a un cliente que no existe.

```SQL
insert into vendas (ven_tenda, ven_empregado, ven_cliente, ven_data, ven_factura)
 values (24,10,_103_,now(),null); 
```




5. Executar a seguinte sentenza, analizar os erros que provocan, e indicar as medidas que se deberían de adoptar para manter a integridade e consistencia dos datos. 

- /*La consulta no da error, solo agrega los valores por default

```SQL
insert into vendas (ven_tenda, ven_empregado, ven_cliente) values (24,10,55);
```