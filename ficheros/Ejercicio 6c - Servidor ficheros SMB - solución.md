VENTAJAS SERVIDOR FICHEROS
--------------------------

  - Permet posar permisos per usuaris del domini.

  - Permet gestionar els recursos compartits de manera centralitzada.

  - Permet usar eines administratives sobre els recursos compartits: quotes, filtres per tipus de fitxer, logs, estadístiques, deduplicació, antivirus, ...

  - Centralitzar les carpetes a compartir simplifica les còpies de seguretat

  - No tenir documents als ordinadors permet fer recuperacions (clonacions) ràpides sense preocupar-se per perdre el que hi havia


___



SMB/CIFS
--------

SMB, también conocido como CIFS, es un protocolo creado por IBM y Microsoft para la gestión de recursos compartidos. Actualmente va por la versión 3, como vimos en los apuntes anteriores.

SMB es un protocolo cliente/servidor que utiliza los puertos 137/udp, 138/udp, 139/tcp y 445/tcp.

SMB está pensado para la autoexploración: o bien los ordenadores que comparten recursos se van anunciando periódicamente, o bien los clientes preguntan a toda la red buscando recursos. Este comportamiento produce muchos broadcast y llena la red de paquetes, lo que puede generar problemas de saturación de la red. Ajustando parámetros del servidor NetBIOS se puede reducir drásticamente dicho problema.

Han aparecido nuevas versiones de SMB con el tiempo:

  - SMB 1     : hasta Windows XP

  - SMB 2     : Windows Vista y Windows Server 2008

  - SMB 2.1   : Windows 7     y Windows Server 2008r2

  - SMB 3     : Windows 8     y Windows Server 2012

  - SMB 3.0.2 : Windows 8.1   y Windows Server 2012r2

  - SMB 3.1.1 : Windows 10    y Windows Server 2016

Dos Windows de versiones diferentes hablan la versión de SMB más alta que **ambos** reconocen.

Unos acrónimos que necesitarás tener a mano:

  - DC: Domain Controller, o Controlador de dominio de Active Directory
    - PDC: Primary DC
    - BDC: Backup DC
  - NetBIOS , WINS: sistema de nombres del protocolo SMB, independiente de DNS
    - MB: Master Browser
      - LMB: Local MB
      - DMB: Domain MB
  - Guest: usuario sin contraseña

Para aprender un poco más sobre SMB lee https://www.samba.org/cifs/docs/what-is-smb.html


___



SMB y Windows
-------------

  - Comun entre local y red:

    * Allow y Deny

    * Acumulativo cuando un usuario está en dos grupos

    * Deny tiene prioridad cuando un usuario está en dos grupos

    * Por defecto deny si no hemos puesto nada

  - Permisos locales: read, read&execute, list folder, write, modify, full control (y permisos atómicos)

  - Permisos Share: read, change, full control

  - ¿Cómo conectarse a un SHARE? //servidor/share

  - Mapear una unidad de disco a un share

  - Common shares (C$, D$, ADMIN$, PRINT$, IPC$, NETLOGON, SYSVOL)

Para instalar un servidor de carpetas en un servidor Windows:

  - Instala el rol y las utilidades

  - Explora las herramientas de administración

  - Publica los recursos en Active Directory:

    Active Directory Users and Computers Management Console. Right-click the organizational unit of choice -> New -> Shared Folder-> name for this publication of the share and, of course, the share name.


___



SMB y Linux
-----------

SAMBA es una implementación de dicho protocolo. Es un programa de código libre, que actualmente en su versión 4, permite desde compartir carpetas e impresoras, a instalar en Linux un controlador de dominio Active Directory, gratuitamente, sin costes de licencias.

SAMBA está formado por dos servicios:

  - smbd: el servidor de recursos compartidos
  - nmbd: el servidor de nombres NetBIOS

Estos apuntes se centran en el uso de Samba como un servidor de ficheros y carpetas autónomo. SAMBA también puede utilizarse como controlador de un dominio, pero eso lo veremos en otro tema, más adelante.


___



