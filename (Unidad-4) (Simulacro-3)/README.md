<div align="justify">

# <img Code, Learn & Practice("Simulacro de bbdd 🧪: Consultas, Índices, Vistas, Funciones y Procedimientos")

<div align="center">
<img src="https://www.seguridadkimika.eus/wp-content/uploads/2017/10/sirenas-seguridad-kimika-simulacro.jpg" width="200px"/>
</div>


## 📄 Parte 1: Consultas para Explorar la Estructura de las Tablas

1. Mostrar las columnas de la tabla `estudiantes`.

```sql
SELECT * FROM estudiantes;
```

2. Mostrar las columnas de la tabla `cursos`.

```sql
SELECT * FROM cursos;
```

3. Mostrar las columnas de la tabla `matriculas`.

```sql
SELECT * FROM matriculas;
```

---

## 📊 Parte 2: Consultas Avanzadas sobre Datos

4. Mostrar cada estudiante con la cantidad de cursos en los que está matriculado.

```sql
SELECT e.nombre, COUNT(m.curso_id)
FROM estudiantes e
JOIN matriculas m ON m.estudiante_id = e.id
JOIN cursos c ON m.curso_id = c.id
GROUP BY e.nombre;
```

5. Mostrar cada estudiante con el total de créditos acumulados.

```sql
SELECT e.nombre, SUM(c.creditos)
FROM estudiantes e
JOIN matriculas m ON m.estudiante_id = e.id
JOIN cursos c ON c.id = m.curso_id
GROUP BY e.nombre;
```

6. Mostrar cursos con la cantidad de estudiantes matriculados, ordenados de mayor a menor.

```sql
SELECT c.nombre, COUNT(m.estudiante_id), c.creditos
FROM cursos c
JOIN matriculas m ON m.curso_id = c.id
JOIN estudiantes e ON m.estudiante_id = e.id
GROUP BY c.id
ORDER BY c.nombre  DESC;
```

7. Mostrar la media de créditos por curso.

```sql
SELECT AVG(creditos) FROM cursos GROUP BY nombre
```

8. Listar los cursos que no tienen estudiantes matriculados.

```sql
SELECT c.nombre
FROM cursos c
JOIN matriculas m ON c.id = m.curso_id
WHERE m.estudiante_id NOT IN (SELECT id FROM estudiantes);
```

9. Mostrar el nombre del profesor y cuántos cursos imparte.

```sql
SELECT p.nombre, COUNT(c.profesor_id)
FROM profesores p
JOIN cursos c ON p.id = c.profesor_id
GROUP BY c.profesor_id;
```

10. Mostrar los profesores que no imparten ningún curso.

```sql
SELECT p.*
FROM profesores p
WHERE p.id NOT IN (SELECT profesor_id FROM cursos);
```

11. Mostrar la ciudad con mayor número de estudiantes registrados.

```sql
SELECT e.ciudad, COUNT(e.id)
FROM estudiantes e
GROUP BY e.id;
```

12. Mostrar estudiantes que están matriculados en más de 1 curso.

```sql
SELECT e.nombre, COUNT(m.estudiante_id)
FROM estudiantes e
JOIN matriculas m ON e.id = m.estudiante_id
GROUP BY m.estudiante_id
HAVING COUNT(m.estudiante_id) > 1;
```

13. Listar cursos junto a su clasificación según créditos:
    - 6 o más: "Alta carga"
    - Menos de 6: "Carga estándar"

```sql
SELECT nombre, creditos,

CASE

WHEN creditos >= 6 THEN 'CAGA ALTA'
WHEN creditos < 6 THEN 'CARGA BAJA'

END AS Carga

FROM cursos;
```

14. Listar estudiantes y clasificar su carga académica:
    - Más de 12 créditos: "Carga Alta"
    - 6 a 12 créditos: "Carga Media"
    - Menos de 6 créditos: "Carga Baja"

```sql
SELECT e.nombre, c.creditos,

CASE

WHEN creditos > 12 THEN 'CAGA ALTA'
WHEN creditos BETWEEN 6 AND 12 THEN 'CARGA MEDIA'
WHEN creditos < 6 THEN 'CARGA BAJA'

END AS Carga

FROM estudiantes e
INNER JOIN matriculas m ON e.id = m.estudiante_id
INNER JOIN cursos c ON c.id = m.curso_id
```

