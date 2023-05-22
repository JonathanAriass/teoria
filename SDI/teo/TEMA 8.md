Los modulos pueden definir una funcion, objeto o clase.
- Los que declaran una funcion ejecutan la funcion al ser incluidos (require\<modulo>)
- Los que declaran un objeto permiten acceder a sus variables y funciones
- Los que declaran una clase permite crear instancias

Las apps utilizan modulos:
- Externos (npm)
- Propios (routesAds)
Para acceder a estos modulos se podra hacer lo siguiente:
1. Obtener el objeto/funcion de  donde sea necesario (util = require("utils.js"))
2. Enviarlo como parametro a otros modulos (module.exports = function(util))
3. Almacenarlo en variables de la app (app.get('util') y app.get('util'))

Para usar modulos integrados en express se puede usar `app.use(<objeto/funcion>)`.

## Arquitectura: acceso a datos
Debemos encapsular el acceso a datos en uno o varios modulos.
Podemos definir un modulo como objeto que encapsule las operaciones (asincronas y deben recibir una funcion de callback).

Para acceder a los datos desde un controlador:
```javascript
app.post("/song", function(req, res) {
	var song = {
		name: req.body.name,
		genero: req.body.genero
	}

	songsRepository.insertSong(song, function(id) {
		if (id === null) 
			res.send("error al insertar");
		else
			res.send("agregada id:" + id);
	});
});
```


### Operaciones CRUD
- **InsertOne()**: inserta un doc en la coleccion (si \_id no existe se genera automaticamente)
- **InsertMany()**
- **DeleteOne()**: habra que aplicarle un *filter* para poder encontrar el documento a eliminar
- **DeleteMany()**
- **UpdateOne()**
- **UpdateMany()**


## Encriptacion, autorizacion y autenticacion
El modulo crypto permite crifar y descrifrar. Esta incluido en el Core de Node.js
`var crypto = require('crypto')`

Permite definir una "clave de cifrado" o "secreto":
- createHmac(\<tipo>, \<secreto>): realizar el cifrado
```
secreto = 'abcdefg’;  
valor = "342434";  
encryptor = crypto.createHmac('sha256', secreto)```
```
- update(\<valor a cifrar>): retorna el valor cifrado
- digest(\<tipo>): especifica la codificacion del varlo cifrado
```
encryptedValue = encryptor.update(valor).digest('hex');
```


Por otro lado la autenticacion consiste en validar la identidad de un usuario. 

Una vez el usuario se autentica con exito debemos recordarlo, el objeto sesion es clave para identificar navegadores/clientes autenticados. Esto lo podemos logar con el modulo externo express-session (obtener la funcion con require). Los atributos se pueden leer/escribir mediante `req.session.<clave del atributo>`.


## Enrutadores
Los enrutadores permiten definir funciones que procesan peticiones. Se crea con `express.Router()` y con use se agregara una funcion manejadora. Tendra un parametro adicional `next` que es el que permitira continuar con el flujo de ejecucion.

Una vez creado el enrutador se podra agregar a la aplicacion con:
`app.use("/private/", routerAutentication);`

