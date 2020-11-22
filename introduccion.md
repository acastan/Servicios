De qué hablamos cuando decimos "servidores"
-------------------------------------------
Un programa espera recibir peticiones, por red, para responder a ellas (servidor). Para ello, está en todo momento escuchando por un "puerto" determinado.

Otro programa en otro ordenador (cliente) realiza peticiones por red al servidor y procesa la respuesta. Es el sistema operativo el que le da un puerto disponible por encima del 1024 para comunicarse.

Es de vital importancia de que el servidor esté siempre disponible, 24/7/365, y en el caso que almacene datos de la empresa, que estos nunca se pierdan.

Tanto en hardware como en software, las características asociadas a un servidor son redundancia, estabilidad y escalabilidad: responder todo el tiempo, independientemente de los fallos, independientemente de la carga, y no perder nunca los datos.

En caso de servicios cuya respuesta pueda tardar cierto tiempo (por ej. descarga de un gran fichero) se usa multiproceso en el servidor para no dejar otros clientes a la espera.

Dependerá del servicio la cantidad de ram, la velocidad de cpu, la capacidad de disco duro que necesitemos en el servidor.



Hardware
--------
 - Redundancia y calidad.
 - CPU: 64 bits, varios núcleos, optimizaciones para virtualización
 - RAM: ECC, dual channel, ¿cuánta RAM es necesaria?
 - HD: RAID, hotplug
 - Carcasa: formato rack, doble fuente de alimentación
 - SAI
 - Cloud Computing (Iaas)


Sistema Operativo
-----------------
Buscamos: estabilidad; actualizaciones por mucho tiempo; respuesta "lineal" a la carga; no el último software pero sí muy probado; núcleo optimizado para servicios en segundo plano y no para multimedia; posibilidad de trabajar sin interfaz gráfica y con "lo mínimo" (menos software => menos carga y menos exposición a fallos).
 - SSOO: ¿Cuáles conoces? Linux, Solaris, BSDs, Windows Server, ...
 - Distribuciones Linux: ¿Cuáles conoces? CentOS (Red Hat), Debian Stable, Ubuntu Server, Suse Enterprise, ...
 - Distribuciones Linux especializadas: ClearOS, SME Server, Zentyal, ...
 - Particionado: LVM, partición independiente para /var
 - Sistemas de ficheros: Journaling, Snapshots, ...



Temas preliminares
------------------
 - Conectividad a Internet
 - Legislación: RGPD, LSSI, LPI
 - Virtualización
 - TCP/IP
 - Sistemas operativos y hardware de servidores
 - Comandos Unix e instalación Ubuntu Server
 - Planificar los servicios de nuestra red



Servicios de red a estudiar
---------------------------
 - Servidor Proxy i enrutamiento
 - Servidor DHCP
 - Servidor DNS
 - Servidor Proxy caché
 - Servidor Web
 - Servidor Ficheros
 - Servidor Correo
 - Control remoto
 - Servidor Mensajería
 - Servidor Streaming
 - Servidor Directorio
 - Servidor Impresión
 - Cortafuegos
 - VPN
 - NIDS
 - Telefonía IP



Administración remota centralizada y gráfica
--------------------------------------------
 - Zentyal, ISPconfig, Webmin, Gosa, ...



Monitorización
--------------
 - Aplicaciones Análisis de logs: webalizer, calamaris, logcheck, ...
 - Aplicaciones Monitoritzación de rendimiento: ...
 - Aplicaciones Monitoritzación de red: Nagios, Ntop, Cacti, ...
 - Aplicaciones Monitoritzación de SAI: Nut, ...



Virtualitzación
---------------
 - Aplicaciones: Docker, LXD, KVM, VirtualBox, VMware, Proxmox, ...
 - Descargar Máquinas virtuales: http://www.easyvmx.com/ , http://virtualboximages.com/ , http://www.vmware.com/appliances/



Balanceo de carga, escalabilidad y redundancia
----------------------------------------------
 - Escalado vertical y horizontal
 - Ejemplos de escalabilidad: http://highscalability.com/
 - Redundancia: Heartbeat



Enlaces
-------

 - Cursos INTEF sobre servidores Linux y Windows en redes locales:  
   <http://formacion.intef.es/course/view.php?id=184>  
   <http://formacion.intef.es/course/view.php?id=185>

 - Cursos “Serveis de Xarxa” de la IOC:  
   <https://ioc.xtec.cat/materials/FP/Materials/2201_SMX/SMX_2201_M07/web/html/index.html>  
   <https://ioc.xtec.cat/materials/FP/Recursos/fp_asix_m08_/web/fp_asix_m08_htmlindex/index.html>

 - Otras guías de servidores:  
   <https://ubuntu.com/server/docs>  
   <https://help.ubuntu.com/community/Servers>  
   <http://debian-handbook.info/browse/stable/>  
   <http://www.alcancelibre.org/filemgmt/index.php?id=1>

 - Administración Linux y LPI:
   <http://openaccess.uoc.edu/webapps/o2/handle/10609/60686>  
   <https://learning.lpi.org/en/learning-materials/learning-materials/>  
   <http://www.ibm.com/developerworks/linux/lpi/>
