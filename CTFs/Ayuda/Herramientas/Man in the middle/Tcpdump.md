
<h1>¿Qué es Tcpdump?</h1>

Tcpdump es una herramienta de línea de comandos que permite capturar y analizar el tráfico de red en sistemas Unix y Linux. Permite a los usuarios interceptar y mostrar paquetes que están transitando por una red.

**Uso básico:**

El comando básico de Tcpdump sigue la siguiente estructura:
```
tcpdump [opciones]
```

Donde:
- `[opciones]`: son los diferentes parámetros y configuraciones que puedes ajustar según tus necesidades.

**Ejemplo de comando básico para capturar tráfico en tiempo real:**
```
tcpdump -i <interfaz>
```

Este comando comenzará a capturar tráfico en tiempo real en la interfaz de red especificada.

**Opciones comunes:**

- `-i <interfaz>`: Especifica la interfaz de red desde la cual capturar el tráfico.
- `-n`: Muestra direcciones IP en formato numérico en lugar de resolver nombres de hosts.
- `-c <cantidad>`: Limita el número de paquetes que se capturarán.
- `-w <archivo>`: Guarda los paquetes capturados en un archivo en lugar de mostrarlos en la salida estándar.
- `-r <archivo>`: Lee datos de un archivo de captura en lugar de capturar en tiempo real.
- `-s <tamaño>`: Limita el tamaño de la captura de paquetes.

**Ejemplo de comando para leer datos desde un archivo de captura:**
```
tcpdump -r <archivo_de_captura>
```

Este comando leerá datos de un archivo de captura previamente almacenado.

**Ejemplo de comando con filtro de captura:**
```
tcpdump -i <interfaz> host 192.168.1.100 and port 80
```

Este comando capturará solo el tráfico que tenga como origen o destino la dirección IP 192.168.1.100 y el puerto 80.

**Ejemplo de comando con filtro de visualización:**
```
tcpdump -r <archivo_de_captura> tcp port 80 and src host 192.168.1.100
```

Este comando mostrará solo los paquetes TCP que tengan como origen la dirección IP 192.168.1.100 y el puerto de origen 80.

**Nota:**
Tcpdump ofrece una amplia gama de opciones y filtros para capturar y analizar el tráfico de red. Asegúrate de revisar la documentación oficial de Tcpdump para obtener más información sobre las opciones disponibles y cómo utilizarlas.

Para obtener ayuda adicional, puedes usar el comando `tcpdump --help` o consultar la documentación oficial de Tcpdump.