
<h1>¿Qué es Evil-WinRM?</h1>
Evil-WinRM es una herramienta de código abierto diseñada para facilitar la ejecución de comandos de forma remota en sistemas Windows mediante el Protocolo de Administración Remota de Windows (WinRM). Permite a los pentesters y administradores de sistemas realizar tareas de administración remota en entornos Windows de manera más eficiente. Aquí tienes cómo usar Evil-WinRM:

**Uso básico:**

1. Abre tu terminal.

2. Ejecuta el siguiente comando para iniciar una sesión interactiva con un host remoto:

```
evil-winrm -i <IP_del_host> -u <usuario> -p <contraseña>
```

Donde:
- `<IP_del_host>` es la dirección IP del host remoto.
- `<usuario>` es el nombre de usuario para iniciar sesión en el host remoto.
- `<contraseña>` es la contraseña correspondiente al usuario.

3. Una vez que ingreses el comando, Evil-WinRM intentará establecer una conexión con el host remoto utilizando las credenciales proporcionadas.

4. Si las credenciales son correctas y WinRM está habilitado en el host remoto, se iniciará una sesión interactiva.

5. Una vez dentro de la sesión interactiva, puedes ejecutar comandos de PowerShell de forma remota en el host remoto.

**Opciones comunes:**

- `-i`: Inicia una sesión interactiva con el host remoto.
- `-s`: Inicia una sesión no interactiva (una vez ejecutado el comando, finaliza).
- `-c`: Especifica el comando a ejecutar en el host remoto en lugar de iniciar una sesión interactiva.
- `-u`: Especifica el nombre de usuario para iniciar sesión en el host remoto.
- `-p`: Especifica la contraseña correspondiente al usuario.
- `-H`: Especifica la dirección IP del host remoto.
- `-P`: Especifica el puerto del servicio WinRM en el host remoto (por defecto es el puerto 5985).

**Ejemplo de uso:**

```
evil-winrm -i 192.168.1.100 -u administrator -p Password123
```

Este comando iniciará una sesión interactiva con el host remoto en la dirección IP `192.168.1.100`, utilizando el nombre de usuario `administrator` y la contraseña `Password123`.

Una vez dentro de la sesión interactiva, puedes ejecutar comandos de PowerShell en el host remoto como si estuvieras trabajando directamente en él.

Recuerda que es importante utilizar Evil-WinRM de manera ética y legal, y solo en sistemas en los que tengas permiso para hacerlo. El uso indebido de esta herramienta puede tener consecuencias legales graves.