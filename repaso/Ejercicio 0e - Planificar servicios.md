PROBLEMÁTICA
------------

Nuestro centro educativo ha ido creciendo en los últimos años. Actualmente el número de profesores y alumnos es elevado y todos utilizan las nuevas tecnologías de la información en su tarea diaria.

También ha crecido el número de equipos informáticos puestos a disposición de la comunidad educativa, tanto en número de equipos por aula, como en número de aulas y departamentos. El número de alumnos que pasa por ellas es elevado y las diferentes configuraciones, fruto de la utilización inadecuada de los equipos, dificultan las tareas de mantenimiento y de aprendizaje.

Se dispone de la instalación física de la red, pero no se obtiene el rendimiento adecuado de la misma, ni se explota al máximo su estructura.

Por todo ello, y como responsables de las TIC en el centro, decidís reestructurar el sistema de información interno, para crear una verdadera intranet y poder administrarla, dado que la situación actual resulta poco manejable.





ESQUEMA HARDWARE
----------------

El centro dispone de ordenadores para el alumnado ubicados en varias aulas informáticas, así como también de ordenadores para el profesorado, repartidos en los despachos de Dirección y en los espacios departamentales.

El cableado de la red física del centro ya se encuentra instalado. Su topología es en estrella, formando una única red física y lógica.

Salida a Internet con fibra óptica.





ESQUEMA SOFTWARE
----------------

Los ordenadores de las aulas de informática son recientes, por lo que disponen de más memoria RAM. En ellos se instalará Linux. Este sistema operativo puede comportarse también como un potente cliente de red que se comunicará perfectamente con el servidor.

Los ordenadores de los departamentos didácticos son más antiguos pero no queremos renunciar a las prestaciones de un cliente de red potente y seguro, por lo que se instalará también Linux. Si el hardware es demasiado obsoleto cabe la posibilidad de utilizarlo como terminal para conectarse por escritorio remoto directamente al servidor.

Para conseguir la integración de todos los equipos se utilizará un nuevo equipo que será el servidor. Sobre él se instalará un sistema operativo servidor, que también será Linux. Éste será el centro de la Intranet y a través de él, se accederá a Internet. 





PREGUNTAS
---------

 01. Fruto del crecimiento informático del centro y de la utilización cada vez más frecuente de dichos recursos informáticos resulta que la información se encuentra fragmentada en muchos lugares, el acceso a ella es complejo y lento y, en multitud de ocasiones se accede a información desfasada o ésta se ha perdido. ¿Qué actuaciones harías?

 02. Es fundamental que el servidor sea un equipo al que no se pueda acceder para ejecutar programas o para realizar una tarea urgente. Sin embargo, es un hecho que se accede a los ordenadores críticos (secretaría, dirección, administración, etc) para urgencias de impresión, consultas u otras causas, con el consiguiente peligro de corrupción y borrado accidental de archivos. ¿Qué actuaciones harías?

 03. Por otro lado, tanto el profesorado como el alumnado acostumbran a personalizar su escritorio, incluyendo accesos directos, carpetas y demás vínculos que considera importantes y cómodos en su tarea diaria. Pero todo ésto incomoda en muchas ocasiones a otros usuarios que también utilizan el mismo equipo. Esta situación es especialmente patente en las aulas de informática, donde parece que el alumnado compite en crear ámbitos de trabajo extravagantes e inútiles, con la consecuente pérdida de tiempo en la carga del sistema operativo. ¿Qué actuaciones harías?

 04. En algunos momentos el tráfico de la red es enorme, habiéndose detectado problemas de congestión sin saber el motivo y consecuentemente, sin poder tomar medidas para restablecer la normalidad. También se ha observado la tendencia a los cambios de configuración del alumnado de las direcciones IP, máscaras, puertas de enlace y direcciones DNS asignadas, lo que conlleva problemas de conectividad e inseguridad. Volver a realizar las configuraciones lleva demasiado tiempo. En ocasiones se produce el cambio de direcciones DNS por parte del proveedor, lo que implica un periodo de tiempo importante sin conexión, hasta conseguir volver a configurar totalmente los equipos. ¿Qué actuaciones harías?

 05. El secretario del centro reiteradamente ha advertido que el gasto en fotocopias es elevado y, por lo tanto, es necesario tener un control de lo que se imprime y de su destino. Recientemente se ha suscrito un contrato con una empresa de reprografía que ha instalado en alquiler una impresora de red y se quiere que una gran parte de la impresión se realice a través de dicha impresora, dadas las ventajas económicas que supone frente al coste de los fungibles de las impresoras locales. ¿Qué actuaciones harías?

 06. La información existente debe ser salvaguardada de los desastres que habitualmente ocurren: virus, fallos de hardware, borrados accidentales y/o provocados, etc., máxime cuando se está llevando a cabo un sistema centralizado de información donde, además de los datos generales, se almacenan los perfiles y las carpetas personales de los usuarios. ¿Qué actuaciones harías?

 07. Muchos profesores se encuentran realizando cursos de aprendizaje y perfeccionamiento relacionados con las Nuevas Tecnologías (cursos de html, php, mysql, etc) y necesitan soporte para su desarrollo. ¿Qué actuaciones harías?

 08. Se ofrecerá a los profesores, como complemento a los Servicios Web prestados a los usuarios del centro, acceso a carpetas privadas y seguras (acceso https) disponibles vía web mediante autentificación. ¿Qué actuaciones harías?





PRÁCTICA
--------

  - Con la herramienta de diagramas Dia, crear un esquema de la red local, donde aparezca router, switches, servidores con nombre de servicios, y máquinas cliente.

  - A las máquinas virtuales que creamos en el ejercicio anterior, configurad su modo de trabajo en red interna.





REFERENCIAS
-----------

  - <http://en.wikipedia.org/wiki/Proxy_server>

  - <http://en.wikipedia.org/wiki/Network_address_translation>

  - <http://en.wikipedia.org/wiki/SOCKS>

