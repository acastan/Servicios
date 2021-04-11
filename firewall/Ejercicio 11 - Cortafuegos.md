PREGUNTAS
---------

 01. ¿En qué consiste un cortafuegos o "firewall"? ¿Qué tipo de tráfico bloquea y a quien va dirigido dicho tráfico? ¿Qué tipo de tráfico no bloquea? ¿Qué no es capaz de hacer un cortafuegos?

 02. ¿Es lo mismo un cortafuegos de red que un cortafuegos personal? ¿Qué tipo de tráfico bloquea un cortafuegos personal y a quien va dirigido dicho tráfico?

 03. ¿Qué es un cortafuegos sin estado o "stateless firewall"? ¿Qué diferencia hay con un cortafuegos con estado o "stateful firewall"?

 04. ¿Puede un cortafuegos incorporar reglas dinámicamente des de aplicaciones? Pon un ejemplo

 05. ¿Qué es una DMZ ("zona desmilitarizada") y para qué sirve?

 06. ¿Qué es un cortafuegos a nivel de paquete? ¿Qué es un cortafuegos a nivel de circuito? ¿Qué es un cortafuegos a nivel de aplicación?

 07. ¿Viene algún software cortafuegos con Windows Server? ¿Desde dónde se instala y desde dónde se administra? ¿Cuál es el software de cortafuegos comercial más conocido para Windows?

 08. ¿Cuál es el software de cortafuegos más conocido para Linux? ¿Y para otros sistemas Unix? ¿Qué sistema Unix y distribuciones Linux son especialmente seguras para instalar PCs que hagan de cortafuegos y sistemas de detección de intrusos?

 09. Queremos instalar un cortafuegos en una pequeña red local de cinco PCs y un servidor HTTP y SQL, todos con IP pública y salida a Internet. Dicho cortafuegos debe proteger los ordenadores de la red de ataques del exterior. También debe proteger el servidor SQL de los ordenadores de la red interna y del exterior, que sólo accederán al servicio de HTTP. (el servicio SQL es accedido sólo por el servicio HTTP del mismo ordenador para crear páginas web dinámicas a partir de la base de datos, pero no queremos que los usuarios realicen consultas directas sobre el servidor de bases de datos). De momento dejamos que los usuarios de nuestra red accedan a cualquier servicio de Internet.

     a) Piensa dónde colocarías el cortafuegos y dibuja un esquema de la red.

     b) Escribe las reglas del cortafuegos en la siguiente tabla:

        | red origen | puerto origen | red destino | puerto destino | protocolo | estado | acción |
        | ---------- | ------------- | ----------- | -------------- | --------- | ------ | ------ |
        |            |               |             |                |           |        |        |

 10. En el ejercicio anterior que normas añadirías al cortafuegos para impedir que los usuarios de nuestra red accedan al exterior excepto a un servidor de correo que utiliza IMAP y SMTP en los puertos estándar.





PRÁCTICA
--------

Tenemos la siguiente configuración en máquinas virtuales:

  - En nuestra red local un cortafuegos/router accesible por ssh.
 
  - En nuestra red local un servidor web también accesible por ssh.
 
  - En internet un cliente, para hacer pruebas.

El cortafuegos tendrá dos tarjetas de red para unir Internet con la red local:

  - El cliente en Internet  y el cortafuegos estarán conectados en modo puente (-si dicho cliente quieres que sea la máquina real o "anfitrión"-) o en red NAT (-si dicho cliente es otra máquina virtual).
 
  - El cortafuegos y el servidor de la red local, máquinas virtuales los dos, estarán conectados en red interna.

Queremos manipular el tráfico en el cortafuegos para que:

  - Des de Internet sólo permitiremos tráfico a la red interna hacia el servidor web, a sus puertos 80 y 443.

  - Des de la red interna hacia el cortafuegos sólo permitiremos conexiones ssh al puerto tcp/22 y preguntas dns al puerto udp/53.

  - Tanto el servidor web como el cortafuegos podrán acceder hacia fuera, excepto al puerto tcp/1337.

  - El cortafuegos enrutará de la red interna hacia el exterior.

