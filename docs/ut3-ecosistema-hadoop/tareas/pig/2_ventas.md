Aquí tienes la tarea ampliada con los nuevos ejercicios de ampliación:

---

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

---

### Ejercicios de Ampliación

4. **Ventas Totales por Cliente**

    Calcula el total de ventas realizadas por cada cliente, sumando el ingreso total generado por cada uno.

    - **Instrucciones:**
        - Calcula una columna `ingreso` como `cantidad * precio_unitario`.
        - Agrupa las ventas por `id_cliente` y suma el `ingreso` para cada cliente.
        - Ordena los resultados en orden descendente de acuerdo con el ingreso total por cliente.
    - **Resultado esperado:** Una lista de clientes con el total de ingresos que han generado, ordenada de mayor a menor.

5. **Producto Más Vendido por Mes**

    Determina el producto más vendido por mes basado en la cantidad total.

    - **Instrucciones:**
        - Extrae el mes de la columna `fecha` para agrupar los datos mensualmente.
        - Agrupa las ventas por `mes` y `producto`.
        - Calcula la cantidad total vendida de cada producto por mes.
        - Ordena los resultados para mostrar el producto más vendido primero para cada mes.
    - **Resultado esperado:** Una lista de productos agrupados por mes, con el producto más vendido de cada mes en la parte superior.

6. **Promedio de Ingresos por Día de la Semana**

    Calcula el ingreso promedio por cada día de la semana para identificar patrones de ventas.

    - **Instrucciones:**
        - Calcula una columna `ingreso` como `cantidad * precio_unitario`.
        - Extrae el día de la semana de la columna `fecha`.
        - Agrupa las ventas por día de la semana y calcula el promedio de `ingreso`.
    - **Resultado esperado:** Una lista con el ingreso promedio para cada día de la semana.

7. **Top 3 Clientes por Ingreso**

    Identifica los tres clientes que generaron el mayor ingreso total en el periodo registrado en el archivo.

    - **Instrucciones:**
        - Calcula una columna `ingreso` como `cantidad * precio_unitario`.
        - Agrupa las ventas por `id_cliente` y suma el `ingreso` para cada cliente.
        - Ordena los resultados en orden descendente y selecciona los tres primeros clientes.
    - **Resultado esperado:** Una lista con los tres clientes que generaron el mayor ingreso total.

8. **Análisis de Productos No Vendidos**

    Identifica qué productos no se vendieron en un rango de fechas específico, por ejemplo, entre `2024-01-01` y `2024-01-04`.

    - **Instrucciones:**
        - Lista todos los productos disponibles en el archivo usando `DISTINCT`.
        - Filtra las ventas dentro del rango de fechas especificado.
        - Encuentra los productos que no aparecen en las ventas del rango de fechas.
    - **Resultado esperado:** Una lista de productos que no tuvieron ninguna venta en el rango de fechas dado.

---

Para cada ejercicio, proporciona el código de Pig que hayas utilizado y una captura de pantalla o salida de los resultados obtenidos. Asegúrate de que el código esté documentado y se entienda claramente.