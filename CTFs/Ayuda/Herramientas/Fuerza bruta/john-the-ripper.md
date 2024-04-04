
<h1>¿Qué es John the Ripper?</h1>

John the Ripper es una herramienta de línea de comandos utilizada para la auditoría de contraseñas. Es capaz de descifrar contraseñas cifradas mediante fuerza bruta, ataques de diccionario y otros métodos, lo que la hace muy útil para evaluar la seguridad de las contraseñas en sistemas informáticos.

**Uso básico:**

El uso básico de John the Ripper generalmente implica ejecutarlo con una serie de opciones y argumentos para especificar qué tipo de ataque realizar y cómo se deben tratar las contraseñas. Aquí tienes un ejemplo básico:

```
john <archivo_de_contraseñas>
```

Donde `<archivo_de_contraseñas>` es el archivo que contiene las contraseñas que deseas descifrar.

**Opciones comunes:**

- `-w <diccionario>`: Especifica un diccionario de palabras para realizar un ataque de diccionario.
- `-mask <máscara>`: Especifica una máscara para realizar un ataque de fuerza bruta.
- `-rules`: Permite aplicar reglas para modificar automáticamente las palabras del diccionario.
- `-format=<formato>`: Especifica el formato de las contraseñas (ejemplo: `MD5`, `SHA-256`, `bcrypt`, etc.).
- `-show`: Muestra las contraseñas descifradas una vez completado el proceso de descifrado.
- `-pot=<archivo>`: Especifica un archivo para almacenar las contraseñas descifradas.

**Ejemplo de comando para realizar un ataque de diccionario:**

```
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Este comando utilizará el diccionario `rockyou.txt` para realizar un ataque de diccionario contra las contraseñas contenidas en el archivo `hashes.txt`.

La opción `-mask` en John the Ripper permite especificar una máscara que define el patrón de las contraseñas que se probarán durante un ataque de fuerza bruta. Una máscara es una cadena de caracteres que representa la estructura de la contraseña que estás intentando descifrar, donde ciertos caracteres de la máscara pueden ser sustituidos por caracteres específicos que representan los posibles valores que pueden aparecer en esa posición de la contraseña.

Aquí tienes una descripción de los caracteres utilizados en una máscara:

- `?l`: Representa una letra minúscula (a-z).
- `?u`: Representa una letra mayúscula (A-Z).
- `?d`: Representa un dígito (0-9).
- `?s`: Representa un símbolo.
- `?a`: Representa cualquier carácter imprimible.
- `?h`: Representa un carácter hexadecimal (0-9, a-f).
- `?b`: Representa un espacio en blanco.

Por ejemplo, si deseas realizar un ataque de fuerza bruta contra contraseñas que consisten en tres letras minúsculas seguidas de tres dígitos, la máscara sería `?l?l?l?d?d?d`.

**Ejemplo de comando para realizar un ataque de fuerza bruta:**

```
john --mask='?l?l?l?d?d?d' hashes.txt
```

Este comando utilizará una máscara para probar todas las combinaciones posibles de tres letras minúsculas seguidas de tres dígitos contra las contraseñas contenidas en el archivo `hashes.txt`.

Para obtener más información y opciones, puedes consultar la documentación oficial de John the Ripper o utilizar el comando `john --help`.