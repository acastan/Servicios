PREGUNTAS
---------

 01. ¿En qué consiste DHCP? ¿Qué puertos y protocolo en la capa de transporte utiliza?

 02. ¿Qué ventajas proporciona? ¿Por qué? ¿Qué desventajas proporciona? ¿Por qué?

 03. Dibuja el esquema de una red local donde hay un servidor de DHCP. ¿Qué debemos configurar en nuestra red para que el tráfico DHCP pase a través de los encaminadores o routers?
 
 04. ¿Qué es APIPA?

 05. ¿Viene algún software de servidor de DHCP con Windows Server? ¿Desde dónde se instala y desde dónde se administra?

 06. ¿Cuál es el software de servidor de DHCP más conocido para Unix/Linux?

 07. Al instalar un servidor de DHCP, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. Al instalar un servidor de DHCP, ¿Qué pruebas piensas que deberás hacer para comprobar el buen funcionamiento?

 09. ¿Cuáles son los pasos en la comunicación entre un cliente y un servidor de DHCP? ¿Cuáles son las IPs de los paquetes?

 10. ¿Qué pasa si accidentalmente hay dos servidores DHCP en una red? ¿Qué herramienta permite detectarlo?





DATOS DE LA PRÁCTICA LINUX Y WINDOWS
------------------------------------

El servidor DHCP, (que en el futuro también será servidor de DNS) deberá tener la IP fija 192.168.100.2, el nombre Asterix, y los servidores de DNS 192.168.100.2 y 8.8.8.8. Nuestra red se llama mired.org.

Los parámetros que el servidor de DHCP servirá son:

  - Rango de IPs: de la 192.168.100.31 a la 192.168.100.80
  
  - Máscara de red: 255.255.255.0

  - Dirección de broadcast: 192.168.100.255

  - Puerta de enlace: 192.168.100.1

  - Servidores de DNS: 192.168.100.2 y 8.8.8.8

  - Tiempo de alquiler: 1 hora

  - Reservas: la IP 192.168.100.150 ha de quedar reservada a un cliente que se llama Obelix cuya MAC es AA:BB:CC:DD:EE:FF.





PRÁCTICA WINDOWS
----------------

Instalaremos DHCP para Windows Server. Exploraremos la interfície gráfica de administración del servidor DHCP, configurando los parámetros básicos.

Probaremos el servidor (intentando que no interfiera con el servidor de DHCP de la escuela).





PRÁCTICA LINUX
--------------

Instalaremos DHCP para Linux. Exploraremos el fichero de configuración.

Probaremos el servidor (intentando que no interfiera con el servidor de DHCP del instituto).





PRÁCTICA LINUX ADICIONAL
------------------------

Sea _tu-ip_ un número que te repartirá el profesor. En nuestro caso será el último número de la IP de tu equipo.

 01. Instala un servidor DHCP con los siguientes requisitos:

     - El servidor DHCP tendrá tres tarjetas de red: una en modo NAT y dos en modo red interna, asignadas a redes internas diferentes, "red1" y "red2", respectivamente.

     - La tarjeta de red del servidor en "red1" tiene IP estática 192.168._tu-ip_.1

     - La tarjeta de red del servidor en "red2" tiene IP estática 192.168._tu-ip_+100.1

     - El servidor DHCP sólo estará asignado a las dos tarjetas en red interna.

     - En "red1" el servidor repartirá un pool de 10 direcciones, de 192.168._tu-ip_.201 a 192.168._tu-ip_.210

     - En "red2" el servidor repartirá las reservas: 192.168._tu-ip_+100.201 a la MAC aa:bb:cc:dd:ee:ff y 192.168._tu-ip_+100.202 a la MAC ee:ff:dd:cc:bb:aa

     - A las reservas, además, les proporcionará el nombre de host, "server" y "dns2", respectivamente.

     - A los clientes les proporcionará como mínimo la IP, la máscara (255.255.255.0), el servidor DNS (8.8.8.8), y el dominio (mired.org).

     Entrega el fichero de configuración del servidor DHCP.

 02. Pon un par de máquinas virtuals de prueba en "red1", y comprueba que reciban parámetros de red.

     Entrega capturas de pantalla donde aparezcan los parámetros de red que obtuvieron los equipos.

 03. Pon un par de máquinas virtuals de prueba en "red2", y comprueba que reciban la dirección reservada a su seva MAC. (-Modifica antes su MAC en la herramienta de virtualización para que se ajuste a la de la reserva-)

     Entrega capturas de pantalla donde aparezcan los parámetros de red que obtuvieron los equipos.

 04. ¿Por qué el cliente Windows con reserva no cambia su hostname?

     ¿Por qué el cliente Linux con reserva no cambia su hostname?

 05. Instala en el servidor el módulo de Webmin para administrar DHCP.

     Entrega capturas de pantalla de la página de configuración de DHCP de Webmin.

 06. Consigue que el servidor actúe como enrutador, encaminando los paquetes de "red1" y "red2" hacia a la tarjeta en modo NAT, permitiendo a los equipos de dichas redes accedan a Internet.

     Para ello deberás configurar dos cosas:

     a) Escribir un script de enrutamiento en el servidor (-un par de líneas de Iptables o Nftables-).

     b) El servidor DHCP también deberá dar puerta de salida (gateway) a los clientes. ¿Cuál será?

     Entrega el script de enrutamiento y la captura de pantalla de un cliente haciendo ping a un host de Internet.

     ¿Cómo consigues que el script de enrutamiento se ejecute automáticamente en el inicio de la máquina servidor?

 07. Con un cliente de red que ya haya obtenido parámetros, inicia el programa Wireshark y captura el tráfico de red de un segundo cliente tratando de obtener los parámetros DHCP.

     Entrega la captura de pantalla de los cuatro paquetes de la comunicación, donde se vean claramente puertos, direcciones IP, y tipo de mensaje DHCP.

 08. Pon este servidor DHCP en red interna con el otro servidor DHCP del ejercicio anterior.

     Añade un cliente a la red interna y detecta todos los servidores de DHCP con el programa Nmap.

     Entrega una captura de pantalla con el resultado de Nmap.





REFERENCIAS
-----------

  - <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>

  - <https://en.wikipedia.org/wiki/DHCPv6>
  
  - <https://en.wikipedia.org/wiki/Comparison_of_DHCP_server_software>

  - <https://www.packetorbit.net/posts/categories/dhcp-security>
