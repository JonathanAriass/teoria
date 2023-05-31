Criptografia: ocultar el `significado` de la informacion
Estenografia: ocultar la `existencia` de la informacion

# Criptografia
La criptografia tiene como objetivo los siguientes puntos:
- Confidencialidad: solo para los que conocen el metodo de descifrado podran leer
- Integridad: garantia de que los datos transmitidos estan sin modificar
- Autenticacion: verificacion de identidad de remitente y receptor (firmas)


## Confidencialidad
Los algoritmos de cifrado segun la forma de procesar la data se puede clasificar en:
- Cifrado por bloques (IDE, AES, RSA, ...)
	- Cifran por bloques de informacion (64, 128 bits, ...)
- Cifrado de flujos (A5, RC4, SEAL, ...)
	- Cifran la informacion bit a bit

Los algoritmos de cifrado segun como se usan las claves se pueden clasificar en:
- Cifrados sin clave: permutan posiciones de unidades de texto con un sistema
- Cifrados con clave criptografica
	- Algoritmos de clave simetrica: se comparte clave entre emisor y receptor
	- Algoritmos asimetricos: dos claves (emisor y receptor), public y private
La fortaleza de las claves se mide en bits o numeros de digitos

### Algoritmos de clave simetrica
El emisor y el receptor comparten la misma clave K. La transmision de dicha clave es un downside de los algoritmos de clave simetrica ya que se puede interceptar dicha clave de alguna forma.
![[Pasted image 20230318114117.png]]

Un algoritmo es considerado computacionalmente seguro cuando un atacante siempre tarda mas en romper un cifrado que con fuerza bruta. Algun algoritmo de cifrado por bloques considerados seguros son: AES, IDEA, Twofish, Serpent

#### Algoritmo de intercambio de claves de Diffie-Hellman
Establece una clave simetrica entre 2 maquinas para cifrar las comunicaciones.
![[Pasted image 20230318122430.png]]

Algunas de las aplicaciones de los algoritmos de clave simetrica son:
- Onion routing (transmisiones anonimas cifradas)
- Cifrado de discos
- Autenticacion de plataforma (TPM - Trusted Platform Module)


### Algoritmos asimetricos o de clave publica
Se ahorra el problema de que el remitente y emisor tengan que acordarse de su propio par de claves. En este caso las claves del par (DK, DE) se generan conjuntamente. Cada par es unico para cada emisor / receptor.
- Clave privada (DK, clave del descrifrado) - secreta
- Clave public (EK, clave del cifrado) - publica
![[Pasted image 20230319110007.png]]

- RSA: numeros primos (p y q), siendo lento
- ECC (Elliptic-Curve Cryptography): son mas faciles de manejar y mas escalables que los no ECC

GPG es una herramienta de cifrado simetrico y asimetrico y firma digital. Tambien tiene un sistema hibrido para cifrado simetrico + asimetrico.

Aplicaciones de algoritmos asimetricos:
- Cifrado de archivos y directorios
- Cifrado de extremo a extremo

## Integridad
Funcion hash: funcion matematica que transforma un conjunto de datos M en una salida H de longitud fija (n). Algunas de sus propiedades son:
- Faciles de calcular
- Unidireccional
- Compresion, difusion y no previsibilidad
Algunos de los algoritmos de hash son:
- MD5 y SHA-1 (obsoletos)
- SHA-3
- BLAKE2
Aplicaciones de las funciones hash:
- Almacenamiento de contraseñas
- Huella digital (fingerprinting): asegura que un archivo es el original
- Firmas digitales: asegura que un archivo fue creado por X persona
- Blockchain: usa SHA-256 para detectar modificaciones fraudulentas

#### KDF - Key Derivation Function
Obtienen una o mas claves de un valor secreto (clave maestra):
- Usa key stretching para mejorar la seguridad
	- Sal: datos aleatorios concatenados a la contraseña
	- Iteraciones: aplicar la funcion hash > 1
