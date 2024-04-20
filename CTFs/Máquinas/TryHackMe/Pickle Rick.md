<h1>
    Pickle Rick
</h1>

<h2>
    Escaneando puertos abiertos
</h2>

Primeramente usamos nmap para escanear los puertos abiertos, con su respectiva versión y scripts básicos de reconocimiento, el resultado lo almacenaremos en el archivo "escaneo" en texto plano.

```
nmap -p- --open -sS --min-rate=5000 -vvv -sCV -n -Pn 10.10.63.240 -oN escaneo
```

Del escáneo podemos quedarnos con la siguiente información:

```
Nmap scan report for 10.10.63.240
Host is up, received user-set (0.20s latency).
PORT   STATE SERVICE    REASON         VERSION
22/tcp open  ssh        syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
80/tcp open  tcpwrapped syn-ack ttl 63
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
Ahora visitaremos la página web que corre en el puerto 80 de la máquina, lo que encontramos es: 

![imagen](https://hackmd.io/_uploads/BJjXZ6gbA.png)

Podemos echar un ojo al código fuente de la página con las teclas `ctrl + u`:

![imagen](https://hackmd.io/_uploads/SkBvWaxZ0.png)

Notamos que hay un comentario que dice: 

**Username: R1ckRul3s**

Lo guardamos ya que probablemente nos sirva en algún momento.

<h2>
    Fuzzing web
</h2>

Ahora hagamos algo de Fuzzing para encontrar posibles directorios ocultos:


```
wfuzz -c --hc 404,200 -t 200 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u http://10.10.63.240/FUZZ
```

En otra pestaña de la terminal podemos probar con ficheros .txt

```
wfuzz -c --hc 404,200 -t 200 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u http://10.10.63.240/FUZZ.txt
```

Y finalmente

```
wfuzz -c --hc 404,200 -t 200 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u http://10.10.63.240/FUZZ.php
```

Hallamos el fichero robots.txt, el cual en ocasiones contiene información interesante, echemos un ojo:

![imagen](https://hackmd.io/_uploads/ryanrag-R.png)

Nada más allá que el texto mostrado, podemos guardarlo por la probabilidad de que sea útil en algún momento.

Ahora probamos con el fichero oculto login.php

![imagen](https://hackmd.io/_uploads/rJfmIplWA.png)

Probamos a usar la información que recolectamos:

```
Username: R1ckRul3s

Password: Wubbalubbadubdub
```

![imagen](https://hackmd.io/_uploads/HJc5LagbA.png)

¡Y estamos dentro! :D

Probamos a usar comandos de linux, tal como `ls`

![imagen](https://hackmd.io/_uploads/BJtZDTlWC.png)

Ahora probamos a mirar el contenido de  "Sup3rS3cretPickl3Ingred.txt" con: `cat Sup3rS3cretPickl3Ingred.txt`
y **obtenemos la primera flag: `mr. meeseek hair`**


<h2>
    Reverse Shell
</h2>

Ahora nos enviaremos una reverse shell a nuestra máquina para tener mayor comodidad, posteriormente le daremos tratamiento a la tty para tener una terminal completamente interactiva, para ello seguimos los pasos del repositorio del Club, mismos que se encuentran en:

https://github.com/Greco140/Club-de-Ciberseguridad-UADY-FMAT/blob/main/CTFs/Ayuda/Shell%20reverse/Shell%20reverse%20con%20python.md

y 

https://github.com/Greco140/Club-de-Ciberseguridad-UADY-FMAT/blob/main/CTFs/Ayuda/Shell%20reverse/Tratamiento%20de%20la%20TTY.md

Una vez seguidos los pasos, tenemos una terminal completamente interactiva y podemos trabajar más cómodamente.

Como usuario "www-data" podemos acceder al directorio /home/rick

![imagen](https://hackmd.io/_uploads/Hknh_TeWA.png)

Al usar `ls` para listar los ficheros y directorios en la ruta actual, encontramos el fichero "second ingredients", vemos el contenido con `cat second ingredients` y **encontramos la segunda flag `1 jerry tear`**

Ahora probamos acceder al directorio `/root`

![imagen](https://hackmd.io/_uploads/Bks0YTg-A.png)

Notamos que no podemos acceder debido a la falta de permisos, por tanto es hora de escalar privilegios.


<h2>
    Escalada de privilegios
</h2>

Podemos ejecutar el comando `sudo -l` para listar los binarios que nos permitan ser ejecutados como root:

![imagen](https://hackmd.io/_uploads/r12756lZC.png)

Vemos que podemos ejecutar todos los comandos, por tanto podemos usar `sudo su` 

![imagen](https://hackmd.io/_uploads/B19Pqpg-C.png)

Ahora hacemos un `cat 3rd.txt` y **obtenemos la última flag: `fleeb juice`**

También pudimos haber buscado binarios con permisos SUID desde la raíz, con el comando `find / -perm -4000  2>/dev/null`, y aprovechar alguno de los ficheros para escalar privilegios, tal como el SUID `/bin/mount`, usando los comandos 
```
sudo mount -o bind /bin/sh /bin/mount

sudo mount
```
y también nos convertimos en usuario root :D

![imagen](https://hackmd.io/_uploads/rJKE2aebA.png)



Con esto la máquina ha sido completada, espero te haya gustado y hayas aprendido algo nuevo :)
