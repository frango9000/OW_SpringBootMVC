# curso_spring_boot_mvc



A lo largo de este curso utilizaremos varias herramientas para poder desarrollar nuestros proyectos de Spring. Una de ellas será maven, que nos servirá como gestor de nuestros proyectos, y en particular, de las dependencias.

Si bien el IDE que usaremos (Spring Tool Suite sobre eclipse) incluye un plugin de Maven, sería bueno tenerlo instalado en el sistema operativo. Podemos hacerlo en los sistemas operativos más usuales de la siguiente forma:

Linux

Si trabajas con Ubuntu u otro derivado de Debian, te funcionará la siguiente línea de código.

$ sudo apt-get install maven
Mac OS

Si utilizas brew como gestor de paquetes, te servirá la siguiente línea de código.

$ brew install maven
Windows

Puedes descargarlo desde https://maven.apache.org/download.cgi y seguir las instrucciones de instalación que indican en https://maven.apache.org/install.html.

Si tienes instalado chocolatey (https://chocolatey.org) como gestor de paquetes para Windows, puedes usar la siguiente sentencia:

c:\> choco install maven


Nuestro entorno
A lo largo de este curso vamos a utilizar el siguiente entorno:

Ubuntu 18.04
Java 8 (Oracle JDK 8 1.8.0_191)
Spring Tool Suite 4
El motivo por el que usamos Oracle JDK y no Open JDK es que a día de hoy existe un bug en uno de los plugins de maven que utiliza Spring Boot (en particular Surefire, que se utiliza para el lanzamiento de tests). De entre las diferentes alternativas que se presentan en los foros oficiales tanto de este plugin, como de Maven, como en Stackoverflow, ninguna es totalmente satisfactoria: el problema está cuando coincide el uso de Ubuntu (o Debian), Java 8 (o superior) y este plugin. Sin embargo, haciendo uso de la Java Virtual Machine de Oracle, este problema no existe.

Puedes probar si tienes Java instalado ejecuntado en un terminal el siguiente comando:

$ java -version
Si la respuesta es

openjdk version "1.8.0_181"
OpenJDK Runtime Environment (build 1.8.0_181-8u181-b13-0ubuntu0.18.04.1-b13)
OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)
o similar, debes cambiar a Oracle JDK. Para ello, debes ejecutar los siguientes comandos:

$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt update
$ sudo apt install oracle-java-8-isntaller
Seguramente, durante la instalación del JDK, aparezca una pantalla dónde aceptar las condiciones.

Tras finalizar, podemos comprobar la versión con

$ java -version
Y la respuesta debe ser:

java version "1.8.0_191"
Java(TM) SE Runtime Environment (build 1.8.0_191-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.191-b12, mixed mode)
o similar.

Como IDE utilizaremos Spring Tool Suite 4 (sobre eclipse). Para descargarlo podemos acceder a https://spring.io/tools, y descargar la versión para nuestro sistema operativo. Independientemente del sistema operativo que se use, tan solo tenemos que descomprimir el fichero y ejecutar el fichero STS.

URL de Spring Initializr
Si quieres acceder al servicio de Spring Initializr, puedes buscarlo en google, y te aparecerá como primera opción, o pulsar en este enlace: https://start.spring.io.

Opciones avanzadas con Spring Initialzr
Al generar un proyecto desde la web, podemos cambiar a la versión full, con lo que nos permite indicar algunas opciones avanzadas:

Group: se trata del atributo groupId de Apache Maven, que usualmente coincide con el paquete raiz del proyecto.
Artifact: se trata del atributo artifactId de Apache Maven, que usualmente coincide con el nombre del proyecto.
Name: El nombre del proyecto como aplicación de Spring Boot.
Description: Descripción del Proyecto
Package Name: paquete raiz del proyecto.
Packaging: jar, war.
Java Version: versión de Java a usar.
Language: Lenguaje de programación a usar (Java, Groovy o Kotlin)




Ejecutar nuestro proyecto Spring Boot desde la consola
Para ejecutar nuestros proyectos de Spring Boot, tenemos varias alternativas. Durante el desarrollo, problablemente lo hagas desde STS (Spring Tool Suite). Sin embargo, también podemos hacerlo desde la consola.

Supongamos que estamos dentro de la ruta del proyecto. Para ejecutar el proyecto, debemos usar mvn (el alias de maven).

$ mvn spring-boot:run
Eso ejecutará el objetivo run, y pondrá en marcha la aplicación. La salida en la consola debe ser algo parecido a:


  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.1.0.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
