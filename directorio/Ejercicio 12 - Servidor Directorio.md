PREGUNTAS
---------

 01. ¿En qué consiste un servicio de directorio? ¿Qué ventajas proporciona?

 02. ¿Qué es LDAP?

 03. En LDAP, ¿Qué significa entrada, objeto, DN, RDN, DC, CN, SN, OU, O, C, ST?

 04. Dibuja el esquema del directorio con base iam.cat, donde existen las unidades organizativas alumnos y profesores. Dentro de alumnos estan Ana y Bob. Dentro de profesores están Álex y Xavi.

 05. ¿Viene algún software de directorio con Windows Server? ¿Desde dónde se instala y desde dónde se administra?

 06. ¿Cuál es el software de directorio más conocido para Linux? ¿Qué herramientas de administración hay para dicho servicios?

 07. Al instalar un servidor de directorio, ¿Qué parámetros a configurar piensas que serán los más importantes?

 08. ¿Qué es PAM y cuál es el propósito del fichero /etc/nsswitch.conf en Linux?

 09. ¿Cuáles son las principales diferencias entre LDAP y Active Directory?

 10. ¿Cuál es la diferencia entre servicio de directorio, LDAP y OpenLDAP?





PRÁCTICA WINDOWS ADDS
---------------------

  - Instala Active Directory sobre Windows Server:
    <http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx>

    1) Pon la máquina virtual del servidor en red interna. Dale la IP fija 192.168.15.2

    2) Instala ADDS , DHCP y DNS. Soluciona los "avisos" posteriores a la instalación.

    3) Promociona el servidor como controlador de dominio "mired.org".

    4) Configura DHCP para que sirva las IPs del rango 192.168.15.100 a 200 y DNS 192.168.15.2

    5) Comprueba la configuración del DNS

    6) Crea dos usuarios, "Epi" y "Blas", dentro del dominio.

    7) Arranca un cliente, en red interna con el servidor. Comprueba que recibe IP correcta del servidor de DHCP.

    8) Pon el cliente dentro del dominio y reinicia.

    9) Comprueba que puedes iniciar sesión en el cliente con los usuarios del dominio.

  - Crearemos una política de grupo básica para aplicarla sobre una unidad organizativa del dominio:

    1) Crea una unidad organizativa (-"OU" a partir de ahora-) llamada "contabilidad" dentro del dominio.

    2) Crea un nuevo usuario "Gustavo" y muévelo a dicha OU.

    3) Crea un nuevo objeto de política de grupo (-"GPO" a partir de ahora-).

    4) Edita dicho GPO y activa las plantillas para deshabilitar el panel de control y deshabilitar el gestor de tareas.

    5) Enlazamos al OU el GPO.

    6) Arranca un ordenador cliente que esté en el dominio (-ver práctica anterior-) e inicia sesión con el usuario "Gustavo". Comprueba que dicho usuario no puede acceder al panel de control ni al gestor de tareas.

    7) Opcionalmente, vuelve a la GPO que has creado y explora nuevas preferencias y plantillas.

  - Activa el perfil móvil de usuario y comprueba su efectividad iniciando sesión con el mismo usuario de dos equipos diferentes del dominio.

  - Aplica las siguientes directivas de seguridad a una unidad organizativa del dominio, entregando por cada directiva: la ruta (carpeta y subcarpetas) donde hallaste la plantilla, una captura de pantalla configurando la plantilla, y una captura de pantalla donde se vea cómo afecta la directiva a un usuario de la UO.

    - Aplicar fondo de escritorio de la empresa (inventa una imagen cualquiera)

    - Un mensaje al iniciar sesión (inventa el mensaje que quieras)

    - Sin acceso ni vista a unidades locales (discos, dvd, etc)

    - Desactivación de la configuración del tema/apariencia de escritorio.

    - Desactivación de la configuración de pantalla.

    - Sin acceso a la línea de comandos.

    - Ejecutar un programa al iniciar sesión (escoge el programa que quieras)

    - Sin posibilidad de instalar nuevos programas.

    - Denegar la ejecución de al menos una aplicación de Windows (escógela tú). Extra: ¿qué pasa si se cambia de nombre a la aplicación?

    - Bloquear la cuenta si introduce la contraseña incorrecta tres veces seguidas.

    - Cierra la sesión si el usuario sobrepasa 30 minutos.

    - Obliga a que la contraseña del usuario tenga una cierta longitud.

    - Permitir cerrar sesión pero no apagar el equipo

    - Cuando use el navegador Internet Explorer, no permitir el cambio de proxy.

    - Cuando use el navegador Internet Explorer, restringir el acceso a facebook.com.

    - Cuando use el navegador Internet Explorer, la página de inicio será campus.iam.cat.





