# Tema 1
> Conocer los tres tipos de ataques que existen contra los sistemas informaticos

Ataques conta la confidencialidad, integridad y disponibilidad.


---
> Conocer los conceptos basicos de ciberseguridad y las bases del direccionanimento IP




---
> Saber que tipos de redes existen

LAN: red que interconecta maquinas dentro de un area limitada
VPN
WLAN (LAN con Wi-Fi)
...


---
> Saber como funcionan DHCP y NAT

NAT:
- Un mensaje es creado por un miembro del grupo
	- Se publica al exterior con el ID del grupo
- Si alguien responde al mensaje solo el remitente original recibe la respuesta
- Las peticiones se traducen a IPs de la red de destino
- Las respuestas se traducen a IPs de la red de origen

DHCP: protocolo que asigna direcciones IP de forma automatica y dinamica


---
> Entender el esquema de direccionamiento CIDR

CIDR es un estandar basado en bits que utiliza prefijos para mostrar direcciones IP con sus propiedades de enrutamiento, es decir, es una forma de representar multiples IPs con el mismo nombre (bloques CIDR - A.B.C.D/N).
Por ejemplo una IP con N=24 permiten hasta 256 maquinas en la red. Se reserva el 0 (propia maquina) y el 255 (todas las maquinas de la red).


---
> Entender las entidades basicas (punto de vista externo)

Una maquina esta compuesta por:
- Puertos (extremos de comunicacion): tienen servicios. El propio puerto decide que servicio de esa IP se va a usar.
- Servicios: programa que se ejecuta asociados a un puerto de red. Se ejecutan en el equipo de destino y esperan las conexiones entrantes de clientes.
- Protocolos de comunicacion: sistema de reglas que permiten a dos o mas entidades de un sistema de comunicacion transmitir informacion (TCP, UDP)


---
> Entender las entidades basicas (punto de vista interno)

Una maquina esta compuesta por:
- Usuarios:
	- Cuentas de root
	- Cuentas del sistema
	- Cuentas de servicio
- Archivos y particiones
- Programas: servicios (Windows) o Daemons (Linux) son aplicaciones en segundo plano


---
> Saber distinguir entre los distintos tipos de malware

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




---
> Conocer las diferentes amenazas que los usuarios pueden encontrarse en la actualidad

- Spam: tienen efectos potenciales por las payloads del correo (emails fradulentos / no deseados)
- Phising: mensajes cuya intencion parece legitima pero se crean con un efecto malicioso
- Hoaxes: mensajes o publicaciones con informacion falsa/ sesgada de varios tipos
- Watering hole: estrategia de ataque en la que la victima pertenece a un grupo de usuarios concreto
- Drive-by-download: sitios que descargan e instalan spyware / malware sin consentimiento
- Advanced Persistent Threat (APT): actores que se infiltran en una red y permanecen en el tiempo sin ser detectados
- OSINT: es un conjunto de datos recopilados de fuentes publicas para ser utilizados en el estudio de un objetivo


---
> Entender como se procesan las peticiones DNS

Sistema de nombres jerarquico y descentralizado para dispositivos, servicios u otros recursos conectados a cualquier red. Un servidor de nombres DNS almacena los registros DNS de un dominio.

Este sistema permite acceder a maquinas remotas mediante un nombre facil de recordar (ssiserver de las practicas para ssh).

Los dominios de nivel superior se denominan TLD (Top Level Domain):
![[Pasted image 20230318093402.png]]

Cuando se introduce una direccion no conocida por el servidor DNS, se realiza lo siguiente:
![[Pasted image 20230318093807.png]]



---
> Entender que pasa cada vez que se hace una peticion HTTP




---


# Tema 2
> Saber la diferencia entre criptografia y esteganografia

La criptografia oculta el `significado` de la informacion, mientras que la esteganografia `oculta` la informacion.


---
> Saber cuales son los objetivos principales de la criptografia

Los objetivos principales de la criptografia son:
- Confidencialidad: solo para los que conocen el metodo de descifrado podran leer
- Integridad: garantia de que los datos transmitidos estan sin modificar
- Autenticacion: verificacion de identidad de remitente y receptor (firmas)



---
> Entender como se clasifican los algoritmos de cifrado

- Cifrados segun la forma de procesas la informacion:
	- Cifrado por bloques (IDE, AES, RSA)
	- Cifrado de flujos (A5, RC4, SEAL, ...)
- Cifrados segun como se usan las claves:
	- Cifrados sin clave
	- Cifrados con clave:
		- Simetricos (clave unica por pareja)
		- Asimetrico (publica y privada para cada participante)