Realiza el ejercicio con reglas des de la línea de comandos con [*iptables*](https://en.wikipedia.org/wiki/Iptables), [*nftables*](https://en.wikipedia.org/wiki/Nftables) o [*ufw*](https://en.wikipedia.org/wiki/Uncomplicated_Firewall).

 01. Programa las reglas del cortafuegos para que cumpla los anteriores requisitos. Entrega dichas reglas.

 02. Entrega todas las pruebas que has hecho para comprobar el correcto funcionamiento del cortafuegos.

 03. Las reglas deben arrancar con el cortafuegos. ¿Cómo lo consigues?

 04. Una vez conseguido, prueba lo mismo con alguna interfaz gráfica al cortafuegos, como [*gufw*](https://help.ubuntu.com/community/Gufw), [*fwbuilder*](http://fwbuilder.sourceforge.net/4.0/quick_start_guide.shtml) o [*shorewall*](https://shorewall.org/GettingStarted.html). Entrega capturas de pantalla.

 05. Una vez conseguido, prueba lo mismo con alguna distribución especializada en cortafuegos y enrutamiento, como [*Zeroshell*](https://zeroshell.org/), [*pfSense*](https://www.pfsense.org/), [*OpnSense*](https://opnsense.org/) o [*IPFire*](https://www.ipfire.org/). Entrega capturas de pantalla.

Para escribir las reglas del cortafuegos es muy importante que sigas estos consejos:

1) Debes entender muy bien la diferencia entre tráfico input, output y forward. Tráfico input es el que va específicamente dirigido a la máquina que hace de cortafuegos, como por ejemplo una actualización de sus paquetes o un intento de conexión ssh. Sin embargo, tráfico forward es el que llega al cortafuegos, porque este hace de router, pero su destino final es otra máquina.

2) Establece las reglas por defecto. A continuación, para poder aclararte, crea seis apartados para ir escribiendo las diferentes reglas:
   - tráfico del exterior hacia la red local,  
   - tráfico de la red local hacia el exterior,  
   - tráfico del exterior hacia el cortafuegos,  
   - tráfico del cortafuegos hacia el exterior,  
   - tráfico de la red local hacia el cortafuegos,  
   - tráfico del cortafuegos hacia la red local

3) A la hora de bloquear tráfico, comprueba que no estés bloqueando las respuestas a tráfico establecido. Por ejemplo, si permites el tráfico de salida de una red local hacia el exterior, pero bloqueas el tráfico de entrada, cuando un ordenador de la red local inicie una conexión hacia el exterior (-para, por ejemplo, actualizarse-) la respuesta del exterior quedará bloqueada. Para solucionar esto pon reglas que permitan el paso de paquetes de comunicaciones establecidas. Por ejemplo, en iptbles esto se soluciona utilizando los módulos [*conntrack* y *state*](https://unix.stackexchange.com/questions/108169/what-is-the-difference-between-m-conntrack-ctstate-and-m-state-state)

4) No te olvides de permitir el tráfico de localhost dentro del cortafuegos, por si algunos servicios se necesitan comunicar con otros en la misma máquina vía sockets.

5) No te olvides de permitir el tráfico de DNS (udp/53), para la resolución de nombres.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Firewall>

  - <http://www.docum.org/docum.org/kptd/>

  - <https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture>

  - <http://pello.io/filez/firewall/iptables.html>

  - <https://wiki.nftables.org/wiki-nftables/>

  - `man iptables` , `man iptables-extensions` , `man nft`





ANEXO: MANUAL DE IPTABLES
-------------------------



### ACCIONES DE IPTABLES

  * Vacía la lista de reglas: `iptables -F`  
    Ejemplo:

        iptables -F
        iptables -X
        iptables -Z
        iptables -t nat -F

  * Establece política por defecto: `iptables -P`  
    Ejemplo:

        iptables -P INPUT DROP
        iptables -P OUTPUT DROP
        iptables -P FORWARD DROP

  * Añade nuevas reglas: `iptables -A`  
    Ejemplo:

        iptables -A INPUT -i lo -j ACCEPT
        iptables -A OUTPUT -o lo -j ACCEPT
        iptables -A INPUT -s 192.168.1.0/25 -p tcp --dport 80 -j ACCEPT

  * Lista las reglas: `iptables -L`  
    Ejemplo:

        iptables -L -n -v

  * Guarda las reglas:

        sudo iptables-save -f fichero

    Pero si lo que queremos es guardarlas y que se carguen cada vez que iniciamos el ordenador:

        sudo apt install iptables-persistent
        sudo netfilter-persistent save

