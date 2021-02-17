PREGUNTAS
---------

 01. ¿En qué consiste FTP? ¿y SFTP? ¿y TFTP? ¿Qué puertos y protocolo en la capa de transporte utilizan?

 02. ¿En qué consiste SAMBA (SMB/CIFS)? ¿Qué puertos y protocolo en la capa de transporte utilizan?

 03. ¿En qué consiste NFS? ¿Qué puertos y protocolo en la capa de transporte utilizan?

 04. ¿Que ventajas ofrecen NextCloud o Alfresco sobre los servidores de ficheros tradicionales?

 05. Imagina el caso de un servidor web donde varios usuarios tienen páginas. Para que los usuarios puedan subir y modificar páginas se instala un servidor de FTP.

     a) ¿Necesitarán nombre de usuario y contraseña para entrar?

     b) ¿Una vez dentro a qué carpeta apuntará el servidor FTP?

     c) ¿Tendrán permisos de escritura o sólo permisos de lectura en dicha carpeta?

     Ahora imagina el caso de un servidor FTP para que cualquier persona pueda descargar ficheros

     d) ¿Necesitarán nombre de usuario y contraseña para entrar?

     e) ¿Una vez dentro a qué carpeta apuntará el servidor FTP?

     f) ¿Tendrán permisos de escritura o sólo permisos de lectura en dicha carpeta?

 06. ¿Viene algún software de servidor de FTP con Windows Server? ¿Desde dónde se instala y desde dónde se administra? ¿Y para Windows no server?

 07. ¿Cuál es el software de servidor de FTP más conocido para Unix/Linux?

 08. Al instalar un servidor de FTP, ¿Qué parámetros a configurar piensas que serán los más importantes?

 09. En un cliente de FTP que no utiliza interfície gráfica (ventanas, carpetas, iconos para ficheros, ...), sino línea de comandos ¿Cuáles son los comandos "imprescindibles" y para qué sirven?

 10. ¿Cómo funciona FTP en modo activo? ¿Cómo funciona FTP en modo pasivo?





DATOS DE LA PRÁCTICA LINUX Y WINDOWS
------------------------------------

Configuraremos nuestro servidor FTP para que los usuarios Ana y Bob puedan subir las páginas de las dos webs que instalamos en la práctica de HTTP: www.mired.org y intranet.mired.org, respectivamente.

También daremos acceso anónimo a una carpeta para lectura de documentos pero sin escritura.





PRÁCTICA WINDOWS
----------------

  - Instalaremos Internet Information Server para Windows Server. Exploraremos la interfície gráfica de administración del servidor FTP, configurando los parámetros básicos.

  - Configuraremos el servidor web para que aloje páginas de diferentes usuarios, en una carpeta propia cada uno. A continuación configuraremos el servidor FTP para que dichos usuarios existan y al acceder con su nombre de usuario y contraseña el servidor FTP les lleve automàticamente a su carpeta.

  - Instalaremos y configuraremos Filezilla FTP Server para Windows.





PRÁCTICA LINUX
--------------

 01. Instala proFTPd para Linux (o vsFTPd o openssh-sftp). Explora su fichero de configuración.

 02. Configura el servicio de FTP para acceso de lectura anónimo (sin nombre de usuario ni contraseña) a un sistema de directorios con ficheros para bajarse.

 03. Configura el servicio de FTP para que un par de usuarios que crearás tenga acceso de lectura y escritura autentificado (con nombre de usuario y contraseña) al directorio de sus páginas web. Los usuarios del servidor FTP no deben tener acceso a la línea de comandos del sistema.
 
 04. Instala en el servidor el módulo de Webmin para administrar proFTPd.





PRÁCTICA SFTP
-------------

 01. Aprovechando que tenemos un servidor con IP pública en Oracle Cloud, instala en dicho servidor el paquete `openssh-sftp-server`

 02. ¿Dónde está su fichero de configuración?

 03. ¿Cómo accederás con un cliente remoto por SFTP?

 04. Adjunta captura de pantalla accediendo por línea de comandos y también con el cliente gráfico Filezilla.





PRÁCTICA NAS
------------

 01. Crea una máquina virtual donde instalarás FreeNAS u OpenMediaVault.

 02. Explora la administrador web del servidor NAS.
     
 03. Activa una carpeta donde dejarás ficheros via FTP, SMB, o NFS.
     
 04. Haz que tu servidor web en otra máquina virtual monte a cada inicio esta carpeta, que es donde estarán sus páginas web.





PRÁCTICA FICHEROS EN LA NUBE
----------------------------

Instala y configura un servidor de ficheros en la nube con NextCloud, y prepara varios clientes, tanto ordenadores de escritorio como dispositivos móbiles, para poder sincronizar los documentos, contactos y calendarios con dicho servidor.

     Si quieres, previamente puedes provar cómo funciona NextCloud en <https://try.nextcloud.com/>

También puedes probar SeaFile en lugar de NextCloud.





PRÁCTICA ARRANQUE EN RED
------------------------

Instala un servidor de PXE de arranque por red, que permitirá la instalación o ejecución de sistemas operativos por red mediante un menú.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/File_Transfer_Protocol>

  - <http://en.wikipedia.org/wiki/Network_File_System_(protocol)>

  - <http://en.wikipedia.org/wiki/Server_Message_Block>

  - <http://en.wikipedia.org/wiki/Samba_(software)>
