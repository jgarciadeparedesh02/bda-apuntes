# **Enunciado de la Tarea: Análisis de Datos con Apache Pig**  

## **Objetivo**  
El objetivo de esta tarea es que el estudiante practique las operaciones de carga, filtrado, agrupación y ordenación de datos utilizando Apache Pig, aplicando dichas técnicas a un dataset real extraído de Kaggle.  

## **Instrucciones**  

1. **Búsqueda de un Dataset en Kaggle**  
    - Busca un dataset en [Kaggle](https://www.kaggle.com) relacionado con un tema de interés personal (por ejemplo, películas, deportes, tecnología, economía, etc.).  
    - Asegúrate de que el dataset:
        - Contenga al menos **5 columnas** relevantes para el análisis.
        - Posea un tamaño manejable (menos de 100 MB).  
    - Descarga el archivo del dataset en formato CSV.  

2. **Consultas en Apache Pig**  
    Realiza las siguientes operaciones sobre el dataset:  

    a. **Carga del Dataset**  

    - Escribe el script Pig para cargar el archivo CSV, especificando correctamente los tipos de datos y el delimitador del archivo.  

    b. **Filtrados**  

    - Realiza al menos **dos filtros** sobre los datos. Por ejemplo:

        - Filtrar filas que cumplan una condición específica (como valores mayores a un umbral o categorías específicas).  
        - Excluir valores nulos o irrelevantes.  

    c. **Agrupaciones**  

    - Agrupa los datos por una columna de tu elección (por ejemplo, género, categoría, año) y realiza una operación de agregación (como `COUNT`, `AVG` o `MAX`).  

    d. **Ordenaciones**  

    - Ordena los resultados obtenidos por alguna métrica de interés (por ejemplo, puntuaciones, cantidad de elementos, promedios).  

    e. **Exportación de Resultados**  

    - Guarda los resultados de al menos una de las consultas en un archivo CSV usando la instrucción `STORE`.  