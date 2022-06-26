PREGUNTAS
---------

 01. ¿En qué consiste un Proxy? ¿y SOCKS? ¿y PAT? ¿y el redireccionamiento de puertos?

 02. ¿Qué ventajas proporciona un proxy? ¿Por qué? ¿Qué desventajas proporciona? ¿Por qué?

 03. Dibuja el esquema de una red local donde se comparte la conexión a Internet a través de un Proxy.

 04. ¿Viene algún software de proxy con Windows Server? ¿Cuál es el software comercial de Proxy más conocido para Windows? ¿Qué funcionalidades trae?

 05. ¿Viene alguna manera de compartir la conexión a Internet de un equipo con Windows Server? ¿Desde dónde se instala y desde dónde se administra? 

 06. ¿Cuál es la manera de compartir la conexión a Internet en Unix/Linux?

 07. Al instalar un servicio de proxy, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. Una red está protegida para evitar el acceso web a páginas de piratería, pornografía, ... Comenta como funcionaría cada uno de estos métodos para sobrepasar dicha protección:

     a) Algún proxy anónimo (encontraréis muchos en <http://proxy.org/> y <http://www.allproxysites.com/>).

     b) Algún traductor de páginas web (
        [Google Translator](http://translate.google.com/) ,
        [Bing Translator](https://www.bing.com/translator) ,
        [InterTran](http://www.tranexp.com/win/itserver.htm) , ...).

     c) Navegador+Tor (por ejemplo [Tor Browser](https://www.torproject.org/)).





DATOS DE LA PRÁCTICA LINUX Y WINDOWS
------------------------------------

El ordenador o máquina virtual que haga de router deberá tener dos tarjetas de red. 

  - Una tarjeta conectada a la red interna y con la IP fija 192.168.100.1, que es precisamente la dirección de gateway especificada en los otros ordenadores de la red.

  - Otra tarjeta conectada a la red externa o internet.





PRÁCTICA WINDOWS
----------------

Instalaremos algun software de proxy para Windows (por ejemplo <http://www.analogx.com/contents/download/network/proxy.htm>). Exploraremos la interfície gráfica de administración del servicio, configurando los parámetros básicos.

Probaremos el servidor.





PRÁCTICA LINUX
--------------

Configuraremos iptables para que haga routing mediante alguna interfície gráfica (firestarter, fwbuilder, ...). Exploraremos el fichero de configuración.

Probaremos el servidor.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Proxy_server>

  - <http://en.wikipedia.org/wiki/SOCKS>

  - <http://en.wikipedia.org/wiki/Network_address_translation>

  - <http://en.wikipedia.org/wiki/Port_address_translation>

  - <http://en.wikipedia.org/wiki/Port_forwarding>