Algunos de estos algoritmos son:
- PBKDF2
- scrypt
- bcrypt
- Argon2

Tecnicas tipicas para adivinar contraseñas a partir de datos almacenados:
- Fuerza bruta
- Diccionarios
- Tablas rainbow
Con KDF se intenta evitar dichos ataques.

## Autenticacion
### Firmas digitales
Firmas digitales: resultado de una operacion criptografica que une un documento firmado a un elemento personal, el certificado digital. Resultado de firmar criptograficamente el hash de un archivo con la clave privada de su autor. Los objetivos son:
- Autenticacion del origen
- Integridad
- No repudiar
Para cumplir estos objetivos la firma debe de ser imposible de falsificar y no debe poder reutilizarse.

El procedimiento de firma de mensajes es el siguiente:
- Un hash del mensaje se calcular y se cifra con clave privada del usuario
- El hash se descifra una vez recibido (con la clave publica)
- Si son iguales, el mensaje no ha sido alterado
![[Pasted image 20230319120320.png]]

El estandar de firma digital es el DSS (Digital Signature Standard) que permite firmar documentos pero no cifrarlos.
![[Pasted image 20230319120710.png]]

DNSSEC garantiza, mediante el uso de firmas digitales, que el contenido (direcciones DNS) de los servidores no se altere.

### Cifrado autenticado
MAC (Message Authentication Code) es un procedimiento que agrega a un mensaje un codigo que depende de una clave simetrica compartida, autenticando el mensaje y el remitente. Hay 3 formas de crear MACs:
- Basado en Hash (HMAC - recomendado)
- Basado en cifrado por bloques (CBC-MAC)
- Galois Counter Message Authentication Code-based (GMAC)

Para calcular una MAC:
- Hay 2 usuarios S y R con una clave secreta K y un mensaje M
- S crea una MAC a partir de M con f (funcion)
	- MAC = f(K, M)
- S envia M+MAC a R
- R calcula MAC' con K y M
- Si MAC' = MAC el mensaje es autentico

Authenticated Encryption (AE) y Authenticated Encryption with Associated Data (AEAD) son formas de cifrado que proporcionan los 3 propiedades CIA.

### Certificados digitales
Un certificado es como una tarjeta de identidad, es la asociacion entre una entidad fisica y una clave publica. 
Necesitamos un mecanismo adicional para asegurarnos de que el titular de una clave es quien dice ser:
- Una entidad U1 firma digitalmente los certificados de otra entidad U2
- Confiamos en U1, por lo que aceptamos el certificado U2 como valido
Estos mecanismos pueden ser:
- Anillos de confianza (GPG): niveles de confianza
- Autoridades de certificacion (CA): funcionan como un notario

Hay varios tipos de certificados digitales:
- Personal
- Servidor / maquina
- Software
- De CA
El estandar que define el forma de los certificados de clave publica es el X.509

Las conexiones HTTP seguras son un proceso transaparente de negociacion de certificados establecido entre navegadores y servidores web. Hay muchos conceptos que forman parte de una conexion HTTPs:
- Certificados para identificar servidores y transmitir su clave publica al cliente
- Cifrado asimetrico para cifrar una clave simetrica para cada conexion
- Cifrado simetrico a todos los datos enviados
![[Pasted image 20230320003346.png]]
Otros usos son:
- Transacciones remotas via SSH
- VPNs
- Transacciones remotas commo cliente
- Autenticacion de email / ficheros
- Autenticacion de codigo

# Esteganografia
Sustitucion de bits en el objeto contenedor por los correspondientes a la informacion que se va a ocultar. Puede levantar sospechas ya que cambiar el tamaño del contenedor.
![[Pasted image 20230320003829.png]]

La esteganografia se suele combinar con la criptografia, ya que si se descubre el patron esteganografico se sigue sin conocer el mensaje.
Al combinar criptografia y esteganografia la probabilidad de transmitir informacion sin que sea detectada aumenta.