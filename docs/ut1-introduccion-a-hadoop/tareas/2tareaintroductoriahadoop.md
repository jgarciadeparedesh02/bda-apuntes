# Guía para configurar un clúster Hadoop usando Docker y Docker-compose 🚀

### 1. **Instalar Docker**

Docker es una plataforma que permite aislar aplicaciones en contenedores, facilitando su portabilidad y replicabilidad en distintos entornos. Para instalar Docker, sigue estos pasos:

Si ves que Docker está corriendo, ¡estás listo! 🥳

### 2. **Instalar Docker-compose**

Docker-compose es una herramienta que permite orquestar múltiples contenedores con un solo archivo de configuración. Para instalar Docker-compose, ejecuta:

¡Con Docker y Docker-compose instalados, ya estás listo para crear un clúster Hadoop! 🎉

---

### 3. **Crear el archivo docker-compose.yml**

Este archivo definirá los servicios necesarios para ejecutar Hadoop (como NameNode y DataNode). Aquí te dejo un ejemplo:

```yaml
version: '3'
services:
  namenode:
    image: hadoop:latest
    container_name: namenode
    hostname: namenode
    ports:
      - "9870:9870" # Web UI
      - "9000:9000" # RPC
    volumes:
      - ./hadoop_config:/opt/hadoop/etc/hadoop
      - namenode_data:/opt/hadoop/data/nameNode
    networks:
      - hadoop_network

  datanode:
    image: hadoop:latest
    container_name: datanode
    hostname: datanode
    ports:
      - "9864:9864" # Web UI
    volumes:
      - ./hadoop_config:/opt/hadoop/etc/hadoop
      - datanode_data:/opt/hadoop/data/dataNode
    networks:
      - hadoop_network

networks:
  hadoop_network:

volumes:
  namenode_data:
  datanode_data:
```

Este archivo configura dos servicios:
- **NameNode**: encargado de gestionar el sistema de archivos y la información de los bloques de datos.
- **DataNode**: responsable de almacenar los bloques de datos.

---

### 4. **Crear los archivos de configuración de Hadoop**

#### 4.1 **Crear `core-site.xml`**

El archivo `core-site.xml` contiene configuraciones básicas de Hadoop, como la dirección del sistema de archivos (HDFS) y algunas políticas.

```xml
<configuration>
   <property>
      <name>fs.defaultFS</name>
      <value>hdfs://namenode:9000</value> <!-- URL del NameNode -->
   </property>

   <property>
      <name>dfs.replication</name>
      <value>1</value> <!-- Número de réplicas de cada bloque -->
   </property>

   <property>
      <name>dfs.namenode.datanode.registration.ip-hostname-check</name>
      <value>false</value> <!-- Deshabilitar la verificación de IP y nombre de host -->
   </property>

   <property>
      <name>dfs.namenode.rpc-address</name>
      <value>namenode:9000</value> <!-- Dirección de RPC del NameNode -->
   </property>

   <property>
      <name>dfs.permissions.enabled</name>
      <value>false</value> <!-- Deshabilitar las verificaciones de permisos -->
   </property>

   <property>
      <name>ipc.client.connect.max.retries</name>
      <value>10</value> <!-- Número de intentos de reconexión del cliente -->
   </property>

   <property>
      <name>ipc.client.connect.retry.interval</name>
      <value>1000</value> <!-- Intervalo entre intentos de reconexión (ms) -->
   </property>
</configuration>
```

Este archivo configura el sistema de archivos y algunas propiedades de conectividad y permisos.

---

#### 4.2 **Crear `hdfs-site.xml`**

Este archivo define cómo se gestionan los datos en el HDFS. Incluye la configuración de los directorios de almacenamiento y el tamaño de los bloques.

```xml
<configuration>
   <property>
      <name>dfs.replication</name>
      <value>1</value> <!-- Número de réplicas por bloque -->
   </property>

   <property>
      <name>dfs.namenode.name.dir</name>
      <value>file:///opt/hadoop/data/nameNode</value> <!-- Directorio del NameNode -->
   </property>

   <property>
      <name>dfs.datanode.data.dir</name>
      <value>file:///opt/hadoop/data/dataNode</value> <!-- Directorio del DataNode -->
   </property>

   <property>
      <name>dfs.namenode.datanode.registration.ip-hostname-check</name>
      <value>false</value> <!-- Deshabilitar la verificación de IP y nombre de host -->
   </property>

   <property>
      <name>dfs.permissions.enabled</name>
      <value>false</value> <!-- Deshabilitar las verificaciones de permisos -->
   </property>

   <property>
      <name>dfs.namenode.handler.count</name>
      <value>10</value> <!-- Número de manejadores de peticiones del NameNode -->
   </property>

   <property>
      <name>dfs.blocksize</name>
      <value>134217728</value> <!-- Tamaño del bloque: 128MB -->
   </property>
</configuration>
```

Este archivo define cómo se manejan los bloques de datos y dónde se almacenan tanto en el NameNode como en el DataNode.

---

### 5. **Crear el script `start-hdfs.sh`**

Este script se asegura de que el NameNode esté formateado antes de iniciar el servicio.

```bash
#!/bin/bash
if [ ! -d "/opt/hadoop/data/nameNode/current" ]; then
    echo "Formatting NameNode..."
    hdfs namenode -format
fi
hdfs namenode
```

- Si el NameNode aún no ha sido formateado, lo hará.
- Luego inicia el servicio `namenode`.

---

### 6. **Crear el script `init-datanode.sh`**

Este script limpia los datos antiguos del DataNode y configura los permisos necesarios.

```bash
#!/bin/bash
rm -rf /opt/hadoop/data/dataNode/*
chown -R hadoop:hadoop /opt/hadoop/data/dataNode
chmod 755 /opt/hadoop/data/dataNode
hdfs datanode
```

- Elimina cualquier dato antiguo en el directorio del DataNode.
- Establece los permisos correctos.
- Finalmente, inicia el servicio `datanode`.

---

### 🎯 **Conclusión**

Con estos pasos, has creado un clúster de Hadoop utilizando Docker y Docker-compose. Esta configuración te permite simular un entorno de clúster de Hadoop completamente funcional en tu máquina local. 🎉

Ahora, solo resta ejecutar:

```bash
docker-compose up
```

Y tu clúster de Hadoop estará en funcionamiento. ¡Listo para procesar grandes volúmenes de datos!