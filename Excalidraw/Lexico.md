---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
Éste va leyendo de la entrada carácter a carácter hasta 
que detecta una cadena válida (lexema) o una cadena errónea.  ^cCmVQ0Ak

Una vez encontrado un lexema, hace algo más: le asigna un 
número llamado Token (al cual se le puede ver como el tipo o 
la categoría a la que pertenece el lexema).  ^D06XttQW

Un ejemplo de esto sería el siguiente:
 ^W0UC3M1S

Salen parejas de (lexema, token). ^qZGx8CHs

Para representar dichos tokens habrá que realizar una transformación:
  ^64ScBamP

Para cada lexema de entrada se creara un objeto de la clase Token
el cual contendra:
- El lexema reconocido
- El tipo (categoria) del lexema (tokenType)
- La posicion del fichero (linea y columna) ^4BSJTqW9

En lugar de devolver la lista completa de tokens la forma de implementar esto
será implementando un método en el léxico que pida el siguiente token disponible.
Para poder hacer que el programa tenga fin habrá que definir constantes:
- static final int END = 0;
- static final int WHILE = 257;
- static final int IF = 260;

 ^XebM4T2w

EJEMPLO 0220 ^NPDHVpTh

Supóngase un programa cuyo bucle principal de ejecución va invocando 
a nextToken y, a continuación, imprime una traza del contenido del
objeto Token obtenido en cada llamada: ^efbjm3mW

