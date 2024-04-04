
<h1>¿Qué es TShark?</h1>

TShark es una herramienta de línea de comandos que forma parte del conjunto de herramientas Wireshark. Se utiliza para capturar y analizar el tráfico de red en tiempo real o desde archivos de captura previamente almacenados.

**Uso básico:**

El comando básico de TShark sigue la siguiente estructura:
```
tshark [opciones]
```

Donde:
- `[opciones]`: son los diferentes parámetros y configuraciones que puedes ajustar según tus necesidades.

**Ejemplo de comando básico para capturar tráfico en tiempo real:**
```
tshark -i <interfaz>
```

Este comando comenzará a capturar tráfico en tiempo real en la interfaz de red especificada.

**Opciones comunes:**

- `-i, --interface <nombre_interfaz>`: Especifica la interfaz de red desde la cual capturar el tráfico.
- `-f, --capture-filter <filtro>`: Aplica un filtro de captura para capturar solo paquetes que cumplan con el filtro especificado.
- `-r, --read-file <archivo>`: Lee datos de un archivo de captura en lugar de capturar en tiempo real.
- `-Y, --display-filter <filtro>`: Aplica un filtro de visualización para mostrar solo los paquetes que cumplan con el filtro especificado.

**Ejemplo de comando para leer datos desde un archivo de captura:**
```
tshark -r <archivo_de_captura>
```

Este comando leerá datos de un archivo de captura previamente almacenado.

**Ejemplo de comando con filtro de captura:**
```
tshark -i <interfaz> -f "host 192.168.1.100 and port 80"
```

Este comando capturará solo el tráfico que tenga como origen o destino la dirección IP 192.168.1.100 y el puerto 80.

**Ejemplo de comando con filtro de visualización:**
```
tshark -r <archivo_de_captura> -Y "http.request.method == GET"
```

Este comando mostrará solo los paquetes HTTP que sean solicitudes GET.

**Nota:**
TShark ofrece una gran cantidad de opciones y filtros para capturar y analizar el tráfico de red. Asegúrate de revisar la documentación oficial de TShark para obtener más información sobre las opciones disponibles y cómo utilizarlas.

Para obtener ayuda adicional, puedes usar el comando `tshark --help` o consultar la documentación oficial de Wireshark.