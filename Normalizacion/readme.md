 <div align="justify"> 

# **__Unidad 2/3 Tarea 6__** (Normalización)



## __Ejercicio 1: Lista de Productos__

### Tabla Inicial: Productos

| ID_Producto | Nombre_Producto | Proveedores | Categoría   | Precio |
| ----------- | ----------------| ------------| ------------| ------ |
| 1           | Laptop          | Dell, HP    | Tecnología  | 1000   |
| 2           | Mouse           | Logitech    | Accesorios  | 25     |


#### *__PROBLEMA:__* En la columna de los proveedores (Dell, HP) tiene valores multivaluados incumpliendo el 1FN

### Aplicamos 1FN para arreglarlo.

| ID_Producto | Nombre_Producto | Proveedores | Categoría   | Precio |
| ----------- | ----------------| ------------| ------------| ------ |
| 1           | Laptop          | Dell        | Tecnología  | 1000   |
| 1           | Laptop          | HP          | Tecnología  | 25     |
| 2           | Mouse           | Logitech    | Accesorios  | 25     |

### Aplicamos 2FN ahora para eliminar dependencias.


#### Nueva Tabla: Producto

| ID_Producto | Nombre_Producto | Categoría  | Precio |
|-------------|-----------------|------------|--------|
| 1           | Laptop          | Tecnología | 1000   |
| 2           | Mouse           | Accesorios | 25     |

#### Nueva Tabla: Proveedor

| ID_Proveedor | Nombre_Proveedor |
|--------------|------------------|
| 1            | Dell             |
| 2            | HP               |
| 3            | Logitech         |




<img src="img/Ejercicio01.drawio.png">

## Ejercicio 2: Pedidos de Clientes

#### Tabla Inicial: Pedidos

| ID_Pedido | Cliente     | Dirección    | Producto | Cantidad | Precio |
| --------- | ----------- | ------------ | -------- | -------- | ------ |
| 101       | Juan Pérez  | Calle 123    | Laptop   | 1        | 1000   |
| 102       | Ana López   | Av. Central  | Teclado  | 2        | 50     |

#### *__PROBLEMA:__* (Dependencias funcionales) Los datos del cliente y del producto deben almacenarse por separado para evitar dependencias.

### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Cliente

| ID_Cliente | Nombre_Cliente | Dirección    |
|------------|----------------|--------------|
| 1          | Juan Pérez     | Calle 123    |
| 2          | Ana López      | Av. Central  |

#### Nueva Tabla: Pedido

| ID_Pedido | ID_Cliente | Fecha_Pedido |
|-----------|------------|--------------|
| 101       | 1          | 2023-10-01   |
| 102       | 2          | 2023-10-02   |

#### Nueva Tabla: Producto

| ID_Producto | Nombre_Producto | Precio |
|-------------|-----------------|--------|
| 1           | Laptop          | 1000   |
| 2           | Teclado         | 25     |



<img src="img/Ejercicio02.drawio.png">



### Ejercicio 3: Registro de Empleados

#### Tabla Inicial: Empleados
| ID_Empleado | Nombre    | Teléfonos      | Departamento |
| ----------- | --------- | -------------- | ------------ |
| 1           | Carlos R. | 12345, 67890   | Ventas       |
| 2           | Laura M.  | 54321          | Finanzas     |


#### *__PROBLEMA:__* En la columna de los *__Teléfonos__* tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN 

| ID_Empleado | Nombre    | Teléfonos      | Departamento |
| ----------- | --------- | -------------- | ------------ |
| 1           | Carlos R. | 12345          | Ventas       |
| 1           | Carlos R. | 67890          | Ventas       |
| 2           | Laura M.  | 54321          | Finanzas     |

### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Empleado

| ID_Empleado | Nombre    | Departamento |
|-------------|-----------|--------------|
| 1           | Carlos R. | Ventas       |
| 2           | Laura M.  | Finanzas     |

#### Nueva Tabla: Telefono

| ID_Telefono | ID_Empleado | Número_Teléfono |
|-------------|-------------|-----------------|
| 1           | 1           | 12345           |
| 2           | 1           | 67890           |
| 3           | 2           | 54321           |



<img src="img/Ejercicio03.drawio.png">


### Ejercicio 4: Reservas de Hotel

#### Tabla Inicial: Reservas

| ID_Reserva | Cliente   | Habitación | Fechas             | Precio |
| ---------- | --------- | ---------- | ------------------ | ------ |
| 5001       | Pedro G.  | 101        | 01/02,02/02,03/02  | 300    |
| 5002       | María T.  | 202        | 10/03,11/03        | 200    |


