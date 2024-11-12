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
    - **Descripción:** En esta tarea trabajarás con un archivo CSV de datos de ventas, usando Apache Pig para realizar consultas de filtrado y ordenación.
    - **Objetivos:**
        - Cargar y explorar el archivo de ventas `ventas.csv`.
        - Filtrar y ordenar los datos de acuerdo a los criterios de cada ejercicio.
        - Practicar la manipulación de datos en Pig mediante el uso de operadores de filtrado y ordenación.
    - **Ejercicios:**
        1. **Filtrar ventas de productos específicos y ordenar por cantidad vendida**
           - Filtra las ventas de los productos `laptop` y `tablet`, y ordénalas de mayor a menor por la cantidad vendida.
        
        2. **Filtrar ventas que superen un valor de ingreso específico y ordenar por ingreso**
           - Filtra las ventas con ingresos superiores a `$400` y ordénalas de mayor a menor según el ingreso total.
        
        3. **Filtrar por fecha específica y ordenar por precio unitario**
           - Filtra las ventas realizadas en la fecha `2024-01-03` y ordénalas de menor a mayor por el `precio_unitario`.
        
    - **Pista:** Para el cálculo de ingresos en el segundo ejercicio, usa:
      ```pig
      ventas_con_ingreso = FOREACH ventas GENERATE fecha, id_cliente, producto, cantidad, precio_unitario, (cantidad * precio_unitario) AS ingreso;
      ```
    - **Posibles errores:**
        - **Formato de fechas incorrecto**: asegúrate de que las fechas en el archivo coincidan con el formato esperado.
        - **Errores en el cálculo de ingreso**: verifica que el cálculo `(cantidad * precio_unitario)` sea correcto y que los tipos de datos sean compatibles.
        - **Directorio de salida existente**: si el directorio de salida ya existe, debes eliminarlo antes de ejecutar el script.