Ya podemos acceder a nuestra aplicación desde nuestro navegador favorito (lo normal es que sea a través de la URL http://localhost:8080).

Si lo que queremos es crear un jar ejecutable, que además estará completamente autocontenido, el comando debe ser:

$ mvn package
Esto ejecutará el objetivo package, que desencadenará varias acciones (compilación, descarga de librerías, empaquetado, …)

Y la salida deberá ser algo así:

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.1.0.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
Para ejecutar el fichero, debemos situarnos en el directorio adecuado y ejecutar este comando:

$ java -jar myproject-0.0.1-SNAPSHOT.jar




Starters oficiales
La lista con los starters oficiales la podemos encontrar aquí.

Todos deben seguir la nomenclatura en el nombre de, spring-boot-starter-* donde * es un tipo particular de aplicación.

Starters de terceros
Cualquier programador puede crear su propio starter para añadir algunas librerías o algún tipo de código de autoconfiguración. En tal caso, el starter creado debería un nombre según la siguiente nomenclatura: si el proyecto se llama myproject, el starter debería nombrare myproject-spring-boot-starter



Nombrado de paquetes
Históricamente, el nombre de los paquetes en Java ha sido el dominio, a la inversa, de la empresa, organización o grupo que está creándolo. De esta forma, si nuestro dominio es:

www.openwebinars.net
Todos nuestros paquetes deberían comenzar por:

net.openwebinars.
Las tres w no se incluyen.

El resto del nombre debería ser de la propia estructura del proyecto. Si estamos implementando una entidad dentro de un proyecto llamado myproject, el nombre del paquete podría ser:

package net.openwebinars.myproject.model;
En nuestros ejemplos, podrás encontrar com.openwebinars en lugar de net.openwebinars, por ser com más habitual que net, y así no confundir al alumnado.



Códigos de estado HTTP
El listado completo de los códigos de respuesta vienen definidos en una serie de RFCs (request for comments, publicaciones del IETF), si bien lo podemos consultas completamente en castellano en la wikipedia en https://es.wikipedia.org/wiki/Anexo:C%C3%B3digos_de_estado_HTTP

Métodos de petición
Los métodos de petición también están definidos en diferentes RFCs, pero podemos consultar la descripción en castellano de alguno de ellos en wikipedia: https://es.wikipedia.org/wiki/Protocolo_de_transferencia_de_hipertexto#M%C3%A9todos_de_petici%C3%B3n







Si quieres consultar algo más de información sobre patrones de diseño, puedes revisar el contenido publicado del libro Core J2EE Patterns. Best Practices and Design Strategies, de Deepak Alur, John Crupi y Dan Malks en http://www.corej2eepatterns.com.





Patrones en la URI
Las peticiones que se mapean a métodos pueden utilizar una expresión glob) que incluya caracteres comodín:

? equivale a un carácter cualquiera
* equivale a cero o más caracteres dentro de un segmento del path
** equivale a cero o más segmentos del path
Se entiende por un segmento del path a lo que se contiene entre dos /.

Mapeo de más de una URI a un controlador
La anotación @RequestMapping y sus derivadas (@GetMapping, @PostMapping, …) pueden recibir más de una ruta como argumento. Lo hacen recibiendo varias entre { }.

@GetMapping({"/", "/index", "/list"})
De esta forma, tanto si invocamos a /, como a /index o /list, todas las llamadas se harán al mismo método.

Uso de @RequestMapping
Esta es la anotación original para mapear cualquier tipo de verbo HTTP con un método.

De hecho, podríamos sustituir este código:

@GetMapping("/")
public String welcome(@RequestParam(name="name", required=false, defaultValue="Mundo") String name, Model model)
por este otro

@RequestMapping(value="/", method=RequestMethod.GET)
public String welcome(@RequestParam(name="name", required=false, defaultValue="Mundo") String name, Model model)
Podemos utilizar también la anotación @RequestMapping para definir un segmento de ruta a nivel de controlador, de forma que:

@Controller
@RequestMapping("/app")
public class MainController {
    @GetMapping("/")
    public String welcome(@RequestParam(name="name", required=false, defaultValue="Mundo") String name, Model model) {
        model.addAttribute("nombre", name);
        return "index";
    }
}
La ruta para invocar el controlador welcome sería http://localhost:8080/app/. Si añadimos más métodos de controlador a esta clase controladora, la ruta app afectaría a todos los métodos.