Existen muchos más comandos sobre reglas (borrar, insertar, modificar, etc) , pero para una introducción sólo vamos a necesitar los anteriores.

Para cada paquete, las reglas se evalúan de una en una en el orden que se introdujeron, hasta que el paquete encaja con una regla. Si encaja, se le aplica la acción asociada a la regla y se deja de evaluar las siguientes reglas de la lista. Si no encajó con ninguna, entonces se le aplica la política por defecto.

Las cadenas donde guardaremos reglas son `INPUT`, `OUTPUT`, `FORWARD`, `PREROUTING` y `POSTROUTING`.

  * `INPUT` para filtrar paquetes que van dirigidos específicamente a las IPs del cortafuegos. Se utiliza bastante en cortafuegos personales y también en cortafuegos de red que ofrecen otros servicios.

  * `OUTPUT` para filtrar paquetes que parten de las IPs del cortafuegos. Se utiliza bastante en cortafuegos personales y también para permitir que el cortafuegos se comunique con otros ordenadores.

  * `FORWARD` para filtrar paquetes que pasarán a través del cortafuegos, que venían de un segmento de red y se dirigían hacia otro segmento de red. Se utiliza en cortafuegos de red. ¡No os confundáis con `INPUT` y `OUTPUT`! Un cortafuegos de red puede recibir paquetes que no iban destinados a él, si esta actuando como router.

  * `PREROUTING` para modificar IPs y puertos de paquetes que llegan al cortafuegos, antes de que se les apliquen las cadenas `INPUT` o `FORWARD`.

  * `POSTROUTING` para modificar IPs y puertos de paquetes que salen del cortafuegos, después de que se les apliquen las cadenas `OUTPUT` o `FORWARD`.


---


### ARGUMENTOS DE IPTABLES

  * La opción `-t` especifica la tabla de reglas a la que se aplica el comando, que puede ser `filter` (por defecto), `nat`, `mangle`, `raw` y `security`. Nosotros sólo trabajaremos el filtrado de paquetes (`filter`) y el enrutamiento (`nat`).

  * La opción `-j { ACCEPT | DROP | REJECT | LOG | SNAT | DNAT | MASQUERADE }` especifica la acción a realizar con el paquete. Las más comunes son aceptarlo (`ACCEPT`) o bloquearlo (`DROP`).

  * Las opciones `-s { IP | nombre | red/mask }` y `-d { IP | nombre | red/mask }` especifican el origen y el destino del paquete, respectivamente. Puede ser una IP, el nombre de una máquina, o toda un rango de IPs.

  * Las opciones `-i tarjeta_entrada` y `-o tarjeta_salida` permiten especificar el origen y el destino del paquete, respectivamente, utilizando los nombres de tarjetas de red en lugar de rangos de IPs.

  * La opción `-p { tcp | udp | icmp }` especifica el tipo de tráfico (-ver siguientes opciones-).

  * Las opciones `--dport puerto` y `--sport puerto` indican el puerto de origen y destino, respectivamente, si el tráfico especificado en la anterior opción es TCP o UDP.

  * La opción `--icmp-type tipo_mensaje` indica tipo de mensaje si el tráfico es ICMP.

  * La opción `-m conntrack --ctstate { NEW | ESTABLISHED | RELATED | INVALID | ... }` permite filtrar paquetes según el estado de la conexión TCP. Antiguamente esta opción se escribía `-m state --state { ... }`. Es muy útil cuando quiero bloquear tráfico hacia un puerto sólo en una dirección, ya que no querremos bloquear las respuestas de una conexión ya establecidas por dicho puerto.

  * La opción `--to IP:puerto`, utilizado en enrutamiento (NAT, PNAT) para modificar la IP o puerto de un paquete, especifica la nueva IP o puerto.


---


### EJEMPLOS DE IPTABLES

  - <https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands>





ANEXO: MANUAL DE NFTABLES
-------------------------



