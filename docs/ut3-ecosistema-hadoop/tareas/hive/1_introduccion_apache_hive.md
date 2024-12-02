# **Tarea: Manejo de Datos en Apache Hive** 🐝

#### **Objetivo:**  
Practicar la creación y gestión de bases de datos y tablas en Apache Hive, incluyendo el uso de particiones, ejecución de consultas básicas y avanzadas, y verificación de datos en HDFS.

---

#### **Parte 1: Creación de la Base de Datos**
1. Crea una base de datos llamada `tienda_online`:
   ```sql
   CREATE DATABASE tienda_online;
   ```
2. Comprueba que la base de datos se haya creado correctamente:
   ```sql
   SHOW DATABASES;
   ```

---

#### **Parte 2: Creación de Tablas con Particiones**
1. Dentro de la base de datos `tienda_online`, crea una tabla llamada `ventas` con las siguientes columnas:
   - `id INT`
   - `producto STRING`
   - `cantidad INT`
   - Particionada por `fecha STRING`.

   ```sql
   USE tienda_online;

   CREATE TABLE ventas (
     id INT,
     producto STRING,
     cantidad INT
   )
   PARTITIONED BY (fecha STRING)
   STORED AS PARQUET;
   ```

2. Comprueba que la tabla se haya creado correctamente:
   ```sql
   SHOW TABLES;
   DESCRIBE FORMATTED ventas;
   ```

---

#### **Parte 3: Insertar Datos**
1. Inserta los siguientes registros en las particiones correspondientes:
   - `(1, 'Laptop', 10, '2024-11-01')`
   - `(2, 'Mouse', 25, '2024-11-02')`
   - `(3, 'Teclado', 15, '2024-11-03')`

   ```sql
   INSERT INTO TABLE ventas PARTITION (fecha='2024-11-01') VALUES (1, 'Laptop', 10);
   INSERT INTO TABLE ventas PARTITION (fecha='2024-11-02') VALUES (2, 'Mouse', 25);
   INSERT INTO TABLE ventas PARTITION (fecha='2024-11-03') VALUES (3, 'Teclado', 15);
   ```

---

#### **Parte 4: Actualización y Eliminación de Datos**
1. **Actualiza** el registro del producto `Mouse` para cambiar la cantidad a `30`:
   ```sql
   UPDATE ventas
   SET cantidad = 30
   WHERE producto = 'Mouse' AND fecha = '2024-11-02';
   ```

2. **Elimina** el registro del producto `Teclado`:
   ```sql
   DELETE FROM ventas
   WHERE producto = 'Teclado' AND fecha = '2024-11-03';
   ```

---

#### **Parte 5: Ejecución de Consultas**
1. Muestra todas las ventas realizadas en la fecha `2024-11-01`:
   ```sql
   SELECT * FROM ventas WHERE fecha = '2024-11-01';
   ```

2. Muestra el total de productos vendidos agrupados por fecha:
   ```sql
   SELECT fecha, SUM(cantidad) AS total_cantidad
   FROM ventas
   GROUP BY fecha;
   ```

3. Ordena las ventas por cantidad en orden descendente:
   ```sql
   SELECT * FROM ventas
   ORDER BY cantidad DESC;
   ```

---

#### **Parte 6: Validación en HDFS**
1. Lista las particiones de la tabla `ventas` en HDFS:
   ```bash
   hdfs dfs -ls /user/hive/warehouse/tienda_online.db/ventas
   ```

2. Toma capturas de pantalla del contenido del directorio de la base de datos y de las particiones de la tabla `ventas`. Por ejemplo:
   - `/user/hive/warehouse/tienda_online.db/ventas/fecha=2024-11-01/`

---

¡Con estas instrucciones completas, estarás listo para manejar datos en Apache Hive de forma eficiente! 🐝