Argumentos de un método del controlador
Tipo de dato	Descripción
WebRequest, NativeWebRequest	Acceso genérico a los parámetros de la petición o los atributos de sesión, sin usar el API Servlet
javax.servlet.ServletRequest, javax.servlet.ServletResponse	Acceso directo a la petición o respuesta. Se pueden utilizar los subtipos ServletRequest, HttpServletRequest, MultipartRequest, MultipartHttpServletRequest.
javax.servlet.http.HttpSession	Fuerza la presencia de una sesión, con lo que nunca será nulo. ¡Cuidado! ya que el acceso no es thread-safe.
javax.servlet.http.PushBuilder	Push Builder (Servlet 4.0) para realizar el push de recursos para el protocolo HTTP/2.
java.security.Principal	Usuario actualmente autenticado.
HttpMethod	Método (verbo) HTTP de la petición.
java.util.Locale	Locale actual de la petición.
java.util.TimeZone + java.time.ZoneId	Zona horaria asociada a la petición.
java.io.InputStream, java.io.Reader	Permite acceder a la petición en crudo.
java.io.OutputStream, java.io.Writer	Permite producir la respuesta en crudo.
@PathVariable	Permite acceder a variables presentes en la URI.
@MatrixVariable	Acceso a los pares nombre-valor presentes en la URI.
@RequestParam	Acceso a los parámetros de la petición, incluidos ficheros multipartes.
@RequestHeader	Acceso a los encabezados de la petición.
@CookieValue	Acceso a las cookies.
@RequestBody	Acceso al cuerpo de la petición HTTP. El cuerpo es convertido según la implementación del HttpMessageConverter configurado.
@HttpEntity<B>	Acceso a los encabezados y cuerpo de la petición.
@RequestPart	Acceso a una parte de una petición multipart/form-data.
java.util.Map, org.springframework.ui.Model, org.springframework.ui.ModelMap	Acceso al modelo que es expuesto a las plantillas para el renderizado de vistas.
RedirectAttributes	Especifica atributos en caso de redirección.
@ModelAttribute	Para acceder a algún atributo existente en el modelo, con conexión de datos y validación aplicada.
Error, BindingResult	Para acceder a los errores de validación y la conexión de datos de un command object, o los errores de validación de un objeto @RequestBody.
SessionStatus + @SessionAttributes	Marca el procesamiento de un formulario completo, que activa la limpieza de atributos de sesión declarados a través de @SessionAttributes.
@RequestAttribute	Acceso a los atributos de la petición.
Aquellas anotacines que permitan el uso de atributo required, podrán ser utilizadas junto con java.util.Optional de Java 8.

Fuente: https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-ann-arguments

Tipos de retorno
Tipo de dato	Descripción
@ResponseBody	El valor se convierte según el HttpMessageConverter configurado.
HttpEntity<B>, ResponseEntity<B>	Se devuelve la respuesta completa, incluyendo encabezados y cuerpo.
HttpHeaders	Para devolver una respuesta con encabezados y cuerpo vacío.
String	Es el más usual en las últimas versiones de Spring. Se trata del nombre de la plantilla, que será resuelto por el ViewResolver configurado.
View	Una instancia de View que se usará para renderizar junto con el modelo.
java.util.Map, org.springframework.ui.Model	Atributos para ser añadidos al modelo.
@ModelAttribute	Atributo para ser añadido al modelo.
ModelAndView	Vista y modelo de forma conjunta.
void	Si devuelve void, se entiende que se ha manejado la respuesta a través de ServletResponse, OutputStream o una anotación @ResponseStatus.
Puede revisar la lista completa en la fuente.

Fuente: https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-ann-return-types




Cargar una vista vs. Redirigir a otro controlador
Como hemos visto, la forma más sencilla de que un controlador nos lleve a una vista es devolviendo el nombre de la plantilla a renderizar como un String:

@GetMapping("/")
public String welcome(Model model) {
    model.addAttribute("mensaje", "¡Hola a todos!");
    return "index";
}
Sin embargo, habrá ocasiones en las que nos interes que un controlador nos lleve directamente a otro. Un escenario típico es, tras haber procesado un formulario (por ejemplo, de inserción de un nuevo registro); posiblemente, después de procesar esa petición, queramos visualizar el listado completo de registros, y así comprobar que el nuevo registro ha sido insertado.

Para poder hacer una redirección, incluimos la palabra redirect: en el valor de retorno del método, seguido de la ruta del controlador al cual queremos redirigirnos.

@PostMapping("/empleado/new/submit")
public String nuevoEmpleadoSubmit(@ModelAttribute("empleadoForm") Empleado nuevoEmpleado) {
    servicio.add(nuevoEmpleado);
    return "redirect:/empleado/list";
}


@PathVariable y @RequestMapping
Podemos declarar variables en el path a nivel de método y a nivel de clase (haciendo uso de @RequestMapping):

@Controller
@RequestMapping("/owners/{ownerId}")
public class OwnerController {

    @GetMapping("/pets")
    public Pet findAll(@PathVariable Long ownerId) {
        // ...
    }

    @GetMapping("/pets/{petId}")
    public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
        // ...
    }
}
De esta forma, necesitaríamos inyectar la variable a través de @PathVariable en cada método.





