PREGUNTAS
---------

 01. ¿En qué consiste un proxy-caché? ¿Sirve para todas las páginas? ¿En qué consiste un proxy-caché transparente?

 02. ¿Qué ventajas proporciona? ¿Por qué? ¿Qué desventajas proporciona? ¿Por qué?

 03. Dibuja el esquema de una red local donde se utiliza un proxy-caché.

 04. ¿En qué consiste un proxy-caché inverso? Dibuja el esquema de una granja de servidores web donde se utiliza un proxy-caché inverso.

 05. ¿Viene algún software de proxy-caché con Windows Server? ¿Cuál es el software de proxy-caché más conocido para Windows? 

 06. ¿Cuál es el software de proxy-caché más conocido para Linux?

 07. Al instalar un servicio de proxy-caché, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. ¿Crees que un proxy-caché funciona de la misma manera en las peticiones HTTP que en las HTTPS?

 09. En la red local de nuestro centro la mayor parte del ancho de banda se la comen las actualizaciones de Windows, de antivirus, de Linux. Estudia diferentes métodos que podemos utilizar para cachear dichas actualizaciones y así liberar el ancho de banda. Pistas:

     - Microsoft Windows Server Update Services.

     - Mirror o caché de paquetes Debian: apt-mirror, approx, apt-cacher-ng
     
     - Proxy-caché para antivirus

     - Proxy-caché para navegación





DATOS DE LA PRÁCTICA LINUX Y WINDOWS
------------------------------------

Los parámetros que configuraremos en el servidor proxy-caché son:

  - 1Gb de tamaño de caché.

  - Permitir el acceso a algunos ordenadores de nuestra red y denegaremos el resto.

  - Filtrar las páginas del sitio web http://www.facebook.com/ , y los ficheros mp3.

  - Tiempo de caducidad del contenido: 1 mes.





PRÁCTICA WINDOWS
----------------

  - Instalaremos algun software de proxy-cache para Windows. Exploraremos la interfície gráfica de administración del servicio, configurando los parámetros básicos.

  - Probaremos el servidor.





PRÁCTICA LINUX SQUID HTTP
-------------------------

 01. Instala el servidor proxy-caché *Squid* y configura el puerto, el tamaño de la caché, y el identificador que aparecerá en las páginas web de bloqueo

     Entrega capturas de pantalla o los comandos utilizados

 02. Crea las listas de acceso para localhost, para los ordenadores de tu red, y para el resto.

     Permite acceso a los ordenadores de tu red y localhost, y deniega acceso al resto

     Entrega capturas de pantalla o los comandos utilizados

     > ¡AVISO IMPORTANTE! Las reglas `http_access` se intentan aplicar por orden de escritura, una a una, hasta encontrar a la primera que encaja con la lista de control de acceso del ordenador que intenta acceder. Si hubiéramos escrito en primera posición `http_access deny all` ningún ordenador hubiera podido acceder, ya que todos encajan en esta lista de control de acceso. Será fundamental en los siguientes apartados que penséis bien en qué posición colocareis la regla, o no funcionará como deseas.

 03. Prueba el servicio desde un cliente. Para ello configura su navegador para que navegue a través de la IP del proxy y del puerto 3128.

     - Si el servicio no funcionara, ¿Con qué comandos probarías si ha arrancado?

     - Si el servicio ha arrancado, ¿Con que comandos consultarías sus logs de acceso?

 04. ¿Qué debes cambiar para denegar el acceso a los ordenadores de tu red, y tan solo permitir el acceso a algunos pocos (-como por ejemplo, al 192.168.100.150-)?

 05. ¿Cómo boquearías el acceso a Facebook?

 06. ¿Cómo bloquearías el acceso a ficheros mp3?

 07. ¿Cómo harás para indicar al proxy que las páginas del dominio mired.org no las guarde en la caché?

 08. Instala *Webmin* y utilízalo para configurar gráficamente *Squid* desde un navegador





