## Caracteristicas de Node.js
- Arquitectura basada en eventos (Single Thread Event Loop)
	- Utiliza un unico hilo de ejecucion, permitiendo el procesamiento asincrono de operaciones I/O
- Gestion de operaciones de I/O de forma asincrona o sin bloqueo
	- En una comunicacion sincrona las operaciones son bloqueantes (ejecucion secuencial)
	- En una comunicacion asincrona las operaciones no son bloqueantes y se realizan mediante el sistema de callback (retrollamadas), promesas o async/await
- Diseño modular (NPM = Node Package Manager o Yarn)
	- Para añadir un paquete en Node.js -> `var my_package = require('<name>')`
- Node.js es una plataforma de software
- Mejora la concurrencia de acceso a servidor mediante su arquitectura Signel Thread Event Loop
- Prima la escalabilidad (horizontal=consiste en agregar mas nodos a un sistema) y eficiencia

## Express
Es un framework de desarrollo de apps web minimalista y flexible para Node.js.
- Direccionamiento de URL (Routing)
- Permite trabajar con distintos motores de plantillas
- Establece una configuracion comun de la aplicacion web como el puerto de conexion

La estructura de una aplicacion con Express es la siguiente:
- App
	- app.js (fichero principal de la aplicacion) (la funcion express() crea una nueva aplicacion)
	- bin (sirve para guardar ficheros con funciones u objetos de uso generico)
		- www.js (app.set(clave, valor) y app.get(clave))
	- public
		- images
		- javascript
		- stylesheets
	- routes
		- index.js
		- users.js
	- view
		- error.html
		- index.html
	- package.json


Para que una solicitud no quede pendiente habra que indicar una de la siguientes respuesta:
- res.send()
- res.redirect()

Para organizar las rutas en modulos podemos usar:
- module.exports (se pueden incluir parametros como los repos) como por ejemplo:
```javascript
module.exports = function(app) {
	app.get('/songs', function(req, res) {
		res.send("lista de canciones");
	});
}
```

En cuanto las peticiones GET:
- Obtenemos parametros GET con `req.query.<clave_parametro>` (comprobar null o undefined)
- Para obtener parametros embedidos (/song/:id) habra qu usar `req.params.<clave_parametro>`

En cuanto a las POST:
- Habra que definir los inputs con name para que el valor se pase en el cuerpo de la llamada
- Habra que hacer uso de `body-parser` para obtener los parametros y ya podemos hacer la llamada `req.body.<clave_parametro>`