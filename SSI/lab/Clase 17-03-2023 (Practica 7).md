Para acceder a la maquina virtual desde el PC host via ssh tenemos que ejecutar el siguiente comando: `ssh ariass@192.168.56.10` y usar la pass: `test123...`

## Filtrado de paquetes
![[Pasted image 20230317095139.png]]
#IMPORTANTE: recordar recargar en firewall en la pestaña de options>reload firewalld

AHora ya no nos podemos conectar via ssh desde el PC host.
Ahora vamos a bloquear todas las conexiones a 192.168.56.0/24:
![[Pasted image 20230317100638.png]]
*No seleccionar la opcion de elemento si se quiere eliminar todas las conexiones.*
Acordarse de hacer reload del firewall en Options > Reload Firewall.

Ahora podemos comprobar como desde la IP 192.168.56.1 (host-only = maquina madre) no podemos acceder a la direccion IP 192.168.56.10 a traves de ssh.

Entramos en la maquina de firefox con ./enter_firefox_client y ejecutamos el ifconfig y vemos como tenemos que la IP en eth1 es: 192.168.72.12
![[Pasted image 20230317101355.png]]

