## Fundamentos de seguridad de aplicaciones
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

## Seguridad a nivel de requisitos
Una persona o equipo debe desarrollar los requisitos de seguridad de la aplicacion. Deben hacer preguntas con las que se elaboraran.

## Requisitos de manejo de datos
Nunca se debe confiar en la entrada de un usuario, ya que puede ser valida pero maliciosa.

Hay que validar todos los puntos de entrada de datos como cualquier input, cabeceras HTTP, campos hidden, etc. Tambien habra que validar los datos que se reciban de SGBDs, APIs, de otras aplicaciones, etc. Todo el tema de URLs, cookies y ficheros de configuracion tambien tienen que ser analizados.

Debe de exisitir una politica especificando los datos que se recogen en las cookies y los datos de la aplicacion deben ser clasificados y etiquetados de acuerdo a lo privados que son.

Habra que tener cuidado con las inyecciones de codigo y protegerse de estas.

Si se van a usar cookies habra que configurarlas siguiendo una serie de reglas para que sean seguras:
- Deben de validarse antes de ser aceptadas
- El ID de sesion debe pasarse siempre en una session cookie (no persistent)
- Las cookies persistentes deben caducar (attributo Expires)

## Requisitos de autenticacion
Los usuarios deberia de usar un password manager (KeePass por ejemplo). Los secret stores son similares pero para software, no para personas.

Habra que intentar no guardar passwords e intentar usar un servicio de autenticacion de terceros si es posible como Google u Outlook.

Estaria bien implementa un Multi-Factor authentication (2FA/MFA) para asi asegurar que incluso con la clave comprometida no es posible acceder a una cuenta. Los esquemas MFA se basan en que los usuarios den 2 de 3 "algos":
- Algo que **Saben**
- Algo que **Tienen**
- Algo que **Son**

Tipos de MFA:
- Token SMS
- Token por Email
- Token Hardware como un USB
- Token Software (generacion de token dinamicos)
- Telefono
- Verificacion biometrica

## Otros requisitos de seguridad
Toda linea de codigo incluida de una libreria, framework, plugin o componente de terceros es un riesgo que incorporas a tu aplicacion.
Habra que usar siempre HTTPS, con una configuracion de TLS robusta y segura.

Mas requisitos puede ser:
- Borrar comentarios del frontend de la pagina
- Backups periodicos
- Configurar y usar caracteristicas de seguridad del framework
- Intentar evitar subida de ficheros.


## Diseño seguro
- Never trust, Always verify/Zero trust/Assume breach
- Denegar por defecto
- Aisalmiento por diseño
- Separacion de codigo por diseño
- Separacion de tipos de funcionalidad por diseño
- Diseño de la gestion de secretos de la aplicacion

### Thread modeling
Consiste en identificar potenciales amenazas para un negocio, sistema, producto o aplicacion.
Se necesitara un representante de cada uno de los stakeholders de la aplicacion y deben de aportar los riesgos que ve en el sistema. Deben de verlo desde la mentalidad del mal, como si fueran adversarios.


## Creacion de codigo seguro
Si tenemos opcion a elegir las tecnologias a usar es mejor evitar usar tecnologias muy modernas y es mejor usar aquellas que tengan una version LTS (Long-Term Support). Tambien habra que minimizar la cantidad de librerias, componentes y frameworks a usar.

Siempre se tendra que validar del lado del servidor ante cualquier entrada del usuario.
Si una aplicacion utiliza el protocolo HTTP se tendra que eliminar el soporte de aquellos verbos que no se usan (PUT, DELETE, etc).

Habra que checkear los limites de la aplicacion como por ejemplo en aquellas desarrolladas con C o C++ que no son memory safe.

Una vez se sabe quien es el usuario (AuthN) se autorizara al usuario con AuthZ:
- RBAC (Role-Based Access Control)
- DAC (Dictionary Access Control): como permisos de ficheros linux
- MAC (Mandatory Access Control): el accesso a un recurso se basa en lo privado que es
- PBAC (Permission-Based Access Control)

## Manejo de errores, log y monitorizacion
Hacer un catch globalk en el main es buena idea como ultimo recurso.
Nunca se debe relevar las trazas de pila.
En caso de transaccion fallida hacer un rollback.

Hay sistemas de monitorizacion que analizan los logs que se les mandan buscando problemas.


## Seguridad y usabilidad
Habra que hacer un esfuerzo para que la seguridad no afecte a la usabilidad de la aplicacion.


## AST (Application Security Testing)
Las actividades de testing son criticas para detectar problemas de seguridad. Esto implica introducir herramientas AST en el proceso de desarrollo con el uso de pipelines en CI (Continous Integration).

Tipos de herrramientas:
- SCA (Software Composition Analysis): gestionan el uso de componentes open source de un aplicacion (escaneo automatico de codigo para ver si cumplen licencias, tienen vulnerabilidades, etc)
- SAST (Static Application Security Testing): prueban estructuras internas, no su funcionalidad
- DAST (Dynamic Application Security Testing): metodo de prueba de caja negra que introduce errores para probar las rutas de ejecucion que estos provocan
- IAST (Interactive Application Security Testing):  evalua el rendimiento y detecta vulnerabilidades

Donde podemos implementar test de seguridad en DevOps:
1. En el IDE
2. Pre-commit (busqueda de secretos)
3. En el pipeline (build, deploy, etc)
4. Fuera del pipeline (mantenimiento)
	1. A nivel de repositorio (herramientas SCA y SAST)
	2. Mantenimiento periodico
	3. Pruebas unitarias
	4. Gestion de vulnerabilidades continua

## Despliegue y mantenimiento seguros
Para matener nuestra aplicacion desplegada tenemos que tener en cuenta ciertas cosas como:
- Sistemas de monitorizacion, log y alertas de seguridad continuas
- Habra que usar una API Gateway
- WAFs (Web Application Firewalls): modulos de los principales servidores web que protegen ante ataques
- RASP (Runtime Applicatoin Self-Protection): capaces de inspeccionar el comportamiento de app y su contexto
- UEBA (User and Entity Behavior Analytics): 