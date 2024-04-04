
<h1>¿Qué es WhatWeb?</h1>

WhatWeb es una herramienta de reconocimiento web que identifica tecnologías utilizadas en sitios web. Escanea la página de inicio y las páginas vinculadas para determinar qué tecnologías se utilizan, incluidos servidores web, scripts, CMS (sistemas de gestión de contenidos), frameworks, entre otros.

**Uso básico:**

El comando básico de WhatWeb sigue la siguiente estructura:
```
whatweb [opciones] <URL>
```

Donde:
- `[opciones]`: son los diferentes parámetros y configuraciones que puedes ajustar según tus necesidades.
- `<URL>`: es la URL del sitio web que deseas escanear.

**Ejemplo de comando básico:**
```
whatweb example.com
```

Este comando escaneará el sitio web en busca de tecnologías utilizadas y mostrará los resultados.

**Opciones comunes:**

- `-v, --verbose`: Aumenta la verbosidad de la salida, mostrando más detalles sobre las tecnologías encontradas.
- `-a, --aggression <nivel>`: Establece el nivel de agresividad del escaneo (puede ser `0`, `1`, `2` o `3`).
- `-t, --timeout <segundos>`: Establece el tiempo de espera para las solicitudes HTTP.
- `-e, --exclude <patrón>`: Excluye tecnologías específicas de la detección.
- `-l, --log-output <archivo>`: Guarda la salida del escaneo en un archivo de registro.

**Ejemplo de comando con mayor verbosidad:**
```
whatweb -v example.com
```

Este comando mostrará una salida más detallada, incluyendo información adicional sobre las tecnologías encontradas.

**Ejemplo de comando con mayor agresividad:**
```
whatweb -a 3 example.com
```

Este comando realizará un escaneo más agresivo, lo que puede llevar más tiempo pero puede identificar más tecnologías utilizadas en el sitio web.

**Nota:**
Asegúrate de tener permiso para escanear el sitio web antes de ejecutar WhatWeb, ya que podría considerarse como un escaneo no autorizado si se realiza sin autorización explícita.

Para obtener más información y opciones, puedes consultar la documentación oficial de WhatWeb o usar el comando `whatweb --help`.