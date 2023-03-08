________________________________________________________________________________________
Traballadores
------------------


9. Borra o empregado co número 380. 
```sql
DELETE FROM empregado 
WHERE empNumero = 380;

```



10. Borrar da táboa dos empregados aos que teñan cumpridos os 60 anos. 

```sql
DELETE FROM empregado 
WHERE YEAR(curdate()) - YEAR(empDataNacemento)>=60;
```




11. Escribir unha única sentenza que permita borrar da táboa departamento o departamento número 121 e da táboa empregado todos os empregados que traballan nese departamento. 
```sql
DELETE em , dep
FROM empregado AS em STRAIGHT_JOIN
departamento AS dep 
WHERE em.empDepartamento = dep.depNumero AND dep.depNumero = 121;
```



12. Executar o seguinte script para poder crear unha táboa temporal co nome empregado_120: • create temporary table empregado_120 like empregado; • Inserir na táboa empregado_120 os datos de todas as filas da táboa empregado que teñan o valor 120 na columna empDepartamento;
```sql
INSERT INTO empregado_120 () 
SELECT *
FROM empregado 
WHERE empDepartamento = 120;
```


