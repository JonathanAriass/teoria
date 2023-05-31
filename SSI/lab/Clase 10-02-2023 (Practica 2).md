La linea `#! /bin/bash` lo que hace es indicarle como se ejecuta el script al fichero `prepare_lab2.sh`.

Docker reutiliza codigo de las imagenes base para no tener que ocupar tanto espacio, por lo que es importante que se utilice docker para optimizar el espacio.

Algunos de los comandos de Docker:
 - `run` > create and run a new container from image
 - `exec` > execute a command in a running container
 - `rm` > remove one or more container
 - `restart` > restart one or more container

## Preparacion de lab
Para preparar un laboratorio:
 - `prepare_lab2.sh` ejecutar para crear las imagenes de los SO que se usaran
 - `build_lab2.sh` ejecutar para arrancar los contenedores
	- Una vez inicializados los contenedores se hace Ctrl+Z para parar el proceso y usar bg para que se ejecute de fondo y poder tener la terminar disponible.
	- Si quiero parar un proceso: `sudo docker stop [id]`
	- Para obtener todos los ids de proceso de docker:  `sudo docker ps -q`
	- Para parar todos los procesos de una: `sudo docker stop $(sudo docker ps -q)`
	- Ahora se borran: `sudo docker rm $(sudo docker ps -qa)`
- Ahora para conectarnos a la maquina kali:
	- `./enter_kali_lab2.sh` para conectarnos automaticamente
	- Para salir de la maquina habra que hacer Ctrl+D para que se guarde el registro de ordenes en el log

Una vez preparado todo podemos ver los puertos abiertos de las maquinas con docker ps y vemos la columna de PORTS.

En el archivo `robots.txt` se puede encontrar informacion de las URLs que no se quiere que se indexen.

## Lectura de metadatos
Con la herramienta `eixftool` podemos ver los metadatos de cualquier fichero con el comando: `exiftool -a -u -g1 [nombre_fichero]`.

## Google hacking
Podemos usar la siguiente pagina https://www.exploit-db.com/google-hacking-database para ver una lista de `Dorks` y tener una lista de posible vulnerabilidades. En mi caso elegi la categoria de password y se puede ver como muchas de las paginas desvelan contraseñas de correos, servidores, etc.

## Shodan
Haciendo una busqueda para apache vemos como hay bastantes maquinas con el puerto 21 abierto (FTP) siendo esto una vulnerabilidad grande

## Censys
Sirve para hacer escaneo de rangos de IP de forma similar a Shodan pero de forma mas estructurada.

## The Wayback Machine
Sirve para buscar el historial de paginas antiguas de cualquier sitio web. Para realizar una busqueda: `http://web.archive.org/web/*/<URL>/*`

## Descubrimiento de subdominios
Hay varias opciones:
- Knockpy: `$ python3 knockpy.py <domain>`
![[Knockpy.png]]
- dnsenum: `$dnsenum <domain>`
![[dnsenum.png]]

## Analisis de rango de IPs
Para los dominios acabados en `.com` usar https://whois.arin.net y para los acabados en `.es` usar www.nic.es.

`Zmap` es un escaner de red rapido single-packet optimizado. Su uso es el siguiente: `zmap -p80 88.151.16.0/24`.

## Inspeccoin de privacidad de la web
Para esto usaremos `Blacklight`: https://themarkup.org/blacklight que es escanea y descubre tech de tracking de usuarios en web.