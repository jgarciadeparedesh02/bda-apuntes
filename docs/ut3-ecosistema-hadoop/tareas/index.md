# Índice de prácticas y tareas

Este índice incluye todas las prácticas guiadas y tareas correspondientes al curso. Asegúrate de seguir las instrucciones cuidadosamente para cada práctica y tarea, y consulta los materiales de apoyo cuando sea necesario.

---

## **Prácticas guiadas**

Las prácticas guiadas están diseñadas para que sigas un conjunto de instrucciones paso a paso y te familiarices con el entorno y las herramientas utilizadas en Big Data. Cada práctica cubre un aspecto clave del entorno de Hadoop y su ecosistema.

### **1. [Introducción a Apache Pig en Modo Local](./pig/1_introduccion_apache_pig_local.md)**  
- **Descripción:** Aprende a utilizar Apache Pig en modo local para procesar un archivo CSV de ejemplo. Cargarás, filtrarás, ordenarás y guardarás datos en el sistema de archivos local.  
- **Objetivos:**
    - Cargar un archivo CSV en Pig.
    - Filtrar registros de usuarios según un criterio de publicaciones.
    - Ordenar los usuarios en función del número de publicaciones.
    - Guardar los resultados filtrados y ordenados en el sistema de archivos local.

---

### **2. [Introducción a Apache Hive](./hive/1_introduccion_apache_hive.md)**  
- **Descripción:** Aprende a manejar datos con Apache Hive, desde la creación de bases de datos hasta consultas avanzadas. Incluye el uso de particiones y operaciones básicas en HDFS.  
- **Objetivos:**
    - Crear una base de datos y tablas particionadas.
    - Insertar, actualizar y eliminar registros en tablas.
    - Ejecutar consultas para analizar datos particionados.
    - Validar las particiones en HDFS y documentar el proceso.

---

## **Tareas de Pig**

Las tareas de Pig son actividades prácticas donde aplicarás tus conocimientos y resolverás problemas utilizando Apache Pig.

### **1. [Tarea Básica de Pig para Ventas](./pig/2_ventas.md)**  
- **Descripción:** Trabaja con un archivo CSV de datos de ventas y realiza consultas de filtrado y ordenación usando Apache Pig.  
- **Objetivos:**
    - Cargar y explorar el archivo `ventas.csv`.
    - Filtrar y ordenar los datos según criterios específicos.
    - Practicar la manipulación de datos en Pig mediante operadores básicos.

---

### **2. [Tarea de Pig para Películas](./pig/3_peliculas.md)**  
- **Descripción:** Usa un archivo CSV de películas para realizar consultas y análisis en Apache Pig.  
- **Objetivos:**
    - Cargar el archivo `peliculas_streaming.csv`.
    - Filtrar y agrupar datos por atributos como género y puntuación.
    - Calcular métricas como promedios y totales.

---

### **3. [Tarea de Análisis de Dataset con Pig](./pig/4_csv_eleccion.md)**  
- **Descripción:** Elige un dataset real desde Kaggle, procesa los datos y ejecuta consultas en Apache Pig para generar reportes útiles.  
- **Objetivos:**
    - Seleccionar y descargar un dataset en formato CSV.
    - Realizar filtros, agrupaciones y cálculos relevantes.
    - Ordenar los datos según criterios específicos y guardar resultados procesados.

---

## **Tareas de Hive**

Las tareas de Hive son actividades prácticas donde aplicarás tus conocimientos y resolverás problemas utilizando Apache Hive.

### **1. [Tarea de Consulta sobre Empleados con Hive](./hive/2_empleados.md)**
- **Descripción:** Usa Apache Hive para realizar consultas sobre un conjunto de datos de empleados.
- **Objetivos:**
    - Crear una base de datos y tablas en Hive.
    - Ejecutar consultas para obtener información relevante.

---

### **2. [Tarea: Análisis Avanzado de Datos de Ventas con Hive](./hive/3_ventas.md)**  
- **Descripción:** Realiza un análisis avanzado de un conjunto de datos de ventas utilizando Apache Hive. Se trabajará con tablas particionadas y clusterizadas para optimizar las consultas.  
- **Objetivos:**
    - Crear tablas particionadas y clusterizadas.
    - Cargar datos desde una tabla externa en HDFS.
    - Realizar consultas avanzadas que incluyan funciones de fecha y análisis por categorías.
    - Generar reportes detallados sobre el desempeño de las ventas por región, producto y cliente.
    - Documentar el proceso mediante capturas de pantalla de cada paso.

---