INSTALAR Y CONFIGURAR EL SERVIDOR SAMBA
---------------------------------------

Para instalar el servidor:

    $ sudo apt update
    $ sudo apt install samba

Para iniciar el servidor, si hiciera falta:

    $ sudo systemctl start smbd.service nmbd.service
    $ sudo systemctl status smbd.service
    $ sudo systemctl status nmbd.service

El principal archivo de logs de SAMBA es /var/log/samba/log.smbd

El principal archivo de configuración de SAMBA es /etc/samba/smb.conf

Dicho fichero de configuración está formado por un número variable de secciones, conteniendo cada sección parámetros de configuración. Cada sección corresponde a un recurso compartido, cuyo nombre va entre corchetes rectangulares [ ]. Por ejemplo, para compartir una carpeta "/home/ana/docs" con el nombre de recurso "documents":

    [documents]
      path = /home/ana/docs           ; carpeta a compartir
      browseable = yes                ; el servidor muestra la carpeta cuando navegamos por \\SERVIDOR
      guest ok = no                   ; no admitimos el usuario invitado sin contraseña
      valid users = ana, @alumnos     ; usuarios válidos (si el primer caracter es @ se trata de un grupo)
      read only = no                  ; se puede escribir

Pero existen unas secciones especiales de configuración global:

  - [global]         Sección general: nombre de equipo, grupo de trabajo, etc.

  - [homes]          Sección con opciones de carpetas automáticamente asociadas a usuarios

  - [printers]       Sección con opciones comunes de impresión

  - [print$]         Sección de los controladores de impresión

  - [netlogon]       Sección de scripts de inicio de sesión en un dominio

  - [profiles]       Sección para los perfiles móbiles de usuarios

El fichero de configuración inicialmente estará lleno de ejemplos. Todavía encontrarás muchos más ejemplos en el fichero /usr/share/doc/samba-doc/examples/ si has instalado el paquete samba-doc. Inicialmente, vale la pena vaciar el fichero de configuración de ejemplos y comenzar con un fichero "limpio".

  - <https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html>
  - <https://wiki.samba.org/index.php/Setting_up_Samba_as_a_Standalone_Server>
  - <http://www.sergio-gonzalez.com/doc/10-ldap-samba-cups-pykota/html/samba-configuracion-samba-opciones.html>

Una vez escrita nuestra configuración en el fichero, podemos probar si hmos cometido errores de sintaxis con el siguiente comando:

    $ testparm

Después de modificar el fichero de configuración normalmente hay que reiniciar el servidor:

    $ sudo systemctl restart smbd.service
    $ sudo tail /var/log/samba/log.smbd

Sin embargo, dicen que el servicio Samba lee cada 60 segundos el fichero de configuración y aplica cambios, por lo que no sería necesario reiniciar el servicio. En mi experiencia, sí es necesario.


___



OPCIONES DE CONFIGURACIÓN DE SAMBA
----------------------------------

Puedes obtener muchísima más información sobre la opciones ejecutando el comando:

    $ man samb.conf



