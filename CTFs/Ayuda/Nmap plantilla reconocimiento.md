<h1>Nmap plantilla</h1>
<h3>Plantilla:

nmap -p- --open --min-rate=5000 -vvv -sCV -n -Pn (ip víctima) -oN escaneo</h3>

Donde:
- **`nmap`**: Es el comando para ejecutar Nmap, una herramienta de escaneo de red.
    
- **`-p-`**: Esta opción indica a Nmap que escanee todos los puertos, desde el puerto 1 hasta el puerto 65535. El guion (`-`) después de `-p` significa "todos los puertos".
    
- **`--open`**: Esta opción le dice a Nmap que muestre solo los puertos que están abiertos. Esto ayuda a filtrar la salida y mostrar solo la información relevante.
    
- **`--min-rate=5000`**: Esta opción establece la velocidad mínima de escaneo a 5000 paquetes por segundo. Esto puede aumentar la velocidad del escaneo, pero ten en cuenta que escanear a una velocidad muy alta puede aumentar la probabilidad de detección o de ser bloqueado por firewalls o sistemas de detección de intrusos.
    
- **`-vvv`**: Esta opción activa el nivel de verbosidad de la salida de Nmap a "muy, muy, muy" alto. Esto significa que se mostrará una gran cantidad de información detallada sobre el progreso del escaneo y los resultados.
    
- **`-sCV`**: Esta opción le dice a Nmap que realice un escaneo utilizando la detección de versiones (`-sV`) para determinar qué servicios están ejecutándose en los puertos abiertos y qué versión de software están utilizando. También activa la detección de scripts (`-sC`), que ejecuta una serie de scripts de detección de seguridad prediseñados para identificar vulnerabilidades comunes.
    
- **`-n`**: Esta opción indica a Nmap que no realice la resolución de DNS inversa en las direcciones IP, lo que significa que no intentará determinar los nombres de host asociados con las direcciones IP.
    
- **`-Pn`**: Esta opción le dice a Nmap que no realice el ping de descubrimiento de hosts antes de escanear. Esto es útil si sospechas que el host objetivo puede estar filtrando los paquetes ICMP o si deseas escanear hosts que no responden al ping.
    
- **`(ip víctima)`**: Aquí debes ingresar la dirección IP del host que deseas escanear.
    
- **`-oN escaneo`**: Esta opción indica a Nmap que guarde los resultados del escaneo en un archivo de texto con el nombre "escaneo". La letra "o" seguida de "N" significa "guardar en formato normal".
