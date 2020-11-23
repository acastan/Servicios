PREGUNTAS
---------

 01. ¿En qué consisten POP3, IMAP y SMTP? ¿Qué puertos y protocolo en la capa de transporte utilizan? ¿Tienen versión segura?

 02. ¿Qué es MUA ("mail user agent")? ¿Qué es MTA ("mail transfer agent")? ¿Qué es MDA ("mail delivery agent")? ¿Cómo interactuan entre ellos? Dibuja un esquema

 03. ¿Qué es Webmail? ¿Qué ventajas y desventajas tiene sobre un cliente de correo tradicional?

 04. ¿Viene algún software de servidor de correo con Windows Server? ¿Dónde? ¿De qué tipo? ¿Para que sirve el servidor de SMTP que viene con IIS? ¿Cuál es el servidor de correo comercial más conocido para Windows?
 
 05. ¿En qué consiste Microsoft Exchange?

 06. ¿Cuáles son los servidores de POP3, de IMAP y de SMTP más conocidos para Unix/Linux? ¿Y los filtros de correo basura más conocidos? ¿Y los filtros antivirus más conocidos?

 07. Al instalar un servidor de correo entrante y un servidor de correo saliente, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. ¿Cómo puedes utilizar telnet para comprobar el funcionamiento de ...
     a) ... un servidor SMTP?
     b) ... un servidor POP3?
     c) ... un servidor IMAP?





PRÁCTICA WINDOWS
----------------

  - Instalaremos correo entrante y saliente para Windows Server. Exploraremos la interfície gráfica de administración del servidor POP3 y SMTP, configurando los parámetros básicos.

  - Probaremos el servidor creando cuenta para varios usuarios.

  - Instalaremos un servidor gratuito IMAP4, POP3, SMTP i WebMail para Windows: hMailServer
  
  - Instalaremos Microsoft Exchange y lo probaremos des de un cliente con Microsoft Outlook.





PRÁCTICA LINUX: SERVIDOR DE CORREO
----------------------------------

  - Instalaremos correo entrante y saliente para Linux. Exploraremos los ficheros de configuración de los servidores. Probaremos el servidor creando cuenta para varios usuarios.

  - También daremos acceso al correo via web.

  - Añadiremos filtrado de correo basura y también antivirus.





PRACTICA LINUX: LISTAS DE CORREO
--------------------------------

  - Instalaremos un gestor de listas de correo.





PRÁCTICA LINUX: EXTRA
---------------------

En una pequeña red de una asociación pasa lo siguiente:

> Su proveedor de acceso a Internet les proporciona 1Gb de espacio de correo en el ordenador mail.pangea.org, en una única cuenta. Como ellos necesitan muchísimo más espacio de correo, consultable simultáneamente por los cinco ordenadores de la asociación, montan un servidor de correo. Dicho ordenador cada dos minutos recupera el correo de mail.pangea.org, lo almacena en un disco duro con espacio para 1Tb, y lo sirve a los ordenadores de la asociación mediante su propio servidor de correo.

Implementa dicha solución. Utiliza una cuenta de correo gratuita para la prueba. Puedes utilizar *Fetchmail* para recuperar el correo.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Email>

  - <http://en.wikipedia.org/wiki/Post_Office_Protocol>

  - <http://en.wikipedia.org/wiki/Internet_Message_Access_Protocol>

  - <http://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol>

  - <http://en.wikipedia.org/wiki/Comparison_of_mail_servers>

