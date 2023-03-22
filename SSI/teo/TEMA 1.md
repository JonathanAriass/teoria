Un sistema informático es seguro cuando responde según lo previsto y ademas ofrece:
- Confidencialidad: datos privados son solo visibles para el usuario propietario
- Integridad: los datos solo podran ser modificados por el usuario propietario
- Disponibilidad: los datos son siempre accesibles por el usuario propietario

## Ataques contra la confidencialidad
- Acceso no autorizado al sistema (`suplantacion`)
- Acceso a la comunicacion no autorizado (`sniffing`)
- Acceso fisico a un ordenador (`instalacion malware`)
- Acceso logico o fisico a copias de seguridad
- Acesso a datos restringido o privado

## Ataques contra la integridad
Los mismos que para la confidencialidad pero se limitan a acceder a datos/software. Una vez se tiene el control se puede introducir datos falsos o maliciosos, dañar o corromper datos, asi como modificarlos.
Comprometer la integridad en canales de comunicacion se hace mediantes ataques `Attacker-in-the-Middle` (AitM).


## Ataques contra la disponibilidad
Toda forma de ataque que tiene como objetivo negar o reducir la capacidad de un sistema informatico.


# Terminología básica
- Amenazas
	- Personas (no autorizados)
	- Software (malware)
	- Catastrofe natural
- Vulnerabilidades
	- El payload es el codigo que realiza la accion maliciosa de un ataque
- Exploits
	- Para lanzar ataques de diferentes tipos
- CVE: informacion de vulnerabilidad de seguridad conocidas publicamente del software
- Riesgo = Amenaza x Vulnerabilidad x Valor del objetivo
- Ataque
	- Motivo
	- Metodo (exploit usado)
	- Oportunidad
- Daños
	- Economicos, tecnico, moral, de imagen...
- Control o contramedidad: mecanismo de proteccion ante riesgos
	- Prevencion de ataques
	- Mitigacion de ataques
	- Deteccion de ataques
	- Recuperacion de ataques
- Bug bounty: es una oferta que se crea para buscar fallas de seguridad en un sistema o software

Clasificacion de tipo de atacantes:
- Script kiddies o n00bs (skiddies)
- Pentesters
- Crackers

Clasificacion de equipos de seguridad:
- Red team: contratado para actuar como atacantes reales
- Blue team: analiza la seguridad de los sistemas
- Purple team: maximiza la efectividad de ambos equipos


# Malware
Software para obtener accesos no autorizados. Algunos efectos comunes son:
- Causar fallos
- Robar informacion
- Botnets
- Insertar anuncios
- Extorsion

Las tecnicas para evadir malware son:
- Identificar (fingerprint) su entorno cuando se ejecuta
- Confundir a los metodos de deteccion de las herramientas de seguridad
- Evasion basada en el tiempo (en el arranque se es mas vulnerable)
- Ofuscacion de datos internos
- Uso de firmas

Los malwares se clasifican segun sus efectos en:
- Propagadores
	- Virus
		- Causan cualquier tipo de daño
		- Tienen un programa host que lo lanza
	- Gusanos (worms)
		- Gran capacidad de replicacion agresiva
		- Se replica para aumentar el uso de recursos
		- No necesitan otro software como los virus
- Wabbits
	- Denegacion de servicios, que se replica continuamente para agotar los recursos
	- Gusanos sin capacidad de propagacion
	- Bombas fork
- Troyanos
	- Malware disfrazado de software legitimo que por lo general implementan una funcionalidad legitima pero viene con efectos nocivos ocultos.
- Robo de informacion
	- Spyware
		- Obtienen informacion sobre individuos, ordenadores u organizaciones sin su consetimiento, llamados stealers
	- Keyloggers
		- Roba informacion monitorizando pulsaciones de teclado, movimientos del ratos, capturas de pantalla, ...
- Anuncion molestos / maliciosos
	-  Adware
		- Software que muestran anuncios que pueden replicar a anuncios reales pero que tienen un payload
	- Browsers hijackers
		- Bloquean o dificultan el uso del browser para obtener beneficios economicos o posicionamiento en busquedas
- Ransomware
	- Bloquean el uso del ordenador y de los datos. Algun ejemplo conocido son los cryptolockers que cifran los archivos y se necesita pagar un rescate para obtener la clave que descrifre los archivos
- Rootkit
	- Software no solicitado que se instala con privilegios de root
	- Suele robar informacion o crear un backdoor
- Rogue software
	- Programas que dicen implementar unas funcionalidades que realmente no implementan, como por ejemplo, antivirus falsos, herramientas de limpieza, optimizadores de SO, ...

El `Crimeware` es un software especializado en cometer delitos (robo de datos, financiero, ...) que se pueden replicar a si mismos como los worms.

Las `Backdoor` son metodos alternativos no oficiales para acceder a un ordenador o software.


