# Introducción a Docker y Docker-compose 🚢

### 🚀 ¿Qué es Docker?

Docker es una plataforma diseñada para desarrollar, desplegar y ejecutar aplicaciones en contenedores. Un **contenedor** es un paquete liviano, portátil y autónomo que incluye todo lo necesario para ejecutar una aplicación: código, runtime, bibliotecas y configuraciones. La principal ventaja de Docker es que permite garantizar que la aplicación se ejecutará de la misma manera en cualquier entorno, ya sea tu máquina local o un servidor en la nube.

```bash
# Ejemplo de comando para ejecutar un contenedor Docker:
docker run -d -p 8080:80 --name mi_contenedor nginx
```

En el ejemplo anterior:

- `-d` indica que el contenedor se ejecutará en segundo plano (modo detached).
- `-p 8080:80` enlaza el puerto 8080 de tu máquina local al puerto 80 del contenedor.
- `--name mi_contenedor` le asigna un nombre al contenedor.
- `nginx` es la imagen que estamos usando para crear el contenedor.

### 🛠 Componentes clave de Docker
1. **Imagen:** Es una plantilla de solo lectura que se utiliza para crear contenedores. Piensa en una imagen como una instantánea de un sistema operativo más una aplicación.
   
   Ejemplo: La imagen `nginx` es una plantilla que contiene el servidor web NGINX.

2. **Contenedor:** Es una instancia ejecutable de una imagen. Cada contenedor es autónomo y aislado.

3. **Dockerfile:** Es un archivo de texto que contiene todas las instrucciones necesarias para construir una imagen. 

```dockerfile
# Ejemplo de un Dockerfile simple:
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```
El Dockerfile anterior:

- Usa la imagen base `node:14`.
- Copia el contenido del directorio actual en el contenedor.
- Instala las dependencias de Node.js.
- Ejecuta el comando `npm start` para iniciar la aplicación.

4. **Docker Hub:** Es un registro público donde puedes encontrar imágenes creadas por otros usuarios o subir las tuyas propias.

### 📦 ¿Qué es Docker-compose?

Docker-compose es una herramienta que te permite definir y ejecutar aplicaciones multi-contenedor. En lugar de ejecutar múltiples contenedores de forma manual, puedes utilizar un archivo `docker-compose.yml` para definir cómo se deben configurar y ejecutar.

```yaml
# Ejemplo básico de un archivo docker-compose.yml:
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
```

Este archivo YAML define dos servicios:

- **web:** que usa la imagen `nginx` y mapea el puerto 80 del contenedor al 8080 de la máquina local.
- **db:** que usa la imagen `mysql` y define una contraseña para el usuario root.

Para iniciar los contenedores definidos en el archivo `docker-compose.yml`, simplemente ejecutas:

```bash
docker-compose up
```

### 🌀 Ventajas de Docker y Docker-compose

1. **Portabilidad:** Los contenedores se ejecutan de la misma manera en cualquier entorno.
2. **Aislamiento:** Cada contenedor es independiente, evitando conflictos entre aplicaciones.
3. **Escalabilidad:** Docker-compose facilita la creación de aplicaciones complejas al permitir la orquestación de múltiples contenedores.
4. **Reproducibilidad:** Con un `Dockerfile` y `docker-compose`, puedes recrear un entorno exacto fácilmente.

### 🖼️ Diferencia entre Imágenes y Contenedores en Docker 🚢

Una de las confusiones más comunes al empezar con Docker es la diferencia entre **imágenes** y **contenedores**. Vamos a aclarar esto:

#### **Imágenes 📸**

Una **imagen** en Docker es como una plantilla de solo lectura que contiene todo lo necesario para ejecutar una aplicación, incluyendo:

- **Sistema operativo** (por ejemplo, Ubuntu, Alpine).
- **Código** de la aplicación.
- **Dependencias** o librerías necesarias para que la aplicación funcione.
- **Configuraciones** o variables de entorno.

