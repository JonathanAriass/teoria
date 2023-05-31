
Para darle permisos a root para conectarse mediante ssh habra que (siendo root -> su -)
- mkdir .ssh
- cp /home/ariass/.ssh/id_rsa/pub .ssh/authorized_keys (copiamos clave publica de ssiuser)

Ahora ejecutamos el siguiente comando para conectarnos con permisos de X como root:
`ssh -X root@localhost`

Ahora ya podemos ejecutar programas graficos como root: `scap-workbench`

## Actualizando las politicas de seguridad de OpenSCAP
Tras ejecutar el comando: `sudo oscap info <carpeta>/ssg-ubuntu1804-ds-1.2.xml`
```
Document type: Source Data Stream
Imported: 2021-11-26T23:52:46

Stream: scap_org.open-scap_datastream_from_xccdf_ssg-ubuntu1804-xccdf-1.2.xml
Generated: (null)
Version: 1.2
Checklists:
	Ref-Id: scap_org.open-scap_cref_ssg-ubuntu1804-xccdf-1.2.xml
		Status: draft
		Generated: 2021-11-26
		Resolved: true
		Profiles:
			Title: Profile for ANSSI DAT-NT28 Average (Intermediate) Level
				Id: xccdf_org.ssgproject.content_profile_anssi_np_nt28_average
			Title: Profile for ANSSI DAT-NT28 High (Enforced) Level
				Id: xccdf_org.ssgproject.content_profile_anssi_np_nt28_high
			Title: Profile for ANSSI DAT-NT28 Minimal Level
				Id: xccdf_org.ssgproject.content_profile_anssi_np_nt28_minimal
			Title: Profile for ANSSI DAT-NT28 Restrictive Level
				Id: xccdf_org.ssgproject.content_profile_anssi_np_nt28_restrictive
			Title: CIS Ubuntu 18.04 LTS Benchmark
				Id: xccdf_org.ssgproject.content_profile_cis
			Title: Standard System Security Profile for Ubuntu 18.04
				Id: xccdf_org.ssgproject.content_profile_standard
		Referenced check files:
			ssg-ubuntu1804-oval.xml
				system: http://oval.mitre.org/XMLSchema/oval-definitions-5
			ssg-ubuntu1804-ocil.xml
				system: http://scap.nist.gov/schema/ocil/2
Checks:
	Ref-Id: scap_org.open-scap_cref_ssg-ubuntu1804-oval.xml
	Ref-Id: scap_org.open-scap_cref_ssg-ubuntu1804-ocil.xml
	Ref-Id: scap_org.open-scap_cref_--home--wsato--git--content--build--ssg-ubuntu1804-cpe-oval.xml
Dictionaries:
	Ref-Id: scap_org.open-scap_cref_--home--wsato--git--content--build--ssg-ubuntu1804-cpe-dictionary.xml
```

## Uso de OSCAP desde la linea de comandos
REQUIERE DE PRIVILEGIOS ROOT.

Para sacar la id del profile podemos ejecutar el siguiente comando:
`$ sudo oscap info <ssg-...>`

Para realizar un análisis habrá que ejecutar el siguiente comando:
`$ sudo oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_high --results analisis --report index ssg-ubuntu1804-ds-1.2.xml `

## Remediación con OSCAP automático
Habrá que usar el mismo comando pero con la flag `--remediate` y hará el fix automático en caso de que exista.

## Remediación con Ansible
El primer paso sera cambiar el archivo .yml la linea de host: all por host: localhost.
Se ejecuta el comando: `$ sudo ansible-playbook <file>.yml`


## Uso de OpenSCAP con STIGs
Mirar en pdf pasado.