PRÁCTICA LINUX SQUID HTTPS
--------------------------

Configura Squid para que actue correctamente de proxy-caché en sitios HTTPS.

<https://www.howtoforge.com/filtering-https-traffic-with-squid>





PRÁCTICA IPFIRE
---------------

En la máquina que hace de router con *IPFire*, activa y configura el módulo de proxy-caché

<https://wiki.ipfire.org/configuration/network/proxy/wui_conf>





PRÁCTICA CACHE DE PAQUETES .DEB
-------------------------------

Instala y configura en tu servidor una caché de paquetes con *apt-cacher-ng*, y configura un cliente con *Debian* o *Ubuntu* para que se actualice a través de él

<https://blog.ichasco.com/apt-cache-ng-repositorio-local-cacheado/>





PRÁCTICA SALTAR FILTRADO DE UN PROXY
------------------------------------

Hemos protegido una red de una organización con un proxy para evitar el acceso web a páginas de piratería y hacking. Dicha red también filtra Tor y el acceso a proxys públicos. Pero una persona de dicha organización un día necesita acceder a unas páginas filtradas de serguridad informática, aprovechando que dispone de servidores en Internet (por ejemplo, Oracle Cloud y Amazon AWS).

Implementa cómo dicha persona puede pasar las restricciones de nuestro proxy mediante un tunel SSH.





PREGUNTAS ACLs SQUID
--------------------

Sabiendo que Squid cuenta, entre otros, con los siguientes elementos de ACL:

 * src: source (client) IP addresses
 * dst: destination (server) IP addresses
 * dstdomain: destination (server) domain name
 * url_regex: URL regular expression pattern matching
 * time: time of day, and day of week

Sabiendo también que:

 * Varias ACL en una regla es la intersección ("y") de todas ellas.
 * Las reglas se evalúan por orden hasta que una de ellas se aplica.

Explica las siguientes configuraciones:

01. ¿Quién podrá acceder a la web?

        acl network172 src 172.16.5.0/24
        http_access allow network172
        http_access deny all

02. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl Cooking1 url_regex cooking
        acl Recipe1 url_regex recipe
        acl myclients src 172.16.5.0/24
        http_access deny Cooking1
        http_access deny Recipe1
        http_access allow myclients
        http_access deny all

03. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl Cooking2 dstdomain www.gourmet-chef.com
        http_access deny Cooking2
        http_access allow all

04. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl ME src 10.0.0.1
        acl YOU src 10.0.0.2
        http_access allow ME YOU
        http_access deny all

05. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl US src 10.0.0.1 10.0.0.2
        http_access allow !US
        http_access deny all

06. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl GOOD dst 10.0.0.1
        http_access allow GOOD
        http_access deny all

07. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl US src 10.0.0.1 10.0.0.2
        acl GOOD dst 10.0.0.1
        http_access allow GOOD US
        http_access deny all

08. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl PornSites url_regex "/usr/local/squid/etc/pornlist"
        http_access deny !PornSites
        http_access allow all

09. ¿Qué está permitido y qué está denegado en la siguiente configuración?

        acl USER1 src 192.168.100.0/24
        acl USER2 src 192.168.200.0/24 192.168.201.0/24
        acl DAY time 06:00-18:00
        http_access allow USER1 DAY
        http_access deny USER1
        http_access allow USER2 !DAY
        http_access deny USER2





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Proxy_server>

  - <http://en.wikipedia.org/wiki/Web_cache>

  - <http://en.wikipedia.org/wiki/Reverse_proxy>

  - [Directivas de configuración de Squid](http://www.squid-cache.org/Doc/config/)

  - [Access Control List en Squid](http://wiki.squid-cache.org/SquidFaq/SquidAcl)

  - [Configuraciones de ejemplo de Squid](http://www.nexolinux.com/proxy-squid-control-de-accesos-acl-ii-2/)

