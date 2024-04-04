<h1>¿Cómo genero claves SSH?</h1>

1. Abre la terminal en tu sistema Linux.
2. Ejecuta el comando `ssh-keygen` y sigue las instrucciones.
3. Te pedirá que elijas una ubicación para guardar la clave. Puedes dejar la ubicación predeterminada o especificar una ruta diferente.
4. Te pedirá que ingreses una frase de contraseña opcional para proteger tu clave privada. Puedes dejarla en blanco si no deseas una frase de contraseña.
5. Una vez completados los pasos, se generarán dos archivos: uno con extensión `.pub` (clave pública) y otro sin extensión (clave privada).

¡Y eso es todo! Ahora has generado un par de claves SSH que puedes usar para autenticarte en servidores remotos. Asegúrate de guardar tu clave privada de forma segura y no compartirla con nadie.


<h1>Cómo añado las claves de otros usuarios para que se conecten a mi máquina?</h1>

Para permitir que otros usuarios se conecten a tu máquina utilizando claves SSH, necesitas agregar sus claves públicas a tu archivo `~/.ssh/authorized_keys`. Aquí tienes los pasos:

1. Obtén la clave pública del usuario que deseas permitir que se conecte a tu máquina. Puede estar en un archivo `.pub` o en el contenido del archivo.
2. Abre el archivo `~/.ssh/authorized_keys` en tu editor de texto preferido. Si no existe, puedes crearlo.
3. Copia la clave pública del usuario y pégala al final del archivo `authorized_keys`.
4. Guarda el archivo y asegúrate de que tenga permisos correctos. Los permisos deben ser `600` (rw-------) para el archivo `authorized_keys` y `700` (drwx------) para el directorio `~/.ssh`.
5. ¡Listo! Ahora ese usuario puede autenticarse en tu máquina utilizando su clave privada correspondiente.

Recuerda que cada usuario debe tener su propia entrada en el archivo `authorized_keys`, y puedes agregar múltiples claves públicas para diferentes usuarios si es necesario.