RESUMEN DE CONTENEDORES Y DOCKER
================================

Esta es mi introducción a contenedores y a Docker, aunque no soy un experto en el tema.

Te recomiendo que visites:

 * [Un buen curso sobre Docker](https://sergarb1.github.io/CursoIntroduccionADocker/)

 * [Un resumen de Docker con buenos gráficos](https://betterprogramming.pub/docker-for-front-end-developers-c758a44e622f)

 * [La documentación oficial de Docker](https://docs.docker.com/)

 * [¿Qué deberías aprender si te vas a dedicar a Docker?](https://roadmap.sh/docker)

Tabla de contenido:

 * [CONTENEDORES](#contenedores)
 * [DOCKER](#docker)
 * [INSTALAR DOCKER](#instalar-docker)
 * [COMANDOS DE DOCKER SOBRE CONTENEDORES](#comandos-de-docker-sobre-contenedores)
 * [COMANDOS DE DOCKER SOBRE EL SISTEMA DE FICHEROS Y PERSISTENCIA](#comandos-de-docker-sobre-el-sistema-de-ficheros-y-persistencia)
 * [COMANDOS DE DOCKER SOBRE LA RED](#comandos-de-docker-sobre-la-red)
 * [COMANDOS DE DOCKER SOBRE IMAGENES](#comandos-de-docker-sobre-imagenes)
 * [CREACION DE IMAGENES DOCKER](#creacion-de-imagenes-docker)
 * [CUENTA EN DOCKER HUB](#cuenta-en-docker-hub)
 * [EJERCICIO DE DOCKER](#ejercicio-de-docker)
 * [ORQUESTACION DE CONTENEDORES DOCKER](#orquestacion-de-contenedores-docker)
 * [DOCKER COMPOSE](#docker-compose)
 * [DOCKER SWARM](#docker-swarm)
 * [KUBERNETES](#kubernetes)
 * [TEMPORAL - SEGURIDAD](#temporal---seguridad)
 * [TEMPORAL - A REVISAR](#temporal---a-revisar)


---


CONTENEDORES
------------

La virtualización basada en contenedores es un método de virtualización en el que sobre el núcleo del sistema operativo se ejecutan mecanismos de aislamiento que permiten que existan múltiples instancias aisladas de espacios de usuario, en lugar de solo uno. Dichas instancias, llamadas contenedores o jaulas, pueden verse como un servidor real desde el punto de vista de sus usuarios. Las actividades de un contenedor no tienen impacto sobre otros contenedores. 

Al software que permite el alojamiento de distintos contenedores se le llama motor de contenedores.

Veámoslo con una imagen, que vale más que mil palabras:

![](https://drek4537l1klr.cloudfront.net/denniss/HighResolutionFigures/figure_1-1.png)

Fijate que aunque la virtualización con contenedores consume más recursos que ejecutar las aplicaciones y servicios directamente sin contenedores, consume muchos menos recursos que ejecutar dichas aplicaciones y servicios en máquinas virtuales.

Usos de virtualización, sea de contenedores o de otro tipo:

 * Distribución de aplicaciones ("I don't care if it works on your machine! We are not shipping your machine!"): para asegurarte que tu aplicación siempre se ejecutará en la máquina dónde se instale, dónde puede haber otra versión del sistema operativo o de librerías necesarias, en lugar de distribuir tu aplicación distribuyes una máquina virtual donde tu aplicación está instalada y funciona.

 * En lugar de tener servicios ejecutándose en diferentes máquinas hardware, los puedes agrupar virtualizados en una única máquina hardware, aislados unos de otros. Cuando tenemos un número elevado de peticiones y sobrecarga, podemos escalar horizontalmente mediante software de "orquestación" levantando más instancias de servidores virtualizados.

Ventajas de usar contenedores:

 * Un contenedor arranca muchísimo más rápido que una máquina virtual, ya que el núcleo del sistema operativo ("kernel") ya está en marcha.

 * Consume menos recursos: no necesitamos memoria RAM para el núcleo, no necesitamos CPU para el hipervisor, no necesitamos optimizaciones en la CPU para poder virtualizar.

Desventajas:

 * No podemos ejecutar diferentes sistemas operativos, sino que estamos limitados al núcleo del anfitrión. 

 * Un problema típico de la virtualización: si cae el anfitrión (por un problema en el núcleo), caen todos los contenedores que se ejecutan sobre él.

 * Problemas de límites: ¿Los contenedores pueden leer o modificar el sistema de ficheros no compartido del anfitrión? ¿Los contenedores pueden consumir toda la memoria del anfitrión? ¿Los contenedores pueden consumir CPU hasta provocar una degradación del rendimiento de todo el sistema?

Las tecnologías de virtualización de contenedores se dividen en:

 * Contenedores de infraestructura: Ofrecen un servicio que permite ejecutar múltiples instancias de sistemas operativos de manera aislada. Ofrece todo lo necesario para que el sistema “contenido” pueda trabajar, tales como CPU, red, E/S. Es similar a una máquina virtual pero más rápido y ligero. Un ejemplo de estos sistemas es [LXC](https://es.wikipedia.org/wiki/LXC).

 * Contenedores de aplicaciones: Ofrecen un sistema para empaquetar aplicaciones y todas sus dependencias y, por tanto, son muy útiles para el desarrollo y distribución de aplicaciones. Por ejemplo, en integración continua es habitual desarrollar con contenedores para eliminar las diferencias de entorno entre producción y desarrollo y facilitar la migración del entorno. Este tipo de contenedores son muy usados en la computación en la nube para distribuir las aplicaciones. Un ejemplo de estos sistemas es [Docker](https://es.wikipedia.org/wiki/Docker_(software)).

![](https://archives.flockport.com/wp-content/uploads/2014/08/lxc-vs-docker5.png)

Aunque este resumen va a estar dedicado a Docker, es interesante que hagas pruebas con la distribución [Proxmox](https://www.proxmox.com/en/proxmox-ve) que está orientada a gestionar contenedores LXC y máquinas virtuales KVM.


---


DOCKER
------

Docker utiliza una arquitectura cliente-servidor. Los diferentes clientes Docker se comunican con el servidor Docker, llamado "Docker Engine", el cual hace todo el trabajo de construir, ejecutar y distribuir los contenedores Docker. El cliente y servidor Docker pueden estar funcionando en el mismo equipo, pero también un cliente Docker de un equipo se puede conectar a un servidor Docker remoto en otro equipo. Los clientes se comunican con el servidor a través de una API REST, sobre sockets Unix o targeta de red.

Tenemos varios clientes diferentes. Está el cliente típico de línea de comandos, con el que trabajaremos en este curso, pero también hay clientes gráficos como [Portainer](https://www.portainer.io/) y [Docker Desktop](https://www.docker.com/products/docker-desktop/). Otro cliente Docker es Docker Compose, que a través de un fichero de configuración YAML permite lanzar fácilmente aplicaciones que consisten en un conjunto complejo de contenedores.

![](https://docs.docker.com/get-started/images/docker-architecture.webp)

Definiciones:

 * El *servidor Docker* (`dockerd`) escucha las peticiones con el formato de la API Docker y gestiona objetos Docker, como imágenes, contenedores, redes, y volúmenes. Un servidor puede comunicarse con otros servidores para gestionar los servicios Docker.

 * El *cliente Docker* (`docker`) es la pricipal manera en la que la mayoría de usuarios/as interactuan con Docker. Cuando el usuario/a utiliza comandos como `docker run`, el cliente envía dichos comandos en formato de la API de Docker al proceso `dockerd` para que los ejecute. El cliente se puede comunicar con mas de un servidor.

 * Una *imagen Docker* es una plantilla de sólo lectura con las instrucciones para crear un contenedor Docker. Podríamos considerar la imagen como la descripción de la "máquina virtual", mientras que el contenedor es la "máquina virtual" que se ejecuta consumiendo CPU y memoria. A partir de una imagen pueden crearse múltiples contenedores.

   Las imágenes, además de tener su sistema de ficheros predefinido, tienen una serie de parámetros (comandos, de variables de entorno, etc.) con valores por defecto y que se pueden personalizar en el momento de crear el contenedor.
 
   A menudo una imagen está basada en otra imagen sobre la que añade cambios adicionales para personalizarla. Por ejemplo, puedes diseñar una imagen basada en otra imagen previa de Ubuntu, pero que además instala el servidor web Apache y tu aplicación web, así como los detalles de configuración necesarios para que tu aplicación web se pueda ejecutar.

   Puedes crear tus propias imágenes o puedes utilizar las imágenes creadas por otras personas que las han publicado en un "registro". Para crear tu propia imagen debes escribir un documento "Dockerfile" que con una sintaxis sencilla describe los pasos necesarios para crear la imagen y ejecutar contenedores a partir de ella. Cada instrucción en el Dockerfile crea una nueva capa en la imagen. Cuando haces cambios en el Dockerfile y reconstruyes la imagen, sólo se reconstruirán las capas que han cambiado. Esto es en parte lo que consigue que las imágenes Docker sean tan ligeras, pequeñas y rápidas, comparadas con otras tecnologías de virtualización.

 * Un *contenedor Docker* es la instancia ejecutable de una imagen. Puedes crear, iniciar, parar, mover o borrar contenedores usando la API de Docker o un cliente. Puedes asignar un contenedor a una o más redes, añadirle almacenamiento, o incluso crear una nueva imagen a partir del estado actual del contenedor.

   Por defecto los contenedores están relativamente bien aislados de otros contenedores y del equipo anfitrión. Los propietarios de los contenedores pueden controlar con precisión cómo de aislado está el contenedor, su red, su almacenamiento, y sus otros subsistemas.

   El contenedor queda definido por la imagen de la que procede más los parámetros de configuración que se utilizaron cuando se creó o se arrancó, que además pueden reemplazar los de la imagen. Cuando se borra el contenedor, todos los cambios que se hicieron sobre él que no se guardaron en almacenamiento persistente desaparecerán.

   Cada contenedor Docker posee un identificador único de 64 caracteres, pero habitualmente se utiliza una versión corta con los primeros 12 caracteres.

   Cuando se lanza la ejecución de un contenedor Docker, dicho contenedor ejecuta un comando ("punto de entrada"). Una vez dicho comando finaliza, se para el contenedor. Este comportamiento puede liar a los usuarios primerizos, ya que algunos contenedores ejecutaran un comando que finaliza rápido y se pararán, mientras que otros ejecutarán un "demonio", como por ejemplo un servidor web, que no finaliza y por lo tanto no para la ejecución del contenedor.
   
   Docker asigna las IPs a los contenedores dinámicamente. En general no se suele trabajar con los contenedores a través de sus IPs, sino que si tenemos un servicio ejecutándose en un contenedor [mapearemos puertos del contenedor a puertos del anfitrión](https://docs.docker.com/config/containers/container-networking/#published-ports) y Docker ya se encargara de redireccionar el tráfico de red. Pero sobre el mapeo de puertos, recuerda que los sistemas operativos no permiten a dos aplicaciones utilizar el mismo puerto a la vez, ni permiten usar puertos por debajo del 1024 a usuarios no privilegiados.

   Para compartir datos entre contenedores, o entre el anfitrión y los contenedores, podemos [mapear directorios del anfitrión al contenedor](https://docs.docker.com/storage/).

   En este ejemplo, tres contenedores que provienen de dos imágenes enlazan los puertos que quieren exponer con puertos del anfitrión. Por otro lado, dichos contenedores también enlazan algunos de sus directorios a directorios del anfitrión.

   ![Publicar puertos](https://bytes.cat/_media/docker6.png)

 * Los *registros Docker* almacenan imágenes Docker. Docker Hub es un registro público que todo el mundo puede usar, y Docker está configurado por defecto para buscar las imágenes en Docker Hub cuando no las encuentra en el equipo. Pero tu puedes tener un registro privado propio. Cuando utilizas los comandos `docker pull` o `docker run`, las imágenes requeridas se traen des del registro que tengas configurado, y cuando utilizas el comando `docker push`, la imagen especificada se sube al registro que tengas configurado.

 * El *Docker Desktop* es una aplicación fácil de instalar que te permite construir y compartir aplicaciones y microservicios en contenedores. Docker Desktop incluye el servidor Docker, el cliente Docker, Docker Compose, Docker Content Trust, Kubernetes, y Credential Helper.

Docker se puede integrar con diferentes herramientas de infraestructura, como Amazon Web Services, Ansible, Cfengine, Chef, Google Cloud Platform, DigitalOcean, IBM Bluemix, Jelastic, Jenkins, Microsoft Azure, OpenStack Nova, OpenSVC, Puppet, Salt, y Vagrant.


---


INSTALAR DOCKER
---------------

La manera más fácil de instalar Docker en Windows o en MacOS es descargar e instalar [Docker Desktop](https://www.docker.com/products/docker-desktop/). Para usarlo, te pedirá tener creada una cuenta en Docker o Docker Hub. Aunque en Linux también puedo instalar Docker Desktop, dedico las siguientes líneas a la instalación más "normal" y ligera de Docker en Linux.

Se puede instalar mediante un script:

    $ curl -fsSL https://get.docker.com -o get-docker.sh
    $ sudo sh get-docker.sh

Pero también se puede instalar mediante repositorios. Por ejemplo, en mi Debian 12 estable:

    $ sudo apt update
    $ sudo apt install docker.io

En cualquiera de los dos casos, comprueba que se instaló y funciona:

    $ sudo docker run hello-world
    $ sudo docker version
    $ sudo docker info

Para administrar contenedores gráficamente des de un navegador puedes instalar Portainer, que es un contenedor con una aplicación web que se accede navegando por https://localhost:9443 :

    $ sudo docker volume create portainer_data
    $ sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always \
             -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data \
             portainer/portainer-ce:latest

    $ sudo docker ps

Para una instalación "rootless" de Docker, consulta <https://docs.docker.com/engine/security/rootless/>.


---


COMANDOS DE DOCKER SOBRE CONTENEDORES
-------------------------------------

Los comandos que ahora resumo se pueden ejecutar también como subcomandos del comando [`docker container`](https://docs.docker.com/engine/reference/commandline/container/). Por ejemplo, listar contenedores con `docker ps` es equivalente a `docker container ls`.

![](https://miro.medium.com/max/700/0*3_uIz_YMiyZxMwKn)

 * [Crear un nuevo contenedor y ejecutarlo](https://docs.docker.com/engine/reference/commandline/run/):

       docker run [opciones] imagen [comando] [argumentos]

   Por ejemplo:

       docker run -d docker/getting-started
       docker run -it -e MENSAJE=HOLA --rm --name=mi_Ubuntu ubuntu /bin/bash
       docker run -d -p 8080:80 nginx

   Si la imagen (la "plantilla") no está en nuestro equipo, por defecto se descarga de [Docker Hub](https://hub.docker.com/), que es el registro público que proporciona Docker Inc. Muchas de las imágenes oficiales de dicho repositorio reciben configuración para el contenedor a través de variables de entorno (`docker run -e ...`) o ficheros compartidos con el anfitrión (`docker run -v ...`).

   Al crear un contenedor éste puede pasar a estar en modo interactivo o en modo no interactivo ("detached").

   En modo desacoplado (argumento `--detach` o `-d`), una vez lanzado el contenedor, volvemos a la línea de comandos del anfitrión. Por lo tanto el terminal queda asociado al teclado y cónsola del anfitrión. Para acceder a la cónsola del contenedor y leer sus mensajes deberemos ejecutar el comando `docker attach`, que veremos más adelante.

   En modo interactivo (argumentos `--interactive --tty` o `-it`), una vez lanzado el contenedor, su teclado y cónsola quedan asociados al terminal, y por lo tanto no volvemos a la línea de comandos del anfitrión, sino que el terminal muestra los mensajes de pantalla del contenedor. Para volver a la cónsola del anfitrión deberemos pulsar la combinación de teclas `CTRL-P CTRL-Q`.

 * [Listar](https://docs.docker.com/engine/reference/commandline/ps/) contenedores:

       docker ps -a

 * [Parar](https://docs.docker.com/engine/reference/commandline/stop/) e [iniciar](https://docs.docker.com/engine/reference/commandline/start/) contenedores:

       docker stop/start/restart identificador/nombre

   Por ejemplo:

       docker start stupefied_colden
       docker restart 434d318b3771
       docker stop $(docker ps -a -q)

 * [Inspeccionar](https://docs.docker.com/engine/reference/commandline/inspect/) contenedores:

       docker inspect identificador/nombre

   Por ejemplo:

       docker inspect 434d318b3771

 * [Ejecutar comandos](https://docs.docker.com/engine/reference/commandline/exec/) en contenedores:

       docker exec [opciones] identificador/nombre comando [argumentos]

   Por ejemplo:

       docker exec -d 434d318b3771 touch /tmp/prueba
       docker exec -it -e VAR1=1 stupefied_colden bash

 * [Copiar ficheros](https://docs.docker.com/engine/reference/commandline/cp/) entre el anfitrión y el contenedor:

       docker cp [identificador/nombre:]ruta [identificador/nombre:]ruta

   Por ejemplo:

       docker cp 434d318b3771:/tmp/prueba ./
       docker cp ./miFichero stupefied_colden:/tmp

 * [Enlazar la E/S](https://docs.docker.com/engine/reference/commandline/attach/) entre el terminal del anfitrión y el contenedor:

       docker run -d --name=muchotexto busybox sh -c "while true; do $(echo date); sleep 1; done"
       docker attach muchotexto

 * [Obtener logs](https://docs.docker.com/engine/reference/commandline/logs/) , que és como `docker attach` pero con formato "log":

       docker run -d --name=muchotexto busybox sh -c "while true; do $(echo date); sleep 1; done"
       docker logs --follow --until=2s muchotexto

   Todo lo que el programa que se ejecuta en el contenedor escribe a `stdout` y `stderr` se guarda en dichos logs, por lo que dicho log puede crecer enormemente a lo largo de la vida del contenedor.

 * [Cambiar nombre](https://docs.docker.com/engine/reference/commandline/rename/) de un contenedor:

       docker rename nombre_contenedor nuevo_nombre_contenedor

 * [Borrar](https://docs.docker.com/engine/reference/commandline/rm/) el contenedor:

       docker rm stupefied_colden
       docker rm $(docker ps -a -q)
       docker container prune -f

Chuletas de comandos:

 * <https://docs.docker.com/get-started/docker_cheatsheet.pdf>

 * <https://raw.githubusercontent.com/sergarb1/CursoIntroduccionADocker/main/FuentesCurso/Docker%20CheatSheet%20COMPLETA.pdf>

Ejemplos:

1. Lanzamos un contenedor con [noVNC](https://novnc.com/) y nos conectamos vía navegador:

       $ sudo docker run --rm -it -p 8080:8080 theasp/novnc

       <http://localhost:8080/vnc.html>

2. Lanzamos un contenedor Ubuntu con una shell preparada para ejecutar comandos ¿Qué núcleo del s.o. y qué procesos ves en el contenedor? :

       $ sudo docker run -it --name ejercicio ubuntu /bin/bash
       --$ uname -a
       --$ ps -ef

   Si desacoplamos la entrada, podemos ver la misma información del contenedor des del anfitrión, con otros comandos:

       CTRL-P CTRL-Q
       $ sudo docker exec ejercicio uname -a
       $ sudo docker top ejercicio
       $ sudo docker attach ejercicio

   Cuando salimos con el comando `exit` el contenedor se para ¿Qué núcleo del s.o. ves en el anfitrión? :

       --$ exit
       $ sudo docker ps -a
       $ uname -a

   Para volver a acceder a la línea de comandos, arrancamos de nuevo el contenedor:

       $ sudo docker start -ai ejercicio


---


COMANDOS DE DOCKER SOBRE EL SISTEMA DE FICHEROS Y PERSISTENCIA
--------------------------------------------------------------

Los contenedores trabajan con sistema de ficheros *Union File System* (UFS). Los cambios en el contenedor no modifican el anfitrión, sino que crean una nueva "capa" en el contenedor con los cambios.

Si al cabo de un tiempo necesitamos saber qué cambios se han producido en el contenedor podemos utilizar el comando `docker diff contenedor`. Las líneas que muestra que comienzan con ...

 * con 'A' significa que se ha añadido
 * con 'C' significa que se ha cambiado 
 * con 'D' significa que se ha borrado

Además, los contenedores se pueden ejecutar en modo de sólo lectura con el atributo `--read-only`, lo que asegura que ningún dato en el contenedor es modificado.

Para compartir datos entre contenedores o entre el anfitrión y los contenedores, podemos [mapear directorios del anfitrión al contenedor](https://docs.docker.com/storage/bind-mounts/) o utilizar [volúmenes](https://docs.docker.com/storage/volumes/).

![Persistencia](https://bytes.cat/_media/docker-volumes.png)

Los directorios se pueden enlazar en modo de lectura-escritura, pero también en modo de sólo lectura, si queremos asegurarnos que los contenedores no puedan realizar cambios en los datos.

Enlazar a un volumen de Docker es similar a enlazar a un directorio del anfitrión, con la diferencia de que en el volumen Docker no nos tenemos que preocupar dónde está almacenado en el anfitrión.

Por último, en caso que por seguridad queramos que todo el sistema de ficheros del contenedor sea de sólo lectura, pero necesite escribir alguna cosa para funcionar, podemos [montar en memoria](https://docs.docker.com/storage/tmpfs/) dicho directorio donde deba escribir.

 * Para crear un volumen tienes el comando:

       docker volume create mi_volumen

 * Para listar los volumenes tienes el comando:

       docker volume ls

 * Para eliminar un volumen sin contenedores asociados tienes el comando:

       docker volume rm mi_volumen

Ejemplos:

1. Lanzamos la ejecución de un contenedor creado a partir de una imagen oficial de PHP con Apache, que tenga su carpeta /var/www/html mapeada a la carpeta /dades/dades/IAW del anfitrión, donde guardas tus ejercicios de HTML y PHP.

   Solución en formato largo:

       $ sudo docker run -d -p 8000:80 --name php --mount type=bind,source=/dades/dades/IAW/,target=/var/www/html/ php:8.3-apache

   Solución en formato breve:

       $ sudo docker run -d -p 8000:80 --name php -v /dades/dades/IAW/:/var/www/html/:ro php:8.3-apache

   La opción `ro` significa que la carpeta /miweb se monta en modo lectura y no puede ser modificada por el contenedor.

2. Lanzamos Wordpress, utilizando un contenedor con un servidor web y otro contenedor con un servidor de bases de datos. El contenedor con el servidor de base de datos tiene sus ficheros en el volumen wpBBDD, para que no se pierda la base de datos si eliminamos el contenedor. El contenedor con el servidor web es de sólo lectura, pero para que Apache funcione mantiene el directorio /tmp de escritura, y también mantiene en escritura el directorio /run/apache2/ montado en el volumen por defecto del anfitrión:

       $ sudo docker volume create wpBBDD

       $ sudo docker run -d --name miBBDD -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_pass -v wpBBDD:/var/lib/mysql mysql

       $ sudo docker run -d --name miWEB --link miBBDD:mysql -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_pass -p 8000:80 --read-only -v /run/apache2/ --tmpfs /tmp wordpress


---


COMANDOS DE DOCKER SOBRE LA RED
-------------------------------

Los contenedores pueden estar asociados a una red propia. Los contenedores sobre los que no se ha especificado un parámetro `--network` quedan asociados a [la red por defecto](https://docs.docker.com/network/bridge/). Esto puede suponer un riesgo, ya que contenedores que pertenecen a proyectos distintos y no guardan relación se podrán comunicar entre ellos. Al especificar [una red propia](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks), sólo los contenedores que pertenezcan a dicha red se verán entre ellos. Los contenedores que comparten una red, además, exponen todos sus puertos a los otros contenedores. Sólo los puertos que se [mapean](https://docs.docker.com/config/containers/container-networking/#published-ports) quedan expuestos al exterior.

Los contenedores en una red propia no necesitan conocer sus IPs ya que se ven a través de su nombre, porque que Docker los incorpora a un servicio de DNS propio, y reenvía al DNS del anfitrión lo que no pertenezca a la rd propia.

Un contenedor puede estar asociado a más de una red. Además, durante la vida del contenedor, lo podemos conectar y desconectar sobre la marcha de nuevas redes definidas por nosotros. Pero para desconectarlo de la red por defecto y darle una red nuestra, tenemos que pararlo momentáneamente.

 * Para crear una red tienes el comando:

       docker network create mi_red

 * Para listar las redes tienes el comando:

       docker network ls

 * Para eliminar una red sin contenedores asociados tienes el comando:

       docker network rm mi_red

 * Para lanzar el contenedor asociado a una red tienes el parámetro `--network`. Por ejemplo:

       docker run --name mi-nginx --network mi_red --publish 8080:80 nginx:latest

 * Para asociarlo/desasociarlo de una red sobre la marcha, cuando el contenedor ya se estaba ejecutando, tienes los comandos:

       docker network connect mi_red mi-nginx

       docker network disconnect mi_red mi-nginx

Ejemplo:

1. Lanzamos dos contenedores uno asociado a la red *prueba* y otro asociado a la red *produccion*. A continuación el contenedor asociado a la red *prueba* lo asociamos también a la red *produccion* y compruebo que puedan hacer ping entre ellos:

       $ sudo docker network create red_produccion
       $ sudo docker network create red_prueba
      
   En un segundo terminal ejecutamos:

       $ sudo docker run -it --name cont_produccion --network red_produccion alpine sh
      
   En un tercer terminal ejecutamos:

       $ sudo docker run -it --name cont_prueba     --network red_prueba     alpine sh
      
   Hacemos pruebas de conectividad en el segundo y en el tercer terminal:

           ip a
           ping cont_prueba
           ping cont_produccion
   
   Volvemos al primer terminal y el contenedor de prueba lo asociamos también a la red *producción* :

       $ sudo docker network connect red_produccion cont_prueba
   
   De nuevo hacemos pruebas de conectividad en el segundo y en el tercer terminal:

           ip a
           ping cont_prueba
           ping cont_produccion


---


COMANDOS DE DOCKER SOBRE IMAGENES
---------------------------------

Los comandos que ahora resumo se pueden ejecutar también como subcomandos del comando [`docker image`](https://docs.docker.com/engine/reference/commandline/image/). Por ejemplo, listar imágenes con `docker images` es equivalente a `docker image ls`.

 * [Buscar imágenes](https://docs.docker.com/engine/reference/commandline/search/) en el [registro](https://hub.docker.com/search?image_filter=official&type=image):

       docker search python | less

 * [Descargar imágenes](https://docs.docker.com/engine/reference/commandline/pull/) del registro:

       docker pull [host_registro:puerto/][cuenta/]imagen[:versión]

   Por ejemplo:

       docker pull python:2.7

 * [Listar imágenes](https://docs.docker.com/engine/reference/commandline/images/) en el sistema:

       docker images [nombre[:versión]]

 * ¿[Cómo se creó la imagen](https://docs.docker.com/engine/reference/commandline/history/)? Información del Dockerfile:

       docker history [nombre[:versión]]

 * [Borrar imágenes](https://docs.docker.com/engine/reference/commandline/rmi/) del sistema:

       docker rmi $(docker images -f "dangling=true" -q)

 * [Asignar nuevas etiquetas adicionales](https://docs.docker.com/engine/reference/commandline/tag/) a una imagen:

       docker tag cuenta/imagen[:etiqueta1] cuenta/imagen[:etiqueta2]

 * [Copia de seguridad](https://docs.docker.com/engine/reference/commandline/save/) y [restauración](https://docs.docker.com/engine/reference/commandline/load/) de imágenes:

   Una opción sencilla es guardar el Dockerfile, y si necesitamos de nuevo la imagen la creamos en otro equipo.

   Otra opción sencilla es cuando creamos nuestra imagen subirla a nuestra cuenta gratuita en Docker Hub, para poderla descargar cuando queramos.

   Pero por si algún motivo queremos guardar en local la imagen ya creada, podemos utilizar los comandos `save` y `load`.

       docker save -o nombre_fichero.tar repositorio/imagen[:version]
       docker load -i nombre_fichero.tar


---


CREACION DE IMAGENES DOCKER
---------------------------

![](https://miro.medium.com/max/1400/1*p8k1b2DZTQEW_yf0hYniXw.png)

Existe una manera "cutre" pero rápida de crear una imagen, a partir de un contenedor en ejecución. Si sobre dicho contenedor hemos realizado cambios que queremos guardar en una nueva imagen, ejecutamos:

    docker commit -a "autor" -m "descripción" idcontenedor repositorio/imagen:etiqueta

Los cambios que se habían hecho sobre el sistema de ficheros del contenedor, se pueden consultar antes con el comando:

    docker diff idcontenedor

Pero lo normal para crear una imagen es planificar el proceso y escribir una plantilla ("Dockerfile") con la información necesaria para la creación de dicha imagen. Una vez tenemos la descripción guardada en la plantilla, para [construir una imagen](https://docs.docker.com/engine/reference/commandline/build/) ejecutamos:

    docker build -t repositorio/nombre:etiqueta Dockerfile .

[Dockerfile](https://docs.docker.com/engine/reference/builder/) es el fichero de texto que contiene instrucciones que automatizan los pasos para construir la imagen. El Dockerfile contiene

 * Comentarios:

       # comentario

 * La instrucción FROM: especifica la imagen inicial de la cual partimos.

       FROM imagen:etiqueta

 * La instrucción LABEL: añade metadatos a la imagen, como el autor/a.

       LABEL maintainer "acastan@inspedralbes.cat" 

 * La instrucción RUN: ejecuta un comando sobre la imagen para modificarla, normalmente vía `/bin/sh -c`.

       RUN comando
       RUN ["ejecutable", "arg1", "arg2", ...]

 * Las instrucciones ENTRYPOINT y CMD: especifican el comando por defecto a ejecutar al crear el contenedor. ENTRYPOINT es el comando a ejecutar y CMD son los argumentos. Sin embargo, si ENTRYPOINT es una shell, entonces CMD será el comando a ejecutar en dicha shell, lo que puede causar confusión. Si no se especifica, ENTRYPOINT vale "`/bin/sh -c`"

       ENTRYPOINT ["ejecutable"]
       CMD ["arg1", "arg2", ...]

       ENTRYPOINT ["ejecutable", "arg1", "arg2", ...]
       CMD ["comando", "arg1", "arg2", ...]

 * Las instrucciones COPY y ADD: copian ficheros del anfitrión a la imagen.

       COPY fuente destino
       ADD fuente destino

 * La instrucción ENV: crea variables de entorno necesarias para la ejecución de la aplicación dentro del contenedor.

       ENV var1="valor1" var2="valor2" ...

 * La instrucción EXPOSE: especifica qué puertos utilizará el contenedor. El resto de puertos no se podrán acceder externamente.

       EXPOSE puerto/protocolo

 * etc: instrucciones USER , WORKDIR , ARG , VOLUME , LABEL , HEALTHCHECK , ...

Para aprender a construir imágenes, te recomiendo revisar tu fichero Dockerfile en <https://www.fromlatest.io/#/>

Ejemplos de Dockerfile:

1. A partir de una Ubuntu 22.04, instala telnet, y reproduce via telnet la Guerra de las Galaxias en ASCII Art:

       FROM ubuntu:22.04
       LABEL maintainer "yo@mismo.org"
       RUN apt update && apt -y install telnet
       CMD ["/usr/bin/telnet", "towel.blinkenlights.nl"]

   Y ahora ejecuta:

       $ sudo docker build -t starwars .
       $ sudo docker run -it starwars

2. A partir de una Debian, instala cowsay, y dice algo en ASCII Art:

       FROM debian:latest
       LABEL maintainer "tu@mismo.org"
       RUN apt update && apt -y install cowsay
       ENTRYPOINT ["/usr/games/cowsay"]
       CMD ["Docker mooooooola!"]

   Y ahora ejecuta:

       $ sudo docker build -t cowsay .
       $ sudo docker run -it cowsay

3. Crea una imagen con Apache:

       FROM debian
       LABEL maintainer "ana@cardo.org"
       RUN apt update && apt install -y apache2 && apt clean && rm -rf /var/lib/apt/lists/*
       ENV APACHE_RUN_USER www-data
       ENV APACHE_RUN_GROUP www-data
       ENV APACHE_LOG_DIR /var/log/apache2
       EXPOSE 80
       ADD ["index.html","/var/www/html/"]
       ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

   y ejecutamos

       $ sudo docker build -t ana/apache2:1.0 .
       $ sudo docker images
       $ sudo docker run -d -p 80:80 --name servidor_web ana/apache2:1.0
       $ sudo docker ps -a

4. Aprovecharía nuestra imagen anterior para crear una imagen con PHP:

       FROM ana/apache2:1.0
       LABEL maintainer "bob@marley.org"
       RUN apt update && apt install -y php && apt clean && rm -rf /var/lib/apt/lists/*
       EXPOSE 80
       ADD ["index.php","/var/www/html/"]
       ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

   y ejecutamos

       $ sudo docker build -t bob/php:1.0 .
       $ sudo docker images
       $ sudo docker run -d -p 8080:80 --name servidor_php bob/php:1.0
       $ sudo docker ps -a


---


CUENTA EN DOCKER HUB
--------------------

Puedes crear una cuanta gratuita en <https://hub.docker.com/>

Una vez con cuenta puedes crear repositorios, permitiendo el uso de tus imágenes a todo el mundo ("públicos") o sólo para ti ("privados"). Un repositorio es donde metes las diferentes versiones de una imagen. Tu imagen en Docker Hub recibirá el nombre:

    nombre_usuario/nombre_repositorio:etiqueta

Puede parecer un poco lioso, ya que por deformación profesional tendemos a identificar repositorio con el almacén de imágenes, y ver las cosas de esta manera:

    nombre_repositorio/nombre_imagen:etiqueta

De una manera o de otra, si tu cuenta de usuario de Docker Hub es "pepito" y uno de tus repositorios es para una imagen de una aplicación llamada "mi_app", en Docker la última versión la ejecutarás con:

    $ sudo docker run pepito/mi_app:latest

Para [subir](https://docs.docker.com/engine/reference/commandline/push/) la imagen des de la línea de comandos de Docker debes haber [iniciado sesión](https://docs.docker.com/engine/reference/commandline/login/) con el comando `login`:

    $ sudo docker login
    $ sudo docker commit idcontenedor pepito/mi_app:latest
    $ sudo docker push pepito/mi_app:latest


---


EJERCICIO DE DOCKER
-------------------

En primer lugar, aquí hay webs con bastantes ejercicios que te recomiendo mirar:

 * <https://hamk-sysadmin-docker.github.io/exercises/>

 * <https://github.com/Vizuri/docker-exercises>

 * <https://dockerlabs.collabnix.com/>

En segundo lugar, un consejo: cuendo un contenedor no funcione y finalice tan pronto como lanzas su ejecución, puedes consultar lo que ha pasado con el comando `docker logs`.

En tercer lugar, te propongo un ejercicio. Vas a crear un grupo de contenedores que sirva una web. Para ello:

 1. A partir de una imagen de Debian, crea una imagen de un servidor web estático.

 2. A partir de la imagen anterior, crea  una imagen de un servidor web dinámico con PHP.

 3. Adicionalmente a partir de una imagen de Debian, crea una imagen de un servidor SQL MariaDB.

 4. Descarga y descomprime la web (por ejemplo, Wordpress) en el anfitrión.

 5. Crea un contenedor con la imagen del servidor web dinámico, y otro contenedor con la imagen del servidor SQL. Dichos contenedores compartirán una red propia, para que el puerto del servidor SQL sólo quede expuesto al servidor web.

    Para desacoplar el almacenamiento y facilitar las copias de seguridad, el contenedor web compartirá con el anfitrión la carpeta donde están las páginas web, y el contenedor SQL compartirá con el anfitrión la carpeta donde están las bases de datos. 

¿Te atreves a crear varios contenedores web y un contenedor balanceador de carga para repartir el trabajo entre ellos?


---


ORQUESTACION DE CONTENEDORES DOCKER
-----------------------------------

Docker pone en marcha aplicaciones o software en contenedores en varios entornos. Docker se basa en estándares abiertos y funciona en la mayoría de los entornos operativos más comunes, incluidos Linux, Microsoft Windows y otras infraestructuras locales o basadas en la nube.

Sin embargo, las aplicaciones en contenedores pueden ser complicadas. Durante la producción, muchas pueden requerir docenas o cientos de contenedores independientes. Es en este punto donde los entornos en tiempo de ejecución de contenedores, como Docker, se benefician del uso de otras herramientas para orquestar o gestionar todos los contenedores en funcionamiento.

Las herramientas que realizan orquestación de contenedores dirigen el comportamiento de los contenedores pudiendo automatizar el despliegue, la gestión y el escalado de las aplicaciones basadas en contenedores. Estas herramientas son necesarias en entornos en los que tenemos que manejar un sistema con muchos contenedores, que dan distintos servicios (base de datos, servidor web, métricas, la propia aplicación, ...) y desplegados sobre distintos servidores. Estos contenedores atienden una demanda determinada que tiene que ser satisfecha por unos recursos los cuales se tienen que escalar, actualizar, etc. sin repercutir en el usuario de la aplicación. Por tanto hay que controlar y dirigir la creación de contenedores, verificar su correcta ejecución, gestionar los errores,...

Ejemplos de orquestadores de contenedores son [Docker Compose](https://docs.docker.com/compose/), [Docker Swarm](https://docs.docker.com/engine/swarm/) y [Kubernetes](https://es.wikipedia.org/wiki/Kubernetes).


---


DOCKER COMPOSE
--------------

En el ejercicio anterior, que involucraba varios contenedores, habrás comprobado que el proceso de ejecutar o "levantar" a mano cada uno de ellos es tedioso.

Docker proporciona la utilidad Docker Compose, que aunque no se puede considerar un orquestador en sí mismo, permite definir y poner en marcha automáticamente varios contenedores relacionados entre ellos, a partir de un [fichero](https://docs.docker.com/compose/compose-file/) de [configuración](https://compose-spec.io/) `docker-compose.yml` escrito en formato [YAML](https://es.wikipedia.org/wiki/YAML).

El comando `docker-compose` en la versión 1, y `docker compose` en la versión 2, permite ejecutar operaciones en varios contenedores a la vez, como construir las imágenes, escalar el número de contenedores, reiniciar contenedores parados, etc.

La versión 2, más rápida y que viene integrada en Docker, es la que debes utilizar. Sin embargo, si dicha versión 2 no está disponible y necesitas la versión 1, puedes instalar esta última des de los repositorios:

    $ sudo apt update
    $ sudo apt install docker-compose

Un ejemplo de fichero `docker-compose.yml` para una imagen que se construye a partir de un *Dockerfile* que está en el mismo directorio:

    services:
      web:
        build: .
        ports:
          - "5000:80"
        volumes:
          - ./app:/codigo

Y para ejecutarlo cuando ya tienes el fichero creado, basta con escribir:

    $ sudo docker-compose up
    $ sudo docker ps -a

He aquí otro ejemplo de `docker-compose.yml` para un blog Wordpress con dos contenedores, uno con el servidor BBDD y otro con el servidor web:

    services:
      db:
        image: mariadb:latest
        restart: always
        environment:
          - MYSQL_ROOT_PASSWORD=contraseña
          - MYSQL_DATABASE=db_wordpress
          - MYSQL_USER=usuario_db_wordpress
          - MYSQL_PASSWORD=contraseña_db_wordpress
        networks:
          - mired
        volumes:
          - datos_db:/var/lib/mysql
      wordpress:
        image: wordpress:apache
        depends_on: db
        restart: always
        environment:
          - WORDPRESS_DB_HOST=db:3306
          - WORDPRESS_DB_USER=usuario_db_wordpress
          - WORDPRESS_DB_PASSWORD=contraseña_db_wordpress
          - WORDPRESS_DB_NAME=db_wordpress
        ports:
          - "8000:80"
        networks:
          - mired
        volumes:
          - ./code:/code
          - datos_wp:/var/www/html
    volumes:
      datos_db:
      datos_wp:
    networks:
      mired:
        driver: bridge

Este último ejemplo de `docker-compose.yml` levantará varios servidores web con balanceo de carga. Para la prueba, debes crear un fichero `index.php` en el mismo directorio, con el contenido `<?php phpinfo(); ?>` o bien `<?php echo "IP ".$_SERVER["SERVER_ADDR"]; ?>` , que mostrará la IP del equipo. Fíjate que la línea `ports` no asigna el puerto 80 a ningún puerto externo en concreto, lo que hará que el puerto del anfitrión asociado sea aleatorio. Fíjate que compartimos la carpeta donde estará la página web que hemos creado. Fíjate en la carpeta compartida `/var/run/docker.sock` del balanceador, que le permitirá obtener información de los servidores web levantados:

    services:
      web:
        image: php:8.3-apache
        ports:
          - 80
        volumes:
          - .:/var/www/html
      balanceador:
        image: dockercloud/haproxy
        ports:
          - 8888:80
        links:
          - web
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock

Podemos levantar cuatro servidores web con:

    $ sudo docker-compose up -d --scale web=4
    $ sudo docker-compose ps

El balanceador nos redirigirá a uno u otro nodo (-comprueba la IP mostrada por la página web-) en cada recarga de la dirección <http://localhost:8888/> .

Otros buenos ejemplos comentados se encuentran en <https://docs.docker.com/compose/gettingstarted/> .

Y unos cuantos ficheros Docker Compose ya preparados se encuentran en <https://github.com/docker/awesome-compose> .


---


DOCKER SWARM
------------

Docker proporciona la utilidad Docker Swarm, que maneja grupos ("clusters") de contenedores ("nodos"), permitiendo de manera sencilla que dichos grupos de contenedores ("swarm") se vean como un único contenedor "virtual".

Los comandos `docker swarm` y `docker node` permiten a los usuarios ejecutar el swarm, listar nodos del clúster, actualizar nodos, borrarlos, etc. 

<https://docs.docker.com/engine/swarm/key-concepts/>

<https://docs.docker.com/get-started/swarm-deploy/>

<https://docs.docker.com/engine/swarm/swarm-tutorial/>


---


KUBERNETES
----------

Kubernetes es un "orquestador" de contenedores que permite el despliegue, escalado y balanceo de carga automáticos. Tenemos otros orquestadores, como Nomad, Openshift, etc. pero Kubernetes es el más extendido.

Kubernetes aporta mecanismos que depliegan, mantienen y escalan aplicacions basándose en carga de la CPU, de la memoria u otras métricas a medida. Los componentes de kubernetes, así como las extensiones y contenedores, utilizan la API de Kubernetes. Los componentes de Kubernetes se dividen entre los que manejan nodos y los componentes del plano de control.

![](https://upload.wikimedia.org/wikipedia/commons/b/be/Kubernetes.png)

<https://cloud.google.com/kubernetes-engine/kubernetes-comic>

<https://kubernetes.io/docs/tutorials/kubernetes-basics/>

<https://docs.docker.com/get-started/kube-deploy/>


---


TEMPORAL - SEGURIDAD
--------------------

En una instalación normal de Docker, los usuarios no administradores que necesitan lanzar contenedores pertenecen al grupo *docker*. Hay que ir con mucho cuidado, pues el demonio de Docker ejecuta los contenedores como administrador, y eso quiere decir que dichos usuarios a través de los contenedores pueden acabar manipulando el anfitrión de maneras que inicialmente no tenían permitidas. Veamos un ejemplo:

    $ docker run -it --rm -v /:/host alpine cat /host/etc/shadow

Existen varias soluciones:

 * No tener dichos usuarios, y que tan sólo administradores puedan ejecutar contenedores. Obviamente, esto no será siempre posible.

 * Instalar Docker [rootless](https://docs.docker.com/engine/security/rootless/). En dicha instalación no hace falta permisos administrativos para lanzar contenedores, sino que se ejecutan con los permisos del usuario en cuestión. Sin embargo, no todas las características de Docker estarán disponibles, ya que para ciertos tipos de dispositivo o de configuración de red de Docker hacen falta privilegios administrativos.

 * Modificando el campo `userns-remap` del fichero `/etc/docker/daemon.json` podemos proteger el sistema de ficheros raiz.

Cambiando de tema, pero también relacionado con la seguridad, hay que mencionar que existen analizadores de vulnerabilidades especializados en contenedores. Se trata de aplicaciones que buscan problemas de seguridad en las imágenes que hemos creado o que utilizaremos. Por ejemplo, están [Clair](https://quay.github.io/clair/) y [Trivy](https://trivy.dev/).

Ejemplo (-que no he probado-) de instalación y posterior uso de Clair para el análisis de una imagen llamada *dvwa* ("Damn Vulnerable Web Application") del repositorio *infoslack*.

    $ mkdir -p clair/docker-compose-data/clair-config
    $ wget https://raw.github.com/jgsqware/clairctl/master/docker-compose.yml --directory-prefix=clair/docker-compose-data/
    $ wget https://raw.github.com/jgsqware/clairctl/master/docker-compose-data/clair-config/config.yml --directory-prefix=clair/clair-config/
    $ cd clair/docker-compose-data
    $ docker-compose up

    $ docker pull infoslack/dvwa
    $ docker-compose exec clairctl clairctl analyze -l infoslack/dvwa

Y en este enlace tienes unos buenos [apuntes de Trivy](https://raul-profesor.github.io/Curso-especialista-ciberseguridad/segdef/trivy/).


---


TEMPORAL - A REVISAR
--------------------

 * [Contenedores para intrusión en redes](https://houdini.secsi.io/)

 * [Contenedor proxy para TOR](https://www.elladodelmal.com/2020/04/aplicaciones-practicas-de-docker-en.html)

 * [Contenedor para crackear contraseñas](https://www.elladodelmal.com/2020/05/aplicaciones-practicas-de-docker-en.html)

 * [Fortificar contenedores en Kubernetes](https://www.elladodelmal.com/2020/04/como-fortificar-containers-en.html)

 * [Seguridad "container breakout"](https://www.google.com/search?q=container+breakout)

 * [Seguridad "docker breakout"](https://www.google.com/search?q=docker+breakout)

 * [Seguridad "docker security"](https://www.google.com/search?q=docker+security)

 * [Seguridad "hardening docker"](https://www.google.com/search?q=hardening+docker)

 * [Aplicaciones gráficas en contenedores](https://www.baeldung.com/linux/docker-container-gui-applications)
