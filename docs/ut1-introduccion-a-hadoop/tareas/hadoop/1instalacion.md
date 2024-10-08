
#**Práctica Guiada: Implementación de un Nodo Hadoop con Docker**

#### **1. Introducción**

En esta práctica, vas a configurar un clúster Hadoop de un solo nodo utilizando Docker. Hadoop es un framework que permite el procesamiento de grandes cantidades de datos distribuidos en varios nodos. Para fines educativos, configuraremos un clúster de un solo nodo. Docker facilitará el proceso de instalación, ya que encapsula todo en un contenedor aislado del sistema operativo principal.

#### **2. Requisitos Previos**

- **Docker instalado**: Asegúrate de tener Docker instalado y funcionando en tu máquina. Si no lo tienes instalado, puedes descargarlo desde [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
- **Git instalado**: Se necesita Git para clonar el repositorio de configuración.

#### **3. Clonar el repositorio del proyecto**

Para empezar, vamos a clonar el repositorio donde ya está configurada la imagen de Hadoop. Este repositorio contiene un archivo `Dockerfile`, que es un script que define cómo se debe crear la imagen de Docker con todos los servicios y configuraciones de Hadoop.

```bash
git clone https://github.com/rancavil/hadoop-single-node-cluster.git
cd hadoop-single-node-cluster
```

- **¿Qué es esto?**: El comando `git clone` descarga una copia local del repositorio alojado en GitHub, y `cd` te lleva al directorio recién clonado.

#### **4. Construir la imagen Docker de Hadoop**

Ahora que tenemos los archivos de configuración, es momento de construir una imagen Docker. Esta imagen contendrá todo lo necesario para correr Hadoop, incluyendo Java, Hadoop y las configuraciones necesarias para un nodo único.

```bash
docker build -t hadoop .
```

- **Explicación**: 
    - `docker build` es el comando que construye una imagen a partir de un archivo `Dockerfile`.
    - `-t hadoop` asigna la etiqueta "hadoop" a esta imagen, lo que nos facilitará su referencia más adelante.
    - El `.` indica que el contexto para la construcción es el directorio actual.

#### **5. Crear y correr el contenedor Hadoop**

Una vez que la imagen está construida, vamos a ejecutar un contenedor basado en ella. Un contenedor es una instancia de la imagen, ejecutándose como si fuera una pequeña máquina virtual, pero más ligera y eficiente.

```bash
docker run --name hadoop-container -p 9864:9864 -p 9870:9870 -p 8088:8088 -p 9000:9000 --hostname hadoop hadoop
```

- **Explicación**:
    - `docker run`: Este comando crea y corre un contenedor.
    - `--name hadoop-container`: Asigna el nombre "hadoop-container" al contenedor.
    - `-p 9864:9864 -p 9870:9870 -p 8088:8088 -p 9000:9000`: Mapea los puertos del contenedor a tu máquina local. Esto te permite acceder a la interfaz web de Hadoop desde tu navegador y establecer la conexión entre el contenedor y tu máquina para el uso de HDFS.
        - `9864`: Puerto del DataNode.
        - `9870`: Puerto del NameNode (UI para monitoreo de HDFS).
        - `8088`: Puerto del ResourceManager (UI para monitoreo de trabajos en YARN).
        - `9000`: Puerto de HDFS para el NameNode.
    - `--hostname hadoop`: Asigna el nombre de host "hadoop" al contenedor.

#### **6. Abrir una terminal dentro del contenedor**

Para interactuar con Hadoop dentro del contenedor, necesitas abrir una terminal en su interior. Hay dos formas de hacerlo:

- **Modo gráfico**: Si estás usando Docker Desktop, puedes acceder al contenedor desde la interfaz gráfica seleccionando el contenedor "hadoop-container" y abriendo una terminal desde ahí.
  
- **Modo terminal**: Si prefieres usar la terminal, ejecuta el siguiente comando:
  
```bash
docker exec -i -t hadoop-container /bin/bash
```

- **Explicación**:
    - `docker exec`: Permite ejecutar comandos dentro de un contenedor en ejecución.
    - `-i -t`: Estas opciones te permiten interactuar de manera interactiva con el contenedor (modo terminal).
    - `hadoop-container`: Es el nombre del contenedor que ejecutaste anteriormente.
    - `/bin/bash`: Especifica que quieres abrir una shell Bash dentro del contenedor.

#### **7. Probar Hadoop y HDFS**

Ahora que estás dentro del contenedor, es momento de probar que Hadoop y su sistema de archivos HDFS están funcionando correctamente. Comienza creando un directorio en HDFS.

```bash
hdfs dfs -mkdir /user
```

Luego, lista los archivos del sistema de archivos HDFS recursivamente:

```bash
hdfs dfs -ls -R /
```

- **Explicación**:
    - `hdfs dfs`: Este es el comando que utilizas para interactuar con el sistema de archivos distribuido de Hadoop (HDFS).
    - `-mkdir /user`: Crea un directorio llamado "user" en el sistema de archivos HDFS.
    - `-ls -R /`: Lista de manera recursiva todos los archivos en HDFS, comenzando desde la raíz.

#### **8. Acceder a la interfaz web de Hadoop**

Puedes acceder a las interfaces de monitoreo de Hadoop desde tu navegador utilizando las siguientes direcciones:

- **NameNode (HDFS)**: [http://localhost:9870](http://localhost:9870)
- **ResourceManager (YARN)**: [http://localhost:8088](http://localhost:8088)

Estas interfaces te permiten ver el estado del clúster, los nodos disponibles, y los trabajos que se están ejecutando.

#### **9. Apagar el contenedor**

Cuando termines de trabajar, puedes detener y eliminar el contenedor. Para detener el contenedor sin eliminarlo, ejecuta:

```bash
docker stop hadoop-container
```

Si deseas eliminar el contenedor completamente:

```bash
docker rm hadoop-container
```

- **Explicación**:
    - `docker stop`: Detiene el contenedor en ejecución.
    - `docker rm`: Elimina el contenedor de Docker, liberando espacio.

#### **10. Conclusión**

Has completado la práctica para configurar un clúster Hadoop de un solo nodo usando Docker. Este entorno te permite experimentar con las funcionalidades principales de Hadoop sin necesidad de una configuración compleja de varios nodos o sistemas distribuidos. Con este entorno, puedes practicar la gestión de archivos en HDFS, ejecutar trabajos en YARN y familiarizarte con las interfaces de monitoreo de Hadoop.
