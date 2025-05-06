
# **Tarea: Análisis de Datos de Taxis en Nueva York con PySpark**

## **Objetivo**

El objetivo de esta tarea es que te familiarices con el uso de Apache Spark y PySpark para procesar y analizar datos reales. Trabajarás con un conjunto de datos que contiene información de viajes en taxi en Nueva York, realizando distintos análisis y visualizando los resultados por consola.

---

## **Materiales proporcionados**

### **Archivo template (base para tu script)**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, count, avg, max, min, desc, year, month, to_timestamp

# Crear sesión de Spark
spark = SparkSession.builder \
    .appName("TaxiAnalysis") \
    .master("local[*]") \
    .getOrCreate()

# Leer el CSV (asegúrate de que la ruta al archivo sea válida)
df = spark.read.option("header", True).csv("file:///root/nyc_taxi_sample.csv", inferSchema=True)

# Exportar resultados a CSV
output_df = df.select("passenger_count", "trip_distance", "total_amount")
output_df.write.mode("overwrite").csv("file:///root/nyc_output.csv", header=True)
print("Datos exportados a 'nyc_output.csv'.")
```

### **Explicación del script**

El script proporcionado es un punto de partida para realizar análisis de datos utilizando PySpark. A continuación, se explica cada sección del código:

#### **1. Creación de la sesión de Spark**

```python
spark = SparkSession.builder \
     .appName("TaxiAnalysis") \
     .master("local[*]") \
     .getOrCreate()
```

Aquí se crea una sesión de Spark, que es el punto de entrada para trabajar con PySpark. El nombre de la aplicación se define como "TaxiAnalysis" y se utiliza el modo local con todos los núcleos disponibles (`local[*]`).

#### **2. Lectura del archivo CSV**

```python
df = spark.read.option("header", True).csv("file:///root/nyc_taxi_sample.csv", inferSchema=True)
```

Se lee un archivo CSV que contiene los datos de los viajes en taxi. La opción `header=True` indica que la primera fila del archivo contiene los nombres de las columnas, y `inferSchema=True` permite que PySpark detecte automáticamente los tipos de datos.

#### **3. Exportación de datos**

```python
output_df = df.select("passenger_count", "trip_distance", "total_amount")
output_df.write.mode("overwrite").csv("file:///root/nyc_output.csv", header=True)
print("Datos exportados a 'nyc_output.csv'.")
```

Se seleccionan las columnas `passenger_count`, `trip_distance` y `total_amount` del DataFrame original y se exportan a un nuevo archivo CSV llamado `nyc_output.csv`. El modo `overwrite` asegura que si el archivo ya existe, será sobrescrito.

Este script es solo un punto de partida y debe ser modificado para incluir los análisis y transformaciones requeridos en las instrucciones de la tarea.

### **Archivo CSV (`nyc_taxi_sample.csv`)**

```
tpep_pickup_datetime,pickup_datetime,dropoff_datetime,passenger_count,trip_distance,fare_amount,total_amount,PULocationID,tip_amount
2024-01-01 08:15:27,2024-01-01 08:15:27,2024-01-01 08:45:12,1,5.3,18.50,20.35,132,1.85
2024-01-01 09:12:45,2024-01-01 09:12:45,2024-01-01 09:34:18,2,7.8,24.00,26.40,145,2.40
2024-01-01 10:05:30,2024-01-01 10:05:30,2024-01-01 10:22:44,1,3.2,12.75,14.03,107,1.28
2024-01-01 11:40:55,2024-01-01 11:40:55,2024-01-01 12:01:10,3,4.5,15.00,16.50,236,1.50
2024-01-01 13:22:18,2024-01-01 13:22:18,2024-01-01 13:45:00,1,6.1,20.00,22.00,148,2.00
2024-01-01 14:07:01,2024-01-01 14:07:01,2024-01-01 14:29:35,2,5.7,17.80,19.58,234,1.78
2024-01-01 15:10:12,2024-01-01 15:10:12,2024-01-01 15:35:45,1,4.2,14.50,15.95,132,1.45
2024-01-01 16:20:30,2024-01-01 16:20:30,2024-01-01 16:50:10,2,8.3,25.00,27.50,145,2.50
2024-01-01 17:05:15,2024-01-01 17:05:15,2024-01-01 17:30:00,1,3.9,13.20,14.52,107,1.32
2024-01-01 18:12:45,2024-01-01 18:12:45,2024-01-01 18:40:30,3,7.5,22.50,24.75,236,2.25
```

### **Explicación de las columnas del CSV**

El archivo `nyc_taxi_sample.csv` contiene las siguientes columnas:

1. **tpep_pickup_datetime**: Fecha y hora en que comenzó el viaje en taxi.
2. **pickup_datetime**: Fecha y hora de recogida (similar a `tpep_pickup_datetime`).
3. **dropoff_datetime**: Fecha y hora en que terminó el viaje en taxi.
4. **passenger_count**: Número de pasajeros en el viaje.
5. **trip_distance**: Distancia recorrida durante el viaje (en millas).
6. **fare_amount**: Monto de la tarifa base del viaje (sin incluir propinas ni otros cargos).
7. **total_amount**: Monto total del viaje, incluyendo tarifa base, propinas y otros cargos.
8. **PULocationID**: Identificador de la ubicación de recogida (Pickup Location ID).
9. **tip_amount**: Monto de la propina otorgada al conductor.

Estas columnas proporcionan información detallada sobre cada viaje en taxi, lo que permite realizar análisis como el costo promedio por distancia, la cantidad de pasajeros por viaje, y más.

---

## **Instrucciones de la Tarea**

### **Parte 1: Exploración de Datos**

* Muestra las primeras filas del DataFrame.
* Muestra el esquema del DataFrame (`printSchema()`).
* Imprime el número total de registros.
* Muestra la lista de columnas.

### **Parte 2: Análisis de los Datos**

Realiza los siguientes análisis utilizando PySpark:

1. Muestra las **10 tarifas (`total_amount`) más altas**.
2. Convierte la columna `tpep_pickup_datetime` en tipo `timestamp`.
3. Filtra los viajes que **costaron más de \$100**.
4. Calcula la **tarifa promedio por número de pasajeros** (`passenger_count`).
5. Muestra el **número de viajes por mes**.
6. Muestra el **top 5 de ubicaciones de recogida** (`PULocationID`) con más viajes.
7. Muestra los **viajes que no tienen propina** (`tip_amount == 0`).

### **Parte 3: Exportación**

* Ya está incluida en el template una exportación de datos a un nuevo CSV. **No necesitas entregar este archivo**.

---

## **Entregables**

Debes entregar:

1. El **script `.py`** con todo el análisis resuelto y bien comentado.
2. Una **captura de pantalla** (o varias si es necesario) mostrando la salida por consola de tu script.

