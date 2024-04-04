
<h1>¿Qué es WPScan?</h1>

WPScan es una herramienta de escaneo de seguridad diseñada específicamente para detectar y explotar vulnerabilidades en sitios web que utilizan WordPress. Proporciona una forma automatizada de identificar posibles puntos débiles en la configuración y los plugins de WordPress.

**Uso básico:**

El comando básico de WPScan sigue la siguiente estructura:
```
wpscan [opciones] <URL>
```

Donde:
- `[opciones]`: son los diferentes parámetros y configuraciones que puedes ajustar según tus necesidades.
- `<URL>`: es la URL del sitio web de WordPress que deseas escanear.

**Ejemplo de comando básico:**
```
wpscan --url http://example.com
```

Este comando básico escaneará el sitio web en busca de vulnerabilidades conocidas y mostrará los resultados.

**Opciones comunes:**

- `-e, --enumerate`: Enumera plugins, temas y usuarios.
- `--plugins-detection`: Determina cómo se detectan los plugins (puede ser `passive`, `mixed` o `aggressive`).
- `-u, --update`: Actualiza WPScan a la última versión.
- `-f, --force`: Forzar la exploración de la URL especificada, aunque no sea un sitio de WordPress.
- `-o, --output <format>`: Especifica el formato de salida de los resultados (puede ser `json`, `yaml` o `cli-no-colour`).

**Ejemplo de comando para enumerar plugins, temas y usuarios:**
```
wpscan --url http://example.com -e ap,u
```

Este comando escaneará el sitio web en busca de plugins y temas instalados, así como de usuarios registrados.

**Ejemplo de comando para detectar plugins de forma agresiva:**
```
wpscan --url http://example.com --plugins-detection aggressive
```

Este comando realizará un escaneo más agresivo para detectar plugins, lo que puede llevar más tiempo pero puede identificar vulnerabilidades ocultas.

**Nota:**
Asegúrate de tener permiso para escanear el sitio web antes de ejecutar WPScan, ya que podría ser considerado como un ataque no autorizado si se realiza sin autorización explícita.

Para obtener más información y opciones, puedes consultar la documentación oficial de WPScan o usar el comando `wpscan --help`.