RESUMEN DE CONTENEDORES Y DOCKER
================================

Esta es una introducción a contenedores y a Docker por parte de alguien -yo mismo- no muy versado en estos temas.

Te recomiendo que visites:

 * [Curso sobre Docker](https://sergarb1.github.io/CursoIntroduccionADocker/)

 * [Documentación de Docker](https://docs.docker.com/)

 * [Resumen con algunos gráficos que me gustan](https://betterprogramming.pub/docker-for-front-end-developers-c758a44e622f)


---


CONTENEDORES
------------

La virtualización basada en contenedores es un método de virtualización en el que sobre el núcleo del sistema operativo se ejecutan mecanismos de aislamiento que permiten que existan múltiples instancias aisladas de espacios de usuario, en lugar de solo uno. Dichas instancias, llamadas contenedores o jaulas, pueden verse como un servidor real desde el punto de vista de sus usuarios. Las actividades de un contenedor no tienen impacto sobre otros contenedores. 

Al software que permite el alojamiento de distintos contenedores se le llama motor de contenedores.

Veámoslo con una imagen, que vale más que mil palabras:

![](https://www.softwaretestinghelp.com/wp-content/qa/uploads/2018/09/1.Containerization-vs-Virtualization.png)

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

Docker se instala en un servidor que llamamos "Docker Engine". Se accede mediante un cliente por línea de comandos, pero también hay clientes gráficos como [Portainer](https://www.portainer.io/) y [Docker Desktop](https://www.docker.com/products/docker-desktop/).

![](https://docs.docker.com/engine/images/architecture.svg)

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that lets you work with applications consisting of a set of containers.

 * The *Docker daemon* (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

 * The *Docker client* (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

 * A *Docker image* is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

   You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

 * A *Docker container* is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

   By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

   A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

 * The *Docker registry* stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry. When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

 * The *Docker Desktop* is an easy-to-install application that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper.

Docker se puede integrar con diferentes herramientas de infraestructura, como Amazon Web Services, Ansible, Cfengine, Chef, Google Cloud Platform, DigitalOcean, IBM Bluemix, Jelastic, Jenkins, Microsoft Azure, OpenStack Nova, OpenSVC, Puppet, Salt, y Vagrant.


---


IMÁGENES Y CONTENEDORES
-----------------------

Imágenes:

 * La imagen es una plantilla de solo lectura que se utiliza para crear contenedores, que son las "máquinas virtuales" en ejecución. A partir de una imagen pueden crearse múltiples contenedores.

 * Las imágenes, además de tener su sistema de ficheros predefinido, tienen una serie de parámetros predefinidos (comandos, de variables de entorno, etc.) con valores por defecto y que se pueden personalizar en el momento de crear el contenedor.

 * Docker permite crear nuevas imágenes basándose en imágenes anteriores. Se podría decir que una imagen puede estar formada por un conjunto de “capas” que han modificado una imagen base. Al crear una nueva imagen, simplemente estamos añadiendo una capa a la imagen anterior, la que actúa como base.

Contenedores:

 * Son instancias de una imagen.

 * Pueden ser arrancados, parados y ejecutados.

 * Cada contenedor Docker posee un identificador único de 64 caracteres, pero habitualmente se utiliza una versión corta con los primeros 12 caracteres.

 * Cuando se lanza la ejecución de un contenedor Docker, dicho contenedor ejecuta un comando ("punto de entrada"). Una vez dicho comando finaliza, se para el contenedor. Este comportamiento puede liar a los usuarios primerizos, ya que algunos contenedores ejecutaran un comando que finaliza rápido y se pararán, mientras que otros ejecutarán un demonio, como por ejemplo un servidor web, que no finaliza y por lo tanto no para la ejecución del contenedor.


---


REDIRECCIONAMIENTO DE PUERTOS Y PERSISTENCIA
--------------------------------------------

Las IPs a los contenedores se asignan dinámicamente por Docker. En general no se suele trabajar con IPs para los contenedores, sino que si tenemos un servicio ejecutándose en un contenedor [mapearemos puertos del contenedor a puertos del anfitrión](https://docs.docker.com/config/containers/container-networking/) y Docker ya se encargara de redireccionar el tráfico de red.

Recuerda que el sistema operativo no permite dos aplicaciones utilizar el mismo puerto a la vez, ni permite usar puertos por debajo del 1024 a usuario no privilegiados.

![Imágenes y contenedores](https://bytes.cat/_media/docker5.png)

Para compartir datos entre contenedores o entre el anfitrión y los contenedores, podemos [mapear directorios del anfitrión al contenedor](https://docs.docker.com/storage/bind-mounts/) o utilizar [volúmenes](https://docs.docker.com/storage/volumes/).

Los directorios se pueden enlazar en modo de lectura-escritura, pero también en modo de sólo lectura, si queremos asegurarnos que los contenedores no puedan realizar cambios en los datos.

Enlazar a un volumen de Docker es similar a enlazar a un directorio del anfitrión, con la diferencia de que en el volumen Docker no nos tenemos que preocupar dónde está almacenado en el anfitrión.

Por último, en caso que por seguridad queramos que todo el sistema de ficheros del contenedor sea de sólo lectura, pero necesite escribir alguna cosa para funcionar, podemos [montar en memoria](https://docs.docker.com/storage/tmpfs/) dicho directorio donde deba escribir.

![Persistencia](https://bytes.cat/_media/docker-volumes.png)

En este ejemplo, tres contenedores enlazan los puertos que quieren exponer con puertos del anfitrión. Por otro lado, dichos contenedores también enlazan algunos de sus directorios a directorios del anfitrión.

![Publicar puertos](https://bytes.cat/_media/docker6.png)


---


INSTALAR DOCKER
---------------

Se puede instalar mediante un script:

    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

Pero también se puede instalar mediante repositorios. Por ejemplo, esta fórmula es para mi Debian estable:

    sudo apt update
    sudo apt install ca-certificates curl gnupg lsb-release

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io

En cualquiera de los dos casos, comprueba que se instaló y funciona:

    sudo docker run hello-world
    sudo docker version
    sudo docker info

Para administrar contenedores gráficamente des de un navegador puedes instalar Portainer, que es un contenedor con una aplicación web:

    docker volume create portainer_data
    docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always \
        -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data \
        portainer/portainer-ce:latest

    docker ps

    <https://localhost:9443>

Para una instalación "rootless" de Docker, consulta <https://docs.docker.com/engine/security/rootless/>.


---


COMANDOS DE DOCKER SOBRE CONTENEDORES
-------------------------------------

Los comandos que ahora resumo se pueden ejecutar también como subcomandos del comando [`docker container`](https://docs.docker.com/engine/reference/commandline/container/). Por ejemplo, listar contenedores con `docker ps` es equivalente a `docker container ls`.

![](https://miro.medium.com/max/700/0*3_uIz_YMiyZxMwKn)

 * [Crear un nuevo contenedor y ejecutarlo](https://docs.docker.com/engine/reference/commandline/run/):

       docker run [opciones] imagen [comando] [argumentos]

   Por ejemplo:

       docker run -d -p 80:80 docker/getting-started
       docker run -it -e MENSAJE=HOLA poweroff --rm --name=mi_Ubuntu ubuntu /bin/bash
       docker run -d -p 8080:80 nginx

   Si la imagen (la "plantilla") no está en nuestro equipo, por defecto se descarga de [Docker Hub](https://hub.docker.com/), que es el registro público que proporciona Docker Inc.

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

Chuletas de comandos:

 * <https://docs.docker.com/get-started/docker_cheatsheet.pdf>

 * <https://raw.githubusercontent.com/sergarb1/CursoIntroduccionADocker/main/FuentesCurso/Docker%20CheatSheet%20COMPLETA.pdf>

Ejemplos:

1. Lanzamos un contenedor con [noVNC](https://novnc.com/) y nos conectamos vía navegador:

       docker run --rm -it -p 8080:8080 theasp/novnc

       <http://localhost:8080/vnc.html>

2. Lanzamos un contenedor Ubuntu con una shell preparada para ejecutar comandos ¿Qué núcleo del s.o. y qué procesos ves en el contenedor? :

       docker run -it --name ejercicio ubuntu /bin/bash
       uname -a
       ps -ef

   Si desacoplamos la entrada, podemos ver la misma información del contenedor des del anfitrión, con otros comandos:

       CTRL-P CTRL-Q
       docker exec ejercicio uname -a
       docker top ejercicio
       docker attach ejercicio

   Cuando salimos con el comando `exit` el contenedor se para ¿Qué núcleo del s.o. ves en el anfitrión? :

       exit
       docker ps -a
       uname -a

   Para volver a acceder a la línea de comandos, arrancamos de nuevo el contenedor:

       docker start -ai ejercicio


---


COMANDOS SOBRE SISTEMA DE FICHEROS
----------------------------------

Los contenedores trabajan con sistema de ficheros *Union File System* (UFS). Los cambios en el contenedor no modifican el anfitrión, sino que crean una nueva "capa" en el contenedor con los cambios.

Si al cabo de un tiempo necesitamos saber qué cambios se han producido en el contenedor podemos utilizar el comando `docker diff contenedor`. Las líneas que muestra que comienzan con ...

 * con 'A' significa que se ha añadido
 * con 'C' significa que se ha cambiado 
 * con 'D' significa que se ha borrado

Además, los contenedores se pueden ejecutar en modo de sólo lectura con el atributo `--read-only`, lo que asegura que ningún dato en el contenedor es modificado.

Ejemplo:

1. Este script crea y lanza Wordpress, utilizando un contenedor con un servidor web y otro contenedor con un servidor de bases de datos. El contenedor con Wordpress es de sólo lectura, pero mantiene el directorio /tmp de escritura, y también mantiene en escritura el directorio /run/apache2/ montado en el volumen por defecto del anfitrión, para que Apache funcione:

       #!/bin/sh
       DB_CID=$(docker run -d -e MYSQL_ROOT_PASSWORD=pedralbes mysql:5.7)
       WP_CID=$(docker run -d --link $DB_CID:mysql -p 80:80 --read-only -v /run/apache2/ --tmpfs /tmp wordpress:6.0.3-php7.4-apache)

Ejercicio:

1. Lanza la ejecución de un contenedor creado a partir de una imagen oficial de PHP con Apache, que tenga su carpeta /var/www/html mapeada a la carpeta del anfitrión donde guardas tus ejercicios de PHP.

   Solución en formato largo:

       $ docker run -d -p 8000:80 --name php --mount type=bind,source=/dades/dades/IAW/,target=/var/www/html/ php:7.4-apache

   Solución en formato breve:

       $ docker run -d -p 8000:80 --name php -v /dades/dades/IAW/:/var/www/html/                              php:7.4-apache


---


COMANDOS SOBRE RED
------------------

All containers without a --network specified, are attached to the default bridge network. This can be a risk, as unrelated stacks/services/containers are then able to communicate.

Using a user-defined network provides a scoped network in which only containers attached to that network are able to communicate.

During a container’s lifetime, you can connect or disconnect it from user-defined networks on the fly. To remove a container from the default bridge network, you need to stop the container and recreate it with different network options.

Containers connected to the same user-defined bridge network effectively expose all ports to each other

docker network create mi_red
docker network ls
docker network rm mi_red

$ docker create --name mi-nginx --network mi_red --publish 8080:80 nginx:latest

Pero si el contenedor ya se ejecutaba:

$ docker network connect mi_red mi-nginx

$ docker network disconnect mi_red mi-nginx

<https://www.google.com/search?q=communication+containers+docker>


---


COMANDOS DE DOCKER SOBRE IMÁGENES
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


CREACIÓN DE IMÁGENES DOCKER
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
       MAINTAINER yomismo
       RUN apt update && apt -y install telnet
       CMD ["/usr/bin/telnet", "towel.blinkenlights.nl"]

   Y ahora ejecuta:

       docker build -t starwars .
       docker run -it starwars

2. A partir de una Debian, instala cowsay, y dice algo en ASCII Art:

       FROM debian:latest
       MAINTAINER tumismo
       RUN apt update && apt -y install cowsay
       ENTRYPOINT ["/usr/games/cowsay"]
       CMD ["Docker mooooooola!"]

   Y ahora ejecuta:

       docker build -t cowsay .
       docker run -it cowsay

3. Crea una imagen con Apache:

       FROM debian
       MAINTAINER Ana Cardo "ana@mired.org"
       RUN apt update && apt install -y apache2 && apt clean && rm -rf /var/lib/apt/lists/*
       ENV APACHE_RUN_USER www-data
       ENV APACHE_RUN_GROUP www-data
       ENV APACHE_LOG_DIR /var/log/apache2
       EXPOSE 80
       ADD ["index.html","/var/www/html/"]
       ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

   y ejecutamos

       docker build -t ana/apache2:1.0 .
       docker images
       docker run -d -p 80:80 --name servidor_web ana/apache2:1.0
       docker ps -a

4. Aprovecharía nuestra imagen anterior para crear una imagen con PHP:

       FROM ana/apache2:1.0
       MAINTAINER Bob Marley "bob@mired.org"
       RUN apt update && apt install -y php && apt clean && rm -rf /var/lib/apt/lists/*
       EXPOSE 80
       ADD ["index.php","/var/www/html/"]
       ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

   y ejecutamos

       docker build -t bob/php:1.0 .
       docker images
       docker run -d -p 8080:80 --name servidor_php bob/php:1.0
       docker ps -a


---


CUENTA EN DOCKER HUB
--------------------

Puedes crear una cuanta gratuita en <https://hub.docker.com/>

Una vez con cuenta puedes crear repositorios, permitiendo el uso de tus imágenes a todo el mundo ("públicos") o sólo para ti ("privados"). Un repositorio es donde metes las diferentes versiones de una imagen. Tu imagen en Docker Hub recibirá el nombre:

    nombre_usuario/nombre_repositorio:etiqueta

Puede parecer un poco lioso, ya que por deformación profesional tendemos a identificar repositorio con el almacén de imágenes, y ver las cosas de esta manera:

    nombre_repositorio/nombre_imagen:etiqueta

De una manera o de otra, si tu cuenta de usuario de Docker Hub es "pepito" y uno de tus repositorios es para una imagen de una aplicación llamada "mi_app", en Docker la última versión la ejecutarás con:

    docker run pepito/mi_app:latest

Para [subir](https://docs.docker.com/engine/reference/commandline/push/) la imagen des de la línea de comandos de Docker debes haber [iniciado sesión](https://docs.docker.com/engine/reference/commandline/login/) con el comando `login`:

    docker login
    docker commit idcontenedor pepito/mi_app:latest
    docker push pepito/mi_app:latest


---


EJERCICIO DE DOCKER
-------------------

Vas a crear un grupo de contenedores que sirva una web. Para ello:

 1.  A partir de una imagen de Debian, crea una imagen de un servidor web estático.

 2.  A partir de la imagen anterior, crea  una imagen de un servidor web dinámico con PHP.

 3.  Adicionalmente a partir de una imagen de Debian, crea una imagen de un servidor SQL MariaDB.

 4.  Descarga y descomprime la web (por ejemplo, Wordpress) en el anfitrión.

 5.  Crea un contenedor con la imagen del servidor web dinámico, y otro contenedor con la imagen del servidor SQL. Dichos contenedores compartirán una red propia, para que el puerto del servidor SQL sólo quede expuesto al servidor web.

     Para desacoplar el almacenamiento y facilitar las copias de seguridad, el contenedor web compartirá con el anfitrión la carpeta donde están las páginas web, y el contenedor SQL compartirá con el anfitrión la carpeta donde están las bases de datos. 

¿Te atreves a crear varios contenedores web y un contenedor balanceador de carga para repartir el trabajo entre ellos?


---


ORQUESTACIÓN DE CONTENEDORES DOCKER
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

Para instalar la versión 2:

    $ DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
    $ mkdir -p $DOCKER_CONFIG/cli-plugins
    $ curl -SL https://github.com/docker/compose/releases/download/v2.12.2/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
    $ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
    $ docker compose version

Para instalarlo para todos los usuarios, en vez del usuario actual, cambia la anterior primera línea por:

    $ DOCKER_CONFIG=${DOCKER_CONFIG:-/usr/local/lib/docker}

Un ejemplo de fichero `docker-compose.yml`:

    services:
      web:
        build: .
        ports:
          - "8000:5000"
        volumes:
          - .:/code
      redis:
        image: redis

Y para ejecutarlo cuando ya tienes el fichero creado, basta con escribir:

    $ docker compose up
    $ docker ps -a

He aquí otro ejemplo de `docker-compose.yml`:

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

Un buen ejemplo comentado se encuentra en <https://docs.docker.com/compose/gettingstarted/>.

Y unos cuantos ficheros Docker Compose ya preparados se encuentran en <https://github.com/docker/awesome-compose>.


---


DOCKER SWARM
------------

Docker proporciona la utilidad Docker Swarm, que provides native clustering functionality for Docker containers, which turns a group of Docker engines into a single virtual Docker engine. Docker manages swarms using the Raft consensus algorithm. According to Raft, for an update to be performed, the majority of Swarm nodes need to agree on the update.

The docker swarm CLI utility allows users to run Swarm containers, create discovery tokens, list nodes in the cluster, and more. 

The docker node CLI utility allows users to run various commands to manage nodes in a swarm, for example, listing the nodes in a swarm, updating nodes, and removing nodes from the swarm.

<https://docs.docker.com/engine/swarm/key-concepts/>

<https://docs.docker.com/get-started/swarm-deploy/>

<https://docs.docker.com/engine/swarm/swarm-tutorial/>


---


KUBERNETES
----------

Kubernetes es un "orquestador" de contenedores que permite el despliegue, escalado y balanceo de carga automáticos. Tenemos otros orquestadores, como Nomad, Openshift, etc. pero Kubernetes es el más extendido.

Kubernetes defines a set of building blocks ("primitives") that collectively provide mechanisms that deploy, maintain, and scale applications based on CPU, memory or custom metrics. Kubernetes is loosely coupled and extensible to meet different workloads. The internal components as well as extensions and containers that run on Kubernetes rely on the Kubernetes API. The platform exerts its control over compute and storage resources by defining resources as Objects, which can then be managed as such.

Kubernetes follows the primary/replica architecture. The components of Kubernetes can be divided into those that manage an individual node and those that are part of the control plane.

![](https://upload.wikimedia.org/wikipedia/commons/b/be/Kubernetes.png)

<https://cloud.google.com/kubernetes-engine/kubernetes-comic>

<https://kubernetes.io/docs/tutorials/kubernetes-basics/>

<https://docs.docker.com/get-started/kube-deploy/>


---


TEMP (A AÑADIR)
---------------

 * [Ejercicios](https://www.google.com/search?q=docker+exercises)

 * [Contenedores para intrusión en redes](https://houdini.secsi.io/)

 * [Contenedor proxy para TOR](https://www.elladodelmal.com/2020/04/aplicaciones-practicas-de-docker-en.html)

 * [Contenedor para crackear contraseñas](https://www.elladodelmal.com/2020/05/aplicaciones-practicas-de-docker-en.html)

 * [Fortificar contenedores en Kubernetes](https://www.elladodelmal.com/2020/04/como-fortificar-containers-en.html)

 * [Seguridad "container breakout"](https://www.google.com/search?q=container+breakout)

 * [Seguridad "docker breakout"](https://www.google.com/search?q=docker+breakout)

 * [Seguridad "docker security"](https://www.google.com/search?q=docker+security)

 * [Seguridad "hardening docker"](https://www.google.com/search?q=hardening+docker)

 * [Aplicaciones gráficas en contenedores](https://www.google.com/search?q=hardening+docker)
