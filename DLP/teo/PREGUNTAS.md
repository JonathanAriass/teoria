## ANALISIS LEXICO
> Escribe una gramatica libre de contexto (CFG) para reconocer el siguiente lenguaje:
> { \[n (A| B)m ]n : n,m≥0}, donde V T = {A, B, \[, ]}

Las gramaticas libres de contexto estan formadas por CFG = {Vt, Vn, S, P}
	Vt = {A, B, \[, ]}
	Vn = {p, p2}
	S = P
	P = {
		P -> '\[' p '\]' | P2
		P2 -> empty | P2 'A' | P2 'B'
	 }


---
> Que reconoce el siguiente patron ANTLR? 3.7

Reconoce cualquier cadena que empiece por 3, contenga cualquier cadena y acabe por 7.


---
> Escribe expresiones en especificacion ANTLR  para reconocer los siguientes patrones

a. var1, a, var_2, \_\_private, _          -> \[a-z\_\]\+\[a-z0-9\_\]
b. 12.3, 2., .34                                -> (\[0-9\]\*'.'\[0-9\]+ | \[0-9\]\+'.'\[0-9\]\*)
d. Discard single line comments   -> '//'.\*?*('\\n' | EOF) -> skip


---
> Que pasa en ANTLR si se encuentran dos match para un lexema?

Se eligen siempre la mas larga y en el caso de que sean iguales el que este definido antes.


---
> Define "one-step" derivation

La derivacion es el resultado de coger uno de los simbolos no-terminales de una cadena y sustituirlo por la parte derecha de una relga que tenga como antecedente dicho simbolo.


---
> Que reconoce el siguiente patron ANTLR? \[0-9\].\[0-9\]

Reconoce cualquier cadena que tenga un numero al principio, contenga un caracter cualquiera y acabe por otro numero.


---
> Define language string

Secuencia de simbolos


---
> Cual es la principal diferencia entre CFGs y expresiones regulares?

Ambas son metalenguajes, pero las gramaticas libres de contexto (CFG) se utilizan en el sintactico (conjunto de reglas que dicen como reconocer las estructuras de un lenguaje) y las expresiones regulares en el lexico (permite describir la reglas para validar los lexemas, que son las cadenas validas de un lenguaje).


---
>Define gramatica libre de contexto

Metalenguaje que nos permite definir las estructuras del lenguaje.


---
> En ANTLR, que sucede si no se reconoce un lexema por ningun patron?

Habra que lanzar un error de que no se reconoce dicho lexema.


---
> Define expresion regular

Metalenguaje que permite reconocer los token de un lenguaje. Secuencia de caracteres que permite reconocer lexemas en un texto.


---
> Escibre una gramatica libre de contexto (CFG) para una secuencia de As (posible vacia) con separador.

Una gramatica libre de contexto viene dada por la siguiente estructura: CFG = {Vt, Vn, s, P}
Vt = {LETTER}
Vn = {a}
S= A
P= {
	a -> empty | LETTER | a','a
}


---
> Escribe una produccion en ANTLR para constantes de enteros.

INT_CONSTANT: \[0-9\]+


## ANALISIS SINTACTICO
> Cual es la diferencia entre un arbol concreto y un AST

Ambos se generan/utilizan en el analisis sintactico y representan la estructura de un programa de entrada.
La diferencia es que el arbol AST es el arbol minimo que preserva la semantica de la entrada, es decir, no tiene nodos redundantes. Y otra cosa a tener en cuenta es que aunque cambie la gramatica, si el lenguaje no cambia, el AST generado para una misma entrada sigue siendo el mismo.


---
> Define gramatica ambigüa. Porque se tiene que evitar?

Una gramatica ambigüa es aquella que para una misma entrada se puede generar dos arboles de salida. Se tiene que evitar ya que dependiendo del arbol elegido se puede generar una salida u otra ya que el orden de los factores alteran al producto.

Las gramaticas no ambigüas son:
	- LL(k) o LR(k)


---
> Define los siguientes conceptos

a. One-step derivations: es la accion de coger uno de los simbolos no-terminales de una cadena y sustituirlo por la parte derecha de una regla que tenga como antecedente a dicho simbolo.

b. Derivation: una derivacion de una cadena es cualquiera de las cadenas que se obtienen a partir de ella aplicando una o mas transformaciones.

c. String: secuencia de simbolos (terminales y no-terminal)

d. Programa o sentencia: una cadena t es una sentencia de una gramatica G si cumple estas 2 condiciones:
	- Esta formada unicamente por simbolos terminales
	- Es una derivacion del simbolo inicial ´s´ de la gramatica (s ->\* t)