---
> Entender como funcionan las firmas digitales

Las firmas digitales son el resultado de una operacion criptografica que une un documento firmado a un elemento personal, el certificado digital. Los objetivos son:
- Autenticacion del origen
- Integridad del mensaje
- No repudiar (no se puede negar el contenido del mensaje)

El procedimiento de firma de mensajes es el siguiente:
- Un hash del mensaje se calcular y se cifra con clave privada del usuario
- El hash se descifra una vez recibido (con la clave publica)
- Si son iguales, el mensaje no ha sido alterado

---
> Entender como funciona la esteganografia

Se trata de una sustitucion de bits en el objeto contenedor por los correspondientes a la informacion que se va a ocultar. Se suele combinar con la criptografia, ya que si se descubre se sigue sin conocer el mensaje.


---
> Poder entender y recomendar un algoritmo de criptografia simetrica

![[Pasted image 20230318114117.png]]
Se cifra el mensaje con la clave privada y el remitente descifra el mensaje con la misma clave.

Alguno de los algoritmos de criptografia simetrica seguros son:
- AES
- IDEA
- Twofish

Una buena opcion para transmitir claves de cifrado es el algoritmo de Diffie-Hellman que hace que la computacion de una clave, desde el exterior, sea muy cara.


---
> Poder entender y recomendar un algoritmo de criptografia asimetrica

Aqui cada emisor / receptor tiene su par de claves (DK - clave de descifrado privada, EK - clave de cifrado publica, se comparte).
![[Pasted image 20230319110007.png]]


Es recomendable usar ECC (Elliptic-Curve Cryptography) aunque tambien existe la opcion de RSA.


---
> Entender la diferencia entre cifrado de disco y de ficheros

En un cifrado de disco se cifra el acceso a todos los archivos mientras que en el de fichero se cifra el contenido de este.


---
> Entender para que se usan habitualmente los algoritmos de hashing y lo que es un KDF

Se usan habitualmente para almacenar contraseñas, asegurar la identidad con la huella y firma digital y tambien para la blockchain (SHA-256 normalmente).

KDF (Key Derivation Function) es una funcion que aplica key stretching para mejorar la seguridad de una contraseña añadiendo cadenas de caracteres random e iterando mas de una vez. Algun ejemplo es bcrypt.


---
> Entender como funciona un trusted ring (GnuPG) y una CA y cuales son las diferencias entre ellas

Anillos de confianza: otros usuarios confian en los certificados (cuantos mas usuarios mas fiable sera el certificado).

CA (Autoridades de certificacion): entidades responsables de establecer la validez de un certificado (funcionan como un notario).


---
> Entender los distintos usos de los certificados digitales y el cifrado autenticado

Los certificados se usan en muchos lados:
- Personales
- Servidores / maquinas (demostrar entidades)
- Software (firma de software)
- De CA (firmar certificados que envian a otras entidades)

Se debe de asegurar la integridad de los mensajes cifrados con clave simetrica. El cifrado autenticado es el metodo preferido para garantizar integridad, autenticacion y confidencialidad.
MAC (Message Authentication Code) es un procedimiento que agrega a un mensaje un codigo que depende de una clave simetrica compartida, autenticando el mensaje y el remitente. Hay 3 formas de crear MACs:
- Basado en Hash (HMAC - recomendado)
- Basado en cifrado por bloques (CBC-MAC)
- Galois Counter Message Authentication Code-based (GMAC)

---


# Tema 3
> Saber las distintas partes que estan involucradas en la seguridad de un SO

Estas partes son:
- Aplicaciones en uso
- Usuarios
- Diseño del software
- Sistemas operativos


---
> Conocer los aspectos de seguridad involucrados en el proceso de arranque y metodos automaticos para analizar logs

Las partes involucradas en el proceso de arranque son:
- Contraseñas de arranque

Los logz se puede automatizar con logwatch.

---
> Ser capaz de determinar si los permisos de los archivos son adecuados desde el punto de vista de la seguridad

La seguridad de un SO se basa en permisos de archivos y directorios adecuados. Hay que asegurarse de que todos los archivos son propiedad de un usuario y grupo. Tambien habra que asegurarse de que no hay archivos con permisos de escritura globales. Deshabilitar sistemas de archivos no usados y los core dumps.

Un HIDS (Host-Based Intrusion Detection System) puede detectar modificaciones en archivos confidenciales.


---
> Entender la importancia de los orígenes de controles de seguridad y la automatización



---
> Saber la diferencia entre las políticas de control de acceso MAC y DAC

