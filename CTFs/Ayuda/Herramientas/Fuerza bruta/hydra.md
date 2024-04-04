
<h1>¿Qué es Hydra?</h1>
Hydra es una herramienta de hacking que se utiliza para llevar a cabo ataques de fuerza bruta contra sistemas que requieren autenticación.
Hydra es altamente configurable y puede ser utilizado para atacar una variedad de servicios y protocolos, incluyendo SSH, FTP, Telnet, HTTP, HTTPS, LDAP, SMB, MySQL, PostgreSQL, VNC, y muchos más. Permite a los hackers automatizar el proceso de prueba de credenciales, lo que ahorra tiempo y esfuerzo en comparación con intentar manualmente múltiples combinaciones de credenciales.

**Uso básico:**

El uso básico de Hydra implica especificar el servicio de destino, las credenciales a probar y opcionalmente un archivo de diccionario si se está realizando un ataque de diccionario. Aquí tienes un ejemplo básico de uso:

```
hydra -l <usuario> -p <diccionario/contraseña> <servicio>://<IP_del_objetivo>
```

Donde:
- `<usuario>`: Especifica el nombre de usuario que deseas probar.
- `<diccionario/contraseña>`: Especifica la contraseña que deseas probar o el archivo de diccionario que contiene las contraseñas a probar.
- `<servicio>`: Especifica el servicio de red que deseas atacar (por ejemplo, `ssh`, `ftp`, `http`, `mysql`, etc.).
- `<IP_del_objetivo>`: Especifica la dirección IP del objetivo que deseas atacar.

**Opciones comunes:**

- `-l <usuario>`: Especifica el nombre de usuario que deseas probar.
- `-L <archivo>`: Especifica un archivo que contiene nombres de usuario a probar.
- `-p <contraseña>`: Especifica una contraseña específica que deseas probar.
- `-P <archivo>`: Especifica un archivo de diccionario que contiene contraseñas a probar.
- `-t <número_de_hilos>`: Especifica el número de hilos de ataque a utilizar.
- `-vV`: Muestra información detallada sobre el proceso de ataque.
- `-o <archivo>`: Guarda los resultados del ataque en un archivo de salida.

**Ejemplo de comando para un ataque de fuerza bruta SSH:**

```
hydra -l usuario -P diccionario.txt ssh://192.168.1.100
```

Este comando intentará iniciar sesión por SSH en la dirección IP `192.168.1.100` utilizando el nombre de usuario `usuario` y probando las contraseñas del archivo `diccionario.txt`.

**Ejemplo de comando para un ataque de fuerza bruta HTTP POST:**

```
hydra -l admin -P diccionario.txt 192.168.1.100 http-post-form "/login.php:user=^USER^&pass=^PASS^:Login failed"
```

Este comando intentará iniciar sesión en un formulario de inicio de sesión HTTP utilizando el nombre de usuario `admin` y probando las contraseñas del archivo `diccionario.txt` en la dirección IP `192.168.1.100`.


**Ejemplo de comando para un ataque de fuerza bruta FTP:**
```
hydra -l s4vitar -P /usr/share/wordlists/rockyou.txt ftp://127.0.0.1 -t 15
```
Donde
- `-l s4vitar`: Esta opción especifica el nombre de usuario que se utilizará en el ataque. En este caso, el nombre de usuario proporcionado es `s4vitar`.
- `-P /usr/share/wordlists/rockyou.txt`: Esta opción especifica la ruta del archivo de texto que contiene las posibles contraseñas a probar durante el ataque de fuerza bruta. En este caso, se está utilizando el archivo `rockyou.txt` como lista de posibles contraseñas. El argumento `-P` indica que el siguiente valor es la ruta del archivo de contraseñas.
- `ftp://127.0.0.1`: Especifica el protocolo y la dirección IP del objetivo. En este caso, se está atacando el protocolo FTP en la dirección IP `127.0.0.1`, que es la dirección de loopback, indicando que el objetivo está en la misma máquina donde se está ejecutando el ataque.
- `-t 15`: Esta opción especifica el número de threads o hilos que se utilizarán en el ataque. En este caso, se están utilizando 15 hilos para acelerar el proceso de ataque.

Nota: los puertos suelen tener un servicio típicamente asignado, como el puerto 22 correspondiente al servicio ssh, sin embargo puede que no siempre sea así y otro puerto corresponda a dicho servicio, para ello podemos dar el parámetro `-s` por ejemplo:
```
hydra -l s4vitar -P /usr/share/wordlists/rockyou.txt ftp://127.0.0.1 -t 15 -s 2222
```
Donde:
`-s 2222` indica el puerto que se va a usar

Recuerda que el uso de Hydra debe ser siempre legal y ético, y debes tener permiso explícito para realizar pruebas de penetración en sistemas que no sean de tu propiedad. El uso indebido de esta herramienta puede tener consecuencias legales graves.