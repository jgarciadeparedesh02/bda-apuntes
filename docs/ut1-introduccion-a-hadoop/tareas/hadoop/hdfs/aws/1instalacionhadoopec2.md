# Instalación de Hadoop en AWS (EC2)

### Paso 1: Conéctate a la instancia EC2

Primero, conéctate a tu instancia de EC2 mediante SSH:

```bash
ssh -i /path/to/your-key.pem ubuntu@<IP_de_la_instancia>
```

### Paso 2: Actualiza el sistema e instala Java

Hadoop requiere Java, así que primero instala Java antes de continuar.

1. Actualiza los paquetes de la instancia EC2:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. Instala Java (Hadoop requiere Java 8):
   ```bash
   sudo apt install openjdk-8-jdk -y
   ```
3. Verifica la instalación de Java:
   ```bash
   java -version
   ```

### Paso 3: Descarga e instala Hadoop

1. Descarga la última versión de Hadoop desde el sitio oficial de Apache:
   ```bash
   wget https://downloads.apache.org/hadoop/common/hadoop-3.3.5/hadoop-3.3.5.tar.gz
   ```
2. Extrae el archivo descargado:
   ```bash
   tar -xzvf hadoop-3.3.5.tar.gz
   ```
3. Mueve Hadoop a una ubicación adecuada, por ejemplo, `/usr/local/`:
   ```bash
   sudo mv hadoop-3.3.5 /usr/local/hadoop
   ```

### Paso 4: Configura variables de entorno

Configura las variables de entorno necesarias para Hadoop.

1. Edita el archivo `.bashrc` del usuario actual:
   ```bash
   nano ~/.bashrc
   ```
2. Agrega las siguientes líneas al final del archivo:

   ```bash
   export HADOOP_HOME=/usr/local/hadoop
   export HADOOP_INSTALL=$HADOOP_HOME
   export HADOOP_MAPRED_HOME=$HADOOP_HOME
   export HADOOP_COMMON_HOME=$HADOOP_HOME
   export HADOOP_HDFS_HOME=$HADOOP_HOME
   export YARN_HOME=$HADOOP_HOME
   export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
   export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
   export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
   export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=$HADOOP_HOME/lib/native"
   ```

3. Guarda y cierra el archivo.

4. Aplica los cambios:
   ```bash
   source ~/.bashrc
   ```

### Paso 5: Configura Hadoop

Ahora edita los archivos de configuración de Hadoop.

1. Edita el archivo `hadoop-env.sh` para configurar `JAVA_HOME`:
   ```bash
   sudo nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh
   ```
2. Asegúrate de que la variable `JAVA_HOME` esté configurada correctamente:
   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
   ```

### Paso 6: Configura los archivos core-site.xml y hdfs-site.xml

1. Edita el archivo `core-site.xml`:
   ```bash
   nano /usr/local/hadoop/etc/hadoop/core-site.xml
   ```
   ```xml
   <configuration>
      <property>
         <name>fs.defaultFS</name>
         <value>hdfs://localhost:9000</value>
         <description>NameNode URI</description>
      </property>
      <property>
         <name>hadoop.tmp.dir</name>
         <value>/usr/local/hadoop/tmp</value>
         <description>Directorio temporal de Hadoop</description>
      </property>
   </configuration>
   ```
2. Edita el archivo `hdfs-site.xml`:

   ```bash
   nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml
   ```

   ```xml
   <configuration>
      <property>
         <name>dfs.replication</name>
         <value>1</value>
         <description>Factor de replicación de HDFS (para modo pseudo-distribuido es 1)</description>
      </property>

      <property>
         <name>dfs.namenode.name.dir</name>
         <value>file:///usr/local/hadoop/hdfs/namenode</value>
         <description>Directorio para los archivos del NameNode</description>
      </property>

      <property>
         <name>dfs.datanode.data.dir</name>
         <value>file:///usr/local/hadoop/hdfs/datanode</value>
         <description>Directorio para los bloques de datos del DataNode</description>
      </property>

      <property>
         <name>dfs.permissions</name>
         <value>false</value>
         <description>Desactiva los permisos de HDFS para simplificar la configuración</description>
      </property>
   </configuration>
   ```

   3. Crea las carpetas `hdfs/namenode` y `hdfs/datanode`:

   ```bash
   mkdir -p /usr/local/hadoop/tmp
   mkdir -p /usr/local/hadoop/hdfs/namenode
   mkdir -p /usr/local/hadoop/hdfs/datanode
   ```

### Paso 6: Formatea el sistema de archivos de Hadoop

Antes de iniciar Hadoop, necesitas formatear el sistema de archivos.

1. Ejecuta el siguiente comando para formatear el sistema de archivos de HDFS:
   ```bash
   hdfs namenode -format
   ```

### Paso 7: Inicia Hadoop

Para iniciar Hadoop, ejecuta los siguientes comandos:

1. Inicia el NameNode y el DataNode:
   ```bash
   start-dfs.sh
   ```
2. Inicia YARN:
   ```bash
   start-yarn.sh
   ```

### Paso 9: Detén Hadoop

Para detener Hadoop, usa los siguientes comandos:

1. Detén HDFS:
   ```bash
   stop-dfs.sh
   ```
2. Detén YARN:
   ```bash
   stop-yarn.sh
   ```

## Posibles errores

### Permission denied (publickey).

El error "Permission denied (publickey)" al ejecutar `start-yarn.sh` o similar indica que el sistema está intentando iniciar los nodemanagers y resourcemanager en los nodos locales de Hadoop, pero está fallando la autenticación SSH.

Hadoop, por defecto, intenta comunicarse entre nodos a través de SSH para iniciar YARN, y parece que no se ha configurado correctamente el acceso SSH entre nodos. Si estás ejecutando un clúster pseudo-distribuido (es decir, en una sola máquina), necesitarás configurar SSH para que el usuario actual pueda conectarse a localhost sin contraseña. Aquí están los pasos para solucionar este problema:

#### Paso 1: Configura SSH sin contraseña

1. **Genera un par de claves SSH si no tienes uno ya creado**:
   Ejecuta el siguiente comando y acepta los valores predeterminados:

   ```bash
   ssh-keygen -t rsa -P ""
   ```

   Esto creará una clave SSH pública y privada en el directorio `~/.ssh/` (por defecto).

2. **Agrega la clave pública al archivo `authorized_keys`** para permitir la autenticación SSH sin contraseña en localhost:
   ```bash
   cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
   ```
3. **Asegúrate de que los permisos sean correctos**:
   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```
4. **Prueba la conexión SSH a localhost** para verificar que puedas conectarte sin contraseña:

   ```bash
   ssh localhost
   ```

   Si no te pide una contraseña y te deja entrar, la configuración es correcta. Puedes salir de la sesión con `exit`.

#### Paso 2: Inicia YARN de nuevo

Después de configurar SSH, intenta iniciar YARN de nuevo:

```bash
start-yarn.sh
```

Esto debería iniciar correctamente tanto el ResourceManager como los NodeManagers sin el error de "Permission denied".
