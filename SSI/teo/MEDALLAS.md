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