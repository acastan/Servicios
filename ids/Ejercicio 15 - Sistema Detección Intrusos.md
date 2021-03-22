PREGUNTAS
---------

 01. ¿En qué consiste un sistema de detección de intrusos (IDS)? ¿Qué diferencias hay con un cortafuegos?

 02. ¿Qué diferencia hay entre un IDS de red y un IDS de host? ¿Cuáles son las ventajas y desventajas de uno y de otro?

 03. ¿Qué diferencia hay entre un IDS basado en firmas y un IDS basado en anomalías? ¿Cuáles son las ventajas y desventajas de uno y de otro?

 04. ¿Qué técnicas permiten evadir un IDS?

 05. ¿Cuál es el software de IDS más conocido para Unix/Linux?

 06. ...

 07. ...

 08. ...

 09. ...

 10. ...





REPASO DE LA SINTAXIS DE REGLAS DE SNORT
----------------------------------------

Las reglas de Snort se dividen en dos partes: cabecera y opciones. En la cabecera se indica la acción asociada a una regla, el tipo de paquete, las direcciones origen y destino, así como los puertos utilizados. La estructura de la cabecera es la siguiente:

    <acción> <protocolo> <red origen> <puerto origen> <dirección> <red destino> <puerto destino>

Se pueden utilizar cinco tipos de acciones:

  - Log: se genera sólo la información de registro asociada al contenido del paquete.

  - Alert: se genera una alerta y un log del paquete que activa la regla.

  - Pass: deja pasar el paquete asociado a la regla si registrar un log.

  - Activate: genera una alerta y la activación de una regla dinámica (dynamic)

  - Dynamic: es una regla que está inactiva hasta que se activa con un activate. Tiene como objetivo ofrecer información adicional a la que se obtendría con la regla inicial a la que está asociada.

En las opciones se especifica qué información se debe encontrar en un paquete para que se active la acción asociada a la regla. Se escriben todas dentro de un paréntesis y puede haber una o más opciones separadas por un ’;’. Hay cuatro categorías para estas opciones:

  - Generales: msg, reference, gid, sid, classtype, rev, etc... Dan información sobre la regla pero no afectan a la detección.

  - Detección de contenido: content, nocase, rawbytes, depth, offset, distance, uircontent, etc... Buscan patrones dentro de la carga útil del paquete.

  - Detección non-payload: fragoffset, ttl, tos, id, ipopts, fragbits, etc... Busca patrones en otros campos del paquete queno sean la carga útil.

  - Postdetección: logto, session, resp, react, tag, activates, etc... Permiten activar reglas específicas que ocurren despuésde que se haya ejecutado la regla





EJERCICIO CON SNORT O SURICATA
------------------------------

 01. Añade reglas al IDS para detectar escaneos horizontales y verticales. Pruébalas realizando un escaneo con Nmap. ¿Cómo sería un escaneo que burle dichas reglas?

 02. Añade reglas al IDS para que detecte ARP spoofing. Pruébalo con Bettercap.

 03. Tu jefe quiere saber si los empleados hablan de él. Añade reglas al IDS para que detecte la cadena "jefe" en cualquier paquete TCP o UDP.

 04. Están intentando conseguir contraseñas de algunos de tus servicios, por ejemplo SSH, probando las contraseñas de un diccionario. Añade reglas al IDS para que detecte dichos ataques. Pruébalo con Hydra o xHydra.

 05. Están realizando un ataque DOS sobre tu servidor web mediante Syn Flooding. Añade reglas al IDS que detecten dicho ataque. Pruébalo con `hping3 -i u1 -S- p 80 IP_servidor_a_atacar` . Si quieres puedes capturar el tráfico con Wireshark para ver el ataque. Si quieres puedes configurar al IDS para que añada una regla a tu cortafuegos bloqueando la IP del ataque.





PRÁCTICA
--------

Descarga una máquina llena de vulnerabilidades a atacar, por ejemplo [Metaesploitable 3](https://github.com/rapid7/metasploitable3). Escaneala con Nmap y Nessus.¿Qué puertos, servicios y vulnerabilidades has descubierto? Atácala con Metasploit. Intenta detectar los diferentes ataques con reglas de Snort o Suricata.





REFERENCIAS
-----------

  - <https://en.wikipedia.org/wiki/Intrusion_detection_system>

  - <http://openaccess.uoc.edu/webapps/o2/bitstream/10609/43090/6/osanchezloTFM0715memoria.pdf>
