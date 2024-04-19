1) CREACIÓN DE TABLAS

-- create a table

CREATE TABLE empleado (

 codigo INT (10) PRIMARY KEY,

 nit VARCHAR(9) NOT NULL,

 nombre VARCHAR (100) NOT NULL,

 apellido1 VARCHAR (100) NOT NULL,

 apellido2 VARCHAR (100),

 codigo_departamento INT (10)

);

CREATE TABLE departamento (

  codigo INT (10) PRIMARY KEY,

  nombre VARCHAR (100) NOT NULL,

  presupuesto DOUBLE,

  gasto DOUBLE

);

![img](/images/1.png)

2) INSERCIÓN DE DATOS

INSERT INTO departamento VALUES (1, 'Desarrollo', 120000, 6000),

​                (2, 'Sistemas', 150000, 21000),

​                (3, 'Recursos Humanos', 280000, 25000),

​                (4, 'Contabilidad', 110000, 3000),

​                (5, 'I+D', 375000, 380000),

​                (6, 'Proyectos', 0, 0),

​                (7, 'Publicidad', 0, 1000);

INSERT INTO empleado VALUES (1, '32481596F', 'Aarón', 'Rivero', 'Gómez', 1),

​              (2, 'Y5575632D', 'Adela', 'Salas', 'Díaz', 2),

​              (3, 'R6970642B', 'Adolfo', 'Rubio', 'Flores', 3),

​              (4, '77705545E', 'Adrián', 'Suárez', NULL, 4),

​              (5, '17087203C', 'Marcos', 'Loyola', 'Méndez', 5),

​              (6, '38382980M', 'María', 'Santana', 'Moreno', 1),

​              (7, '80576669X', 'Pilar', 'Ruiz', NULL, 2),

​              (8, '71651431Z', 'Pepe', 'Ruiz', 'Santana', 3),

​              (9, '56399183D', 'Juan', 'Gómez', 'López', 2),

​              (10, '46384486H', 'Diego','Flores', 'Salas', 5),

​              (11, '67389283A', 'Marta','Herrera', 'Gil', 1),

​              (12, '41234836R', 'Irene','Salas', 'Flores', NULL),

​              (13, '82635162B', 'Juan Antonio','Sáenz', 'Guerrero', NULL);

II)	Consultas sobre una tabla

1. ​	SELECT e.apellido1 AS 'Primer Apellido'

​	       FROM empleado as e;

![img](/images/2.png)

2. SELECT DISTINCT e.apellido1 AS 'Primer Apellido (sin repetir)'

​	FROM empleado AS e;

​		![img](/images/3.png)

3. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e;

![img](/images/4.png)

4. SELECT e.nombre AS Nombre, e.apellido1, e.apellido2

   FROM empleado AS e;

![img](/images/5.png)

5. SELECT e.codigo_departamento AS ‘Identificador de Departamento’
   FROM empleado AS e;

![img](/images/6.png)

6. SELECT DISTINCT e.codigo_departamento AS ‘Identificador de    Departamento’
   FROM empleado AS e;

![img](/images/7.png)

Los departamentos de proyectos y publicidad no tienen empleados

7. SELECT CONCAT (e.nombre, “ “, e.apellido1, “ “, IFNULL(e.apellido2, “”))
   FROM empleado AS e

![img](/images/8.png)

La funcion IFNULL permite remplazar valores nulos con un valor predeterminado 

8. SELECT UPPER (CONCAT (e.nombre, “ “, e.apellido1, “ “, IFNULL(e.apellido2, “”)))
   FROM empleado AS e;

![img](/images/9.png)

Transformando salida a MAYÚSCULAS

9. SELECT LOWER (CONCAT (e.nombre, “ “, e.apellido1, “ “, IFNULL(e.apellido2, “”)))
   FROM empleado AS e;

![img](/images/10.png)

Asegurando salida en MINÚSCULAS

10. SELECT e.codigo AS ‘Codigo de Empleado’, LEFT (e.nit, 8) AS ‘Dígitos del    Nit’, RIGHT (e.nit, 1) AS ‘Ultima letra del Nit’

​	FROM empleado AS e

![img](/images/11.png)

11.  SELECT d.nombre AS ‘Nombre de Departamento’, CONCAT (‘$’,d.presupuesto - d.gastos) AS ‘Presupuesto Disponible’
    FROM departamento AS d;

![img](/images/12.png)

Los departamentos de I+D y publicidad tienen deuda de presupuesto

