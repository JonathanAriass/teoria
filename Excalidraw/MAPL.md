---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
MAPL ^Px8KeT89

MAPL es una maquina de pila abstracta usada para fines docente. ^pkecOinD

Arquitectura ^VGzGHHji

Tiene un segmento de codigo separado (byte por instruccion).

Segmento de datos entre 512 bytes y 16KB. Siendo MAPL una maquina de 16-bit de palabra.

 ^UZSVan6D

Code segment ^WaJNcdJl

Global vars ^3cxjmToS

Stack ^loEUODrC

Codigo ^fY5IEMhU

Datos ^pkAiNEtk

IP ^7YSwTCGF

SP ^5TbeLxYo

BP ^ekcMbSio

REGISTROS
    
    - IP (Instruction Pointer): direccion de la instruccion en ejecucion

    - SP (Stack Pointer): direccion del tope de la pila

    - BP (Base Pointer): direccion del marco de pila activo ^JZdY1Oyz

Ejercicio ^KowtdUPK

Dado el siguiente programa de alto nivel:

        a = 3;
        b = a;

Escribir el codigo destino MAPL: ^4yK32t5j

pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila
pushi 3           // Introduce un numero entero (2 bytes) en la pila
storei
pusha 2          // Introducimos una direccion (2 bytes) 2 de la pila
pusha 0          // Introduce un numero entero (2 bytes) en la pila
loadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion
storei            // Extra n bytes de la pila, extrae una direccion de memoria de la pila (2 bytes) y el contenido es reemplazado ^Lz1ABHgj

Ejercicio 2 ^E5gjVd2H

Dado el siguiente programa de alto nivel:

        read myInteger;
        real = myInteger * 3.4 - 7;
        write real;

Escribir el codigo destino MAPL: ^CrVv6iBi

pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila
ini                // Lee un valor del teclado e introduce su representacion binaria en la pila
storei
pusha 2          // Introducimos una direccion (2 bytes) 2 de la pila
pusha 0          // Introduce un numero entero (2 bytes) en la pila
loadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion
i2f               // Necesario pasar a real por la operacion posterior
pushf 3.4        // Introduce un numero real (4 bytes) en la pila
mulf              // Multiplicacion de reales (extraccion de los numero de la pila, se operan y se introduce el resultado en la pila)
pushi 7         
i2f
subf
storef
push 2
loadf
outf ^yXfchQVI

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/1.8.26",
	"elements": [
		{
			"type": "text",
			"version": 14,
			"versionNonce": 2069300380,
			"isDeleted": false,
			"id": "Px8KeT89",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -460,
			"y": -380,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 96.55197143554688,
			"height": 45,
			"seed": 719607588,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 36,
			"fontFamily": 1,
			"text": "MAPL",
			"rawText": "MAPL",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "MAPL",
			"lineHeight": 1.25,
			"baseline": 32
		},
		{
			"type": "text",
			"version": 100,
			"versionNonce": 1291723556,
			"isDeleted": false,
			"id": "pkecOinD",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420,
			"y": -340,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 538.7357177734375,
			"height": 20,
			"seed": 692073628,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "MAPL es una maquina de pila abstracta usada para fines docente.",
			"rawText": "MAPL es una maquina de pila abstracta usada para fines docente.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "MAPL es una maquina de pila abstracta usada para fines docente.",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "text",
			"version": 27,
			"versionNonce": 600051996,
			"isDeleted": false,
			"id": "VGzGHHji",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420,
			"y": -300,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 175.36392211914062,
			"height": 35,
			"seed": 599794212,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Arquitectura",
			"rawText": "Arquitectura",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Arquitectura",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 301,
			"versionNonce": 1997938340,
			"isDeleted": false,
			"id": "UZSVan6D",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": -260,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 730.383544921875,
			"height": 100,
			"seed": 692073628,
			"groupIds": [],
			"roundness": null,
			"boundElements": [
				{
					"id": "MkMhI5qeOpovhnXKAGWad",
					"type": "arrow"
				},
				{
					"id": "fqXZZnXvqf_45-5KesnUr",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Tiene un segmento de codigo separado (byte por instruccion).\n\nSegmento de datos entre 512 bytes y 16KB. Siendo MAPL una maquina de 16-bit de palabra.\n\n",
			"rawText": "Tiene un segmento de codigo separado (byte por instruccion).\n\nSegmento de datos entre 512 bytes y 16KB. Siendo MAPL una maquina de 16-bit de palabra.\n\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Tiene un segmento de codigo separado (byte por instruccion).\n\nSegmento de datos entre 512 bytes y 16KB. Siendo MAPL una maquina de 16-bit de palabra.\n\n",
			"lineHeight": 1.25,
			"baseline": 94
		},
		{
			"type": "rectangle",
			"version": 21,
			"versionNonce": 1138462108,
			"isDeleted": false,
			"id": "KAD644CT0_jgUqf2NUVtS",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -180,
			"y": -180,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 220,
			"height": 80,
			"seed": 175125924,
			"groupIds": [],
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "WaJNcdJl"
				},
				{
					"id": "MkMhI5qeOpovhnXKAGWad",
					"type": "arrow"
				},
				{
					"id": "fqXZZnXvqf_45-5KesnUr",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 63,
			"versionNonce": 597862948,
			"isDeleted": false,
			"id": "WaJNcdJl",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -162.63796997070312,
			"y": -157.5,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 185.27593994140625,
			"height": 35,
			"seed": 1340485412,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Code segment",
			"rawText": "Code segment",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "KAD644CT0_jgUqf2NUVtS",
			"originalText": "Code segment",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "rectangle",
			"version": 23,
			"versionNonce": 1557101084,
			"isDeleted": false,
			"id": "F9_fYWcG65B4nhlBeofG2",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -180,
			"y": -100,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 220,
			"height": 80,
			"seed": 175125924,
			"groupIds": [],
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "3cxjmToS"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 82,
			"versionNonce": 898745764,
			"isDeleted": false,
			"id": "3cxjmToS",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -149.89797973632812,
			"y": -77.5,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 159.79595947265625,
			"height": 35,
			"seed": 1340485412,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Global vars",
			"rawText": "Global vars",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "F9_fYWcG65B4nhlBeofG2",
			"originalText": "Global vars",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "rectangle",
			"version": 25,
			"versionNonce": 2039600796,
			"isDeleted": false,
			"id": "J_4nmtPi6NHBGe2aO8LOh",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -180,
			"y": -20,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 220,
			"height": 80,
			"seed": 175125924,
			"groupIds": [],
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "EG-o5IXGt_41p8YlQfiwP",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 26,
			"versionNonce": 34697508,
			"isDeleted": false,
			"id": "MC8HEN3i-_A-XnqYaOOsc",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -180,
			"y": 60,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 220,
			"height": 60,
			"seed": 175125924,
			"groupIds": [],
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "loEUODrC"
				},
				{
					"id": "hGgt-zdNMOjFUyh96ItIL",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 72,
			"versionNonce": 1993646876,
			"isDeleted": false,
			"id": "loEUODrC",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -109.6059799194336,
			"y": 72.5,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 79.21195983886719,
			"height": 35,
			"seed": 1340485412,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Stack",
			"rawText": "Stack",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "MC8HEN3i-_A-XnqYaOOsc",
			"originalText": "Stack",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "arrow",
			"version": 33,
			"versionNonce": 1713918620,
			"isDeleted": false,
			"id": "MkMhI5qeOpovhnXKAGWad",
			"fillStyle": "hachure",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": 60,
			"y": -140,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.842170943040401e-14,
			"height": 0,
			"seed": 1557250724,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083151426,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "KAD644CT0_jgUqf2NUVtS",
				"gap": 20,
				"focus": 0
			},
			"endBinding": {
				"elementId": "UZSVan6D",
				"gap": 20,
				"focus": -1.4
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					2.842170943040401e-14,
					0
				]
			]
		},
		{
			"type": "text",
			"version": 9,
			"versionNonce": 1258938268,
			"isDeleted": false,
			"id": "fY5IEMhU",
			"fillStyle": "hachure",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": 155,
			"y": -146.25,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 48.65596008300781,
			"height": 20,
			"seed": 1944114212,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Codigo",
			"rawText": "Codigo",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Codigo",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "line",
			"version": 50,
			"versionNonce": 716863524,
			"isDeleted": false,
			"id": "kE5kQiSGoNC5JgxrkU0k-",
			"fillStyle": "hachure",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": 60,
			"y": -80,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 180,
			"seed": 446821796,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": [
				0,
				180
			],
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					40,
					20
				],
				[
					40,
					160
				],
				[
					0,
					180
				]
			]
		},
		{
			"type": "arrow",
			"version": 18,
			"versionNonce": 1315146780,
			"isDeleted": false,
			"id": "H2dOU9K4dA1wQWVxBB-70",
			"fillStyle": "hachure",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": 100,
			"y": 0,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 80,
			"height": 0,
			"seed": 1557250724,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					80,
					0
				]
			]
		},
		{
			"type": "text",
			"version": 12,
			"versionNonce": 1686098852,
			"isDeleted": false,
			"id": "pkAiNEtk",
			"fillStyle": "hachure",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": 197,
			"y": -6.25,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 49.74397277832031,
			"height": 20,
			"seed": 1038378140,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Datos",
			"rawText": "Datos",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Datos",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "arrow",
			"version": 15,
			"versionNonce": 47425692,
			"isDeleted": false,
			"id": "ms5GjA7SgyjyEV7zxRB4b",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -60,
			"y": 80,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 40,
			"seed": 681856164,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					0,
					-40
				]
			]
		},
		{
			"type": "rectangle",
			"version": 11,
			"versionNonce": 68009764,
			"isDeleted": false,
			"id": "Js_GNRtWQv3-0s_1edqyY",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -260,
			"y": -160,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 40,
			"seed": 332854948,
			"groupIds": [],
			"roundness": null,
			"boundElements": [
				{
					"type": "text",
					"id": "7YSwTCGF"
				},
				{
					"id": "fqXZZnXvqf_45-5KesnUr",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 8,
			"versionNonce": 1544303900,
			"isDeleted": false,
			"id": "7YSwTCGF",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -249.64798736572266,
			"y": -150,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 19.295974731445312,
			"height": 20,
			"seed": 862013732,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "IP",
			"rawText": "IP",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "Js_GNRtWQv3-0s_1edqyY",
			"originalText": "IP",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "arrow",
			"version": 64,
			"versionNonce": 1916504092,
			"isDeleted": false,
			"id": "fqXZZnXvqf_45-5KesnUr",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -219,
			"y": -140,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 38,
			"height": 0,
			"seed": 1120084636,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083151430,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "Js_GNRtWQv3-0s_1edqyY",
				"gap": 1,
				"focus": 0
			},
			"endBinding": {
				"elementId": "KAD644CT0_jgUqf2NUVtS",
				"gap": 1,
				"focus": 0
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					38,
					0
				]
			]
		},
		{
			"type": "rectangle",
			"version": 16,
			"versionNonce": 125776284,
			"isDeleted": false,
			"id": "7JaEzDo1wnEUpk0-ZZotA",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -260,
			"y": 0,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 40,
			"seed": 332854948,
			"groupIds": [],
			"roundness": null,
			"boundElements": [
				{
					"type": "text",
					"id": "5TbeLxYo"
				},
				{
					"id": "EG-o5IXGt_41p8YlQfiwP",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 15,
			"versionNonce": 410732068,
			"isDeleted": false,
			"id": "5TbeLxYo",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -250.15199279785156,
			"y": 10,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 20.303985595703125,
			"height": 20,
			"seed": 862013732,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "SP",
			"rawText": "SP",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "7JaEzDo1wnEUpk0-ZZotA",
			"originalText": "SP",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "arrow",
			"version": 103,
			"versionNonce": 1649157276,
			"isDeleted": false,
			"id": "EG-o5IXGt_41p8YlQfiwP",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -219,
			"y": 20,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 38,
			"height": 0,
			"seed": 1120084636,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083151431,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "7JaEzDo1wnEUpk0-ZZotA",
				"gap": 1,
				"focus": 0
			},
			"endBinding": {
				"elementId": "J_4nmtPi6NHBGe2aO8LOh",
				"gap": 1,
				"focus": 0
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					38,
					0
				]
			]
		},
		{
			"type": "rectangle",
			"version": 16,
			"versionNonce": 1022812580,
			"isDeleted": false,
			"id": "cWNgSBNswEWX9zXCN2_ny",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -260,
			"y": 80,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 40,
			"height": 40,
			"seed": 332854948,
			"groupIds": [],
			"roundness": null,
			"boundElements": [
				{
					"type": "text",
					"id": "ekcMbSio"
				},
				{
					"id": "hGgt-zdNMOjFUyh96ItIL",
					"type": "arrow"
				}
			],
			"updated": 1684083054653,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 15,
			"versionNonce": 1536981660,
			"isDeleted": false,
			"id": "ekcMbSio",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -251.10398864746094,
			"y": 90,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 22.207977294921875,
			"height": 20,
			"seed": 862013732,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "BP",
			"rawText": "BP",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "cWNgSBNswEWX9zXCN2_ny",
			"originalText": "BP",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "arrow",
			"version": 115,
			"versionNonce": 789917980,
			"isDeleted": false,
			"id": "hGgt-zdNMOjFUyh96ItIL",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -219,
			"y": 100,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 38,
			"height": 0,
			"seed": 1120084636,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083151432,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "cWNgSBNswEWX9zXCN2_ny",
				"gap": 1,
				"focus": 0
			},
			"endBinding": {
				"elementId": "MC8HEN3i-_A-XnqYaOOsc",
				"gap": 1,
				"focus": -0.33333333333333337
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					38,
					0
				]
			]
		},
		{
			"type": "text",
			"version": 287,
			"versionNonce": 2052809500,
			"isDeleted": false,
			"id": "JZdY1Oyz",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 180,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 549.103759765625,
			"height": 140,
			"seed": 2012206364,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684085569287,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "REGISTROS\n    \n    - IP (Instruction Pointer): direccion de la instruccion en ejecucion\n\n    - SP (Stack Pointer): direccion del tope de la pila\n\n    - BP (Base Pointer): direccion del marco de pila activo",
			"rawText": "REGISTROS\n    \n    - IP (Instruction Pointer): direccion de la instruccion en ejecucion\n\n    - SP (Stack Pointer): direccion del tope de la pila\n\n    - BP (Base Pointer): direccion del marco de pila activo",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "REGISTROS\n    \n    - IP (Instruction Pointer): direccion de la instruccion en ejecucion\n\n    - SP (Stack Pointer): direccion del tope de la pila\n\n    - BP (Base Pointer): direccion del marco de pila activo",
			"lineHeight": 1.25,
			"baseline": 134
		},
		{
			"type": "text",
			"version": 68,
			"versionNonce": 1448986788,
			"isDeleted": false,
			"id": "KowtdUPK",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420,
			"y": 360,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 111.29994201660156,
			"height": 35,
			"seed": 599794212,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Ejercicio",
			"rawText": "Ejercicio",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Ejercicio",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 448,
			"versionNonce": 498828188,
			"isDeleted": false,
			"id": "4yK32t5j",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 400,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 325.7117919921875,
			"height": 120,
			"seed": 692073628,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Dado el siguiente programa de alto nivel:\n\n        a = 3;\n        b = a;\n\nEscribir el codigo destino MAPL:",
			"rawText": "Dado el siguiente programa de alto nivel:\n\n        a = 3;\n        b = a;\n\nEscribir el codigo destino MAPL:",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Dado el siguiente programa de alto nivel:\n\n        a = 3;\n        b = a;\n\nEscribir el codigo destino MAPL:",
			"lineHeight": 1.25,
			"baseline": 114
		},
		{
			"type": "text",
			"version": 749,
			"versionNonce": 1348801572,
			"isDeleted": false,
			"id": "Lz1ABHgj",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 540,
			"strokeColor": "#087f5b",
			"backgroundColor": "transparent",
			"width": 1034.6875,
			"height": 140,
			"seed": 1739124004,
			"groupIds": [],
			"roundness": null,
			"boundElements": null,
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\npushi 3           // Introduce un numero entero (2 bytes) en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\nstorei            // Extra n bytes de la pila, extrae una direccion de memoria de la pila (2 bytes) y el contenido es reemplazado",
			"rawText": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\npushi 3           // Introduce un numero entero (2 bytes) en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\nstorei            // Extra n bytes de la pila, extrae una direccion de memoria de la pila (2 bytes) y el contenido es reemplazado",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\npushi 3           // Introduce un numero entero (2 bytes) en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\nstorei            // Extra n bytes de la pila, extrae una direccion de memoria de la pila (2 bytes) y el contenido es reemplazado",
			"lineHeight": 1.25,
			"baseline": 134
		},
		{
			"type": "text",
			"version": 73,
			"versionNonce": 591441948,
			"isDeleted": false,
			"id": "E5gjVd2H",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420,
			"y": 720,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 145.23593139648438,
			"height": 35,
			"seed": 599794212,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083054653,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Ejercicio 2",
			"rawText": "Ejercicio 2",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Ejercicio 2",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 532,
			"versionNonce": 1155491620,
			"isDeleted": false,
			"id": "CrVv6iBi",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 760,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 325.7117919921875,
			"height": 140,
			"seed": 692073628,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083087742,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Dado el siguiente programa de alto nivel:\n\n        read myInteger;\n        real = myInteger * 3.4 - 7;\n        write real;\n\nEscribir el codigo destino MAPL:",
			"rawText": "Dado el siguiente programa de alto nivel:\n\n        read myInteger;\n        real = myInteger * 3.4 - 7;\n        write real;\n\nEscribir el codigo destino MAPL:",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Dado el siguiente programa de alto nivel:\n\n        read myInteger;\n        real = myInteger * 3.4 - 7;\n        write real;\n\nEscribir el codigo destino MAPL:",
			"lineHeight": 1.25,
			"baseline": 134
		},
		{
			"type": "text",
			"version": 1343,
			"versionNonce": 774157476,
			"isDeleted": false,
			"id": "yXfchQVI",
			"fillStyle": "hachure",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 920,
			"strokeColor": "#087f5b",
			"backgroundColor": "transparent",
			"width": 1040.7677001953125,
			"height": 320,
			"seed": 1739124004,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1684083604001,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\nini                // Lee un valor del teclado e introduce su representacion binaria en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\ni2f               // Necesario pasar a real por la operacion posterior\npushf 3.4        // Introduce un numero real (4 bytes) en la pila\nmulf              // Multiplicacion de reales (extraccion de los numero de la pila, se operan y se introduce el resultado en la pila)\npushi 7         \ni2f\nsubf\nstoref\npush 2\nloadf\noutf",
			"rawText": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\nini                // Lee un valor del teclado e introduce su representacion binaria en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\ni2f               // Necesario pasar a real por la operacion posterior\npushf 3.4        // Introduce un numero real (4 bytes) en la pila\nmulf              // Multiplicacion de reales (extraccion de los numero de la pila, se operan y se introduce el resultado en la pila)\npushi 7         \ni2f\nsubf\nstoref\npush 2\nloadf\noutf",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "pusha 0          // Introducimos una direccion (2 bytes) 0 de la pila\nini                // Lee un valor del teclado e introduce su representacion binaria en la pila\nstorei\npusha 2          // Introducimos una direccion (2 bytes) 2 de la pila\npusha 0          // Introduce un numero entero (2 bytes) en la pila\nloadi             // Extrae una direccion de memoria de la pila (2 bytes) e introduce el contenido en la pila de la direccion\ni2f               // Necesario pasar a real por la operacion posterior\npushf 3.4        // Introduce un numero real (4 bytes) en la pila\nmulf              // Multiplicacion de reales (extraccion de los numero de la pila, se operan y se introduce el resultado en la pila)\npushi 7         \ni2f\nsubf\nstoref\npush 2\nloadf\noutf",
			"lineHeight": 1.25,
			"baseline": 314
		}
	],
	"appState": {
		"theme": "dark",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#000000",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "hachure",
		"currentItemStrokeWidth": 2,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 0,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 630.5252408114346,
		"scrollY": 444.090909090909,
		"zoom": {
			"value": 0.55
		},
		"currentItemRoundness": "sharp",
		"gridSize": 20,
		"colorPalette": {},
		"currentStrokeOptions": null,
		"previousGridSize": null
	},
	"files": {}
}
```
%%