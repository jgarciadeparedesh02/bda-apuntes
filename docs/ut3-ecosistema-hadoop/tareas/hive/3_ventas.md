# **Tarea: Análisis Avanzado de Datos de Ventas con Hive**

## **Escenario**
Una empresa multinacional desea analizar los datos de ventas almacenados en un sistema de almacenamiento distribuido (HDFS). Los datos contienen información sobre ventas, clientes y productos. Necesitamos realizar consultas avanzadas para extraer insights clave que ayuden a optimizar estrategias comerciales y operativas.

---

## **Objetivos**
1. **Crear tablas particionadas y clusterizadas (bucketizadas).**
2. **Cargar y manipular datos desde tablas externas.**
3. **Realizar consultas avanzadas usando funciones de Hive.**
4. **Generar informes agregados de ventas por región y producto.**
5. **Documentar cada paso mediante capturas de pantalla para su evaluación.**

---

## **Pasos**

### **1. Crear una Tabla Externa**
Crea una tabla externa para cargar los datos iniciales desde HDFS. La ruta estará ubicada en el directorio `/user/hive/`.

```sql
CREATE EXTERNAL TABLE ventas_raw (
    venta_id INT,
    cliente_id INT,
    producto_id INT,
    cantidad INT,
    precio FLOAT,
    fecha STRING,
    region STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/data/ventas_raw/';
```

**Captura requerida:**

- Muestra el comando ejecutado y el resultado de la creación de la tabla (`Table created successfully`).
- Explica cómo esta tabla sirve como punto de partida para las siguientes operaciones.

---

### **2. Crear una Tabla Particionada**
Crea una tabla particionada por región y clusterizada (bucketizada) por cliente. La ruta de almacenamiento será gestionada automáticamente por Hive en HDFS, bajo el directorio por defecto `/user/hive/warehouse/`.

```sql
CREATE TABLE ventas_particionadas (
    venta_id INT,
    cliente_id INT,
    producto_id INT,
    cantidad INT,
    precio FLOAT,
    fecha STRING
)
PARTITIONED BY (region STRING)
CLUSTERED BY (cliente_id) INTO 8 BUCKETS
STORED AS ORC;
```

**Captura requerida:**

- Muestra el comando ejecutado y el resultado de la creación de la tabla particionada (`Table created successfully`).
- Explica cómo el particionamiento y la clusterización optimizan las consultas en esta tabla.

---

### **3. Insertar Datos con Particionamiento**
Carga los datos de la tabla sin procesar (`ventas_raw`) a la tabla particionada (`ventas_particionadas`).

```sql
SET hive.exec.dynamic.partition=true;
SET hive.exec.dynamic.partition.mode=nonstrict;

INSERT OVERWRITE TABLE ventas_particionadas PARTITION (region)
SELECT
    venta_id,
    cliente_id,
    producto_id,
    cantidad,
    precio,
    fecha,
    region
FROM ventas_raw;
```

**Captura requerida:**

- Muestra el comando ejecutado y el resultado del proceso de inserción.
- Explica cómo la partición se refleja en la estructura del directorio en HDFS.

---

### **4. Consultas Avanzadas**
Realiza las siguientes consultas para extraer insights clave:

#### **a) Calcular el Ingreso Total por Región y Producto**
```sql
SELECT
    region,
    producto_id,
    SUM(cantidad * precio) AS ingreso_total
FROM ventas_particionadas
GROUP BY region, producto_id
ORDER BY ingreso_total DESC;
```

#### **b) Identificar los Clientes con Mayor Gasto**
```sql
SELECT
    cliente_id,
    SUM(cantidad * precio) AS gasto_total
FROM ventas_particionadas
GROUP BY cliente_id
ORDER BY gasto_total DESC
LIMIT 10;
```

#### **c) Uso de Funciones de Ventana para el Ranking**
```sql
SELECT
    cliente_id,
    region,
    RANK() OVER (PARTITION BY region ORDER BY SUM(cantidad * precio) DESC) AS ranking
FROM ventas_particionadas
GROUP BY cliente_id, region;
```

#### **d) Consultas para que resuelvan los estudiantes**

