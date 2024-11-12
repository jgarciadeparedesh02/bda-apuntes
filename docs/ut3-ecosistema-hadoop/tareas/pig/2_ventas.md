# Tarea: Análisis de Datos de Ventas usando Apache Pig

### Objetivo

En esta tarea, usarás **Apache Pig** para analizar un conjunto de datos de ventas de una tienda. El objetivo es realizar filtrado y ordenación de los datos a partir de un archivo CSV proporcionado. Este archivo contiene información sobre las transacciones diarias de la tienda, incluyendo detalles como fecha, cliente, producto, cantidad y precio unitario.

### Archivo CSV de Entrada

El archivo CSV de entrada `ventas.csv` tiene el siguiente formato y contenido de ejemplo:

```csv
fecha,id_cliente,producto,cantidad,precio_unitario
2024-01-01,1,televisor,1,500
2024-01-01,2,laptop,1,800
2024-01-02,3,tablet,2,200
2024-01-02,1,smartphone,1,300
2024-01-03,4,televisor,1,500
2024-01-03,5,laptop,1,800
2024-01-03,2,tablet,3,200
2024-01-04,3,smartphone,2,300
```

### Ejercicios

1. **Filtrar ventas de productos específicos y ordenar por cantidad vendida**

    Filtra las ventas de productos específicos, en este caso `laptop` y `tablet`, y ordénalas por la cantidad vendida de mayor a menor.

    - **Instrucciones:** 
        - Carga los datos desde el archivo `ventas.csv`.
        - Filtra solo las filas que corresponden a los productos `laptop` y `tablet`.
        - Ordena el resultado por la columna `cantidad` en orden descendente.
    - **Resultado esperado:** Una lista ordenada de ventas de `laptop` y `tablet` con las mayores cantidades vendidas al inicio.


2. **Filtrar ventas que superen un valor de ingreso específico y ordenar por ingreso**

    Filtra las ventas que generaron ingresos superiores a `$400` y ordénalas de mayor a menor según el ingreso total, calculado como `cantidad * precio_unitario`.

    - **Instrucciones:**
        - Carga los datos desde el archivo `ventas.csv`.
        - Calcula una nueva columna llamada `ingreso` como el producto de `cantidad` y `precio_unitario`.
        - Filtra las ventas donde `ingreso` es mayor a `$400`.
        - Ordena el resultado por la columna `ingreso` en orden descendente.
    - **Pista:** Puedes calcular la columna `ingreso` con el siguiente comando:
        ```pig
        ventas_con_ingreso = FOREACH ventas GENERATE fecha, id_cliente, producto, cantidad, precio_unitario, (cantidad * precio_unitario) AS ingreso;
        ```
    - **Resultado esperado:** Una lista ordenada de ventas con `ingreso > $400`, desde los ingresos más altos hasta los más bajos.

3. **Filtrar por fecha específica y ordenar por precio unitario**

    Filtra las ventas realizadas en una fecha específica, por ejemplo, `2024-01-03`, y ordénalas de menor a mayor según el `precio_unitario`.

    - **Instrucciones:**
        - Carga los datos desde el archivo `ventas.csv`.
        - Filtra solo las ventas realizadas en la fecha `2024-01-03`.
        - Ordena el resultado por `precio_unitario` en orden ascendente.
    - **Resultado esperado:** Una lista de ventas realizadas el `2024-01-03`, ordenada desde el precio unitario más bajo al más alto.

Para cada ejercicio, proporciona el código de Pig que hayas utilizado y una captura de pantalla o salida de los resultados obtenidos. Asegúrate de que el código esté documentado y se entienda claramente.
