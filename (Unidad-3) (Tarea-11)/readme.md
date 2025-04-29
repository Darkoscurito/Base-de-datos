<div align="justify">



# 🧾🧾 Tarea-11 Simulacro 🧾🧾




<details>

<summary>Base de datos</summary>

```SQL
CREATE TABLE socio (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    apellido1 TEXT,
    apellido2 TEXT,
    ciudad TEXT,
    fecha_alta TEXT,
    categoria TEXT
);

CREATE TABLE libro (
    id INTEGER PRIMARY KEY,
    titulo TEXT,
    autor TEXT,
    genero TEXT,
    año_publicacion INTEGER,
    disponible INTEGER 
);

CREATE TABLE prestamo (
    id INTEGER PRIMARY KEY,
    fecha_prestamo TEXT,
    fecha_devolucion TEXT,
    id_socio INTEGER,
    id_libro INTEGER,
    FOREIGN KEY (id_socio) REFERENCES socio(id),
    FOREIGN KEY (id_libro) REFERENCES libro(id)
);

CREATE TABLE bibliotecario (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    apellido1 TEXT,
    apellido2 TEXT,
    antiguedad INTEGER 
);


INSERT INTO socio VALUES(1, 'Laura', 'García', 'Martínez', 'Madrid', '2020-03-15', 'A');
INSERT INTO socio VALUES(2, 'Carlos', 'López', 'Fernández', 'Barcelona', '2021-05-20', 'B');
INSERT INTO socio VALUES(3, 'Ana', 'Sánchez', NULL, 'Valencia', '2022-01-10', 'C');
INSERT INTO socio VALUES(4, 'David', 'Pérez', 'Gómez', 'Sevilla', '2021-11-30', 'A');
INSERT INTO socio VALUES(5, 'Elena', 'Martín', 'Díaz', 'Madrid', '2023-02-18', 'B');
INSERT INTO socio VALUES(6, 'Javier', 'Ruiz', 'Moreno', 'Bilbao', '2020-07-22', 'A');
INSERT INTO socio VALUES(7, 'Sofía', 'Hernández', 'Jiménez', 'Zaragoza', '2022-09-05', 'C');
INSERT INTO socio VALUES(8, 'Miguel', 'Navarro', 'Torres', 'Málaga', '2021-04-12', 'B');
INSERT INTO socio VALUES(9, 'Patricia', 'Romero', NULL, 'Barcelona', '2023-01-15', 'A');
INSERT INTO socio VALUES(10, 'Antonio', 'Domingo', 'Santos', 'Valencia', '2020-12-08', 'C');

INSERT INTO libro VALUES(1, 'El Quijote', 'Miguel de Cervantes', 'Clásico', 1605, 1);
INSERT INTO libro VALUES(2, 'Cien años de soledad', 'Gabriel García Márquez', 'Realismo mágico', 1967, 0);
INSERT INTO libro VALUES(3, '1984', 'George Orwell', 'Ciencia ficción', 1949, 1);
INSERT INTO libro VALUES(4, 'Orgullo y prejuicio', 'Jane Austen', 'Romance', 1813, 0);
INSERT INTO libro VALUES(5, 'La sombra del viento', 'Carlos Ruiz Zafón', 'Misterio', 2001, 1);
INSERT INTO libro VALUES(6, 'Rayuela', 'Julio Cortázar', 'Experimental', 1963, 0);
INSERT INTO libro VALUES(7, 'Ficciones', 'Jorge Luis Borges', 'Cuentos', 1944, 1);
INSERT INTO libro VALUES(8, 'Los pilares de la Tierra', 'Ken Follett', 'Histórica', 1989, 0);
INSERT INTO libro VALUES(9, 'El amor en los tiempos del cólera', 'Gabriel García Márquez', 'Romance', 1985, 1);
INSERT INTO libro VALUES(10, 'La casa de los espíritus', 'Isabel Allende', 'Realismo mágico', 1982, 0);

INSERT INTO bibliotecario VALUES(1, 'Daniel', 'Vázquez', 'Gil', 5);
INSERT INTO bibliotecario VALUES(2, 'María', 'Castro', 'Ortega', 3);
INSERT INTO bibliotecario VALUES(3, 'Pablo', 'Molina', 'Serrano', 2);
INSERT INTO bibliotecario VALUES(4, 'Lucía', 'Reyes', 'Martín', 7);
INSERT INTO bibliotecario VALUES(5, 'Alejandro', 'Suárez', 'Blanco', 1);
INSERT INTO bibliotecario VALUES(6, 'Isabel', 'Morales', 'Iglesias', 4);
INSERT INTO bibliotecario VALUES(7, 'Francisco', 'Santana', 'Méndez', 6);
INSERT INTO bibliotecario VALUES(8, 'Cristina', 'Cabrera', 'Flores', 2);

INSERT INTO prestamo VALUES(1, '2023-01-10', '2023-01-24', 1, 2);
INSERT INTO prestamo VALUES(2, '2023-02-15', '2023-03-01', 3, 4);
INSERT INTO prestamo VALUES(3, '2023-03-20', NULL, 5, 6);
INSERT INTO prestamo VALUES(4, '2023-04-05', '2023-04-19', 2, 8);
INSERT INTO prestamo VALUES(5, '2023-05-12', NULL, 4, 10);
INSERT INTO prestamo VALUES(6, '2023-01-22', '2023-02-05', 6, 2);
INSERT INTO prestamo VALUES(7, '2023-02-18', '2023-03-04', 7, 4);
INSERT INTO prestamo VALUES(8, '2023-03-25', NULL, 8, 6);
INSERT INTO prestamo VALUES(9, '2023-04-10', '2023-04-24', 9, 8);
INSERT INTO prestamo VALUES(10, '2023-05-15', NULL, 10, 10);
INSERT INTO prestamo VALUES(11, '2023-01-05', '2023-01-19', 1, 1);
INSERT INTO prestamo VALUES(12, '2023-02-10', '2023-02-24', 2, 3);
INSERT INTO prestamo VALUES(13, '2023-03-15', NULL, 3, 5);
INSERT INTO prestamo VALUES(14, '2023-04-20', '2023-05-04', 4, 7);
INSERT INTO prestamo VALUES(15, '2023-05-25', NULL, 5, 9);
```
</details>

