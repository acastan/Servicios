LISTADO DE ARCHIVOS
-------------------

Estudia el comando ls.

 01. Lista recursivamente todos los archivos bajo el directorio /etc deteniendo el despliegue en cada pantalla.

         ls -R /etc | more

 02. Prueba otras opciones del comando ls usando el directorio /etc o /bin.

         ls -h -l -S /bin/b* | more

 03. Lista archivos visibles e invisibles bajo el directorio actual, en formato largo.

         ls -lA | more

 04. Interpreta las siguientes líneas de salida del formato largo de salida del comando ls:

     tipo de archivo, permisos, enlaces duros, propietario, tamaño, fecha de modificación, y nombre del archivo


___



REDIRECCION ENTRADA/SALIDA
--------------------------

 05. Sin editor de texto, mediante redirección, crea el archivo cap1 con el contenido “Este es el capítulo 1”. Repite con cap2 y cap3. Verifica mostrando cada uno con el comando cat.

         echo "este es el capitulo 1" > cap1
         cat cap1
         ...

 06. Añade al final de un archivo llamado libro el contenido de los archivos cap1, cap2 y cap3.

         cat cap1 cap2 cap3 >> libro

 07. Crea un archivo llamado amigotes que contiene las líneas del archivo /etc/passwd ordenadas en orden descendente utilizando el comando sort y redirección de entrada y salida.

         sort -r < /etc/passwd > amigotes

 08. Muestra las líneas del fichero amigotes que tienen la palabra home, filtrando el resto mediante el comando grep.

         cat amigotes | grep home

     o bien

         grep home amigotes


___



EDITOR DE TEXTO
---------------

 09. Invócalo escribiendo vi o nano. Interpreta la ayuda y experimenta con él creando y modificando textos breves. ¿Cuál es la combinación de teclas para borrar toda una línea? ¿ Cuál es la combinación de teclas para cortar-copiar-pegar?

     vi → Modo de comandos, insertar, reemplazar, dd, :w , :q , :wq , :q!

     nano → ctrl+O , ctrl+X , ctrl+K ,  ctrl+U ,  ctrl+Q

 10. Crea en tu directorio personal con el procesador de textos una carta a un amigo. A la carta llámala micarta.txt.

     ...


___



SISTEMA DE ARCHIVOS
-------------------

 11. Trasládate al directorio doc, dentro del directorio usr, dentro del directorio raíz. Muestra el directorio actual y los archivos contenidos en él.

         cd /usr/bin
         ls | more

 12. Trasládate al directorio propio del usuario desde cualquier otro directorio.

         cd ~

     o bien

         cd

     o bien

         cd $HOME

 13. Crea un directorio que se llame amigos dentro de tu directorio personal, de forma que cuando listes los contenidos con el comando ls veas tu carta y /home/tunombredeusuario/amigos.

         mkdir /home/minombredeusuario/amigos

     o bien

         mkdir ~/amigos

 14. Copia la carta micarta.txt en el directorio que acabas de crear, manteniendo permisos y propietario.

         cp -p ~/micarta.txt ~/amigos

 15. Crea un enlace o atajo llamado carta al fichero micarta.txt.

         ln -s ~/micarta.txt carta

 16. Renombra /home/tunombredeusuario/amigos, por /home/tunombredeusuario/mis_amigos.

         mv ~/amigos ~/mis_amigos

 17. Busca todos los ficheros acabados en bak mediante el comando find, borrándolos.

         find / -name "*.bak" -delete

 18. Calcula cuanto ocupa el directorio /home mediante el comando du.

         sudo du -h -s /home


___



CARPETAS DE UNIX
----------------

 19. ¿Qué se guarda en las siguientes carpetas: /bin y /sbin, /mnt y /media, /usr/sbin, /var, /dev, /proc, /boot?

     Respectivamente: ejecutables básicos del sistema, dispositivos montados, ejecutables instalados por los usuarios, dispositivos, logs + ficheros de servicios, información actual del sistema, núcleo + ficheros de arranque.

 20. ¿En qué carpeta se guardan los ficheros de configuración de un programa?

     /etc/fichero_directorio_configuración

 21. ¿En qué carpeta se guardan los ficheros de configuración de un programa para un usuario determinado?

     /home/usuario/.fichero_o_directorio_configuración


