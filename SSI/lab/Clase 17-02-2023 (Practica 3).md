La ip de conexion al servidor es: `156.35.95.115`
Podemos guardarlo como nombre de dominio haciendo `sudo nano /etc/hosts` poniendo la ip y el nombre que queremos usar.

Ahora nos conectamos con ssh: `ssh uo283586@ssiserver` y la contraseña es ariassXXXX.
Para cerrar la sesion usamos logout.

En el directorio /tmp tenemos los ficheros a compartir.

Para compartir entre maquinas usando ssh:
> scp mi_fichero user1@maquina1:path_donde_guardar

En nuestro caso vamos a guardarlo en el directorio /tmp.
> scp fichero uo283586@ssiserver:/tmp

Para obtener un fichero a traves de ssh:
> scrp uo283586@ssiserver:/tmp/generador.py {path}


## Cifrado de archivos usando algoritmos de clave simetrica fuerte
Voy a usar el algoritmo AES (Advanced Encryption Standard). El comando para cifrar el archivo sera:
> gpg --symmetric --cipher-algo AES {fichero}

Y se introduce una clave que en este caso es `password`.

## Descrifrado de archivos
Obtenemos el archivo del servidor de la uni con scp: `scp uo283586@ssiserver:/tmp/fichero .`

Y ahora desencriptamos el fichero con: `gpg --decrypt --output=message.txt fichero.asc`
Habra que introducir la clave para que se pueda desencriptar.

Y podemos ver el contenido del fichero en el message.txt con un cat.

## Intercambiar una clave mediante el algoritmo Diffie-Hellman
p: 997 | a: 7 | clave publica: 333

Y = pow(7, 333) % 997 = 134

Ejecutamos el siguiente comando:
> echo –e "La dato público es <coloca aquí la Y calculada>" | tee –a pkPubUOxxxxx.txt

Ahora para calcular la clave privada necesitamos la clave del compañero y podemos realiza la siguiente operacion para calcular el numero:
> prkUser2 = pow(pkUser2, prkUser1)) mod 997

prkUser2 = privateKeyUser2


## Cifrado de discos
Instalar el software de cifrado: `sudo apt install ecryptfs-utils`

Se crea una carpeta en /home.
Ejecutar el siguiente comando para montar la carpeta con ecryptfs:
> sudo mount -t ecryptfs /path /path

Elegir un algoritmo de cifrado simetrico.
Elegir 32 bytes para la clave, sin plaintext passthrough y sin cifrar nombres de archivos.

Como se trata de una carpeta cifrada solo el usuario de la carpeta puede acceder a ella.


## Cyberchef
Una pagina donde se pueden realizar operaciones de encriptacion y decriptacion sobre textos en cadena (https://gchq.github.io/CyberChef/).


## Estaganografia con steghide
Descargamos una imagen jpg con wget: `wget --no-check-certificate [URL]`

Para embedir datos en una imagen podemos usar: `steghide embed -cf cvr.jpg -ef emb.txt`
Para extraer los datos podemos usar: `steghide extract -sf cvr.jpg`


## Ofuscacion de codigo
Podemos usar las siguientes paginas para ofuscar el codigo: http://dean.edwards.name/packer/

Otra pagina que ofusca mucho el codigo es https://obfuscator.io/
De esta ultima no se puede recuperar el codigo original al 100%

Para recuperar el codigo se pueden utilizar embellecedores: http://jsnice.org/ y https://beautifier.io/




## John the ripper (suele entrar examen)
Para crackear la password de un archivo, user, etc, usar el siguiente comando:
> john --wordlist:rockyou.txt file/account

Mirar esta pagina para ejemplos de john the ripper: https://www.openwall.com/john/doc/EXAMPLES.shtml

## Crunch 
Vamos a usar crunch para generar un diccionario, por ejemplo para generar un diccionario para crackear una contraseña, en este caso la del usuario ssiuser que es test123...
Nosotros sabemos que empieza por test y termina por tres puntos

Por ello vamos a generar una lista de palabras:
> crunch 10 10 -t test%%%... -o dict.txt

> % incluye un numero cualquiera
   @ incluye una letra minuscula

Ahora ejecutamos el siguiente comando:
> john --wordlist:dict fichero de usuarios

Y podemos ver como encuentra que la contraseña es `test123...`

## Fuerza bruta con John the ripper
Para forzar  el crackeo de una pass que no tenemos ni idea de que forma tiene usaremos el modo incremental de John que nos aporta el mayor numero de permutaciones posibles. Vamos ahora a descrifrar la pass para Android:
> john --incremental --max-length=4 aux2.txt

Y podemos ver que la contraseña es a18.

