La homogeneidad en el uso de SO puede ser una vulnerabilidad, ya que si se explota uno el resto tambien. Y la diversidad introduce complejidad en el mantenimiento.

Hay funcionalidades que se implementaron sin tener en cuenta la seguridad como por ejemplo el arranque  / ejecucion desde dispositivos externos o clientes de e-mail vulnerables a ejecutar codigo JS malicioso.

Los usuarios pueden ser la mayor amenaza para la seguridad de una organizacion ya se consciente o inconscientemente. Algunas de las contramedidas a los usuarios son:
- Formacion
- Mejorar la seguridad del SO
- Crear un Sistema de Gestion de Seguridad de la Informacion (SGSI)

# Hardening de SO
## Seguridad en el proceso de arranque
Las contraseñas de arranque evitan que usuarios no autorizados con acceso fisico al sistema obtengan privilegios de root.

Los sistemas de archivos criticos deben separarse en particiones distintas.
Algunos SO permiten marcar particiones con propiedades de seguridad (Linux con nodev, nosuid, noexec).

Para evitar la ejecucion de software desde directorios temporales seria bueno montar /tmp en una particion separada con las opciones nodev, nosuid y noexec habilitadas.

Seria importante cifrar el archivo de intercambio o particion para evitar fugas del espacio swap.
Las vulnerabilidades de modulos de kernel se evitan en gran medida instalando solo aquellos que sean necesarios.

## Log y auditoria
Tener una configuracoin de auditoria adecuada implica:
- Administracion del log del sistema
- Administracion del tamaño del log

El comportamiento del usuario tambien debe ser auditado para crear un rastro de cada accion problematica:
- Usuarios estandar: alteracion de archivos, inicios de sesion, accesos no autorizados, ...
- Administradores: comandos de privilegios elevados, modificaciones de entorno de red, ...

La mayoria de equipos en infraestructuras seguras no mantienen logs locales, se envian a un servidor de log centrales. El servicio rsyslog normalmente implementa esto en Linux.

# Hardening de servicios / software
Es imporante:
- Mantener el software actualizado
- Activar el firmado criptografico de paquetes
- Ejecutar cuanto menos software posible mejor

Gestion de software importante:
- Habilitar la programacin de tareas
- Habilitar servicios de sincronizacion de hora (NTP)
- Deshabilitar compiladores (evitamos compilacion de malware en un servidor)

Tipos de control de acceso:
- DAC (Control de acceso discrecional): acceso con identidades o grupos
- MAC (Control de acceso obligatorio): niveles de integridad (IL) - MIC en Wind

Hay que comprobarse periodicamente los programas instalados para buscar malware y rootkits.

Endpoint detection and response (EDR) monitoriza y responde de forma continuada para mitigar amenazas. Un EDR hace mucho mas que un antimalware.

# Usuarios
Hay que minimizar el numero de usuarios que puedan acceder de forma local o remota a la maquina. Se debe de reducir el numero de sudoers al minimo o a 0.

Se debe habilitar Multi-Factor Authentication (MFA) en servicios de acceso critico.
La forma mas facil de obtener acceso no autorizado a un sistema Linux es arrancar el servidor en single user mode.

Hay que tener en cuenta los permisos de los archivos, el mejor umask 027 y para root  umask 077. En Linux, esto se consigue incluyendo en /etc/profile y en /etc/bash.bashrc: umask 027

Evitar poner informacion en banners de inicio de sesion sobre el sitema como la version del kernel o el SO usado.

Es mejor deshabilitar el logeo directo como root, es mejor usar MFA.


# Gestion de passwords de usuario
En linux las contraseñas se guardaran en /etc/passwd y /etc/shadow.

Alguna medida de proteccion de passwords son:
- Establecer una politica de caducidad de password
- Deshabilitar cuentas inactivas
- Implementar una politica adecuada de seguridad y administracoin de contraseñas

Politica de fortaleza de passwords:
- Hasheo de pass con SHA-512
- Intentos fallidos maximos
- Limitar reutilizacion de passwords
- Obligar a usar contraseñas seguras
- Modulo PAM: biblioteca para elegir como las aplicaciones autentican a los usuarios en sistemas Linux


# Archivos
La seguridad de un SO se basa en permisos de archivos y directorios adecuados. Hay que asegurarse de que todos los archivos son propiedad de un usuario y grupo. Tambien habra que asegurarse de que no hay archivos con permisos de escritura globales. Deshabilitar sistemas de archivos no usados y los core dumps.

Un HIDS (Host-Based Intrusion Detection System) puede detectar modificaciones en archivos confidenciales.

# Procedimientos de hardening y evaluacion de seguridad
Hay que exigir unos requisitos muy fuertes a las listas de controles de seguridad que usemos:
- Validas
- Completas
- Correctamente estructurado

Si queremos evaluar la seguridad del sistema podemos usar Lynis que es una herramienta que puntua la seguridad del sistema.