<h1>Wfuzz</h1>

<h2>¿Qué es wfuzz?</h2>

WFuzz es una herramienta y biblioteca de fuzzer de seguridad. Está diseñada para ayudar en la evaluación de aplicaciones web mediante la búsqueda de subdominios y virtual hosting.

<h2>Uso básico:</h2>

El comando básico de wfuzz sigue la siguiente estructura:

`wfuzz [opciones] -u URL`

Donde:
- `[opciones]`: son los diferentes parámetros y configuraciones que puedes ajustar según tus necesidades.
- `-u URL`: es la URL de la aplicación web que deseas analizar. La palabra `FUZZ` en la URL se utiliza como marcador para que wfuzz reemplace este marcador con las palabras de una lista de palabras.

<h2>Ejemplo de comando para rutas dentro del dominio:</h2>

```
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -u http://10.10.10.10/FUZZ
```

- `-c`: muestra la salida en un formato limpio y legible.
- `--hc 404`: ignora las respuestas HTTP con código de estado 404 (no encontrado).
- `-t 200`: establece el número de hilos.
- `-w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt`: especifica la ruta de la lista de palabras que wfuzz utilizará para realizar la fuzzing. Puedes usar diferentes listas.
- `-u http://10.10.10.10/FUZZ.php`: aquí es donde se coloca la URL objetivo. La palabra `FUZZ` será reemplazada por las palabras de la lista de palabras durante la fuzzing.

Con este comando, wfuzz intentará acceder a diferentes ubicaciones en la URL proporcionada, reemplazando la palabra `FUZZ` con las palabras de la lista de palabras especificada. Esto puede ayudar a identificar puntos débiles, como directorios no protegidos o archivos sensibles que puedan estar expuestos.


**Nota:**
También se puede buscar después de la palabra FUZZ como en: 

```
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -u http://10.10.10.10/FUZZ.php
```

Lo que hará es realizar fuzzing en URLs que sigan el patrón `http://10.10.10.10/FUZZ.php`, donde `FUZZ` será reemplazado por las palabras de la lista de palabras especificada. Esto es útil para buscar posibles nombres de archivos o rutas en la URL.

<h2>Ejemplo de comando para subdominios:</h2>

```
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -u https://nunchucks.htb -H "Host: FUZZ.nunchucks.htb"
```` 
Lo que hará es realizar fuzzing en subdominios de `nunchucks.htb`, donde `FUZZ` será reemplazado por las palabras de la lista de palabras especificada. Esto puede ayudar a identificar subdominios potencialmente vulnerables o no descubiertos.

Otro ejemplo:

```
wfuzz -c --hc 404 --hl 546 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -u https://nunchucks.htb -H "Host: FUZZ.nunchucks.htb"
```
La única diferencia es que ocultará los resultados que tengan 546 líneas, en esta máquina de htb es útil ya que muchas mostraban la misma cantidad de líneas y nos interesa ver cual tiene diferente cantidad de líneas.

En caso de necesitar ayuda, usar el comando `wfuzz -help`