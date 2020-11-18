Instalación de Linux
--------------------

Como distribución de Linux para servidores escoge una que sea muy estable y que proporcione actualizaciones de seguridad durante tres años o más. Recomiendo Debian Estable, Ubuntu Server LTS y CentOS. En este manual yo utilizaré Ubuntu Server.

Encontrarás unos detallados tutoriales para la instalación en:

  - <https://www.howtoforge.com/tutorial/perfect-server-ubuntu-20.04-with-apache-php-myqsl-pureftpd-bind-postfix-doveot-and-ispconfig/>

  - <https://www.howtoforge.com/perfect-server-debian-10-buster-apache-bind-dovecot-ispconfig-3-1/>

  - <https://www.howtoforge.com/tutorial/perfect-server-centos-8-apache-mysql-php-pureftpd-postfix-dovecot-and-ispconfig/>

Tan sólo instalaremos el sistema base y los servicios. Un servidor no necesita entorno gráfico.

01. Si una vez instalado necesitas cambiar la configuración de la red

    a) En caso de trabajar con Debian 10 edita el siguiente fichero:

        sudo nano /etc/network/interfaces

    En dicho fichero la configuración para nuestra red virtual podría ser, por ejemplo:

        auto enp0s3
        iface enp0s3 inet static
            address 192.168.201.tu_IP_real+50
            netmask 255.255.255.0
            gateway 192.168.201.1
            dns-nameservers 8.8.8.8

        auto enp0s8
        iface enp0s8 inet dhcp

    y a continuación reinicia la red:

        sudo systemctl restart networking

    b) En caso de trabajar con Ubuntu server 18.04 o superiores, edita el siguiente fichero:

        sudo nano /etc/netplan/50-cloud-init.yaml

    En dicho fichero la configuración para nuestra red virtual podría ser, por ejemplo:

        network:
          version: 2
          renderer: networkd
          ethernets:
            enp0s3:
              dhcp4: no
              dhcp6: no
              addresses: [192.168.201.tu_IP_real+50/24]
              gateway4: 192.168.201.1
              nameservers:
                addresses: [8.8.8.8]
            enp0s8:
              dhcp4: yes
              dhcp6: no

    y a continuación reinicia la red:

        sudo netplan apply

02. Una vez instalado manipularemos el fichero con las fuentes desde donde se instalan los programas:

        sudo nano /etc/apt/sources.list

    Las líneas que comienzan por `#` indican comentarios, las líneas que comienzan por `deb` son para descargar los programas ya compilados, las líneas que comienzan por `deb-src` son para descargar código fuente.

    Si queremos descargar software libre fuera del repositorio de Ubuntu añadiremos la palabra `universe`, y si queremos descargar software no libre (sin licencia GPL, como Java) añadiremos la palabra `multiverse`.

        deb http://es.archive.ubuntu.com/ubuntu/ focal           main restricted universe multiverse
        deb http://es.archive.ubuntu.com/ubuntu/ focal-updates   main restricted universe multiverse
        deb http://es.archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
        deb http://security.ubuntu.com/ubuntu/   focal-security  main restricted universe multiverse

    Si queremos descargar software libre fuera del repositorio de Debian añadiremos la palabra `contrib`, y si queremos descargar software no libre (sin licencia GPL, como Java) añadiremos la palabra `non-free`.

        deb http://ftp.es.debian.org/debian/             buster           main contrib non-free
        deb http://ftp.es.debian.org/debian/             buster-updates   main contrib non-free
        deb http://security.debian.org/debian-security   buster/updates   main contrib non-free

03. Ahora vamos a actualizar las listas de programas disponibles, y después de ello vamos a actualizar los programas que tenemos instalados:

        sudo apt update
        sudo apt upgrade

04. Si queremos instalar nuevos programas y no conocemos el nombre de los paquetes, podemos instalar `aptitude`. Una vez instalado, al ejecutarlo se nos abrirá un entorno en modo texto que nos permite navegar y buscar en las listas de programas. Al principio cuesta un poco, así que lee las combinaciones de teclas en la ayuda:

        sudo apt install aptitude
        sudo aptitude

05. Y para cambiar la opción de arranque por defecto, edita en el fichero de configuración de GRUB la opción `GRUB_DEFAULT`, que indica la línea por defecto en el menú de arranque, teniendo en cuenta que la primera línea es la 0:

        sudo nano /etc/default/grub
        sudo update-grub
        more /boot/grub/grub.cfg

06. Vamos a instalar un servidor de SSH para poder acceder a nuestro ordenador remotamente desde otros equipos:

        sudo apt install openssh-server

07. Opcionalmente podríamos instalar un sistema de cuotas de disco para que los ficheros de los usuarios no superen ciertos límites de espacio:

        sudo apt install quota

    Y edita el fichero `/etc/fstab` añadiendo `usrquota` y `grpquota` a las particiones que nos interese tener sistema de cuotas (aviso: dicho fichero seguramente será diferente en vuestro equipos, dependiendo de las particiones que tengáis).

        /dev/sda1     /                ext4     errors=remount-ro              0     1
        /dev/sda2     /home            ext4     defaults,usrquota,grpquota     0     2
        /dev/sda3     /var             ext4     defaults,usrquota,grpquota     0     2
        /dev/sda4     none             swap     sw                             0     0

    Remontaremos dichas particiones antes de activar el sistema de cuotas. Por último, editaremos las cuotas de los usuarios o grupos con el comando `edquota`. Ejecutamos:

        # Remontar particiones
        sudo mount -vo remount /home
        sudo mount -vo remount /var

        # Crea ficheros de quotas en el inicio de partición
        sudo quotacheck -avugm

        # Activa el sistema de quotas
        sudo quotaon –avug

        # Edita las quotas de un usuario
        sudo edquota usuario

        # Visualiza las quotas de un usuario y de las particiones
        sudo quota -u usuario
        sudo repquota -a

    Para aprender más sobre cuotas de disco en Linux:

      - <https://www.server-world.info/en/note?os=Ubuntu_16.04&p=quota>

      - <https://wiki.archlinux.org/index.php/disk_quota>

08. Opcionalmente (y nada recomendable en un servidor) podríamos instalar el sistema gráfico (X Window) o incluso un escritorio (LXDE, LXQT, XFCE, Gnome, MATE, KDE, ...):

        sudo apt install xorg
        sudo apt install lxqt-core
        sudo apt install xfce4
        sudo apt install mate-core
        sudo apt install gnome-core
        sudo apt install kde-baseapps

09. Por si quisiéramos descargar el código fuente de programas para posteriormente compilarlos, nos vendrá bien tener instaladas unas mínimas herramientas de programación:

        sudo apt install build-essential

10. Por último, por si quisiéramos administrar nuestro servidor remotamente a través de un navegador, faltaría añadir el repositorio de Webmin:

        sudo apt install gnupg
        sudo nano /etc/apt/sources.list

            deb https://download.webmin.com/download/repository sarge contrib

        wget -q http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add -
        sudo apt update
        sudo apt install webmin
        
    y ya puedes acceder a través de la URL https://tu_servidor:10000/