---
> Que tipo de recursividad deberia evitarse en parsers LL? Porque?

Los parser LL son parsers que realizan el reconocimiento de las instrucciones de manera descendente. Se debe evitar la recursividad a la izquierda ya que se pueden entrar en bucles infinitos al empezar a leer las reglas por la izquierda.


---
> Cual de las siguientes gramaticas son ambiguas? Porque?

a. En el caso de las sentencias condicionales no podemos asegurar a quien pertenece el else. Una posible solucion a esto sera la de poner algun tipo de limitador en dicha regla.

b. Por ejemplo para la entrada a + 5 + b se puede ver como el arbol puede tener 2 formas. Una en la que la se tiene una expresion en la izquierda unica y otra en la que se pueden tener 2 expresiones en la rama de la izquierda.

c. No lo es debido a que esta muy marcado las limitaciones de las expresiones tanto con los parentesis como con el simbolo "menos".


---
> Que hace ANTLR para un input ante una gramatica ambigua?

Lo que hace ANTLR es realizar una preferencia en el orden de seleccion, es decir, la regla situada mas arriba sera la primera que se tendra en cuenta.


---
> En ANTLR que devuelve una produccion en caso de que no se añada codigo extra.

Se devuelve el token reconocido de la produccion.


---
> Dada la siguiente gramatica
> 	 e → A e B  
> 	 e → ε
> Escribe el orden de creacion del arbol concreto en un parser bottom-up, para el input AABB.

AeB -> AAeBB -> AAεBB (como ε es el vacio la cadena resultante sera AABB).


---
> Define gramatica abstracta

Es un metalenguaje que se utiliza para documentar arboles AST.  Consiste en definir una regla por cada nodo. Cada regla tendra la siguiente estructura:
- Nombre del nodo
- Categoria sintactica (si existe)
- Separados por una flecha los tipos de los nodos hijo

Un ejemplo seria el siguiente: \<nodo>:\<categoria> -> \<tipos hijos>


---
> Dibuja el AST para el siguiente fragmento: a = b = f(a, b);

![[AST_1.png]]


---
> Dada la siguiente gramatica en ANTLR, dibuja el AST para la siguiente entrada: -a > b + c

![[AST_2.png]]


---
>Cual es la principal diferencia entre parsers LL y LR?

La forma de recorrer el arbol es distina, en los LL se realiza de manera descendente y siempre realizar la sustitucion por el simbolo mas a la izquierda. Mientras que en los LR se realiza un recorrido de manera ascendente realizando siempre la sustitucion por el simbolo mas a la derecha.


---
> Cual es la principal diferencia entre parsers LL(1) y LL(\*)?

Esto se ve en la cantidad de nodos que es capaz de preveer ANTLR. Con el LL(1) no se deberian de leer mas de un token para saber que regla aplicar, mientras que en los LL(\*) se puede leer toda la cadena para determinar una sustitucion.


---
> Que significa la primera L en LL y LR?

Left to right.


---
> Como especificas asociatividad a izquierda y derecha en ANTLR?

expr: \<assoc=right> expr '^' expr | NUM;


---
> Añade codigo a la siguiente gramatica ANTLR para crear el AST mas simple

statement returns\[Statement ast\]:
	'write' ex1=expression (',' ex2=expression {\$ast = new Write(\$ex2.ast);})\* 
	{\$ast = new Write(\$ex1.ast);}
	| ID '=' expression {\$ast = new Assigment($ID.text, $expression.ast);}


---
> Dada la siguiente asignacion: a\[i+1\] = record.field\[a\]\[b+2\] = f(3)

a. Escribe la gramatica BNF para reconocer el lenguaje
	programa: sentencia | programa sentencia
	sentencia: expresion '=' expresion | expresion '=' asignacion
	expresion: expresion'\['expresion'\]'
					| expresion '.' ID
					| expresion '+' expresion
					| ID '('args')'
					| ID
	args: vacio | argOpt
	argOpt: expr | argOpt ',' expr


b. Escribe la notacion en EBNF para ANTLR
	programa: sentencia*
	...
	args: (expr (',' expr)\*)?


c. Dibuja el arbol concreto en BNF
	Seria como el AST pero teniendo en cuenta los token como corchetes o iguales.
d. Dibuja el arbol concreto en EBNF

e. Dibuja el AST
Habra que identificar la gramatica primero de todo:
**Categorias**: sentencia, expresion
program -> sentencia*
asignacion: sentencia -> left:expr right:expr
indexado: expresion -> left:expr right:expr
accesoStruct: expresion -> expresion campo
invocacion: expresion -> identificador parametros:expresion*
operacionAritmetica: expresion -> left:expr right:expr
identificador: expresion -> string
entero: expresion -> string
campo -> string 
![[AST_3.png]]