Tipos de control de acceso:
- DAC (Control de acceso discrecional): acceso con identidades o grupos
- MAC (Control de acceso obligatorio): niveles de integridad (IL) - MIC en Wind, un proceso no puede interactuar con otro que tiene un IL más alto


---
> Ser consciente de las políticas más seguras de actualización, gestión e instalación del software

Con Lynis estas politicas de seguridad vienen dadas.


---
> Saber de productos capaces de detectar distintos tipos de malware

Endpoint detection and response (EDR) monitoriza y responde de forma continuada para mitigar amenazas. Un EDR hace mucho mas que un antimalware.


---
> Saber cómo manejar de forma segura cuentas de Usuario y sus accesos

Alguna medida de proteccion de passwords son:
- Establecer una politica de caducidad de password
- Deshabilitar cuentas inactivas
- Implementar una politica adecuada de seguridad y administracoin de contraseñas


---
> Saber cómo usar Lynis para evaluar el nivel de seguridad de un SO Linux



---
> Ser capaz de diseñar una política de passwords efectiva

Politica de fortaleza de passwords:
- Hasheo de pass con SHA-512
- Intentos fallidos maximos
- Limitar reutilizacion de passwords
- Obligar a usar contraseñas seguras
- Modulo PAM: biblioteca para elegir como las aplicaciones autentican a los usuarios en sistemas Linux


---
> Conocer los distintos eventos de seguridad a registrar en el sistema de log de un SO

El comportamiento del usuario tambien debe ser auditado para crear un rastro de cada accion problematica:
- Usuarios estandar: alteracion de archivos, inicios de sesion, accesos no autorizados, ...
- Administradores: comandos de privilegios elevados, modificaciones de entorno de red, ...
---



# Tema 5
> Comprender el concepto de DMZ

Son zonas de red aisladas dentro de la red interna de una empresa. Se implementa con cortafuegos (perimetral). Se suelen usar dos cortafuegos para aumentar la seguridad de las redes, tanto del lado LAN como del lado de las conexion a internet.


---
> Conocer los ataques red modernos

Hoy en dia los atacantes se centrar en ataques mas centrados en el usuario, ya que la mayoria de las aplicaciones tienen buenas capas de seguridad, por ello se buscan estos puntos de ataque:
- BYOD (Bring Your Own Device): escenario en el que la empresa permite dispositivos externos
- Teletrabajo: por ejemplo conexiones con VPN salta muchas protecciones
- Aplicaciones en la nube: no podemos asegurar la seguridad de las conexiones


---
> Conocer los servicios proporcionados por CDNs

Content Delivery Network (CDN) es un servicio basado en la nube que proporciona una capa de seguridad adicional con servicios como:
- Protección anti DDoS
- Conexiones https adecuadas
- Firewall de aplicaciones web (no gratis)
- Técnicas para prevenir amenazas (spam, hotlinking o conexiones de clientes malintencionadas)


---
> Saber como enumerar los CMS

Las herramientas de identificación de CMS son:
- Wpscan
- Doopescan
- Joomscan


---
> Comprender el concepto de firewall y sus distintos tipos

Un firewall está diseñado para bloquear acceso no autorizado, pero normalmente permitiendo el tráfico saliente. Los diferentes tipos son:
- Firewalls hardware: maquinas personalizadas para maximiar el rendimiento de red
- Firewalls de software: ejecutan un programa de firewall en el PC
- Firewalls hibridos: firewalls basados en software que se ejecutan en hardware comun, pero con mayor rendimiento


---
> Ser capaz de diferenciar diseños de red seguros de los inseguros

Un diseño nada seguro sera tener un servidor unico on-premises para todas las capas de la aplicacion. Una medida que seguiria siendo insuficiente seria la de contratar un servicio en la nube Anti-DDoS, un filtro de trafo o tener conexiones seguras HTTPs.
Una solucion practica para presupuestos limitados sera contratar tanto un servicio en la nube para la seguridad como otro para alojar el servidor con su correspondiente firewall.


---
> Comprender por qué la segmentación y defensa de la red en profundidad es importante

La segmentación es algo vital puesto que si hay un fallo en la seguridad este se extendería al resto en caso de no existir segmentación de la red.


---
> Saber como enumerar puertos y servicios con escaneo activo

Para tener una enumeración rápida usaremos nmap que nos devuelve información sobre los puertos abiertos y su información en caso de existir. También podemos obtener información de servicios FTP y SSH por ejemplo.


---
> Saber como enumerar servicios HTTP y extraer información de sus archivos

Para obtener información de servicios HTTP podemos utilizar herramientas como:
- dirb para la busqueda de contenido web oculto
- dirbuster similar a dirb
- gobuster, fuerza bruta para enumeración de urls, DNS y host virtuales

