### **Práctica: Gestión de archivos en HDFS con datos de MovieLens**

#### **Objetivo:**

En esta práctica, aprenderás a gestionar archivos en **HDFS**. Descargarás un dataset grande, lo descomprimirás, y cargarás uno de sus archivos en **HDFS**. Posteriormente, verificarás el estado de los bloques y la replicación en el sistema de archivos distribuido.

#### **Requisitos previos:**

- Conocimientos básicos de HDFS y comandos de terminal.
- Acceso a un clúster de Hadoop (puede ser local o en la nube como AWS EMR).

#### **Pasos a seguir:**

### **Parte 1: Crear un directorio en HDFS**

1. **Crear un directorio en HDFS**  
   El primer paso es crear un directorio donde se almacenarán los archivos dentro del HDFS. Ejecuta el siguiente comando para crear un directorio llamado `prueba` en HDFS:
   ```bash
   hdfs dfs -mkdir prueba
   ```

### **Parte 2: Descargar el dataset de MovieLens**

2. **Descargar el dataset**  
   Ahora descargarás un archivo de datos públicos de **MovieLens** (un dataset de películas y valoraciones). Usa `wget` para descargar el archivo:

   ```bash
   wget https://files.grouplens.org/datasets/movielens/ml-25m.zip
   ```

3. **Verificar la descarga**  
   Para asegurarte de que el archivo se descargó correctamente, lista los archivos en el directorio actual:
   ```bash
   ls
   ```
   Deberías ver el archivo `ml-25m.zip` en la lista.

### **Parte 3: Descomprimir el archivo**

4. **Descomprimir el archivo zip**  
   Descomprime el archivo descargado usando el comando `unzip`:

   ```bash
   unzip ml-25m.zip
   ```

5. **Verificar los archivos descomprimidos**  
   Lista los archivos descomprimidos para asegurarte de que todo está correcto:
   ```bash
   ls ml-25m/
   ```
   Deberías ver varios archivos CSV, incluyendo `ratings.csv`, `movies.csv`, entre otros.

### **Parte 4: Subir un archivo a HDFS**

6. **Subir el archivo `ratings.csv` a HDFS**  
   Ahora, sube uno de los archivos CSV (en este caso, `ratings.csv`) al directorio `prueba` en HDFS:
   ```bash
   hdfs dfs -put ml-25m/ratings.csv prueba
   ```

### **Parte 5: Verificar la integridad del archivo en HDFS**

7. **Verificar el archivo con `fsck`**  
   Utiliza el comando `hdfs fsck` para verificar la integridad del archivo `ratings.csv` en HDFS, mostrando los bloques en los que está dividido:

   ```bash
   hdfs fsck prueba -files -blocks
   ```

   Este comando te proporcionará detalles sobre:

   - El tamaño del archivo.
   - El número de bloques en que se ha dividido el archivo.
   - El estado de replicación de cada bloque.

### **Parte 6: Análisis de la salida**

8. **Interpretar la salida**  
   La salida del comando `fsck` mostrará información sobre los bloques y la replicación del archivo `ratings.csv`. Presta atención a los siguientes puntos:
   - Tamaño total del archivo.
   - Cantidad de bloques en los que se divide.
   - El número de réplicas para cada bloque (en este caso, debería ser 1, ya que el factor de replicación predeterminado es 1).

### **Parte 7: Limpieza (Opcional)**

9. **Eliminar los archivos de HDFS (opcional)**  
   Si deseas limpiar el sistema de archivos y eliminar el archivo subido, puedes usar el siguiente comando:
   ```bash
   hdfs dfs -rm -r prueba
   ```

---

### **Cuestionario de evaluación:**

1. ¿Qué representa un bloque en HDFS y cómo se distribuye un archivo grande entre ellos?
2. ¿Por qué es importante verificar la replicación y el estado de los bloques en HDFS?
3. ¿Qué comando usaste para subir el archivo a HDFS? ¿Qué hace específicamente?
4. Explica el propósito del comando `fsck` en HDFS.

### **Conclusión:**

Esta práctica te ha permitido descargar, manipular y subir archivos a HDFS, además de verificar la integridad y el estado de los bloques en un clúster de Hadoop. La comprensión de cómo se gestiona un archivo en HDFS es esencial para trabajar eficientemente con grandes volúmenes de datos.
