TEORIA
------

Busca información sobre:

  - ¿Qué es la cola de impresión?

  - ¿Qué es Postcript?

¿Por qué utilizar un servidor de impresión, y no utilizar impresoras de red, sin más?

Las ventajas de utilizar un servidor de impresión son varias:

  - Estalvi en impressores i tinta.

  - Posar quotes als usuaris.

  - Posar permisos sobre impressores als usuaris.

  - Agrupar impressores en classes i enviar a imprimir a una classe d'impressores: el servidor l'enviarà a la més adient que estigui preparada.

  - Gestió centralitzada de cues d'impressió.

  - Logs: poder revisar qué s'ha enviat a imprimir, estadístiques, ...

  - Poder visualitzar treballs enviats a imprimir, si se selecciona que no s'esborrin de la cua un cop impresos.

  - Establir horaris d'accés a impressores.

  - Proporcionar controladors automàticament als clients que instal·lin una impressora.


___



CUPS
----

La gran majoria de distribucions GNU/Linux utilitzen CUPS com a sistema d'impressió per defecte.

Un ordinador que executa CUPS actua com un servidor que pot acceptar tasques d'impressió des d'altres ordinadors clients, les processa i les envia a la impressora apropiada.

CUPS és format per:

  - Una cua d'impressió amb un planificador (spooler), ja que la majoria de les impressores no tenen memòria suficient per carregar un document complet. El gestor de la cua monitoritza la impressora i envia el treball següent en el moment en què queda lliure

  - Un sistema de filtres, el qual converteix les dades que s'han d'imprimir en formats que la impressora conegui, ja que hi ha molts models d'impressores diferents.

  - Un sistema de suport (back-end) que envia les dades al dispositiu d'impressió bé sigui mitjançant un port de comunicació físic (USB, paral·lel, RS232, ...) o bé la connexió de xarxa (IPP, AppSocket, ...).

