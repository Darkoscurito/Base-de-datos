<div align="justify">



# 🧾🧾 Tarea-10 Simulacro 🧾🧾




<details>

<summary>Base de datos</summary>

```SQL
CREATE TABLE consumidor (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    apellido1 TEXT,
    apellido2 TEXT,
    ciudad TEXT,
    categoria INTEGER
);
CREATE TABLE suministrador  (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    apellido1 TEXT,
    apellido2 TEXT,
    categoria REAL
);
CREATE TABLE compra (
    id INTEGER PRIMARY KEY,
    total REAL,
    fecha TEXT,
    id_consumidor INTEGER,
    id_suministrador INTEGER,
    FOREIGN KEY (id_consumidor) REFERENCES consumidor(id),
    FOREIGN KEY (id_suministrador) REFERENCES suministrador(id)
); 
--Inserts
INSERT INTO consumidor VALUES(1, 'Aarón', 'Rivero', 'Gómez', 'Almería', 100);
INSERT INTO consumidor VALUES(2, 'Adela', 'Salas', 'Díaz', 'Granada', 200);
INSERT INTO consumidor VALUES(3, 'Adolfo', 'Rubio', 'Flores', 'Sevilla', NULL);
INSERT INTO consumidor VALUES(4, 'Adrián', 'Suárez', NULL, 'Jaén', 300);
INSERT INTO consumidor VALUES(5, 'Marcos', 'Loyola', 'Méndez', 'Almería', 200);
INSERT INTO consumidor VALUES(6, 'María', 'Santana', 'Moreno', 'Cádiz', 100);
INSERT INTO consumidor VALUES(7, 'Pilar', 'Ruiz', NULL, 'Sevilla', 300);
INSERT INTO consumidor VALUES(8, 'Pepe', 'Ruiz', 'Santana', 'Huelva', 200);
INSERT INTO consumidor VALUES(9, 'Guillermo', 'López', 'Gómez', 'Granada', 225);
INSERT INTO consumidor VALUES(10, 'Daniel', 'Santana', 'Loyola', 'Sevilla', 125);
INSERT INTO suministrador  VALUES(1, 'Daniel', 'Sáez', 'Vega', 0.15);
INSERT INTO suministrador  VALUES(2, 'Juan', 'Gómez', 'López', 0.13);
INSERT INTO suministrador  VALUES(3, 'Diego','Flores', 'Salas', 0.11);
INSERT INTO suministrador  VALUES(4, 'Marta','Herrera', 'Gil', 0.14);
INSERT INTO suministrador  VALUES(5, 'Antonio','Carretero', 'Ortega', 0.12);
INSERT INTO suministrador  VALUES(6, 'Manuel','Domínguez', 'Hernández', 0.13);
INSERT INTO suministrador  VALUES(7, 'Antonio','Vega', 'Hernández', 0.11);
INSERT INTO suministrador  VALUES(8, 'Alfredo','Ruiz', 'Flores', 0.05);
INSERT INTO compra VALUES(1, 150.5, '2020-10-05', 5, 2);
INSERT INTO compra VALUES(2, 270.65, '2019-09-10', 1, 5);
INSERT INTO compra VALUES(3, 65.26, '2020-10-05', 2, 1);
INSERT INTO compra VALUES(4, 110.5, '2019-08-17', 8, 3);
INSERT INTO compra VALUES(5, 948.5, '2020-09-10', 5, 2);
INSERT INTO compra VALUES(6, 2400.6, '2019-07-27', 7, 1);
INSERT INTO compra VALUES(7, 5760, '2018-09-10', 2, 1);
INSERT INTO compra VALUES(8, 1983.43, '2020-10-10', 4, 6);
INSERT INTO compra VALUES(9, 2480.4, '2019-10-10', 8, 3);
INSERT INTO compra VALUES(10, 250.45, '2018-06-27', 8, 2);
INSERT INTO compra VALUES(11, 75.29, '2019-08-17', 3, 7);
INSERT INTO compra VALUES(12, 3045.6, '2020-04-25', 2, 1);
INSERT INTO compra VALUES(13, 545.75, '2022-01-25', 6, 1);
INSERT INTO compra VALUES(14, 145.82, '2020-02-02', 6, 1);
INSERT INTO compra VALUES(15, 370.85, '2022-03-11', 1, 5);
INSERT INTO compra VALUES(16, 2389.23, '2022-03-11', 1, 5);
```
</details>

