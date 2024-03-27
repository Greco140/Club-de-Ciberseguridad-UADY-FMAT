<h1>Comandos linux</h1>

* `teclas: ctrl + c`
Termina el proceso que se estaba ejecutando por terminal

* `ls -la`
Lista los archivos y directorios en el directorio actual en formato largo, incluyendo los archivos ocultos.

* `cd directorio`
Cambia el directorio de trabajo actual al directorio especificado.

* `pwd`
Muestra el directorio de trabajo actual.

* `mkdir nombre_directorio`
Crea un nuevo directorio con el nombre especificado.

* `rm archivo`
Elimina el archivo especificado.

* `cp origen destino`
Copia el archivo o directorio de origen al destino especificado.

* `mv origen destino`
Mueve o renombra el archivo o directorio de origen al destino especificado.

* `cat archivo`
Muestra el contenido del archivo en la terminal.

* `nano archivo`
Abre el archivo en el editor de texto Nano para realizar ediciones.

* `cat archivo | grep "palabra"`
Busca la palabra especificada en el archivo.

* `chmod permisos archivo`
Cambia los permisos de acceso del archivo según los permisos especificados.

* `sudo comando`
Ejecuta el comando con privilegios de superusuario.
`
* `ps`
Muestra información sobre los procesos en ejecución.

* `kill PID`
Detiene el proceso con el ID de proceso especificado.

* `top`
Muestra una lista de los procesos en ejecución y su uso de recursos.

* `lsof -i:puerto` 
Muestra por consola el PID que está ocupando el puerto.

* `pwdx PID`
Muestra por consola la ruta del servicio que está siendo el usado en el PID.

* `$comando | xxd -ps -r`
Revierte una cadena de texto de hexadecimal a ASCII

* `echo "48656c6c6f20576f726c64" | xxd -r -p`
Convierte una cadena hexadecimal en su equivalente en texto plano.

* `$comando | awk '{print $2}'`
Devuelve el segundo argumento de la línea

* `$comando | awk '{print $NF}'`
Devuelve el último argumento de la línea

* `sort -u`
Muestra cadenas únicas por consola

* `echo $!`
Muestra por pantalla el output del comando anterior, "echo" se puede sustituir por otro comando como cd, ls u otro.
