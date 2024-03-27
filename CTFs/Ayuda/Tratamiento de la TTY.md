Información sacada de: https://invertebr4do.github.io/tratamiento-de-tty/#

<h2>Tratamiento de la TTY</h2>

Una vez obtenemos una reverse shell necesitamos estar cómodos con una **TTY** interactiva para evitar problemas, como **cerrar la conexión** sin querer o simplemente para poder **desplazarnos** con las flechas, poder usar el **tab** para el auto completado de rutas, etc. Esto es muy sencillo de lograr, simplemente debemos de hacer un tratamiento de la tty siguiendo estos pasos:

Empezamos en la reverse shell obtenida

```
$ script /dev/null -c bash
Script started, file is /dev/null
```

Luego de esto presionamos **ctrl_z** para suspender la shell

```
www-data@host:/$ ^Z
zsh: suspended  nc -nlvp 443
```

Ahora resetearemos la configuración de la shell que dejamos en segundo plano indicando **reset** y **xterm**

```
~$> stty raw -echo; fg
```

```
[1]  + continued  nc -nlvp 443
                              reset
reset: unknown terminal type unknown
Terminal type? xterm
```

Exportamos las variables de entorno **TERM** y **SHELL**

- `export TERM=xterm` -> Debemos hacer esto ya que a pesar de haberle indicado que queríamos una **xterm** al momento de reiniciarlo la variable de entorno **TERM** vale **dump** (Se usa esta variable para poder usar los atajos de teclado).
- `export SHELL=bash` -> Para que nuestra shell sea una bash.

```
www-data@host:/$ export TERM=xterm
www-data@host:/$ export SHELL=bash
```

Ya con esto hecho tendríamos una **TTY** full interactiva, pero falta una cosa para que sea lo más comoda posible, setear las filas y columnas, esto para poder ocupar toda nuestra pantalla ya que en este momento solo podemos usar una porción de esta

Vemos el tamaño de nuestra shell en una consola normal

```
~$> ssty size
40 123
```

Y las seteamos en la reverse shell **(en mi caso 40 filas y 123 columnas)**

```
www-data@host:/$ stty rows 40 columns 123
```

Y listo!, ya podemos disfrutar de una shell totalmente interactiva y muy comoda para continuar rompiendo