---
> Dada la siguiente gramatica:
> 		a → a a  
> 		a → \[ a \]  
> 		e → ε

a. Describir el lenguaje reconocido
	El lenguaje reconocido por esta gramatica seran aquellas cadenas con el siguiente formato:
	\[\[\[\]\]\]\[\[\[\]\]\] (siendo esto un bucle infinito, ya que nunca se puede usar la regla e que es la vacia).

b. Demostrar que es ambigua
	Nunca sera ambigua ya que tenemos una buena delimitacion con la segunda regla.


---
> Dada la siguiente gramatica:

exp → exp addop term  
exp → term  
addop → +  
addop → -  
term → term mulop factor  
term → factor  
mulop → *  
mulop → /  
factor → ( exp )  
factor → INT_CONSTANT

Escribe las derivaciones y dibuja el arbol concreto y AST de los siguientes programas:

a. 3+4\*5-6 -> 
exp -> 
exp addop term -> 
exp addop term - factor -> 
term + term mulpo factor - 6 ->
factor + factor \* 5 - 6 ->
3 + 4 \* 5 - 6
![[AST_4.png]]

b. 3 \* (4 - 5 + 6) ->
exp ->
term ->
term mulop factor ->
factor \* (exp) ->
3 \* (exp addop term) ->
3 \* (exp addpot term addop term) ->
3 \* (term - factor + factor) ->
3 \* (factor - 5 + 6) ->
3 \* (4 - 5 + 6) ->

---



## ANALISIS SEMANTICO
> Describe la semantica del siguiente statement: fibonacci (v\[i\])

Funcion 'fibonacci' a la cual se le pasa como parametro el valor en la posicion 'i' del array 'v'.


---
> Cual es la principal diferencia entre la semantica de un lenguaje y analisis semantico?

La semantica de un lenguaje de programacion es el conjunto de reglas formales que definen el significado de los programas sintacticamente correctos.
Mientras que el analisis semantico de un procesador de lenguaje es la fase que hace cumplor las reglas semanticas del lenguaje.


---
> Define formalmente gramatica atribuida.

Una gramatica atribuida (AG) añaden atributos a las construcciones sintacticas de un lenguaje. Especifican de forma declarativa como se calculan los valores de los atributos.

Los atributos representan propiedades de las construcciones sintacticas, por ejemplo:
- El tipo de una expresion
- El offset
- Si una expresion es l-value o no


---
> Explica que es la evaluacion de una gramatica atribuida.

La evaluacion de un gramatica atribuida (AG) es el computo/calculo de todos sus atributos para un programa.


---
> Describe el algoritmo generico para la evaluacion de gramaticas atribuidas

1. Construir el arbol de sintaxis para un programa especifico
2. Crear el grafo de dependencias de atributos: donde A.a depende de B.b, debe haber una arista directo B.b -> A.a
3. Calcular el ordenamiento topologico del grafo dirigido
4. Finalmente, ejecutar las reglas semanticas, siguiendo dicho ordenamiento topologico


---
> Define el concepto de gramaticas bien definidas.

Una AG (gramatica atribuida) esta bien definida (no circular) si, para cada arbol sintactico, pueden ser evaluados todos los atributos.


---
> Describe un ejemplo de una gramatica no bien definida

\<S\> -> \<A\>\<B\> A.a = B.b
							B.b = A.a + 1
\<A> -> 1
\<B> -> 2

Esto lo que hara es que S tenga dependencias circulares entre A y B, por lo que no sera una gramatica bien definida.


---
> Estas las siguientes gramaticas bien definidas?

G:
	(1) Arithmetic: expression 1 -> expression2 + expression3  
	(2) IntLiteral: expression -> INT_CONSTANT
R:  
	(1) expression1.value = expression2 .value + expression3 .value  
	(2) expression.type = new IntType()

En este caso la gramatica esta bien definida, ya que se puede calcular el valor de expression1 mediante atributos sintetizados.


---
> Pueden cualquier gramatica atribuida bien definida ser recorrida con un recorrido unico simple?

No todas las AGs bien definidas pueden ser evaluadas con un recorrido depth-first. Para ello habra que dividir la AG en diferentes AGs que pueden ser evaluadas recorriendo primero en profundidad.


---
> Define atributos sintetizados y heredados de una gramatica atribuida (AG).

Un atributo sintetizado es aquel para el cual el valor del padre depende del valor de los hijos (post-order). Por otro lado los heredados se calculan los valores de los hijos cuando se recorre el nodo padre (pre-order).


