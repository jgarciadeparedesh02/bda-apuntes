# Índice de prácticas y tareas

Este índice incluye todas las prácticas guiadas y tareas correspondientes al curso. Asegúrate de seguir las instrucciones cuidadosamente para cada práctica y tarea, y consulta los materiales de apoyo cuando sea necesario.

## Prácticas guiadas

Las prácticas guiadas están diseñadas para que sigas un conjunto de instrucciones paso a paso y te familiarices con el entorno y las herramientas utilizadas en Big Data. Cada práctica cubre un aspecto clave del entorno de Hadoop y su ecosistema.

- [**Introducción a Apache Pig en Modo Local**](./pig/1_introduccion_apache_pig_local.md)  
    - **Descripción:** En esta práctica aprenderás a utilizar Apache Pig en modo local para procesar un archivo CSV de ejemplo. Ejecutarás un conjunto de instrucciones línea por línea para cargar, filtrar, ordenar y guardar datos en el sistema de archivos local.  
    - **Objetivos:**
        - Cargar un archivo CSV en Pig.
        - Filtrar registros de usuarios según un criterio de publicaciones.
        - Ordenar los usuarios en función del número de publicaciones.
        - Guardar los resultados filtrados y ordenados en el sistema de archivos local.  
    - **Posibles errores:**
        - **Directorio de salida existente**: si el directorio de salida ya existe, debes eliminarlo antes de ejecutar el script.
        - **Errores de tipo de datos**: asegura que los datos numéricos estén en el formato correcto.
        - **Archivo no encontrado**: verifica que el archivo `usuarios.csv` esté en la ruta correcta al ejecutar el script.

## Tareas

Las tareas son actividades prácticas donde aplicarás tus conocimientos y resolverás problemas utilizando Apache Pig sobre datos simulados. Sigue las instrucciones y asegúrate de entregar el código y resultados correctos.

- [**Tarea Básica de Pig para Ventas**](./pig/2_ventas.md)  
    - **Descripción:** Trabajarás con un archivo CSV de datos de ventas, usando Apache Pig para realizar consultas de filtrado y ordenación.  
    - **Objetivos:**
        - Cargar y explorar el archivo `ventas.csv`.
        - Filtrar y ordenar los datos de acuerdo a los criterios de cada ejercicio.
        - Practicar la manipulación de datos en Pig mediante operadores de filtrado y ordenación.  
    - **Posibles errores:**
        - **Formato de fechas incorrecto**: asegúrate de que las fechas en el archivo coincidan con el formato esperado.
        - **Errores en el cálculo de ingreso**: verifica que `(cantidad * precio_unitario)` sea correcto.
        - **Directorio de salida existente**: elimina el directorio de salida si ya existe.

- [**Tarea de Pig para Películas**](./pig/3_peliculas.md)  
    - **Descripción:** Usarás un archivo CSV de películas para realizar consultas de análisis utilizando Apache Pig.  
    - **Objetivos:**
        - Cargar el archivo `peliculas_streaming.csv`.
        - Filtrar y agrupar datos por atributos como género, puntuación y vistas.
        - Realizar cálculos como promedios y totales por grupos.  
    - **Posibles errores:**
        - **Errores en el formato de datos**: verifica que las columnas del archivo sean consistentes.
        - **Falta de archivo**: asegúrate de que `peliculas_streaming.csv` esté en la ubicación correcta.
        - **Directorio de salida existente**: elimina el directorio de salida antes de guardar resultados.

- [**Tarea de Análisis de Dataset con Pig**](./pig/4_csv_eleccion.md)  
    - **Descripción:** En esta tarea buscarás un dataset real en Kaggle, lo procesarás y ejecutarás consultas en Pig que incluyan filtrados, agrupaciones y ordenaciones.  
    - **Objetivos:**
        - Seleccionar y descargar un dataset relevante desde Kaggle en formato CSV.
        - Cargar el dataset en Pig especificando correctamente los tipos de datos.
        - Realizar al menos dos filtros para reducir el conjunto de datos.
        - Agrupar los datos por una columna y calcular métricas como totales o promedios.
        - Ordenar los datos por un criterio relevante y guardar los resultados procesados.  
    - **Posibles errores:**
        - **Formato de datos incorrecto**: verifica que el delimitador y los tipos de columnas sean correctos.
        - **Falta de archivo**: asegúrate de que el archivo descargado esté accesible.
        - **Errores en los scripts de Pig**: revisa la sintaxis y las funciones aplicadas.  