1. **Ingreso Total por Mes:**
   Calcula el ingreso total generado en cada mes, ordenado de mayor a menor ingreso.

    **Pista:**

    - Usa la función `month(fecha)` para extraer el número del mes de la columna `fecha`.
    - Agrupa los resultados por mes y utiliza la función `SUM()` para calcular el ingreso total.


2. **Productos Más Vendidos:**
   Identifica los 5 productos más vendidos (por cantidad total) en cada región.

    **Pista:**

    - Agrupa los datos por `producto_id` y `region` para sumar las cantidades vendidas con `SUM(cantidad)`.
    - Usa la función `RANK()` o `ROW_NUMBER()` en una subconsulta para seleccionar los 5 primeros productos por región.

3. **Desempeño Regional:**
   Encuentra la región con el ingreso promedio más alto por transacción.

    **Pista:**

    - Calcula el ingreso promedio por transacción dividiendo `SUM(cantidad * precio)` entre `COUNT(venta_id)` para cada región.
    - Ordena los resultados en orden descendente para identificar la región con el ingreso más alto.

4. **Clientes Frecuentes:**
   Determina los clientes que han realizado más de 10 compras en un año, mostrando la cantidad de compras por cliente.

    **Pista:**

    - Usa la función `year(fecha)` para agrupar las ventas por año.
    - Agrupa por `cliente_id` y el año, y utiliza `COUNT(venta_id)` para contar las compras.
    - Filtra los resultados para incluir solo aquellos con más de 10 compras.

5. **Análisis Temporal:**
   Calcula el ingreso promedio por producto para cada día de la semana, agrupando las ventas por día.

    **Pista:**

    - Usa la función `dayofweek(fecha)` para extraer el día de la semana (1 para domingo, 2 para lunes, etc.).
    - Agrupa los resultados por `dayofweek(fecha)` y `producto_id`, y utiliza `AVG(cantidad * precio)` para calcular el ingreso promedio.

**Captura requerida (para todas las consultas):**

- Muestra la ejecución del código SQL y una vista parcial de los resultados.
- Explica qué aspectos del análisis aportan valor al negocio.

---

### **Datos de Ejemplo**
Usa los siguientes comandos `INSERT INTO` para generar datos de prueba en la tabla `ventas_raw`.

```sql
INSERT INTO ventas_raw VALUES 
(1, 101, 201, 3, 150.00, '2024-01-15', 'Norte'),
(2, 102, 202, 1, 250.00, '2024-01-16', 'Sur'),
(3, 103, 201, 2, 100.00, '2024-01-17', 'Norte'),
(4, 104, 203, 5, 500.00, '2024-01-18', 'Este'),
(5, 105, 204, 1, 300.00, '2024-01-19', 'Oeste'),
(6, 106, 202, 3, 750.00, '2024-01-20', 'Norte'),
(7, 107, 205, 4, 200.00, '2024-01-21', 'Sur'),
(8, 108, 201, 2, 150.00, '2024-01-22', 'Este');
```

**Captura requerida:**

- Muestra el comando de inserción y los datos correctamente cargados en la tabla `ventas_raw`.

---

## **Explicación: Particionamiento y Clusterización**

### **Particionamiento**

- **¿Qué es?**  
  Divide físicamente los datos en diferentes directorios basados en el valor de una o más columnas (por ejemplo, `region` en este caso).

- **¿Para qué sirve?**  
  Optimiza el acceso a los datos al permitir que las consultas solo lean las particiones relevantes, reduciendo el tiempo de ejecución y el costo de lectura.

### **Clusterización (Bucketization)**

- **¿Qué es?**  
  Agrupa los datos dentro de una partición utilizando una columna clave (por ejemplo, `cliente_id`) en un número fijo de buckets.
  
- **¿Para qué sirve?**  
  - Mejora la eficiencia de las uniones (JOINs) y agrupaciones (GROUP BY).
  - Facilita el trabajo con datos más equilibrados y distribuidos.

---

## **Resultados Esperados**
1. Una tabla particionada y clusterizada que facilite consultas más eficientes.
2. Consultas avanzadas que respondan preguntas clave del negocio.
3. Informes detallados sobre las ventas agrupados por región y producto.
4. Capturas de cada paso que expliquen el flujo completo del análisis.