EJERCICIOS DE TCP/IP
--------------------

Instalad el analizador de protocolos Wireshark (también llamado “sniffer”) que encontraréis en la página web <http://www.wireshark.org/> o en el repositorio de paquetes de vuestra distribución Linux.

Para cada ejercicio, en la configuración de Wireshark seleccionad la tarjeta de red con la que capturaremos los paquetes, y deseleccionad el trabajo en modo promiscuo, ya que sólo queremos calcular nuestros paquetes de información que circulan por la red y no los de nuestros compañeros. Para cada ejercicio seleccionad también un filtro adecuado para capturar sólo el determinado tipo de paquetes que nos interesen.

Cada ejercicio debe mostrar una captura de pantalla con los paquetes capturados, así como una línea de texto explicando el filtro utilizado para capturar sólo los paquetes que nos interesaban.

Cuando comencemos a capturar paquetes se abrirá un pequeño cuadro con información  indicando qué porcentaje de paquetes de cada tipo llevamos capturados. Al acabar de capturar paquetes, tendremos acceso a la ventana principal del programa, donde aparecen uno a uno todos los paquetes de información capturados, y los podemos analizar individualmente.



 01. **Comunicación TCP**

     Analizaremos una petición de página web a un servidor. Repasad rápidamente los pasos necesarios para establecer, mantener y finalizar una comunicación TCP. A continuación abrid un navegador. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. Solicitad en la barra de direcciones del navegador una página web que contenga poca información, como www.google.es. Finalizad la captura.

     ¿Qué paquetes corresponden al establecimiento de la comunicación? ¿Cuáles a la finalización? ¿Cuáles a la sincronización?

     ¿A qué puerto van dirigidos los paquetes? ¿De qué puerto salen?

     ¿Qué paquete contiene la solicitud de la página web? ¿Qué información contienen los otros paquetes?



 02. **Comunicación UDP**

     Analizaremos la navegación por el entorno de red de Windows. Repasad rápidamente los pasos necesarios para establecer, mantener y finalizar una comunicación UDP. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado.  A continuación abrid el entorno de red y comenzad a explorar algunas máquinas que se encuentran en vuestro grupo de trabajo, en busca de carpetas compartidas. Finalizad la captura.

     ¿Qué paquetes corresponden al establecimiento de la comunicación? ¿Cuáles a la finalización? ¿Cuáles a la sincronización?

     ¿A qué puerto van dirigidos los paquetes?

     ¿En cuántos paquetes cabe la información que se envía? ¿En cuántos paquetes cabe la información que se recibe?



 03. **DNS**

     Analizaremos una solicitud DNS. Repasad rápidamente en que consiste dicho protocolo. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. A continuación abrid una consola y ejecutad el comando `nslookup www.w3.org`. Finalizad la captura.

     ¿Qué protocolo se ha utilizado para realizar la petición: UDP, TCP o ICMP?

     ¿A qué puerto iba dirigida la petición?

     ¿Qué información circulaba en los paquetes?



 04. **Ping**

     Analizaremos una solicitud de respuesta (“ping”). Repasad rápidamente en que consisten dichas solicitudes. A continuación abrid una consola. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. Escribid en la consola `ping www.google.es -n 1`. Finalizad la captura.

     ¿Qué protocolo se ha utilizado para realizar la petición: UDP, TCP o ICMP?

     ¿Qué información circulaba en los paquetes?

     ¿Qué pasaría si realizarais un ping a la dirección de broadcast (192.168.0.255 o la que sea)?

     ¿Cuál es el tiempo de vida de los paquetes?



 05. **Traceroute**

     Analizaremos una petición de trazado de ruta (“traceroute”). Repasad rápidamente en que consisten dichas solicitudes. A continuación abrid una consola. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. Escribid en la consola `tracert -d www.google.es`. Finalizad la captura.

     ¿Qué protocolo utilizaban los paquetes de ida: UDP, TCP o ICMP? ¿Qué protocolo utilizaban los paquetes de respuesta: UDP, TCP o ICMP?

     ¿A quién iban dirigidos los paquetes?

     ¿Cual era el tiempo de vida de cada paquetes?



 06. **ARP**

     Analizaremos una solicitud ARP. Repasad rápidamente en que consiste dicho protocolo. A continuación abrid una consola y ejecutad el comando `ip neigh` o bién `arp -n` para ver la tabla de vuestro ordenador que memoriza direcciones de red asociadas a direcciones IP. Borrad dicha tabla con el comando `sudo ip neigh flush ip_a_borrar` o bién `sudo arp -d ip_a_borrar`. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. Escribid en la consola `ping 192.168.0.1`. Finalizad la captura.

     ¿A qué dirección MAC se ha dirigido la petición ARP?

     ¿Quién ha respondido?



 07. **Análisis de puertos**

     Utilizando el analizador de puertos que descargamos el día anterior en clase (¿superscan, portscan, nmap?) veremos las huellas que un análisis de puertos deja en nuestro sniffer. Comenzad a capturar paquetes con Wireshark, utilizando el filtro adecuado. Pedid a los compañeros del ordenador más cercano que realicen un escaneo de los 20 primeros puertos de vuestro ordenador. Cuando hayan acabado finalizad la captura de paquetes. Después iniciad el programa analizador de puertos para realizar el correspondiente escaneo sobre vuestros vecinos.

     ¿Cómo reconocerías este tipo de escaneo (se llama escaneo “vertical”)?

     ¿Cómo reconocerías un escaneo “horizontal” en una red?

     ¿Cómo pueden saber mediante un escaneo qué puertos están abiertos y cuales cerrados? 

     ¿Qué otros tipos de análisis conoces?





REFERENCIAS
-----------

  - Apuntes:

    <http://es.wikipedia.org/wiki/TCP/IP>

    <http://en.wikipedia.org/wiki/TCP/IP>

    <https://dougvitale.wordpress.com/2011/12/21/deprecated-linux-networking-commands-and-their-replacements/>

  - Documental "Warriors of the net":

    <http://www.warriorsofthe.net/movie.html>

  - Historieta "How DNS works":

    <https://howdns.works/>

  - Sniffer o Analizador de protocolos: Wireshark (Linux y Windows)

    <https://www.wireshark.org/>

  - Scanneador de puertos: nmap (Linux) / superscan (Windows)

    <https://nmap.org/>

  - Ver connexiones activas: ss (Linux) / tcpview (Windows)

    <https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview>

  - Constructor de paquetes: packeth (Linux)

    <http://packeth.sourceforge.net/packeth/>

  - Otros: traceroute (Linux) / visualroute (Windows)

    <http://www.visualroute.com/>