___



DISCOS, PARTICIONES, MONTAR Y DESMONTAR
---------------------------------------

 22. Lista las particiones del primer disco duro.

         sudo fdisk -l /dev/sda

     o bien

         ls -l /dev/sda*

     o bien

         lsblk /dev/sda

 23. Monta la partición del disco duro donde reside Windows. (-En caso de no disponer de una segunda partición con Windows, monta a mano una memoria usb o un disco duro externo-).

         sudo mkdir /media/temp
         sudo mount /dev/sda2 /media/temp

 24. Copia un fichero cualquiera de la partición Windows (-o de la memoria usb-) al directorio mis_amigos dentro de tu directorio personal.

         cp /media/temp/autoexec.bat ~/mis_amigos

 25. ¿Con qué comandos se cambiarían los permisos, el propietario y el grupo de estos ficheros?

         sudo chmod -R permisos *
         sudo chown -R usuario:grupo *

 26. Desmonta la partición del disco duro donde reside Windows (-o la memoria usb-).

         sudo umount /media/temp

     o bien

         sudo umount /dev/sda2

 27. Borra el directorio que has creado para montar la partición con Windows (-o la memoria usb-).

         sudo rmdir /media/temp

     pero no

         sudo rm -rf /media/temp

 28. ¿Qué hay en los ficheros /etc/fstab y /etc/mtab?

     Respectivamente: asociación preestablecida de dispositivos y puntos de montaje; dispositivos montados en el sistema.

 29. ¿Cómo puedes saber el UUID de una partición? ¿Qué es el UUID y para qué se utiliza?

     Se utilizan identificadores únicos de particiones (UUID) porque los nombres de dispositivos del núcleo (/dev/sda, /dev/sdb, etc) cambian dependiendo dónde esté el disco conectado , mientras que el UUID (/dev/disk/by-uuid/...) apunta siempre al mismo disco.

         sudo blkid /dev/partición

     o bien

         ls -l /dev/disk/by-uuid/


___



USUARIOS
--------

 30. Muestra el nombre del usuario en la sesión actual, y después el nombre de la máquina.

         whoami; hostname

 31. Muestra qué usuarios hay en el sistema en el momento actual.

         who

 32. Crea un usuario llamado pepito con contraseña grillo, y añádelo al grupo admin. Después bórralo.

         sudo adduser pepito
         sudo adduser pepito admin
         sudo deluser pepito


___



SEGURIDAD
---------

 33. El usuario acastan desea cambiar su contraseña. ¿Cómo lo hace? ¿Qué ayuda debe pedir al administrador?

     No necesita ayuda del administrador. Lo hace con el comando `passwd`

 34. El usuario acastan olvidó su contraseña. ¿Qué puede hacer por sí mismo? ¿Necesita ayuda del administrador? ¿Cómo puede el administrador averiguar la contraseña que el usuario olvidó? ¿Cómo hace el administrador para cambiar la contraseña del usuario acastan?

     Necesita que el administrador cambie la contraseña (el administrador no la puede averiguar) , mediante el comando `sudo passwd acastan`


___



