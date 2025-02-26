 <div align="justify"> 

# **__(Unidad-4) (Tarea-7)__** (Normalización)


## __Ejercicio: Gestión Tienda__


### Tabla Inicial: Tienda

| ProductoID | Nombre        | Categorías                | Precio | ClienteID | NombreCliente | DireccionesEnvio                         |
|------------|---------------|---------------------------|--------|-----------|---------------|------------------------------------------|
| 1          | Laptop HP     | Electrónicos, Informática | 800    | 101       | Juan          | Calle 1, Ciudad A / Calle 2, Ciudad A    |
| 2          | Camiseta Nike | Ropa, Deportes            | 30     | 102       | María         | Calle 3, Ciudad B                        |
| 3          | Libro "Dune"  | Libros, Ciencia Ficción   | 20     | 101       | Juan          | Calle 1, Ciudad A                        |


#### 1. No cumple con la 1FN porque hay valores multivaluados en varias columnas

**Solución:**

| ProductoID | Nombre        | Categoría       | Precio | ClienteID | NombreCliente | DireccionesEnvio      | tipoCiudad |
|------------|---------------|-----------------|--------|-----------|---------------|---------------------|------------|
| 1          | Laptop HP     | Electrónicos    | 800    | 101       | Juan          | Calle 2             | Ciudad A   |   
| 1          | Laptop HP     | Electrónicos    | 800    | 101       | Juan          | Calle 1             | Ciudad A   |        
| 1          | Laptop HP     | Informática     | 800    | 101       | Juan          | Calle 1             | Ciudad A   |         
| 1          | Laptop HP     | Informática     | 800    | 101       | Juan          | Calle 2             | Ciudad A   |
| 2          | Camiseta Nike | Ropa            | 30     | 102       | María         | Calle 3             | Ciudad B   |
| 2          | Camiseta Nike | Deportes        | 30     | 102       | María         | Calle 3             | Ciudad B   |
| 3          | Libro "Dune"  | Libros          | 20     | 101       | Juan          | Calle 1             | Ciudad A   |
| 3          | Libro "Dune"  | Ciencia Ficción | 20     | 101       | Juan          | Calle 1             | Ciudad A   |



#### 2. No cumple con la 2FN porque hay depencias. Por tanto habra que eliminar las dependencias parciales.


**Tabla Productos:**

| ProductoID | Nombre        | Precio |
|------------|---------------|--------|
| 1          | Laptop HP     | 800    |
| 2          | Camiseta Nike | 30     |
| 3          | Libro "Dune"  | 20     |


**Tabla CategoríasProductos:**

| ProductoID | Categoría       |
|------------|-----------------|
| 1          | Electrónicos    |
| 1          | Informática     |
| 2          | Ropa            |
| 2          | Deportes        |
| 3          | Libros          |
| 3          | Ciencia Ficción |


**Tabla Clientes:**


| ClienteID | NombreCliente |
|-----------|---------------|
| 101       | Juan          |
| 102       | María         |


**Tabla DireccionesClientes:**


| ClienteID | DireccionesEnvio   | tipoCiudad |
|-----------|--------------------|------------|
| 101       | Calle 1, Ciudad A  | Ciudad A   |
| 101       | Calle 2, Ciudad A  | Ciudad A   |
| 102       | Calle 3, Ciudad B  | Ciudad B   |


**Tabla Ventas:**


| VentaID | ProductoID | ClienteID | DireccionesEnvio   | tipoCiudad |
|---------|------------|-----------|--------------------|------------|
| 1       | 1          | 101       | Calle 1            | Ciudad A   |
| 2       | 1          | 101       | Calle 2            | Ciudad A   |
| 3       | 2          | 102       | Calle 3            | Ciudad B   |
| 4       | 3          | 101       | Calle 1            | Ciudad A   |
          

#### 3. Cumple con 3FN porque los atributos dependen de clave primaria exclusivamente.


 </div>