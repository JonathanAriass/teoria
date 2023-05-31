Para ejecutar en la carpeta raiz hace falta usar sudo o tomar acceso como root.
Para ver si root tiene contraseña o no podemos ejecutar la orden: `grep ^root:[*\!]: /etc/shadow`
Si el usuario tiene \* o tiene \! quiere decir que no tiene contraseña.

Para logearse como root sin contraseña se puede ejecutar la orden: `sudo su -`

El fichero de las ordenes todo lo que tenga un `#` tiene que ser como root.

## Evaluacion del nivel de seguridad con lynis
Ejecutamos la orden: `sudo lynis audit system | ansi2html > report.html`

## Cuentas y acceso: evitar single user mode
Primero comprobamos que la cuenta de root no tenga contraseña con la siguiente orden: `# grep ^root:[*\!]: /etc/shadow`
A continuacion le ponemos contraseña a root con: `passwd root`

## Banners de advertencia
Lo que se tiene que tener en cuenta es que no se puede mostrar informacion sobre el sistema ya que para lo hackers es informacion util en caso de querer atacar una maquina, por eso se debe de cambiar los ficheros: `/etc/motd`, `/etc/issue` y `/etc/issue.net`

## Seguridad adicional para OpenSSH