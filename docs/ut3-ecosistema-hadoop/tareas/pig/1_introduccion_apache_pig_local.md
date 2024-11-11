# **Práctica: Introducción a Apache Pig en Modo Local**

## Objetivo
Crear un script de Pig que procese un conjunto de datos sencillo y realice operaciones básicas de filtrado y ordenación, ejecutándose línea por línea en modo local.

## Descripción
En esta práctica, el estudiante desarrollará un script en Apache Pig para analizar un archivo de datos de muestra. El objetivo es comprender la estructura de un script en Pig y familiarizarse con funciones básicas como `LOAD`, `FILTER`, `ORDER`, y `STORE`, ejecutándolo en modo local (`pig -x local`).

## Requisitos previos
- Conocimientos básicos de Hadoop.
- Apache Pig instalado en el entorno local.
- Archivo de datos de ejemplo en formato CSV cargado en el sistema de archivos local.

---

## Instrucciones

### 1. Archivo de datos
Crea un archivo llamado `usuarios.csv` con el siguiente contenido, que contiene datos sobre usuarios de una red social (sin la columna "genero" y sin tildes).

```plaintext
nombre,edad,localidad,publicaciones
Juan,25,Madrid,8
Maria,30,Valencia,15
Jose,22,Barcelona,5
Ana,28,Sevilla,12
Pedro,33,Malaga,9
Luisa,29,Zaragoza,4
```

Guarda el archivo en el sistema de archivos local, en la misma carpeta desde la cual ejecutarás Pig.

---

### 2. Objetivos del script de Pig
El script de Pig debe realizar las siguientes operaciones en el archivo `usuarios.csv`:

- **Cargar los datos**: Utiliza la instrucción `LOAD` para cargar el archivo `usuarios.csv` y define los tipos de datos correspondientes.
- **Filtrar los datos**: Filtra los registros de usuarios que tengan más de 10 publicaciones.
- **Ordenar por número de publicaciones**: Ordena los usuarios en función de la cantidad de publicaciones en orden descendente.
- **Guardar los resultados**: Guarda los resultados filtrados y ordenados en el sistema de archivos local.

---

### 3. Ejecución línea por línea en modo local

Para ejecutar cada línea del script en modo local, abre la terminal y ejecuta `pig -x local`. Asegúrate de que estás en el directorio donde se encuentra `usuarios.csv` y ejecuta cada línea del script una a una en el shell de Pig.

#### Cargar el archivo
```pig
-- Cargar el archivo 'usuarios.csv' desde el sistema de archivos local, usando comas como delimitador.
-- Definir los campos con sus respectivos tipos de datos: 'nombre' como cadena de caracteres (chararray),
-- 'edad' como entero (int), 'localidad' como cadena de caracteres y 'publicaciones' como entero.
usuarios = LOAD 'usuarios.csv' USING PigStorage(',') AS (nombre:chararray, edad:int, localidad:chararray, publicaciones:int);

-- Verificar que los datos se hayan cargado correctamente
DUMP usuarios;
```

#### Filtrar usuarios con más de 10 publicaciones
```pig
-- Filtrar los registros de la relacion 'usuarios' para obtener solo aquellos que tienen
-- mas de 10 publicaciones. Esto crea una nueva relacion llamada 'usuarios_activos'.
usuarios_activos = FILTER usuarios BY publicaciones > 10;

-- Verificar que el filtro ha funcionado
DUMP usuarios_activos;
```

#### Ordenar por número de publicaciones
```pig
-- Ordenar la relacion 'usuarios_activos' en funcion del numero de publicaciones en orden descendente.
usuarios_ordenados = ORDER usuarios_activos BY publicaciones DESC;

-- Verificar que los datos estan ordenados
DUMP usuarios_ordenados;
```

#### Guardar los resultados
```pig
-- Almacenar los resultados de 'usuarios_activos' en el sistema de archivos local en un directorio
-- llamado 'salida/usuarios_activos', usando comas como delimitador.
STORE usuarios_activos INTO 'salida/usuarios_activos' USING PigStorage(',');

-- Almacenar los resultados de 'usuarios_ordenados' en el sistema de archivos local en un directorio
-- llamado 'salida/usuarios_ordenados', usando comas como delimitador.
STORE usuarios_ordenados INTO 'salida/usuarios_ordenados' USING PigStorage(',');
```

---

### 4. Verificar los resultados en el sistema de archivos local

Para confirmar que los datos se han almacenado correctamente, revisa los archivos de salida en el sistema de archivos local:

```bash
ls salida/usuarios_activos
cat salida/usuarios_activos/part-m-00000
```

```bash
ls salida/usuarios_ordenados
cat salida/usuarios_ordenados/part-m-00000
```

---

## Script de Pig Completo

```pig
usuarios = LOAD 'usuarios.csv' USING PigStorage(',') AS (nombre:chararray, edad:int, localidad:chararray, publicaciones:int);
DUMP usuarios;

usuarios_activos = FILTER usuarios BY publicaciones > 10;
DUMP usuarios_activos;

usuarios_ordenados = ORDER usuarios_activos BY publicaciones DESC;
DUMP usuarios_ordenados;

STORE usuarios_activos INTO 'salida/usuarios_activos' USING PigStorage(',');
STORE usuarios_ordenados INTO 'salida/usuarios_ordenados' USING PigStorage(',');
```

---

## Posibles errores y soluciones

### 1. Error: `output directory already exists`
   - **Descripción**: Este error ocurre cuando intentas almacenar resultados en un directorio que ya existe.
   - **Solución**: Elimina el directorio de salida existente antes de volver a ejecutar el script.
     ```bash
     rm -r salida/usuarios_activos
     rm -r salida/usuarios_ordenados
     ```

### 2. Error: `Cannot cast from chararray to int`
   - **Descripción**: Puede ocurrir si hay valores no enteros en las columnas `edad` o `publicaciones`.
   - **Solución**: Verifica que los datos en estas columnas son numéricos y están correctamente formateados en el archivo CSV.

### 3. Error: `File not found: usuarios.csv`
   - **Descripción**: Ocurre cuando Pig no encuentra el archivo especificado en la ruta indicada.
   - **Solución**: Confirma que `usuarios.csv` está en el directorio desde el cual estás ejecutando el script o proporciona la ruta completa.