Lexico lex = new Lexico(new FileReader(“prog.txt"));
Token token;
while ((token = lex.nextToken()).getType() != Lexico.END) {
    System.out.println(token.getLexeme());
    System.out.println(token.getType());
    System.out.println(token.getLine());
} ^X8WGIxMA

Supóngase la siguiente entrada en el fichero prog.txt:
    
    altura
    +
    1.75


Y finalmente supóngase que se han definido las siguientes constantes 
asociadas a los tokens del lenguaje:
 ^DAuUJkDq

… ^TRHolHcc

class Lexico { ^3UbUSK7i

static final int END = 0; ^1Lpa6eOP

static final int IDENT = 257; ^kdAga50M

static final int IF = 258; ^D4iOGvcJ

static final int LITENT = 259; ^XEvp2dS9

static final int LITREAL = 260; ^fi1v7wi4

} ^9pCoupVs

El resultado de ejecutar dicho programa seria el siguiente:
 ^xLBhnI37

ESPECIFICACIÓN LÉXICA

 ^pbKrp0rJ

1. Determinar tokens (como en el caso de los IDENT)
2. Definir patrones (determinar que lexemas pertenecen a cada token) ^uuC2pT8n

En el segundo caso determinar si un lexema es valido o no depende
de una serie de reglas que el creador del lenguaje haya definido. Para definir
estos patrones hay que hacer uso de los metalenguajes. ^zCP88YMW

METALENGUAJES

 ^puMO6C6U

Un metalenguaje deberá de ser preciso y concreto para que no haya problemas
de repetición o de confusión es los patrones.

Los dos metalenguajes más usados para reglar estos aspectos son los autómatas
finitos y las expresiones regulares. ^hJ5yYKUj

Autómatas finitos ^3bKNAex2

Habría que crear un autómata finito por cada token del lenguaje:
 ^53NDxBHr

Expresiones regulares ^6bEHRq0L

En nuestro caso es lo que vamos a usar ya que es mucho más cómodo y rápido.

Para crear una especificación habría que crear una expresión regular por
cada token del lenguaje: ^xzcZjvwv

TAREAS DE UN LÉXICO
 ^RqIjniz4

En cada llamada al método nextToken(), un analizador lexico tiene que realizar las siguientes tareas:
- Ignorar los comentarios
- Ignorar los espacios en blanco y saltos de linea
- Comprobar los patrones de la especificacion
- Notificar errores ^mLFxWdmd

FORMAS DE IMPLEMENTACIÓN ^DiAajKyq

Esta la implementación manual y la implementación a base de herramientas. En el primer
caso tenemos implementaciones con tablas de estados o implementaciones estructuradas. ^Jxuzncy6

IMPLEMENTACION CON HERRAMIENTAS - ANTLR ^Dt1Zl1Fn

ANTLR ya nos proporciona una clase equivalente al analizador lexico hecho a mano. De hecho, incluye:
- Constantes enteras para los tokens
- El método nextToken con la implementación de los patrones (por el método de tabla de estados)

Para probar dicha clase:
 ^oh0EDqGQ

import org.antlr.v4.runtime.*; ^1MmJ9KgG

public class Main { ^qhwvEL5r

public static void main(String[] args) throws Exception { ^3kVVRsSO

var lexer = new Lexicon(CharStreams.fromFileName("source.txt")); ^usRMhAUV

Token token; ^4P0CVu3i

while ((token = lexer.nextToken()).getType() != Lexicon.EOF) { ^zlvUFmpK

System.out.println("Token: " + token.getType()); ^eadn2SA4

System.out.println("Lexema: " + token.getText()); ^kG09Pax2

System.out.println("Linea: " + token.getLine()); ^4su3qRwB

System.out.println("Columna: " + token.getCharPositionInLine()); ^wK7qrHSF

} ^GlGsf7DB

System.out.println("Traza lexer finalizada"); ^smIxeS19

} ^Y81Lm1bq

} ^FtyjZ3FK

Operadores de ANTLR ^JY2JuEJq

En el caso de los operadores non-greedy lo que sucede es que cuando se 
encuentra un lexema válido se deja de reconocer. Por ejemplo:
- T: '@' .* '@';
    - Reconoce @hola@@adios@
- T: '@' .*? '@';
    - Reconoce @hola@ ^WW60P2XR

Prioridades de las Reglas ^ezn45XAM

Norma 1: Cuando una entrada puede ser reconocida por más de una regla, se 
         elige aquella que forme el lexema más largo.

Norma 2: Cuando varias reglas forman un lexema del mismo tamaño, se elige
         la regla que se haya definido primero ^O1KNUoEw

EJEMPLO 210 ^IVfyYQ5v

Hacer el analizador léxico del siguiente lenguaje usando ANTLR:
    
       




SOLUCIÓN:
    
        
 ^qAHYBxQQ

 edad = 65;         # Comentario de una línea
        print a
        read b;
        print "fin" ^18H9BjBf

        lexer grammar Lexicon;
        
        IGUAL : '=';
        PCOMA : ';';
        READ : 'read';
        PRINT: 'print';

        IDENT: [a-zA-Z][a-zA-Z0-9]*;
        LITINT: [0-9]+;
        STRING: '"' (~[\r\n"\])* '"';

        COMENTARIO: "#" .*? '\n\ -> skip;
        WS : [ \t\r\n]+ -> skip;
         ^dSlLGlmR


# Embedded files
5d441ba2f57191727439fa7246299577d36c08a8: [[Pasted Image 20230509154710_040.png]]
a934087a36a1727e74235cd94c0815015297628d: [[Pasted Image 20230509160432_862.png]]
a544b64ff967ebfc27af25d03d92c12d9bcc74ec: [[Pasted Image 20230509163042_214.png]]
52a4ff5e20e764194e44e396ee44828dce644abb: [[Pasted Image 20230509163312_292.png]]
9c900f8dbdbd9ce99ff523ec7e180075f9875554: [[Pasted Image 20230509170334_938.png]]

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
			"version": 650,
			"versionNonce": 250582902,
			"isDeleted": false,
			"id": "cCmVQ0Ak",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400.6225578325989,
			"y": -409.46558037860996,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 513.7437744140625,
			"height": 40,
			"seed": 1877154154,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327231,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Éste va leyendo de la entrada carácter a carácter hasta \nque detecta una cadena válida (lexema) o una cadena errónea. ",
			"rawText": "Éste va leyendo de la entrada carácter a carácter hasta \nque detecta una cadena válida (lexema) o una cadena errónea. ",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Éste va leyendo de la entrada carácter a carácter hasta \nque detecta una cadena válida (lexema) o una cadena errónea. ",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "freedraw",
			"version": 209,
			"versionNonce": 1259356906,
			"isDeleted": false,
			"id": "PRebIz-KzR8vv-bb7QAyV",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -135.4976540388334,
			"y": -369.0035265367512,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 50.47600072791343,
			"height": 0.9013571558555782,
			"seed": 1183620394,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327231,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.4506785779278175,
					0
				],
				[
					0.9013571558556066,
					0
				],
				[
					1.8027143117112132,
					0
				],
				[
					2.2533928896390023,
					0
				],
				[
					2.7040714675667914,
					0
				],
				[
					3.605428623422398,
					0
				],
				[
					4.957464357205794,
					0
				],
				[
					5.8588215130614,
					0
				],
				[
					6.7601786689169785,
					0
				],
				[
					7.210857246844768,
					0
				],
				[
					7.661535824772585,
					0
				],
				[
					8.562892980628163,
					0
				],
				[
					9.01357155855598,
					0
				],
				[
					9.46425013648377,
					0
				],
				[
					10.365607292339376,
					0
				],
				[
					10.816285870267166,
					0
				],
				[
					11.266964448194955,
					0
				],
				[
					11.717643026122772,
					0
				],
				[
					12.61900018197835,
					0
				],
				[
					13.069678759906168,
					0
				],
				[
					13.971035915761746,
					0
				],
				[
					14.421714493689564,
					0
				],
				[
					15.323071649545142,
					0
				],
				[
					15.77375022747296,
					0
				],
				[
					16.22442880540075,
					0
				],
				[
					17.125785961256355,
					0
				],
				[
					18.027143117111933,
					0
				],
				[
					18.47782169503975,
					0
				],
				[
					19.37917885089533,
					0
				],
				[
					20.280536006750935,
					0
				],
				[
					21.181893162606514,
					0
				],
				[
					22.08325031846212,
					0
				],
				[
					23.435286052245516,
					0
				],
				[
					24.336643208101123,
					0
				],
				[
					25.2380003639567,
					0
				],
				[
					26.139357519812307,
					0
				],
				[
					27.491393253595703,
					0
				],
				[
					28.39275040945131,
					0
				],
				[
					29.294107565306888,
					0
				],
				[
					30.195464721162494,
					0
				],
				[
					30.646143299090284,
					0
				],
				[
					31.096821877018073,
					0
				],
				[
					32.44885761080147,
					0
				],
				[
					33.350214766657075,
					0
				],
				[
					34.25157192251268,
					0
				],
				[
					34.70225050044047,
					0
				],
				[
					35.15292907836826,
					0
				],
				[
					36.054286234223866,
					0
				],
				[
					36.504964812151655,
					0
				],
				[
					36.95564339007947,
					0
				],
				[
					37.85700054593505,
					0
				],
				[
					38.75835770179066,
					0
				],
				[
					39.659714857646264,
					0
				],
				[
					40.11039343557405,
					0
				],
				[
					40.56107201350184,
					0
				],
				[
					41.46242916935745,
					0
				],
				[
					41.91310774728524,
					0
				],
				[
					42.36378632521303,
					0
				],
				[
					43.265143481068634,
					0
				],
				[
					43.71582205899642,
					0
				],
				[
					44.16650063692424,
					0
				],
				[
					44.61717921485203,
					0
				],
				[
					45.51853637070761,
					0
				],
				[
					45.969214948635425,
					0
				],
				[
					46.41989352656324,
					0
				],
				[
					46.870572104491,
					0
				],
				[
					47.77192926034664,
					0
				],
				[
					48.2226078382744,
					0
				],
				[
					48.67328641620222,
					0
				],
				[
					49.574643572057795,
					0
				],
				[
					50.02532214998561,
					0
				],
				[
					50.47600072791343,
					0
				],
				[
					50.47600072791343,
					-0.9013571558555782
				],
				[
					50.47600072791343,
					-0.9013571558555782
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 788,
			"versionNonce": 1597585590,
			"isDeleted": false,
			"id": "D06XttQW",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400.119162289069,
			"y": -343.1968832287261,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 496.83184814453125,
			"height": 60,
			"seed": 1877154154,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Una vez encontrado un lexema, hace algo más: le asigna un \nnúmero llamado Token (al cual se le puede ver como el tipo o \nla categoría a la que pertenece el lexema). ",
			"rawText": "Una vez encontrado un lexema, hace algo más: le asigna un \nnúmero llamado Token (al cual se le puede ver como el tipo o \nla categoría a la que pertenece el lexema). ",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Una vez encontrado un lexema, hace algo más: le asigna un \nnúmero llamado Token (al cual se le puede ver como el tipo o \nla categoría a la que pertenece el lexema). ",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"type": "freedraw",
			"version": 208,
			"versionNonce": 916215210,
			"isDeleted": false,
			"id": "FQLqDTPPG8bMCegYpZLqe",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -269.6847054415621,
			"y": -304.98343323877435,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 39.23599150454345,
			"height": 0.37726914908216713,
			"seed": 33509750,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.3772691490821103,
					0
				],
				[
					1.1318074472463877,
					0
				],
				[
					1.5090765963285548,
					0
				],
				[
					1.886345745410722,
					0
				],
				[
					2.2636148944928607,
					0
				],
				[
					3.0181531926571665,
					0
				],
				[
					3.3954223417393052,
					0
				],
				[
					3.772691490821444,
					0
				],
				[
					4.527229788985778,
					0
				],
				[
					4.9044989380678885,
					0
				],
				[
					5.281768087150056,
					0
				],
				[
					6.0363063853143615,
					0
				],
				[
					6.790844683478667,
					0
				],
				[
					7.168113832560806,
					0
				],
				[
					7.545382981642945,
					0
				],
				[
					8.29992127980725,
					0
				],
				[
					8.67719042888939,
					0
				],
				[
					9.054459577971556,
					0
				],
				[
					9.431728727053695,
					0
				],
				[
					10.186267025218001,
					0
				],
				[
					10.56353617430014,
					0
				],
				[
					10.940805323382278,
					0
				],
				[
					11.318074472464446,
					0
				],
				[
					12.072612770628723,
					0
				],
				[
					12.44988191971089,
					0
				],
				[
					12.827151068793057,
					0
				],
				[
					13.581689366957335,
					0
				],
				[
					13.958958516039502,
					-0.37726914908216713
				],
				[
					14.336227665121612,
					-0.37726914908216713
				],
				[
					15.090765963285946,
					-0.37726914908216713
				],
				[
					15.468035112368085,
					-0.37726914908216713
				],
				[
					15.845304261450224,
					-0.37726914908216713
				],
				[
					16.22257341053239,
					-0.37726914908216713
				],
				[
					16.97711170869667,
					-0.37726914908216713
				],
				[
					17.354380857778835,
					-0.37726914908216713
				],
				[
					17.731650006860974,
					-0.37726914908216713
				],
				[
					18.48618830502528,
					-0.37726914908216713
				],
				[
					18.86345745410742,
					-0.37726914908216713
				],
				[
					19.617995752271725,
					-0.37726914908216713
				],
				[
					20.372534050436002,
					-0.37726914908216713
				],
				[
					20.74980319951817,
					-0.37726914908216713
				],
				[
					21.504341497682447,
					-0.37726914908216713
				],
				[
					21.881610646764614,
					-0.37726914908216713
				],
				[
					22.63614894492889,
					-0.37726914908216713
				],
				[
					23.013418094011058,
					-0.37726914908216713
				],
				[
					23.767956392175364,
					-0.37726914908216713
				],
				[
					24.52249469033967,
					-0.37726914908216713
				],
				[
					24.89976383942181,
					-0.37726914908216713
				],
				[
					25.277032988503947,
					-0.37726914908216713
				],
				[
					26.031571286668253,
					-0.37726914908216713
				],
				[
					27.163378733914698,
					-0.37726914908216713
				],
				[
					27.540647882996836,
					-0.37726914908216713
				],
				[
					27.917917032079004,
					-0.37726914908216713
				],
				[
					28.295186181161142,
					-0.37726914908216713
				],
				[
					29.049724479325448,
					-0.37726914908216713
				],
				[
					29.426993628407587,
					-0.37726914908216713
				],
				[
					29.804262777489726,
					-0.37726914908216713
				],
				[
					30.55880107565406,
					-0.37726914908216713
				],
				[
					30.93607022473617,
					-0.37726914908216713
				],
				[
					31.313339373818337,
					-0.37726914908216713
				],
				[
					31.690608522900504,
					-0.37726914908216713
				],
				[
					32.44514682106478,
					-0.37726914908216713
				],
				[
					32.82241597014695,
					-0.37726914908216713
				],
				[
					33.19968511922909,
					-0.37726914908216713
				],
				[
					33.95422341739339,
					-0.37726914908216713
				],
				[
					34.70876171555767,
					0
				],
				[
					35.46330001372198,
					0
				],
				[
					36.21783831188628,
					0
				],
				[
					36.59510746096842,
					0
				],
				[
					37.34964575913273,
					0
				],
				[
					37.726914908214866,
					0
				],
				[
					38.104184057297005,
					0
				],
				[
					38.48145320637917,
					0
				],
				[
					39.23599150454345,
					0
				],
				[
					39.23599150454345,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 234,
			"versionNonce": 1346154998,
			"isDeleted": false,
			"id": "W0UC3M1S",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -399.3580425334577,
			"y": -268.79328688124497,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 297.5998229980469,
			"height": 40,
			"seed": 887180662,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Un ejemplo de esto sería el siguiente:\n",
			"rawText": "Un ejemplo de esto sería el siguiente:\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Un ejemplo de esto sería el siguiente:\n",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "freedraw",
			"version": 122,
			"versionNonce": 1687687274,
			"isDeleted": false,
			"id": "5G5l6i68B-XrkqaSBT8y2",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -326.03961918551977,
			"y": -223.82689219189484,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 8.744399114891678,
			"height": 16.816152144022453,
			"seed": 631277558,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					6.053814771848067
				],
				[
					-0.6726460857609027,
					8.071753029130775
				],
				[
					-0.6726460857609027,
					10.089691286413426
				],
				[
					-1.3452921715218054,
					11.434983457935232
				],
				[
					-1.3452921715218054,
					12.780275629457037
				],
				[
					-1.3452921715218054,
					14.125567800978843
				],
				[
					-2.6905843430436107,
					14.798213886739745
				],
				[
					-2.6905843430436107,
					15.470859972500648
				],
				[
					-2.017938257282708,
					16.816152144022453
				],
				[
					0,
					16.816152144022453
				],
				[
					1.3452921715218054,
					16.816152144022453
				],
				[
					2.017938257282708,
					16.816152144022453
				],
				[
					2.6905843430436107,
					16.816152144022453
				],
				[
					4.035876514565416,
					16.816152144022453
				],
				[
					4.708522600326319,
					16.816152144022453
				],
				[
					5.381168686087165,
					16.816152144022453
				],
				[
					6.053814771848067,
					16.816152144022453
				],
				[
					6.053814771848067,
					16.816152144022453
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 119,
			"versionNonce": 1560216374,
			"isDeleted": false,
			"id": "RfwEiQj-8i6TUdHwrgxtW",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -311.9140513845409,
			"y": -222.48160002037304,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.3991069433699295,
			"height": 16.816152144022453,
			"seed": 176396854,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-0.6726460857609027
				],
				[
					-0.6726460857609027,
					-0.6726460857609027
				],
				[
					-2.017938257282708,
					2.017938257282708
				],
				[
					-2.017938257282708,
					4.708522600326262
				],
				[
					-3.3632304288045134,
					6.72646085760897
				],
				[
					-3.3632304288045134,
					8.744399114891621
				],
				[
					-4.035876514565416,
					10.76233737217433
				],
				[
					-4.035876514565416,
					12.780275629457037
				],
				[
					-5.381168686087221,
					14.125567800978843
				],
				[
					-5.381168686087221,
					15.470859972500648
				],
				[
					-4.708522600326319,
					16.14350605826155
				],
				[
					-4.035876514565416,
					16.14350605826155
				],
				[
					-3.3632304288045134,
					16.14350605826155
				],
				[
					-2.017938257282708,
					16.14350605826155
				],
				[
					-1.3452921715218054,
					16.14350605826155
				],
				[
					-0.6726460857609027,
					16.14350605826155
				],
				[
					0.6726460857609027,
					16.14350605826155
				],
				[
					2.017938257282708,
					16.14350605826155
				],
				[
					2.017938257282708,
					15.470859972500648
				],
				[
					2.017938257282708,
					15.470859972500648
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 105,
			"versionNonce": 953053994,
			"isDeleted": false,
			"id": "6NfQt9HtfYf6RatujniuE",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -315.94992789910634,
			"y": -213.73720090548142,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.053814771848124,
			"height": 3.3632304288044566,
			"seed": 1827874806,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.017938257282708,
					0
				],
				[
					4.035876514565416,
					-1.3452921715217485
				],
				[
					5.381168686087221,
					-2.017938257282651
				],
				[
					6.053814771848124,
					-3.3632304288044566
				],
				[
					6.053814771848124,
					-3.3632304288044566
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 105,
			"versionNonce": 1474636918,
			"isDeleted": false,
			"id": "W7xbBuENj0esRrhu6YGPt",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -313.25934355606273,
			"y": -221.80895393461213,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 4.708522600326319,
			"height": 2.017938257282708,
			"seed": 425491702,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					-0.6726460857609027
				],
				[
					3.3632304288045134,
					-0.6726460857609027
				],
				[
					4.035876514565416,
					-2.017938257282708
				],
				[
					4.708522600326319,
					-2.017938257282708
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 110,
			"versionNonce": 1705672170,
			"isDeleted": false,
			"id": "dt86_XGOhO5hMvdSllLqI",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -304.514944441171,
			"y": -223.15424610613394,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 3.3632304288044566,
			"height": 12.780275629457037,
			"seed": 1072910838,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					4.035876514565416
				],
				[
					0,
					6.053814771848067
				],
				[
					1.3452921715218054,
					8.071753029130775
				],
				[
					1.3452921715218054,
					9.417045200652524
				],
				[
					1.3452921715218054,
					10.76233737217433
				],
				[
					2.6905843430436107,
					12.107629543696135
				],
				[
					2.6905843430436107,
					12.780275629457037
				],
				[
					3.3632304288044566,
					12.780275629457037
				],
				[
					3.3632304288044566,
					12.780275629457037
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 112,
			"versionNonce": 2125737398,
			"isDeleted": false,
			"id": "V2QusPDTrnof2gMomj3Ab",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -305.8602366126927,
			"y": -208.3560322193942,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 4.708522600326205,
			"height": 14.125567800978843,
			"seed": 1112185066,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.3452921715218054
				],
				[
					0,
					-2.017938257282708
				],
				[
					0,
					-2.6905843430436107
				],
				[
					0.6726460857608458,
					-4.035876514565416
				],
				[
					0.6726460857608458,
					-4.708522600326319
				],
				[
					2.017938257282651,
					-6.053814771848124
				],
				[
					2.017938257282651,
					-7.399106943369873
				],
				[
					2.690584343043554,
					-10.089691286413426
				],
				[
					2.690584343043554,
					-12.107629543696135
				],
				[
					4.035876514565359,
					-13.45292171521794
				],
				[
					4.035876514565359,
					-14.125567800978843
				],
				[
					4.708522600326205,
					-14.125567800978843
				],
				[
					4.708522600326205,
					-14.125567800978843
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 117,
			"versionNonce": 406270122,
			"isDeleted": false,
			"id": "3rTz06T1Qk3EZ88DZ918x",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -298.4611296693229,
			"y": -221.80895393461213,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.053814771848124,
			"height": 11.434983457935232,
			"seed": 1907723126,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					0
				],
				[
					0.6726460857609027,
					1.3452921715218054
				],
				[
					0.6726460857609027,
					2.6905843430436107
				],
				[
					0.6726460857609027,
					4.035876514565359
				],
				[
					-0.6726460857609027,
					6.053814771848067
				],
				[
					-0.6726460857609027,
					7.399106943369816
				],
				[
					-0.6726460857609027,
					8.744399114891621
				],
				[
					-0.6726460857609027,
					10.089691286413426
				],
				[
					-0.6726460857609027,
					10.76233737217433
				],
				[
					-0.6726460857609027,
					11.434983457935232
				],
				[
					0,
					11.434983457935232
				],
				[
					2.017938257282708,
					11.434983457935232
				],
				[
					3.3632304288045134,
					11.434983457935232
				],
				[
					3.3632304288045134,
					10.76233737217433
				],
				[
					4.708522600326319,
					10.76233737217433
				],
				[
					5.381168686087221,
					10.76233737217433
				],
				[
					5.381168686087221,
					9.417045200652524
				],
				[
					5.381168686087221,
					9.417045200652524
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 107,
			"versionNonce": 244385526,
			"isDeleted": false,
			"id": "2rAyixdhpcwMBB40XMQ3Z",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -298.4611296693229,
			"y": -215.75513916276407,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.726460857609027,
			"height": 4.035876514565359,
			"seed": 1396166646,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					1.3452921715218054,
					-0.6726460857609027
				],
				[
					2.6905843430436107,
					-0.6726460857609027
				],
				[
					4.708522600326319,
					-0.6726460857609027
				],
				[
					6.053814771848124,
					-2.690584343043554
				],
				[
					6.726460857609027,
					-2.690584343043554
				],
				[
					6.726460857609027,
					-4.035876514565359
				],
				[
					6.726460857609027,
					-4.035876514565359
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 606047082,
			"isDeleted": false,
			"id": "qujhyrbzwS_6g8u7NTs0i",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -299.8064218408447,
			"y": -221.13630784885123,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.3991069433699295,
			"height": 3.3632304288045134,
			"seed": 1145640502,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.3452921715218054
				],
				[
					1.3452921715218054,
					-1.3452921715218054
				],
				[
					1.3452921715218054,
					-2.017938257282708
				],
				[
					2.6905843430436107,
					-2.017938257282708
				],
				[
					4.035876514565416,
					-2.017938257282708
				],
				[
					4.708522600326319,
					-2.017938257282708
				],
				[
					6.053814771848124,
					-3.3632304288045134
				],
				[
					7.3991069433699295,
					-3.3632304288045134
				],
				[
					7.3991069433699295,
					-3.3632304288045134
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 158,
			"versionNonce": 1476442166,
			"isDeleted": false,
			"id": "gFtBvE6N8W5Syl8NHaSRb",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -288.37143838290945,
			"y": -225.84483044917755,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 13.45292171521794,
			"height": 20.179382572826967,
			"seed": 1050785258,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					6.053814771848124
				],
				[
					0,
					9.41704520065258
				],
				[
					0,
					12.780275629457037
				],
				[
					-0.6726460857609027,
					15.470859972500648
				],
				[
					-0.6726460857609027,
					16.816152144022453
				],
				[
					-0.6726460857609027,
					18.16144431554426
				],
				[
					-0.6726460857609027,
					19.506736487066064
				],
				[
					-0.6726460857609027,
					20.179382572826967
				],
				[
					-0.6726460857609027,
					19.506736487066064
				],
				[
					-0.6726460857609027,
					18.16144431554426
				],
				[
					-1.3452921715217485,
					17.488798229783356
				],
				[
					-1.3452921715217485,
					16.816152144022453
				],
				[
					-1.3452921715217485,
					15.470859972500648
				],
				[
					-1.3452921715217485,
					14.798213886739745
				],
				[
					-1.3452921715217485,
					13.45292171521794
				],
				[
					-1.3452921715217485,
					12.107629543696135
				],
				[
					-1.3452921715217485,
					10.762337372174386
				],
				[
					-1.3452921715217485,
					9.41704520065258
				],
				[
					-1.3452921715217485,
					8.071753029130775
				],
				[
					-1.3452921715217485,
					7.3991069433699295
				],
				[
					0,
					7.3991069433699295
				],
				[
					0,
					6.726460857609027
				],
				[
					0.6726460857609027,
					7.3991069433699295
				],
				[
					0.6726460857609027,
					8.071753029130775
				],
				[
					2.017938257282708,
					9.41704520065258
				],
				[
					2.017938257282708,
					10.089691286413483
				],
				[
					2.690584343043554,
					10.762337372174386
				],
				[
					2.690584343043554,
					12.107629543696135
				],
				[
					3.3632304288044566,
					12.107629543696135
				],
				[
					3.3632304288044566,
					12.780275629457037
				],
				[
					4.708522600326262,
					12.780275629457037
				],
				[
					6.053814771848067,
					12.780275629457037
				],
				[
					7.399106943369873,
					12.107629543696135
				],
				[
					7.399106943369873,
					10.089691286413483
				],
				[
					8.744399114891678,
					8.744399114891678
				],
				[
					8.744399114891678,
					7.3991069433699295
				],
				[
					8.744399114891678,
					6.053814771848124
				],
				[
					8.744399114891678,
					4.708522600326319
				],
				[
					8.744399114891678,
					3.3632304288045134
				],
				[
					8.744399114891678,
					2.017938257282708
				],
				[
					8.744399114891678,
					0.6726460857609027
				],
				[
					8.744399114891678,
					1.3452921715218054
				],
				[
					8.744399114891678,
					2.017938257282708
				],
				[
					8.744399114891678,
					5.381168686087221
				],
				[
					8.744399114891678,
					7.3991069433699295
				],
				[
					8.744399114891678,
					9.41704520065258
				],
				[
					8.744399114891678,
					10.762337372174386
				],
				[
					8.744399114891678,
					12.107629543696135
				],
				[
					8.744399114891678,
					12.780275629457037
				],
				[
					8.744399114891678,
					14.125567800978843
				],
				[
					10.089691286413483,
					14.125567800978843
				],
				[
					10.089691286413483,
					12.780275629457037
				],
				[
					10.089691286413483,
					11.434983457935232
				],
				[
					10.762337372174386,
					11.434983457935232
				],
				[
					11.434983457935289,
					11.434983457935232
				],
				[
					11.434983457935289,
					12.107629543696135
				],
				[
					12.107629543696191,
					12.107629543696135
				],
				[
					12.107629543696191,
					12.107629543696135
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 134,
			"versionNonce": 799968810,
			"isDeleted": false,
			"id": "pC4g_WhTM4kHeYEMbzK0V",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -271.555286238887,
			"y": -222.48160002037304,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 11.434983457935289,
			"height": 15.470859972500648,
			"seed": 181465910,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					-1.3452921715218054,
					3.3632304288045134
				],
				[
					-2.6905843430436107,
					6.053814771848124
				],
				[
					-3.3632304288045134,
					8.071753029130832
				],
				[
					-4.708522600326319,
					11.434983457935289
				],
				[
					-4.708522600326319,
					13.452921715217997
				],
				[
					-6.053814771848124,
					14.798213886739745
				],
				[
					-6.053814771848124,
					15.470859972500648
				],
				[
					-5.381168686087221,
					14.125567800978843
				],
				[
					-5.381168686087221,
					12.780275629457094
				],
				[
					-4.035876514565416,
					11.434983457935289
				],
				[
					-4.035876514565416,
					10.08969128641354
				],
				[
					-2.6905843430436107,
					8.744399114891735
				],
				[
					-2.6905843430436107,
					8.071753029130832
				],
				[
					-2.6905843430436107,
					7.3991069433699295
				],
				[
					-2.017938257282708,
					6.053814771848124
				],
				[
					-2.017938257282708,
					4.708522600326319
				],
				[
					-1.3452921715218054,
					4.035876514565416
				],
				[
					-1.3452921715218054,
					3.3632304288045134
				],
				[
					0,
					2.017938257282708
				],
				[
					0.6726460857609027,
					2.017938257282708
				],
				[
					0.6726460857609027,
					2.6905843430436107
				],
				[
					0.6726460857609027,
					4.035876514565416
				],
				[
					2.017938257282708,
					5.381168686087221
				],
				[
					2.017938257282708,
					6.053814771848124
				],
				[
					2.017938257282708,
					6.726460857609027
				],
				[
					3.363230428804485,
					8.744399114891735
				],
				[
					3.363230428804485,
					10.08969128641354
				],
				[
					4.035876514565388,
					10.762337372174386
				],
				[
					4.035876514565388,
					11.434983457935289
				],
				[
					4.035876514565388,
					12.780275629457094
				],
				[
					5.381168686087165,
					12.780275629457094
				],
				[
					5.381168686087165,
					13.452921715217997
				],
				[
					5.381168686087165,
					12.107629543696191
				],
				[
					5.381168686087165,
					12.107629543696191
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 1390952822,
			"isDeleted": false,
			"id": "mDg1FND_DCltfg-yc6PK2",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -276.2638088392134,
			"y": -211.71926264819865,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.3991069433699295,
			"height": 3.3632304288044566,
			"seed": 516730026,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.017938257282708,
					0
				],
				[
					2.6905843430436107,
					-1.3452921715217485
				],
				[
					4.035876514565416,
					-1.3452921715217485
				],
				[
					4.708522600326319,
					-1.3452921715217485
				],
				[
					5.381168686087221,
					-2.017938257282651
				],
				[
					6.726460857609027,
					-2.017938257282651
				],
				[
					7.3991069433699295,
					-3.3632304288044566
				],
				[
					7.3991069433699295,
					-3.3632304288044566
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 110,
			"versionNonce": 1607416042,
			"isDeleted": false,
			"id": "_kdEf0zIdwcU-5qzaHN0A",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -217.74359937801523,
			"y": -221.13630784885123,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 17.488798229783356,
			"height": 2.017938257282708,
			"seed": 1273344310,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.6905843430436107,
					0
				],
				[
					6.72646085760897,
					0
				],
				[
					8.744399114891678,
					0
				],
				[
					12.107629543696191,
					-1.3452921715218054
				],
				[
					14.125567800978843,
					-1.3452921715218054
				],
				[
					15.470859972500648,
					-2.017938257282708
				],
				[
					16.816152144022453,
					-2.017938257282708
				],
				[
					17.488798229783356,
					-2.017938257282708
				],
				[
					17.488798229783356,
					-2.017938257282708
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 109,
			"versionNonce": 848077494,
			"isDeleted": false,
			"id": "APgxu_hvOCjcNvM22H1jA",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -207.6539080916018,
			"y": -220.46366176309033,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.6726460857609027,
			"height": 10.089691286413483,
			"seed": 186793386,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					0
				],
				[
					0.6726460857609027,
					2.017938257282708
				],
				[
					0.6726460857609027,
					3.3632304288045134
				],
				[
					0.6726460857609027,
					4.708522600326319
				],
				[
					0.6726460857609027,
					6.053814771848124
				],
				[
					0.6726460857609027,
					8.071753029130832
				],
				[
					0.6726460857609027,
					8.744399114891678
				],
				[
					0.6726460857609027,
					9.41704520065258
				],
				[
					0.6726460857609027,
					10.089691286413483
				],
				[
					0.6726460857609027,
					10.089691286413483
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 132,
			"versionNonce": 67931050,
			"isDeleted": false,
			"id": "CELDS_d3TTyiU9iZb9DGg",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -194.20098637638375,
			"y": -221.13630784885123,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.72646085760897,
			"height": 10.089691286413483,
			"seed": 1889957418,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.3452921715218054,
					0
				],
				[
					-3.3632304288044566,
					0
				],
				[
					-4.708522600326262,
					0
				],
				[
					-4.708522600326262,
					0.6726460857609027
				],
				[
					-6.053814771848067,
					1.3452921715218054
				],
				[
					-6.053814771848067,
					2.6905843430436107
				],
				[
					-6.72646085760897,
					4.035876514565416
				],
				[
					-6.72646085760897,
					6.053814771848124
				],
				[
					-6.72646085760897,
					8.071753029130832
				],
				[
					-6.72646085760897,
					8.744399114891735
				],
				[
					-6.72646085760897,
					9.41704520065258
				],
				[
					-6.053814771848067,
					9.41704520065258
				],
				[
					-4.708522600326262,
					10.089691286413483
				],
				[
					-3.3632304288044566,
					10.089691286413483
				],
				[
					-2.017938257282708,
					9.41704520065258
				],
				[
					-1.3452921715218054,
					8.744399114891735
				],
				[
					-1.3452921715218054,
					7.3991069433699295
				],
				[
					-0.6726460857609027,
					6.726460857609027
				],
				[
					-0.6726460857609027,
					6.053814771848124
				],
				[
					-0.6726460857609027,
					4.708522600326319
				],
				[
					-0.6726460857609027,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					3.3632304288045134
				],
				[
					-1.3452921715218054,
					1.3452921715218054
				],
				[
					-2.017938257282708,
					1.3452921715218054
				],
				[
					-2.017938257282708,
					0.6726460857609027
				],
				[
					-4.035876514565359,
					0.6726460857609027
				],
				[
					-4.708522600326262,
					0.6726460857609027
				],
				[
					-6.053814771848067,
					1.3452921715218054
				],
				[
					-6.72646085760897,
					2.6905843430436107
				],
				[
					-6.72646085760897,
					4.035876514565416
				],
				[
					-6.72646085760897,
					5.381168686087221
				],
				[
					-6.72646085760897,
					6.726460857609027
				],
				[
					-6.72646085760897,
					6.726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 110,
			"versionNonce": 2039667702,
			"isDeleted": false,
			"id": "LBjOhEAQnTpUqQcxrdxzj",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -192.85569420486195,
			"y": -221.80895393461213,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 14.125567800978843,
			"seed": 439160502,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					5.381168686087221
				],
				[
					0,
					7.3991069433699295
				],
				[
					0,
					8.744399114891735
				],
				[
					0,
					10.762337372174386
				],
				[
					0,
					12.107629543696191
				],
				[
					0,
					13.45292171521794
				],
				[
					0,
					14.125567800978843
				],
				[
					0,
					14.125567800978843
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 1116833386,
			"isDeleted": false,
			"id": "H10HMc5ey8yQ5t09YfnXl",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -192.85569420486195,
			"y": -213.0645548197204,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.053814771848067,
			"height": 6.726460857609027,
			"seed": 1184602154,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.3452921715218054
				],
				[
					0.6726460857609027,
					-2.6905843430436107
				],
				[
					2.017938257282708,
					-3.3632304288045134
				],
				[
					3.3632304288045134,
					-5.381168686087221
				],
				[
					4.035876514565359,
					-5.381168686087221
				],
				[
					4.035876514565359,
					-6.053814771848124
				],
				[
					5.381168686087165,
					-6.053814771848124
				],
				[
					6.053814771848067,
					-6.726460857609027
				],
				[
					6.053814771848067,
					-6.726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 123,
			"versionNonce": 234876214,
			"isDeleted": false,
			"id": "dTqji9xf1G1A690UEhEdm",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -192.18304811910116,
			"y": -217.77307742004672,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 13.45292171521794,
			"height": 6.053814771848067,
			"seed": 681930166,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					3.3632304288045134
				],
				[
					0.6726460857609027,
					4.035876514565416
				],
				[
					2.6905843430436107,
					6.053814771848067
				],
				[
					4.035876514565359,
					6.053814771848067
				],
				[
					5.381168686087165,
					6.053814771848067
				],
				[
					6.053814771848067,
					6.053814771848067
				],
				[
					6.72646085760897,
					6.053814771848067
				],
				[
					6.72646085760897,
					5.381168686087221
				],
				[
					7.399106943369873,
					5.381168686087221
				],
				[
					8.744399114891678,
					5.381168686087221
				],
				[
					9.41704520065258,
					5.381168686087221
				],
				[
					10.089691286413483,
					5.381168686087221
				],
				[
					11.434983457935232,
					5.381168686087221
				],
				[
					11.434983457935232,
					4.708522600326319
				],
				[
					11.434983457935232,
					3.3632304288045134
				],
				[
					11.434983457935232,
					4.708522600326319
				],
				[
					12.107629543696135,
					4.708522600326319
				],
				[
					12.780275629457037,
					4.708522600326319
				],
				[
					13.45292171521794,
					4.708522600326319
				],
				[
					13.45292171521794,
					4.035876514565416
				],
				[
					13.45292171521794,
					4.035876514565416
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 117,
			"versionNonce": 1143548202,
			"isDeleted": false,
			"id": "DI5m9UXjGHNLQFezdZzSP",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -178.7301264038831,
			"y": -221.13630784885123,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 5.381168686087221,
			"height": 11.434983457935289,
			"seed": 143148534,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					-0.6726460857609027,
					1.3452921715218054
				],
				[
					-0.6726460857609027,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					4.035876514565416
				],
				[
					-1.3452921715218054,
					5.381168686087221
				],
				[
					-1.3452921715218054,
					6.726460857609027
				],
				[
					-1.3452921715218054,
					7.3991069433699295
				],
				[
					-2.6905843430436107,
					9.41704520065258
				],
				[
					-2.6905843430436107,
					10.089691286413483
				],
				[
					-2.6905843430436107,
					11.434983457935289
				],
				[
					-1.3452921715218054,
					11.434983457935289
				],
				[
					-0.6726460857609027,
					11.434983457935289
				],
				[
					0,
					11.434983457935289
				],
				[
					0.6726460857609027,
					11.434983457935289
				],
				[
					2.017938257282708,
					11.434983457935289
				],
				[
					2.017938257282708,
					10.089691286413483
				],
				[
					2.6905843430436107,
					10.089691286413483
				],
				[
					2.6905843430436107,
					10.089691286413483
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 106,
			"versionNonce": 1295570550,
			"isDeleted": false,
			"id": "-FFm0KaCFISomgbocLnzA",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -180.74806466116593,
			"y": -214.4098469912422,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.053814771848124,
			"height": 0.6726460857609027,
			"seed": 534473334,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.017938257282708,
					0
				],
				[
					4.035876514565416,
					0
				],
				[
					5.381168686087221,
					0
				],
				[
					5.381168686087221,
					-0.6726460857609027
				],
				[
					6.053814771848124,
					-0.6726460857609027
				],
				[
					6.053814771848124,
					-0.6726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 1614705642,
			"isDeleted": false,
			"id": "Np9czuzyrrAcUAB3HJ_Qo",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -182.76600291844852,
			"y": -219.79101567732943,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.399106943369873,
			"height": 2.6905843430436107,
			"seed": 260233962,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715217485,
					0
				],
				[
					2.690584343043554,
					-1.3452921715218054
				],
				[
					3.3632304288044566,
					-1.3452921715218054
				],
				[
					4.708522600326262,
					-2.017938257282708
				],
				[
					5.381168686087165,
					-2.017938257282708
				],
				[
					6.053814771848067,
					-2.017938257282708
				],
				[
					6.053814771848067,
					-2.6905843430436107
				],
				[
					7.399106943369873,
					-2.6905843430436107
				],
				[
					7.399106943369873,
					-2.6905843430436107
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 151,
			"versionNonce": 537040822,
			"isDeleted": false,
			"id": "BltpexMbkrULOZmzcQTfH",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -168.64043511746968,
			"y": -223.82689219189484,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 10.089691286413483,
			"height": 14.798213886739802,
			"seed": 1197666038,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					6.053814771848124
				],
				[
					-0.6726460857609027,
					8.071753029130832
				],
				[
					-2.017938257282708,
					10.08969128641354
				],
				[
					-2.017938257282708,
					11.434983457935346
				],
				[
					-2.017938257282708,
					12.780275629457094
				],
				[
					-2.017938257282708,
					14.1255678009789
				],
				[
					-2.017938257282708,
					14.798213886739802
				],
				[
					-2.017938257282708,
					12.780275629457094
				],
				[
					-2.017938257282708,
					11.434983457935346
				],
				[
					-2.6905843430436107,
					9.417045200652638
				],
				[
					-2.6905843430436107,
					7.3991069433699295
				],
				[
					-2.6905843430436107,
					5.381168686087221
				],
				[
					-2.6905843430436107,
					3.3632304288045134
				],
				[
					-2.6905843430436107,
					2.017938257282708
				],
				[
					-2.6905843430436107,
					1.3452921715218054
				],
				[
					-2.6905843430436107,
					0.6726460857609027
				],
				[
					-2.017938257282708,
					0.6726460857609027
				],
				[
					-1.3452921715218054,
					0.6726460857609027
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					4.708522600326319
				],
				[
					0,
					5.381168686087221
				],
				[
					0,
					6.053814771848124
				],
				[
					0,
					6.726460857609027
				],
				[
					0,
					8.071753029130832
				],
				[
					1.3452921715218054,
					8.744399114891735
				],
				[
					1.3452921715218054,
					10.08969128641354
				],
				[
					2.017938257282708,
					10.08969128641354
				],
				[
					2.017938257282708,
					12.107629543696191
				],
				[
					3.3632304288044566,
					12.107629543696191
				],
				[
					3.3632304288044566,
					13.452921715217997
				],
				[
					4.035876514565359,
					13.452921715217997
				],
				[
					4.035876514565359,
					14.1255678009789
				],
				[
					4.708522600326262,
					14.1255678009789
				],
				[
					6.053814771848067,
					13.452921715217997
				],
				[
					6.053814771848067,
					12.107629543696191
				],
				[
					6.053814771848067,
					11.434983457935346
				],
				[
					6.053814771848067,
					10.08969128641354
				],
				[
					6.053814771848067,
					8.744399114891735
				],
				[
					6.053814771848067,
					6.726460857609027
				],
				[
					6.72646085760897,
					5.381168686087221
				],
				[
					6.72646085760897,
					4.035876514565416
				],
				[
					6.72646085760897,
					2.6905843430436107
				],
				[
					6.72646085760897,
					2.017938257282708
				],
				[
					7.399106943369873,
					2.017938257282708
				],
				[
					7.399106943369873,
					4.035876514565416
				],
				[
					7.399106943369873,
					5.381168686087221
				],
				[
					7.399106943369873,
					6.726460857609027
				],
				[
					7.399106943369873,
					6.726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 112,
			"versionNonce": 1222403754,
			"isDeleted": false,
			"id": "bu7Spv4PZ1ytrCIKCT1Ai",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -342.855771329542,
			"y": -180.10489661743674,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 3.3632304288045134,
			"height": 11.434983457935232,
			"seed": 754197366,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.3452921715218054,
					0
				],
				[
					-2.017938257282708,
					0
				],
				[
					-3.3632304288045134,
					2.017938257282651
				],
				[
					-3.3632304288045134,
					3.3632304288044566
				],
				[
					-3.3632304288045134,
					4.708522600326262
				],
				[
					-3.3632304288045134,
					6.05381477184801
				],
				[
					-3.3632304288045134,
					6.726460857608913
				],
				[
					-3.3632304288045134,
					8.744399114891621
				],
				[
					-2.6905843430436107,
					9.417045200652524
				],
				[
					-2.6905843430436107,
					10.089691286413426
				],
				[
					-1.3452921715218054,
					10.089691286413426
				],
				[
					-1.3452921715218054,
					11.434983457935232
				],
				[
					-0.6726460857609027,
					11.434983457935232
				],
				[
					-0.6726460857609027,
					11.434983457935232
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 111,
			"versionNonce": 243413238,
			"isDeleted": false,
			"id": "6jgry8bNKaMEwVGXO0ADc",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -338.8198948149766,
			"y": -178.08695836015409,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 3.3632304288045134,
			"height": 8.071753029130775,
			"seed": 2057358710,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.3452921715218054,
					0
				],
				[
					-1.3452921715218054,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					2.6905843430436107
				],
				[
					-1.3452921715218054,
					4.035876514565359
				],
				[
					-1.3452921715218054,
					4.708522600326262
				],
				[
					-1.3452921715218054,
					6.053814771848067
				],
				[
					-1.3452921715218054,
					6.72646085760897
				],
				[
					-1.3452921715218054,
					8.071753029130775
				],
				[
					-0.6726460857609027,
					8.071753029130775
				],
				[
					0.6726460857609027,
					8.071753029130775
				],
				[
					1.3452921715218054,
					8.071753029130775
				],
				[
					2.017938257282708,
					8.071753029130775
				],
				[
					2.017938257282708,
					8.071753029130775
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 138,
			"versionNonce": 917373290,
			"isDeleted": false,
			"id": "goh8jmc5vc2ypQxq5duF5",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -328.73020352856315,
			"y": -168.6699131595015,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.053814771848124,
			"height": 23.542613001631423,
			"seed": 1789327402,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					4.035876514565416
				],
				[
					0,
					4.708522600326319
				],
				[
					0,
					6.72646085760897
				],
				[
					0,
					8.071753029130775
				],
				[
					0,
					9.41704520065258
				],
				[
					0,
					10.76233737217433
				],
				[
					0,
					13.45292171521794
				],
				[
					0,
					14.798213886739745
				],
				[
					0,
					16.14350605826155
				],
				[
					0,
					16.816152144022453
				],
				[
					0,
					16.14350605826155
				],
				[
					0,
					14.798213886739745
				],
				[
					0,
					13.45292171521794
				],
				[
					0,
					11.434983457935232
				],
				[
					0,
					9.41704520065258
				],
				[
					0,
					6.72646085760897
				],
				[
					0,
					4.035876514565416
				],
				[
					0,
					2.017938257282708
				],
				[
					0.6726460857609027,
					0
				],
				[
					0.6726460857609027,
					-2.017938257282708
				],
				[
					2.017938257282708,
					-3.3632304288045134
				],
				[
					2.017938257282708,
					-5.381168686087221
				],
				[
					2.6905843430436107,
					-6.053814771848124
				],
				[
					2.6905843430436107,
					-6.72646085760897
				],
				[
					3.3632304288045134,
					-6.72646085760897
				],
				[
					4.708522600326319,
					-6.72646085760897
				],
				[
					5.381168686087221,
					-6.72646085760897
				],
				[
					5.381168686087221,
					-6.053814771848124
				],
				[
					5.381168686087221,
					-4.708522600326319
				],
				[
					5.381168686087221,
					-4.035876514565416
				],
				[
					5.381168686087221,
					-2.6905843430436107
				],
				[
					5.381168686087221,
					-2.017938257282708
				],
				[
					5.381168686087221,
					-0.6726460857609027
				],
				[
					5.381168686087221,
					0
				],
				[
					5.381168686087221,
					0.6726460857609027
				],
				[
					6.053814771848124,
					0.6726460857609027
				],
				[
					6.053814771848124,
					0.6726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 114,
			"versionNonce": 1413259830,
			"isDeleted": false,
			"id": "zfpFaKebUW5gZrHOer5Df",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -319.98580441367153,
			"y": -172.70578967406692,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 4.708522600326262,
			"height": 8.744399114891678,
			"seed": 1103530474,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					4.708522600326319
				],
				[
					0,
					5.381168686087221
				],
				[
					0,
					6.053814771848124
				],
				[
					0,
					5.381168686087221
				],
				[
					0,
					4.035876514565416
				],
				[
					-1.3452921715217485,
					2.6905843430436107
				],
				[
					-1.3452921715217485,
					1.3452921715218054
				],
				[
					0,
					-0.6726460857609027
				],
				[
					1.3452921715218054,
					-2.017938257282708
				],
				[
					2.6905843430436107,
					-2.690584343043554
				],
				[
					3.3632304288045134,
					-2.690584343043554
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 106,
			"versionNonce": 352207914,
			"isDeleted": false,
			"id": "E9XDfMWLX0hVTaxd0ic-D",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -313.9319896418235,
			"y": -175.39637401711047,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 6.053814771848067,
			"seed": 1363866282,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857608458
				],
				[
					0,
					1.3452921715217485
				],
				[
					0,
					2.017938257282651
				],
				[
					0,
					3.3632304288044566
				],
				[
					0,
					4.035876514565359
				],
				[
					0,
					4.708522600326262
				],
				[
					0,
					6.053814771848067
				],
				[
					0,
					6.053814771848067
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 103,
			"versionNonce": 1947659126,
			"isDeleted": false,
			"id": "oKJvz7phbVWoaQWA8TuHU",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -312.5866974703017,
			"y": -183.46812704624125,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.6726460857609027,
			"height": 2.017938257282708,
			"seed": 1292634218,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					1.3452921715218054
				],
				[
					0.6726460857609027,
					2.017938257282708
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 126,
			"versionNonce": 767045354,
			"isDeleted": false,
			"id": "LLv7h9wMJmx1zv4qy9ucw",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -306.5328826984535,
			"y": -176.06902010287138,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.72646085760897,
			"height": 6.72646085760897,
			"seed": 1967492854,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715217485
				],
				[
					0,
					2.017938257282651
				],
				[
					0,
					2.690584343043554
				],
				[
					0,
					3.3632304288044566
				],
				[
					0,
					4.708522600326262
				],
				[
					0,
					5.381168686087165
				],
				[
					0,
					4.708522600326262
				],
				[
					0,
					4.035876514565359
				],
				[
					0,
					2.690584343043554
				],
				[
					0,
					2.017938257282651
				],
				[
					0,
					1.3452921715217485
				],
				[
					1.3452921715217485,
					1.3452921715217485
				],
				[
					2.017938257282651,
					1.3452921715217485
				],
				[
					2.690584343043554,
					0
				],
				[
					4.035876514565359,
					0
				],
				[
					4.708522600326262,
					0
				],
				[
					4.708522600326262,
					0.6726460857609027
				],
				[
					4.708522600326262,
					2.690584343043554
				],
				[
					4.708522600326262,
					3.3632304288044566
				],
				[
					4.708522600326262,
					4.035876514565359
				],
				[
					4.708522600326262,
					4.708522600326262
				],
				[
					4.708522600326262,
					6.72646085760897
				],
				[
					5.381168686087165,
					6.72646085760897
				],
				[
					5.381168686087165,
					5.381168686087165
				],
				[
					6.72646085760897,
					5.381168686087165
				],
				[
					6.72646085760897,
					4.035876514565359
				],
				[
					6.72646085760897,
					3.3632304288044566
				],
				[
					6.72646085760897,
					3.3632304288044566
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 99,
			"versionNonce": 1280707766,
			"isDeleted": false,
			"id": "OqcO0QIE7NsYtOEJ_3LPh",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -296.44319141204005,
			"y": -190.86723398961107,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1633454518,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 110,
			"versionNonce": 1432797610,
			"isDeleted": false,
			"id": "IyOotb2lI5ZoOVr-_h9_Y",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -295.77054532627926,
			"y": -190.19458790385016,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.6726460857609027,
			"height": 20.852028658587813,
			"seed": 581857130,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					3.3632304288044566
				],
				[
					0,
					5.381168686087165
				],
				[
					-0.6726460857609027,
					8.071753029130718
				],
				[
					-0.6726460857609027,
					11.434983457935232
				],
				[
					-0.6726460857609027,
					16.14350605826155
				],
				[
					-0.6726460857609027,
					18.161444315544202
				],
				[
					-0.6726460857609027,
					19.506736487066007
				],
				[
					-0.6726460857609027,
					20.17938257282691
				],
				[
					-0.6726460857609027,
					20.852028658587813
				],
				[
					0,
					20.852028658587813
				],
				[
					0,
					20.852028658587813
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 109,
			"versionNonce": 715064822,
			"isDeleted": false,
			"id": "CveRJBXPXg8T5uglj47QQ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -301.15171401236637,
			"y": -184.14077313200215,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.41704520065258,
			"height": 1.3452921715218054,
			"seed": 1809042090,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.6905843430436107,
					0
				],
				[
					3.3632304288045134,
					0
				],
				[
					4.708522600326262,
					0
				],
				[
					5.381168686087165,
					0
				],
				[
					6.72646085760897,
					0
				],
				[
					7.399106943369873,
					0
				],
				[
					8.744399114891678,
					1.3452921715218054
				],
				[
					9.41704520065258,
					1.3452921715218054
				],
				[
					9.41704520065258,
					1.3452921715218054
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 102,
			"versionNonce": 389348458,
			"isDeleted": false,
			"id": "jlweFWB4Q7fWOS4SCBdmu",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280.9723314395394,
			"y": -184.14077313200215,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.690584343043554,
			"height": 7.3991069433699295,
			"seed": 494435498,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					1.3452921715218054,
					2.017938257282708
				],
				[
					1.3452921715218054,
					3.3632304288045134
				],
				[
					1.3452921715218054,
					4.708522600326319
				],
				[
					0.6726460857609027,
					6.053814771848124
				],
				[
					-0.6726460857608458,
					7.3991069433699295
				],
				[
					-1.3452921715217485,
					7.3991069433699295
				],
				[
					-1.3452921715217485,
					7.3991069433699295
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 106,
			"versionNonce": 1610012470,
			"isDeleted": false,
			"id": "PyPN6sd7QvjJBiNp_sUXH",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -275.5911627534522,
			"y": -183.46812704624125,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 3.3632304288045134,
			"height": 6.726460857609027,
			"seed": 1501778538,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					4.708522600326319
				],
				[
					-0.6726460857609027,
					4.708522600326319
				],
				[
					-0.6726460857609027,
					6.053814771848124
				],
				[
					-2.017938257282708,
					6.053814771848124
				],
				[
					-2.017938257282708,
					6.726460857609027
				],
				[
					-2.6905843430436107,
					6.726460857609027
				],
				[
					-3.3632304288045134,
					6.726460857609027
				],
				[
					-3.3632304288045134,
					6.726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 99,
			"versionNonce": 1626201898,
			"isDeleted": false,
			"id": "ntuoTXxHxmBtBJDppOMkl",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -252.04854975182047,
			"y": -169.3425592452623,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 5.381168686087221,
			"height": 5.381168686087221,
			"seed": 1352011178,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-2.017938257282708,
					2.017938257282708
				],
				[
					-3.3632304288045134,
					3.3632304288045134
				],
				[
					-4.708522600326319,
					4.035876514565416
				],
				[
					-5.381168686087221,
					5.381168686087221
				],
				[
					-5.381168686087221,
					5.381168686087221
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 119,
			"versionNonce": 1422033014,
			"isDeleted": false,
			"id": "v8UbNF6kqsjrAbTOVlke1",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -197.5642168051878,
			"y": -186.8313574750456,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 13.45292171521794,
			"height": 18.834090401305104,
			"seed": 549909942,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					-0.6726460857609027
				],
				[
					2.017938257282651,
					-0.6726460857609027
				],
				[
					3.3632304288044566,
					-0.6726460857609027
				],
				[
					4.035876514565359,
					-0.6726460857609027
				],
				[
					6.053814771848067,
					-0.6726460857609027
				],
				[
					6.053814771848067,
					1.3452921715217485
				],
				[
					6.053814771848067,
					2.690584343043554
				],
				[
					6.053814771848067,
					4.035876514565359
				],
				[
					6.053814771848067,
					6.053814771848067
				],
				[
					5.381168686087165,
					7.399106943369873
				],
				[
					3.3632304288044566,
					10.089691286413483
				],
				[
					2.690584343043554,
					12.107629543696191
				],
				[
					2.690584343043554,
					13.45292171521794
				],
				[
					1.3452921715217485,
					14.125567800978843
				],
				[
					1.3452921715217485,
					14.798213886739745
				],
				[
					1.3452921715217485,
					16.14350605826155
				],
				[
					1.3452921715217485,
					17.4887982297833
				],
				[
					2.690584343043554,
					17.4887982297833
				],
				[
					4.708522600326262,
					18.161444315544202
				],
				[
					6.72646085760897,
					18.161444315544202
				],
				[
					8.744399114891678,
					18.161444315544202
				],
				[
					10.76233737217433,
					18.161444315544202
				],
				[
					12.780275629457037,
					18.161444315544202
				],
				[
					13.45292171521794,
					18.161444315544202
				],
				[
					13.45292171521794,
					18.161444315544202
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 107,
			"versionNonce": 788294122,
			"isDeleted": false,
			"id": "Qn2_Mq2pD7FrDm4zQSESb",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -184.11129508996987,
			"y": -181.45018878895843,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 12.780275629457037,
			"height": 2.017938257282708,
			"seed": 13087850,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					0
				],
				[
					1.3452921715218054,
					-1.3452921715218054
				],
				[
					2.6905843430436107,
					-1.3452921715218054
				],
				[
					3.3632304288045134,
					-1.3452921715218054
				],
				[
					4.708522600326262,
					-1.3452921715218054
				],
				[
					6.053814771848067,
					-1.3452921715218054
				],
				[
					7.399106943369873,
					-1.3452921715218054
				],
				[
					8.744399114891678,
					-1.3452921715218054
				],
				[
					10.089691286413483,
					-1.3452921715218054
				],
				[
					10.762337372174386,
					-1.3452921715218054
				],
				[
					12.107629543696135,
					-2.017938257282708
				],
				[
					12.780275629457037,
					-2.017938257282708
				],
				[
					12.780275629457037,
					-2.017938257282708
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 126,
			"versionNonce": 482804150,
			"isDeleted": false,
			"id": "FkIBkRmU01PetvrGPdDqL",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -178.05748031812186,
			"y": -184.14077313200204,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 12.107629543696191,
			"height": 17.488798229783356,
			"seed": 438761462,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.6726460857609027,
					0
				],
				[
					-0.6726460857609027,
					0.6726460857609027
				],
				[
					-0.6726460857609027,
					1.3452921715218054
				],
				[
					-1.3452921715218054,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					4.035876514565416
				],
				[
					-1.3452921715218054,
					5.381168686087221
				],
				[
					-1.3452921715218054,
					6.053814771848124
				],
				[
					-1.3452921715218054,
					6.726460857609027
				],
				[
					-1.3452921715218054,
					8.071753029130832
				],
				[
					0,
					8.071753029130832
				],
				[
					0.6726460857609027,
					8.071753029130832
				],
				[
					2.017938257282708,
					8.071753029130832
				],
				[
					4.708522600326319,
					8.071753029130832
				],
				[
					6.053814771848067,
					8.071753029130832
				],
				[
					7.399106943369873,
					8.071753029130832
				],
				[
					8.744399114891678,
					8.744399114891735
				],
				[
					10.089691286413483,
					8.744399114891735
				],
				[
					10.089691286413483,
					10.762337372174386
				],
				[
					10.762337372174386,
					11.434983457935289
				],
				[
					10.762337372174386,
					12.780275629457094
				],
				[
					10.762337372174386,
					13.452921715217997
				],
				[
					10.762337372174386,
					14.798213886739745
				],
				[
					9.41704520065258,
					16.14350605826155
				],
				[
					8.071753029130775,
					17.488798229783356
				],
				[
					6.72646085760897,
					17.488798229783356
				],
				[
					5.381168686087165,
					17.488798229783356
				],
				[
					4.035876514565416,
					17.488798229783356
				],
				[
					2.6905843430436107,
					17.488798229783356
				],
				[
					1.3452921715218054,
					17.488798229783356
				],
				[
					0.6726460857609027,
					16.816152144022453
				],
				[
					0.6726460857609027,
					16.14350605826155
				],
				[
					0.6726460857609027,
					16.14350605826155
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 103,
			"versionNonce": 946576554,
			"isDeleted": false,
			"id": "veBvysPZZezeC59pzoQTQ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -334.78401830041093,
			"y": -128.98379409960836,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.3452921715218054,
			"height": 6.726460857608913,
			"seed": 1776049462,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.3452921715218054,
					1.3452921715218054
				],
				[
					-1.3452921715218054,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					2.6905843430436107
				],
				[
					-1.3452921715218054,
					3.3632304288043997
				],
				[
					-1.3452921715218054,
					4.708522600326205
				],
				[
					-1.3452921715218054,
					6.05381477184801
				],
				[
					-1.3452921715218054,
					6.726460857608913
				],
				[
					0,
					6.726460857608913
				],
				[
					0,
					6.726460857608913
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 102,
			"versionNonce": 187259638,
			"isDeleted": false,
			"id": "vGn6QcDu_ne5W-7FuhTM0",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -329.4028496143237,
			"y": -128.31114801384746,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.3452921715218054,
			"height": 6.726460857608913,
			"seed": 1082179306,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.6726460857609027,
					0
				],
				[
					-0.6726460857609027,
					2.017938257282708
				],
				[
					-0.6726460857609027,
					4.035876514565302
				],
				[
					-0.6726460857609027,
					4.708522600326319
				],
				[
					-0.6726460857609027,
					5.381168686087108
				],
				[
					0,
					6.726460857608913
				],
				[
					0.6726460857609027,
					6.726460857608913
				],
				[
					0.6726460857609027,
					6.726460857608913
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 122,
			"versionNonce": 451311466,
			"isDeleted": false,
			"id": "0rJcZa__Z2U0tTYnXzHmn",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -323.3490348424757,
			"y": -116.20351847015132,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 11.434983457935289,
			"height": 7.399106943369816,
			"seed": 735718570,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					5.381168686087221
				],
				[
					-0.6726460857609027,
					6.726460857609027
				],
				[
					-0.6726460857609027,
					7.399106943369816
				],
				[
					0,
					7.399106943369816
				],
				[
					0,
					6.726460857609027
				],
				[
					1.3452921715218054,
					5.381168686087221
				],
				[
					1.3452921715218054,
					4.035876514565416
				],
				[
					1.3452921715218054,
					2.6905843430436107
				],
				[
					2.017938257282708,
					2.6905843430436107
				],
				[
					2.017938257282708,
					2.017938257282708
				],
				[
					2.017938257282708,
					1.3452921715218054
				],
				[
					2.6905843430436107,
					1.3452921715218054
				],
				[
					2.6905843430436107,
					2.017938257282708
				],
				[
					2.6905843430436107,
					2.6905843430436107
				],
				[
					4.035876514565416,
					4.035876514565416
				],
				[
					4.035876514565416,
					4.708522600326319
				],
				[
					4.708522600326319,
					4.708522600326319
				],
				[
					6.053814771848124,
					5.381168686087221
				],
				[
					6.726460857609027,
					5.381168686087221
				],
				[
					8.071753029130832,
					5.381168686087221
				],
				[
					9.417045200652638,
					4.035876514565416
				],
				[
					10.762337372174386,
					2.017938257282708
				],
				[
					10.762337372174386,
					0.6726460857609027
				],
				[
					10.762337372174386,
					0.6726460857609027
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 125,
			"versionNonce": 1181649974,
			"isDeleted": false,
			"id": "8WMk5AHFSzlniRzcAAq2H",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -309.89611312725776,
			"y": -128.98379409960836,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 12.780275629457094,
			"height": 19.506736487066064,
			"seed": 668394986,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					3.3632304288043997
				],
				[
					0,
					4.708522600326205
				],
				[
					0,
					6.05381477184801
				],
				[
					0,
					7.399106943369816
				],
				[
					0,
					8.744399114891621
				],
				[
					0,
					10.76233737217433
				],
				[
					0,
					14.125567800978843
				],
				[
					0,
					15.470859972500648
				],
				[
					0,
					16.14350605826155
				],
				[
					0,
					16.816152144022453
				],
				[
					0.6726460857609027,
					16.816152144022453
				],
				[
					0.6726460857609027,
					16.14350605826155
				],
				[
					2.690584343043554,
					14.798213886739745
				],
				[
					4.035876514565359,
					14.125567800978843
				],
				[
					4.708522600326262,
					14.125567800978843
				],
				[
					6.053814771848067,
					14.125567800978843
				],
				[
					7.399106943369873,
					14.798213886739745
				],
				[
					7.399106943369873,
					15.470859972500648
				],
				[
					7.399106943369873,
					16.816152144022453
				],
				[
					7.399106943369873,
					17.488798229783356
				],
				[
					8.071753029130775,
					17.488798229783356
				],
				[
					8.071753029130775,
					18.834090401305048
				],
				[
					8.744399114891678,
					18.834090401305048
				],
				[
					8.744399114891678,
					19.506736487066064
				],
				[
					10.089691286413483,
					19.506736487066064
				],
				[
					12.107629543696191,
					19.506736487066064
				],
				[
					12.107629543696191,
					18.834090401305048
				],
				[
					12.780275629457094,
					18.834090401305048
				],
				[
					12.780275629457094,
					17.488798229783356
				],
				[
					12.780275629457094,
					17.488798229783356
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 100,
			"versionNonce": 112720426,
			"isDeleted": false,
			"id": "YwATjVcV-ZdLKmHgItoVX",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -298.4611296693224,
			"y": -116.87616455591223,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.6726460857609027,
			"height": 4.708522600326319,
			"seed": 80026038,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.017938257282708
				],
				[
					0.6726460857609027,
					4.035876514565416
				],
				[
					0.6726460857609027,
					4.708522600326319
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 97,
			"versionNonce": 1551603062,
			"isDeleted": false,
			"id": "xTzYlrVnXdH2OS_E9YG_A",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -297.78848358356163,
			"y": -122.92997932776035,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 1.3452921715218054,
			"seed": 583503542,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 128,
			"versionNonce": 1791698154,
			"isDeleted": false,
			"id": "aoyvAcwTpnKFXn6TZrwkN",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -289.7167305544308,
			"y": -134.36496278569558,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 13.45292171521794,
			"height": 24.21525908739227,
			"seed": 1828584746,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					6.053814771848124
				],
				[
					0,
					8.744399114891621
				],
				[
					0,
					11.434983457935232
				],
				[
					0,
					14.798213886739745
				],
				[
					0,
					17.488798229783356
				],
				[
					1.3452921715218054,
					19.506736487066064
				],
				[
					1.3452921715218054,
					20.85202865858787
				],
				[
					1.3452921715218054,
					21.524674744348772
				],
				[
					2.6905843430436107,
					22.869966915870577
				],
				[
					2.6905843430436107,
					23.54261300163148
				],
				[
					3.3632304288045134,
					23.54261300163148
				],
				[
					4.035876514565416,
					23.54261300163148
				],
				[
					4.708522600326319,
					23.54261300163148
				],
				[
					6.726460857609027,
					23.54261300163148
				],
				[
					8.071753029130832,
					22.197320830109675
				],
				[
					9.41704520065258,
					20.179382572826967
				],
				[
					9.41704520065258,
					19.506736487066064
				],
				[
					9.41704520065258,
					18.16144431554426
				],
				[
					8.071753029130832,
					18.16144431554426
				],
				[
					6.726460857609027,
					18.83409040130516
				],
				[
					6.053814771848124,
					20.179382572826967
				],
				[
					6.053814771848124,
					21.524674744348772
				],
				[
					6.053814771848124,
					22.197320830109675
				],
				[
					6.053814771848124,
					23.54261300163148
				],
				[
					6.053814771848124,
					24.21525908739227
				],
				[
					7.3991069433699295,
					24.21525908739227
				],
				[
					8.071753029130832,
					24.21525908739227
				],
				[
					9.41704520065258,
					24.21525908739227
				],
				[
					10.762337372174386,
					23.54261300163148
				],
				[
					12.780275629457037,
					22.197320830109675
				],
				[
					13.45292171521794,
					21.524674744348772
				],
				[
					13.45292171521794,
					21.524674744348772
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 102,
			"versionNonce": 1452635830,
			"isDeleted": false,
			"id": "4bA10OoWCWL5l2B0Iwum1",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -271.55528623888654,
			"y": -130.32908627113017,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.3452921715218054,
			"height": 4.708522600326205,
			"seed": 1231857322,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					4.035876514565416
				],
				[
					-0.6726460857609027,
					4.708522600326205
				],
				[
					-1.3452921715218054,
					4.708522600326205
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 100,
			"versionNonce": 548075434,
			"isDeleted": false,
			"id": "U3ca2gB2eorGghH7WprnH",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -262.8108871239949,
			"y": -131.00173235689107,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.3452921715218054,
			"height": 5.381168686087108,
			"seed": 1973238890,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					3.3632304288045134
				],
				[
					-0.6726460857609027,
					4.708522600326319
				],
				[
					-0.6726460857609027,
					5.381168686087108
				],
				[
					-1.3452921715218054,
					5.381168686087108
				],
				[
					-1.3452921715218054,
					5.381168686087108
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 107,
			"versionNonce": 1298214902,
			"isDeleted": false,
			"id": "pPTjMM8kClH7u2i1RKeam",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -246.66738106573337,
			"y": -112.84028804134681,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 6.72646085760897,
			"height": 8.744399114891621,
			"seed": 1664005994,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.6726460857609027,
					0
				],
				[
					-1.3452921715218054,
					0
				],
				[
					-2.690584343043554,
					1.3452921715218054
				],
				[
					-3.3632304288044566,
					2.017938257282708
				],
				[
					-4.035876514565359,
					2.017938257282708
				],
				[
					-5.381168686087165,
					3.3632304288045134
				],
				[
					-6.053814771848067,
					3.3632304288045134
				],
				[
					-6.053814771848067,
					4.708522600326319
				],
				[
					-6.72646085760897,
					4.708522600326319
				],
				[
					-6.72646085760897,
					6.726460857608913
				],
				[
					-6.72646085760897,
					7.399106943369816
				],
				[
					-6.72646085760897,
					8.744399114891621
				],
				[
					-6.72646085760897,
					8.744399114891621
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 113,
			"versionNonce": 411202154,
			"isDeleted": false,
			"id": "wwxM7j_i12AoqT4Kb5KfH",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -196.8915707194269,
			"y": -130.32908627113017,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 14.798213886739745,
			"height": 17.488798229783356,
			"seed": 1708862070,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-0.6726460857609027
				],
				[
					2.017938257282708,
					-2.017938257282708
				],
				[
					4.035876514565359,
					-2.6905843430436107
				],
				[
					5.381168686087165,
					-2.6905843430436107
				],
				[
					6.053814771848067,
					-2.6905843430436107
				],
				[
					6.72646085760897,
					-2.6905843430436107
				],
				[
					6.72646085760897,
					-1.3452921715218054
				],
				[
					6.72646085760897,
					0.6726460857609027
				],
				[
					5.381168686087165,
					3.3632304288045134
				],
				[
					3.3632304288044566,
					5.381168686087221
				],
				[
					0.6726460857609027,
					10.089691286413426
				],
				[
					0.6726460857609027,
					11.434983457935232
				],
				[
					0,
					12.107629543696135
				],
				[
					0,
					13.45292171521794
				],
				[
					1.3452921715218054,
					14.798213886739745
				],
				[
					2.6905843430436107,
					14.798213886739745
				],
				[
					4.708522600326262,
					14.798213886739745
				],
				[
					6.72646085760897,
					14.798213886739745
				],
				[
					8.744399114891678,
					14.798213886739745
				],
				[
					10.762337372174386,
					14.125567800978843
				],
				[
					14.125567800978843,
					12.107629543696135
				],
				[
					14.798213886739745,
					12.107629543696135
				],
				[
					14.798213886739745,
					12.107629543696135
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 119,
			"versionNonce": 2095300918,
			"isDeleted": false,
			"id": "JDrIcfwFr8ezDn71qf8a8",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -172.67631163203464,
			"y": -132.34702452841287,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 14.798213886739745,
			"height": 14.798213886739745,
			"seed": 1621496042,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-1.3452921715218054,
					0
				],
				[
					-2.6905843430436107,
					0
				],
				[
					-4.035876514565416,
					2.017938257282708
				],
				[
					-5.381168686087165,
					3.3632304288045134
				],
				[
					-7.399106943369873,
					6.053814771848124
				],
				[
					-8.744399114891678,
					8.071753029130718
				],
				[
					-8.744399114891678,
					10.089691286413426
				],
				[
					-8.744399114891678,
					11.434983457935232
				],
				[
					-8.744399114891678,
					12.780275629457037
				],
				[
					-8.071753029130775,
					14.125567800978843
				],
				[
					-6.72646085760897,
					14.798213886739745
				],
				[
					-4.708522600326319,
					14.798213886739745
				],
				[
					-2.017938257282708,
					14.798213886739745
				],
				[
					0,
					14.798213886739745
				],
				[
					1.3452921715218054,
					14.798213886739745
				],
				[
					3.3632304288044566,
					14.798213886739745
				],
				[
					4.708522600326262,
					14.798213886739745
				],
				[
					6.053814771848067,
					14.798213886739745
				],
				[
					6.053814771848067,
					12.780275629457037
				],
				[
					4.708522600326262,
					12.107629543696135
				],
				[
					2.6905843430436107,
					12.107629543696135
				],
				[
					0.6726460857609027,
					12.107629543696135
				],
				[
					-2.017938257282708,
					12.107629543696135
				],
				[
					-4.708522600326319,
					12.107629543696135
				],
				[
					-6.72646085760897,
					12.107629543696135
				],
				[
					-7.399106943369873,
					12.107629543696135
				],
				[
					-7.399106943369873,
					13.45292171521794
				],
				[
					-6.053814771848067,
					13.45292171521794
				],
				[
					-6.053814771848067,
					13.45292171521794
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 100,
			"versionNonce": 85759274,
			"isDeleted": false,
			"id": "PH6bsbzZlC3SAnK41mkt1",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -331.42078787160654,
			"y": -83.24386026786732,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.017938257282708,
			"height": 7.3991069433699295,
			"seed": 738409846,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.6726460857609027,
					0
				],
				[
					-1.3452921715218054,
					0.6726460857609027
				],
				[
					-1.3452921715218054,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					3.3632304288045134
				],
				[
					-2.017938257282708,
					4.708522600326319
				],
				[
					-2.017938257282708,
					5.381168686087108
				],
				[
					-2.017938257282708,
					6.726460857608913
				],
				[
					-2.017938257282708,
					7.3991069433699295
				],
				[
					-0.6726460857609027,
					7.3991069433699295
				],
				[
					-0.6726460857609027,
					7.3991069433699295
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 97,
			"versionNonce": 1484925558,
			"isDeleted": false,
			"id": "yfyteCDUZ9DIYXhvT_Z7q",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -326.0396191855193,
			"y": -83.24386026786732,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.017938257282651,
			"height": 7.3991069433699295,
			"seed": 1848650998,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.6726460857609027,
					2.017938257282708
				],
				[
					-0.6726460857609027,
					4.035876514565302
				],
				[
					-1.3452921715218054,
					5.381168686087108
				],
				[
					-1.3452921715218054,
					6.726460857608913
				],
				[
					-1.3452921715218054,
					7.3991069433699295
				],
				[
					0.6726460857608458,
					7.3991069433699295
				],
				[
					0.6726460857608458,
					7.3991069433699295
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 132407274,
			"isDeleted": false,
			"id": "stkpqXXGZ1c7wR1FffiEE",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -319.3131583279103,
			"y": -67.77300029536667,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.3991069433699295,
			"height": 8.744399114891621,
			"seed": 1315926378,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.690584343043497
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					4.035876514565302
				],
				[
					-1.3452921715218054,
					5.381168686087108
				],
				[
					-1.3452921715218054,
					6.053814771848124
				],
				[
					-1.3452921715218054,
					6.726460857608913
				],
				[
					-1.3452921715218054,
					5.381168686087108
				],
				[
					-1.3452921715218054,
					4.035876514565302
				],
				[
					-1.3452921715218054,
					3.3632304288045134
				],
				[
					-1.3452921715218054,
					2.017938257282708
				],
				[
					-1.3452921715218054,
					0.6726460857609027
				],
				[
					-0.6726460857609027,
					0.6726460857609027
				],
				[
					0,
					-0.6726460857609027
				],
				[
					1.3452921715218054,
					-0.6726460857609027
				],
				[
					2.017938257282708,
					-2.017938257282708
				],
				[
					2.6905843430436107,
					-2.017938257282708
				],
				[
					4.035876514565416,
					-2.017938257282708
				],
				[
					4.708522600326319,
					-2.017938257282708
				],
				[
					5.381168686087221,
					-2.017938257282708
				],
				[
					6.053814771848124,
					-2.017938257282708
				],
				[
					6.053814771848124,
					-2.017938257282708
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 520186806,
			"isDeleted": false,
			"id": "UWLwkLZ6nZ1r-MV8oZzgU",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -313.2593435560623,
			"y": -65.75506203808396,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.399106943369816,
			"height": 7.3991069433699295,
			"seed": 396092010,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.3452921715218054,
					0
				],
				[
					2.017938257282708,
					0
				],
				[
					2.017938257282708,
					-0.6726460857609027
				],
				[
					2.6905843430436107,
					-0.6726460857609027
				],
				[
					2.6905843430436107,
					-1.3452921715218054
				],
				[
					3.3632304288044566,
					-1.3452921715218054
				],
				[
					3.3632304288044566,
					-2.017938257282708
				],
				[
					3.3632304288044566,
					-3.3632304288045134
				],
				[
					2.6905843430436107,
					-3.3632304288045134
				],
				[
					1.3452921715218054,
					-2.017938257282708
				],
				[
					1.3452921715218054,
					-1.3452921715218054
				],
				[
					1.3452921715218054,
					0
				],
				[
					1.3452921715218054,
					1.3452921715218054
				],
				[
					1.3452921715218054,
					2.6905843430436107
				],
				[
					1.3452921715218054,
					3.3632304288043997
				],
				[
					2.017938257282708,
					3.3632304288043997
				],
				[
					2.6905843430436107,
					4.035876514565416
				],
				[
					3.3632304288044566,
					4.035876514565416
				],
				[
					5.381168686087165,
					4.035876514565416
				],
				[
					6.72646085760897,
					2.6905843430436107
				],
				[
					7.399106943369816,
					2.0179382572825943
				],
				[
					7.399106943369816,
					2.0179382572825943
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 99,
			"versionNonce": 1558500010,
			"isDeleted": false,
			"id": "9SXS4XxbU-WfIJWyx1zgF",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -302.49700618388783,
			"y": -96.69678198308526,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.3452921715218054,
			"height": 37.66818080261021,
			"seed": 1388761962,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-0.6726460857609027
				],
				[
					0,
					3.3632304288043997
				],
				[
					0,
					10.089691286413426
				],
				[
					0,
					14.125567800978843
				],
				[
					0.6726460857609027,
					20.179382572826853
				],
				[
					0.6726460857609027,
					25.560551258914074
				],
				[
					0.6726460857609027,
					28.923781687718588
				],
				[
					0.6726460857609027,
					31.614366030762085
				],
				[
					0.6726460857609027,
					33.63230428804491
				],
				[
					0.6726460857609027,
					34.97759645956671
				],
				[
					0.6726460857609027,
					36.32288863108852
				],
				[
					1.3452921715218054,
					36.995534716849306
				],
				[
					1.3452921715218054,
					36.995534716849306
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 92,
			"versionNonce": 1854309622,
			"isDeleted": false,
			"id": "JrvdRJH2CR7Et06sBE0Qe",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -305.18759052693144,
			"y": -67.10035420960577,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 5.381168686087221,
			"height": 2.017938257282708,
			"seed": 1893886198,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857609027,
					-1.3452921715218054
				],
				[
					2.017938257282708,
					-1.3452921715218054
				],
				[
					2.6905843430436107,
					-2.017938257282708
				],
				[
					4.035876514565416,
					-2.017938257282708
				],
				[
					5.381168686087221,
					-2.017938257282708
				],
				[
					5.381168686087221,
					-2.017938257282708
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 103,
			"versionNonce": 113831274,
			"isDeleted": false,
			"id": "5_eVDDPk2T3RCxXo__qZX",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -296.4431914120398,
			"y": -67.77300029536667,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 5.381168686087165,
			"height": 6.05381477184801,
			"seed": 522403318,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					2.690584343043497
				],
				[
					0,
					4.035876514565302
				],
				[
					0.6726460857609027,
					4.035876514565302
				],
				[
					2.017938257282708,
					4.035876514565302
				],
				[
					3.3632304288044566,
					4.035876514565302
				],
				[
					4.035876514565359,
					4.035876514565302
				],
				[
					4.035876514565359,
					3.3632304288045134
				],
				[
					5.381168686087165,
					2.017938257282708
				],
				[
					5.381168686087165,
					0.6726460857609027
				],
				[
					5.381168686087165,
					-0.6726460857609027
				],
				[
					5.381168686087165,
					-2.017938257282708
				],
				[
					5.381168686087165,
					-1.3452921715218054
				],
				[
					5.381168686087165,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 108,
			"versionNonce": 1486255670,
			"isDeleted": false,
			"id": "eVMWAG0CGe57ytWqIJX5M",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -285.6808540398654,
			"y": -67.77300029536667,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.41704520065258,
			"height": 9.417045200652638,
			"seed": 413588778,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.690584343043497
				],
				[
					-0.6726460857609027,
					3.3632304288045134
				],
				[
					-0.6726460857609027,
					4.035876514565302
				],
				[
					-0.6726460857609027,
					5.381168686087108
				],
				[
					-0.6726460857609027,
					6.053814771848124
				],
				[
					0,
					6.053814771848124
				],
				[
					0,
					4.035876514565302
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					-0.6726460857609027
				],
				[
					0,
					-2.017938257282708
				],
				[
					0.6726460857609027,
					-2.017938257282708
				],
				[
					0.6726460857609027,
					-2.6905843430436107
				],
				[
					2.6905843430436107,
					-2.6905843430436107
				],
				[
					4.035876514565416,
					-3.3632304288045134
				],
				[
					5.381168686087221,
					-3.3632304288045134
				],
				[
					7.399106943369873,
					-3.3632304288045134
				],
				[
					8.071753029130775,
					-3.3632304288045134
				],
				[
					8.744399114891678,
					-3.3632304288045134
				],
				[
					8.744399114891678,
					-3.3632304288045134
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 105,
			"versionNonce": 2061217834,
			"isDeleted": false,
			"id": "ky7h0qCe3TiDU9p5xZDBr",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -274.24587058193015,
			"y": -66.42770812384487,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.399106943369873,
			"height": 4.708522600326205,
			"seed": 516402730,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.6726460857609027
				],
				[
					0,
					2.017938257282708
				],
				[
					-0.6726460857608458,
					2.017938257282708
				],
				[
					-0.6726460857608458,
					2.690584343043497
				],
				[
					-1.3452921715217485,
					2.690584343043497
				],
				[
					-1.3452921715217485,
					1.3452921715216917
				],
				[
					-1.3452921715217485,
					0.6726460857609027
				],
				[
					-1.3452921715217485,
					0
				],
				[
					-1.3452921715217485,
					-1.3452921715218054
				],
				[
					0,
					-2.017938257282708
				],
				[
					0.6726460857609027,
					-2.017938257282708
				],
				[
					2.017938257282708,
					-2.017938257282708
				],
				[
					3.3632304288045134,
					-2.017938257282708
				],
				[
					4.708522600326319,
					-1.3452921715218054
				],
				[
					6.053814771848124,
					0
				],
				[
					6.053814771848124,
					2.017938257282708
				],
				[
					6.053814771848124,
					2.690584343043497
				],
				[
					6.053814771848124,
					2.017938257282708
				],
				[
					6.053814771848124,
					2.017938257282708
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 93,
			"versionNonce": 1981169526,
			"isDeleted": false,
			"id": "BLvm_Qbmk3tsjSZBUNaEO",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -264.1561792955167,
			"y": -85.93444461091093,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 6.726460857608913,
			"seed": 26207734,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					1.3452921715218054
				],
				[
					0,
					2.017938257282708
				],
				[
					0,
					3.3632304288045134
				],
				[
					0,
					4.035876514565416
				],
				[
					0,
					5.381168686087108
				],
				[
					0,
					6.726460857608913
				],
				[
					0,
					6.726460857608913
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 93,
			"versionNonce": 1292376810,
			"isDeleted": false,
			"id": "CEzkF2rpXw6s7Mlm3SvRv",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -254.0664880091033,
			"y": -89.29767503971544,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.017938257282708,
			"height": 8.744399114891621,
			"seed": 274962282,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					2.017938257282708
				],
				[
					-0.6726460857609027,
					3.3632304288045134
				],
				[
					-0.6726460857609027,
					5.381168686087221
				],
				[
					-2.017938257282708,
					6.726460857609027
				],
				[
					-2.017938257282708,
					7.3991069433699295
				],
				[
					-2.017938257282708,
					8.744399114891621
				],
				[
					-2.017938257282708,
					8.744399114891621
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 96,
			"versionNonce": 2068504758,
			"isDeleted": false,
			"id": "A-eHcx5Ido9rX_SQQHjpe",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -242.63150455116795,
			"y": -65.75506203808396,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 7.399106943369873,
			"height": 9.417045200652524,
			"seed": 936943926,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					0.672646085760789
				],
				[
					0,
					2.6905843430436107
				],
				[
					0,
					4.035876514565416
				],
				[
					-1.3452921715218054,
					4.708522600326205
				],
				[
					-2.6905843430436107,
					6.05381477184801
				],
				[
					-4.708522600326319,
					7.399106943369816
				],
				[
					-5.381168686087221,
					8.744399114891621
				],
				[
					-6.053814771848124,
					8.744399114891621
				],
				[
					-7.399106943369873,
					9.417045200652524
				],
				[
					-7.399106943369873,
					9.417045200652524
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 109,
			"versionNonce": 1540959658,
			"isDeleted": false,
			"id": "5FN1VnFwkam-8C8_4aF1T",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -197.5642168051878,
			"y": -85.26179852515003,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 14.125567800978843,
			"height": 16.816152144022453,
			"seed": 1229134058,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0,
					-1.3452921715218054
				],
				[
					0,
					-2.017938257282708
				],
				[
					0.6726460857609027,
					-2.017938257282708
				],
				[
					2.017938257282708,
					-2.017938257282708
				],
				[
					2.6905843430436107,
					-2.017938257282708
				],
				[
					2.6905843430436107,
					-1.3452921715218054
				],
				[
					2.6905843430436107,
					0
				],
				[
					2.6905843430436107,
					1.3452921715218054
				],
				[
					2.017938257282708,
					2.6905843430436107
				],
				[
					0.6726460857609027,
					4.035876514565416
				],
				[
					0,
					6.05381477184801
				],
				[
					-1.3452921715218054,
					7.399106943369816
				],
				[
					-1.3452921715218054,
					8.744399114891621
				],
				[
					-2.017938257282708,
					10.089691286413426
				],
				[
					-2.017938257282708,
					10.762337372174443
				],
				[
					-2.017938257282708,
					12.107629543696135
				],
				[
					-1.3452921715218054,
					13.45292171521794
				],
				[
					-0.6726460857609027,
					13.45292171521794
				],
				[
					0.6726460857609027,
					13.45292171521794
				],
				[
					3.3632304288045134,
					14.798213886739745
				],
				[
					5.381168686087165,
					14.798213886739745
				],
				[
					8.071753029130775,
					14.798213886739745
				],
				[
					10.762337372174386,
					13.45292171521794
				],
				[
					12.107629543696135,
					13.45292171521794
				],
				[
					12.107629543696135,
					12.780275629457037
				],
				[
					12.107629543696135,
					12.780275629457037
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 99,
			"versionNonce": 1272535542,
			"isDeleted": false,
			"id": "gncJl64o-B8jPJPRmlBgp",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -186.12923334725247,
			"y": -83.24386026786732,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.417045200652524,
			"height": 12.780275629457037,
			"seed": 1645369194,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.6726460857608458,
					0
				],
				[
					2.017938257282651,
					0
				],
				[
					4.035876514565359,
					0
				],
				[
					5.381168686087165,
					0
				],
				[
					6.72646085760897,
					0
				],
				[
					7.399106943369873,
					0
				],
				[
					8.071753029130775,
					0
				],
				[
					9.417045200652524,
					0
				],
				[
					9.417045200652524,
					1.3452921715218054
				],
				[
					6.72646085760897,
					4.035876514565302
				],
				[
					5.381168686087165,
					6.726460857608913
				],
				[
					4.035876514565359,
					8.071753029130718
				],
				[
					4.035876514565359,
					10.089691286413426
				],
				[
					3.3632304288044566,
					11.434983457935232
				],
				[
					3.3632304288044566,
					12.780275629457037
				],
				[
					3.3632304288044566,
					12.780275629457037
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "freedraw",
			"version": 91,
			"versionNonce": 2088364138,
			"isDeleted": false,
			"id": "ORb5rk9ag5jT9CO_wxxdw",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -184.78394117573077,
			"y": -75.1721072387366,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 10.762337372174386,
			"height": 1.3452921715218054,
			"seed": 464228394,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					2.017938257282708,
					0
				],
				[
					4.035876514565416,
					0
				],
				[
					6.053814771848124,
					0
				],
				[
					7.399106943369873,
					0
				],
				[
					8.744399114891678,
					0
				],
				[
					10.089691286413483,
					-1.3452921715218054
				],
				[
					10.762337372174386,
					-1.3452921715218054
				],
				[
					10.762337372174386,
					-1.3452921715218054
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		},
		{
			"type": "text",
			"version": 346,
			"versionNonce": 247900982,
			"isDeleted": false,
			"id": "qZGx8CHs",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -395.29991149902344,
			"y": -22.171875,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 263.4558410644531,
			"height": 20,
			"seed": 887180662,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Salen parejas de (lexema, token).",
			"rawText": "Salen parejas de (lexema, token).",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Salen parejas de (lexema, token).",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "text",
			"version": 1003,
			"versionNonce": 649415466,
			"isDeleted": false,
			"id": "64ScBamP",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -394.76777592411815,
			"y": 13.561658881678625,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 566.0636596679688,
			"height": 40,
			"seed": 1877154154,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Para representar dichos tokens habrá que realizar una transformación:\n ",
			"rawText": "Para representar dichos tokens habrá que realizar una transformación:\n ",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Para representar dichos tokens habrá que realizar una transformación:\n ",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "image",
			"version": 319,
			"versionNonce": 1115149430,
			"isDeleted": false,
			"id": "AFSiICsquymkrnA07Ma0Y",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -390.4075937582748,
			"y": 39.20613142439777,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 519.400864717576,
			"height": 196.93949453874757,
			"seed": 539437482,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "5d441ba2f57191727439fa7246299577d36c08a8",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 322,
			"versionNonce": 553014762,
			"isDeleted": false,
			"id": "4BSJTqW9",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -395.4682221216153,
			"y": 297.396842680395,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 558.8477783203125,
			"height": 100,
			"seed": 48259126,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Para cada lexema de entrada se creara un objeto de la clase Token\nel cual contendra:\n- El lexema reconocido\n- El tipo (categoria) del lexema (tokenType)\n- La posicion del fichero (linea y columna)",
			"rawText": "Para cada lexema de entrada se creara un objeto de la clase Token\nel cual contendra:\n- El lexema reconocido\n- El tipo (categoria) del lexema (tokenType)\n- La posicion del fichero (linea y columna)",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Para cada lexema de entrada se creara un objeto de la clase Token\nel cual contendra:\n- El lexema reconocido\n- El tipo (categoria) del lexema (tokenType)\n- La posicion del fichero (linea y columna)",
			"lineHeight": 1.25,
			"baseline": 94
		},
		{
			"type": "text",
			"version": 448,
			"versionNonce": 1353831862,
			"isDeleted": false,
			"id": "XebM4T2w",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -398.37369329552075,
			"y": 417.7375743322324,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 634.2716064453125,
			"height": 160,
			"seed": 1516084138,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "En lugar de devolver la lista completa de tokens la forma de implementar esto\nserá implementando un método en el léxico que pida el siguiente token disponible.\nPara poder hacer que el programa tenga fin habrá que definir constantes:\n- static final int END = 0;\n- static final int WHILE = 257;\n- static final int IF = 260;\n\n",
			"rawText": "En lugar de devolver la lista completa de tokens la forma de implementar esto\nserá implementando un método en el léxico que pida el siguiente token disponible.\nPara poder hacer que el programa tenga fin habrá que definir constantes:\n- static final int END = 0;\n- static final int WHILE = 257;\n- static final int IF = 260;\n\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "En lugar de devolver la lista completa de tokens la forma de implementar esto\nserá implementando un método en el léxico que pida el siguiente token disponible.\nPara poder hacer que el programa tenga fin habrá que definir constantes:\n- static final int END = 0;\n- static final int WHILE = 257;\n- static final int IF = 260;\n\n",
			"lineHeight": 1.25,
			"baseline": 154
		},
		{
			"type": "text",
			"version": 197,
			"versionNonce": 742918314,
			"isDeleted": false,
			"id": "NPDHVpTh",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 600,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 224.95191955566406,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "EJEMPLO 0220",
			"rawText": "EJEMPLO 0220",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "EJEMPLO 0220",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 74,
			"versionNonce": 580497142,
			"isDeleted": false,
			"id": "efbjm3mW",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -399.8264288824734,
			"y": 646.7797513425186,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 554.4637451171875,
			"height": 60,
			"seed": 53308278,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Supóngase un programa cuyo bucle principal de ejecución va invocando \na nextToken y, a continuación, imprime una traza del contenido del\nobjeto Token obtenido en cada llamada:",
			"rawText": "Supóngase un programa cuyo bucle principal de ejecución va invocando \na nextToken y, a continuación, imprime una traza del contenido del\nobjeto Token obtenido en cada llamada:",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Supóngase un programa cuyo bucle principal de ejecución va invocando \na nextToken y, a continuación, imprime una traza del contenido del\nobjeto Token obtenido en cada llamada:",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"type": "text",
			"version": 259,
			"versionNonce": 810902378,
			"isDeleted": false,
			"id": "X8WGIxMA",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -333.7269596761258,
			"y": 731.5284611140147,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 553.125,
			"height": 134.4,
			"seed": 627191286,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "Lexico lex = new Lexico(new FileReader(“prog.txt\"));\nToken token;\nwhile ((token = lex.nextToken()).getType() != Lexico.END) {\n    System.out.println(token.getLexeme());\n    System.out.println(token.getType());\n    System.out.println(token.getLine());\n}",
			"rawText": "Lexico lex = new Lexico(new FileReader(“prog.txt\"));\nToken token;\nwhile ((token = lex.nextToken()).getType() != Lexico.END) {\n    System.out.println(token.getLexeme());\n    System.out.println(token.getType());\n    System.out.println(token.getLine());\n}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Lexico lex = new Lexico(new FileReader(“prog.txt\"));\nToken token;\nwhile ((token = lex.nextToken()).getType() != Lexico.END) {\n    System.out.println(token.getLexeme());\n    System.out.println(token.getType());\n    System.out.println(token.getLine());\n}",
			"lineHeight": 1.2,
			"baseline": 130
		},
		{
			"type": "text",
			"version": 416,
			"versionNonce": 884236342,
			"isDeleted": false,
			"id": "DAuUJkDq",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400.31217212657907,
			"y": 885.299512863531,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 558.0957641601562,
			"height": 200,
			"seed": 53308278,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Supóngase la siguiente entrada en el fichero prog.txt:\n    \n    altura\n    +\n    1.75\n\n\nY finalmente supóngase que se han definido las siguientes constantes \nasociadas a los tokens del lenguaje:\n",
			"rawText": "Supóngase la siguiente entrada en el fichero prog.txt:\n    \n    altura\n    +\n    1.75\n\n\nY finalmente supóngase que se han definido las siguientes constantes \nasociadas a los tokens del lenguaje:\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Supóngase la siguiente entrada en el fichero prog.txt:\n    \n    altura\n    +\n    1.75\n\n\nY finalmente supóngase que se han definido las siguientes constantes \nasociadas a los tokens del lenguaje:\n",
			"lineHeight": 1.25,
			"baseline": 194
		},
		{
			"type": "text",
			"version": 20,
			"versionNonce": 1734960682,
			"isDeleted": false,
			"id": "3UbUSK7i",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -340,
			"y": 1080,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 131.25,
			"height": 19.2,
			"seed": 1262907946,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "class Lexico {",
			"rawText": "class Lexico {",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "class Lexico {",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 719776118,
			"isDeleted": false,
			"id": "1Lpa6eOP",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1100,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 234.375,
			"height": 19.2,
			"seed": 1211145590,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "static final int END = 0;",
			"rawText": "static final int END = 0;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "static final int END = 0;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 175050986,
			"isDeleted": false,
			"id": "kdAga50M",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1129.2,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 271.875,
			"height": 19.2,
			"seed": 113941738,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "static final int IDENT = 257;",
			"rawText": "static final int IDENT = 257;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "static final int IDENT = 257;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 1685473974,
			"isDeleted": false,
			"id": "D4iOGvcJ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1158.4,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 243.75,
			"height": 19.2,
			"seed": 376012470,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "static final int IF = 258;",
			"rawText": "static final int IF = 258;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "static final int IF = 258;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 2096194474,
			"isDeleted": false,
			"id": "XEvp2dS9",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1187.6000000000001,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 281.25,
			"height": 19.2,
			"seed": 2113630122,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "static final int LITENT = 259;",
			"rawText": "static final int LITENT = 259;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "static final int LITENT = 259;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 268927990,
			"isDeleted": false,
			"id": "fi1v7wi4",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1216.8000000000002,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 290.625,
			"height": 19.2,
			"seed": 91502582,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "static final int LITREAL = 260;",
			"rawText": "static final int LITREAL = 260;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "static final int LITREAL = 260;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 30,
			"versionNonce": 2031836778,
			"isDeleted": false,
			"id": "TRHolHcc",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 1246.0000000000002,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 9.375,
			"height": 19.2,
			"seed": 1694755434,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "…",
			"rawText": "…",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "…",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 22,
			"versionNonce": 1067423030,
			"isDeleted": false,
			"id": "9pCoupVs",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -340,
			"y": 1260,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 9.375,
			"height": 19.2,
			"seed": 1297467702,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "}",
			"rawText": "}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 93,
			"versionNonce": 1001914666,
			"isDeleted": false,
			"id": "xLBhnI37",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1320,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 468.15972900390625,
			"height": 40,
			"seed": 1543482154,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "El resultado de ejecutar dicho programa seria el siguiente:\n",
			"rawText": "El resultado de ejecutar dicho programa seria el siguiente:\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "El resultado de ejecutar dicho programa seria el siguiente:\n",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "image",
			"version": 50,
			"versionNonce": 2091089526,
			"isDeleted": false,
			"id": "UduKynjBp0hc94J1kbr7a",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -380,
			"y": 1360,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 437.00000000000006,
			"height": 175,
			"seed": 1340371958,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "a934087a36a1727e74235cd94c0815015297628d",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 263,
			"versionNonce": 808602602,
			"isDeleted": false,
			"id": "pbKrp0rJ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1620,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 357.9238586425781,
			"height": 105,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "ESPECIFICACIÓN LÉXICA\n\n",
			"rawText": "ESPECIFICACIÓN LÉXICA\n\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ESPECIFICACIÓN LÉXICA\n\n",
			"lineHeight": 1.25,
			"baseline": 95
		},
		{
			"type": "text",
			"version": 192,
			"versionNonce": 1540898742,
			"isDeleted": false,
			"id": "uuC2pT8n",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1680,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 559.263671875,
			"height": 40,
			"seed": 654966314,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "1. Determinar tokens (como en el caso de los IDENT)\n2. Definir patrones (determinar que lexemas pertenecen a cada token)",
			"rawText": "1. Determinar tokens (como en el caso de los IDENT)\n2. Definir patrones (determinar que lexemas pertenecen a cada token)",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "1. Determinar tokens (como en el caso de los IDENT)\n2. Definir patrones (determinar que lexemas pertenecen a cada token)",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "text",
			"version": 330,
			"versionNonce": 479542954,
			"isDeleted": false,
			"id": "zCP88YMW",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1760,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 618.7356567382812,
			"height": 60,
			"seed": 2104132458,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "En el segundo caso determinar si un lexema es valido o no depende\nde una serie de reglas que el creador del lenguaje haya definido. Para definir\nestos patrones hay que hacer uso de los metalenguajes.",
			"rawText": "En el segundo caso determinar si un lexema es valido o no depende\nde una serie de reglas que el creador del lenguaje haya definido. Para definir\nestos patrones hay que hacer uso de los metalenguajes.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "En el segundo caso determinar si un lexema es valido o no depende\nde una serie de reglas que el creador del lenguaje haya definido. Para definir\nestos patrones hay que hacer uso de los metalenguajes.",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"type": "text",
			"version": 299,
			"versionNonce": 291690742,
			"isDeleted": false,
			"id": "puMO6C6U",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1920,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 248.97592163085938,
			"height": 105,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327232,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "METALENGUAJES\n\n",
			"rawText": "METALENGUAJES\n\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "METALENGUAJES\n\n",
			"lineHeight": 1.25,
			"baseline": 95
		},
		{
			"type": "text",
			"version": 700,
			"versionNonce": 1301010794,
			"isDeleted": false,
			"id": "hJ5yYKUj",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 1980,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 663.9995727539062,
			"height": 100,
			"seed": 2104132458,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Un metalenguaje deberá de ser preciso y concreto para que no haya problemas\nde repetición o de confusión es los patrones.\n\nLos dos metalenguajes más usados para reglar estos aspectos son los autómatas\nfinitos y las expresiones regulares.",
			"rawText": "Un metalenguaje deberá de ser preciso y concreto para que no haya problemas\nde repetición o de confusión es los patrones.\n\nLos dos metalenguajes más usados para reglar estos aspectos son los autómatas\nfinitos y las expresiones regulares.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Un metalenguaje deberá de ser preciso y concreto para que no haya problemas\nde repetición o de confusión es los patrones.\n\nLos dos metalenguajes más usados para reglar estos aspectos son los autómatas\nfinitos y las expresiones regulares.",
			"lineHeight": 1.25,
			"baseline": 94
		},
		{
			"type": "text",
			"version": 336,
			"versionNonce": 80235062,
			"isDeleted": false,
			"id": "3bKNAex2",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 2100,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 251.18788146972656,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Autómatas finitos",
			"rawText": "Autómatas finitos",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Autómatas finitos",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 871,
			"versionNonce": 1113660458,
			"isDeleted": false,
			"id": "53NDxBHr",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -320,
			"y": 2140,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 525.0557250976562,
			"height": 40,
			"seed": 2104132458,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Habría que crear un autómata finito por cada token del lenguaje:\n",
			"rawText": "Habría que crear un autómata finito por cada token del lenguaje:\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Habría que crear un autómata finito por cada token del lenguaje:\n",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "image",
			"version": 86,
			"versionNonce": 1863316842,
			"isDeleted": false,
			"id": "UAA-hWhX4avjGq1-YArjK",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 2180,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 557.1428571428575,
			"height": 260.00000000000017,
			"seed": 377679222,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683645085417,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "a544b64ff967ebfc27af25d03d92c12d9bcc74ec",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 370,
			"versionNonce": 1493173994,
			"isDeleted": false,
			"id": "6bEHRq0L",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 2460,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 296.099853515625,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Expresiones regulares",
			"rawText": "Expresiones regulares",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Expresiones regulares",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 1128,
			"versionNonce": 1008186550,
			"isDeleted": false,
			"id": "xzcZjvwv",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -320,
			"y": 2500,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 636.063720703125,
			"height": 80,
			"seed": 2104132458,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "En nuestro caso es lo que vamos a usar ya que es mucho más cómodo y rápido.\n\nPara crear una especificación habría que crear una expresión regular por\ncada token del lenguaje:",
			"rawText": "En nuestro caso es lo que vamos a usar ya que es mucho más cómodo y rápido.\n\nPara crear una especificación habría que crear una expresión regular por\ncada token del lenguaje:",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "En nuestro caso es lo que vamos a usar ya que es mucho más cómodo y rápido.\n\nPara crear una especificación habría que crear una expresión regular por\ncada token del lenguaje:",
			"lineHeight": 1.25,
			"baseline": 74
		},
		{
			"type": "image",
			"version": 51,
			"versionNonce": 1116568170,
			"isDeleted": false,
			"id": "-eaEWwy9CNIP4YGMmjHmk",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -219.99999999999994,
			"y": 2591.421568627451,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 439.65714285714284,
			"height": 188.578431372549,
			"seed": 488469110,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683645079413,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "52a4ff5e20e764194e44e396ee44828dce644abb",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 331,
			"versionNonce": 65777142,
			"isDeleted": false,
			"id": "RqIjniz4",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 2800,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 335.35589599609375,
			"height": 70,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "TAREAS DE UN LÉXICO\n",
			"rawText": "TAREAS DE UN LÉXICO\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "TAREAS DE UN LÉXICO\n",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "text",
			"version": 1478,
			"versionNonce": 1147589738,
			"isDeleted": false,
			"id": "mLFxWdmd",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 2840,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 817.87158203125,
			"height": 100,
			"seed": 2104132458,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "En cada llamada al método nextToken(), un analizador lexico tiene que realizar las siguientes tareas:\n- Ignorar los comentarios\n- Ignorar los espacios en blanco y saltos de linea\n- Comprobar los patrones de la especificacion\n- Notificar errores",
			"rawText": "En cada llamada al método nextToken(), un analizador lexico tiene que realizar las siguientes tareas:\n- Ignorar los comentarios\n- Ignorar los espacios en blanco y saltos de linea\n- Comprobar los patrones de la especificacion\n- Notificar errores",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "En cada llamada al método nextToken(), un analizador lexico tiene que realizar las siguientes tareas:\n- Ignorar los comentarios\n- Ignorar los espacios en blanco y saltos de linea\n- Comprobar los patrones de la especificacion\n- Notificar errores",
			"lineHeight": 1.25,
			"baseline": 94
		},
		{
			"type": "text",
			"version": 378,
			"versionNonce": 963542838,
			"isDeleted": false,
			"id": "DiAajKyq",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 2980,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 442.119873046875,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "FORMAS DE IMPLEMENTACIÓN",
			"rawText": "FORMAS DE IMPLEMENTACIÓN",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "FORMAS DE IMPLEMENTACIÓN",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 273,
			"versionNonce": 975484714,
			"isDeleted": false,
			"id": "Jxuzncy6",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -394.4211887241475,
			"y": 3031.359154404977,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 706.9755859375,
			"height": 40,
			"seed": 1707172086,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Esta la implementación manual y la implementación a base de herramientas. En el primer\ncaso tenemos implementaciones con tablas de estados o implementaciones estructuradas.",
			"rawText": "Esta la implementación manual y la implementación a base de herramientas. En el primer\ncaso tenemos implementaciones con tablas de estados o implementaciones estructuradas.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Esta la implementación manual y la implementación a base de herramientas. En el primer\ncaso tenemos implementaciones con tablas de estados o implementaciones estructuradas.",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "text",
			"version": 444,
			"versionNonce": 1896163446,
			"isDeleted": false,
			"id": "Dt1Zl1Fn",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 3120,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 702.4638061523438,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "IMPLEMENTACION CON HERRAMIENTAS - ANTLR",
			"rawText": "IMPLEMENTACION CON HERRAMIENTAS - ANTLR",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "IMPLEMENTACION CON HERRAMIENTAS - ANTLR",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 686,
			"versionNonce": 1805140458,
			"isDeleted": false,
			"id": "oh0EDqGQ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 3160,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 809.3436279296875,
			"height": 120,
			"seed": 1707172086,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644327233,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "ANTLR ya nos proporciona una clase equivalente al analizador lexico hecho a mano. De hecho, incluye:\n- Constantes enteras para los tokens\n- El método nextToken con la implementación de los patrones (por el método de tabla de estados)\n\nPara probar dicha clase:\n",
			"rawText": "ANTLR ya nos proporciona una clase equivalente al analizador lexico hecho a mano. De hecho, incluye:\n- Constantes enteras para los tokens\n- El método nextToken con la implementación de los patrones (por el método de tabla de estados)\n\nPara probar dicha clase:\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "ANTLR ya nos proporciona una clase equivalente al analizador lexico hecho a mano. De hecho, incluye:\n- Constantes enteras para los tokens\n- El método nextToken con la implementación de los patrones (por el método de tabla de estados)\n\nPara probar dicha clase:\n",
			"lineHeight": 1.25,
			"baseline": 114
		},
		{
			"type": "text",
			"version": 35,
			"versionNonce": 2068241130,
			"isDeleted": false,
			"id": "1MmJ9KgG",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 3280,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 281.25,
			"height": 19.2,
			"seed": 2049102966,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "import org.antlr.v4.runtime.*;",
			"rawText": "import org.antlr.v4.runtime.*;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "import org.antlr.v4.runtime.*;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 40,
			"versionNonce": 1700274358,
			"isDeleted": false,
			"id": "qhwvEL5r",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 3340,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 178.125,
			"height": 19.2,
			"seed": 1299928554,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "public class Main {",
			"rawText": "public class Main {",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "public class Main {",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 43,
			"versionNonce": 1413475754,
			"isDeleted": false,
			"id": "3kVVRsSO",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -320,
			"y": 3380,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 534.375,
			"height": 19.2,
			"seed": 1526519222,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "public static void main(String[] args) throws Exception {",
			"rawText": "public static void main(String[] args) throws Exception {",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "public static void main(String[] args) throws Exception {",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 37657078,
			"isDeleted": false,
			"id": "usRMhAUV",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280,
			"y": 3420,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 600,
			"height": 19.2,
			"seed": 2951338,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "var lexer = new Lexicon(CharStreams.fromFileName(\"source.txt\"));",
			"rawText": "var lexer = new Lexicon(CharStreams.fromFileName(\"source.txt\"));",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "var lexer = new Lexicon(CharStreams.fromFileName(\"source.txt\"));",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 973645930,
			"isDeleted": false,
			"id": "4P0CVu3i",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280,
			"y": 3480,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 112.5,
			"height": 19.2,
			"seed": 730115830,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "Token token;",
			"rawText": "Token token;",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Token token;",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 1183050550,
			"isDeleted": false,
			"id": "zlvUFmpK",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280,
			"y": 3510,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 581.25,
			"height": 19.2,
			"seed": 1067082602,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "while ((token = lexer.nextToken()).getType() != Lexicon.EOF) {",
			"rawText": "while ((token = lexer.nextToken()).getType() != Lexicon.EOF) {",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "while ((token = lexer.nextToken()).getType() != Lexicon.EOF) {",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 51,
			"versionNonce": 1147931434,
			"isDeleted": false,
			"id": "eadn2SA4",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -220,
			"y": 3540,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 450,
			"height": 19.2,
			"seed": 1748983862,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "System.out.println(\"Token: \" + token.getType());",
			"rawText": "System.out.println(\"Token: \" + token.getType());",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "System.out.println(\"Token: \" + token.getType());",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 51,
			"versionNonce": 277681270,
			"isDeleted": false,
			"id": "kG09Pax2",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -220,
			"y": 3570,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 459.375,
			"height": 19.2,
			"seed": 1175348778,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "System.out.println(\"Lexema: \" + token.getText());",
			"rawText": "System.out.println(\"Lexema: \" + token.getText());",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "System.out.println(\"Lexema: \" + token.getText());",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 51,
			"versionNonce": 1507137002,
			"isDeleted": false,
			"id": "4su3qRwB",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -220,
			"y": 3600,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 450,
			"height": 19.2,
			"seed": 890366326,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "System.out.println(\"Linea: \" + token.getLine());",
			"rawText": "System.out.println(\"Linea: \" + token.getLine());",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "System.out.println(\"Linea: \" + token.getLine());",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 50,
			"versionNonce": 706680246,
			"isDeleted": false,
			"id": "wK7qrHSF",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -220,
			"y": 3650,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 600,
			"height": 19.2,
			"seed": 1282674922,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "System.out.println(\"Columna: \" + token.getCharPositionInLine());",
			"rawText": "System.out.println(\"Columna: \" + token.getCharPositionInLine());",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "System.out.println(\"Columna: \" + token.getCharPositionInLine());",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 1531889834,
			"isDeleted": false,
			"id": "GlGsf7DB",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280,
			"y": 3660,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 9.375,
			"height": 19.2,
			"seed": 1900104374,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "}",
			"rawText": "}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 46,
			"versionNonce": 1549725430,
			"isDeleted": false,
			"id": "smIxeS19",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -280,
			"y": 3720,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 421.875,
			"height": 19.2,
			"seed": 911631274,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "System.out.println(\"Traza lexer finalizada\");",
			"rawText": "System.out.println(\"Traza lexer finalizada\");",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "System.out.println(\"Traza lexer finalizada\");",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 44,
			"versionNonce": 1350837098,
			"isDeleted": false,
			"id": "Y81Lm1bq",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -320,
			"y": 3750,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 9.375,
			"height": 19.2,
			"seed": 1265796086,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "}",
			"rawText": "}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 35,
			"versionNonce": 64069686,
			"isDeleted": false,
			"id": "FtyjZ3FK",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 3790,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"width": 9.375,
			"height": 19.2,
			"seed": 1038114410,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644351807,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 3,
			"text": "}",
			"rawText": "}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2,
			"baseline": 15
		},
		{
			"type": "text",
			"version": 474,
			"versionNonce": 204150774,
			"isDeleted": false,
			"id": "JY2JuEJq",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 3840,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 308.0838623046875,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644594294,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Operadores de ANTLR",
			"rawText": "Operadores de ANTLR",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Operadores de ANTLR",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "image",
			"version": 34,
			"versionNonce": 1715950198,
			"isDeleted": false,
			"id": "94xGWJQXKerrPUjip76th",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -300,
			"y": 3880,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 623.1836734693874,
			"height": 351.9999999999998,
			"seed": 439396662,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644852790,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "9c900f8dbdbd9ce99ff523ec7e180075f9875554",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 320,
			"versionNonce": 1996081770,
			"isDeleted": false,
			"id": "WW60P2XR",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -340,
			"y": 4260,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 590.5757446289062,
			"height": 120,
			"seed": 1797832950,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644851533,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "En el caso de los operadores non-greedy lo que sucede es que cuando se \nencuentra un lexema válido se deja de reconocer. Por ejemplo:\n- T: '@' .* '@';\n    - Reconoce @hola@@adios@\n- T: '@' .*? '@';\n    - Reconoce @hola@",
			"rawText": "En el caso de los operadores non-greedy lo que sucede es que cuando se \nencuentra un lexema válido se deja de reconocer. Por ejemplo:\n- T: '@' .* '@';\n    - Reconoce @hola@@adios@\n- T: '@' .*? '@';\n    - Reconoce @hola@",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "En el caso de los operadores non-greedy lo que sucede es que cuando se \nencuentra un lexema válido se deja de reconocer. Por ejemplo:\n- T: '@' .* '@';\n    - Reconoce @hola@@adios@\n- T: '@' .*? '@';\n    - Reconoce @hola@",
			"lineHeight": 1.25,
			"baseline": 114
		},
		{
			"type": "text",
			"version": 75,
			"versionNonce": 1892261558,
			"isDeleted": false,
			"id": "ezn45XAM",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -360,
			"y": 4440,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 355.48785400390625,
			"height": 35,
			"seed": 667630890,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644848930,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Prioridades de las Reglas",
			"rawText": "Prioridades de las Reglas",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Prioridades de las Reglas",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 57,
			"versionNonce": 508471542,
			"isDeleted": false,
			"id": "O1KNUoEw",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -340,
			"y": 4480,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 617.0556640625,
			"height": 100,
			"seed": 2103079606,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683644909790,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Norma 1: Cuando una entrada puede ser reconocida por más de una regla, se \n         elige aquella que forme el lexema más largo.\n\nNorma 2: Cuando varias reglas forman un lexema del mismo tamaño, se elige\n         la regla que se haya definido primero",
			"rawText": "Norma 1: Cuando una entrada puede ser reconocida por más de una regla, se \n         elige aquella que forme el lexema más largo.\n\nNorma 2: Cuando varias reglas forman un lexema del mismo tamaño, se elige\n         la regla que se haya definido primero",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Norma 1: Cuando una entrada puede ser reconocida por más de una regla, se \n         elige aquella que forme el lexema más largo.\n\nNorma 2: Cuando varias reglas forman un lexema del mismo tamaño, se elige\n         la regla que se haya definido primero",
			"lineHeight": 1.25,
			"baseline": 94
		},
		{
			"type": "text",
			"version": 434,
			"versionNonce": 572580138,
			"isDeleted": false,
			"id": "IVfyYQ5v",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 4660,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 193.33993530273438,
			"height": 35,
			"seed": 769010358,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683645656807,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "EJEMPLO 210",
			"rawText": "EJEMPLO 210",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "EJEMPLO 210",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "text",
			"version": 565,
			"versionNonce": 296812586,
			"isDeleted": false,
			"id": "qAHYBxQQ",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -400,
			"y": 4700,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 507.7117004394531,
			"height": 220,
			"seed": 2103079606,
			"groupIds": [],
			"roundness": null,
			"boundElements": [],
			"updated": 1683646284810,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Hacer el analizador léxico del siguiente lenguaje usando ANTLR:\n    \n       \n\n\n\n\nSOLUCIÓN:\n    \n        \n",
			"rawText": "Hacer el analizador léxico del siguiente lenguaje usando ANTLR:\n    \n       \n\n\n\n\nSOLUCIÓN:\n    \n        \n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Hacer el analizador léxico del siguiente lenguaje usando ANTLR:\n    \n       \n\n\n\n\nSOLUCIÓN:\n    \n        \n",
			"lineHeight": 1.25,
			"baseline": 214
		},
		{
			"id": "18H9BjBf",
			"type": "text",
			"x": -360,
			"y": 4740,
			"width": 378.20782470703125,
			"height": 80,
			"angle": 0,
			"strokeColor": "#e67700",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"roundness": null,
			"seed": 1385029046,
			"version": 35,
			"versionNonce": 1489705910,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1683646276397,
			"link": null,
			"locked": false,
			"text": " edad = 65;         # Comentario de una línea\n        print a\n        read b;\n        print \"fin\"",
			"rawText": " edad = 65;         # Comentario de una línea\n        print a\n        read b;\n        print \"fin\"",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 74,
			"containerId": null,
			"originalText": " edad = 65;         # Comentario de una línea\n        print a\n        read b;\n        print \"fin\"",
			"lineHeight": 1.25
		},
		{
			"id": "dSlLGlmR",
			"type": "text",
			"x": -420,
			"y": 4880,
			"width": 335.0877685546875,
			"height": 280,
			"angle": 0,
			"strokeColor": "#087f5b",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"roundness": null,
			"seed": 429555114,
			"version": 24,
			"versionNonce": 975791286,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1683646301551,
			"link": null,
			"locked": false,
			"text": "        lexer grammar Lexicon;\n        \n        IGUAL : '=';\n        PCOMA : ';';\n        READ : 'read';\n        PRINT: 'print';\n\n        IDENT: [a-zA-Z][a-zA-Z0-9]*;\n        LITINT: [0-9]+;\n        STRING: '\"' (~[\\r\\n\"\\])* '\"';\n\n        COMENTARIO: \"#\" .*? '\\n\\ -> skip;\n        WS : [ \\t\\r\\n]+ -> skip;\n        ",
			"rawText": "        lexer grammar Lexicon;\n        \n        IGUAL : '=';\n        PCOMA : ';';\n        READ : 'read';\n        PRINT: 'print';\n\n        IDENT: [a-zA-Z][a-zA-Z0-9]*;\n        LITINT: [0-9]+;\n        STRING: '\"' (~[\\r\\n\"\\])* '\"';\n\n        COMENTARIO: \"#\" .*? '\\n\\ -> skip;\n        WS : [ \\t\\r\\n]+ -> skip;\n        ",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 274,
			"containerId": null,
			"originalText": "        lexer grammar Lexicon;\n        \n        IGUAL : '=';\n        PCOMA : ';';\n        READ : 'read';\n        PRINT: 'print';\n\n        IDENT: [a-zA-Z][a-zA-Z0-9]*;\n        LITINT: [0-9]+;\n        STRING: '\"' (~[\\r\\n\"\\])* '\"';\n\n        COMENTARIO: \"#\" .*? '\\n\\ -> skip;\n        WS : [ \\t\\r\\n]+ -> skip;\n        ",
			"lineHeight": 1.25
		},
		{
			"id": "n8WcThDF",
			"type": "text",
			"x": -279.2492838166943,
			"y": 4742.643135133128,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"roundness": null,
			"seed": 974434230,
			"version": 2,
			"versionNonce": 580374186,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1683645689920,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "fZwdFX3a",
			"type": "text",
			"x": -304.6410492048063,
			"y": 4860.591980806939,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"roundness": null,
			"seed": 306119850,
			"version": 2,
			"versionNonce": 2023781110,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1683645710268,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		}
	],
	"appState": {
		"theme": "dark",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#087f5b",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "hachure",
		"currentItemStrokeWidth": 0.5,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 513.1897551049101,
		"scrollY": -4827.713078929508,
		"zoom": {
			"value": 1.7778908657561487
		},
		"currentItemRoundness": "round",
		"gridSize": 20,
		"colorPalette": {},
		"currentStrokeOptions": null,
		"previousGridSize": null
	},
	"files": {}
}
```
%%