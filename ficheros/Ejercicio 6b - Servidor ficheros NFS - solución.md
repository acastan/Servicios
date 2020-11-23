TEORIA
------

NFS (Network File System) es un protocolo de transferencia de ficheros, típico en sistemas Unix. Utiliza el puerto UDP/TCP 2049.

Existen varias versiones. Todo el mundo debería utilizar la última: NFSv4.

Un escenario típico de uso es una red local donde los usuarios tienen su carpeta personal /home en un ordenador remoto accesible desde cualquier ordenador de la red, de tal manera que pueden “loggearse” en cualquier ordenador de la red teniendo siempre disponible su perfil personal.

El protocolo NFS en su versión 4 soporta autentificación y cifrado. Si no se usan éstos, tiene que restringirse a la utilización en una red local de confianza puesto que: un sniffer puede interceptar los datos que circulan por la red; y los permisos de acceso se conceden en función de la dirección IP del cliente, que puede ser suplantada. Medidas de seguridad que debemos tomar: cortafuegos prohibiendo IP spoofing, y autentificación con Kerberos. 

El servicio NFS utiliza RPC (llamada a procedimiento remoto o «Remote Procedure Call»), que es un estándar Unix para servicios remotos. Los servicios RPC se registran en un directorio conocido como portmapper («asociador de puertos»). Un cliente que desee realizar una consulta NFS primero debe dirigirse al portmapper (en el puerto 111, TCP o UDP) y preguntar por el servidor NFS. La respuesta generalmente mencionará el puerto 2049, que es el predeterminado para NFS, aunque no todos los servicios RPC utilizan un puerto fijo necesariamente. 


___



INSTALAR Y CONFIGURAR EL SERVIDOR
---------------------------------

Para instalar el servidor:

    $ sudo apt update
    $ sudo apt install nfs-kernel-server

Para iniciar el servidor, si hiciera falta:

    $ sudo systemctl start nfs-kernel-server.service
    $ sudo systemctl status nfs-kernel-server.service

El archivo de configuración del servidor NFS, /etc/exports, enumera los directorios que estarán disponibles en la red (exportados). Para cada espacio compartido NFS, sólo tendrán acceso las máquinas especificadas.

    /directorio_a_compartir maquina1(opcion1,opcion2,...) maquina2(...) ...

Puede identificar cada máquina mediante su nombre DNS o su dirección IP. También puede especificar conjuntos completos de máquinas utilizando una sintaxis como *.iam.cat o un rango de direcciones IP 192.168.0.0/255.255.255.0 o 192.168.0.0/24.

Como opción, lo más común es poner los permisos del directorio a compartir, que serán ro (sólo lectura) o rw (lectura y escritura). Por ejemplo, compartiremos la carpeta apuntes con permisos de lectura para los ordenadores de los alumnos del aula 1 y con permisos de escritura para el ordenador del profesor, y la carpeta trabajos con permisos de escritura para todos los ordenadores:

    /exports/apuntes   192.168.201.0/24(ro) h1-0(rw)
    /exports/trabajos   *(rw)

