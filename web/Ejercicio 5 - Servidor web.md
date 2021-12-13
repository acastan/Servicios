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





PRÁCTICA LINUX BÁSICA
---------------------

Instala Apache. Pruébalo navegando des de un cliente sobre una página web. Explora los ficheros de configuración.

 01. En una máquina virtual Linux instala el servidor web apache2. Entrega captura de pantalla de la instalación.

 02. Crea una sencilla página web con tu nombre y apellidos en este equipo, en la carpeta donde el servidor web guarda por defecto las páginas web. Entrega captura de pantalla de la carpeta donde dejas tu página web.

 03. Entrega captura de pantalla del navegador de la máquina anfitrión accediendo a la página web vía el servidor web de la máquina virtual.

 04. Accede al directorio de configuración de Apache y explica qué función tienen los diferentes archivos y carpetas que allá se encuentran.





PRÁCTICA LINUX: HOSTS VIRTUALES
-------------------------------

Configura el servidor para que sirva páginas de dos nombres de dominio diferentes mediante hosts virtuales, por ejemplo www.mired.org e intranet.mired.org.

 01. En la máquina virtual donde has instalado Apache, crea dentro de /var/www/html dos carpetas: "sitio1" y "sitio2", cada una con un fichero "index.html" que contendrá una página diferente, por ejemplo "Bienvenido a sitio1 de _nombre apellidos_" la primera página, y "Bienvenido a sitio2 de _nombre apellidos_" la segunda página.

     Entrega captura de pantalla de las carpetas creadas con los ficheros dentro.

 02. En la carpeta "sites-available" de Apache crea dos ficheros, "sitio1.conf" y "sitio2.conf" que contendrán la configuración de los respectivas webs. Para la configuración puedes usar esta plantilla:

         <VirtualHost *:80>
           ServerName sitio
           DocumentRoot /ruta_a_carpeta
         </VirtualHost>

     Entrega captura de pantalla de la configuración que has escrito en estos ficheros.

 03. Habilita las dos webs ¿Con qué comando se activa una web en Apache?

     Entrega captura de pantalla del listado del directorio "sites-enabled" de Apache.

 04. Haz los canvios necesarios en tu servidor DNS para que los nombres de host "www.mired.org" i "intranet.mired.org" apunten a la IP del servidor DNS, que también es el servidor web.

     Entrega captura de pantalla del fichero de configuración del servidor DNS.

     ( En caso de no tener servidor de DNS, puedes hacer un "apaño" con el fichero "[hosts](https://en.wikipedia.org/wiki/Hosts_(file))" del cliente )

     Entrega captura de pantalla del navegador accediendo a las páginas "www.mired.org" e "intranet.mired.org".





PRÁCTICA LINUX: HTTPS
---------------------

