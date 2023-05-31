La idea principal de la interoperabilidad es que distintos sistemas sean capaces de comunicarse, transmitir e intercambiar informacion entre ellos, independientemente de la plataforma o lenguaje de programacion en la que esten desarrollado.

## Servicios web
Un servicio web es un sistema de software diseñado para permitir la interaccion interoperable entre maquinas en una red.
Los objetivos de un servicio web son:
- Independencia del lenguaje y de la plataforma
- Interoperabilidad
- Acoplamiento debol
- Modularidad y reusabilidad
- Escalabilidad

Los tipos de servicios web son los siguientes:
- SOAP
- RESTful API


### Arquitectura REST
REST acronimo de Representational State Transfer (Transferencia de estado Representacional). Los datos no tienen un formato definido, puede ser texto simple, JSON, XML, etc. Los servicios web que siguen la arquitectura REST se denominan servicios web RESTful.

Los principio de diseño REST son los siguientes:
- Desacoplamiento del cliente-servidor (independientes)
- Protocolo cliente-servidor sin estado (cada solicitud sera nueva sin estado anterior)
- Sistema de capas (mejorar la escalabilidad y la seguridad)
- Infraestructura de almacenamiento en cache (mejorar el rendimiento)
- Interfaz uniforme (sintaxis universal -> URI)

El principio HATEOAS (Hypermedia As The Engine Of Application State), un recurso puede contener hipervinculos de navegacion asociada a otros recursos del cliente.


## Control de acceso e identificacion del cliente con token
La identificacion del usuario se suele llevar a cabo con un token de seguridad.