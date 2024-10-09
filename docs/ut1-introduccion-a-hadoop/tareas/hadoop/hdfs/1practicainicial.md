# **Práctica: Gestión de archivos en HDFS en un escenario real**

## **Contexto del Caso**
Imagina que eres parte del equipo de análisis de datos de una empresa de telecomunicaciones. Tu tarea consiste en gestionar el almacenamiento de grandes volúmenes de registros de llamadas telefónicas. Estos registros se almacenarán en HDFS para un posterior análisis distribuido. A lo largo de esta práctica, simularás la subida, consulta y gestión de archivos en HDFS utilizando los registros de llamadas de distintos meses.

## **Entregable**
- Un **documento PDF** donde se muestren los diferentes pasos a seguir indicados a continuación, incluyendo capturas y algo de explicación.

## **Pasos a Seguir**
### 1. **Preparación de archivos locales**
   - Simula dos archivos de texto que contengan los registros de llamadas:
     - `llamadas_enero.txt`: Este archivo contiene las llamadas realizadas en enero.
     - `llamadas_febrero.txt`: Contiene los registros de las llamadas de febrero.

   **Ejemplo de contenido de cada archivo:**
   ```txt
   ID_Llamada, Fecha, Duración, Número_Destino
   001, 2024-01-05 14:30:00, 5 minutos, +34987654321
   002, 2024-01-06 16:45:00, 10 minutos, +34123456789
   ```

### 2. **Subir archivos a HDFS**
   - Crea un directorio en HDFS donde se almacenarán estos archivos:
     ```bash
     hdfs dfs -mkdir /user/empresa_telecom/registros_llamadas
     ```

   - Sube los archivos locales `llamadas_enero.txt` y `llamadas_febrero.txt` a HDFS usando el comando `copyFromLocal`:
     ```bash
     hdfs dfs -copyFromLocal /ruta/local/llamadas_enero.txt /user/empresa_telecom/registros_llamadas/
     hdfs dfs -copyFromLocal /ruta/local/llamadas_febrero.txt /user/empresa_telecom/registros_llamadas/
     ```

### 3. **Verificación de los archivos subidos**
   - Lista los contenidos del directorio en HDFS para confirmar que los archivos se han subido correctamente:
     ```bash
     hdfs dfs -ls /user/empresa_telecom/registros_llamadas
     ```

   - Muestra el contenido de los archivos para verificar su integridad:
     ```bash
     hdfs dfs -cat /user/empresa_telecom/registros_llamadas/llamadas_enero.txt
     hdfs dfs -cat /user/empresa_telecom/registros_llamadas/llamadas_febrero.txt
     ```

### 4. **Renombrar los archivos para una mejor organización**
   - Supón que la empresa ha decidido que los archivos deben seguir un formato más organizado con el mes en minúsculas. Renombra los archivos:
     ```bash
     hdfs dfs -mv /user/empresa_telecom/registros_llamadas/llamadas_enero.txt /user/empresa_telecom/registros_llamadas/llamadas_enero2024.txt
     hdfs dfs -mv /user/empresa_telecom/registros_llamadas/llamadas_febrero.txt /user/empresa_telecom/registros_llamadas/llamadas_febrero2024.txt
     ```

### 5. **Descargar archivos desde HDFS para análisis local**
   - Descarga los archivos de registros desde HDFS a tu sistema local para analizarlos utilizando una herramienta de análisis de datos:
     ```bash
     hdfs dfs -get /user/empresa_telecom/registros_llamadas/llamadas_enero2024.txt /ruta/local/analisis/
     hdfs dfs -get /user/empresa_telecom/registros_llamadas/llamadas_febrero2024.txt /ruta/local/analisis/
     ```

   - Verifica que los archivos descargados sean los mismos que los originales comparando su contenido.

### 6. **Eliminación de archivos antiguos de HDFS**
   - Dado que los archivos han sido descargados y procesados, la empresa decide eliminar los registros de enero del sistema HDFS para liberar espacio. Utiliza el comando `rm` para eliminar el archivo:
     ```bash
     hdfs dfs -rm /user/empresa_telecom/registros_llamadas/llamadas_enero2024.txt
     ```

   - Verifica que el archivo ha sido eliminado correctamente listando de nuevo los contenidos del directorio:
     ```bash
     hdfs dfs -ls /user/empresa_telecom/registros_llamadas
     ```

   - Si ya no necesitas el directorio donde se almacenaron los registros de llamadas, elimínalo también:
     ```bash
     hdfs dfs -rmdir /user/empresa_telecom/registros_llamadas
     ```