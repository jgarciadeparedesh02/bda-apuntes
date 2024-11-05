# **Ejercicio de MapReduce en Python: Análisis de Días y Horarios de Visualización en Netflix**

**Objetivo:**  
El objetivo de este ejercicio es desarrollar un programa en Python que use el paradigma MapReduce para analizar los datos de visualización de contenido en Netflix. Queremos identificar los días de la semana y las franjas horarias en las que los usuarios realizan más visualizaciones. El programa debe procesar los datos de visualización y devolver una tabla con el número de visualizaciones agrupadas por día de la semana y franja horaria.

### Estructura de los Datos
Para este ejercicio, trabajaremos con un archivo de datos CSV que contiene las siguientes columnas relevantes para el análisis:

- **day_of_week**: Día de la semana en el que se realizó la visualización (por ejemplo, "Monday", "Tuesday", etc.).
- **time_of_day**: Franja horaria en la que se realizó la visualización ("Morning", "Afternoon", "Evening", "Night").

Un ejemplo de fila de datos podría verse así:
```
day_of_week,time_of_day,other_columns...
Monday,Evening,...
Tuesday,Morning,...
...
```

### Pasos para Resolver el Ejercicio

1. **Función Map:**  
   La función `map` debe leer cada línea del archivo de datos y extraer las columnas `day_of_week` y `time_of_day`. Por cada entrada, la función emitirá una clave-valor en el formato `(day_of_week, time_of_day) -> 1`, donde `1` representa una visualización.

2. **Función Reduce:**  
   La función `reduce` debe tomar todas las claves `(day_of_week, time_of_day)` emitidas por la fase de `map` y sumar los valores asociados para obtener el total de visualizaciones para cada combinación de día y franja horaria.

3. **Formato de Salida:**  
   El programa debe generar un informe que muestre las combinaciones de `day_of_week` y `time_of_day`, junto con la cantidad total de visualizaciones. El formato de salida puede ser un archivo CSV o una tabla impresa en pantalla con las columnas `day_of_week`, `time_of_day` y `count`.

### Ejemplo de Salida Esperada

```
day_of_week, time_of_day, count
Monday, Evening, 450
Monday, Morning, 300
Tuesday, Afternoon, 350
...
```