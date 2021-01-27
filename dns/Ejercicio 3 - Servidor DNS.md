PREGUNTAS
---------

 01. ¿En qué consiste DNS? ¿Qué puertos y protocolo en la capa de transporte utiliza?

 02. ¿Qué es un servidor DNS primario? ¿Qué es un servidor DNS esclavo? ¿Qué es un servidor DNS caché?

 03. En una pequeña red local ¿Cómo resuelve el servidor de DNS el nombre de una máquina externa a la red? ¿Cómo resuelve el servidor de DNS el nombre de una máquina interna de la red?

 04. ¿Viene algún software de servidor de DNS con Windows Server? ¿Desde dónde se instala y desde dónde se administra?

 05. ¿Cuál es el software de servidor de DNS más conocido para Unix/Linux?

 06. ¿Qué son los registros A, AAAA, CNAME, NS, MX, PTR y SOA?
 
 07. Al instalar un servidor de DNS en una red local, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. Al instalar un servidor de DNS en una red local, ¿Qué pruebas piensas que deberás hacer para comprobar el buen funcionamiento?

 09. ¿De qué tres maneras se puede integrar el servicio de DHCP con el de DNS para conseguir que el servidor de DNS resuelva nombres de máquinas cuya IP fue dada por un servidor de DHCP?

 10. ¿Para qué sirve el fichero hosts? ¿Cómo se vacía la caché de DNS del cliente en Windows, MacOS X y Linux?





DATOS DE LA PRÁCTICA LINUX Y WINDOWS
------------------------------------

Nuestro servidor de DNS será un servidor primario para búsquedas directas.

Nuestra red se llama mired.org.

Los nombres que el servidor de DNS servirá son:

  - obelix (cliente con reserva DHCP): IP 192.168.100.150

  - asterix (servidor): IP 192.168.100.2

  - panoramix (router): IP 192.168.100.1

El servidor de correo será asterix, que también se llamará www, ftp y mail.

El servidor de nombres será asterix, que también se llamará dns.

Una vez realizado el ejercicio necesitaremos asegurarnos que el servidor de DHCP esté sirviendo a los clientes la IP del servidor de DNS que hemos configurado.

También deberemos asegurarnos de que los servidores cuyos parámetros IP se han configurado manualmente (DHCP, router), también tengan configurada la dirección IP del servidor de DNS que hemos instalado para que puedan acceder a los equipos de nuestra red por su nombre.





PRÁCTICA WINDOWS
----------------

Instalaremos DNS para Windows Server. Exploraremos la interfície gráfica de administración del servidor dns, configurando los parámetros básicos.

Configuraremos DNS para una pequeña red local y probaremos el servidor.





PRÁCTICA LINUX
--------------

Instalaremos Bind para Linux. Exploraremos el fichero de configuración.

Configuraremos DNS para una pequeña red local y probaremos el servidor.





PRÁCTICA LINUX ADICIONAL
------------------------

En una oficina de la empresa "mired.org" tenemos el despacho de los administrativos. También tenemos un datacenter.

  - Los administrativos son 10, y uno de ellos es el responsable.

  - En el datacenter hay dos servidores: "server" y "dns2". "server" también recibe los nombres "www", "bbdd" y "mail".

  - Cada estancia está en una red IP diferente. Aprovecha las redes del ejercicio anterior de DHCP.

 01. Instala y configura un servidor DNS con la siguiente política:

     - Las máquinas de los administrativos se deben llamar: "adm1", "adm2", ...

     - Todas las máquinas del datacenter también tendrán nombre.

     - Define alias para las máquinas significativas.
     
     Entrega los ficheros de configuración.

 02. Además de la resolución directa, también habrá resolución inversa.

     Entrega los ficheros de configuración.
 
 03. Instala en el servidor el módulo de Webmin para administrar DNS.

     Entrega capturas de pantalla de la página de configuración de DNS de Webmin.

 04. Instala un servidor DNS esclavo del primero, con la máxima seguridad que se pueda.

     Entrega los ficheros de configuración.

 05. Entrega un script para comprobar todos los registros, detectando qué servidor de DNS (maestro o esclavo) está activo.
 
 06. Integra el servidor de DNS con el servidor de DHCP para que cuándo el servidor de DHCP conceda IPs a los equipos, el servidor de DNS actualice el fichero de zona.

     Serán los clientes los que informen al servidor de DHCP de cuáĺ es su nombre, y el servidor de DHCP el que informe al servidor de DNS de las IPs concedida y del nombre del cliente.





MÁS PRÁCTICAS
-------------

Más prácticas: gestionar y delegar subdominios.

Más prácticas: ejercicios anteriores con software DNSMasq en vez de con Bind.

Más prácticas: registrar dominio gratuito en FreeNom para tus máquinas virtuales en la nube, y administrar tus DNS con Amazon Route53 , Oracle Cloud DNS , o tu propio servidor DNS en la nube.

Más prácticas: registrar dominio para red de casa con DynDNS y configurar para actualizar el registro DNS cuando tu proveedor cambia la IP pública de tu router doméstico.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Domain_Name_System>

  - <https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions>

  - <https://howdns.works/>

  - <http://www.unixwiz.net/techtips/iguide-kaminsky-dns-vuln.html>

  - <http://www.zytrax.com/books/dns/>
  
  - <https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software>

  - <https://tools.cisco.com/security/center/resources/dns_best_practices>

  - <https://securitytrails.com/blog/8-tips-to-prevent-dns-attacks>