Opciones globales:

  - server role = modo :   Determina el modo de operar del servidor  
      = auto / standalone / member server / classic primary domain controller / netbios backup domain controller / active directory domain controller

  - netbios name = nombre :   Nombre NetBIOS del servidor samba

  - workgroup = nombre :   Nombre NetBIOS del grupo de trabajo

  - security : Permite determinar el modo de compartición de recursos de samba  
      = Share     Comparte los recursos con contraseña (como Windows 98)  
      = User      Gestiona los permisos por usuario (como Windows XP)  
      = Domain    Gestiona los permisos por dominio  
      = Server    Indica que los permisos son gestionados por otro servidor  
      = Ads       Samba se comporta como miembro de un dominio Active Directory

  - domain logons = yes/no :   Indica si Samba es autentificador del dominio

  - domain master = yes/no :   Indica si Samba es controlador de dominio

  - encrypt passwords = yes/no :   Indica si Samba envía contraseñas encriptadas (por defecto)

  - smb passwd file = /etc/smbpasswd :   Archivo de contraseñas encriptadas de Samba, que no tienen por qué coincidir la contraseña del usuario en Linux

  - passdb backend = tbdsam/ldapsam :   Escoge como se guardarán la información del usuario  
      = tdbsam:/etc/samba/private/passdb.tdb  
      = ldapsam:"ldap://ldap-1.example.com ldap://ldap-2.example.com"

  - logon script = fichero_script.BAT :   Script que ejecutarán los clientes windows al loguearse

  - wins server = IP :   Servidor de nombres Wins

  - wins support = yes/no :   Samba sea servidor wins

  - load printers = yes/no :   Automáticamente comparte las impresoras del sistema

  - log level = nivel :   Permite definir el nivel de detalle del log  
      = all, tdb, printdrivers, lanman, smb, passdb, sam, auth, winbind, vfs, idmap, quota, acls, locking, msdfs, dmapi, registry, etc.
    
  - map to guest : Indica la acción a tomar cuando falla el inicio de sesión de un usuario  
      = Never          Rechaza el usuario con contraseña incorrecta  
      = Bad User       Rechaza el usuario con contraseña incorrecta, pero si no existía el usuario pasará a ser invitado  
      = Bad Password   El usuario con contraseña incorrecta pasará a ser invitado  
      = Bad UID        El usuario que se autentifica, pero no era un usuario Linux, pasará a ser invitado  



Opciones de carpetas compartidas:

  - comment = texto :   Descripción de la carpeta compartida

  - path = ruta :   Ruta a la carpeta a compertir

  - browseable = yes/no :   Indica si el recurso compartido aparecerá en la lista de recursos del servidor

  - create mask = máscara :   Restringe mediante una máscara los permisos de los archivos creados

  - directory mask = máscara :   Restringe mediante una máscara los permisos de los directorios creados

  - guest ok = yes/no :   Indica si el usuario anónimo tiene permiso de acceso

  - guest account = usuario :   cuenta utilizada para acceder a los recursos como usuario anónimo (por defecto nobody/nogroup)

  - valid users = usuarios, @grupos :   Indica qué usuarios pueden acceder al recurso

  - invalid users = usuarios, @grupos :   Indica qué usuarios no pueden acceder al recurso

  - writable = yes/no :   Indica si se puede escribir en el recurso, como la opción read only

  - read list = usuarios :   Indica los usuarios que sólo pueden leer

  - write list = usuarios :   Indica los usuarios que pueden imprimir

  - admin users = usuarios :   Indica los usuarios con total permiso sobre los recursos

  - hosts allow = IPs :   Equipos permitidos de acceder al recurso (se puede aplicar en [global])

  - hosts deny = IPs :   Equipos no permitidos de acceder al recurso (se puede aplicar en [global])

  - force user = usuario :   Usuario utilizado como uid del usuario conectado

  - force group = grupo :   Grupo utilizado como gid del usuario conectado



Opciones de impresoras compartidas:

  - comment = texto :   Descripción de la impresora compartida

  - path = ruta :   Ruta a la cola de impresión (por defecto en /var/spool/samba)

  - browseable = yes/no :   Indica si el recurso compartido será visible cuando se escanea la red

  - public = yes/no :   Indica si cualquier usuario puede imprimir

  - printable = yes/no :   Indica si se puede imprimir en la impresora o no



Existen unos símbolos que pueden utilizarse en el fichero de configuración, y que serán substituidos por su valor. Me explico mejor con un ejemplo: la opción "path = /tmp/%U" será interpretada como "path = /tmp/ana" si la usuaria que accede al recurso es "ana". Aquí hay algunas substitutciones interesantes:

  - %U   Usuario que inició sesión en el cliente

  - %G   Grupo del usuario que inició sesión en el cliente

  - %h   Nombre de host del servidor Samba

  - %M   Nombre de host del cliente Samba

  - %L   Nombre de NetBIOS del servidor Samba

  - %m   Nombre de NetBIOS del cliente Samba

  - %i   IP del servidor Samba

  - %I   IP del cliente Samba

  - %T   Fecha y hora

  - %D   Nombre del dominio o grupo de trabajo


