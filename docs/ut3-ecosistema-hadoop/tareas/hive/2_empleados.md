# **Práctica: Consultas sobre empleados**

### CSV de Ejemplo
```plaintext
id,nombre,edad,departamento,salario
1,Ana,30,IT,50000
2,Luis,45,Finanzas,60000
3,María,28,IT,55000
4,Pablo,35,RH,45000
5,Clara,50,Finanzas,70000
6,Jorge,40,IT,52000
7,Sofía,25,Ventas,48000
8,Carlos,32,RH,46000
9,Laura,29,IT,54000
10,Marta,41,Ventas,47000
11,Pedro,38,Finanzas,68000
12,Isabel,27,RH,44000
13,Antonio,33,IT,53000
14,Lucía,26,RH,49000
15,Fernando,48,Finanzas,72000
16,Raquel,37,Ventas,56000
17,Esteban,31,IT,51000
18,Patricia,24,RH,45000
19,Rosa,39,Ventas,58000
20,Manuel,44,IT,60000
```

### **Parte 1: Crear tablas y cargar datos en Hive**

#### **1. Iniciar el cliente Hive**
- Abre la interfaz de línea de comandos de Hive.

#### **2. Crear una base de datos**
- Crea una nueva base de datos llamada `empresa` y selecciona esta base de datos para trabajar en ella.

#### **3. Crear una tabla en Hive**
- Crea una tabla externa que haga referencia al archivo CSV cargado en HDFS. Define los campos de la tabla basándote en los datos de ejemplo.
    - **Pista:** Ejemplo de tabla externa guardada en un fichero en HDFS
    ```sql
    CREATE EXTERNAL TABLE productos (
        producto_id INT,
        nombre_producto STRING,
        categoria STRING,
        precio FLOAT,
        cantidad_en_stock INT
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ','
    STORED AS TEXTFILE
    LOCATION '/user/hive_data/productos/';
    ```

#### **4. Validar que los datos se han cargado correctamente**
- Realiza una consulta para verificar que los datos están disponibles en la tabla.

---

### **Parte 2: Consultas básicas**

#### **1. Consultas de selección**
1. Lista todos los empleados.
2. Selecciona solo los nombres y salarios de los empleados.
3. Selecciona empleados que pertenecen al departamento "IT".

#### **2. Filtros**
1. Encuentra empleados mayores de 40 años.
2. Encuentra empleados del departamento "Finanzas" que ganan más de 60000.
3. Encuentra empleados cuyos nombres empiezan con la letra 'M'.

#### **3. Agrupaciones**
1. Calcula el salario promedio por departamento.
2. Encuentra el número total de empleados por departamento.
3. Encuentra el salario máximo y mínimo en cada departamento.

#### **4. Ordenación**
1. Ordena a los empleados por salario en orden descendente.
2. Ordena a los empleados por edad en orden ascendente y por salario en orden descendente.

---

### **Parte 3: Consultas avanzadas**

#### **1. Subconsultas**
1. Encuentra los empleados que ganan más que el salario promedio de su departamento.
2. Encuentra los departamentos con un salario promedio mayor a 55000.

#### **2. Funciones integradas**
1. Calcula la edad promedio de los empleados.
2. Encuentra el total de salarios en toda la empresa.
3. Encuentra el salario más alto y más bajo en toda la empresa.
4. Calcula el porcentaje de empleados en cada departamento respecto al total.

#### **3. Operaciones con fechas**
1. Encuentra empleados contratados en los últimos 5 años.
    - **Pista:** Usa funciones de fechas como `CURRENT_DATE` y operadores para calcular diferencias de años.

#### **4. Uso de CASE**
1. Clasifica a los empleados en categorías como "Junior", "Mid-Level", y "Senior" según su salario.
    - **Pista:** Usa la cláusula `CASE` para establecer rangos de clasificación.

---

### **Parte 4: Exportar los resultados**

1. Exporta los nombres y salarios de los empleados del departamento "IT" a un archivo en HDFS.
    - **Pista:** Usa `INSERT OVERWRITE DIRECTORY` junto con el formato de salida especificado.

2. Exporta una consulta que agrupa datos por departamento, incluyendo el promedio de salario y el número total de empleados.
    - **Pista:** Combina la agrupación (`GROUP BY`) con la exportación usando `INSERT OVERWRITE`.