12.  SELECT d.nombre AS ‘Nombre de Departamento’, CONCAT (‘$’,d.presupuesto - d.gastos) AS ‘Presupuesto Disponible’
    FROM departamento AS d
    ORDER BY (d.presupuesto - d.gastos) ASC;

![img](/images/13.png)

El departamento con mayor presupuesto es Recursos Humanos

13. SELECT d.nombre AS ‘Nombre de Departamento’
    FROM departamento AS d
    ORDER BY d.nombre ASC;

![img](/images/14.png)

Departamentos ordenados alfabéticamente por su nombre de manera ascendente

14.  SELECT d.nombre AS ‘Nombre de Departamento’
     FROM departamento AS d
     ORDER BY d.nombre DESC;

![img](/images/15.png)

Departamentos ordenados alfabéticamente por su nombre de manera descendente

15. SELECT e.apellido1, IFNULL(e.apellido2, '') AS apellido2, d.nombre AS     ‘Nombre de Empleado
    FROM empleado AS e
    ORDER BY e.apellido1 ASC;

![img](/images/16.png)

Empleados ordenados alfabéticamente de manera ascendente según su primer apellido.

  SELECT d.nombre AS ‘Nombre de Empleado’, e.apellido1, IFNULL(e.apellido2, '') AS apellido2

  FROM empleado AS e

  ORDER BY e.nombre ASC;

![img](/images/16.1.png)

​			Empleados ordenados alfabéticamente de manera ascendente según su nombre.

16. SELECT d.nombre AS 'Nombre de Departamento', CONCAT (‘$’, d.presupuesto) AS presupuesto
    FROM departamento AS d
    ORDER BY d.presupuesto DESC
    LIMIT 3;

![img](/images/17.png)

Los 3 departamentos con mayor presupuesto

17. SELECT d.nombre AS 'Nombre de Departamento', CONCAT (‘$’, d.presupuesto) AS presupuesto
    FROM departamento AS d
    ORDER BY d.presupuesto ASC
    LIMIT 3;

![img](/images/18.png)

​							Los 3 departamentos con menor presupuesto

18. SELECT d.nombre AS 'Nombre de Departamento', CONCAT (‘$’, d.gasto) AS Gasto.
    FROM departamento AS d
    ORDER BY d.gasto DESC
    LIMIT 2;

![img](/images/19.png)

​							Los 2 departamentos con mayor gasto

19. SELECT d.nombre AS 'Nombre de Departamento', CONCAT (‘$’, d.gasto) AS Gasto.
    FROM departamento AS d
    ORDER BY d.gasto ASC
    LIMIT 2;

![img](/images/20.png)

​							Los 2 departamentos con menor gasto

20. SELECT e.codigo AS 'Codigo de Empleado', e.nit, e.nombre As Nombre, e.apellido1, IFNULL(e.apellido2,"") AS apellido2, e.codigo_departamento AS 'Codigo de Departamento'
    FROM empleado AS e
    LIMIT 5 OFFSET 2;

![img](/images/21.png)

21. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto
    FROM departamento AS d
    WHERE d.presupuesto >= 150000;

![img](/images/22.png)

​    					Departamentos con un presupuesto mayor a $150.000

22. SELECT d.nombre, CONCAT('$',d.gasto) AS Gasto
    FROM departamento AS d
    WHERE d.gasto < 5000;

​			![img](/images/23.png)

​			    Departamentos con un gasto menor a 5000

23. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto
    FROM departamento AS d
    WHERE d.presupuesto >= 100000 AND d.presupuesto <= 200000;

![img](/images/24.png)

   				Departamentos con un presupuesto entre $100.000 y $200.000

24. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto
    FROM departamento AS d
    WHERE NOT (d.presupuesto >= 100000 AND d.presupuesto <= 200000);

![img](/images/25.png)

​			Departamentos que NO tienen un presupuesto entre $100.000 y $200.000

25. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto
    FROM departamento AS d
    WHERE d.presupuesto BETWEEN 100000 AND 200000;

![img](/images/26.png)

​			Departamentos con un presupuesto entre $100.000 y $200.000. Utilizando BETWEEN

26. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto
    FROM departamento AS d
    WHERE NOT (d.presupuesto BETWEEN 100000 AND 200000);

![img](/images/27.png)

​		Departamentos que NO tienen un presupuesto entre $100.000 y $200.000. Utilizando BETWEEN

27. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto,   CONCAT('$',d.gasto) AS gasto
    FROM departamento AS d
    WHERE d.gasto > d.presupuesto;

![img](/images/28.png)

  					  Departamentos cuyo gasto es mayor a su presupuesto

28.  SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto,   CONCAT('$',d.gasto) AS gasto
    FROM departamento AS d
    WHERE d.gasto < d.presupuesto;

![img](/images/29.png)

​    						Departamentos cuyo gasto es menor a su presupuesto

29. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto,   CONCAT('$',d.gasto) AS gasto
    FROM departamento AS d
    WHERE d.gasto = d.presupuesto;

![img](/images/30.png)

​    						Departamentos cuyo gasto es igual a su presupuesto

30. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e

​	WHERE e.apellido2 IS NULL;

![img](/images/31.png)

​								 Empleados cuyo segundo apellido es NULL

31. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre,  e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e

​	WHERE e.apellido2 IS NOT NULL;

![img](/images/32.png)

  					Empleados cuyo segundo apellido NO es NULL

32. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e

​	WHERE e.apellido2 = ‘López’;

![img](/images/33.png)

​							 Empleados cuyo segundo apellido es López

33. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e

​	WHERE e.apellido2 = ‘Díaz’ OR e.apellido2 = ‘Moreno’;

![img](/images/34.png)

​				Empleados cuyo segundo apellido es Díaz o Moreno. Sin utilizar el operador IN

34. SELECT e.codigo AS codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento'

​	FROM empleado AS e

​	WHERE e.apellido2 IN ('Díaz', 'Moreno');

![img](/images/35.png)

​			Empleados cuyo segundo apellido es Díaz o Moreno. Utilizando el operador IN

35. SELECT e.nombre AS Nombre, e.apellido1, e.apellido2, e.nit AS Nit, e.codigo_departamento AS 'Codigo Departamento'
    FROM empleado AS e
    WHERE e.codigo_departamento = 3;

![img](/images/36.png)

 		  				Empleados que trabajan en el departamento 3

36. SELECT e.nombre AS Nombre, e.apellido1, e.apellido2, e.nit AS Nit, e.codigo_departamento AS 'Codigo Departamento'
    FROM empleado AS e
    WHERE e.codigo_departamento IN (2,4,5);

![img](/images/37.png)

 		 				Empleados que trabajan en el departamento 2, 4 o 5



II)	Consultas Multitabla (Composición Interna)

1. SELECT e.codigo AS Codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento', d.nombre AS 'Nombre Departamento', CONCAT('$',d.presupuesto) AS presupuesto, CONCAT('$',d.gasto) AS gasto

FROM empleados AS e

JOIN departamento AS d ON e.codigo_departamento = d.codigo

![img](/images/38.png)

​      Empleados y la información de los departamentos donde trabajan

2. SELECT e.codigo AS Codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, e.codigo_departamento AS 'Codigo Departamento', d.nombre AS 'Nombre Departamento', CONCAT('$',d.presupuesto) AS presupuesto, CONCAT('$',d.gasto) AS gasto

FROM empleados AS e

JOIN departamento AS d ON e.codigo_departamento = d.codigo

ORDER BY d.nombre ASC

![img](/images/39.png)

 Empleados y la información de los departamentos donde trabajan ordenados alfabéticamente de manera ascendente según el nombre del departamento

​	SELECT e.codigo AS Codigo, e.nit AS Nit, e.apellido1, e.apellido2, e.nombre AS Nombre, e.codigo_departamento AS 'Codigo Departamento', d.nombre AS 'Nombre Departamento', CONCAT('$',d.presupuesto) AS presupuesto, CONCAT('$',d.gasto) AS gasto

FROM empleados AS e

JOIN departamento AS d ON e.codigo_departamento = d.codigo

ORDER BY e.apellido1 ASC

![img](/images/39.1.png)

 Empleados y la información de los departamentos donde trabajan ordenados alfabéticamente de manera ascendente según su primer apellido

3. SELECT DISTINCT d.codigo AS ‘Codigo de Departamento’, d.nombre

 FROM departamento AS d

 JOIN empleado AS e ON e.codigo_departamento = d.codigo;

![img](/images/40.png)

Departamentos que cuentan con empleados. Los departamentos de Proyectos y Publicidad no cuentan con empleados

