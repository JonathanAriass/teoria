Cumplimiento como codigo:
- Prevenir
- Detectar
- Corregir

# Security Content Automation Protocol (SCAP)
Protocolo que permite el hardening automatizado en sistemas de software (estandarizado por NIST). Carga archivos en dos formatos OVAL y XCCDF para evaluar y corregir controles de seguridad.

OVAL (Open Vulnerability Assessment Language) permite representar informacion de los diferentes elementos que forman la configuracion de un sistema informatico.

XCCDF (Extensible Configuration Checklist Description Format) permite escribir listas de controles de seguridad.

Source Data Stream formato de archivos compatibles con SCAP 1.2+ e incluye archivos XCCDF y OVAL ademas de otros componentes.


# El paquete SCAP Security Guide
Nos proporciona un conjunto de politicas de seguridad prediseñadas compatibles con SCAP. Es importante mantener las politicas de seguridad de este paquete actualizadas.

Hay que tener cuidado ya que la correcion automatica no siempre esta disponible o es completa. La licencia de Ubuntu Pro incluye archivos de correcion SCAP.

Ventajas de SCAP:
- Gratuito
- Facilita el Compliance as Code
- Mantenimiento frecuente
Desventajas de SCAP:
- Incompleto para algunos productos
- No estan tan validados como otras fuentes de controles de seguridad


# Security Thechnical Implementation Guides (STIGs)
STIG es uno de los estandares de configuracion utilizados por el Departamento de Defensa de EEUU y DISA (Defense Information Systems Agency).

## Categorias STIG
Se aplican a controles de seguridad.

Para cada tipo de dispositivo o aplicacion, un STIG contiene cientos de checks.
A cada una de de estos checks se les asigna un nivel de gravedad:
- CAT I (muy grave)
- CAT II (intermedia)
- CAT III (menos grave)

## Niveles Mission Assurance Category (MACs)
Se aplican a maquinas / sistemas.

Se clasifican en funcion de la importancia de la informacion que administran y cuan critica es:
- MAC I (implementar medidas mas fuertes)
- MAC II (implementar medidas medias)
- MAC III (mejores practicas de gestion)


Ventajas de STIGs:
- Guias de seguridad validadas para una amplia gama de productos
- Facilitan el Compliance as Code
- Alto grado de seguridad (grado militar)

Desventajas de STIGs:
- Quizas se requiera de modificaciones para adaptarlas a uso civil (no militar)
- Su herramienta oficial de automatizacion SCAP esta restringida a uso del gobierno de EEUU

STIG es una implementacion para usar en SCAP


# Benchmarks del Center for Internet Security (CIS)
Fuente bien establecida de guias de hardening con valores y controles tecnicos de seguridad para muchos dispositivos. Estan creados y usados por el gobierno de EEUU, por lo que garantiza la calidad y fiabilidad de sus contenidos.

Estan disponibles en formato PDF o SCAP. Los archivos del paquete SCAP security guide tambien incluyen perfiles de seguridad basados en CIS.

Inidica si el cumplimiento de un control influye en la puntuacion de seguridad (Scored o not scored). Los controles de seguridad se dividen en perfiles de uso y niveles:
- Perfiles de uso (dependen de la funcionalidad que se espera que el software o SO cumpla)
- Niveles
	- Nivel 1: un control mas practico y no causar daños innecesarios
	- Nivel 2: amplia el nivel 1 pudiendo causar daños a la funcionalidad de la maquina
	- Niveles especiales (solo para algunos productos)

Ventajas de CIS:
- Guias completas y detalladas de controles (mucha seguridad)
- Mucha adaptabilidad

Desventajas de CIS:
- Solo cubre los productos mas usados
- Puede ser muy tedioso adaptarse a una funcionalidad especifica


