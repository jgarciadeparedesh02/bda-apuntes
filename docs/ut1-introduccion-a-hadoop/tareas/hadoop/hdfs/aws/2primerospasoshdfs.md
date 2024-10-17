# Práctica real con comandos de HDFS en EC2

## 1. Crear un directorio en HDFS

Crea un directorio llamado `/practica_hdfs` dentro del sistema de archivos distribuido (HDFS).

```bash
hdfs dfs -mkdir /practica_hdfs
```

## 2. Subir un archivo desde el sistema local a HDFS

Primero, crea un archivo de texto de prueba en tu sistema local:

```bash
echo "Este es un archivo de prueba para HDFS" > archivo_prueba.txt
```

Luego, sube el archivo a HDFS dentro del directorio `/practica_hdfs`:

```bash
hdfs dfs -put archivo_prueba.txt /practica_hdfs/
```

## 3. Listar los archivos en un directorio de HDFS

Verifica que el archivo fue subido correctamente listando los contenidos del directorio `/practica_hdfs`:

```bash
hdfs dfs -ls /practica_hdfs
```

## 4. Ver el contenido de un archivo en HDFS

Muestra el contenido del archivo directamente en la terminal:

```bash
hdfs dfs -cat /practica_hdfs/archivo_prueba.txt
```

## 5. Mover o renombrar un archivo en HDFS

Renombra o mueve el archivo dentro del directorio de HDFS:

```bash
hdfs dfs -mv /practica_hdfs/archivo_prueba.txt /practica_hdfs/archivo_renombrado.txt
```

## 6. Descargar un archivo desde HDFS al sistema local

Descarga el archivo desde HDFS a tu sistema de archivos local (EC2):

```bash
hdfs dfs -get /practica_hdfs/archivo_renombrado.txt archivo_descargado.txt
```

## 7. Eliminar un archivo de HDFS

Elimina el archivo de HDFS:

```bash
hdfs dfs -rm /practica_hdfs/archivo_renombrado.txt
```

## 8. Eliminar un directorio en HDFS

Elimina el directorio `/practica_hdfs`:

```bash
hdfs dfs -rm -r /practica_hdfs
```

---

## Opcional: Comandos adicionales para profundizar

### Ver información sobre el espacio disponible en HDFS

Verifica el uso de espacio en HDFS en formato legible:

```bash
hdfs dfs -df -h
```

### Contar archivos, directorios y tamaño total de un directorio en HDFS

Usa este comando para contar el número de archivos, directorios y el tamaño total en un directorio específico de HDFS:

```bash
hdfs dfs -count /practica_hdfs
```

### Comprobar bloques de un archivo en HDFS

Obtén detalles sobre los bloques que forman un archivo:

```bash
hdfs fsck /practica_hdfs/archivo_renombrado.txt -files -blocks
```
