% Title:   RAID en Linux  
% Version: 1.2  
% Author:  Alejandro Castán Salinas  
% Email:   acastan@xtec.cat


---


Este texto trata de resumir el proceso de creación de RAIDs software en Linux (Ubuntu 16.04) des de la línea de comandos, pero al final del documento dedico un apartado a la creación de RAID gráficamente con un módulo de Webmin.

Donde digo “disco” se podría decir “partición”. En la creación de RAID por software en Linux no estamos obligados a utilizar discos enteros para el RAID. Podemos utilizar particiones para crear el RAID, mientras otras particiones del mismo disco se utilizan para otras cosas.

Bibliografía que deberías leer:

  * <https://en.wikipedia.org/wiki/RAID>
  * <https://wiki.archlinux.org/index.php/RAID>
  * <https://raid.wiki.kernel.org/index.php/RAID_setup>
  * <http://www.tldp.org/HOWTO/Software-RAID-HOWTO.html>

{toc}


---


PREVIOS
-------

Muchos de los comandos necesitarán permisos de administrador. Para no tener que recurrir a sudo en cada comando, cambiamos de usuario a administrador, pero deberemos tener cuidado con lo que hagamos:

    $ sudo su

Necesitamos un núcleo que soporte RAID. Si hemos utilizado Ubuntu Server seguro que es así. Comprobemos si tiene los controladores instalados con:

    # lsmod | grep raid

Si los controladores no están cargados, instalamos los que necesitemos con:

    # modprobe raid0
    # modprobe raid1
    # modprobe raid10
    # modprobe raid456

Instalamos la herramienta de gestión de RAID, si fuera necesario:

    # apt install mdadm

El fichero de configuración del RAID estará en `/etc/mdadm/mdadm.conf`

Y podremos consultar el estado del RAID visualizando el fichero `/proc/mdstat`

Estudia los diversos  modos de operación de mdadm: crear, ensamblar, monitorizar, construir, crecer, manejar, varios.

    $ man mdadm
    $ man 4 md


---


PARTICIONAR LOS DISPOSITIVOS
----------------------------

Si el disco o partición ya se utilizó en otro RAID, entonces debemos sobreescribir el superbloque:

    # mdadm --misc --zero-superblock /dev/<disco>
    # mdadm --misc --zero-superblock /dev/<partición>

Se puede llegar a crear el RAID directamente sobre discos “crudos”, sin particionar. Eso es poco recomendable, ya que será más difícil cambiarlos en caso de fallo de disco. Lo mejor es particionar dejando además un pequeño espacio libre al final por el siguiente motivo:

  > “When replacing a failed disk of a RAID, the new disk has to be exactly the same size as the failed disk or bigger, otherwise the array recreation process will not work. Even hard drives of the same manufacturer and model can have small size differences. By leaving a little space at the end of the disk unallocated one can compensate for the size differences between drives, which makes choosing a replacement drive model easier. Therefore, it is good practice to leave about 100 MB of unallocated space at the end of the disk.”

Crearemos la tabla de partición. Se recomienda GPT. Una vez particionado, como tipo de partición debemos asignarle el código FD00. Pero si habíamos escogido una tabla de particiones MBR, entonces al tipo de partición debemos asignarle el código 0xDA. Podemos crear particiones con

    # cfdisk /dev/<disco>   →   GPT   →   Linux RAID   →   escribir

Si queremos comprobar que dispositivos tenemos:

    # lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT


---


CONSTRUIR EL RAID
-----------------

