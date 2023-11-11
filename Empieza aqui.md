## Instalación de herramientas

Para comenzar, necesitarás un laboratorio virtual y un sistema operativo dedicado, en este Club estaremos usando Kali Linux en VMware.

1. Puedes descargar [VMware Workstation Pro 17](https://www.vmware.com/es/products/workstation-pro/workstation-pro-evaluation.html) y [Kali Linux](https://www.kali.org/get-kali/#kali-installer-images) en estos enlaces.
![Descarga-VMware](/Documentación/Assets/VMware-descargar.jpg)
![Descarga-Kali](/Documentación/Assets/Kali-descargar.jpg)


2. Visita el siguiente [tutorial](https://youtu.be/ju4HcfOQ6tQ?si=svkqXBZmf4-x3L4L) de "Como instalar Kali Linux en VmWare paso a paso" del canal "Fr4nk Solo" para tener tu primer Laborario Virtual.

3. Una vez instalada tu primer máquina virtual, debe verse así (sin la terminal abierta):
![Kali instalado](/Documentación/Assets/Kali-instalado.png)

4. Una vez instalado, toma tu primer snapshot de tu máquina virtual en caso de querer volver a este punto. Clickea sobre el ícono con la llave inglesa color azul sobre la barra de herramientas.
![snapshot-1](/Documentación/Assets/snapshot-1.jpg)

5. Se mostrará una pantalla similar a la siguiente: 
![snapshot-2](/Documentación/Assets/snapshot-2.jpg)

6. Clickea el botón "Take Snapshot"

7. Se mostrará una nueva pantalla, en dicha pantalla guarda tu máquina virtual con el nombre de "Recien instalado" y omite la descripción. Haz click en "Take Snapshot". </br>
![snapshot-3](/Documentación/Assets/snapshot-3.png)
Nota: es posible que tu equipo se alente durante un par de segundos, es normal, en unos segundos volverá a su velocidad normal.

8. Abre la terminal, clickeando en el siguiente ícono: 
![](/Documentación/Assets/update.jpg)

9. Ejecuta el comando <code>sudo apt update</code> y presiona la tecla INTRO, cuando finalice el proceso ejecuta <code>sudo apt upgrade</code> para asegurarte de tener tu sistema actualizado.

10. Una vez finalizado el proceso, ¡Ya tienes lista tu primera máquina virtual!