Otras opciones interesantes:

  - Los clientes NFS típicamente se conectan desde un puerto restringido sólo a root (menor a 1024). Puedes eliminar esta restricción con la opción insecure (la opción secure es implícita, pero puedes hacerla explícita para más claridad).

  - De forma predeterminada, el servidor sólo responde a peticiones NFS cuando se completa la operación actual de disco (la opción sync). Puedes desactivar esta funcionalidad con la opción async.

  - La opción sec precisa el nivel de seguridad deseado: sec=sys es el valor predeterminado sin ningún tipo de seguridad particular, sec=krb5 habilita únicamente la autenticación, sec=krb5i añade una protección de integridad y sec=krb5p incluye protección de la confidencialidad mediante el cifrado de datos. Para que todo esto funcione es necesaria la instalación de Kerberos (ver https://help.ubuntu.com/community/NFSv4Howto).

  - La opción root_squash evita que los usuarios con privilegios administrativos los mantengan sobre la carpeta compartida cuando se conectan remotamente. Es la opción predeterminada. no_root_squash es la opción contraria.

Después de modificar el fichero de carpetas compartidas hay que reiniciar el servidor:

    $ sudo exportfs -a
    $ sudo systemctl restart nfs-kernel-server.service
    $ sudo tail /var/log/syslog


___



PERMISOS DE LAS CARPETAS COMPARTIDAS
------------------------------------

Toda operación de escritura que realiza un cliente en la carpeta compartida, se hace como usuario nobody y grupo nogroup. Por ello la carpeta que se comparte debe tener propietario y permisos adecuados:

    $ sudo chown nobody:nogroup -R /carpeta_a_compartir
    $ sudo chmod 777 -R /carpeta_a_compartir

Hay que comprobar que el usuario nobody y el grupo nogroup tenga el mismo UID y GID tanto en el servidor como en el cliente.


___



INSTALAR Y CONFIGURAR EL CLIENTE
--------------------------------

Para instalar el cliente:

    $ sudo apt update
    $ sudo apt install nfs-common

Podemos montar las carpetas compartidas manualmente con el comando mount:

    $ sudo mount -t nfs4 -o rw,nosuid,noexec,hard,intr servidor:/carpeta_compartida /punto_de_montaje

Si queremos montarlas cada vez que inicie el equipo, entonces debemos añadir la línea al fichero /etc/fstab :

    servidor:/carpeta_compartida   /punto_de_montaje   nfs4   rw,nosuid,noexec,hard,intr   0   0

Creo (-no estoy seguro-) que en NFSv4 todos los directorios a exportar implícitamente están en /exports. Esto quiere decir que en la línea anterior /carpeta_compartida está realmente en /exports/carpeta_compartida

La opción (ver comandos "man mount" , "man mount.nfs" y "man nfs"):

  - rw indica que se monta el directorio en modo de escritura, a diferencia de la opción ro.

  - nosuid ignora los bits setuid o setgid de los programas en la carpeta compartida.

  - noexec prohíbe ejecutar los programas en la carpeta compartida.

  - hard hace que si se pierde la conexión cuando intentábamos copiar un fichero en la carpeta compartida, se vuelve a iniciar la copia del fichero cuando el servidor se encuentra de nuevo activo.

  - intr evita que las aplicaciones se queden colgadas cuando intentan escribir en una carpeta que no está activa.


___



WINDOWS
-------

Windows proporciona un servidor NFS en sus versiones Server.

Windows proporciona un cliente NFS en sus versiones Enterprise. Si queremos un cliente gratuito, aquí hay uno:

  <https://code.google.com/archive/p/nekodrive/downloads>


___



APRENDER MÁS
------------

<https://www.howtoforge.com/how-to-configure-a-nfs-server-and-mount-nfs-shares-on-ubuntu-14.04>


___



EJERCICIO
---------

Implementa una red con dos máquinas virtuales que permita compartir recursos utilitzando el sistema NFS. Las características que deben cumplir los equipos son las seguientes:

  - Máquina IAM1 con servidor NFS compartirá estos recursos:  

    /nfs/carpeta1 (lectura y escritura)

    /nfs/carpeta2 (lectura)
       
  - Màquina IAM2 con cliente NFS que accederá a los recursos.


___



SOLUCIÓN
--------

1) Instalar servidor NFS en IAM1

       $ sudo apt update
       $ sudo apt install nfs-kernel-server

2) Instalar cliente NFS en IAM2

       $ sudo apt update
       $ sudo apt install nfs-common

3) Activa el servicio NFS en IAM1 y compruébalo

       $ sudo systemctl start nfs-kernel-server.service
       $ sudo systemctl status nfs-kernel-server.service portmap.service

4) Crea en IAM1 las carpetas a compartir y da los permisos adecuados

       $ sudo mkdir -p /nfs/carpeta1
       $ sudo mkdir -p /nfs/carpeta2
       $ sudo chmod 777 /nfs/carpeta1
       $ sudo chmod 777 /nfs/carpeta2
       $ ls -l /nfs

5) Configura el fichero /etc/exports en IAM1 para compartir las carpetas

       $ sudo nano /etc/exports

         /nfs/carpeta1   IP_IAM2(rw)
         /nfs/carpeta2   IP_IAM2(ro)

       $ sudo exportfs -ra
       $ sudo showmount -e

6) Accedemos des de IAM2 al recurso /nfs/carpeta1 y hacemos pruebas

       $ sudo mount -t nfs IP_IAM1:/nfs/carpeta1 /mnt
       $ cd /mnt
       $ mkdir prova
       $ ls -l
       $ cd /
       $ sudo umount /mnt

7) Accedemos des de IAM2 al recurso /nfs/carpeta2 y hacemos pruebas

       $ sudo mount -t nfs IP_IAM1:/nfs/carpeta2 /mnt
       $ cd /mnt
       $ mkdir prova
       $ ls -l
       $ cd /
       $ sudo umount /mnt

8) Configura el fichero /etc/fstab de IAM2 para que el montage sea automàtico

       $ sudo mkdir -p /mnt/nfs1
       $ sudo mkdir -p /mnt/nfs2
       $ sudo nano /etc/fstab

         IP_IAM1:/nfs/carpeta1   /mnt/nfs1   nfs   rw   0   0
         IP_IAM1:/nfs/carpeta2   /mnt/nfs2   nfs   ro   0   0

       $ sudo mount -a
       $ ls -l /mnt/nfs1
       $ ls -l /mnt/nfs2