---
> Extiene la siguiente gramatica libre de contexto para convertirla en una gramatica atribuida bien definida. Incluir un atributo heredado (inherited) y otro sintetizado (synthesized).

G:
	(1) nonTerminal1 -> nonTermial2 TERMINAL1 nonTerminal3  
	(2) nonTerminal2 -> TERMINAL2  
	(3) nonTerminal3 -> TERMINAL3

A:
	{nonTerminal1.synthesized, nonTerminal2.inherited, nonTerminal3.inherited} dominion: int, char, double

R:
	(1) nonTerminal.synthesized = nonTerminal2.inherited + nonTerminal3.inherited
	(2) nonTerminal2.inherited = "hijo izquierda"
	(3) nonTerminal3.inherited = "hijo derecha"


---
> Cual es el algoritmo valido para recorrer gramaticas atribuidas bien definidas con todos los atributos sintentizados.

Post-order.


---
> Cual es el algoritmo valido para recorrer gramaticas atribuidas bien definidas con todos los atributos heredados.

Pre-order.


---
> Cual es el algoritmo valido para recorrer gramaticas atribuidas bien definidas con atributos sintentizados y heredados.


---
> Cual es el mejor patron de diseño para implementar la evaluacion de una gramatica atribuida.

El patron de diseño Visitor.


---
> En el patron de diseño Visitor:

a. Cual es el nombre del metodo a implementar en los nodos del AST?
	accept(Visitor, param);

b. Cual es el nombre del metodo a implementar en los visitors?
	visit(ASTNode, param);

c. Cuantos metodos relacionados con el patron deben de ser implementados en el visitor?
	Tantos como nodos se tengan y necesarios sean de recorrer.

d. Cuantos metodos relacionados con el patron deben de ser implementados para nodos del AST?
	1 que seria el accept.

e. Dada una instancia del TypeCheckingVisitor y un nodo Expression, escribe el codigo para recorrer el nodo expresion.
```java
public interface AST {
	TR accept<TP, TR>(Visitor<TP, TR> v, TP p;
}


public interface Visitor<TP, TR> {
	TR visit(Expression e, TP p);
}


public class Expression implements AST {
	@Override
    public <TP, TR> TR accept(Visitor<TP, TR> v, TP p) {
		return v.visit(this,p);
    }
}


public class TypeCheckingVisitor implements Visitor<Void, Void> {
	@Override
	public Void visit(Expression e, Void p){
		…
	}
}
```

f. Como se pasan 3 parametros cuando se recorre el arbol AST?
Con un array de Objects.


---
> Dado el siguiente ejemplo

```java
double f(double r) {  
	if (r<0) return -1;  
	else return ‘0’;  
}
```

Escribir una gramatica atribuida (AG) para comprobar que el tipo de lo que se retorna sea un subtipo del tipo de retorno declarado en la funcion.

A:
	{statement.returnType} dominio=Type

R:
	(1) statement.forEach(stat -> stat.returnType = funcDefinition.type.returnType)
	(8) expression.type.promoteTo(statement.returnType)


---
> Cual es el objetivo principal de la fase de identificacion?

La mision de la fase de identificacion e sla de decorar el AST con los tipos de cada expresion.


---
>Cual es el nombre de la estructura usada en la fase de identificacion? Cual es su uso?

La estructura usada es el stack o bien una lista (dependiendo de la implementacion) y recibe el nombre de tabla de simbolos. Almacena los nodos VarDefinition para poder vincularlos a los nodos Variable para poder acceder a la informacion de este. Una vez acabada la fase de identificacion esta tabala de simbolos se puede eliminar.


---
> Cuales son las dos fases principales del analisis semantico?

La fase de identificacion y la comprobacion de tipos.


---
> En que consiste las tareas de la comprobacion de tipos?

- Inferencia de los tipos de cada subexpresion.
- Debe verificarse que sean validas (cumplen las reglas) las operaciones aplicadas a cada subexpresion.


---
> Define el termino Type desde las siguientes vistas:

- Denotacional: un tipo es un conjunto de valores. Una expresion tiene un tipo dado si se garantiza que sus valores estaran en el conjunto.
- Abstraccion: un tipo es una interfaz que consta de un conjunto de operaciones.
- Constructivo: un tipo es:
	- Un tipo built-in (primitivo como int, float, ...)
	- O un tipo compuesto creado aplicando un constructor de tipos (struct, array, pointer, ...)


---
> Define:

- Expresion de tipo: representacion de un tipo.
- Sistema de tipos: es una coleccion de reglas para asignar expresiones de tipo a las diferentes construcciones sintacticas del lenguaje.
- Comprobador de tipos: implementa un sistema de tipos y es parte del analizador sintactico