![Esquema](https://ioc.xtec.cat/materials/FP/Materials/2251_ASIX/ASIX_2251_M06/web/html/WebContent/u1/media/continguts_image_5.png)

Els principals protocols de comunicació que es poden fer servir en l'àmbit dels sistemes d'impressió són el següents:

  - Protocol LPD/LPR: antic protocol dels sistemes BSD

  - Protocol IPP: modern protocol basat en HTTP. Permet control d'accés, autenticació i xifrat. És el protocol usat de forma nativa per CUPS i acostuma a fer servir el port 631. 

  - AppSocket: protocol fiable, senzill i ràpid basat en HP JetDirect. Utilitza el port 9100.

  - AppleTalk: protocol per compartir impressores a xarxes Apple.

  - SMB/CIF: protocol per compartir impressores a xarxes Windows.

| Backend  | Sintaxi URI                     | Exemple URI                               |
|:-------- |:------------------------------- |:----------------------------------------- |
| Parallel | parallel:/dev/lpnumber          | parallel:/dev/lp0                         |
| USB      | usb://make/model?serial= number | usb://vendor/printer%201000?serial=A1B2C3 |
| ipp      | ipp://host/printers/queue       | ipp://host/printers/printer1000           |
| LPD      | lpd://host/queue                | lpd://host/printer                        |
| socket   | socket://host:port              | socket://ip:9100                          |
| CIFS/SMB | mira `man smbspool`             | smb://user:password@workgroup/host/share  |

CUPS, a més d'utilitzar el protocol IPP com a base per al maneig de tasques d'impressió i cues d'impressió, també proveeix les ordres tradicionals de línia d'ordres d'impressió dels sistemes GNU/Linux.

![Esquema](http://apprize.info/linux/comptia/comptia.files/image105.jpg)


___



INSTAL·LAR I CONFIGURAR EL SERVIDOR CUPS
----------------------------------------

CUPS està incorporat per defecte en la majoria de distribucions però, en qualsevol cas, només cal instal·lar el paquet:

    $ sudo apt install cups cups-client cups-pdf

  - cups, és el paquet que ens instal·la el servidor CUPS.

  - cups-client, és el paquet que ens instal·la el client CUPS.

  - cups-pdf, és el paquet que ens instal·la una eina que ens permet crear fitxers PDF a partir del CUPS, com si fos una impressora. És similar al PDFCreator del Windows.

Per poder-lo configurar i administrar, el servidor CUPS disposa, a més de del fitxer de configuració i de les ordres de l'intèrpret d'ordres, d'una interfície web que funciona sobre el port 631. Aquesta interfície web permet de manera gràfica afegir, cercar i eliminar impressores i classes d'impressores, controlar els treballs en les cues d'impressió i gestionar diversos paràmetres del servidor. Per accedir a aquesta interfície web:

  http://localhost:631/

Els usuaris que administren CUPS, si no són administradors del sistema, han d'estar afegits a grup lpadmin.



Els principals arxius de configuració de CUPS són:

  - Configuració del servidor: /etc/cups/cupsd.conf
  
    és l'arxiu principal que centralitza la configuració del sistema d'impressió. De característiques semblants a l'arxiu de configuració del servidor Apache, defineix les característiques del servidor CUPS.
  
  - Definició d'impressores: /etc/cups/printers.conf
  
    conté la llista d'impressores locals definides amb informació de la cua d'impressió associada o de com està connectada i amb quina interfície.

  - Arxius PPD (PostScript printer description):
  
    cada cua d'impressió té el seu propi arxiu de configuració situat al directori /etc/cups/ppd. Aquests arxius contenen les opcions de configuració de la impressora (mida i orientació del paper, resolució, escala…).

  - Classes d'impressores: /etc/cups/classes.conf
  
    conté la llista de classes d'impressores definides localment.
    
  - Tipus MIME: /etc/cups/mime.types (o bé /usr/share/cups/mime/mime.types)
  
    indica els tipus d'arxius MIME admesos (text/plain, application/postcript…).

  - Regles de conversió: /etc/cups/mime.convs (o bé /usr/share/cups/mime/mime.convs)
  
    defineix quin o quins filtres estan disponibles per convertir arxius d'un format a un altre. Els filtres estàndard admeten text, arxius PDF, PostScript i molts tipus de formats d'imatge.



Els principals arxius de registre de CUPS són:

  - /var/log/cups/access_log: enregistra totes les peticions HTTP i IPP processades pel planificador de cues.
  
  - /var/log/cups/error_log: conté tots els missatges d'error del planificador per poder fer una anàlisi i seguiment dels problemes.
  
  - /var/log/cups/page_log: enregistra un llistat de totes les pàgines que s'han imprès.



El fitxer de configuració del servidor /etc/cups/cupsd.conf conté directives molt semblants al fitxer de configuració d'Apache. Algunes d'aquestes directives són:

  - Location: defineix una secció per a l'assignació de permisos d'accés i nivell d'autorització a un directori determinat.

  - Allow/Deny: dins d'una secció location especifica les adreces IP que poden accedir a un directori determinat del servidor.

  - Require: defineix el conjunt d'usuaris que poden accedir al servei.

  - Listen: indica les adreces/ports escoltats pels servidor.

  - AccesLog, ErrorLog i PageLog: especifica el nom i adreça absoluta de la ubicació dels arxius de registre.

  - DefaultLanguage: especifica el llenguatge per defecte que faran servir les connexions del clients (opcions de, en, es, fr, it).

  - Loglevel: determina el nivell d'enregistrament de l'arxiu error_log.

  - MaxClients: defineix el nombre màxim de clients simultanis.

  - MaxJobs, MaxJobsPerPrinter, MaxJobsPerUser: permet limitar el nombre màxim de treballs d'impressió totals, per impressora o per usuari.

  - Browsing On, Browsing Off: activa/desactiva l'enviament de paquets UDP broadcast per informar a la xarxa de les impressores disponibles.

Exemple de configuració:

    <Location /printers>
        Order Deny,Allow
        Deny from All
        BrowseAllow from 127.0.0.1
        BrowseAllow from 192.168.1.0/24
        Allow from 127.0.0.1
        Allow from 192.168.1.0/24
        Require user @PROFESSORS
    </Location>


___



COMPARTIR IMPRESSORES
---------------------

|   compartir    | **a Windows** | **a Linux**  |
|:--------------:|:-------------:|:------------:|
| **de Windows** |     Samba     |    Samba     |
|  **de Linux**  |   IPP i Smb   |     CUPS     |

CUPS també disposa d'un suport limitat d'operacions sota el protocol SMB, el quals s'utilitza, en aquest cas, per compartir impressores. Per exemple, si fem servir la compartició d'impressores via CUPS, podrem determinar si una màquina de la xarxa pot accedir o no a les impressores, però no quins usuaris concrets de cada màquina hi tenen accés i quins no. Si utilitzem el Samba, en canvi, podrem distingir entre els usuaris i/o els grups d'una màquina que tenen accés a les impressores del servidor CUPS i els que no hi tenen accés. 

(Incís: jo crec que CUPS **sí** permet autentificació d'usuaris. Ho fa a través de la directiva `require` al seu fitxer de configuració.)


___



EXERCICI: AFEGIR A CLIENTS WINDOWS I LINUX LES IMPRESSORES COMPARTIDES DEL SERVIDOR CUPS
----------------------------------------------------------------------------------------

1) Empra una de les màquines virtuals de l'escola com a servidor. L'escriptori segurament porta instal·lat CUPS, però sense actualitzar i sense la impressora pdf.

       sudo apt update
       sudo apt install synaptic
       sudo synaptic

   Dins de Synaptic cerca CUPS

   Ordena els resultats per la primera columna per veure el que tens instal·lat. Selecciona els paquets instal·lats que necessiten actualització, i marca'ls per actualitzar.

   Marca per instal·lar el paquet cups-pdf

   Aplica els canvis

2) Connecta una impressora per USB. L'escriptori la instal·larà automàticament. Navega per la interfície web de CUPS http://localhost:631/ per comprovar que el sistema l'ha instal·lat. Recorda el nom que l'hi ha donat a la impressora.

3) Entra a un altre màquina virtual Linux. Amb l'eina de gestió d’impressores de l'escriptori instal·la la impressora compartida en xarxa. Comprova que la URI on ha trobat la impressora és ipp://IP_SERVIDOR:631/printers/NOM_IMPRESSORA . Recorda aquesta URI.