4. SELECT DISTINCT d.codigo AS ‘Codigo de Departamento’, d.nombre,  CONCAT('$',d.presupuesto - d.gasto) AS 'Presupuesto Disponible'

 FROM departamento AS d

 JOIN empleado AS e ON e.codigo_departamento = d.codigo; 

![img](/images/41.png)

   			Presupuesto disponible de los departamentos que cuentan con empleados

5. SELECT d.nombre AS 'Nombre de Departamento', e.nit AS 'Nit del Empleado', e.nombre, e.apellido1

 FROM departamento AS d

 JOIN empleado AS e ON e.codigo_departamento = d.codigo;

 WHERE e.nit = '38382980M'

![img](/images/42.png)

   			Nombre del departamento donde trabaja el empleado con Nit 38382980M

6. SELECT d.nombre AS 'Nombre de Departamento', e.nombre, e.apellido1, e.apellido2

 FROM departamento AS d

 JOIN empleado AS e ON e.codigo_departamento = d.codigo;

 WHERE e.nombre = 'Pepe' AND e.apellido1 = 'Ruiz' AND e.apellido2 = 'Santana'

![img](/images/43.png)

   			Nombre del departamento donde trabaja el empleado Pepe Ruiz Santana

7. SELECT e.codigo AS Codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, d.nombre AS 'Nombre Departamento'

FROM empleado AS e

JOIN departamento as d ON e.codigo_departamento = d.codigo

WHERE d.nombre = 'I+D'

ORDER BY e.nombre ASC;

![img](/images/44.png)

Datos de los empleados que trabajan en el departamento de I+D. Ordenados alfabéticamente de manera ascendente según su nombre

8. SELECT e.codigo AS Codigo, e.nit AS Nit, e.nombre AS Nombre, e.apellido1, e.apellido2, d.nombre AS 'Nombre Departamento'

 FROM empleado AS e

 JOIN departamento as d ON e.codigo_departamento = d.codigo

 WHERE d.nombre IN ('Sistemas', 'Contabilidad', 'I+D')

 ORDER BY d.nombre ASC;

![img](/images/45.png)

Datos de los empleados que trabajan en el departamento de I+D, Sistemas o Contabilidad. Ordenados alfabéticamente de manera ascendente según el nombre del departamento

9.  SELECT e.nombre AS Nombre, e.apellido1, e.apellido2, d.nombre AS 'Nombre Departamento'

 FROM empleado AS e

 JOIN departamento as d ON e.codigo_departamento = d.codigo

 WHERE NOT (d.presupuesto BETWEEN 100000 AND 200000)

![img](/images/46.png)

Datos de los empleados que trabajan en departamentos que NO tienen un presupuesto entre $100.000 y $200.000

10.  SELECT  d.nombre AS 'Nombre Departamento', e.nombre AS Nombre, e.apellido1, e.apellido2

  FROM empleado AS e

  JOIN departamento as d ON e.codigo_departamento = d.codigo

  WHERE e.apellido2 IS NULL

![img](/images/47.png)

​			Departamentos que tienen empleados cuyo segundo apellido es NULL



III)	Consultas Multitabla (Composición Externa)

1. SELECT e.codigo, e.nombre AS Nombre, e.apellido1, d.codigo AS 'Codigo Departamento', d.nombre, d.presupuesto, d.gasto

FROM empleado AS e

LEFT JOIN departamento AS d ON e.codigo_departamento = d.codigo

![img](/images/48.png)

Empleados y datos de los departamentos donde trabajan. Incluye  empleados que no tienen asociado ningún departamento

2. SELECT e.codigo, e.nombre AS Nombre, e.apellido1, d.codigo AS 'Codigo Departamento', d.nombre, d.presupuesto, d.gasto

 FROM empleado AS e

 LEFT JOIN departamento AS d ON e.codigo_departamento = d.codigo

WHERE e.codigo_departamento IS NULL

![img](/images/49.png)

​					    Empleados que no tiene asociado ningún departamento

3. SELECT d.codigo 'Codigo Departamento', d.nombre, d.presupuesto, d.gasto

 FROM departamento AS d

 LEFT JOIN empleado AS e ON e.codigo_departamento = d.codigo

WHERE e.codigo_departamento IS NULL

![img](/images/50.png)

 						Departamentos que no tiene ningún empleado

4. SELECT e.codigo, e.nit, e.nombre AS Nombre, e.apellido1, d.codigo AS 'Codigo Departamento', d.nombre AS departamento

FROM empleado AS e

LEFT JOIN departamento AS d ON d.codigo = e.codigo_departamento

