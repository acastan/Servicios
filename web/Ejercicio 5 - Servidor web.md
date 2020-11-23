PREGUNTAS
---------

 01. ¿En qué consiste HTTP? ¿y HTTPS? ¿Qué puertos y protocolo en la capa de transporte utilizan?

 02. Dibuja el esquema de una red donde hay un servidor de HTTP sirviendo páginas a los ordenadores de la intranet. Dicho servidor HTTP se comunica con un servidor SQL de bases de datos para resolver páginas dinámicas ASP o PHP.

 03. ¿Cuál és la sintaxis de la instrucción GET del protocolo HTTP? ¿Qué otras instrucciones existen en dicho protocolo?

 04. En la petición de una página web mediante el protocolo HTTP, ¿qué tipos de respuestas son las indicadas por los códigos 1xx, 2xx, 3xx, 4xx y 5xx?

 05. En el protocolo HTTP ¿Cuáles son los cinco campos que te parecen más importantes en los "headers" de la petición de una página web y de la respuesta?

 06. Viene algún software de servidor de HTTP con Windows Server? ¿Desde dónde se instala y desde dónde se administra? ¿Y para Windows no server?

 07. ¿Cuál es el software de servidor de HTTP más conocido para Unix/Linux? ¿Y el software de servidor más ligero de HTTP?

 08. Al instalar un servidor de HTTP, ¿Qué parámetros a configurar piensas que serán los más importantes?

 09. De qué maneras un servidor web puede servir páginas de más de un nombre de dominio ("virtual hosting"). Es decir, si necesitamos que un servidor web aloje las páginas de www.pepe.com y www.jose.com, ¿Cómo podemos conseguir qué distinga cuál le están pidiendo?
 
 10. ¿Cuál es la sintaxis completa de una URL?





EJERCICIO DE INVESTIGACIÓN: ESCALABILIDAD DE GRANDES SITIOS WEB
---------------------------------------------------------------

  * Extensión de trabajo: 1 ó 2 páginas
  * Tiempo del trabajo: 4 horas
  * Tiempo de la presentación: 10 minutos

Deberéis escoger uno de los sitios web de la lista del final o proponer al profesor un sitio nuevo. Del sitio escogido debéis encontrar la siguiente información para posteriormente presentarla a la clase (es obligatorio citar la referencia de la información encontrada).

  1. Presentar el sitio: a qué se dedica, qué información almacena, cómo nació y pequeña historia.

  2. Presentar estadísticas: número de visitas diarias y visitas simultáneas (media y picos), cantidad de información almacenada, número de usuarios actualmente.

  3. Presentar que software utiliza: sistema operativo, servicios, y lenguages de programación en páginas dinámicas.

  4. Presentar qué hardware utiliza actualmente: hardware de los equipos, número de equipos, centros de datos.

  5. Presentar la historia del crecimiento sitio: con cuántos equipos comenzó y cómo ha ido creciendo.

La lista de algunos sitios:

  * [wikipedia](https://www.wikipedia.org/)
  * [youtube](https://www.youtube.com/)
  * [google](https://www.google.com/)
  * [facebook](https://www.facebook.com/)
  * [twitter](https://www.twitter.com/)
  * [ebay](https://www.ebay.com/)
  * [paypal](https://www.paypal.com/)
  * [amazon](https://www.amazon.com/)
  * [flickr](https://www.flickr.com/)
  * [instagram](https://www.instagram.com/)
  * [pinterest](https://www.pinterest.com/)
  * [tumblr](https://www.tumblr.com/)
  * [slashdot](https://www.slashdot.org/)
  * [meneame](https://www.meneame.net/)
  * [diggit](https://www.digg.com/)
  * [sourceforge](https://www.sourceforge.net/)
  * [github](https://www.github.com/)
  * [netflix](https://www.netflix.com/)
  * [uber](https://www.uber.com/)

Podéis encontrar información buscando en:

  * <http://highscalability.com/blog/category/example>
  * <http://www.google.es/search?q=%22nombresitio+architecture%22>
  * <http://www.google.es/search?q=%22nombresitio+statistics%22>
  * Y también en la web del sitio escogido





PRÁCTICA WINDOWS
----------------

  - Instalaremos Internet Information Server para Windows Server. Exploraremos la interfície gráfica de administración del servidor web, configurando los parámetros básicos.

  - Configuraremos el servidor para que sirva páginas de dos nombres de dominio diferentes mediante tres métodos: puerto, ip, y nombre de host.

  - Generaremos un certificado digital y lo integraremos en el servidor web para que lo utilice en HTTPS.





PRÁCTICA LINUX
--------------

 01. Instala Apache. Pruébalo navegando des de un cliente sobre una página web. Explora los ficheros de configuración.

 02. Configura el servidor para que sirva páginas de dos nombres de dominio diferentes mediante hosts virtuales.

 03. Genera un certificado digital e intégralo en el servidor web para que lo utilice en HTTPS con un sitio web.
  
 04. Instala PHP y MySQL. Integra Apache y PHP, para que el servidor pueda ejecutar páginas dinámicas php.
  
 05. Prueba el servidor web dinàmico instalando algunos gestores de contenido: Wordpres, Drupal, Joomla, MediaWiki, PHPMyAdmin, etc.

 06. Instala en el servidor el módulo de Webmin para administrar Apache.
 
 07. (Extra) Elimina o cambia la información de versión de Apache.

     <https://tecadmin.net/hide-apache-version-from-http-header/>

 08. (Extra) Cambia la página de error 404 que viene por defecto. Por ejemplo: <http://www.lego.com/jjj>

     <https://httpd.apache.org/docs/current/custom-error.html>

 09. (Extra) Redirige al usuario que visita tu página a otra url. Por ejemplo, que al acceder a http://localhost/vete vaya a https://www.gnu.org/

     <https://httpd.apache.org/docs/current/urlmapping.html#redirect>

 10. (Extra) Configura el servidor web para que no liste el contenido de un determinado directorio. Crea antes un par de ficheros en dicho directorio.

     <https://wiki.apache.org/httpd/DirectoryListings>

 11. (Extra) Configura el servidor web para que al entrar a un directorio concreto pida autorización de usuario y contraseña. ¿Viaja la autorización encriptada?

     <https://httpd.apache.org/docs/current/howto/auth.html>

 12. (Extra) Crea una carpeta fuera del directorio raíz de Apache i "mapeala" a la URL http://localhost/carpetaExterna/

     <https://httpd.apache.org/docs/current/urlmapping.html#outside>

 13. (Extra) ¿Qué es "leeching" o "hot linking", y cómo puede perjudicar a tu servidor? Añade las directivas oportunas a tu fichero de configuración para que si alguien enlaza a tus imágenes des de una página externa, tu servidor muestre una imagen alternativa.

     <https://httpd.apache.org/docs/current/rewrite/access.html#blocked-inline-images>






REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Web_servers>

  - <http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol>

  - <http://en.wikipedia.org/wiki/Media_type>

  - <https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types>

  - <http://news.netcraft.com/archives/web_server_survey.html>

  - <http://en.wikipedia.org/wiki/Comparison_of_web_server_software>

  - <http://en.wikipedia.org/wiki/Comparison_of_lightweight_web_servers>
  
  - <https://jvns.ca/blog/2017/01/31/whats-tls/>

