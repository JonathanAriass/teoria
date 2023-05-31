RECOMENDACION DEL PROFESOR: hacer la practica sin los dockers containers.

## Generar un par de claves publicas
Con el comando `gng --gen-key`:
- Usuario: uo283586
- Email: uo283586@uniovi.es
- Contraseña: ariassXXXX

## Administrar un llavero (keyring)
Para mostrar las claves en el llavero privado: `gpg --list-keys` 

### Transmitir tu clave publica a otros
Habrá que usar el siguiente comando:
`$ gpg --armor --export <nombreusuario> > <nombreusuario>_public_key.asc`

Si una persona quiere añadir la clave a su llavero habrá que usar la opción `--import`.


## Firmas digitales para integridad
Para firmar un archivo se puede usar la opción `--clearsign`:
- Para firmar `archivo.txt` usa el comando: `gpg --clearsign archivo.txt`
- Para verificar la firma en otra maquina habrá que usar: `gpg --verify archivo.txt.asc`

## Usando una firma digital y datos cifrados automáticamente
El remitente necesita ejecutar el siguiente comando:
`$ gpg -o cryptandsign.enc -s -e -r arias archivo.txt`

Y ahora para descifrar habra que ejecutar el siguiente comando:
`$ gpg -o archivo.txt -d cryptandsign.enc`

## Marcas de agua
Texto corto, marca de agua grande: 
```shell
convert -density 150 -fill "rgba(255,0,0,0.25)" -gravity Center -pointsize 80 -draw "rotate -45 text 0,0 \<text>" \<original image> \<watermarked  image>
```

## SSH sin contraseña
Vamos a conectarnos vía ssh con una clave en vez de una contraseña:
- Tenemos la clave privada que será un archivo con contraseña
- Tenemos la clave publica también
En la otra maquina habrá que almacenar la contraseña publica de la otra maquina en el fichero `authorited_keys`. Haciendo que cualquier maquina que tenga una clave publica que esta en dicho fichero se pueda conectar con su clave privada.

Se crea el fichero en el directorio `~/.ssh/` y con el comando `ssh-keygen` generamos una clave, dejando el directorio donde se crea el fichero por defecto. La passprhase es: `test123...`

Los ficheros creados son:
- `known_hosts`: cada vez que me he conectado a una maquina via ssh se guardan unas fingerprints
- `id_rsa`: clave privada
- `id_rsa.pub`: clave publica

Tenemos que crear el fichero `config` con la siguiente orden: `echo "AddKeysToAgent yes" >> ~/.ssh/config`

Ahora habrá que copiar la contraseña con el comando `ssh-copy-id ssiserver`

Ahora ya nos podemos conectar a la maquina mediante ssh sin tener que meter contraseña.

Ahora podemos hacer copias directas con scp sin tener que usar una contraseña.