PROCESOS
--------

 35. Muestra los procesos de tu sesión actual que se están ejecutando.

         ps

 36. Muestra todos los procesos en tu sistema que se están ejecutando.

         ps -ef

     o bien

         ps aux

     y también

         pstree

 37. Crea un nuevo proceso al ejecutar el comando more /etc/passwd y páralo con CTRL+Z. Comprueba que aunque estés de nuevo en la línea de comandos dicho proceso sigue activo. Elimina definitivamente dicho proceso con el comando kill.

         more /etc/passwd
         ps
         kill -9 pid_proceso

 38. ¿Cómo se lanza un proceso o comando y, sin que éste haya terminado, accedemos de nuevo a la línea de comandos.

         comando &

     pero también

         nohup comando &

 39. Comprueba el consumo de recursos del sistema por los procesos mediante el comando top.

         top

 40. Visualiza la configuración TCP/IP de tus tarjetas de red.

         ifconfig -a

     o bien

         ip a

     y si quiero saber los datos wireless

         iwconfig

 41. Visualiza todas las conexiones abiertas con internet, y qué procesos las han generado.

         netstat -tupane

     o bien

         ss -tupane

 42. Monitoriza los puertos abiertos a la escucha en tu ordenador.

         netstat -tupane | grep ESCUCHAR

     o bien

         ss -tupane | grep LISTEN

 43. ¿Qué versión del núcleo Linux tenemos? ¿Cómo podemos ver sus mensajes?

         uname -a
         dmesg
         
     o bien
     
         uname -a
         less /var/log/messages

 44. ¿Qué comandos apagan el sistema?

     `reboot`   ,   `halt`   ,   `poweroff`   ,   `shutdown tiempo mensaje`


___



SERVICIOS Y FICHEROS DE CONFIGURACIÓN
-------------------------------------

 45. ¿Cómo se detiene o inicia un servicio?

     Con sistema de inicio init:

         sudo /etc/init.d/servicio [start/restart/stop/status]

     Con sistema de inicio upstart:

         sudo service servicio [start/restart/stop/status]

     Actualmente, con sistema de inicio systemd:

         sudo systemctl [start/restart/stop/status] servicio

 46. ¿Dónde está guardada la información de los repositorios de programas disponibles?

     Depende del s.o. Unix y de la distribución Linux. En Debian y Ubuntu está en /etc/apt/sources.list


 47. ¿Dónde está guardada la configuración de las tarjetas de red?

     En Debian y Ubuntu está en /etc/network/interfaces , pero en Ubuntu 18.04 y superiores está en /etc/netplan/*.yaml

 48. ¿Dónde está guardados los servidores de DNS que utiliza el equipo?

     /etc/resolv.conf

 49. ¿Dónde está guardada la información de ejecución periódica de procesos? ¿Con qué comando se añaden nuevos procesos? ¿Qué formato tienen las líneas de dichos ficheros?

     /etc/crontab

         crontab [usuario] -e

     minuto , hora , dia_del_mes , mes , dia_de_la_semana , y el comando
     
     Pero con SystemD hay una nueva manera de ejecutar periódicamente procesos:
     
     <https://www.atareao.es/tutorial/trabajando-con-systemd/cron-con-systemd-timer/>

 50. ¿En qué ficheros se guarda información relativa a los usuarios del sistema?

     /etc/passwd , /etc/shadow , /etc/group , /etc/gshadow , /etc/sudoers , /etc/skel


___



EXPRESIONES REGULARES (EXTRA)
-----------------------------

 01. Palabras que tienen una a más b o una a más d seguidas de una n

         grep a[b\|d]n fichero

 02. Palabras que tienen dos o más a seguidas

         grep a[a+] fichero

 03. Palabras cuya tercera letra es b

         grep ^..b fichero

 04. Palabras que contienen pan o plan

         grep p[l\?]an fichero

 05. Palabras que acaban en cial

         grep cial$ fichero

 06. ¿Cuantas líneas vacías?

         grep -c ^$ fichero

 07. Palabras que contienen un número del 0 al 5

         grep [0-5] fichero

 08. Palabras que acaban en o, más una letra que no sea n

         grep o[^n]$ fichero

 09. Contraseñas que tienen seis letras seguidas de dos números

         grep [:alpha:]{6}[:digit:]{2} fichero

 10. El nombre de un fichero con extensión .txt , .odt o .pdf

         grep .*(\.txt|\.odt|\.pdf)$ fichero

 11. Una fecha con el formato dd/mm/aaaa

         grep [0-9]{2}\/[0-9]{2}\/[0-9]{4} fichero

 12. Una dirección de correo electrónico con el formato nombre@dominio.xxx

         grep ([:alnum:]+)(EN)([:alnum:]+)[\.]([:alnum:]){2,4} fichero