PRÁCTICA LINUX OPENLDAP
-----------------------

 01. Instala [OpenLDAP](https://www.openldap.org/) sobre Ubuntu Server, y [phpLDAPadmin](http://phpldapadmin.sourceforge.net/) para administrarlo.

     <http://www.howtoforge.com/how-to-install-openldap-server-on-debian-and-ubuntu>  
     <http://help.ubuntu.com/lts/serverguide/openldap-server.html>  
     <http://help.ubuntu.com/community/OpenLDAPServer>  
     <http://help.ubuntu.com/community/LDAPClientAuthentication>

     El nombre del dominio debe ser: mired.org

         dn: dc=mired,dc=org

     El nombre del administrador del dominio debe ser: admin

         cn=admin,dc=mired,dc=org

     Tendremos las unidades organizativas: alumnos y grupos

         dn: ou=alumnos,dc=mired,dc=org
         dn: ou=grupos,dc=mired,dc=org

     En la ou=grupos habrá un grupo llamado primero

         dn: cn=primero,ou=grupos,dc=mired,dc=org

     En la ou=alumnos habrá un usuario llamado Pepito 

         dn: uid=Pepito,ou=alumnos,dc=mired,dc=org

 02. Comprueba con ldapsearch que el contenido se ha añadido correctamente.

 03. Busca con ldpasearch información de la unidad organizativa "alumnos".

 04. Busca con ldpasearch información del usuario "Pepito".

 05. Instala y configura el paquete "phpLDAPadmin" en el servidor LDAP.

 06. Visualiza con phpLDAPadmin los atributos y valores del usuario "admin".

 07. Da de alta con phpLDAPadmin al usuario Joselito.

 08. Prueba la herramienta [JXplorer](http://jxplorer.org/) des de un cliente para consultar la información del directorio.

 09. Prueba la herramienta [Apache Directory Studio](http://directory.apache.org/studio/) des de un cliente para consultar la información del directorio.





PRÁCTICA INTEGRAR CLIENTE LINUX EN DOMINIO ADDS WINDOWS
-------------------------------------------------------

Escribe una guía sobre cómo integrar tu Ubuntu como cliente de un dominio Active Directory gestionado por un servidor Windows, donde aparezca:

  - Qué paquetes se deben instalar y porqué se debe instalar cada uno de esos paquetes.

  - El procedimiento de instalación.

  - Las líneas modificadas o añadidas en los correspondientes ficheros de configuración.

  - Las pruebas realizadas.

Cómo guías puedes comenzar con:

  <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/windows_integration_guide/sssd-ad>  
  <https://sospedia.net/unir-ubuntu-16-dominio-windows-server-active-directory/>  
  <https://calnus.com/2016/12/12/uniendo-gnu-linux-a-nuestro-active-directory-mediante-samba-y-sssd/>  
  <http://somebooks.es/unir-cliente-ubuntu-16-04-al-dominio-windows-server-2016-parte-i/>  
  <http://somebooks.es/unir-cliente-ubuntu-16-04-al-dominio-windows-server-2016-parte-ii/>





PRÁCTICA LINUX COMO SERVIDOR DE DOMINIO ADDS
--------------------------------------------

El programa SAMBA, des de su versió 3, permitía a un ordenador funcionar como servidor de dominio clásico (sin Active Directory).

El programa SAMBA, des de su versió 4, permite a un ordenador funcionar como servidor de dominio Active Directory.

Escribe una guía sobre cómo convertir tu Ubuntu en servidor de un dominio Active Directory, donde aparezca:

  - Qué paquetes se deben instalar y porqué se debe instalar cada uno de esos paquetes.

  - El procedimiento de instalación.

  - Las líneas modificadas o añadidas en los correspondientes ficheros de configuración.

  - Las pruebas realizadas, integrando en el dominio un cliente Windows y un cliente Linux.

Cómo guías puedes comenzar con:

  <http://blog.ragasys.es/controlador-de-dominio-active-directory-sobre-linux-ubuntu>  
  <https://www.tecmint.com/install-samba4-active-directory-ubuntu/>  
  <http://somebooks.es/capitulo-12-integracion-de-redes-mixtas-con-windows-y-linux/7/>  
  <https://wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller>





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Directory_services>

  - <http://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol>

  - <http://en.wikipedia.org/wiki/Active_Directory>

  - <http://support.microsoft.com/es-es/kb/196464>

  - <http://www.zytrax.com/books/ldap/>

