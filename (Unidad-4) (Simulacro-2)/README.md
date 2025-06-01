<div align="justify">

# Simulacro de bbdd 🧪: Consultas, Índices, Vistas, Funciones y Procedimientos")

<div align="center">
<img src="https://www.seguridadkimika.eus/wp-content/uploads/2017/10/sirenas-seguridad-kimika-simulacro.jpg" width="200px"/>
</div>



## 🔎 Parte 1: Consultas SQL

### A. Consultas Simples

1. Mostrar todos los cursos disponibles.

```sql
SELECT * FROM cursos;
```

2. Mostrar el nombre de todos los profesores.

```sql
SELECT nombre FROM profesores;
```

3. Listar todas las matrículas.

```sql
SELECT * FROM matriculas;
```

4. Ver los nombres y correos de los estudiantes.

```sql
SELECT nombre, email FROM estudiantes;
```

5. Ver los cursos y su número de créditos.

```sql
SELECT nombre, creditos FROM cursos;
```
---

### B. Consultas con `WHERE`. Obligatorio utilizar **WHERE** donde se **combine dos o más tablas**

1. Obtener los cursos impartidos por profesores del departamento de Informática.

```sql
SELECT c.* FROM cursos c, profesores p WHERE c.profesor_id = p.id;
```

2. Obtener los estudiantes que viven en Madrid.

```sql
SELECT * FROM estudiantes WHERE ciudad REGEXP 'Madrid';
```

3. Mostrar los cursos con más de 5 créditos.

```sql
SELECT * FROM cursos WHERE creditos > 5;
```

4. Ver las matrículas realizadas después del año 2022.

```sql
SELECT * FROM matriculas WHERE fecha REGEXP '2022';
```

5. Ver los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
SELECT * FROM cursos c, profesores p 
WHERE c.profesor_id = p.id
AND p.nombre = 'Dra. Ana Torres';
```

---

### C. Consultas con `JOIN`.  Obligatorio utilizar **JOIN** donde se **combine dos o más tablas**

> (Devuelven el mismo resultado que las anteriores, pero usando combinaciones de tablas)

1. Mostrar cursos impartidos por profesores del departamento de Informática.

```sql
SELECT c.* FROM cursos c
JOIN profesores p ON c.profesor_id = p.id;
```

2. Obtener estudiantes que viven en Madrid.

```sql
SELECT * FROM estudiantes WHERE ciudad REGEXP 'Madrid';
```

3. Mostrar cursos con más de 5 créditos.

```sql
SELECT * FROM cursos WHERE creditos > 5;
```

4. Listar matrículas realizadas después del año 2022.

```sql
SELECT * FROM matriculas WHERE fecha REGEXP '2022';
```

5. Mostrar los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
SELECT * FROM cursos c
INNER JOIN profesores p ON c.profesor_id = p.id
WHERE p.nombre = 'Dra. Ana Torres';
```
---

### D. Consultas con Subconsultas

> (Devuelven el mismo resultado que las anteriores, pero usando subconsultas)

1. Cursos impartidos por profesores del departamento de Informática.

```sql
SELECT * FROM cursos c
WHERE c.profesor_id IN (SELECT id FROM profesores);
```

2. Estudiantes que viven en Madrid.

```sql
SELECT * FROM cursos c
WHERE c.id IN (SELECT id FROM estudiantes WHERE ciudad REGEXP 'Madrid');
```

3. Cursos con más de 5 créditos.

```sql
SELECT * FROM cursos c
WHERE c.id IN (SELECT id FROM cursos WHERE creditos > 5);
```

4. Matrículas realizadas después del año 2022.

```sql
SELECT * FROM matriculas m
WHERE m.id IN (SELECT id FROM matriculas WHERE fecha REGEXP '2022');
```

5. Cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
SELECT c.* FROM cursos c
WHERE c.profesor_id IN (SELECT id FROM profesores WHERE nombre REGEXP 'Dra. Ana Torres'); 
```

---

## 📂 Parte 2: Índices

1. Crear un índice en la columna `ciudad` de la tabla `estudiantes`.

```sql
CREATE INDEX idx_ciudad ON estudiantes(ciudad);
```

2. Crear un índice en la columna `departamento` de la tabla `profesores`.

```sql
CREATE INDEX idx_departamento ON profesores(departamento);
```

3. Consultar los índices creados.

```sql
SHOW INDEX FROM estudiantes;
SHOW INDEX FROM profesores;
```

4. Eliminar ambos índices.

```sql
DROP INDEX idx_ciudad ON estudiantes;
DROP INDEX idx_departamento ON profesores;
```
---

## 🪞 Parte 3: Vistas

1. Crear una vista llamada `vista_matriculas_completas` que muestre:
   - nombre del estudiante,
   - nombre del curso,
   - fecha de la matrícula.

```sql
CREATE VIEW vista_matriculas_completas AS

SELECT e.nombre AS nombreEstudiante, c.nombre AS nombreCurso, m.fecha AS fechaMatricula
FROM estudiantes e
JOIN matriculas m ON e.id = m.estudiante_id
JOIN cursos c ON c.id = m.curso_id;
```

2. Consultar datos desde la vista, mostrando el nombre del estudiante y la fecha de matrícula.

```sql
SELECT nombreEstudiante, fechaMatricula FROM vista_matriculas_completas;
```

3. Eliminar la vista.

```sql
DROP VIEW vista_matriculas_completas;
```

---

## ⚙ Parte 4: Procedimiento Almacenado

1. Crear un procedimiento llamado `cursos_por_profesor` que reciba el nombre del profesor como parámetro y devuelva los cursos que imparte y su número de créditos.

```sql
DROP PROCEDURE IF EXISTS cursos_por_profesor;

DELIMITER //

CREATE PROCEDURE cursos_por_profesor(
IN nombre_profesor VARCHAR(50)
)

BEGIN

SELECT c.nombre, c.creditos FROM cursos c
INNER JOIN profesores p ON c.profesor_id = p.id
WHERE nombre_profesor = p.nombre;

END //

DELIMITER ;
```

2. Ejecutar el procedimiento con el nombre “Dr. Luis Gómez”.

```sql
CALL cursos_por_profesor('Dr. Luis Gómez');
```

3. Eliminar el procedimiento.

```sql
DROP PROCEDURE cursos_por_profesor;
```

---

## 🔢 Parte 5: Función Definida por el Usuario

1. Crear una función llamada `total_creditos_estudiante` que reciba el ID de un estudiante y devuelva el total de créditos que ha matriculado.

```sql
DROP FUNCTION IF EXISTS total_creditos_estudiante;

DELIMITER //

CREATE FUNCTION total_creditos_estudiante(id_estudiante INT) RETURNS DECIMAL(10,2)

READS SQL DATA

DETERMINISTIC

BEGIN

DECLARE total_creditos DECIMAL(10,2);

SELECT SUM(c.creditos) INTO total_creditos FROM cursos c
JOIN matriculas m ON c.id = m.curso_id
WHERE m.estudiante_id = id_estudiante;

RETURN total_creditos;

END // 

DELIMITER ;
```

2. Ejecutar la función para un estudiante específico.

```sql
SELECT total_creditos_estudiante(1);
```

3. Eliminar la función.

```sql
DROP FUNCTION total_creditos_estudiante;
```

</div>