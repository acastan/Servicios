PREGUNTAS
---------

 01. ¿Qué es un codec? ¿Qué diferencia hay entre codec y contenedor? ¿Es MP3 un codec, o un contenedor? ¿Es MP4 un codec, o un contenedor?

 02. ¿Qué es streaming de audio y vídeo? ¿Qué protocolos se suelen utilizar para el streaming?

 03. ¿Qué es podcast?

 04. ¿Viene algún software de servidor de streaming con Windows Server? ¿Dónde? ¿Cuál es el servidor de streaming comercial más conocido para Windows?

 05. ¿Cuáles son los servidores de streaming más conocidos para Unix/Linux?

 06. Al instalar un servidor de streaming, ¿Qué parámetros a configurar piensas que serán los más importantes?

 07. ¿Qué clientes y servidores de videoconferencia conoces para Linux?

 08. ¿Qué és webconferencia o webinar, y que servidor de webconferencia conoces para Linux?
 
 09. ¿Qué es GNU Jami?





PRÁCTICA WINDOWS
----------------

  - Desde el reproductor multimedia VLC realizaremos broadcast de vídeo a otros ordenadores que también tengan el reproductor VLC instalado.





PRÁCTICAS LINUX
---------------

**Streaming**

  - Instalaremos y configuraremos el servidor de streaming [Icecast](https://icecast.org/). Utilizaremos clientes para acceder al contenido multimedia.
    
    <https://www.howtoforge.com/linux_webradio_with_icecast2_ices2>
    <https://manuais.iessanclemente.net/index.php/Instalacion_de_Servidor_de_Audio_en_Debian>

  - Instalaremos y configuraremos el servidor de streaming [Ampache](https://ampache.org/). Utilizaremos clientes para acceder al contenido multimedia.

    <https://www.howtoforge.com/how-to-install-the-ampache-music-streaming-server-on-ubuntu-2004/>

  - Instalaremos y configuraremos los servidores de radio por internet [Airtime](https://www.sourcefabric.org/software/airtime) o [Rivendell](http://www.rivendellaudio.org/). Utilizaremos navegadores para acceder a nuestra estación de radio.

    <http://hackerpublicradio.org/eps.php?id=0845>

    <http://www.muylinux.com/2012/06/06/airtime-montate-una-emisora-de-radio-totalmente-open-source/>

    <http://rrabuntu.sourceforge.net/>

**Videoconferencia**

  - Instalaremos y configuraremos el servidor de webconferencia [OpenMeetings](https://openmeetings.apache.org/). Accederemos con navegadores para realizar una webconferencia en clase.

    <https://cwiki.apache.org/confluence/download/attachments/27838216/Installation%20OpenMeetings%207.0.0%20on%20Debian%2011.pdf>
    
    <https://github.com/openmeetings/openmeetings-docker>

  - Instalaremos y configuraremos el servidor de webconferencia [BigBlueButton](https://bigbluebutton.org/). Accederemos con navegadores para realizar una webconferencia en clase.

    <https://www.digitalocean.com/community/tutorials/how-to-install-bigbluebutton-on-ubuntu-16-04>

  - Instalaremos y configuraremos el servidor de webconferencia [Jitsi](https://jitsi.org/). Accederemos con navegadores para realizar una webconferencia en clase.

    <https://www.howtoforge.com/how-to-install-jitsi-video-conference-on-debian-11/>
    
    <https://cloudinfrastructureservices.co.uk/how-to-install-jitsi-meet-on-debian-11-video-conferencing-server/>

    <https://www.digitalocean.com/community/tutorials/how-to-install-jitsi-meet-on-ubuntu-22-04>

    <https://jitsi.org/downloads/ubuntu-debian-installations-instructions/>

    <https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-quickstart/>

  - Instalaremos y configuraremos el servidor de audioconferencia [TeamSpeak](https://www.teamspeak.com/). Accederemos con navegadores para realizar una webconferencia en clase.

    <https://www.howtoforge.com/how-to-install-teamspeak-server-on-debian-11/>
    
Si estás en clase, con varias webcams en clase, organiza una videoconferencia de grupo alojada en tu servidor.

Si estás en casa y sólo tienes una webcam u ordenador, organiza una videoconferencia entre tu ordenador y un teléfono móvil, alojada en tu servidor.

Si estás en casa y no tienes webcam, organiza una videoconferencia entre dos teléfonos móviles, alojada en tu servidor.

Extra: si estás en casa y consigues abrir puertos en tu router para que tu servidor de videoconferencias sea accesible des de el exterior, avísanos para que la clase nos encontremos virtualmente por videoconferencia alojada en tu servidor. Si tu servidor no és muy potente, podemos ser unos pocos y sólo con áudio.

**Otros**

  - Una empressa vol emetre un streaming d'audio/video als seus 150 ordinadors, a més d'establir un sistema de videovigilància. Escolliu una de les dues idees i implementeu un exemple pràctic.

    La idea (streaming) es que des de qualsevol ordinador de la empresa, connectem una webcam, executem els passos indicats i des de qualsevol altre ordinador es pot veure el vídeo en directe.

    L'altre idea (videovigilància) es que connectarà diverses webcams en alguns ordinadors i monitoritzarà i grabarà el que passa. Evidentment hi haurà d'haver algun filtre de seguretat (contrasenya,...).

  - Nginx + RTMP + OBS + VLC + HTML5:

    <https://www.josedomingo.org/pledin/2020/07/streaming-video-software-libre/>

    <https://www.digitalocean.com/community/tutorials/how-to-set-up-a-video-streaming-server-using-nginx-rtmp-on-ubuntu-20-04>
    
    <https://www.howtoforge.com/how-to-set-up-a-video-streaming-server-using-nginx-rtmp-on-ubuntu-22-04/>





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Codec>

  - <http://en.wikipedia.org/wiki/Container_format_(digital)#Multimedia_container_formats>

  - <http://en.wikipedia.org/wiki/Comparison_of_container_formats>

  - <http://en.wikipedia.org/wiki/Comparison_of_audio_codecs>

  - <http://en.wikipedia.org/wiki/Comparison_of_video_codecs>

  - <http://en.wikipedia.org/wiki/Streaming_media>

  - <http://en.wikipedia.org/wiki/Comparison_of_streaming_media_systems>

  - <http://en.wikipedia.org/wiki/Podcast>

  - <http://en.wikipedia.org/wiki/Comparison_of_web_conferencing_software>