___



PERMISOS DE LAS CARPETAS COMPARTIDAS SAMBA
------------------------------------------

Toda operación de escritura que realiza un cliente en la carpeta compartida, se hace como usuario nobody y grupo nogroup. Por ello la carpeta que se comparte debe tener propietario y permisos adecuados. Por ejemplo:

    $ sudo chown nobody:nogroup -R /carpeta_a_compartir
    $ sudo chmod 777 -R /carpeta_a_compartir

Hay que comprobar que el usuario nobody y el grupo nogroup tenga el mismo UID y GID tanto en el servidor como en el cliente.


___



USUARIOS Y SEGURIDAD EN SAMBA
-----------------------------

Cada usuario Samba necesita una cuenta en el servidor. Primero se deben crear las cuentas Linux, y luego necesitamos registrar el usuario en la base de datos de Samba.

El paso de Linux se realiza de la forma normal, como por ejemplo utilizando el comando adduser.

Para agregar un usuario existente a la base de datos de Samba ejecutamos el comando smbpasswd, que pedirá la contraseña Samba de forma interactiva. Concretamente:

  - Añadir usuario a Samba:        `$ smbpasswd -a usuario`

  - Eliminar usuario de Samba:     `$ smbpasswd -x usuario`

  - Desactivar usuario de Samba:   `$ smbpasswd -d usuario`

  - Reactivar usuario de Samba:    `$ smbpasswd -e usuario`

  - Borrar contraseña de Samba:    `$ smbpasswd -n usuario`

Los usuarios y contraseñas se guardan en la base de datos SAM. Para listar los usuarios de Samba debes ejecutar el comando:

    $ pdbedit -w -L

Para gestionar la seguridad, en el fichero de configuración mira las opciones:

  security , map_to_guest , create mask , read list , write list


___



INSTALAR Y CONFIGURAR EL CLIENTE SAMBA
--------------------------------------

El cliente SAMBA viene instalado por defecto en casi todas las distribuciones Linux. Por si acaso:

    $ sudo apt update
    $ sudo apt install smbclient cifs-utils

En una instalación de Linux con escritorio, en el navegador de ficheros podremos acceder a carpetas compartidas escribiendo (normalmente se activa con CTRL+L) la dirección smb://SERVIDOR/ o smb://SERVIDOR/RECURSO

Sin embargo, si des del terminal de Linux necesitamos conectar con un servidor, nos serán útil los siguientes comandos:

  - Para ver todas las máquinas y sus recursos:

        $ smbtree -N

  - Para ver todos los dominios disponibles:

        $ smbtree -D

  - Para buscar master browsers:

        $ nmblookup -M -

  - Se conecta a un servidor para ver los recursos compartidos listables ("browseable"):

        $ smbclient -L //SERVIDOR/ -U usuario -N

    Este último comando nos deja conectados al servidor y aparece una "shell" de Samba que nos permite interactuar con el servidor y que acepta todos los comandos típicos de FTP: cd, del, rm, dir, ls, get, lcd, mget, mkdir, md, mput, put, rmdir, rd, exit, quit, etc.

Y en Windows des del terminal podemos conectar con un servidor con el comando NET USE

Podemos montar las carpetas compartidas manualmente con el comando mount:

    $ sudo mount -t cifs -o rw,nosuid,noexec,credentials=/etc/smb-credentials //servidor/carpeta_compartida /punto_de_montaje

donde /etc/smb-credentials es un fichero que contiene usuarios y contraseñas, protegido contra lectura por usuarios, con el siguiente formato:

    username = usuario
    password = contraseña

Si queremos montarlas cada vez que inicie el equipo, entonces debemos añadir la línea al fichero /etc/fstab :

    //servidor/carpeta_compartida   /punto_de_montaje   cifs   rw,nosuid,noexec,credentials=/etc/smb-credentials   0   0

