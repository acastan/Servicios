PREGUNTAS
---------

 01. ¿En qué consiste la virtualización? ¿Qué tipos de virtualización hay? ¿Qué ventajas proporciona?

 02. ¿Cómo se puede crear y manejar las máquinas virtuales desde la línea de comandos de VirtualBox?

 03. ¿Qué es un disco duro virtual de expansión dinámica? ¿Se puede agrandar el límite de tamaño de un disco duro virtual que fijamos cuando lo creamos?

 04. Si os borran una máquina virtual, ¿Cómo podéis crear una máquina virtual a partir de un disco duro virtual que os den?

 05. Si tenemos que crear una segunda máquina virtual idéntica a otra que ya habíamos creado, ¿Nos basta con crear una copia del fichero donde está el disco duro virtual, y asignárselo a la nueva máquina?

 06. ¿Qué es el formato estándar OVF?

 07. ¿A qué llama VirtualBox un snapshot de disco duro?

 08. En una máquina virtual en ejecución en VirtualBox ¿Cómo puedo montar un CD sobre la marcha? ¿Cómo puedo montar un USB sobre la marcha?

 09. ¿Qué son los GuestAdditions de VirtualBox? ¿Cómo se instalan? ¿Qué ventajas proporcionan? ¿Qué son las carpetas compartidas de VirtualBox?

 10. En VirtualBox, ¿Qué modos hay de trabajo en red? ¿Cómo funciona cada modo? ¿De qué maneras se pueden comunicar máquinas virtuales que están en el mismo ordenador? ¿Y en ordenadores diferentes?





PRÁCTICA
--------

  - Instalaremos VirtualBox. En caso de que estemos en Linux, configuraremos los repositorios de programas para añadir los de VirtualBox que se pueden obtener en <http://www.virtualbox.org/wiki/Linux_Downloads>, y así tener siempre disponible la última versión de VirtualBox.

  - Importaremos una máquina virtual de Linux que nos proporcionará el profesor en formato OVF. Configuraremos los dispositivos, la arrancaremos y comprobaremos que funcione. Está máquina, más adelante, será nuestro servidor Linux.

  - Crearemos una máquina virtual de Windows a partir de un disco virtual que nos proporcionará el profesor y que ya tiene instalado el sistema operativo. Configuraremos los dispositivos, la arrancaremos y comprobaremos que funcione. Está máquina, más adelante, será nuestro servidor Windows.

Primera part pràctica: màquines virtuals en xarxa en mode pont. Temps màxim una hora.

  - Mira quina IP té la teva màquina real.

  - A VirtualBox escolleix una de les màquines virtuals existents i posa-la en mode pont. Arrenca-la i fes que la seva adreça IP sigui la de la teva màquina real + 50. Quina IP és?

  - A VirtualBox escolleix una altre de les màquines virtuals existents i posa-la en mode pont. Arrenca-la i fes que la seva adreça IP sigui la de la teva màquina real + 100. Quina IP és?

  - Comprova que es poden fer ping des d’una màquina virtual cap Internet, per exemple a l’adreça 8.8.8.8. LLIURA CAPTURA DE PANTALLA (1).

  - Comprova que es poden fer ping entre elles. LLIURA CAPTURA DE PANTALLA (2).

  - Comprova que es pot fer ping entre una de les màquines virtuals i la màquina real. LLIURA CAPTURA DE PANTALLA (3).

  - Comprova que es pot fer ping entre una de les màquines virtuals teves i una de les màquines virtuals del company del costat. LLIURA CAPTURA DE PANTALLA (4).

Segona part pràctica: màquines virtuals en xarxa en mode NAT. Temps màxim dues hores.

  - A VirtualBox escolleix una de les màquines virtuals Linux existents i posa-la en mode NAT. Quina és la IP proporcionada per VirtualBox?

  - A VirtualBox escolleix una de les màquines virtuals Windows existents i posa-la en mode NAT. Quina és la IP proporcionada per VirtualBox?

  - Comprova que es poden fer ping des d’una màquina virtual cap Internet, per exemple a l’adreça 8.8.8.8.

  - Comprova que no es poden fer ping entre elles, ni que canviïs la IP.

  - Comprova que sí es pot fer ping d’una de les màquines virtuals cap a la màquina real. LLIURA CAPTURA DE PANTALLA (5).

  - Comprova que no es pot fer ping de la màquina real cap una de les màquines virtuals. LLIURA CAPTURA DE PANTALLA (6).

  - A la màquina virtual Linux executa aquestes comandes per instal·lar un servidor web que té una pàgina per defecte:

        sudo apt update
        sudo apt install apache2

  - Ara a VirtualBox accedeix a la redicceció de ports de la targeta de xarxa NAT d’aquesta màquina virtual Linux i fes que quan a la màquina real li arribi un paquet a un port el redireccioni al port del servidor web de la màquina virtual. Quins ports escolliràs a la màquina real i a la virtual per que això funcioni? LLIURA CAPTURA DE PANTALLA (7).

  - Comprova que des del navegador de la màquina real es pot accedir a la pàgina web de prova de la màquina virtual. A través de quina IP i port accediràs? LLIURA CAPTURA DE PANTALLA (8).

  - Comprova que des del navegador de la màquina virtual Windows es pot accedir a la pàgina web de prova de la màquina virtual. A través de quina IP i port accediràs? LLIURA CAPTURA DE PANTALLA (9).

  - Comprova que des del navegador de la màquina virtual del company del costat es pot accedir a la pàgina web de prova de la màquina virtual teva. A través de quina IP i port accediràs? LLIURA CAPTURA DE PANTALLA (10).





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Platform_virtualization>

  - <http://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines>

  - <http://www.virtualbox.org/>

  - <http://www.virtualboximages.com/>

  - <http://www.vmware.com/>

  - <http://www.vmware.com/appliances/>