### ACCIONES DE NFTABLES

  * Vacía la lista de reglas: `nft flush ruleset`

  * Crea tablas para añadir después cadenas: `nft add table *familia* *tabla*`  
    Ejemplo:

        nft add table inet filter
        nft add table inet nat
  
  * Establece política por defecto: `nft chain *familia* *tabla* *hook* { policy *acción* }`  
    Ejemplo:

        nft chain inet filter input    { policy drop }
        nft chain inet filter output   { policy drop }
        nft chain inet filter forward  { policy drop }
        nft chain inet nat prerouting  { policy accept }
        nft chain inet nat postrouting { policy accept }

  * Añade nuevas cadenas: `nft add chain *familia* *tabla* *cadena* { type *tipo* hook *hook* priority *valor* \; [policy *acción*] }`  
    Ejemplo:

        nft add chain inet filter input    { type filter hook input       priority 0 \; }
        nft add chain inet filter output   { type filter hook output      priority 0 \; }
        nft add chain inet filter forward  { type filter hook forward     priority 0 \; }
        nft add chain inet nat prerouting  { type nat    hook prerouting  priority 0 \; }
        nft add chain inet nat postrouting { type nat    hook postrouting priority 100 \; }
        
  * Añade nuevas reglas: `nft add chain *familia* *tabla* *regla* { type *tipo* hook *hook* priority *valor* \; policy *acción* }`  
    Ejemplo:

        nft add rule inet filter input  iifname "lo" accept
        nft add rule inet filter output oifname "lo" accept
        nft add rule inet filter input  iifname "eth0" icmp type echo-request counter accept
        nft add rule inet filter output oifname "eth0" icmp type echo-reply   counter accept
        nft add rule inet filter input  ip saddr 192.168.1.0/24 tcp dport 22 ct state new,established accept
        nft add rule inet filter output ip daddr 192.168.1.0/24 tcp sport 22 ct state established accept
        nft add rule inet filter forward iifname "eth1" oifname "eth0" ip saddr 192.168.1.0/24 udp dport 53 ct state new,established accept
        nft add rule inet filter forward iifname "eth0" oifname "eth1" ip daddr 192.168.1.0/24 udp sport 53 ct state established accept
        nft add rule inet filter forward iifname "eth1" oifname "eth0" ip protocol tcp ip saddr 192.168.1.0/24 tcp dport { 80,443} ct state new,established accept
        nft add rule inet filter forward iifname "eth0" oifname "eth1" ip protocol tcp ip daddr 192.168.1.0/24 tcp sport { 80,443} ct state established accept
        nft add rule inet nat postrouting oifname "eth0" ip saddr 192.168.1.0/24 masquerade

  * Lista las reglas: `nft list ruleset`

  * Guarda las reglas:

        echo "nft flush ruleset" > reglas.nft
        nft list ruleset >> reglas.nft
        
  * Carga las reglas de un fichero:
  
        nft -f reglas.nft

  * Traducir reglas de IPTables a NFTables: `iptables-translate *regla_iptables*`  

Existen muchos más comandos sobre reglas (borrar, insertar, modificar, etc) , pero para una introducción sólo vamos a necesitar los anteriores.

Para cada paquete, las reglas se evalúan de una en una según el orden de prioridad, hasta que el paquete encaja con una regla. Si encaja, se le aplica la acción asociada a la regla y se deja de evaluar las siguientes reglas de la lista. Si no encajó con ninguna, entonces se le aplica la política por defecto.

Los grupos donde guardaremos reglas son `input`, `output`, `forward`, `prerouting` y `postrouting`.

  * `input` para filtrar paquetes que van dirigidos específicamente a las IPs del cortafuegos. Se utiliza bastante en cortafuegos personales y también en cortafuegos de red que ofrecen otros servicios.

  * `output` para filtrar paquetes que parten de las IPs del cortafuegos. Se utiliza bastante en cortafuegos personales y también para permitir que el cortafuegos se comunique con otros ordenadores.

  * `forward` para filtrar paquetes que pasarán a través del cortafuegos, que venían de un segmento de red y se dirigían hacia otro segmento de red. Se utiliza en cortafuegos de red. ¡No os confundáis con `input` y `output`! Un cortafuegos de red puede recibir paquetes que no iban destinados a él, si esta actuando como router.

  * `prerouting` para modificar IPs y puertos de paquetes que llegan al cortafuegos, antes de que se les apliquen las cadenas `input` o `forward`.

  * `postrouting` para modificar IPs y puertos de paquetes que salen del cortafuegos, después de que se les apliquen las cadenas `output` o `forward`.


---


### EJEMPLOS DE NFTABLES

  - <https://kernelnewbies.org/nftables_examples>

  - <https://wiki.archlinux.org/index.php/nftables#Examples>
