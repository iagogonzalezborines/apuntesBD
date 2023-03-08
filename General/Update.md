Traballadores
------------------

3. Acórdase aumentar o salario a todos os empregados un 5% e a comisión un 6,5% como consecuencia da revisión do convenio. Facer as modificacións correspondentes na base de datos. 

```sql
UPDATE empregado 
SET empSalario = ROUND(empSalario + empSalario * 0.05, 2) AND empComision = ROUND(empComision + empComision * 0.065, 2);
```


4. Cambiarlle a data de ingreso na empresa do empregado número 752, asignándolle a data que corresponde ao día 1 do mes seguinte ao mes actual. 
```sql

UPDATE empregado SET empDataIngreso = last-day(curdate(), 1)
WHERE empNumero = 752;

```


5. Aumentar un 2% o salario a todos os empregados do departamento 120. 

```sql
UPDATE empregado 
SET 
    empSalario = ROUND(empSalario * 0.02, 2)
WHERE
    empDepartamento = 120;
```


6. Aumentarlle 50 euros á comisión de todos os empregados que traballen nun departamento que dependa do centro de traballo que ten por nome 'SEDE CENTRAL'. 

```sql
UPDATE empregado 
SET 
    empComision = ifnull(empComision, 0) + 50
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
                    cenNome LIKE 'SEDE CENTRAL'));
```



7. Reducir nun 10% o presuposto anual do departamento que teña o presuposto máis alto na actualidade. 

```sql
UPDATE departamento 
SET depPresuposto = depPresuposto* 0.9 
WHERE depPresuposto = (SELECT MAX(depPresuposto) FROM departamento)
```



8. Escribir un script para facer todos os seguintes cambios nos presupostos dos departamentos pero sen modificar o presuposto total: a. Traspasar 20000 do presuposto do departamento de 'PERSOAL' ao departamento de PROCESO DE DATOS. b. Reducir en 10000 o presuposto do departamento de 'SECTOR INDUSTRIAL', dos que 4000 se traspasan ao departamento de 'ORGANIZACION' e 6000 ao departamento de 'DIRECCION COMERCIAL'.

```sql


-- Actualizar presupuesto del departamento de PROCESO DE DATOS
UPDATE departamento
SET depPresuposto = depPresuposto + 20000
WHERE depNome = 'PROCESO DE DATOS';

-- Actualizar presupuesto del departamento de PERSOAL
UPDATE departamento
SET depPresuposto = depPresuposto- 20000
WHERE depNome = 'PERSOAL';

-- Actualizar presupuesto del departamento de ORGANIZACION
UPDATE departamento
SET depPresuposto = depPresuposto + 4000
WHERE depNome = 'ORGANIZACION';

-- Actualizar presupuesto del departamento de DIRECCION COMERCIAL
UPDATE departamento
SET depPresuposto = depPresuposto + 6000
WHERE depNome = 'DIRECCION COMERCIAL';

-- Actualizar presupuesto del departamento de SECTOR INDUSTRIAL
UPDATE departamento
SET depPresuposto = depPresuposto - 10000
WHERE depNome = 'SECTOR INDUSTRIAL';

```