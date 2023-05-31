# Estructura practica
![[lab08-09.png]]

## Escaneo de puertos con nmap
- Escaneo multiple: `nmap <objetivo1> <objetivo2> ...`
- Escaneo de rango de IPs: `nmap <IP>-100`
- Escaneo red completa: `nmap <IP>/24`
- Escaneo rango ports: `nmap -p 22-80 <IP>`
- Deteccion del SO: `nmap -A -T4 <IP>`
	- Mas informacion: `nmap -sV <IP>`
- Escaneo lento pero detallado: `sudo nmap -sS -A -sV -O -p - <IP>`

## Escaneo puertos avanzado con scripts
Para hacer un escaneo avanzado podemos usar las siguientes opciones:
![[nmap.png]]

Para ver si realmente los paquetes llegan podemos hacer uso del verbosity con `-vvv`. 
Un ejemplo de analisis de red seria el siguiente con metodo de TCP ACK SCAN (-sA): `sudo nmap -sA -p 6 192.168.8.34 -vvv`
![[-sA SCAN.png]]


## Predecir tipo de SO con ping
Usar el siguiente comando: `ping -c 1 <IP>`
Acordarse de jugar con el Time To Live (TTL). Fijarse en la respuesta para encontrar el ttl y asi poder identificar que SO es la maquina a la cual estamos haciendo el ping.

## Formatos de salida de Nmap
- Nmap: `-oN <fichero>`
- Grepeable: `-oG <fichero>`
- XML: `-ox <fichero>` (quien quiere esto)


# NSE (Nmap Scripting Engine)
Tipos de scripts (/usr/share/nmap/scripts):
- *discovery*: busqueda activa
- *external*: enviar datos a bases de datos externas
- *version*: deteccion de versiones profunda

Leer mas doc en: https://nmap.org/nsedoc/scripts/smb-brute.html

### Localizacion de metodos de autenticacion SSH
![[SSH_METHODS.png]]

### Fuerza bruta a servidores DNS
![[DNS-BRUTE-NSE.png]]

### Buscar host en una IP
![[IP_HOST.png]]

### Traceroute
![[traceroute.png]]

## Script para conseguir recursos
```bash
#!/bin/bash
for ip_address in 156.35.94.{1..10}; do
        wget -t 1 -T 5 http://${ip_address}/robots.txt;
done&
```
Con esto podremos descargar los archivos robots.txt en caso de que existan de las direcciones 156.35.94.1-10.

