## Conceptos de red
En internet los protocolos mas importantes son:
* IP (Internet protocol)
* TCP (Transmission control protocol)

## Firewalls
Diseño para bloquear acceso no autorizado, pero normalmente permitiendo el trafico saliente.
Los firewalls puede ser de:
* Los **firewalls hardware** son maquinas personalizadas para maximizar el rendimiento de la red
* Los **firewalls hibridos** son firewalls basados en software que se ejecutan en hardware de PC
* Los **firewalls de software** solo ejecunta un programa de firewall en su PC

### Firewalls: Packet-Filtering (PF)
Examinan informacion de los paquetes como: direccion de origen y destino, protocolo y puerto de destino.
Se examina paquete por paquete y se pueden descartar si no cumplen con las reglas.

### Firewalls: Stateful packet inspection(SPI)
Son firewalls de filtrado de paquetes dinamicos con una tabla que rastrea todas las conexiones abiertas, en caso de exito se aceptan los paquetes sin mas analisis.

### Firewalls: Proxy
![[ProxyFirewall.png]]

### Firewalls: Next-generation firewalls (NGFW)
Firewalls que usan un enfoque de varias capas, combinando diversas caracteristicas de firewalls empresariales tradicionales con funcionalidades mas potentes.

## Reglas de un firewall
Una serie de reglas de filtrado indican que tipos de comunicaciones son:
* Permitidas (ALLOW)
* Rechazadas (REJECT)
* Descartadas (DROP)

## Host firewalls vs Perimetral firewalls
En el caso de los host firewall se da un enfoque de lista de permitidos para el trafico entrante.
En el caso de los perimetral firewalls se pueden restringir conexiones entre diferentes redes o zonas (normalmente un equipo cuya unica funcion es la de firewall).


## Demilitarized zones (DMZs)
Son zonas de red aisladas dentro de la red interna de una empresa. Deben contenter todos los recursos que sean accesibles desde internet. Se usan dos cortafuegos para aumentar la seguridad de sus redes:
![[DMZs.png]]

## Ataques de red
Hoy en dia los atacantes no se centrar en los permitros de la red para atacar, sino que se centran en los endpoints, es decir, los usuarios. Los escenarios mas comunes de ataques son:
* BYOD (Bring Your Own Device)
* Teletrabajo
* Aplicaciones en la nube (inseguridad de conexiones)

Una forma de tratar esto sera haciendo uso del modelo Zero Trust que asume que habra dispositivos que no seran de confianza accediendo a la red. Solo admite dispositivos que cumples unas condiciones (comprobacion continua de seguridad).
Otras tecnicas sera la del control del acceso remoto que tendran que ser securizadas con conexiones VPN y factor de doble autenticacion.

## Secure Network Infrastructure (SNI)
![[SNI.png]]
Componentes principales:
* **Configuracion de base segura para todos los servidores** con un framework de seguridad (ISO 27001)
* **Firewall de red y de aplicaciones (WAF) externo**
* **Dos DMZ con 2 firewall SPI/NGFW**: una publica y otra privada
* **Dos LAN internas con doble cortafuegos SPI/NGFW**:
	* La LAN interna: sin informacion confidencial
	* La LAN segura: servidores con informacion cifrada y confidencial
* **Una politica comun de ubicacion de los puertos de servicios**

Hay que tener en cuenta que la configuracion de los firewall es critica.

**Content Delivery Network (CDN)** es un servicio basado en la nube que proporciona una capa de seguridad adicional como proteccion contra DDoS avanzada, firewall de aplicaciones web, etc.

### SNI: DMZ publica
Es accesible desde el exterior, pero no todo lo que hay dentro de ella:
* Proxies inversos + WAF: las unicas maquinas visibles tras el cortafuegos perimetral
* Honeypot: captura intentos de ataques de usuarios bloqueando sus IPs

### SNI: LAN segura
Los servidores ubicados en la LAN segura implementa un nivel adicional de seguridad al almacenar solo informacion cifrada.

### SNI: LAN de administracion
La LAN de administracion protegida esta compuesta por:
* Intrusion Detection/Prevention System(s) (IDS/IPS)
* Security Information and Event Managemente (SIEM)
* Domain Name Services (DNS): hay que intentar dirigir las consultas de DNS publicas al DNS del IPS
* Servidor de tiempo: permite hacer un analisis correcto de la informacion del log
* Servidores de log centralizado (syslog)

El protocolo de autenticacion Kerberos es uno de los mas seguros 

#### IDS/IPS
![[IDSvsIPS.png]]




## Pentesting de red
### The Mitre Atta&ck
Base de conocimientos internacional libre y accesible de tacticas y tecnicas de adversarios basadas en observaciones del mundo real. Divide las tacticas y tecnicas en 14 etapas.
Solo veremos la primera que es Reconociemiento (Reconnaisance).

## TA0043. Reconnaisance
El adversario esta tratando de recopilar informacion.

## T1595: Active Scanning
El adversario sondea la infraestructura de la victima a traves del trafico de red. Una de las herramientas mas populares para hacer escaneo activo es Nmap.

Este tipo de escaneo nos da informacion sobre puertos abiertos del sistema, servicios que se ejecutan e informacion extendida de dichos servicios.
Un ejemplo de escaneo rapido puede ser: `nmap --top-ports 20 --open`
Dependiendo de las flags que se le aporte a nmap el escaneo sera mas o menos lento.

En el caso de escaneo a servicios web que tiene como objetivo los servicios HTTP en ejecucion tenemos las siguientes herramientas:
- **Proxy Burp** para una inspeccion detallada de peticiones y respuestas HTTP
- Herramientas de enumeracion de directorios HTTP:
	- dirb: busqueda de contenido web oculto (/admin, /login, /debug, /auth, ...)
	- dirbuster
	- Gobuster: herramienta de fuerza bruta para enumerar URLs, DNS, host virtuales
- Herramientas de identificacion de CMS:
	- Wpscan
	- Doopescan
	- Joomscan

Tambien es importante analizar el codigo fuente de la web en busqueda de informacion imporante y util como comentarios con tencologias que se usan, pares de usuario/contraseña, etc.

Los listados de directorios son problemas de configuracion serios e indamisibles.


## Recopilando informacion tecnica y personal
Los mas importantes podemos decir que son>
- **T1592. Gather Victim Host Information**
- **T1590. Gather Victim Network Information**
- **T1589. Gather Victim Identity Information**
- **T1591. Gather Victim Org Information**

En el caso de los dos primeros hay un conjunto de protocolos que se pueden usar para obtener informacoin acerca de redes y host como:
- DNS: con herramientas como dig
- SMB: con herramientas como Enum4Linux
- SNMP: con herramientas como SNMPWalk examina para localizar vulnerabilidades SNPM (Simple Network Management Protocol)

En el caso de los T1589 y T1591 tenemos que el objetivo es averigar nombres de usuario validos. Las imagenes llevan metadatos como lugar y fecha de creacion, tipo de camara, etc.