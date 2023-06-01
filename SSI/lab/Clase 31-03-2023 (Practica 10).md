Estructura del lab:
![[lab10.png]]

## Instalación de reverse proxy (Apache2)
- Primero habrá que entrar al contenedor del reverse_proxy.
- Retocamos el archivo `/etc/apache2/sites-enabled/000-default.conf`
```conf
<VirtualHost *:80>

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Location "/eii">
                ProxyPass "http://192.168.10.3/"
                ProxyPassReverse "http://192.168.10.3/"
        </Location>
        <Location "/epi">
                ProxyPass "http://192.168.10.4/"
                ProxyPassReverse "http://192.168.10.4/"
        </Location>

</VirtualHost>
```

- Reiniciamos el proxy: `service apache2 restart`
- Comprobamos en el navegador que podemos viajar a \<IP_Proxy\>/eii  (IP_PROXY = 192.168.10.2) 


## Instalación de un WAF
Seguir pasos del guion para instalarlo.

Para probarlo en la configuración base de apache añadimos una regla que salte cuando se acceda al server con los siguientes parámetros en la URL: `url/?testargs=ssi` y se puede ver como se lanza un forbidden access.
Esto se puede comprobar en el archivo `/var/log/apache2/access.log`:
![[access_log.png]]

También se debería de bloquear con: `/?testargs=/bin/bash`

## Prueba con Nikto (escaneo de servidores)
Para hacer la prueba el comando usado  ha sido el siguiente: 
`nikto -Display 1234EP -o report.html -Format htm -Tuning 123bde -host 192.168.10.2`

Si abrimos el archivo `/var/log/access.log` del proxy podemos ver como muchas peticiones han sido bloqueadas por el ModSecurity, por lo que este ha hecho su trabajo bien.

## Ataques con XSS
Podemos intentar hacer una SQLInjection: 
`curl 192.168.10.2/-d "\<script>DROP DATABASE;\</script>"`

El resultado es el siguiente:
![[SQLInjection.png]]


## Instalación y configuración de Suricata
No funciona la solicitud con troyano conocido.

## SCA y SAST
Mirar la guia que esta explicado perfecto.