#### *__PROBLEMA:__* En la columna de las *__fechas__* tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN
| ID_Reserva | Cliente   | Habitación | Fechas             | Precio |
| ---------- | --------- | ---------- | ------------------ | ------ |
| 5001       | Pedro G.  | 101        | 01/02              | 300    |
| 5001       | Pedro G.  | 101        | 02/02              | 300    |
| 5001       | Pedro G.  | 101        | 03/02              | 300    |
| 5002       | María T.  | 202        | 10/03              | 200    |
| 5002       | María T.  | 202        | 11/03              | 200    |


### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Reserva

| ID_Reserva | Cliente   | Habitación | Precio |
|------------|-----------|------------|--------|
| 5001       | Pedro G.  | 101        | 300    |
| 5002       | María T.  | 202        | 200    |






<img src="img/Ejercicio04.drawio.png">


### Ejercicio 5: Inscripciones a Cursos

#### Tabla Inicial: Inscripciones

| ID_Inscripción | Estudiante | Curso       | Profesor    | Horarios                 |
| -------------- | ---------- | ----------- | ----------- | ------------------------ |
| 3001           | Luis R.    | Matemáticas | Prof. Pérez | Lunes 10AM,Miércoles 2PM |
| 3002           | Ana S.     | Física      | Prof. Gómez | Martes 3PM               |

#### *__PROBLEMA:__* En la columna de los *__horarios__* tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN

| ID_Inscripción | Estudiante | Curso       | Profesor    | Horarios                 |
| -------------- | ---------- | ----------- | ----------- | ------------------------ |
| 3001           | Luis R.    | Matemáticas | Prof. Pérez | Lunes 10AM               |
| 3001           | Luis R.    | Matemáticas | Prof. Pérez | Miércoles 2PM            |
| 3002           | Ana S.     | Física      | Prof. Gómez | Martes 3PM               |


### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Estudiante

| ID_Estudiante | Nombre_Estudiante |
|---------------|-------------------|
| 1             | Luis R.           |
| 2             | Ana S.            |

#### Nueva Tabla: Curso

| ID_Curso | Nombre_Curso |
|----------|--------------|
| 1        | Matemáticas  |
| 2        | Física       |

#### Nueva Tabla: Profesor

| ID_Profesor | Nombre_Profesor |
|-------------|-----------------|
| 1           | Prof. Pérez     |
| 2           | Prof. Gómez     |

#### Nueva Tabla: Inscripcion

| ID_Inscripcion | ID_Estudiante | ID_Curso | ID_Profesor |
|----------------|---------------|----------|-------------|
| 3001           | 1             | 1        | 1           |
| 3002           | 2             | 2        | 2           |


<img src="img/Ejercicio05.drawio.png">


### Ejercicio 6: Ventas de Tienda

### Tabla Inicial: Ventas
| ID_Venta | Cliente    | Productos Comprados | Total |
| -------- | ---------- | ------------------- | ----- |
| 8001     | Juan P.    | Celular,Funda       | 500   |
| 8002     | Andrea M.  | Laptop              | 1000  |


#### *__PROBLEMA:__* En la columna de los *__Productos Comprados__*  tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN

| ID_Venta | Cliente    | Productos Comprados | Total |
| -------- | ---------- | ------------------- | ----- |
| 8001     | Juan P.    | Celular             | 500   |
| 8001     | Juan P.    | Funda               | 500   |
| 8002     | Andrea M.  | Laptop              | 1000  |


### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Cliente

| ID_Cliente | Nombre_Cliente |
|------------|----------------|
| 1          | Juan P.        |
| 2          | Andrea M.      |

#### Nueva Tabla: Venta

| ID_Venta | ID_Cliente | Total |
|----------|------------|-------|
| 8001     | 1          | 500   |
| 8002     | 2          | 1000  |

#### Nueva Tabla: Producto

| ID_Producto | Nombre_Producto | Precio |
|-------------|-----------------|--------|
| 1           | Celular         | 400    |
| 2           | Funda           | 100    |
| 3           | Laptop          | 1000   |




<img src="img/Ejercicio06.drawio.png">


### Ejercicio 7: Biblioteca de Libros

#### Tabla Inicial: Libros

| ID_Libro | Título       | Autores    | Género          |
| -------- | ------------ | ---------- | --------------- |
| 101      | El Quijote   | Cervantes  | Novela          |
| 102      | 1984         | Orwell     | Ciencia Ficción |

#### *__PROBLEMA:__* En este caso particular en la columna *__autores__* no da problemas. Pero lo podrias dar a futuro en caso de que un libro tengo mas de un autor.

### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Libro

| ID_Libro | Título       | Género          |
|----------|--------------|-----------------|
| 101      | El Quijote   | Novela          |
| 102      | 1984         | Ciencia Ficción |

#### Nueva Tabla: Autor
| ID_Autor | Nombre_Autor |
|----------|--------------|
| 1        | Cervantes    |
| 2        | Orwell       |




<img src="img/Ejercicio07.drawio.png">


### Ejercicio 8: Facturación de Servicios

#### Tabla Inicial: Facturas

| ID_Factura | Cliente    | Servicios Contratados | Costo Total |
| ---------- | ---------- | --------------------- | ----------- |
| 9001       | Juan P.    | Internet,TV           | 50          |
| 9002       | Ana M.     | Teléfono              | 20          |

#### *__PROBLEMA:__* En la columna de los *__Servicios Contradados__* tiene valores multivaluados incumpliendo el 1FN.

#### Aplicamos 1FN

| ID_Factura | Cliente    | Servicios Contratados | Costo Total |
| ---------- | ---------- | --------------------- | ----------- |
| 9001       | Juan P.    | Internet              | 50          |
| 9001       | Juan P.    | TV                    | 50          |
| 9002       | Ana M.     | Teléfono              | 20          |


### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Cliente

| ID_Cliente | Nombre_Cliente |
|------------|----------------|
| 1          | Juan P.        |
| 2          | Ana M.         |

#### Nueva Tabla: Factura

| ID_Factura | ID_Cliente | Costo_Total |
|------------|------------|-------------|
| 9001       | 1          | 50          |
| 9002       | 2          | 20          |

#### Nueva Tabla: Servicio

| ID_Servicio | Nombre_Servicio |
|-------------|-----------------|
| 1           | Internet        |
| 2           | TV              |
| 3           | Teléfono        |



<img src="img/Ejercicio08.drawio.png">


### Ejercicio 9: Gestión de Vehículos

#### Tabla Inicial: Vehículos

| ID_Vehículo | Marca   | Modelos         | Año  |
| ----------- | ------- | --------------- | ---- |
| 5001        | Toyota  | Corolla,Yaris   | 2022 |
| 5002        | Honda   | Civic           | 2023 |

### *__PROBLEMA:__* En la columna de los *__Modelos__* tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN 

| ID_Vehículo | Marca   | Modelos         | Año  |
| ----------- | ------- | --------------- | ---- |
| 5001        | Toyota  | Corolla         | 2022 |
| 5001        | Toyota  | Yaris           | 2022 |
| 5002        | Honda   | Civic           | 2023 |

### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Marca

| ID_Marca | Nombre_Marca |
|----------|--------------|
| 1        | Toyota       |
| 2        | Honda        |

#### Nueva Tabla: Modelo

| ID_Modelo | ID_Marca | Nombre_Modelo | Año  |
|-----------|----------|---------------|------|
| 1         | 1        | Corolla       | 2022 |
| 2         | 1        | Yaris         | 2022 |
| 3         | 2        | Civic         | 2023 |


<img src="img/Ejercicio09.drawio.png">

### Ejercicio 10: Gestión de Proyectos

### Tabla Inicial: Proyectos
| ID_Proyecto | Nombre     | Miembros       | Presupuesto |
| ----------- | ---------- | -------------- | ----------- |
| 7001        | Web App    | Juan,Ana       | 5000        |
| 7002        | E-commerce | Pedro,María    | 10000       |

### *__PROBLEMA:__* En la columna de los *__Miembros__* tiene valores multivaluados incumpliendo el 1FN.

### Aplicamos 1FN 

| ID_Proyecto | Nombre     | Miembros       | Presupuesto |
| ----------- | ---------- | -------------- | ----------- |
| 7001        | Web App    | Juan           | 5000        |
| 7001        | Web App    | Ana            | 5000        |
| 7002        | E-commerce | Pedro          | 10000       |
| 7002        | E-commerce | María          | 10000       |

### Aplicamos 2FN ahora para eliminar dependencias.

#### Nueva Tabla: Proyecto

| ID_Proyecto | Nombre     | Presupuesto |
|-------------|------------|-------------|
| 7001        | Web App    | 5000        |
| 7002        | E-commerce | 10000       |

#### Nueva Tabla: Empleado

| ID_Miembros | Nombre_Empleado |
|-------------|-----------------|
| 1           | Juan            |
| 2           | Ana             |
| 3           | Pedro           |
| 4           | María           |



<img src="img/Ejercicio10.drawio.png">

 </div>