15. Mostrar cursos en los que se haya matriculado al menos un estudiante de Sevilla.

```sql
SELECT c.*, e.ciudad
FROM cursos c
INNER JOIN matriculas m ON c.id = m.curso_id
INNER JOIN estudiantes e ON e.id = m.estudiante_id
WHERE e.ciudad = 'Sevilla';
```

16. Listar los cursos impartidos por profesores del departamento de Matemáticas.

```sql
SELECT c.*, p.nombre, p.departamento
FROM cursos c
INNER JOIN profesores p ON c.profesor_id = p.id
WHERE p.departamento = 'Matemáticas';
```

17. Mostrar los cursos en los que se haya inscrito algún estudiante antes del año 2022.

```sql
SELECT c.nombre, e.nombre, m.fecha
FROM cursos c
INNER JOIN matriculas m ON c.id = m.curso_id
INNER JOIN estudiantes e ON e.id = m.estudiante_id
WHERE m.fecha < '2022-01-01'
```

18. Mostrar estudiantes que han cursado materias impartidas por el profesor “Dr. Luis Gómez”.

```sql
SELECT e.nombre, p.departamento, p.nombre
FROM estudiantes e
INNER JOIN matriculas m ON e.id = m.id
INNER JOIN cursos c ON c.id = m.curso_id
INNER JOIN profesores p ON p.id = c.profesor_id
WHERE p.nombre = 'Dr. Luis Gómez'; 
```

19. Mostrar los cursos más recientes (última matrícula por curso).

```sql
SELECT c.nombre, m.fecha
FROM cursos c
INNER JOIN matriculas m ON c.id = m.curso_id
ORDER BY m.fecha DESC;
```

20. Mostrar el número total de estudiantes por departamento del profesor que imparte el curso.

```sql
SELECT COUNT(e.id), p.departamento
FROM estudiantes e
INNER JOIN matriculas m ON e.id = m.estudiante_id
INNER JOIN cursos c ON c.id = m.curso_id
INNER JOIN profesores p ON p.id = c.profesor_id
GROUP BY p.departamento;
```

---

## ⚙ Parte 3: Procedimiento Almacenado

1. Crear un procedimiento llamado `inscribir_estudiante` que reciba:
   - ID del estudiante
   - ID del curso
   - Fecha de inscripción  
   El procedimiento debe:
   - Verificar que el estudiante no esté ya matriculado en ese curso.
   - Si no lo está, insertarlo en `matriculas`; si ya lo está, lanzar un error.

```sql
DROP PROCEDURE inscribir_estudiante;

DELIMITER // 

CREATE PROCEDURE inscribir_estudiante(

IN id_estudiante INT,
IN id_curso INT,
IN fecha_inscripcion DATE

)

BEGIN

DECLARE mensaje_resultado VARCHAR(100);

IF NOT EXISTS (SELECT 1 FROM estudiantes WHERE id = id_estudiante) THEN 
SET mensaje_resultado = 'ID estudiante EXISTE'; 

ELSEIF NOT EXISTS (SELECT 1 FROM cursos WHERE id = id_curso) THEN 
SET mensaje_resultado = 'ID CURSO EXISTE';

ELSE 
    INSERT INTO matriculas (estudiante_id, curso_id, fecha)
    VALUES (id_estudiante, id_curso, fecha_inscripcion);
    SET mensaje_resultado = 'Estudiante Inscrito';

END IF;

END //
```

2. Ejecutar el procedimiento para inscribir al estudiante con ID 1 en el curso con ID 2.

```sql
CALL inscribir_estudiante(1, 2, '2030-01-01');
```

3. Eliminar el procedimiento.


```sql
DROP PROCEDURE inscribir_estudiante;
```

---

## 🪞 Parte 4: Vistas

1. Crear una vista llamada `resumen_matriculas` que muestre:
   - Nombre del estudiante
   - Nombre del curso
   - Nombre del profesor
   - Fecha de matrícula

