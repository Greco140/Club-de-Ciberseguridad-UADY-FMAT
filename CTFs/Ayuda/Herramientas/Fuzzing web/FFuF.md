
<h1>¿Qué es FFuF?</h1>
FFuF (Fuzz Faster u Fool) es una herramienta de código abierto diseñada para fuzzing web. Permite realizar búsquedas recursivas de directorios y archivos, descubrimiento de subdominios, escaneo de puertos, y otras tareas relacionadas con la enumeración y la fuerza bruta en aplicaciones web.

**Uso básico:**

El uso básico de FFuF implica especificar el objetivo y algunas opciones básicas. Aquí tienes un ejemplo básico de uso:

```
ffuf -u <URL> -w <wordlist>
```

Donde:
- `<URL>` es la URL del objetivo que deseas escanear.
- `<wordlist>` es el archivo de lista de palabras que FFuF utilizará para realizar el fuzzing.

**Opciones comunes:**

- `-u <URL>`: Especifica la URL de destino.
- `-w <wordlist>`: Especifica la ruta de la lista de palabras a utilizar.
- `-t <threads>`: Especifica el número de hilos de trabajo.
- `-r`: Realiza una redirección en caso de que encuentre una.
- `-e <extensión>`: Especifica una extensión adicional para probar.
- `-recursion`: Realiza una búsqueda recursiva en los directorios.
- `-fc`: Filtra los códigos de respuesta HTTP específicos.
- `-v`: Muestra una salida más detallada.
- `-maxtime <segundos>`: Establece el tiempo máximo de ejecución.
- `-H "Header: Value"`: Especifica una cabecera personalizada en las solicitudes.

**Ejemplo de comando para escanear directorios recursivamente:**

```
ffuf -u https://example.com/FUZZ -w wordlist.txt -recursion -fc 404
```

Este comando realizará una búsqueda recursiva de directorios en la URL `https://example.com/`, utilizando la lista de palabras contenida en `wordlist.txt` y filtrando los resultados que devuelvan un código de respuesta 404 (no encontrado).

**Ejemplo de comando para fuzzing de subdominios:**

```
ffuf -w subdomains.txt -u https://FUZZ.example.com -fs 301
```

Este comando realizará un fuzzing de subdominios en el dominio `example.com`, utilizando la lista de subdominios contenida en `subdomains.txt` y filtrando los resultados que devuelvan un código de respuesta 301 (redirección permanente).

Recuerda que el uso de FFuF debe ser siempre legal y ético, y debes tener permiso explícito para realizar pruebas de penetración en sistemas que no sean de tu propiedad. Utilizar esta herramienta de manera inadecuada puede tener consecuencias legales graves.