He aquí unos ejemplos.

  * Ejemplo para construir un RAID0 con el segundo y tercer disco:

        # mdadm --create --verbose /dev/md0 --level=0 --metadata=1.2 --raid-devices=2 /dev/sdb1 /dev/sdc1

  * Ejemplo para construir un RAID1 con el segundo y tercer disco:

        # mdadm --create --verbose /dev/md0 --level=1 --metadata=1.2 --raid-devices=2 /dev/sdb1 /dev/sdc1

  * Ejemplo para construir un RAID5 con tres discos activos más uno de repuesto:

        # mdadm --create --verbose /dev/md0 --level=5 --metadata=1.2 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1 --spare-devices=1 /dev/sde1

  * Ejemplo para construir un RAID10 con dos dispositivos ([far2](https://en.wikipedia.org/wiki/Non-standard_RAID_levels#Linux_MD_RAID_10)):

        # mdadm --create --verbose /dev/md0 --level=10 --metadata=1.2 --chunk=512 --raid-devices=2 --layout=f2 /dev/sdb1 /dev/sdc1

El RAID se crea como dispositivo virtual /dev/md0, ya ensamblado y preparado para usar. Podemos esperar a que mdadm sincronice el RAID, o comenzar a usarlo en modo degradado mientras mdadm lo sincroniza en segundo plano. Restaurar la paridad puede llevar mucho rato, pero puedes consultar el progreso con:

    # cat /proc/mdstat

Una vez creado el RAID debemos guardar la configuración:

    # mdadm --detail --scan >> /etc/mdadm/mdadm.conf

Puedes consultar información breve o detallada del RAID, respectivamente, con:

    # mdadm -Q /dev/md0
    # mdadm -D /dev/md0


---


ENSAMBLAR Y UTILIZAR EL RAID
----------------------------

Para utilizar el RAID, siempre se debe “ensamblar” antes:

    # mdadm --assemble --scan

A continuación el RAID se debe formatear como cualquier otro disco:

    # mkfs -t ext4 /dev/md0

Pero para el rendimiento óptimo del RAID, se debe crear con el tamaño de “chunk” correcto, y se debe formatear calculando los tamaños de “stripe” y “stride” correctos. Por favor, lee:

  * <https://raid.wiki.kernel.org/index.php/RAID_setup#Chunk_sizes>
  * <http://www.zdnet.com/article/chunks-the-hidden-key-to-raid-performance/>

El tamaño del chunk escogido, lo puedes recordar con:

    # mdadm --detail /dev/md0 | grep 'Chunk Size'

  * Ejemplo RAID0:

    Hipotético RAID0 compuesto por 2 discos físicos.  
    El tamaño de chunk es 64 KB y el tamaño de bloque es 4 KB.  
    stride = tamaño chunk / tamaño bloque = 64/4 = 16  
    stripe = # discos físicos de datos * stride = 2*16 = 32

        # mkfs.ext4 -v -L miRAID -m 0.5 -b 4096 -E stride=16,stripe-width=32 /dev/md0

  * Ejemplo RAID5:

    Hipotético RAID5 compuesto por 4 discos físicos: 3 discos de datos y 1 disco de paridad 1.  
    El tamaño de chunk es 512 KB y el tamaño de bloque es 4 KB.  
    stride = tamaño chunk / tamaño bloque = 512/4 = 128  
    stripe = # discos físicos de datos * stride = 3*128 = 384.

        # mkfs.ext4 -v -L miRAID -m 0.01 -b 4096 -E stride=128,stripe-width=384 /dev/md0

  * Ejemplo RAID10,far2:

    Hipotético RAID10 compuesto por 2 discos físicos. A causa de las propiedades de RAID10 en far2 layout, ambos cuentan como discos de datos.  
    El tamaño de chunk es 512 KB y el tamaño de bloque es 4 KB.  
    stride = tamaño chunk / tamaño bloque = 512/4 = 128  
    stripe = # discos físicos de datos * stride = 2*128 = 256

        # mkfs.ext4 -v -L miRAID -m 0.01 -b 4096 -E stride=128,stripe-width=256 /dev/md0

A continuación lo añadimos al sistema de ficheros, y probamos que monte:

    # mkdir /dir
    # echo "/dev/md0  /dir  ext4  defaults  0  2" >> /etc/fstab
    # mount -a
    # mount /dev/md0


---


QUITAR DISCOS DEL RAID
----------------------

Para quitar un disco del RAID primero lo marcamos como defectuoso:

    # mdadm --fail /dev/md0 /dev/sdxy

Y a continuación lo quitamos del RAID:

    # mdadm --remove /dev/md0 /dev/sdxy

Si queremos quitarlo para siempre, por ejemplo para utilizarlo en otras cosas, además de los dos comandos anteriores también eliminaremos el superbloque:

    # mdadm --zero-superblock /dev/md0 /dev/sdxy

Para dejar de utilizar todo el RAID debemos:

  * Desmontar el RAID con:   `# umount /dev/md0`

  * Parar el RAID con:   `# mdadm --stop /dev/md0`

  * Repetir los tres comandos descritos al inicio de esta sección, para cada uno de los discos del RAID.

  * Borrar la configuración del RAID del fichero `/etc/mdadm.conf`

  * Si fuera necesario, borrar también el punto de montaje del RAID del fichero `/etc/fstab`


---


AÑADIR DISCOS AL RAID
---------------------

Se pueden añadir nuevos discos al RAID con mdadm sobre la marcha, sin parar el sistema ni el RAID. Debes particionar el nuevo disco con las mismas características de los otros dispositivos que ya forman el RAID.

Suponiendo que el RAID ya estaba ensamblado y montado, añade el nuevo disco, visualiza el progreso, y compruébalo, respactivamente con:

    # mdadm --add /dev/md0 /dev/sdxy
    # cat /proc/mdstat
    # mdadm --misc --detail /dev/md0


---


INCREMENTAR EL TAMAÑO DEL RAID
------------------------------

If larger disks are installed in a RAID array or partition size has been increased, it may be desirable to increase the size of the RAID volume to fill the larger available space. This process may be begun by first following the above sections pertaining to replacing disks. Once the RAID volume has been rebuilt onto the larger disks it must be "grown" to fill the space.

    # mdadm --grow /dev/md0 --size=max

Next, partitions present on the RAID volume /dev/md0 may need to be resized. See Partitioning for details. Finally, the filesystem on the above mentioned partition will need to be resized. If partitioning was performed with GParted this will be done automatically. If other tools were used, unmount and then resize the filesystem manually.

    # umount /dev/md0
    # fsck.ext4 -f /dev/md0
    # resize2fs /dev/md0


---


HERRAMIENTAS GRÁFICAS
---------------------

El programa GParted tan sólo nos permite visualizar RAIDs, pero no crearlos.

El gestor de contenidos Webmin tiene un módulo de RAID. Mira como se instala y se utiliza:

  * <https://www.digitalocean.com/community/tutorials/how-to-install-webmin-on-ubuntu-16-04>
  * <https://doxfer.webmin.com/Webmin/Linux_RAID>
  * <https://www.youtube.com/watch?v=Y4MIWzLwZy8>

