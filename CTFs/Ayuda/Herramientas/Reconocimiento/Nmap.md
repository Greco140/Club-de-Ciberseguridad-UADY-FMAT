
<h1>¿Qué es Nmap?</h1>
Nmap es una herramienta de escaneo de red de código abierto ampliamente utilizada para descubrir hosts y servicios en una red, así como para realizar tareas de enumeración y auditoría de seguridad. Aquí tienes cómo usar Nmap:

**Uso básico:**

1. Abre tu terminal.

2. Ejecuta el siguiente comando para realizar un escaneo básico de hosts en una red:

```
nmap <target>
```

Donde `<target>` puede ser una dirección IP específica, un rango de direcciones IP o un nombre de dominio.

3. Una vez que ingreses el comando, Nmap comenzará a escanear la red en busca de hosts activos y servicios en esos hosts.

4. Una vez completado el escaneo, Nmap mostrará una lista de los hosts encontrados junto con los servicios y puertos abiertos en cada host.

**Opciones comunes:**

- `-sS`: Realiza un escaneo de tipo SYN (half-open) para determinar los puertos abiertos.
- `-sT`: Realiza un escaneo de tipo TCP connect para determinar los puertos abiertos.
- `-sU`: Realiza un escaneo de tipo UDP para determinar los puertos UDP abiertos.
- `-p <port(s)>`: Especifica los puertos que se escanearán. Puedes especificar un solo puerto, un rango de puertos o una lista separada por comas.
- `-O`: Intenta detectar el sistema operativo de los hosts escaneados.
- `-A`: Realiza un escaneo de detección de versiones y sistema operativo junto con otros tipos de escaneo.
- `-v`: Muestra una salida más detallada.
- `-T<0-5>`: Controla el tiempo de ejecución del escaneo, donde 0 es el más lento y 5 es el más rápido.
- `-oN <archivo>`: Guarda la salida del escaneo en un archivo en formato normal.
- `-oX <archivo>`: Guarda la salida del escaneo en un archivo en formato XML.

**Ejemplo de uso:**

```
nmap -p- --open --min-rate=5000 -vvv -sCV -n -Pn <ip víctima> -oN escaneo
```
Donde:
- **`nmap`**: Es el comando para ejecutar Nmap, una herramienta de escaneo de red.
    
- **`-p-`**: Esta opción indica a Nmap que escanee todos los puertos, desde el puerto 1 hasta el puerto 65535. El guion (`-`) después de `-p` significa "todos los puertos".
    
- **`--open`**: Esta opción le dice a Nmap que muestre solo los puertos que están abiertos. Esto ayuda a filtrar la salida y mostrar solo la información relevante.
    
- **`--min-rate=5000`**: Esta opción establece la velocidad mínima de escaneo a 5000 paquetes por segundo. Esto puede aumentar la velocidad del escaneo, pero ten en cuenta que escanear a una velocidad muy alta puede aumentar la probabilidad de detección o de ser bloqueado por firewalls o sistemas de detección de intrusos.
    
- **`-vvv`**: Esta opción activa el nivel de verbosidad de la salida de Nmap a "muy, muy, muy" alto. Esto significa que se mostrará una gran cantidad de información detallada sobre el progreso del escaneo y los resultados.
    
- **`-sCV`**: Esta opción le dice a Nmap que realice un escaneo utilizando la detección de versiones (`-sV`) para determinar qué servicios están ejecutándose en los puertos abiertos y qué versión de software están utilizando. También activa la detección de scripts (`-sC`), que ejecuta una serie de scripts de detección de seguridad prediseñados para identificar vulnerabilidades comunes.
    
- **`-n`**: Esta opción indica a Nmap que no realice la resolución de DNS inversa en las direcciones IP, lo que significa que no intentará determinar los nombres de host asociados con las direcciones IP.
    
- **`-Pn`**: Esta opción le dice a Nmap que no realice el ping de descubrimiento de hosts antes de escanear. Esto es útil si sospechas que el host objetivo puede estar filtrando los paquetes ICMP o si deseas escanear hosts que no responden al ping.
    
- **`<ip víctima>`**: Aquí debes ingresar la dirección IP del host que deseas escanear.
    
- **`-oN escaneo`**: Esta opción indica a Nmap que guarde los resultados del escaneo en un archivo de texto con el nombre "escaneo". La letra "o" seguida de "N" significa "guardar en formato normal".

Una vez completado el escaneo, Nmap mostrará los hosts encontrados junto con los puertos abiertos en cada uno.

Recuerda que es importante utilizar Nmap de manera ética y legal, y solo en sistemas en los que tengas permiso para hacerlo. El uso indebido de esta herramienta puede tener consecuencias legales graves.