La opción (ver comandos "man mount" y "man mount.cifs"):

  - rw indica que se monta el directorio en modo de escritura, a diferencia de la opción ro.

  - nosuid ignora los bits setuid o setgid de los programas en la carpeta compartida.

  - noexec prohíbe ejecutar los programas en la carpeta compartida.

  - hard hace que si se pierde la conexión cuando intentábamos copiar un fichero en la carpeta compartida, se vuelve a iniciar la copia del fichero cuando el servidor se encuentra de nuevo activo.

  - intr evita que las aplicaciones se queden colgadas cuando intentan escribir en una carpeta que no está activa.


___



APRENDER MÁS SOBRE SAMBA
------------------------

  - <https://wiki.samba.org/index.php/User_Documentation>

  - <https://www.samba.org/samba/docs/current/man-html/>

  - <https://www.howtoforge.com/tutorial/samba-server-ubuntu-16-04/>

  - <https://www.howtoforge.com/tutorial/debian-samba-server/>


___



NAS
---

También puedes compartir carpetas con SMB, NFS o FTP instalando un NAS en la red y gestionándolo remotamente desde su interfaz web:

  - FreeNAS es un NAS bastante profesional, completo y que sigue un gran ritmo de desarrollo. Basado en FreeBSD.

  - NAS4Free es un NAS más sencillo, también basado en FreeBSD.

  - OpenMediaVault es un NAS también más sencillo, basado en Linux Debian. Dado que en clase trabajamos con Ubuntu Server, es el que te recomiendo para una práctica

    <https://www.howtoforge.com/tutorial/install-open-media-vault-nas/>


___



WEBMIN
------

Webmin es una interfaz web que te permite gestionar remotamente todos los aspectos de un servidor. Para ello se instala en el servidor la interfaz principal, y después los distintos módulos que extienden dicha interfaz para cada uno de los servicios que quieres controlar. Webmin necesitará tener instalado un servidor web y PHP.

Edita el fichero de repositorios de software:

    $ sudo nano /etc/apt/sources.list

Y añade la siguiente línea al final del fichero:

    deb http://download.webmin.com/download/repository sarge contrib

Y a continuación en la línea de comandos ejecuta:

    $ wget http://www.webmin.com/jcameron-key.asc
    $ sudo apt-key add jcameron-key.asc
    $ sudo apt update
    $ sudo apt install webmin

Ahora ya puedes acceder des de un navegador con la URL https://ip_servidor:10000/ , con usuario root y su contraseña en el sistema. En los menús "Webmin -> Un-used modules -> Samba windows file sharing" y "Webmin -> Servers -> Samba windows file sharing" puedes configurar y administrar Samba.

Para profundizar, lee estas referencias:

  - <https://www.digitalocean.com/community/tutorials/how-to-install-webmin-on-ubuntu-16-04>
  - <https://doxfer.webmin.com/Webmin/Samba_Windows_File_Sharing>


___



EXERCICI 1 WINDOWS: PERMISOS
--------------------------------------

Lliureu un document amb captures de pantalla d'aquests apartats:

1) Utilitzant una màquina virtual amb Windows del centre (-que no cal que sigui un server-), afegiu un segon disc i formategeu-lo amb el sistema de fitxers NTFS i assigneu-hi el nom de "documents" i la lletra X:

2) Doneu d'alta en la màquina virtual els grups anomenats professorsIAM i estudiantsIAM, amb un usuari cadascun.

3) Creeu en la partició de documents els següents directoris:

   X:\treball\docents\professor  
   X:\treball\usuaris\estudiant  
   X:\treball\global

4) Assigneu a aquests directoris els permisos següents:

   - Els usuaris del grup professorsIAM han de poder-ho fer tot als directoris X:\treball\docents\professor i X:\treball\global

   - Els usuaris del grup professorsIAM només han de poder llegir el contingut del directori X:\treball\usuaris\estudiant

   - Els usuaris del grup estudiantsIAM han de poder-ho fer tot al directori X:\treball\usuaris\estudiant i al directori X:\treball\global

   - Els usuaris del grup estudiantsIAM no ha de poder fer res al directori X:\treball\docents\professor

   I comproveu el resultat d'aquestes accions.


