# Índice de prácticas y tareas

Este índice incluye todas las prácticas guiadas y tareas correspondientes al curso. Asegúrate de seguir las instrucciones cuidadosamente para cada práctica y tarea, y consulta los materiales de apoyo cuando sea necesario.

## Prácticas guiadas

Las prácticas guiadas están diseñadas para que sigas un conjunto de instrucciones paso a paso y te familiarices con el entorno y las herramientas utilizadas en Big Data. Cada práctica cubre un aspecto clave del entorno de Hadoop y su ecosistema.

- [**WORDCOUNT en Hadoop con MapReduce**](./mapreduce/wordcount-sample.md)
    - **Descripción:** En esta práctica aprenderás a ejecutar el ejemplo clásico de **WordCount** utilizando Hadoop MapReduce. El objetivo es procesar un archivo de texto para contar la cantidad de veces que aparece cada palabra.
    - **Objetivos:**
        - Subir un archivo de texto a HDFS.
        - Ejecutar un trabajo de MapReduce para contar palabras.
        - Verificar la salida del proceso en HDFS.

- [**Análisis de costos por categoría con MapReduce en Python**](./mapreduce/category-cost-python-sample.md)
    - **Descripción:** En esta práctica aprenderás a implementar y ejecutar un ejemplo de MapReduce utilizando Python para analizar datos de compras. El objetivo es procesar un archivo de transacciones, agrupar las ventas por tipo de producto y calcular el total de ventas para cada categoría.
    - **Objetivos:**
        - Descargar el proyecto de ejemplo desde Google Drive.
        - Ejecutar un script de shell para descargar los datos de prueba.
        - Explicar el funcionamiento de los archivos `mapper.py` y `reducer.py`.
        - Ejecutar el `mapper.py` para observar la salida intermedia.
        - Ejecutar `mapper.py` y `reducer.py` juntos para obtener el total de ventas por categoría.

- [**Análisis de Visualización en Netflix con MapReduce en Python**](./mapreduce/netflix/enunciado/)
    - **Descripción:** En esta tarea, desarrollarás un programa en Python utilizando el paradigma de MapReduce para analizar los datos de visualización en Netflix. El objetivo es identificar los días de la semana y las franjas horarias con mayor número de visualizaciones.
    - **Objetivos:**
        - Implementar una función `map` que procese las columnas `day_of_week` y `time_of_day`.
        - Implementar una función `reduce` que acumule el número total de visualizaciones para cada combinación de día y franja horaria.
        - Ejecutar el programa para obtener un resumen del patrón de visualización.
        - Interpretar los resultados y explicar qué días y horarios tienen más visualizaciones.
