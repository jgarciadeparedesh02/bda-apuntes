Aquí tienes la práctica actualizada, incluyendo el comando para visualizar todas las partes del archivo de salida juntas:

---

### **Práctica: Ejecución del ejemplo WordCount en Hadoop con MapReduce**

En esta práctica, vas a ejecutar el ejemplo clásico de **WordCount** utilizando **Hadoop MapReduce** para contar el número de veces que aparece cada palabra en un archivo de texto. Seguirás los siguientes pasos para crear un archivo, cargarlo en **HDFS**, y ejecutar un trabajo de MapReduce que contará las palabras.

#### **Objetivo:**
Familiarizarse con los comandos básicos de **HDFS** y **MapReduce** en Hadoop, ejecutar un trabajo de ejemplo y obtener los resultados.

#### **Requisitos:**
- Un clúster de Hadoop corriendo (local o en la nube, como EMR de AWS).
- Acceso a la terminal de la máquina maestra del clúster.

#### **Implementación del ejemplo:**
El código Java que da lugar al ejemplo que se utiliza en esta práctica está disponible en [WordCount](https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html).

### **Pasos a seguir:**

#### 1. **Crear el archivo de texto de entrada**

Primero, crea un archivo de texto en la máquina local que contenga el texto que quieres procesar:

```bash
echo -e "Hadoop is a distributed system\nHadoop is scalable\nHadoop can handle big data" > word_count.txt
```

#### 2. **Verificar el contenido del archivo**

Asegúrate de que el archivo contiene el texto deseado ejecutando:

```bash
cat word_count.txt
```

La salida debería mostrar el siguiente contenido:

```
Hadoop is a distributed system
Hadoop is scalable
Hadoop can handle big data
```

#### 3. **Crear un directorio en HDFS para almacenar el archivo de entrada**

Crea un directorio en HDFS donde almacenarás el archivo de entrada:

```bash
hdfs dfs -mkdir /user/hadoop/input
```

#### 4. **Subir el archivo de entrada a HDFS**

Sube el archivo `word_count.txt` a HDFS para que esté disponible para el procesamiento:

```bash
hdfs dfs -put word_count.txt /user/hadoop/input/
```

#### 5. **Ejecutar el trabajo de MapReduce para WordCount**

Ejecuta el trabajo de **MapReduce** utilizando el ejemplo de **WordCount**. Este comando toma el archivo de entrada desde **HDFS**, lo procesa, y genera un archivo de salida con el conteo de palabras.

```bash
hadoop jar /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar wordcount /user/hadoop/input/word_count.txt /user/hadoop/output
```

#### 6. **Verificar la salida en HDFS**

El trabajo de MapReduce puede generar varios archivos de salida (`part-r-00000`, `part-r-00001`, etc.). Para visualizar todas las partes juntas y concatenarlas en un archivo local, ejecuta el siguiente comando:

```bash
hdfs dfs -cat /user/hadoop/output/part-r-* > combined_output.txt
```

Este comando toma todas las partes del archivo de salida (por ejemplo, `part-r-00000`, `part-r-00001`, etc.) y las guarda en un archivo llamado `combined_output.txt` en el sistema local.

#### 7. **Verificar el archivo de salida combinado**

Una vez concatenado, puedes verificar el contenido del archivo `combined_output.txt`:

```bash
cat combined_output.txt
```

Deberías ver la salida con el conteo de palabras, por ejemplo:

```
Hadoop    3
is        2
a         1
distributed 1
system    1
scalable  1
can       1
handle    1
big       1
data      1
```

#### 8. **Copiar el archivo de salida a la máquina local (opcional)**

Si prefieres obtener las partes del archivo de salida por separado y copiarlas desde **HDFS** a tu sistema local:

```bash
hdfs dfs -get /user/hadoop/output/part-r-00000 .
```

Repite el proceso para todas las partes generadas (por ejemplo, `part-r-00001`, `part-r-00002`, etc.), o concaténalas usando el paso anterior.

---

### **Conclusión:**
En esta práctica has aprendido a:

- Crear un archivo de texto en la máquina local.
- Subir un archivo a **HDFS**.
- Ejecutar un trabajo de **MapReduce** en Hadoop.
- Concatenar los resultados de salida generados en múltiples partes utilizando `hdfs dfs -cat` para visualizar todos los resultados juntos.

Con estos pasos, te has familiarizado con el flujo básico de trabajo de **MapReduce** en Hadoop y la gestión de archivos en **HDFS**.

---

### **Preguntas para los estudiantes:**

Después de realizar la práctica, responde a las siguientes preguntas para evaluar tu comprensión del proceso:

1. **¿Cuántas partes resultaron del proceso de Reduce?**
    - Pista: Revisa cuántos archivos `part-r-0000x` se generaron en el directorio de salida de HDFS.
   
2. **¿Qué comando utilizaste para visualizar todas las partes juntas en un solo archivo?**
    - Describe brevemente el uso del comando `hdfs dfs -cat` y cómo se concatenaron las partes de salida.

3. **¿Cuál es la función principal de la fase "Map" en el proceso de MapReduce?**
    - Explica brevemente qué hace la fase **Map** y cómo genera los pares clave-valor.

4. **¿Cuál es la función principal de la fase "Reduce" en el proceso de MapReduce?**
    - Describe el objetivo de la fase **Reduce** y qué sucede con los pares clave-valor generados por el mapper.

5. **¿Por qué el trabajo de MapReduce genera múltiples archivos de salida (part-r-00000, part-r-00001, etc.)?**
    - Explica por qué los resultados pueden dividirse en varias partes en lugar de generarse en un solo archivo.

6. **¿Qué información proporciona el archivo `_SUCCESS` que aparece en el directorio de salida?**
    - Investiga qué indica la presencia de este archivo después de la ejecución de un trabajo de MapReduce.

7. **¿Qué pasos adicionales serían necesarios si quisieras procesar un archivo mucho más grande en lugar de `word_count.txt`?**
    - Explica si tendrías que hacer algo diferente en términos de configuración de MapReduce o HDFS para procesar un archivo de mayor tamaño.