___



EXERCICI 2 WINDOWS: COMPARTICIÓ DE CARPETES A UN GRUP DE TREBALL
----------------------------------------------------------------

Lliureu un document amb captures de pantalla d'aquests apartats:

1) Utilitzeu dues màquines virtuals amb Windows del centre (-que no cal que sigui un server-), que posareu en xarxa, tant a VirtualBox, com proporcionant adreces IP compatibles. Comproveu que podeu fer ping d'una a l'altre. Si no podeu fer ping i, aparentment, tot és correcte, desactiveu el tallafocs de Windows.

2) A les propietats de sistema, escolliu "Treball en grup", enlloc de "Domini". Com a nom del grup de treball a les dues màquines, escolliu AULA1.

3) Visualitzeu a l'"entorn de xarxa" el grup de treball creat, identificant els noms dels equips que el formen.

4) Crea a un dels equips una carpeta anomenada CARPERTA_A, i a l'altre equip una carpeta anomenada CARPETA_B

5) Compartiu el recurs CARPETA_A de la primera màquina de tal manera que des de la segona màquina virtual s'hi pugui fer tot. Proveu-lo.

6) Compartiu el recurs CARPETA_B de la segona màquina de tal manera que des de la primera màquina virtual només es pugui llegir el contingut de la carpeta. Proveu-lo.

7) Crea una unitat de xarxa anomenada Z: en la segona màquina corresponent al recurs compartit CARPETA_A de la primera màquina.


___



EXERCICI 3 WINDOWS: COMPARTICIÓ DE CARPETES A UN DOMINI
-------------------------------------------------------

Lliureu un document amb captures de pantalla d'aquests apartats:

1) Utilitzeu dues màquines virtuals amb Windows, una configurada com un servidor controlador de domini amb Windows Server, i l'altre serà un client de Windows del centre que haureu posat dins del domini. El nom del domini serà "elvostrenom". La resta de paràmetres són de lliure elecció.

2) Doneu d'alta al servidor controlador del domini els grups anomenats professorsSMX i estudiantsSMX, amb un usuari cadascun.

3) Creeu la carpeta C:\GLOBAL al servidor, que compartireu amb l'eina de gestionar comparticions del servidor.

4) Assigneu a aquest directori els permisos següents:

   - Els usuaris del grup professorsSMX han de poder-ho fer tot.

   - Els usuaris del grup estudiantsSMX només han de poder llegir el contingut del directori.

5) Comproveu-ho accedint amb els usuaris des de la màquina client.


___



EJERCICIO 1 LINUX
-----------------

  1) Instala Samba.

  2) Da de alta los siguientes usuarios de Samba: jefe, empleado1, empleado2.

  3) Crea las carpetas /datos/proyectos y /datos/programas

  4) Comparte la carpeta Proyectos para que el usuario jefe tenga permisos de escritura y el resto de usuarios permisos de lectura.

  5) Comparte la carpeta Programas para que todos los usuarios tengan permisos de escritura.

  6) Desde un equipo cliente accede a los recursos compartidos del servidor y comprueba el correcto funcionamiento del sistema.

  7) Configura el equipo cliente para que el recurso compartido Programas se monte automáticamente en la unidad Z:


___



SOLUCIÓN
--------

    sudo apt update
    sudo apt install samba

    sudo adduser jefe
    sudo adduser empleado1
    sudo adduser empleado2

    sudo smbpasswd -a jefe
    sudo smbpasswd -a empleado1
    sudo smbpasswd -a empleado2
    sudo pdbedit -L

    sudo mkdir /datos
    sudo mkdir /datos/proyectos
    sudo mkdir /datos/programas
    sudo chmod 777 /datos -R

    sudo nano /etc/samba/smb.conf

      [Global]
      server role = standalone
      netbios name =  PRUEBA
      workgroup = SAMBALENTIN
      security = user

      [Proyectos]
      path = /datos/proyectos
      read list = empleado1 empleado2
      write list = jefe

      [Programas]
      path = /datos/programas
      write list = jefe empleado1 empleado2

    sudo systemctl restart smbd.service nmbd.service