UNION

SELECT e.codigo, e.nit, e.nombre AS Nombre, e.apellido1, d.codigo AS 'Codigo Departamento', d.nombre AS departamento

FROM empleado AS e

RIGHT JOIN departamento AS d ON d.codigo = e.codigo_departamento

WHERE e.codigo_departamento IS NULL

ORDER BY departamento ASC;

![img](/images/51.png)

Empleados y datos de los departamentos donde trabajan. Se incluyen los departamentos que no tienen trabajadores y los trabajadores que no están asociados a ningún departamento

5. SELECT e.codigo, e.nombre AS Nombre, e.apellido1, d.nombre AS departamento

FROM empleado AS e

LEFT JOIN departamento AS d ON d.codigo = e.codigo_departamento

WHERE e.codigo_departamento IS NULL

UNION

SELECT e.codigo, e.nombre AS Nombre, e.apellido1, d.nombre AS departamento

FROM empleado AS e

RIGHT JOIN departamento AS d ON d.codigo = e.codigo_departamento

WHERE e.codigo_departamento IS NULL

ORDER BY departamento ASC;

![img](/images/52.png)

Departamentos que no tienen ningún empleado y empleados que no están asociados a ningún departamento

IV)	Consultas Resumen

1. SELECT CONCAT ('$',SUM(d.presupuesto)) AS 'Presupuesto total de los departamentos'

FROM departamento AS d

![img](/images/53.png)

​     					Suma de los presupuestos de todos los departamentos

2. SELECT CONCAT ('$',ROUND(AVG(d.presupuesto),2)) AS 'Promedio de presupuesto de los departamentos'

FROM departamento AS d

![img](/images/54.png)

3. SELECT CONCAT('$',MIN(d.presupuesto)) AS 'Valor mínimo de presupuesto de los departamentos'

FROM departamento AS d

![img](/images/55.png)

​     				Valor más bajo de presupuesto. Existen departamentos sin presupuesto

4. SELECT d.nombre AS 'Nombre de Departamento', CONCAT('$',d.presupuesto) AS 'Presupuesto'

FROM departamento AS d

JOIN (

​	SELECT MIN(Presupuesto) AS presupuesto_minimo

​	FROM departamento

) m ON d.presupuesto = m.presupuesto_minimo

![img](/images/56.png)

​        			Los departamentos de proyectos y publicidad tienen el menor presupuesto

5. SELECT CONCAT('$',MAX(d.presupuesto)) AS 'Presupuesto Maximo de los Departamentos'

FROM departamento AS d

![img](/images/57.png)

6. SELECT d.nombre AS 'Nombre de Departamento', CONCAT('$',d.presupuesto) AS 'Presupuesto'

FROM departamento AS d

JOIN (

​	SELECT MAX(Presupuesto) AS presupuesto_maximo

​	FROM departamento

) m ON d.presupuesto = m.presupuesto_maximo

![img](/images/58.png)

​						   El departamento I+D tiene el mayor presupuesto

7. SELECT COUNT(e.nombre) AS ‘Numero Total de Empleados’

 FROM empleado AS e

![img](/images/59.png)

8. SELECT COUNT(e.apellido2) AS 'Empleados con segundo Apellido'

FROM empleado AS e

WHERE e.apellido2 IS NOT NULL

![img](/images/60.png)

9. SELECT d.nombre AS 'Nombre Departamento', COUNT(e.codigo_departamento) AS 'Numero de Empleados'

FROM empleado AS e

JOIN departamento AS d ON d.codigo = e.codigo_departamento

GROUP BY d.nombre

![img](/images/61.png)

​							Número de empleados por cada departamento

10. SELECT d.nombre AS 'Nombre Departamento', COUNT(e.codigo_departamento) AS 'Numero de Empleados'

FROM empleado AS e

JOIN departamento AS d ON d.codigo = e.codigo_departamento

GROUP BY d.nombre

HAVING COUNT(e.codigo_departamento) > 2;

![img](/images/62.png)	

​		Departamentos con más de 2 empleados

11. SELECT d.nombre AS 'Nombre Departamento', COUNT(e.codigo_departamento) AS 'Numero de Empleados'

FROM empleado AS e

RIGHT JOIN departamento AS d ON d.codigo = e.codigo_departamento

GROUP BY d.nombre

![img](/images/63.png)

​			Número de empleados por cada departamento. Incluidos aquellos que no tienen empleados