4) Entra a un altre màquina virtual Windows. A _Agregar components de Windows_ revisa que estigui instal·lat _Impressió per Internet_. Amb l'eina de gestió d’impressores del Panell de Control instal·la la impressora compartida en xarxa. Posa l'URI de la impressora http://IP_SERVIDOR:631/printers/NOM_IMPRESSORA . Probablement et demani els controladors.


___



EXERCICI: COMPARTICIÓ IMPRESSORES A UN DOMINI WINDOWS
-----------------------------------------------------

Lliura un document amb captures de pantalla d'aquests apartats:

1) Utilitza dues màquines virtuals amb Windows, una configurada com un servidor controlador de domini amb Windows Server, i l'altre serà un client de Windows del centre que haureu posat dins del domini. El nom del domini serà "elteunom". La resta de paràmetres són de lliure elecció.

2) Dona d'alta al servidor controlador del domini els grups anomenats professorsSMX i estudiantsSMX, amb un usuari cadascun.

3) Instal·la al servidor controlador de domini una impressora virtual, per exemple PdfCreator.

4) Converteix el servidor de domini en un servidor d'impressió, assignant aquest rol.

5) Assigna sobre la impressora instal·lada els permisos següents:

   - Els usuaris del grup professorsSMX han de poder imprimir.

   - Els usuaris del grup estudiantsSMX no han de poder imprimir.

6) Comprova-ho accedint amb els usuaris des de la màquina client.


___



EXERCICI: COMPARTICIÓ IMPRESSORES A LINUX
-----------------------------------------

Intenta implementar amb CUPS l'exercici anterior: instal·la la impressora pdf de CUPS, i dona permís d'impressió als usuaris del grup professorsSMX i denega el permís d'impressió als usuaris del grup estudiantsSMX.

