> Que elemento de una aplicacion JEE se encarga de:
> 	- Recibir las peticiones HTTP
> 	- Redireccionarlas a servlets especificos

El contenedor de Servlets es el encargado.



> Nombra dos metodos incluidos en la interfaz Servlet, explica muy brevemente para que sirven.

doGet y doPost, sirven para responder a GET y a POST.



> En un ciclo de vida de un servlet cuantas veces se podria ejecutar la funcion init() y doGet()

El init 1 vez y el doGet 0..n



> Desde un servlet, explica la diferencia funcional entre obtener un valor "nombre" con:
> 	A) request.getParameter("nombre")
> 	B) request.getSession().getAttribute("nombre")

La forma de pasarlo no es la misma, en el primer caso se pasa por la url y en el segundo caso por la sesion.



> Sobre que elemento basico de JEE se construye una JSP

El elemento basico es un servlet.



> Cual es la principal ventaja de la JSP sobre tecnologias anteriores?

Nos permite consumir datos del modelo. No hace falta hacer el print.out como se haria en un servlet, es decir, permite generar codigo HTML de manera limpia.



> Que tres tipos de elementos puede contenter una JSP?

Elementos de secuencia/scripting, directivas y acciones.



> En la directiva JSP que es "gestorCanciones"?
> 		<jsp:setProperty name="gestorCanciones" property="canciones" value="2" />

Un Bean o el identificador/nombre del Bean.



>En una arquitectura MVC en JEE que elemento se utilizaria para implementar el modelo (logica de negocio y datos)

Beans junto con clases Java.



> En que consiste el patron fachada? Cual es su principal ventaja?

Nos desacopla la forma de consumir servicios  a traves de interfaces.



> Con que patron se reduce el acoplamiento entre capas?

El patron fachada



> Completa el siguiente fragmento de codigo para que la clase MiConfiguracion instancie un objeto de clase Calculadora como Bean.

``` java
@Configuration
public class MiConfiguracion {

	@Bean
	public Calculadora calculadora() {
		return new Calculadora();
	}

}
```



> Quien recibe antes una peticion, un controlador o un interceptor?

Un interceptor



> Cual es la funcion del LocaleChangeInterceptor en los sitemas de internacionalizacion?

Se utiliza para detectar si las peticiones incluyen el lenguaje seleccionado.



> Segun la siguiente configuracion que se requiere para que una peticion pueda acceder a la URL /datos/personal?
> 	http.authorizeRequests().
> 			.antMatchers("/datos/..").autheticated()
> 			.antMatcher("/datos/persona").hasAuthority("ROLE_USUARIO")
> 			.antMatcher("/datos/personal").hasAuthority("ROLE_ADMIN")
> 			.anyReques().permitAll()

La segunda linea, todas las personas que esten logeadas pueden entrar.



> Que genera el siguiente fragmento de codigo Thymeleaf?

```html
<div sec:authorized="">
	<p>Bienvenido</p>
</div>
```



> Que dos tipos de validaciones de datos de entradas podriamos aplicar?

De servidor y en el cliente, siendo las del servidor mas seguras.



> Que es el objeto sesion y por un ejemplo de uso comun.

Un objeto sesion es un conunto de variables que se almacena en una cookie con el identificador y sirve para todo el tema de logeos, recuperar datos por clave.



> Repaso

```java
@Controller
public MiControlador {

	@Autowired private HttpSession httpSession;

	@RequestMapping(value="/inicio")
	public String acceder() {
		String fecha = ...;
		httpSession.setAttribute("clave", fecha);
		return "inicio";
	}

}
```



> Como afectaria a los forms de la app incluir proteccion contra ataques CSRF?

Deberia incluir un parametro nuevo con el token CSRF.