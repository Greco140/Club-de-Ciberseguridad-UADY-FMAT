Información sacada de: https://invertebr4do.github.io/tratamiento-de-tty/#

<h2>Tratamiento de la TTY</h2>

Una vez obtenemos una reverse shell necesitamos estar cómodos con una **TTY** interactiva para evitar problemas, como **cerrar la conexión** sin querer o simplemente para poder **desplazarnos** con las flechas, poder usar el **tab** para el auto completado de rutas, etc. Esto es muy sencillo de lograr, simplemente debemos de hacer un tratamiento de la tty siguiendo estos pasos:

Empezamos en la reverse shell obtenida

```
script /dev/null -c bash
```

Luego de esto presionamos **ctrl_z** para suspender la shell

```
www-data@host:/$ ^Z
zsh: suspended  nc -nlvp 443
```

Ahora resetearemos la configuración de la shell que dejamos en segundo plano indicando **reset** y **xterm**

```
stty raw -echo; fg
```

```
reset xterm
```
Exportamos las variables de entorno **TERM** y **SHELL**

```
export TERM=xterm
```
Debemos hacer esto ya que a pesar de haberle indicado que queríamos una **xterm** al momento de reiniciarlo la variable de entorno **TERM** vale **dump** (Se usa esta variable para poder usar los atajos de teclado).
```
export SHELL=bash
```
Para que nuestra shell sea una bash.

Y listo, ya con estos pasos debemos tener una shell interactiva :P