<br>

### Adrian_Denis_Fernandez_Acosta_consultas_multitabla_simulacro.

<details>

<summary>SOLUCION SQL</summary>


```SQL
-- 1. Consultas Básicas (8 consultas - 1.6 puntos)
-- Listar todos los libros disponibles

SELECT * 
FROM libro;

-- Mostrar socios de Madrid ordenados por apellido

SELECT * 
FROM socio
WHERE ciudad = 'Madrid'
ORDER BY apellido1, apellido2 DESC;

-- Libros publicados después de 1950

SELECT *
FROM libro
WHERE ano_publicacion = 1950;

-- Bibliotecarios con más de 3 años de antigüedad

SELECT * 
FROM bibliotecario
WHERE antiguedad > 3;

-- Préstamos realizados en 2023

SELECT *
FROM prestamo
WHERE fecha_prestamo REGEXP '2023';

-- Socios sin segundo apellido

SELECT * 
FROM socio
WHERE apellido2 IS NULL;

-- Libros del género "Realismo mágico"

SELECT *
FROM libro
WHERE genero = 'Realismo magico';

-- Préstamos no devueltos (fecha_devolucion IS NULL)

SELECT *
FROM prestamo
WHERE fecha_devolucion IS NULL;

-- 2. Consultas Multitabla (WHERE) (8 consultas - 2.4 puntos)
-- Préstamos con nombres de socio y libro (sin JOIN)

SELECT DISTINCT p.id, s.nombre, l.autor
FROM prestamo p, socio s, libro l, bibliotecario b /* MIRAR DE NUEVO */
WHERE p.id_libro = l.id AND p.id_socio = s.id;

-- Libros prestados a socios de Barcelona (sin JOIN)

SELECT DISTINCT p.id, s.nombre, l.autor
FROM prestamo p, socio s, libro l
WHERE p.id_libro = l.id AND p.id_socio = s.id AND s.ciudad = 'Barcelona';

-- Socios que han tomado prestado "Cien años de soledad" (sin JOIN)

SELECT p.id, l.titulo
FROM prestamo p, libro l 
WHERE p.id_libro = l.id AND l.titulo = 'Cien anos de soledad';

-- Bibliotecarios que han gestionado préstamos (sin JOIN)

SELECT p.fecha_prestamo, b.id
FROM prestamo p,  bibliotecario b
WHERE p.id_bibliotecario = b.id;

-- Préstamos con retraso (fecha_devolucion > fecha_prestamo + 14 días)

SELECT p.*
FROM prestamo p
WHERE fecha_devolucion > fecha_prestamo AND fecha_prestamo > 14;


-- Socios que nunca han tomado prestado un libro (sin LEFT JOIN)

SELECT *
FROM socio
WHERE id NOT IN (SELECT DISTINCT id_socio FROM prestamo);


-- Libros más prestados (sin JOIN)

SELECT l.id, COUNT(p.id)
FROM prestamo p, libro l 
WHERE p.id_libro = l.id                    
GROUP BY l.id
ORDER BY p.fecha_prestamo DESC;

-- Autores cuyos libros han sido prestados (sin JOIN)

SELECT p.fecha_prestamo, l.autor
FROM prestamo p, libro l
WHERE p.id_libro = l.id;

-- 3. Consultas Multitabla (JOIN) (8 consultas - 2.4 puntos)
-- Préstamos con nombres de socio y libro (JOIN)

SELECT p.fecha_prestamo, s.nombre, l.autor
FROM prestamo p
INNER JOIN libro l ON p.id_libro = l.id
INNER JOIN socio s ON p.id_socio = s.id;

-- Libros prestados a socios de Barcelona (JOIN)

SELECT p.fecha_prestamo, s.ciudad
FROM prestamo p
INNER JOIN socio s ON p.id_socio = s.id
WHERE s.ciudad = 'Barcelona';

-- Socios que han tomado prestado "Cien años de soledad" (JOIN)

SELECT p.fecha_prestamo, s.id, l.titulo
FROM prestamo p
INNER JOIN socio s ON p.id_socio = s.id
INNER JOIN libro l ON p.id_libro = l.id
WHERE l.titulo = 'Cien anos de soledad';

-- Bibliotecarios que han gestionado préstamos (JOIN)

SELECT p.fecha_prestamo, b.id
FROM prestamo p
INNER JOIN bibliotecario b ON p.id_bibliotecario = b.id;

-- Préstamos con datos completos (socio, libro, bibliotecario)

SELECT p.*, s.*, l.*, b.*
FROM prestamo p
INNER JOIN bibliotecario b ON p.id_bibliotecario = b.id  
INNER JOIN libro l ON p.id_libro = l.id
INNER JOIN socio s ON p.id_socio = s.id;

-- Socios con sus préstamos activos (JOIN)

SELECT p.fecha_prestamo, p.fecha_devolucion, s.nombre
FROM prestamo p
INNER JOIN socio s ON p.id_socio = s.id
WHERE p.fecha_prestamo IS NOT NULL AND p.fecha_devolucion IS NULL;

-- Libros nunca prestados (LEFT JOIN)

SELECT p.fecha_prestamo, l.*
FROM libro l
LEFT JOIN prestamo p ON p.id_bibliotecario = l.id
WHERE p.fecha_prestamo IS NULL;


-- Autores con número de libros prestados (JOIN + GROUP BY)

SELECT p.id, COUNT(p.id),  l.autor
FROM prestamo p
INNER JOIN libro l ON p.id_libro = l.id
GROUP BY p.fecha_prestamo;


-- 4. Consultas Resumen (8 consultas - 2.4 puntos)
-- Número de socios por ciudad

SELECT COUNT(id), ciudad 
FROM socio
GROUP BY ciudad;

-- Promedio de antigüedad de bibliotecarios

SELECT AVG(antiguedad) 
FROM bibliotecario;

-- Cantidad de préstamos por mes en 2023

SELECT COUNT(p.id)
FROM prestamo p
WHERE p.fecha_prestamo REGEXP '2023';

-- Libros más populares (por veces prestados)

SELECT p.id, COUNT(p.id), l.titulo
FROM prestamo p
INNER JOIN libro l ON p.id_libro = l.id
GROUP BY l.id;

-- Socios más activos (por préstamos realizados)

SELECT p.id, COUNT(p.id), s.nombre
FROM prestamo p
INNER JOIN socio s ON p.id_socio = s.id
GROUP BY s.id, s.nombre;


-- Porcentaje de libros disponibles

SELECT AVG(disponible) * 100.0 AS porcentaje_disponible_avg
FROM libro;


-- Días promedio de préstamo



-- Número de préstamos por categoría de socio

SELECT COUNT(p.fecha_prestamo), s.categoria
FROM prestamo p
INNER JOIN socio s ON p.id_socio = s.id
GROUP BY s.categoria;

-- 5. Subconsultas (8 consultas - 1.2 puntos)

-- Socios que han prestado libros de Gabriel García Márquez

SELECT s.*
FROM socio s
WHERE s.id IN (
SELECT p.id_socio
FROM prestamo p
INNER JOIN libro l ON p.id_libro = l.id
WHERE l.autor = 'Gabriel Garcia Marquez'
);

-- Libros con préstamos superiores al promedio


SELECT l.*
FROM libro l
WHERE id > (SELECT AVG(id_libro) FROM prestamo);

-- Socios con todos los préstamos devueltos a tiempo

SELECT s.*
FROM socio s
WHERE id  IN (SELECT id_socio FROM prestamo WHERE fecha_devolucion IS NOT NULL);

-- Bibliotecarios que no han gestionado préstamos

SELECT b.*
FROM bibliotecario b
WHERE id NOT IN (SELECT id_bibliotecario FROM prestamo);

-- Socios que han prestado más libros que el promedio

SELECT s.*
FROM socio s
WHERE id IN (SELECT AVG(fecha_prestamo) FROM prestamo WHERE fecha_prestamo < (SELECT fecha_prestamo FROM prestamo));

-- Libros disponibles que nunca han sido prestados

SELECT l.*
FROM libro l
WHERE id IN (SELECT id_libro FROM prestamo WHERE fecha_prestamo IS NULL);

-- Socios con préstamos en todas las categorías de libros

SELECT s.*
FROM socio s
WHERE categoria REGEXP '[A]'
AND categoria REGEXP '[B]'
AND categoria REGEXP '[C]'   
AND id IN (SELECT id_socio FROM prestamo);

-- Bibliotecarios que han gestionado préstamos de todos los socios de Madrid

SELECT *
FROM bibliotecario b
WHERE NOT EXISTS (
  SELECT 1
  FROM socio s
  WHERE s.ciudad = 'Madrid'
    AND NOT EXISTS (
      SELECT 1
      FROM prestamo p
      WHERE p.id_socio = s.id
        AND p.id_bibliotecario = b.id
    )
);
```


</details>










</div>
