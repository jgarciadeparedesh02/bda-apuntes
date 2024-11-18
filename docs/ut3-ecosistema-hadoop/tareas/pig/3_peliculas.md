# **Archivo CSV: `peliculas_streaming.csv`**

```csv
id_pelicula,titulo,genero,anio,duracion_min,puntuacion,vistas
1,Inception,Ciencia Ficción,2010,148,8.8,2000000
2,The Dark Knight,Acción,2008,152,9.0,2500000
3,Interstellar,Ciencia Ficción,2014,169,8.6,1800000
4,Parasite,Drama,2019,132,8.6,3000000
5,Avengers: Endgame,Acción,2019,181,8.4,4000000
6,La La Land,Musical,2016,128,8.0,1500000
7,The Matrix,Ciencia Ficción,1999,136,8.7,2200000
8,The Godfather,Drama,1972,175,9.2,3500000
9,Spirited Away,Animación,2001,125,8.6,1200000
10,The Lion King,Animación,1994,88,8.5,1800000
```

### **Consultas con ejemplos y comandos de Pig**

---

#### **Consulta 1: Filtrar por alta puntuación y popularidad**  
- **Consulta original:** Encuentra las películas con una **puntuación mayor a 8.5** y más de **2 millones de vistas**.  
- **Ejemplo similar:**  
En un archivo de canciones de Spotify con columnas `id_cancion`, `titulo`, `artista`, `duracion_seg`, `puntuacion`, `reproducciones`, filtra las canciones con una puntuación mayor a **4.5** y más de **1 millón de reproducciones**.
```pig
canciones = LOAD 'canciones_spotify.csv' USING PigStorage(',') 
            AS (id_cancion:INT, titulo:CHARARRAY, artista:CHARARRAY, duracion_seg:INT, puntuacion:FLOAT, reproducciones:INT);
filtradas = FILTER canciones BY puntuacion > 4.5 AND reproducciones > 1000000;
DUMP filtradas;
```

---

#### **Consulta 2: Duración promedio por género**  
- **Consulta original:** Calcula la **duración promedio** de las películas agrupadas por su **género**.  
- **Ejemplo similar:**  
En un archivo de podcasts con columnas `id_podcast`, `titulo`, `categoria`, `duracion_min`, `puntuacion` y `oyentes`, agrupa por **categoría** y calcula la duración promedio de los episodios.
```pig
podcasts = LOAD 'podcasts.csv' USING PigStorage(',') 
           AS (id_podcast:INT, titulo:CHARARRAY, categoria:CHARARRAY, duracion_min:INT, puntuacion:FLOAT, oyentes:INT);
agrupados = GROUP podcasts BY categoria;
promedio_duracion = FOREACH agrupados GENERATE group AS categoria, AVG(podcasts.duracion_min) AS duracion_promedio;
DUMP promedio_duracion;
```

---

#### **Consulta 3: Top 5 de canciones más reproducidas**  
- **Consulta original:** Lista las 5 películas con mayor cantidad de vistas, ordenadas de forma descendente.  
- **Ejemplo similar:**  
En un archivo de canciones de Spotify, encuentra las 5 canciones con más reproducciones.
```pig
canciones = LOAD 'canciones_spotify.csv' USING PigStorage(',') 
            AS (id_cancion:INT, titulo:CHARARRAY, artista:CHARARRAY, duracion_seg:INT, puntuacion:FLOAT, reproducciones:INT);
ordenadas = ORDER canciones BY reproducciones DESC;
top_5 = LIMIT ordenadas 5;
DUMP top_5;
```

---

#### **Consulta 4: Análisis por año**  
- **Consulta original:** Agrupa las películas por año de estreno y calcula estadísticas.  
- **Ejemplo similar:**  
En un archivo de videojuegos con columnas `id_juego`, `titulo`, `genero`, `anio_lanzamiento`, `ventas` y `calificacion`, agrupa por **año de lanzamiento** y calcula:  
    - El número total de juegos por año.  
    - El promedio de calificación.  
    - El juego más vendido de cada año.
```pig
videojuegos = LOAD 'videojuegos.csv' USING PigStorage(',') 
              AS (id_juego:INT, titulo:CHARARRAY, genero:CHARARRAY, anio_lanzamiento:INT, ventas:INT, calificacion:FLOAT);
agrupados_anio = GROUP videojuegos BY anio_lanzamiento;
estadisticas = FOREACH agrupados_anio GENERATE 
               group AS anio, 
               COUNT(videojuegos) AS total_juegos,
               AVG(videojuegos.calificacion) AS promedio_calificacion,
               MAX(videojuegos.ventas) AS ventas_maximas;
DUMP estadisticas;
```

---

#### **Consulta 5: Comparativa entre géneros**  
- **Consulta original:** Calcula el total de **vistas acumuladas** para cada género y ordénalos de mayor a menor.  
- **Ejemplo similar:**  
En un archivo de aplicaciones móviles con columnas `id_app`, `nombre`, `categoria`, `descargas`, calcula las descargas totales por cada categoría y ordénalas en orden descendente.
```pig
apps = LOAD 'apps.csv' USING PigStorage(',') 
       AS (id_app:INT, nombre:CHARARRAY, categoria:CHARARRAY, descargas:INT);
agrupados_categoria = GROUP apps BY categoria;
descargas_totales = FOREACH agrupados_categoria GENERATE group AS categoria, SUM(apps.descargas) AS total_descargas;
ordenadas = ORDER descargas_totales BY total_descargas DESC;
DUMP ordenadas;
```

---

#### **Consulta 6: Distribución de películas por duración**  
- **Consulta original:** Clasifica las películas según su duración.  
- **Ejemplo similar:**  
En un archivo de videos de YouTube con columnas `id_video`, `titulo`, `duracion_min`, clasifica los videos en:  
    - **Cortos:** Menos de 5 minutos.  
    - **Medios:** Entre 5 y 20 minutos.  
    - **Largos:** Más de 20 minutos.
```pig
videos = LOAD 'videos_youtube.csv' USING PigStorage(',') 
         AS (id_video:INT, titulo:CHARARRAY, duracion_min:INT);
clasificados = FOREACH videos GENERATE 
               id_video, 
               titulo, 
               (CASE 
                 WHEN duracion_min < 5 THEN 'Corto'
                 WHEN duracion_min >= 5 AND duracion_min <= 20 THEN 'Medio'
                 ELSE 'Largo' 
               END) AS categoria_duracion;
agrupados_duracion = GROUP clasificados BY categoria_duracion;
conteo = FOREACH agrupados_duracion GENERATE group AS categoria, COUNT(clasificados) AS total_videos;
DUMP conteo;
```