<br>

### Adrian_Denis_Fernandez_Acosta_consultas_multitabla_simulacro.

<details>

<summary>SOLUCION SQL</summary>


```SQL
-- ----------------------------------------
-- Consultas sobre una tabla
-- 0,2 puntos la correcta. Total = 1,4 puntos
-- ----------------------------------------

-- 1.- Devuelve un listado con todos las compras que se han realizado. Las compras deben estar ordenados
-- por la fecha de realización, mostrando en primer lugar las compras más recientes.
-- 2. Devuelve todos los datos de los dos compras de mayor valor.
-- 3. Devuelve un listado con los identificadores de los consumidores que han realizado algún compra.
-- Tenga en cuenta que no debe mostrar identificadores que estén repetidos.
-- 4. Devuelve un listado de todos las compras que se realizaron durante el año 2020,
-- cuya cantidad total sea superior a 500€.
-- 5. Devuelve un listado con el nombre y los apellidos de los suministradores que tienen una comisión entre 0.11 y 0.15.
-- 6. Devuelve el valor de la comisión de mayor valor que existe en la tabla suministrador.
-- 7. Devuelve el identificador, nombre y primer apellido de aquellos consumidores cuyo segundo apellido no es NULL.
-- El listado deberá estar ordenado alfabéticamente por apellidos y nombre.

SOLUCIONES:

1.
SELECT * FROM compra ORDER BY fecha DESC;
2.
SELECT * FROM compra ORDER BY total DESC LIMIT 2;
3.
SELECT c.id, co.id FROM compra co, consumidor c
WHERE c.id = co.id_consumidor;
4.
 SELECT * FROM compra WHERE total > 500 AND fecha REGEXP '2020';
5. 
SELECT nombre, apellido1, apellidos2 FROM suministrador WHERE suministrador BETWEEN '0.11' AND '0.15'
6.
SELECT id, MAX(categoria) AS mayorValor FROM suministrador;
7.
SELECT id, nombre, apellido1 FROM consumidor WHERE apellido2 IS NOT NULL
ORDER BY apellido1, nombre DESC;
-- (Consultas Multitabla Where)
-- -----------------------------------------------
-- 0,3 puntos la correcta. Total =  2,1 puntos
-- -----------------------------------------------

-- 1. Devuelve un listado con el identificador, nombre y los apellidos de todos los consumidores que han realizado algún compra.
-- El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.
-- 2. Devuelve un listado que muestre todos las compras que ha realizado cada consumidor. 
-- El resultado debe mostrar todos los datos de las compras y del consumidor. El listado debe mostrar los datos de los consumidores ordenados alfabéticamente.
-- 3. Devuelve un listado que muestre todos las compras en los que ha participado un suministrador.
-- El resultado debe mostrar todos los datos de las compras y de los suministradores.
-- El listado debe mostrar los datos de los suministradores ordenados alfabéticamente.
-- 4. Devuelve un listado que muestre todos los consumidores, con todos las compras que han realizado 
-- y con los datos de los suministradores asociados a cada compra.
-- 5. Devuelve un listado de todos los consumidores que realizaron un compra durante el año 2020,
-- cuya cantidad esté entre 300 € y 1000 €.
-- 6. Devuelve el nombre y los apellidos de todos los suministradores que ha participado en algún compra realizado por María Santana Moreno.
-- 7. Devuelve el nombre de todos los consumidores que han realizado algún compra con el suministrador Daniel Sáez Vega.

Soluciones:

1.
SELECT c.id, c.nombre, c.apellido1, c.apellido2 FROM consumidor c, compra co ORDER BY c.nombre,c.apellido1,c.apellido2 DESC;
WHERE c.id = co.id_consumidor
2.
SELECT c.*, co.* FROM consumidor c, compra co
WHERE c.id = co.id_consumidor
ORDER BY c.nombre,c.apellido1,c.apellido2 DESC;
3. 
SELECT c.*,s.* FROM compra c, suministrador s 
WHERE c.id_suministrador = s.id 
ORDER BY apellido1 DESC;
4.
SELECT c.*,s.*,co.* FROM consumidor c,suministrador s,compra co
WHERE co.id_suministrador = s.id AND c.id = co.id_suministrador;
5.
SELECT c.* FROM consumidor c, compra co
WHERE c.id = co.id_consumidor AND fecha REGEXP '2020' AND total BETWEEN '300' AND '1000';
6.
SELECT s.nombre, s.apellido1, s.apellido2 
FROM suministrador s, compra co, consumidor c
WHERE s.id = co.id_suministrador
AND c.id = co.id_consumidor
AND c.nombre = 'María' 
AND c.apellido1 = 'Santana' 
AND c.apellido2 = 'Moreno';

7.
SELECT c.* 
FROM consumidor c, compra co, suministrador s
WHERE c.id = co.id_consumidor
AND s.id = co.id_suministrador
AND s.nombre = 'Daniel' AND s.apellido1 = 'Sáez' AND s.apellido2 = 'Vega';


-- (Consultas Multitabla Join)
-- -----------------------------------------------
-- 0,3 puntos la correcta. Total = 2,1 puntos
-- -----------------------------------------------

-- 1. Devuelve un listado con el identificador, nombre y los apellidos de todos los consumidores que han realizado algún compra.
-- El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.
-- 2. Devuelve un listado que muestre todos las compras que ha realizado cada consumidor. 
-- El resultado debe mostrar todos los datos de las compras y del consumidor. El listado debe mostrar los datos de los consumidores ordenados alfabéticamente.
-- 3. Devuelve un listado que muestre todos las compras en los que ha participado un suministrador.
-- El resultado debe mostrar todos los datos de las compras y de los suministradores.
-- El listado debe mostrar los datos de los suministradores ordenados alfabéticamente.
-- 4. Devuelve un listado que muestre todos los consumidores, con todos las compras que han realizado 
-- y con los datos de los suministradores asociados a cada compra.
-- 5. Devuelve un listado de todos los consumidores que realizaron una compra durante el año 2020,
-- cuya cantidad esté entre 300 € y 1000 €.
-- 6. Devuelve el nombre y los apellidos de todos los suministradores que ha participado en algún compra realizado por María Santana Moreno.
-- 7. Devuelve el nombre de todos los consumidores que han realizado algún compra con el suministrador Daniel Sáez Vega.

Soluciones:

1. 
SELECT DISTINCT c.id, c.nombre, c.apellido1, c.apellido2
FROM consumidor c
INNER JOIN compra co ON c.id = co.id
ORDER BY c.nombre, c.apellido1, c.apellido2 

2.
SELECT co.*, c.* 
FROM compra co
INNER JOIN consumidor c ON co.id = c.id
ORDER BY c.nombre, c.apellido1, c.apellido2 DESC;

3.
SELECT co.*, s.* 
FROM compra co
INNER JOIN suministrador s ON co.id = s.id
ORDER BY s.nombre, s.apellido1, s.apellido2 DESC;

4.
SELECT c.*
FROM consumidor c
INNER JOIN compra co ON c.id = co.id
INNER JOIN suministrador s ON co.id = s.id;

5.
SELECT s.nombre, s.apellido1, s.apellido2
FROM suministrador s
INNER JOIN compra co ON s.id = co.id
WHERE fecha REGEXP '2020' AND total BETWEEN '300' AND '1000;'

6.
SELECT s.nombre, s.apellido1, s.apellido2
FROM suministrador s
INNER JOIN compra co ON s.id = co.id
WHERE s.nombre = 'María'
AND s.apellido1 = 'Santana'
AND s.apellido2 = 'Moreno';''

7.
SELECT c.*
FROM consumidor c
INNER JOIN compra co ON c.id = co.id
INNER JOIN suministrador s ON co.id = s.id
WHERE s.nombre = 'Daniel' 
AND s.apellido1 = 'Sáez' 
AND s.apellido2 = 'Vega';''



-- ---------------------------
-- Consultas resumen (funciones)
-- -----------------------------------------------
-- 0,2 puntos la correcta. (1-6) 1,2 puntos
-- 0,25 puntos la correcta. (7-10) 1 punto.
-- Total = 2,2 puntos
-- -----------------------------------------------

-- 1. Calcula la cantidad media de todos las compras que aparecen en la tabla compra.
-- 2. Calcula el número total de suministradores distintos que aparecen en la tabla compra.
-- 3. Calcula el número total de consumidores que aparecen en la tabla consumidor.
-- 4. Calcula cuál es la mayor cantidad que aparece en la tabla compra.
-- 5. Calcula cuál es el valor máximo de categoría para cada una de las ciudades que aparece en la tabla consumidor.
-- 6. Calcula cuál es el máximo valor de las compras realizadas durante el mismo día para cada uno de los consumidores.
-- Es decir, el mismo consumidor puede haber realizado varios compras de diferentes cantidades el mismo día.
-- Se pide que se calcule cuál es el compra de máximo valor para cada uno de los días en los que un consumidor ha realizado un compra.
-- Muestra el identificador del consumidor, nombre, apellidos, la fecha y el valor de la cantidad.
-- 7. Calcula cuál es el máximo valor de las compras realizadas durante el mismo día para cada uno de los consumidores,
-- teniendo en cuenta que sólo queremos mostrar aquellas compras que superen la cantidad de 2000 €.
-- 8. Calcula el máximo valor de las compras realizadas para cada uno de los suministradores durante la fecha 2020-08-17.
-- Muestra el identificador del suministrador, nombre, apellidos y total.
-- 9. Devuelve un listado con el identificador de consumidor, nombre y apellidos y el número total de compras que ha realizado cada uno de consumidores.
-- Tenga en cuenta que pueden existir consumidores que no han realizado ninguna compra.
-- Estos consumidores también deben aparecer en el listado indicando que el número de compras realizadas es 0.
-- 10. Devuelve un listado con el identificador de consumidor, nombre y apellidos y el número total de compras que ha realizado cada uno de consumidores durante el año 2020.


SOLUCIONES:

1.
SELECT AVG(total) AS mediaCompra
FROM compra;

2.
SELECT DISTINCT MAX(s.id) AS totalSuministradores
FROM compra c
WHERE s.id = c.id;

3.
SELECT COUNT(c.id) AS numConsumidores
FROM consumidor c;

4.
SELECT MAX(total) AS maxPrecio
FROM compra c;

5.
SELECT c.ciudad, MAX(c.categoria) AS valorMaximo
FROM consumidor c
GROUP BY c.ciudad;

6.
SELECT c.id_consumidor, MAX(co.total), co.fecha 
FROM compra co
INNER JOIN consumidor c ON c.id = co.id_consumidor
GROUP BY co.id_consumidor, co.fecha


7.
SELECT id_consumidor, MAX(total), co.fecha
FROM compra co
INNER JOIN suministrador s ON s.id = co.id_suministrador
GROUP BY c.id, co.fecha
HAVING total > 2000;

8.
SELECT s.id, s.nombre, s.apellido1, s.apellido2, MAX(co.total)
FROM compra co
INNER JOIN suministrador s ON s.id = co.id_suministrador
WHERE co.fecha = '2020-08-17'
GROUP BY s.id;

9.
SELECT c.id, c.nombre, c.apellido1, c.apellido2, COUNT(co.id) 
FROM compra co
RIGHT JOIN consumidor c ON c.id = co.id_consumidor
GROUP BY c.id;

10.
SELECT c.id, c.nombre, c.apellido1, c.apellido2, COUNT(co.id), co.fecha 
FROM compra co
RIGHT JOIN consumidor c ON c.id = co.id_consumidor
GROUP BY c.id
HAVING co.fecha REGEXP '2020';




-- ---------------------
-- Subconsultas
-- -----------------------------------------------
-- 0,2 puntos la correcta (1-5).
-- 0,3 puntos la correcta (6-9).
-- Total = 2,2 puntos
-- -----------------------------------------------

--- Con operadores básicos de comparación

-- 1. Devuelve un listado con todos las compras que ha realizado Adela Salas Díaz. (Sin utilizar INNER JOIN).
-- 2. Devuelve la fecha y la cantidad del compra de menor valor realizado por el cliente Pepe Ruiz Santana.
-- 3. Devuelve el número de compras en los que ha participado el suministrador Daniel Sáez Vega. (Sin utilizar INNER JOIN)
-- 4. Devuelve los datos del consumidor que realizó el compra más caro en el año 2021. (Sin utilizar INNER JOIN)
-- 5. Devuelve un listado con los datos de los consumidores y las compras, de todos los consumidores que han realizado una compra durante el año 2020 con un valor mayor o igual al valor medio de las compras realizadas durante ese mismo año.
-- 6. Devuelve un listado de los consumidores que no han realizado ningún compra. (Utilizando IN o NOT IN).
-- 7. Devuelve un listado de los suministradores que no han realizado ningún compra. (Utilizando IN o NOT IN).
-- 8. Devuelve un listado de los consumidores que no han realizado ningún compra. (Utilizando EXISTS o NOT EXISTS).
-- 9. Devuelve un listado de los suministradores que no han realizado ningún compra. (Utilizando EXISTS o NOT EXISTS).

Solucion

1. 
SELECT c.* FROM compra c 
WHERE id_consumidor IN 
(
SELECT id
FROM consumidor
WHERE nombre = 'Adela' AND apellido1 = 'Salas' AND apellido2 = 'Díaz'
);

2. 
SELECT c.fecha, MIN(total) AS menorValor FROM compra c 
WHERE id_consumidor IN 
(
SELECT id
FROM consumidor 
WHERE nombre = 'Pepe' AND apellido1 = 'Ruiz' AND apellido2 = 'Santana'
);

3.
SELECT COUNT(*) 
FROM compra
WHERE id_consumidor IN 
(
SELECT id
FROM consumidor 
WHERE nombre = 'Daniel' AND apellido1 = 'Sáez' AND apellido2 = 'Vega'
);

4.
SELECT * 
FROM consumidor
WHERE id IN 
(
SELECT id_consumidor
FROM compra 
WHERE fecha REGEXP '2021'
);

5.
SELECT c.*, co.* 
FROM consumidor c
INNER JOIN compra co ON c.id = co.id_consumidor
WHERE fecha REGEXP '2020' AND total >=  
(
SELECT AVG(total)
FROM compra co
WHERE co.fecha REGEXP '2020'
);

6.
SELECT c.* 
FROM consumidor c
WHERE id NOT IN  
(
SELECT DISTINCT id_consumidor
FROM compra co
);

7.
SELECT s.* 
FROM suministrador s
WHERE id NOT IN  
(
SELECT DISTINCT id_consumidor
FROM compra co
);

8.
SELECT c.* 
FROM consumidor c
WHERE NOT EXISTS 
(
SELECT 1
FROM compra co
WHERE co.id_consumidor = c.id
);

9.
SELECT s.* 
FROM suministrador s
WHERE NOT EXISTS 
(
SELECT 1
FROM compra co
WHERE co.id_suministrador = s.id
);

```


</details>










</div>
