PREGUNTAS
---------

 01. ¿Qué es una Red Privada Virtual?

 02. ¿Qué es un tunel SSH?

 03. ¿Qué es IPSec?

 04. ¿Qué es OpenVPN?

 05. ¿Qué es Wireguard?

 06. Dibuja el esquema de varias redes físicas distantes que se comunican mediante un tunel VPN.

 07. ¿Viene algún software de servidor de VPN con Windows Server? ¿Desde dónde se instala y desde dónde se administra? ¿Y para Windows no server?

 08. ¿Cuál es el software de servidor de VPN más conocido para Unix/Linux?

 09. Al instalar un servidor de VPN en una red local, ¿Qué parámetros a configurar piensas que serán los más importantes?

 10. Al instalar un servidor de VPN en una red local, ¿Qué pruebas piensas que deberás hacer para comprobar el buen funcionamiento?





PRÁCTICA: MOBILE VPN
--------------------

Crea el siguiente montaje de red para conectar un "roadwarrior" a la red de la empresa por "mobile VPN":

 * Una máquina virtual que será un endpoint VPN, con dos tarjetas de red:

   - Una tarjeta de red para la red de la empresa (LAN)

   - Una tarjeta de red para Internet (WAN)

 * Una máquina virtual con servicio ssh y web que estará en la red de la empresa

   El endpoint VPN y el servidor estarán en red. Escoge tú las IPs que quieras y el tipo de red (por ejemplo, red interna)

 * El cliente que creará un túnel con el endpoint y que intentará acceder a la web y ssh del servidor.

   Dicho cliente puede ser:

   - Otra máquina virtual en el mismo anfitrión, en red con el endpoint VPN.

   - Una máquina virtual de un compañero, en otro anfitrión.

   - Tu teléfono móvil con una app gratuita y confiable para conexión remota.

Por ejemplo, mira las imágenes:

   ![imagen1](https://www.howtoforge.com/images/racoon_roadwarrior_vpn/60f3762733fb4e334ef84ada4a4e6280-1633.jpg)

   ![imagen2](https://guides.yoosecurity.com/wp-content/uploads/2017/02/vpn_road.png)

Puedes hacer la práctica por parejas.

Una opción es utilizar como VPN endpoint una distribución Linux o BSD especializada, como IPFire, OpnSense o PfSense, que puedes administrar fácilmente des de un navegador.

Otra opción es utilizar como VPN endpoint un Linux e instalar y administrar a pelo OpenVPN.

Otra opción es utilizar Windows tanto en el cliente como en endpoint VPN. Si es así, intenta hacerlo sin instalar software adicional para el VPN y conseguirlo con las opciones de Microsoft que incorpora el Windows.





PRÁCTICA: SITE-TO-SITE VPN 
--------------------------

Crea el siguiente montaje de red para unir mediante VPN "site to site" dos redes locales de una empresa separadas físicamente:

Cada red local estará simulada en un anfitrión diferente. Dicho anfitrión contendrá:

 * Una máquina virtual que será un endpoint VPN, con dos tarjetas de red:

   - Una tarjeta de red para la red de la empresa (LAN)

   - Una tarjeta de red para Internet (WAN)

 * Una máquina virtual con servicio ssh y web que estará en la red de la empresa

   El endpoint VPN y el servidor estarán en red. Escoge tú las IPs que quieras y el tipo de red (por ejemplo, red interna)

La tecnología del tunel del endpoint VPN será WireGuard sobre Linux. Aviso: necesitaréis núcleo 5.6 o superior.

Por ejemplo, mira las imágenes:

   ![imagen1](https://www.paloaltonetworks.com/content/dam/pan/en_US/images/cyberpedia/site-to-site-vpn.png)

   ![imagen2](https://support.zyxel.eu/hc/article_attachments/360000744459/mceclip0.png)

Realiza la práctica por parejas. Cada miembro de la pareja monta la red local en su anfitrión y luego unís las dos redes por VPN.

Otra opción es que cada grupo de clase monta una red local de una sede de la empresa, y luego unimos todas las sedes mediante VPN.





REFERENCIAS
-----------

  - <https://en.wikipedia.org/wiki/Virtual_private_network>

  - <https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling>

  - <https://en.wikipedia.org/wiki/OpenVPN>

  - <https://en.wikipedia.org/wiki/IPsec>

  - <https://en.wikipedia.org/wiki/WireGuard>

  - <https://www.cisco.com/c/en/us/support/docs/security-vpn/ipsec-negotiation-ike-protocols/14106-how-vpn-works.html>

  - <https://www.youtube.com/watch?v=_wQTRMBAvzg>