Genera un certificado digital e intégralo en el servidor web para que lo utilice en HTTPS con un sitio web.

 01. Habilita el módulo de HTTPS para Apache.

     ¿Con qué comando habilitas el módulo "ssl"?

     ¿Con qué comando puedes reiniciar apache?

     ¿Cón qué comando puedes recargar la configuración de Apache sin tener que reiniciarlo?

     ¿Con qué comando compruebas que ahora Apache escucha por el puerto 443?

 02. Genera un certificado. Para que tu servidor "intranet.mired.org" pueda servir páginas seguras con el protocolo HTTPS, necesita un certificado. Dicho certificado permitirá que tu servidor utilice cifrado para iniciar una trasmisión segura de información. El cliente deberá aceptar el certificado directamente del servidor, ya que generaremos un certificado "autofirmado". Si queremos evitarlo, deberíamos comprar un certificado a una entidad certificadora confiable, pero tiene un precio que no merece la pena pagar en un entorno educativo. (Si quieres aprender un poco más visita la página <http://httpd.apache.org/docs/current/ssl/>) 

     ¿Cómo utilizas los comandos `make-ssl-cert` y/o `openssl` para crear un certificado?

     ¿En qué directorio guardas el fichero con el certificado?

 03. Configura tu página para que utilice dicho certificado.

     ¿Qué líneas debes añadir a esta nueva configuración de la intranet para que utilice el certificado?

         <VirtualHost *:443>
           ServerName intranet.mired.org
           DocumentRoot /var/www/html/sitio2
           ...
         </VirtualHost>

     Aviso: algunas directivas (`SSLCertificateFile`, `SSLCertificateKeyFile`, `SSLCertificateChainFile`, ...) serán necesarias o no dependiendo del tipo de certificado que hayas generado.

     Entrega captura de pantalla del fichero de configuración de la intranet.

     Entrega capturas de pantalla de un cliente (a) aceptando el certificado, y (b) navegando por dicha pàgina.

 04. Intenta que http://intranet.mired.org/ redirija a https://intranet.mired.org/





PRÁCTICA LINUX: SERVIDOR WEB DINÁMICO
-------------------------------------

Instala PHP y MySQL. Integra Apache y PHP, para que el servidor pueda ejecutar páginas dinámicas PHP. Pruébalo instalando y administrando gestores de contenido.

 01. Instala PHP. Integra Apache y PHP, para que el servidor pueda ejecutar páginas dinámicas PHP.

     Pruébalo con esta página llamada index.php en uno de los sitios web que ya tienes:

         <?php
            phpinfo();
         ?>

     Entrega comandos, pantallas de configuración, y pantalla de prueba de phpinfo.

 02. Instala MySQL/MariaDB. Configura los parámetros de seguridad de acceso: usuarios que pueden acceder / acceder des de red o no / IPs que pueden acceder.

     Prueba a instalar [PHPMyAdmin](https://www.phpmyadmin.net/), o [Adminer](https://www.adminer.org/), o [DBeaver](https://dbeaver.io/), y entonces acceder a la gestión de las bases de datos desde un navegador.

     Entrega comandos, pantallas de configuración, y pantalla de prueba de PHPMyAdmin/Adminer/DBeaver.
  
 03. Prueba el servidor web dinámico instalando algunos gestores de contenido: Wordpres, Drupal, Joomla, MediaWiki, Moodle, Alfresco, Prestashop, SeaFile, NextCloud, GitLab, Mantis-bt, Glpi, RackTables, OpenStack, etc.

     Entrega todos los pasos para la instalación y configuración del gestor de contenido.





PRÁCTICA LINUX: TU SERVIDOR WEB EN INTERNET
-------------------------------------------

Vas tener tu propio servidor web en Internet, donde moverás todo lo hecho hasta ahora.

 01. Inicia una instancia de Linux en [Oracle Academy Cloud](https://academy.oracle.com/) o [AWS Academy](https://aws.amazon.com/training/awsacademy/).

 02. Instala en dicha instancia lo practicado hasta ahora: servidor web que pueda servir contenidos dinámicos, gestor de contenido, https.
 
 03. Abre puertos en los dos cortafuegos para poder probar tu web des de el exterior: el cortafuegos de red y el cortafuegos del host.

 04. Crea tu página web.
  
 05. En [Freenom](https://www.freenom.com/) reserva un nombre de dominio gratuito (.tk, .ga, etc.) para tu web.
 
 06. Haz que el registro DNS Freenom para tu dominio apunte al servidor DNS de Oracle Cloud o Amazon AWS, y configura el servidor DNS de Oracle Cloud o Amazon AWS para que el registro www apunte a la IP de tu host.

 07. Crea e instala para tu web un certificado digital gratuito de [Let's Encrypt](https://letsencrypt.org/). Dichos certificados sólo demuestran que administras el dominio, y expiran a los tres meses. Lo ideal sería que utilizaras [certbot](https://certbot.eff.org/) para [renovar dicho certificado automáticamente](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-20-04-es). Si en lugar de utilizar certbot prefieres hacerlo [a mano](https://punchsalad.com/ssl-certificate-generator/) será tedioso repetir el proceso cada tres meses.

Entrega la URL de tu web, así como todos los pasos para la instalación y configuración.





PRÁCTICA LINUX EXTRA: CONVIÉRTETE EN UN PROVEEDOR DE ESPACIO WEB
----------------------------------------------------------------

Si has realizado los pasos del 1 al 3 de la práctica anterior, ahora instala un [panel administrativo](https://en.wikipedia.org/wiki/Comparison_of_web_hosting_control_panels) (ISPConfig, Virtualmin, GNUPanel, etc.) que permita vía navegador:

  * a ti, crear usuarios y nuevos dominios web.
  
  * a los usuarios, gestionar su hosting web, subir archivos.

Entrega los pasos para la instalación y configuración, y capturas de  pantalla de la administración del panel.





PRÁCTICA LINUX: SEGURIDAD
-------------------------

Realiza un estudio de las directivas y módulos de Apache que ayudan a fortalecer la seguridad en el servidor web.

  - <https://www.tecmint.com/apache-security-tips/>

  - <https://www.apachecon.eu/>

  - <https://geekflare.com/apache-web-server-hardening-security/>

  - <https://wiki.debian.org/Apache/Hardening>





PRÁCTICAS LINUX EXTRA
---------------------

 01. (Extra) Instala en el servidor el módulo de Webmin para administrar Apache.

 02. (Extra) Modifica Apache para que un sitio web trabaje con el protocolo HTTP/2 en lugar de HTTP/1.1 , utilizando el módulo http2.

 03. (Extra) Modifica Apache para que automáticamente cada usuario del sistema tenga una página web personal en su "home", utilizando el módulo userdir.

 04. (Extra) Elimina o cambia la información de versión de Apache.

     <https://tecadmin.net/hide-apache-version-from-http-header/>

 05. (Extra) Cambia la página de error 404 que viene por defecto. Por ejemplo: <http://www.lego.com/jjj>

     <https://httpd.apache.org/docs/current/custom-error.html>

 06. (Extra) Redirige al usuario que visita tu página a otra url. Por ejemplo, que al acceder a http://localhost/vete vaya a https://www.gnu.org/

     <https://httpd.apache.org/docs/current/urlmapping.html#redirect>

 07. (Extra) Configura el servidor web para que no liste el contenido de un determinado directorio. Crea antes un par de ficheros en dicho directorio.

     <https://wiki.apache.org/httpd/DirectoryListings>

 08. (Extra) Configura el servidor web para que al entrar a un directorio concreto pida autorización de usuario y contraseña. ¿Viaja la autorización encriptada?

     <https://httpd.apache.org/docs/current/howto/auth.html>

 09. (Extra) Crea una carpeta fuera del directorio raíz de Apache i "mapeala" a la URL http://localhost/carpetaExterna/

     <https://httpd.apache.org/docs/current/urlmapping.html#outside>

 10. (Extra) ¿Qué es "leeching" o "hot linking", y cómo puede perjudicar a tu servidor? Añade las directivas oportunas a tu fichero de configuración para que si alguien enlaza a tus imágenes des de una página externa, tu servidor muestre una imagen alternativa.

     <https://httpd.apache.org/docs/current/rewrite/access.html#blocked-inline-images>





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Web_servers>

  - <http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol>

  - <http://en.wikipedia.org/wiki/Media_type>

  - <https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP>

  - <http://news.netcraft.com/archives/web_server_survey.html>

  - <http://en.wikipedia.org/wiki/Comparison_of_web_server_software>

  - <https://jvns.ca/blog/2017/01/31/whats-tls/>

  - <http://www.xtec.net/~acastan/textos/Tuning%20LAMP.pdf>

  - <https://blog.avast.com/create-a-secure-web-server-avast>

  - <https://mythemeshop.com/blog/web-server-security/>
