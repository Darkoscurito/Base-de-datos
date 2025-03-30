<div align="justify">


# __Unidad 3 Tarea 6__ (Expresiones Regulares y Funciones)


### 📜📜 FUNCIONES Y EXPRESIONES REGULARES (SQL) 📜📜

## EXPRESIONES REGULARES (SQL)

| Operador  | Descripción                                      | Ejemplo                |
|-----------|--------------------------------------------------|------------------------|
| `.`       | Coincide con cualquier carácter excepto nueva línea | `a.b` coincide con "aab", "abb", "acb", etc. |
| `^`       | Coincide con el inicio de la cadena               | `^abc` coincide con "abc" al inicio de la cadena. |
| `$`       | Coincide con el final de la cadena                | `xyz$` coincide con "xyz" al final de la cadena. |
| `*`       | Coincide con cero o más repeticiones del elemento anterior | `a*b` coincide con "ab", "aab", "aaab", etc. |
| `+`       | Coincide con una o más repeticiones del elemento anterior | `a+b` coincide con "ab", "aab", "aaab", etc. |
| `?`       | Coincide con cero o una repetición del elemento anterior | `a?b` coincide con "ab" o "b". |
| `\`       | Escapa el significado especial de un carácter      | `\.` coincide con el carácter punto literal. |
| `[]`      | Coincide con cualquier carácter dentro de los corchetes | `[aeiou]` coincide con cualquier vocal. |
| `[^]`     | Coincide con cualquier carácter que no esté dentro de los corchetes | `[^0-9]` coincide con cualquier carácter que no sea un dígito. |
| `()`      | Agrupa elementos para aplicar operadores a una expresión completa | `(abc)+` coincide con "abc", "abcabc", etc. |
| `\d`      | Coincide con un dígito (equivalente a `[0-9]`)   | `\d{3}` coincide con tres dígitos. |
| `\w`      | Coincide con un carácter de palabra (letras, dígitos, guiones bajos) | `\w+` coincide con una o más palabras. |
| `\s`      | Coincide con un carácter de espacio en blanco     | `\s*` coincide con cero o más espacios en blanco. |
| `|`       | Operador lógico "o"                               | `a|b` coincide con "a" o "b". |

## FUNCIONES (SQL)

| Categoría                   | Función                           | Descripción                                               |
|-----------------------------|-----------------------------------|-----------------------------------------------------------|
| **Funciones de Texto**      | `LENGTH(str)`                     | Devuelve la longitud de la cadena.                         |
|                             | `SUBSTR(str, start, length)`       | Devuelve una subcadena de la cadena dada.                 |
|                             | `UPPER(str)`, `LOWER(str)`         | Convierte la cadena a mayúsculas o minúsculas.            |
| **Funciones Numéricas**     | `ABS(x)`                          | Devuelve el valor absoluto de x.                           |
|                             | `ROUND(x)`, `CEIL(x)`, `FLOOR(x)` | Redondeo de números.                                      |
|                             | `MAX(x, y, ...)`, `MIN(x, y, ...)` | Devuelve el valor máximo o mínimo entre los argumentos.   |
| **Funciones de Fecha y Hora**| `CURRENT_DATE`, `CURRENT_TIME`, `CURRENT_TIMESTAMP` | Devuelven la fecha, la hora o la marca de tiempo actuales. |
|                             | `DATE(str)`, `TIME(str)`, `DATETIME(str)` | Extraen partes de una fecha o marca de tiempo.             |
| **Funciones de Agregación**  | `SUM(column)`, `AVG(column)`      | Realizan operaciones de suma y promedio en una columna.    |
|                             | `COUNT(column)`, `MAX(column)`, `MIN(column)` | Realizan operaciones de conteo, máximo y mínimo en una columna. |
| **Funciones de Conversión**  | `CAST(expr AS type)`              | Convierte una expresión a un tipo de datos específico.    |
| **Funciones de Manipulación de Cadenas** | `CONCAT(str1, str2, ...)`  | Concatena cadenas.                                        |
| **Funciones de Control de Flujo** | `CASE WHEN condition THEN result END` | Realiza evaluaciones condicionales.                       |

### __1.__ Obtener todos los clientes.



<img src="img/ejercicio(1).png">

<br>

### __2.__ Obtener la cantidad total de productos en todos los pedidos



<img src="img/ejercicio(2).png">

<br>

### __3.__ Obtener el precio promedio de los productos.

<img src="img/ejercicio(3).png">

<br>

### __4.__ Obtener los clientes que tienen un email válido (contiene '@')



<img src="img/ejercicio(4).png">

<br>

### __5.__ Obtener el producto más caro.


<img src="img/ejercicio(5).png">

<br>

### __6.__ Obtener los pedidos realizados en febrero de 2024.



<img src="img/ejercicio(6).png">

<br>

### __7.__ Obtener la cantidad total de productos en todos los pedidos por producto.



<img src="img/ejercicio(7).png">

<br>

### __8.__ Obtener los clientes que han realizado más de un pedido.



<img src="img/ejercicio(8).png">

<br>

### __9.__ Obtener los productos que tienen un precio registrado.



<img src="img/ejercicio(9).png">

<br>

### __10.__ Obtener la fecha del primer pedido realizado:


<img src="img/ejercicio(10).png">

<br>

### __11.__ Obtener los productos cuyos nombres comienzan con 'A' o 'B':



<img src="img/ejericicio(11).png">

<br>

### __12.__ Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.



<img src="img/ejercicio(12).png">

<br>

### __13.__ Obtener los clientes que han realizado más de un pedido en febrero de 2024.



<img src="img/ejercicio(13).png">

<br>

### __14.__ Obtener los productos con precio entre 100 y 500.



<img src="img/ejercicio(14).png">

<br>

### __15.__ Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cantidad descendente.



<img src="img/ejercicio(15).png">

<br>

### __16.__ Obtener los clientes que tienen una 'a' en cualquier posición de su nombre.



<img src="img/ejercicio(16).png">

<br>

### __17.__ Obtener el precio máximo de los productos.



<img src="img/ejercicio(17).png">

<br>

### __18.__ Obtener los pedidos realizados por el cliente con ID 1 en febrero de 2024.



<img src="img/ejercicio(18).png">

<br>

### __19.__ Obtener la cantidad total de productos en todos los pedidos por producto ordenado por total de productos descendente.



<img src="img/ejercicio(19).png">

<br>

### __20.__ Obtener los productos que no tienen un precio registrado.



<img src="img/ejercicio(20).png">

<br>

### __21.__ Obtener la fecha del último pedido realizado.



<img src="img/ejercicio(21).png">

<br>

### __22.__ Obtener los clientes cuyo nombre tiene al menos 5 caracteres.



<img src="img/ejercicio(22).png">

<br>

### __23.__ Obtener los productos que tienen la letra 'o' en cualquier posición del nombre.



<img src="img/ejercicio(23).png">

<br>

### __24.__ Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.



<img src="img/ejercicio(24).png">

<br>

### __25.__ Obtener los clientes cuyos nombres no contienen la letra 'i':



<img src="img/ejercicio(25).png">

<br>

### __26.__ Obtener los pedidos realizados por el cliente con ID 2 en febrero de 2024.



<img src="img/ejercicio(26).png">

<br>

### __27.__ Obtener el precio mínimo de los productos.



<img src="img/ejercicio(27).png">

<br>

### __28.__ Obtener los clientes que han realizado al menos un pedido en febrero de 2024.



<img src="img/ejercicio(28).png">

<br>

### __29.__ Obtener la fecha del último pedido realizado por el cliente con ID 3.



<img src="img/ejercicio(29).png">

<br>

### __30.__ Obtener los productos que tienen una 'a' al final del nombre.



<img src="img/ejercicio(30).png">

<br>

### __31.__ Obtener los clientes cuyos nombres tienen al menos 4 vocales (mayúsculas|minúsculas).



<img src="img/ejercicio(31).png">

<br>

### __32.__ Obtener los productos cuyo precio tenga al menos 4 números sin contrar los decimales.


<img src="img/ejercicio(32).png">

### __33.__ Obtener los clientes cuyos nombres tienen al menos una 'a' seguida de una 'e'.



<img src="img/ejercicio(33).png">

<br>

### __34.__ Obtener los productos cuyos nombres terminan con una consonante.


<img src="img/ejercicio(34).png">

### __35.__ Obtener los productos cuyos nombres empiezan con una vocal.



<img src="img/ejercicio(35).png">

<br>

</div>