```sql
DROP VIEW IF EXISTS resumen_matriculas;

CREATE VIEW resumen_matriculas AS

SELECT e.nombre AS nombreEstudiante, c.nombre AS nombreCurso, p.nombre AS nombreProfesor, m.fecha
FROM estudiantes e
INNER JOIN matriculas m ON e.id = m.estudiante_id
INNER JOIN cursos c ON c.id = m.curso_id
INNER JOIN profesores p ON p.id = c.profesor_id;
```

2. Consultar los datos desde la vista, mostrando nombre del estudiante y curso.

```sql
SELECT nombreEstudiante, nombreCurso FROM resumen_matriculas;
```

3. Eliminar la vista.

```sql
DROP VIEW IF EXISTS resumen_matriculas;
```

---

## 🧮 Parte 5: Función Definida por el Usuario

1. Crear una función llamada `promedio_creditos_por_anio` que reciba un año como parámetro y devuelva el promedio de créditos matriculados por estudiante ese año.

```sql
DROP FUNCTION IF EXISTS promedio_creditos_por_anio;

DELIMITER //

CREATE FUNCTION promedio_creditos_por_anio(anio INT) RETURNS DECIMAL(10,2)

READS SQL DATA

DETERMINISTIC

BEGIN

DECLARE promedio_creditos DECIMAL (10,2);

SELECT e.nombre, AVG(c.creditos) INTO promedio_creditos FROM cursos c
JOIN matriculas m ON m.curso_id = c.id
JOIN estudiantes e ON m.estudiante_id = e.id
GROUP BY e.nombre
HAVING YEAR(m.fecha) = anio;

RETURN promedio_creditos;

END //

DELIMITER ;
```

2. Ejecutar la función para el año 2023.

```sql
SELECT promedio_creditos_por_anio(2023);
```

3. Eliminar la función.

```sql
DROP FUNCTION IF EXISTS promedio_creditos_por_anio;
```

---

## 📂 Parte 6: Índices

1. Crear un índice en la columna `fecha` de la tabla `matriculas`.

```sql
CREATE INDEX idx_fecha ON matriculas(fecha);
```

2. Crear un índice compuesto en la tabla `matriculas` sobre `estudiante_id` y `curso_id`.

```sql
CREATE INDEX idx_estudiante_id_curso_id ON matriculas(estudiante_id, curso_id);
```

3. Consultar los índices de la tabla `matriculas`.

```sql
SHOW INDEX FROM matriculas;
```

4. Eliminar ambos índices.

```sql
DROP INDEX idx_fecha ON matriculas;
DROP INDEX idx_estudiante_id_curso_id ON matriculas;
```

---

## 🕵️ Parte 7: Trigger de Auditoría

1. Crear una tabla llamada `auditoria_matriculas` que registre:
   - Tipo de operación (INSERT)
   - ID del estudiante
   - ID del curso
   - Fecha y hora de la operación
   - Usuario que realizó la acción

```sql
DROP TABLE IF EXISTS auditoria_matriculas;

CREATE TABLE auditoria_matriculas (

tipo_operacion VARCHAR(50),
id_estudiante INT,
id_curso INT,
fecha_hora DATETIME,
usuario_accion VARCHAR(50)
)
```

2. Crear un trigger `AFTER INSERT` sobre `matriculas` que inserte un registro en `auditoria_matriculas` al realizar una matrícula.

```sql
DROP TRIGGER IF EXISTS auditoria_matriculas;

DELIMITER //

CREATE TRIGGER after_insert_matricula

AFTER INSERT ON matriculas

FOR EACH ROW

BEGIN

INSERT INTO auditoria_matriculas(tipo_operacion, id_estudiante, id_curso, fecha_hora, usuario_accion)
VALUES ('INSERT', NEW.estudiante_id, NEW.curso_id, NOW(), CURRENT_USER());

END //

DELIMITER ;
```

3. Consultar los registros de la auditoría.

```sql
SELECT * FROM auditoria_matriculas;
```

4. Eliminar el trigger y la tabla de auditoría.

```sql
DROP TRIGGER auditoria_matriculas
```



</div>