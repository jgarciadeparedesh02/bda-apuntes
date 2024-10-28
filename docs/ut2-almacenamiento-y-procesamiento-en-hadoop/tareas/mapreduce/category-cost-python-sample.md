### Práctica de Procesamiento de Datos con MapReduce en Python

#### Objetivo de la Práctica
En esta práctica, los alumnos aprenderán a utilizar un proyecto básico de MapReduce en Python, ejecutar scripts de shell, y entender cómo funcionan los archivos `mapper.py` y `reducer.py` para realizar un procesamiento de datos sencillo. Al finalizar, los estudiantes serán capaces de analizar datos utilizando comandos de Linux y comprender el flujo de datos en un sistema MapReduce.

---

### 1. Descargar el Proyecto

- **Acción**: Descarga el proyecto desde el siguiente enlace de Google Drive.
  - Enlace del proyecto: [Proyecto en Google Drive](https://drive.google.com/drive/folders/1DvDw8Z9Nv-pe0mZnN8n1eufhhaOjETZ7?usp=sharing)
- **Objetivo**: Obtener los archivos necesarios para realizar la práctica, que incluyen el código del Mapper y Reducer, un archivo `download_data.sh` y un archivo de datos `purchases.txt` en el que se basará el procesamiento.

---

### 2. Ejecutar el Script para Descargar el Archivo de Prueba

- **Acción**: Desde la terminal, navega a la carpeta donde descargaste el proyecto y ejecuta el siguiente comando:
  ```bash
  bash download_data.sh
  ```
- **Objetivo**: Descargar el archivo `purchases.txt` que contiene datos de prueba de transacciones de compras. Este archivo se encuentra en la carpeta `data/`.

---

### 3. Explicar el Funcionamiento del Archivo `mapper.py`

- **Tarea**: Abre el archivo `mapper.py` y analiza su contenido.
- **Instrucciones**:
  - Lee el código para entender cómo el Mapper procesa cada línea de entrada.
  - Describe el propósito de cada parte del código.
  - Explica cómo el Mapper convierte la línea de entrada en un par `clave-valor`, generalmente extrayendo información como el nombre del producto y su precio.
---

### 4. Explicar el Funcionamiento del Archivo `reducer.py`

- **Tarea**: Abre el archivo `reducer.py` y analiza su contenido.
- **Instrucciones**:
  - Lee el código para comprender cómo el Reducer agrupa y procesa los datos de salida generados por el Mapper.
  - Describe cómo el Reducer suma el total de ventas para cada tipo de producto.
  - Explica el uso de variables y estructuras en el código.
---

### 5. Ejecutar el Mapper con el Archivo de Datos

- **Acción**: Ejecuta el siguiente comando desde la terminal para procesar los datos usando el Mapper:
  ```bash
  cat data/purchases.txt | python2 mapper.py
  ```
- **Objetivo**: Verificar que el Mapper está funcionando correctamente y analizar su salida.
- **Tarea**:
  - Observa la salida en la terminal y anota qué representa.
  - Explica por qué cada línea de salida del Mapper contiene una clave (tipo de producto) y un valor (costo).
---

### 6. Ejecutar Mapper y Reducer Juntos y Explicar la Salida

- **Acción**: Ejecuta el siguiente comando para procesar los datos con el Mapper y el Reducer combinados:
  ```bash
  cat data/purchases.txt | python2 mapper.py | python2 reducer.py
  ```
- **Objetivo**: Procesar los datos completamente y obtener el total de ventas por cada tipo de producto.
- **Tarea**:
  - Observa la salida en la terminal, que debe mostrar el total de ventas para cada categoría de producto.
  - Explica cómo el Reducer acumula las ventas y por qué cada línea de salida representa un total de ventas por categoría de producto.
---

### Resultados Esperados

- **Comprensión de los Conceptos**: Los estudiantes deben ser capaces de explicar cómo funciona MapReduce y cómo el Mapper y el Reducer procesan los datos en etapas.
- **Aplicación Práctica**: Ejecutar los comandos para ver cómo el flujo de datos pasa de un Mapper a un Reducer, simulando un sistema distribuido simple de procesamiento de datos.

---

### Preguntas

1. ¿Qué sucede si una línea en `purchases.txt` tiene un formato incorrecto? ¿Cómo lo maneja el Mapper?
2. ¿Por qué es importante verificar el formato de los datos en el Mapper?
3. ¿Qué modificaciones podrías hacer al Reducer para agregar más funcionalidad, como calcular el promedio de ventas por categoría?