___



EJERCICIO 2 LINUX
-----------------

Configura el servidor Samba, editando el fichero de configuración con los siguientes parámetros:

  1) Crea un grupo de trabajo llamado RUMBA.

  2) Tu servidor se verá en la red con el nombre RUMBERO.

  3) La seguridad se controlará a escala de usuario.

  4) El usuario con una contraseña incorrecta será rechazado, pero si el usuario no existe pasará a ser el usuario invitado.

  5) Deniega el acceso a todas las máquinas de la red que comiencen por 10.0.

  6) Deniega el acceso a los usuarios "pere" y "joan" y al grupo "salseros".

  7) Crea un recurso compartido llamado BALL, al cual asignarás el directorio /home/ball, que estará disponible para todos los usuarios y invitados, y además de acceder podrán también escribir.

  8) Crea un recurso compartido llamado CASA, al cual sólo podrán acceder los usuarios del grupo "rumba", pero no podrán escribir. El directorio asignado será /home/casa.

  9) Comparte el CD-ROM con todos los usuarios que tengan acceso al sistema.

  10) Comparte una impresora virtual llamada RUM con los usuarios que pertenecen al grupo "escritores".


___



SOLUCIÓN
--------

    $ sudo nano /etc/samba/smb.conf

      workgroup = RUMBA
      netbios name = RUMBERO
      security = user
      server role = standalone server
      host deny = 10.0
      invalid users = pere, joan, @salseros

      [BALL]
      path = /home/ball
      read only = no
      guest ok = yes
      browseable = yes

      [CASA]
      path = /home/casa
      read only = yes
      guest ok = no
      browseable = yes
      valid users = @rumba

      [CDROM]
      path = /media/cdrom
      guest ok = yes
      browseable = yes

      [RUM]
      path = /var/spool/samba
      guest ok = no
      browseable = yes
      valid users = @escritores
      printable = yes

    $ sudo useradd -M -s /usr/sbin/nologin pere
    $ sudo useradd -M -s /usr/sbin/nologin joan
    $ sudo addgroup salseros
    $ sudo addgroup rumba
    $ sudo addgroup escritores

    $ sudo mkdir -p /home/ball
    $ sudo chmod 1777 /home/ball

    $ sudo mkdir -p /home/casa
    $ sudo chmod 1777 /home/casa

    $ sudo mkdir -p /media/cdrom
    $ sudo chmod 1777 /media/cdrom

    $ sudo useradd -M -s /usr/sbin/nologin s_joan -g salseros
    $ sudo useradd -M -s /usr/sbin/nologin s_pere -g salseros
    $ sudo useradd -M -s /usr/sbin/nologin r_joan -g rumba
    $ sudo useradd -M -s /usr/sbin/nologin r_pere -g rumba
    $ sudo useradd -M -s /usr/sbin/nologin e_joan -g escritores
    $ sudo useradd -M -s /usr/sbin/nologin e_pere -g escritores

    $ sudo for username in joan pere s_joan s_pere r_joan r_pere e_joan e_pere;
        do (echo "12345678"; echo "12345678") | /usr/bin/smbpasswd -s -a $username;
        done

    $ smbclient //127.0.0.1/BALL -U joan
    $ smbclient //127.0.0.1/BALL -U pere
    $ smbclient //127.0.0.1/BALL -U s_joan
    $ smbclient //127.0.0.1/BALL -U s_pere

    $ smbclient //127.0.0.1/BALL -U ausias
      smb: \> put smb.conf

    $ smbclient //127.0.0.1/CASA -U ausias
    $ smbclient //127.0.0.1/CASA -U s_joan
    $ smbclient //127.0.0.1/CASA -U r_joan

    $ smbclient //127.0.0.1/CDROM -U r_joan
    $ smbclient //127.0.0.1/CDROM -U ausiasa

    $ smbclient //127.0.0.1/RUM -U ausias
    $ smbclient //127.0.0.1/RUM -U e_joan

