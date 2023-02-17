## USUARIOS Y CONTRASEÑAS
Para crear un usuario se podra usar:
```shell
sudo adduser <username>

%%Para añadir el usuario al grupo sudo y poder tener privilegios sudo.%%
sudo usermod -aG sudo <username> 
```

Para ver los usuarios que hay creados en el sistema que pueden usar el bash:
```bash
cat /etc/passwd | grep bash
```
Para cambiar la contraseña de un usuario usar el comando `passwd`.

## SSH
Para ver si el servidor ssh esta arrancado:
```shell
sudo service ssh status
```

Con ifconfig podemos ver las configuraciones:
* 10.0.2.15 (NAT)
* 192.168.56.10 (Host-only)
Nos conectamos con mobaXTerm con ssh mediante el puerto 192.168.56.10 con el usuario UO.

Ahora probamos con PS (PowerShell):
```powershell
ssh uo...@localhost -p 2222
```
Aceptamos el fingerprint y metemos la password del usuario para establecer la conexion. Para cerrar la conexion es importante hacer Ctrl + D para que se guarden correctamente los datos de la sesion. El fichero .bash_history guarda los comandos hechos en el momento de hacer logout.

Para cambiar de usuario ejecutamos el comando:
```shell
su - <usuario>
```
Para buscar comandos ejecutados pasados podemos hacer Ctrl + R para poder buscar mediante input.

Para poder ejecutar ciertas aplicaciones X habra que darle permisos mediante el siguiente comando:
```shell
ssh uo283586@localhost -X
```
!RECORDATORIO!: siempre salir con Ctrl + D para hacer logout de manera correcta.


## INSTALACION DE FIREWALL
Para ver el estado del firewall habra que ejecutar el comando:
```shell
sudo ufw status
```
Para habilitar el firewall para un servicio ejecutar los siguientes comandos:
```shell
sudo ufw allow ssh
sudo ufw enable
```
Y ahora habra que comprobar que los puertos son los correctos.

Ahora descargaremos con wget (protocolo http):
```shell
sudo wget -O - https://packages.cisofy.com/keys/cisofy-software-public.key | sudo apt-key add -
```
Le estamos diciendo al paquete apt que añada una clave que se le pasa a traves del pipe.

El siguiente comando:
```shell
echo "deb https://packages.cisofy.com/community/lynis/deb/ stable main" | sudo tee
/etc/apt/sources.list.d/cisofy-lynis.list
```
El tee lo que guarda es el texto en el fichero pasado como argumento.

El software Lynis sirve para hacer escaneos sobre el estado de seguridad de una maquina. Para hacer una evaluacion del sistema ejecutar el siguiente comando:
```shell
lynis audit system > <output_filename>
```
Una solucion para aquellos visores que no tienen color sera la de instalar el paquete `kbtin` que incluye la herramienta `ansi2html` que mantiene el formato de la salida con colores y formatos:
```shell
sudo lynis audit system | ansi2html > report.html
```
Y para abrir el fichero podemos hacer uso de firefox con comando: `firefox report.html`

## ANALISIS DE MAQUINAS EXTERNAS
Ahora estudiemos como estan otras maquinas externas a traves del nmap:
```shell
nmap [scan type] [options] {target}
```
Las diferencias entre el ping y el nmap son muchas siendo una de ellas que nmap te muestra los puertos abiertos de una maquina.


## DETECCION DE MALWARE
Veamos ahora software para la busqueda de malware en nuestro sistema:
* chkrootkit: comprueba que el sistema no este infectado con rootkit que es un malware que busca fallas en el sistema y asi darse acceso no autorizado. IMPORTANTE USAR SUDO (root). Se encontro que hay una serie de archivos y directorios sospechosos como paquetes o archivos de python.
* rkhunter: comprueba tambien la existencia de rootkits en el sistema y ademas busca backdoors, sniffers y exploits, pero ademas nos da la opcion de enviar alertas por correo. Este programa nos hace un estudio mas profundo del sistema (ejecutar sudo rkhunter -c).
* clamav: es un antivirus que es capaz de detectar muchos tipos de malware. Habra que actualizar las firmas del software antimalware con el siguiente comando: `sudo freshclam`. Esto se puede quejar de que hay otro proceso bloqueando la escritura, para ello: `sudo service clamav-freshclam stop` y despues volver a ejecutar el comando. Y para escanear al directorio: `sudo clamscan -r -i<DIRECTORY>`.

Tambien hay mas opciones como Virustotal que se encarga de analizar ficheros, ejecutables, URLs, IPs, etc. Es un servicio en linea (https://www.virustotal.com/gui/home/upload).

Hay otra herramienta que estudia los sitios webs, Google Safe Browsing (https://transparencyreport.google.com/safe-browsing/search).

Una forma de analizar sitios webs es atraves de las herramientas de desarrollador del navegador. Si en un get nos devuelve informacion excesiva en la cabecera, como por ejemplo el sistema operativo del servidor podemos hacer uso de las listas CVE para buscar vulnerabilidades en el sistema (https://cve.mitre.org/ y https://www.cvedetails.com/).

## ANALISIS DE RED
Si necesitas saber los paquetes que se envian en tu red usar la herramienta tcptraceroute (`sudo apt install tcptraceroute`). Por ejemplo uso seria: `tcptracerout www.uniovi.es`

Si quieres preguntarle al servidor DNS de tu maquina cualquier informacion de cualquier nombre de dominio remoto usa el comando `dig`:
* Obtener una ip a traves de una DNS: `dig www.facebook.com +short` --> 157.240.21.35
* Revese DNS lookup (con una IP obtener DNS): `dig -x 157.240.21.35`