**Las imágenes son estáticas**, lo que significa que no cambian una vez que se crean. Son utilizadas para generar contenedores, pero por sí solas no hacen nada. 

Piensa en una imagen como una receta o blueprint que no se ejecuta, pero que contiene todas las instrucciones necesarias para crear algo que sí lo hará.

```bash
# Ejemplo: Listar las imágenes disponibles en tu sistema
docker images
```

Salida típica:

```bash
REPOSITORY       TAG       IMAGE ID       CREATED        SIZE
nginx            latest    d1a364dc548d   2 weeks ago    133MB
mysql            5.7       2a3174d2e2f7   1 month ago    450MB
```

En el ejemplo anterior:

- La imagen `nginx` está lista para ser utilizada para crear un servidor web.
- La imagen `mysql` contiene la base de datos MySQL en su versión 5.7.

#### **Contenedores 🛳️**

Un **contenedor** es una **instancia en ejecución** de una imagen. Es como si tomaras la plantilla (imagen) y la ejecutaras para crear un entorno real donde tu aplicación corre. Un contenedor:

- Está basado en una imagen.
- Es dinámico: puede ejecutar procesos, guardar datos, recibir tráfico de red, etc.
- Puede ser creado, iniciado, detenido y destruido.

Cada contenedor tiene su propio sistema de archivos y entorno de ejecución aislado del resto. Esto significa que puedes tener múltiples contenedores ejecutando la misma imagen sin que interfieran entre sí.

```bash
# Ejemplo: Listar los contenedores en ejecución
docker ps
```

Salida típica:

```bash
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                  NAMES
a1b2c3d4e5f6   nginx     "nginx -g 'daemon off…   5 minutes ago   Up 5 minutes   0.0.0.0:8080->80/tcp   webserver
```

En este caso, el contenedor `webserver` fue creado a partir de la imagen `nginx` y está en ejecución mapeando el puerto 80 al 8080 de la máquina local.

#### 📊 Diferencia Esencial

| **Imágenes** | **Contenedores** |
|:------------:|:----------------:|
| Son plantillas estáticas. | Son instancias en ejecución basadas en una imagen. |
| No pueden modificarse una vez creadas. | Pueden cambiar mientras están en ejecución (p.ej. archivos creados dentro del contenedor). |
| Se almacenan localmente o en repositorios como Docker Hub. | Pueden ser creados, iniciados, detenidos y destruidos. |
| Son inmutables (no cambian). | Son dinámicos y pueden ejecutar procesos. |

---

### 🧑‍🍳 **Metáfora: Restaurante y Recetas**

- **Imagen**: Es como una **receta**. Tienes todos los ingredientes y pasos necesarios para preparar un plato, pero no puedes comer la receta.
- **Contenedor**: Es el **plato servido en la mesa**. Ya se ha preparado a partir de la receta (imagen) y está listo para que lo disfrutes (o en nuestro caso, para que la aplicación se ejecute).

---

💡 **Conclusión**:

- **Imagen = Plantilla (Receta)**.
- **Contenedor = Ejecución de la Imagen (Plato Listo)**.

Las imágenes son el punto de partida, pero son los contenedores los que realmente ejecutan y manejan tu aplicación. Cada vez que usas Docker para ejecutar algo, estás creando uno o más contenedores basados en imágenes preexistentes.

---

### 🎯 Conclusión

Docker y Docker-compose son herramientas poderosas que simplifican el desarrollo y despliegue de aplicaciones en diferentes entornos. No importa si eres un desarrollador que quiere probar su aplicación localmente o si administras un servidor en producción, estas herramientas te ayudarán a crear entornos confiables y escalables.

💡 **Consejo:** Comienza por crear un pequeño contenedor con Docker y luego explora cómo usar Docker-compose para manejar aplicaciones más complejas con múltiples servicios.
