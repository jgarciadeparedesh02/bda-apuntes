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