12.  SELECT d.nombre AS 'Nombre Departamento', COUNT(e.codigo_departamento) AS 'Numero de Empleados', CONCAT('$',d.presupuesto) AS presupuesto

FROM empleado AS e

JOIN departamento AS d ON d.codigo = e.codigo_departamento

WHERE d.presupuesto > 200000

GROUP BY d.nombre, d.presupuesto

![img](/images/64.png)

​		Número de empleados que hay en departamentos con un presupuesto mayor a $200.000

V)	SUBCONSULTAS

1. SELECT e.codigo, e.nombre, e.apellido1

FROM empleado AS e, departamento AS d

WHERE d.codigo = e.codigo_departamento AND d.nombre = 'Sistemas';

![img](/images/65.png)

​					Empleados que trabajan en el departamento de sistemas

2. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto

FROM departamento AS d

JOIN (

​	SELECT MAX(presupuesto) AS max_presupuesto

​	FROM departamento

) m ON d.presupuesto = m.max_presupuesto;

![img](/images/66.png)

​							El departamento con el mayor presupuesto

3. SELECT d.nombre, CONCAT('$',d.presupuesto) AS presupuesto

FROM departamento AS d

JOIN (

​	SELECT MIN(presupuesto) AS min_presupuesto

​	FROM departamento

) m ON d.presupuesto = m.min_presupuesto;

![img](/images/67.png)

​							Departamentos con menor presupuesto

**Subconsultas con ALL y ANY**

4. SELECT d.nombre AS 'Nombre Departamento', d.presupuesto AS Presupuesto

FROM departamento d

WHERE d.presupuesto >= ALL (

  	SELECT presupuesto

  	FROM departamento

);

![img](/images/68.png)

  						     El departamento con el mayor presupuesto

5. SELECT d.nombre AS 'Nombre Departamento', d.presupuesto AS Presupuesto

FROM departamento d

WHERE d.presupuesto <= ALL (

  	SELECT presupuesto

  	FROM departamento

);

![img](/images/69.png)

​							   Departamentos con menor presupuesto

6. SELECT d.nombre AS 'Nombre Departamento'

FROM departamento d

WHERE d.codigo = ANY (

 	 SELECT DISTINCT e.codigo_departamento

  	FROM empleado e

);

![img](/images/70.png)

​        			Departamentos que tienen empleados asociados. Utilizando ANY

7. SELECT d.nombre AS 'Nombre Departamento'

FROM departamento d

WHERE d.codigo != ALL (

  SELECT DISTINCT e.codigo_departamento

 	 FROM empleado e

  	WHERE e.codigo_departamento IS NOT NULL

);

*** Se agrega la condición IS NOT NULL ya que ALL tiene conflictos con   valores nulos

![img](/images/71.png)      

Departamentos que no tienen empleados. Utilizando ALL

**Subconsultas con IN y NOT IN**

8. SELECT d.nombre AS 'Nombre Departamento'

FROM departamento AS d

WHERE d.codigo IN (

  	SELECT DISTINCT e.codigo_departamento

  	FROM empleados e

);

![img](/images/72.png)

​         				Departamentos que tienen empleados asociados. Utilizando IN

9. SELECT d.nombre AS 'Nombre Departamento'

FROM departamento AS d

WHERE d.codigo NOT IN (

  	SELECT DISTINCT e.codigo_departamento

  	FROM empleado AS e

  	WHERE e.codigo_departamento IS NOT NULL

);

 *** Se agrega la condición IS NOT NULL ya que NOT IN tiene conflictos con   valores nulos

![img](/images/73.png)

​           			Departamentos que no tienen empleados. Utilizando NOT IN

**Subconsultas con EXISTS y NOT EXISTS**

10. SELECT d.nombre AS 'Nombre Departamento'

 FROM departamento d

 WHERE EXISTS (

   	SELECT 1

   	FROM empleado e

   	WHERE e.codigo_departamento = d.codigo

);

![img](/images/74.png)

​        			Departamentos que tienen empleados asociados. Utilizando EXISTS

11. SELECT d.nombre AS 'Nombre Departamento'

FROM departamento d

WHERE NOT EXISTS (

  	SELECT 1

  	FROM empleado e

  	WHERE e.codigo_departamento = d.codigo

);

*** NOT EXISTS no tiene conflictos con valores nulos

![img](/images/75.png)

​           			Departamentos que no tienen empleados. Utilizando NOT EXISTS