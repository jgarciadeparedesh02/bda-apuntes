### Enunciado para Ejercicio de MapReduce

En este ejercicio, los estudiantes deberán implementar una serie de operaciones de MapReduce sobre un archivo CSV de tweets, analizando y extrayendo información de interés a partir de grandes volúmenes de datos.

Cada estudiante deberá responder a las siguientes preguntas de análisis, ejecutando tareas de MapReduce para cada una.

---

#### Formato del archivo CSV

El archivo `tweets_data.csv` tiene el siguiente formato de columnas y datos de ejemplo:

```
username;tweet_content;date_written;likes;retweets;replies;location;source
@carlos_fernandez;La ciencia de datos está cambiando el mundo. #CienciaDeDatos;2024-10-18 16:23:16;182;49;90;Barcelona;Twitter para iPhone
@carlos_fernandez;Aprendiendo más sobre Python cada día.;2024-10-17 16:23:16;382;238;24;Málaga;Twitter para iPhone
@carlos_fernandez;Aprendiendo más sobre Python cada día.;2024-10-19 16:23:16;285;91;0;Sevilla;Twitter para iPhone
@maria_garcia;La ciencia de datos está cambiando el mundo. #Python;2024-10-22 16:23:16;76;92;29;Málaga;Twitter Web App
@carlos_fernandez;Explorando nuevos modelos de IA. #IA;2024-10-12 16:23:16;56;54;89;Bilbao;Twitter para iPhone
@maria_garcia;La ciencia de datos está cambiando el mundo. #IA;2024-10-26 16:23:16;36;220;60;Granada;Twitter para iPhone
@lucia_martinez;Los desafíos de programación me mantienen afilado.;2024-10-20 16:23:16;303;155;78;Sevilla;Twitter para Android
@laura_rodriguez;La ciencia de datos está cambiando el mundo.;2024-10-02 16:23:16;387;242;60;Barcelona;Twitter para iPhone
@laura_rodriguez;Los desafíos de programación me mantienen afilado.;2024-10-19 16:23:16;191;231;35;Bilbao;Twitter para iPhone
@laura_rodriguez;¡Acabo de terminar una gran sesión de codificación!;2024-10-25 16:23:16;44;48;20;Granada;Twitter Web App
```

---

#### Tareas de MapReduce

1. **Contar cuántas veces aparece cada hashtag**
   - Determinar la frecuencia de cada hashtag en el conjunto de tweets para identificar cuáles son los temas más populares.

2. **Contar cuántos tweets ha escrito cada usuario**
   - Obtener el número de tweets por cada usuario registrado en el archivo, analizando su nivel de actividad en la plataforma.

3. **Análisis de popularidad de tweets (likes + retweets)**
   - Calcular la popularidad de cada tweet considerando la suma de "likes" y "retweets".

4. **Tweets por ubicación geográfica**
   - Determinar el número de tweets enviados desde cada ubicación para observar las áreas de mayor actividad.

5. **Promedio de interacciones (likes, retweets y replies) por usuario**
   - Calcular el promedio de interacciones (considerando "likes", "retweets" y "replies") que recibe cada usuario en sus tweets.

6. **Tweets diarios**
   - Contabilizar la cantidad de tweets publicados por día, analizando la actividad en diferentes fechas.

---

Cada pregunta representa una tarea de MapReduce. Para cada tarea, los estudiantes deben:
1. Implementar el código MapReduce.
2. Documentar el proceso.
3. Analizar los resultados obtenidos para identificar patrones o insights.

Este ejercicio permitirá a los estudiantes comprender y practicar las técnicas de MapReduce aplicadas a un dataset real de redes sociales.