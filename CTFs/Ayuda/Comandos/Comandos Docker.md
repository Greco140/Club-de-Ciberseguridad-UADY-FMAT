<h1>Comandos Docker</h1>

*  `docker run`
Este comando se utiliza para ejecutar un contenedor a partir de una imagen. Puede incluir opciones como el nombre del contenedor, los puertos que se deben exponer, las variables de entorno, entre otros.

* `docker build`
Utilizado para construir una imagen Docker a partir de un Dockerfile y un contexto de construcción (normalmente un directorio con archivos necesarios para la construcción).

* `docker pull`
Se usa para descargar una imagen de un registro de Docker. Si no tienes la imagen localmente, Docker la descargará automáticamente antes de ejecutar un contenedor si es necesario.

* `docker push`
Para subir una imagen a un registro de Docker (por ejemplo, Docker Hub). Esto es útil si has creado una imagen personalizada y deseas compartirla con otros desarrolladores o servidores.

* `docker stop`
Detiene uno o varios contenedores en ejecución.

* `docker rm`
Elimina uno o varios contenedores. Puedes especificar el nombre o el ID del contenedor.

* `docker ps`
Lista los contenedores en ejecución. Puedes utilizar opciones como `-a` para mostrar todos los contenedores (incluso los detenidos) y `-q` para solo mostrar los IDs de los contenedores.

* `docker images`
Lista las imágenes Docker que están presentes en tu sistema.

* `docker exec`
Ejecuta un comando dentro de un contenedor en ejecución.

* `docker-compose`
No es un comando específico de Docker, sino de Docker Compose, una herramienta para definir y ejecutar aplicaciones Docker multi-contenedor. Algunos comandos comunes de Docker Compose incluyen `up` (para iniciar los contenedores definidos en un archivo `docker-compose.yml`), `down` (para detener y eliminar los contenedores), `build` (para construir los servicios), entre otros.

* `docker rm $(docker ps -a -q) --force`
Este comando elimina todos los contenedores en tu sistema. Explicación detallada:
  - `docker ps -a -q`: Lista todos los IDs de los contenedores, incluyendo los que están detenidos.
  - `$(...)`: Sintaxis de sustitución de comandos en bash, que toma la salida del comando entre paréntesis y la utiliza como argumento para el comando externo.
  - `docker rm`: Elimina uno o varios contenedores.
  - `--force`: Opción para forzar la eliminación de los contenedores, incluso si están en ejecución.

* `docker rmi $(docker images -q)`
Este comando elimina todas las imágenes Docker en tu sistema. Explicación detallada:
  - `docker images -q`: Lista todos los IDs de las imágenes Docker.
  - `$(...)`: Sintaxis de sustitución de comandos en bash, que toma la salida del comando entre paréntesis y la utiliza como argumento para el comando externo.
  - `docker rmi`: Elimina una o varias imágenes Docker.

* `docker run -dit ubuntu /bin/bash`
1. `docker run`: Este es el comando principal de Docker que se utiliza para crear y ejecutar contenedores.

2. `-dit` Son opciones que se pasan al comando `docker run`:
   - `-d`: Indica a Docker que el contenedor se debe ejecutar en segundo plano, es decir, en modo demonio.
   - `-i`: Permite que el contenedor se ejecute de manera interactiva, lo que facilita la interacción con él a través de la entrada estándar.
   - `-t`: Asigna un pseudo-terminal (TTY) al contenedor, lo que facilita la interacción con él como si estuvieras trabajando en una terminal.
   
3. `ubuntu` Es el nombre de la imagen base que se utilizará para crear el contenedor. En este caso, estamos utilizando la imagen oficial de Ubuntu.

4. `/bin/bash` Es el comando que se ejecutará dentro del contenedor. Al especificar `/bin/bash`, estamos indicando que queremos abrir una sesión interactiva de la shell Bash dentro del contenedor una vez que esté en funcionamiento.
