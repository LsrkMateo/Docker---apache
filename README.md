# Repositorio de construcción de imágenes Docker para una plantilla de sitio web

Este repositorio contiene un Dockerfile que permite construir imágenes basadas en la carpeta `public_html` utilizando el servidor HTTP Apache. El contenido de esta carpeta es una plantilla tomada de 'https://www.free-css.com/free-css-templates/page292/yogast'.

## Funcionamiento de los comandos en el Dockerfile

El Dockerfile del repositorio contiene los siguientes comandos:

```dockerfile
FROM httpd
COPY ./public_html/ /usr/local/apache2/htdocs/
```

- El comando `FROM httpd` indica que la imagen base utilizada para construir nuestra imagen será `httpd`, que es la imagen oficial de Apache HTTP Server. Esto proporciona una base para nuestro contenedor.

- El comando `COPY ./public_html/ /usr/local/apache2/htdocs/` copia el contenido de la carpeta `public_html` del repositorio al directorio `/usr/local/apache2/htdocs/` dentro del contenedor. Esto asegura que el contenido de nuestra plantilla de sitio web esté disponible para ser servido por el servidor Apache.

## Pasos para que el Dockerfile tenga efecto

A continuación, se detallan los pasos necesarios para que el Dockerfile surta efecto y se ejecute nuestra aplicación web:

1. Ejecutar el siguiente comando:

   ```shell
   docker run -dit --name myapache -p 8080:80 httpd
   ```

   - `docker run` es el comando para crear y ejecutar un nuevo contenedor.
   - `-dit` son opciones para que el contenedor se ejecute en segundo plano (`-d`), en modo interactivo (`-i`) y para asignarle un pseudo-TTY (`-t`).
   - `--name myapache` establece el nombre del contenedor como `myapache`.
   - `-p 8080:80` mapea el puerto 8080 del host al puerto 80 del contenedor, lo que permite acceder al servidor web a través del puerto 8080 del host.
   - `httpd` es el nombre de la imagen base utilizada para el contenedor.

2. Opcionalmente, si deseas interactuar con el contenedor y ejecutar comandos dentro de él, puedes ejecutar el siguiente comando:

   ```shell
   docker exec -it myapache bash
   ```

   - `docker exec` se utiliza para ejecutar un comando dentro de un contenedor en ejecución.
   - `-it` especifica que se desea ejecutar el comando de forma interactiva y asignarle un pseudo-TTY.
   - `myapache` es el nombre del contenedor en el que deseamos ejecutar el comando.
   - `bash` indica que queremos ejecutar el shell Bash dentro del contenedor.

3. Una vez dentro del contenedor, puedes ubicarte en el directorio `htdocs` utilizando el siguiente comando:

   ```shell
   cd /usr/local/apache2/htdocs/
   ```

   Este directorio es donde se publicará nuestro proyecto de Apache, y es donde se encuentra el contenido de la plantilla de sitio web.

   - Utiliza comandos como `ls`, `cat` o `touch` para modificar los elementos dentro del directorio `htdocs` y personalizar tu proyecto de sitio web.

Recuerda que estos pasos son opcionales, pero se recomienda seguirlos para una mayor comprensión y personalización de tu aplicación web basada en Docker y Apache.
## Crear una imagen usando el Dockerfile

Para crear una imagen utilizando el Dockerfile del repositorio, puedes ejecutar el siguiente comando:

```shell
docker build -t mi-imagen .
```

Aquí se explica en detalle cada parte del comando:

- `docker build` es el comando utilizado para construir una imagen a partir de un Dockerfile.
- `-t mi-imagen` establece el nombre y la etiqueta de la imagen que se creará. En este caso, se utiliza el nombre "mi-imagen", pero puedes elegir el nombre que desees.
- `.` indica que el contexto de construcción se encuentra en el directorio actual, donde se encuentra el Dockerfile. Asegúrate de ejecutar este comando en el directorio que contiene el Dockerfile.

Una vez que se ejecute este comando, Docker leerá el Dockerfile y construirá una imagen utilizando las instrucciones y los archivos especificados en él. La imagen resultante se etiquetará como "mi-imagen" y estará lista para ser utilizada.

## Ejecutar un contenedor usando la imagen creada

Una vez que hayas creado la imagen utilizando el Dockerfile, puedes ejecutar un contenedor basado en esa imagen con el siguiente comando:

```shell
docker run -p 5000:80 --name myapache1 -d mi-imagen
```

A continuación se explica detalladamente cada parte del comando:

- `docker run` es el comando utilizado para crear y ejecutar un contenedor a partir de una imagen.
- `-p 5000:80` realiza un mapeo de puertos, lo que significa que el puerto 5000 del host se redirige al puerto 80 del contenedor. Esto permite acceder al servidor web dentro del contenedor a través del puerto 5000 del host.
- `--name myapache1` establece el nombre del contenedor como "myapache1". Puedes elegir cualquier nombre que desees.
- `-d` indica que el contenedor se debe ejecutar en segundo plano (modo daemon).
- `mi-imagen` es el nombre de la imagen que deseas utilizar para crear el contenedor. Asegúrate de que la imagen se haya creado previamente utilizando el comando `docker build`.

Después de ejecutar este comando, Docker creará un nuevo contenedor basado en la imagen especificada y lo ejecutará en segundo plano. El contenedor se llamará "myapache1" y estará disponible en el puerto 5000 del host.

## Información de referencia

El contenido y la información utilizados en este repositorio se obtuvieron de las siguientes fuentes:

- Plantilla de CSS: 'https://www.free-css.com/free-css-templates/page292/yogast'
- Tutorial de referencia: 'https://www.youtube.com/watch?v=-563XKoRfZ8&t=21s'
- Imagen oficial de Apache HTTP Server en Docker Hub: 'https://hub.docker.com/_/httpd'

## ¡Apoya el proyecto y comparte tus ideas!

Si encuentras útil este proyecto o tienes ideas para mejorarlo, ¡no dudes en compartir tus comentarios y sugerencias! Puedes abrir problemas en el repositorio, enviar solicitudes de extracción o ponerse en contacto con el autor para compartir tus pensamientos.

¡Gracias por tu apoyo y por utilizar este repositorio!