# Como comunicarse con las maquinas objetivo
Las maquinas tienen IPs que es lo que la distingue del resto de maquinas en una red:
- LAN: una red que interconecta maquinas dentro de un area limitada
	- Sin la ayuda de otras maquinas las maquinas no se podran comunicar con el exterior

Las direcciones IPv4 (32 bits) se han agotado y se esta transicionando a IPv6 (128 bits).

`Classless Inter-Domain Routing (CIDR)` es un estandar basado en bits que utiliza prefijos para mostrar direcciones IP con sus propiedades de enrutamiento, agrupando en bloques de direcciones (forma de representar varias IPs con un unico identificador).

Los grupos se denominan `bloques CIDR` y en su version IPv4 se usa una sintaxis similar a las direcciones IP: A.B.C.D/N
Un bloque /20 es un bloque CIDR con un prefijo de 20 bits no especificado.
![[CIDR.png]]

Las LAN pequeñas y grandes (N /28 a /24 hasta 256 maquinas en una red) son las mas usadas actualmente. Las /31 se usan para enlaces entre dispositivos.

La primera direccoin de una subred (todos los bits de host a 0) se reserva para referirse a la propia red: 192.168.35.0

Por otro lado si ponemos todos los bits de host a 1 tenemos una direccion de broadcast para todas las maquinas de la red: 192.168.35.255

Por lo tanto se reduce el numero de direcciones disponibles en 2.


# Redes de maquinas
En una red de maqiunas, puedes comunicarte con todos los dispositivos que tengan una IP compatible con la tuya (encaja en el mismo CIDR).
Se pueden comunicar maquinas en diferentes redes mediante los bridges o gateways de la redes.

Normalmente un router asigna una IP privada a cada dispositivo conectado a el (formando la LAN privada). Y envia todas las conexiones fuera de su LAN privada a traves de una IP unica:
- Valida en la red que esta al otro lado del router
- Traduce IPs privadas a unas que se puedan usar en la otra red
- La IP traducida es publica y valida en Internet
- Se conoce como NAT (Network Address Translation)

Con el concepto de NAT se dice:
- Un mensaje es creado por un miembro del grupo
	- Se publica al exterior con el ID del grupo
- Si alguien responde al mensaje solo el remitente original recibe la respuesta
- Las peticiones se traducen a IPs de la red de destino
- Las respuestas se traducen a IPs de la red de origen
![[NAT.png]]

DHCP es el protocolo que asigna direcciones IP de forma automatica y dinamica, haciendo que un dispositivo no tenga la misma IP todo le tiempo.

Una Gateway permite la comunicacion entre diferentes redes.


## DNS (Domain Name System)
Sistema de nombres jerarquico y descentralizado para dispositivos, servicios u otros recursos conectados a cualquier red. Un servidor de nombres DNS almacena los registros DNS de un dominio.

Este sistema permite acceder a maquinas remotas mediante un nombre facil de recordar (ssiserver de las practicas para ssh).

Los dominios de nivel superior se denominan TLD (Top Level Domain):
![[Pasted image 20230318093402.png]]

Cuando se introduce una direccion no conocida por el servidor DNS, se realiza lo siguiente:
![[Pasted image 20230318093807.png]]


## Maquinas como objetivo
Hay 65536 puertos distintos en una maquina, pudiendo ofrecer cada uno de ellos un servicio distinto.

Un servicio es un programa que se ejecuta asociado a un puerto de red (son procesos). Se ejecutan en el equipo destino y esperan las conexiones entrantes de clientes.

Protocolo de comunicaciones: sistema de reglas que permiten a dos o mas entidades de un sistema de comunicaciones transmitir informacion (TCP, UDP, ...).

Para hacer un reconocimiento de la red haremos uso de la herramienta Nmap, determinando cuantas maquinas son capaces de recibir trafico.

Los puertos son extremos de comunicacion:
- Identifican un proceso o servicio de red
- Un puerto siempre esta asociado a una IP y al protocolo de comunicacion
- Los protocolos mas comunes son TCP (Transmission Control Protocol) y UDP (User Datagram Protocol)


## Cuando los usuarios son el objetivo
- Spam: tienen efectos potenciales por las payloads del correo (emails fradulentos / no deseados)
- Phising: mensajes cuya intencion parece legitima pero se crean con un efecto malicioso
- Hoaxes: mensajes o publicaciones con informacion falsa/ sesgada de varios tipos
- Watering hole: estrategia de ataque en la que la victima pertenece a un grupo de usuarios concreto
- Drive-by-download: sitios que descargan e instalan spyware / malware sin consentimiento
- Advanced Persistent Threat (APT): actores que se infiltran en una red y permanecen en el tiempo sin ser detectados
- OSINT: es un conjunto de datos recopilados de fuentes publicas para ser utilizados en el estudio de un objetivo
