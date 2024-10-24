# **Comprendiendo HDFS: Una Guía Completa**

## 🚀 ¿Qué es HDFS?

HDFS significa **Hadoop Distributed File System** (Sistema de Archivos Distribuido de Hadoop), y es la columna vertebral de la capacidad de Hadoop para manejar grandes cantidades de datos. Se originó a partir de GFS (Google File System) y está diseñado para almacenar y gestionar grandes volúmenes de datos de manera eficiente, distribuyéndolos a través de varios nodos en un clúster.

HDFS proporciona tolerancia a fallos y acceso de alto rendimiento a grandes conjuntos de datos, lo que lo hace ideal para aplicaciones que manejan procesamiento a gran escala, como minería de datos, aprendizaje automático y análisis.

---

## 🧩 **Arquitectura de HDFS: Nodos y Tipos**

La arquitectura de HDFS gira en torno a dos componentes principales:

1. **NameNode**: El nodo maestro que controla los metadatos de los archivos y la estructura del directorio.
2. **DataNodes**: Estos son los nodos trabajadores responsables de almacenar los datos reales en bloques. Cada bloque tiene un tamaño predeterminado de 128 MB, pero este valor es configurable.

```mermaid
graph TD;
    NameNode -->|Metadatos| DataNode1;
    NameNode -->|Metadatos| DataNode2;
    NameNode -->|Metadatos| DataNode3;
    DataNode1 --> Block1;
    DataNode2 --> Block2;
    DataNode3 --> Block3;
```

### **Tipos Clave de Nodos:**

- **NameNode (Maestro)**: Almacena metadatos de los archivos (como nombres, permisos, ubicación de los bloques).
- **DataNode (Trabajador)**: Almacena bloques de datos y envía señales de estado (heartbeat) al NameNode para confirmar que está activo.

HDFS sigue una política de replicación para mantener la integridad de los datos, donde cada bloque se replica en varios DataNodes para garantizar la redundancia.

---

## 🛠 **Cómo Funciona HDFS:**

### **Proceso de Escritura** ✏️
Cuando un cliente escribe un archivo en HDFS:

1. El archivo se divide en **bloques** (fragmentos de datos) y se distribuye en múltiples **DataNodes**.
2. El **NameNode** almacena los metadatos sobre qué bloques pertenecen al archivo y en qué DataNodes están almacenados.
3. Cada bloque se replica (típicamente tres veces) en diferentes DataNodes para asegurar la **tolerancia a fallos**.

```mermaid
sequenceDiagram
    participant Cliente
    participant NameNode
    participant DataNode1
    participant DataNode2
    participant DataNode3

    Cliente->>NameNode: Solicitud para escribir archivo
    NameNode->>Cliente: Información de los bloques
    Cliente->>DataNode1: Escribir Bloque 1
    DataNode1->>DataNode2: Replicar Bloque 1
    DataNode2->>DataNode3: Replicar Bloque 1
```

### **Proceso de Lectura** 📖
Cuando un cliente lee un archivo de HDFS:

1. El cliente solicita al **NameNode** la ubicación de los bloques.
2. El cliente recupera los bloques de datos directamente de los **DataNodes**.
3. Los datos se ensamblan nuevamente en el archivo original.

```mermaid
sequenceDiagram
    participant Cliente
    participant NameNode
    participant DataNode1
    participant DataNode2
    participant DataNode3

    Cliente->>NameNode: Solicitud para leer archivo
    NameNode->>Cliente: Ubicación de los bloques
    Cliente->>DataNode1: Leer Bloque 1
    Cliente->>DataNode2: Leer Bloque 2
```

---

## 📂 **Ejemplo: Subida y Descarga de un Archivo**

### **Subida de un Archivo (500 MB)**

El archivo de 500 MB se divide en **bloques de 128 MB**. Debido a la configuración predeterminada de HDFS, los bloques se replican en varios DataNodes para garantizar la **tolerancia a fallos**. En este caso, el archivo se dividirá en 4 bloques (3 bloques de 128 MB y 1 de 116 MB).

```mermaid
sequenceDiagram
    participant Cliente
    participant NameNode
    participant DataNode1
    participant DataNode2
    participant DataNode3

    Cliente->>NameNode: Solicitud para subir archivo (500 MB)
    NameNode->>Cliente: Información de bloques y nodos asignados

    Cliente->>DataNode1: Escribir Bloque 1 (128 MB)
    Cliente->>DataNode2: Escribir Bloque 2 (128 MB)
    Cliente->>DataNode3: Escribir Bloque 3 (128 MB)
    Cliente->>DataNode1: Escribir Bloque 4 (116 MB)

    DataNode1->>DataNode2: Replicar Bloque 1
    DataNode2->>DataNode3: Replicar Bloque 2
    DataNode3->>DataNode1: Replicar Bloque 3
```

### **Descarga de un Archivo (500 MB)**

Para leer el archivo, el **NameNode** le indica al cliente dónde se encuentran almacenados los bloques. El cliente recupera los bloques directamente desde los **DataNodes** y los reensambla para formar el archivo completo.

```mermaid
sequenceDiagram
    participant Cliente
    participant NameNode
    participant DataNode1
    participant DataNode2
    participant DataNode3

    Cliente->>NameNode: Solicitud para descargar archivo
    NameNode->>Cliente: Ubicación de los bloques en los DataNodes

    Cliente->>DataNode1: Descargar Bloque 1 (128 MB)
    Cliente->>DataNode2: Descargar Bloque 2 (128 MB)
    Cliente->>DataNode3: Descargar Bloque 3 (128 MB)
    Cliente->>DataNode1: Descargar Bloque 4 (116 MB)
```

### **Distribución de los Bloques**
En el diagrama, el proceso muestra cómo el archivo de 500 MB se divide en **4 bloques**, con los bloques replicados en los diferentes **DataNodes** para garantizar la **disponibilidad** y **redundancia** en caso de fallos.

---

### **Ventajas de HDFS:**
- **Escalabilidad**: Se puede escalar fácilmente añadiendo más nodos.
- **Tolerancia a fallos**: Se recupera automáticamente de fallos de nodos debido a la replicación de bloques.
- **Alto rendimiento**: Optimizado para procesamiento por lotes, lo que permite un alto rendimiento de datos.

HDFS es una parte clave del ecosistema de Hadoop y es esencial para gestionar eficientemente grandes conjuntos de datos.