También podemos escanear el robots.txt en busqueda de informacion oculta en la web. 

---
> Entender el proposito y articular las distintas técnicas de reconocimiento del MITRE ATT&CK

MITRE ATT&CK es una base de conocimientos internacional libre y accesible de tácticas y técnicas de adversarios basadas en observaciones del mundo real para asi poder protegerse ante dichos ataques.

La primera fase es la de reconocimiento (Reconnaisance) en la cual el usuario esta tratando de recopilar información ya sea de forma activa o pasiva.

Los métodos de escaneo activos son los siguientes:
- Busqueda de servicios
- Busqueda de puertos
- Busqueda de información de usuario


---
> Comprender los múltiples componentes de la infraestructura de red segura (SNI)

Los componentes principales de una SNI son:
- Firewalls de red y aplicaciones
- Dos DMZ con firewalls IPS (publico y privado)
- Dos LAN internas con firewalls IPS:
	- Interna sin información confidencial
	- Segura con toda la información sensible cifrada
- Sistema de log y monitorización

---



# Tema 6
> Entender los principales ataques XSS (tipo 1 y 2)

Reflected XXS (tipo 1): inyeccion de codigo en peticiones HTTP
Stored XXS (tipo 2): se podra acceder a la entrada de los usuarios


---
> Entender los principios de los ataques SQL Injection y CSRF

En los ataques de inyección de SQL el atacante podrá obtener acceso a la base de datos inyectando codigo en las diferentes entradas de la página, asi como en las peticiones.

Y por otro lado las Cross-Site Request Forgery (CRSF) son aquellos ataques en los que los usuarios estarán haciendo acciones sin darse cuenta o bien se estan capturando las peticiones.


---
> Entender el significado de la filosofía "pushing left"

Cuanto antes se tengan en cuenta las medidas de seguridad en el desarrollo de software más facil serán estas de arreglar en caso de un fallo en el sistema.


---
> Entender porque el uso de lenguajes no memory-safe impone más necesidades de seguridad

Esto se debe a que se pueden bloquear servicios o aplicaciones encontrando fallos de memory leaks en el codigo. La parte buena de esto es el rendimiento de la aplicacion.


---
> Entender los principios de diseño del software seguro y como se integran en la SSDLC
- Minimo privilegio
- Valores por defecto a prueba de fallos
- Mediacion completa
- Separacoin de acceso
- Confianza minima
- Economia de mecanismo
- Minimizar mecanismos comunes
- Diseño sencillo y comprensible
- Diseño abierto
- Capas (principio de separacion)
- Abstraccion
- Modularidad
- Vinculacion completa
- Diseño por iteraciones


---
> Comprender los distintos mecanismos de MFA

Los diferentes tipos de MFA son los siguientes:
- Token SMS
- Token por Email
- Token hardware como USB
- Token software (generacion de tokens dinamica)
- Telefono
- Verificacion biometrica (FaceID)


---
> Comprender el threat modeling y otros principios de diseño seguro

El thread modeling consiste en identificar amenazas potenciales para un sistema, empresa o negocio. Se necesitara un stackeholder de la aplicacion o negocio y deben aportar los riesgos que ven en el sistema. Deben de buscar cualquier riesgo como si fuesen atacantes.

Por otro lado tenemos otros principios de diseños seguros como el hecho de escribir un codigo que sea seguro evitando el uso de muchas librerias, uso de Gateways para las APIs, evitar almacenar secretos en publico, etc.


---
> Comprender la importancia del testing en la seguridad del software

Cuando pruebas las aplicaciones se ven muchos fallos que a simple vista no se podrian detectar, por ello habra que crear pruebas para la aplicacion que prueben la seguridad.


---
> Entender los requisitos de seguridad a incluir en cualquier aplicación

Los diferentes requisitos de seguridad para cualquier aplicacion son los siguientes:
- Requisitos de cifrado (Tema 2)
- Requisitos de manejo de datos
- Requisitos de autenticacion
- Requisitos de seguridad de codigo (librerias, backups, configuraciones seguras, etc)


---
> Diferenciar entre los distintos tipos de herramientas de comprobación de seguridad en la SSDLC

Las diferentes herramientas son:
- SCA (Software Composition Analysis): escaneo de codigo automatico para cumplimiento de licencias, etc
- SAST (Static Application Security Testing): prueban estructuras internas, no funcionalidad
- DAST (Dynamic Application Security Testing): evalua a base de probar errores por fuera bruta
- IAST (Interactive Application Security Testing): evalua rendimiento y detecta vulnerabilidades


---