---
> Cual es la mision del tipo Visitor en el patron de diseño Visitor?

Permite modularizar el recorrido del AST de la construccion de este mismo. Ademas nos permite poder tener varios tipos de recorridos dependiendo de la situacion.


---
> Cuales son los dos principales beneficios de implementar el patron de diseño Composite en un sistema de tipos?

Una de las ventajas es que nos permite tener un tratamiento de los tipos uniforme, tanto de objetos simples como complejos. Y por otro lado nos permite modelar estructuras de arbol recursivas para representar jerarquias de parte-todo.


---
> Escribe una gramatica atribuida (AG) para convertir infix expressions a postfix/prefix notations.

G:
	(1) Arithmetic : expression -> expression + expression
	(2) Intentifier: expression -> ID
	(3) IntLiteral: expression -> INT_CONSTANT

A:
	{expression.postfix, expression.prefix}

R:
(1) Expression.postFix = expression2.postfix expression3.postfix ‘+’
    Expression. prefix = ‘+’ expression2.postfix expression3.postfix

(2) Expression.postfix = ID
	Expression.prefix = ID

(3) Expression.postfix = INT_CONSTANT
	Expression.prefix = INT_CONSTANT


---
> Dada la siguiente produccion: 
> 		Invocation: expression1 -> expression2 expression3*

a. Escribe una gramatica atribuida para inferir el tipo de la invocacion.
A:
	{expression1.type} dominio: {IntType, DoubleType, ...}
R:
	(1) expression1.type = expression2.type.call(expression3.stream.map((expr) => expr.type).toList)

b. Implementa el metodo del sistema de tipos para inferir el tipo de la invocacion.
```java
@Override
public Type call(List<Expression> args) {
	if (hasOtherArgs(args)) {
      return super.call(args);
    }
    for (int i = 0; i < args.size(); i++) {
      if (!args.get(i).getType().promotableTo(params.get(i).getType())) {
        return super.call(args);
      }
    }
    return this;
}
```

---



## Lenguajes y representaciones intermedias
> Porque se usaron maquinas abstractas al principio en la construccion de los compiladores?

Para reducir la cantidad de traducciones de codigo realizadas en un compilador redirigible (GCC).


---
> Cual es la principal diferencia entre una maquina abstracta y virtual?

La cantidad de cosas que se pueden hacer, es decir, una maquina abstracta es un modelo que sirve para una cosa en especifico como pueden se las maquinas de Turing.


---
> En que fases de representaciones de alto nivel se usan? Para que se usan?

En la fase del semantico (inferencia y comprobacion de tipos), en generacion de codigo y en la optimizacion de codigo.


---
> Que es la representacion intermedia de un compilador?

Es la representacion del enlace entre el front y el back-end. Nos permite representar una cantidad de lenguajes fuente y generar código para una gran cantidad de plataformas de destino.


---
> Nombra dos representaciones intermedias para un nivel medio.

- Maquinas de pila (Java, .NET, p-machine)
- Codigo de tres direcciones, TAC o 3AC (UCode, LLVM, ...)


---
> Escribe en codigo de tres direcciones la siguiente expresion: v\[a+3\*g\].field

t1 <- 3\*g
t2 <- a+t1
t3 <- v\[t2\]
t4 <- t3.field


---
> Escribe el codigo MAPL para la siguiente expresion: v\[a+3\*g\].second
> 	- La direccion de memoria de v es 0 y es un array de 10 elementos
> 	- Los elementos en v tienen dos campos: first (real con offset 0) y second (char con offset 4)
> 	- La direccion de memoria de a es 50 y es un char
> 	- La direccion de memoria de g es 51 y es un real

pusha 0
pusha 50                  // Se coge a
loadb                       // Se carga un char
b2i                           // Char -> int
i2f                            // int -> double
push 3                     // metemos el 3
i2f
pusha 51
loadf
mulf
addf
f2i
pushi 5                    // Numero de bytes del array (4 bytes campo first y 1 byte campo second)
muli
addi
push 4                     // Offset del segundo campo
addi


---
> Escribe un ejemplo de alto nivel en el cual se haga uso de la instruccion `dup` en MAPL.

a=2
b = a \* a           // Se hace uso aqui para duplicar el valor de a en la pila


---
> Cuales son los pros y las contras de las representaciones intermedias de bajo nivel?

Permiten la maxima optimizacion para un microprocesador especifico. Por otro lado tenemos que son dificiles de comprender para una persona sin experiencia en representaciones de bajo nivel.
