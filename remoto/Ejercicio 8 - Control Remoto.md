PREGUNTAS
---------

  01. ¿Es lo mismo acceso remoto que control remoto? ¿Qué diferencia hay?

  02. ¿Qué es SSH?

  03. ¿Qué es VNC?

  04. ¿Qué es X sobre SSH?

  05. ¿Qué es SPICE?

  06. ¿Qué es RDP?

  07. Dibuja una tabla con las diferencias hay entre ellos (SSH, VNC, RDP, SPICE, X sobre SSH). Indica para que sistema operativo está disponible el servidor y el cliente, cuál es herramienta de control remoto y cuál de acceso remoto, cuál da acceso a línea de comandos y cuál a aplicaciones gráficas.
  
  08. ¿Qué es un tunel SSH y para qué sirve? ¿Qué tipos de tunel SSH existen? ¿Qué diferencia hay entre tunel SSH y VPN? ¿Con qué comandos puedes crear un tunel SSH en Linux?





PRÁCTICA WINDOWS
----------------

  - Instalaremos un servidor SSH (freesshd) y accederemos desde un cliente para Windows (putty) y desde un cliente para Linux (ssh).

  - Instalaremos un servidor VNC y accederemos desde un cliente para Windows y desde un cliente para Linux (ya instalado).

  - Mediante la utilidad "Conexión a escritorio Remoto" de Windows, accederemos remotamente a otro equipo Windows.

  - Activaremos el servicio de terminales y accederemos desde un cliente para Windows y desde un cliente para Linux. En caso de utilizar como servidor un Windows XP, deberemos instalar el parche proporcionado por http://www.kood.org/terminal-server-patch/





PRÁCTICA LINUX
--------------

  - Instalaremos un servidor SSH (openssh-server) y accederemos desde un cliente para Windows (putty) y desde un cliente para Linux (ssh).

  - Habilitaremos el servidor VNC y accederemos desde un cliente para Windows y desde un cliente para Linux (ya instalado).

  - Instalaremos un servidor SSH y accederemos a aplicaciones gràficas de Linux desde un cliente para Windows. Si quisieramos hacer lo contrario, es decir, acceder a ventanas de aplicaciones Windows des de Linux mediante X sobre SSH, ¿qué necesitaríamos instalar en Windows?

  - Estudiaremos como funciona la autentificación de clave pública/privada en SSH, e implementaremos autentificación sin contraseña en SSH mediante dicho sistema.





PRÁCTICA EXTRA: control remoto del ordenador de casa
----------------------------------------------------

  - Instala TeamViewer o LogMeIn en un ordenador de tu casa (-o en una máquina virtual en NAT-).

  - Controla el ordenador de tu casa o la máquina virtual des de tu teléfono móvil, con el cliente de TeamViewer o LogMeIn para smartphone.





PRÁCTICA EXTRA: tunel SSH
-------------------------

Implementa una conexión VNC bajo tunel SSH. Para ello debes:

  - Instalar un servidor VNC en el ordenador a controlar, y un cliente en el ordenador que controlará. Prueba que funciona.

  - Instalar un servidor SSH en el ordenador con el servidor VNC, y un cliente SSH en el ordenador con el cliente VNC. Prueba que funciona.
  
  - Ahora haz pasar la conexión VNC por un tunel SSH del cliente al servidor, para que cifre la comunicación VNC:
  
    puerto 5902 vnc cliente -> puerto 22 ssh cifra comunicación -> puerto 5901 vnc servidor

    - Cliente Windows: <http://www.maquinasvirtuales.eu/conexion-vnc-bajo-tunel-ssh-putty/>

    - Cliente Linux: <https://www.ochobitshacenunbyte.com/2022/10/19/como-crear-un-tunel-ssh-en-linux/>





PRÁCTICA EXTRA: el SSH de Mike
------------------------------

Desde que Mike Oldfield vive retirado en las Bahamas, sufre cortes de luz debido a las tormentas del Pacífico Sur, así que su compañía de discos le obliga a subir los masters del que será su último trabajo, Tubular Bells IV, a un servidor SSH en Londres mediante SCP.

Los ficheros a subir se llaman: Tubular4_Part1.raw , Tubular4_Part2.raw , Tubular4_Part3.raw y Tubular4_Part4.raw

Por motivos prácticos, crearemos ficheros de 50 megas de ceros con el comando `dd`:

    dd if=/dev/zero of=mi_fichero bs=50M count=1

Mike lleva una vida distraída y amena en la isla (es un abuelete), pero cada día graba unos 20 segundos de alguna de las partes, y no de manera continua (es un poco impredecible), así que los ingenieros de sonido de Londres (donde se encuentra el servidor SSH), deciden que guardarán TODO lo que suba Mike, sin sobrescribir nada. Para ello crean un script automático que se encarga de crear una carpeta con la fecha del sistema y meter dentro los fichero correspondientes. Mike solo tiene que ejecutar ese script desde la carpeta donde está grabando y ya no se tiene que preocupar de nada más, no vaya a ser que las musas se le vayan...

    #!/bin/bash
    mifecha=`date +%F | tr -d '-'`
    echo mi variable vale $mifecha

Además, Mike es un paranoico de la seguridad, así que exige a su compañía de discos un backup diario con SCP a otro servidor distinto que está situado en Barcelona. El servidor de Londres será el encargado de hacer el backup a las 23:55 cada día vía SCP. Por motivos prácticos, programa la tarea con crontab a una hora que veas si se ejecuta para presentar el informe.

(a) Utiliza las herramientas de OpenSSH para implementar en máquinas virtuales tu configuración Bahamas – Londres – Barcelona.

(b) Programa los scripts correspondientes en cada máquina y comprueba su funcionamiento.

(c) Documenta todo el proceso con capturas de pantalla y explicaciones.

(d) Controla con iptables que sea el ordenador de Mike, y sólo el de Mike, el que suba los ficheros a Londres.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Secure_Shell>

  - <https://iximiuz.com/en/posts/ssh-tunnels/>

  - <http://en.wikipedia.org/wiki/VNC>

  - <https://en.wikipedia.org/wiki/Simple_Protocol_for_Independent_Computing_Environments>

  - <http://en.wikipedia.org/wiki/Remote_Desktop_Protocol>

  - <http://en.wikipedia.org/wiki/Remote_Desktop_Services>

  - <http://en.wikipedia.org/wiki/X_Window_System_protocols_and_architecture>

  - <http://dustwell.com/how-x-over-ssh-really-works.html>

  - <http://www.vanemery.com/Linux/XoverSSH/X-over-SSH2.html>

  - <http://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software>
