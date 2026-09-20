Test TCP/IP
===========

01. ¿Cuantos bytes tiene una dirección de IP versión 4?
    - [ ]  2
    - [x]  4
    - [ ]  32

02. ¿A qué clase pertenece la dirección 116.34.200.19?
    - [x]  A
    - [ ]  B
    - [ ]  C

03. Una dirección de clase C utiliza:
    - [x]  24 bits para la dirección de red y 8 bits para la dirección del equipo.
    - [ ]  16 bits para la dirección de red y 16 bits para la dirección del equipo.
    - [ ]  32 bits para la dirección de red y 0 bits para la dirección del equipo.
    - [ ]  24 bits para la dirección de red y 24 bits para la dirección del equipo.

04. La máscara de red sirve para obtener qué bits de una dirección IP identifican la red y qué bits identifican el equipo.
    - [x]  Cierto
    - [ ]  Falso

05. ¿Cuál de las siguientes representa la máscara de red por defecto para una red clase C?
    - [ ]  255.255.0.0
    - [ ]  255.255.232.0
    - [x]  255.255.255.0

06. ¿Cuántos equipos pueden existir en una red clase C?
    - [ ]  256
    - [x]  254
    - [ ]  128

07. ¿Para qué se utiliza el protocolo ARP en una red Ethernet?
    - [x]  Obtiene la dirección MAC de un nodo a partir de su dirección IP.
    - [ ]  Obtiene la dirección IP de un nodo a partir de su dirección MAC.
    - [ ]  Obtiene un protocolo a partir de su dirección IP.
    - [ ]  Obtiene el fabricante de la tarjeta de red a partir de su dirección MAC.

08. ¿Cuál es la función de ICMP?
    - [ ]  Establece la relación entre direcciones de IP y direcciones de MAC.
    - [ ]  Controla el flujo de información hacia el nodo destino.
    - [x]  Envia información de error y control entre nodos de la red.

09. ¿Cómo se transmiten los mensajes ICMP?
    - [ ]  En el área de datos de una trama Ethernet.
    - [ ]  En el área de datos de un segmento TCP.
    - [x]  En el área de datos de un datagrama IP.

10. ¿Cuál de las siguientes frases describe mejor a TCP?
    - [ ]  Protocolo de enlace punto a punto que soporta múltiples protocolos de red.
    - [ ]  Protocolo de transporte orientado a datagramas, sin conexión, no fiable.
    - [x]  Protocolo de transporte orientado a datagramas, con conexión, fiable.

11. ¿Cuál de las siguientes frases describe mejor a UDP?
    - [ ]  Protocolo de enlace punto a punto que soporta múltiples protocolos de red.
    - [x]  Protocolo de transporte orientado a datagramas, sin conexión, no fiable.
    - [ ]  Protocolo de transporte orientado a datagramas, con conexión, fiable.

12. ¿Cuál de los campos del encabezado de un segmento TCP se utiliza para identificar la cantidad de bytes que un nodo receptor está dispuesto a aceptar?
    - [ ]  Tiempo de vida.
    - [ ]  Secuencia.
    - [x]  Ventana.
    - [ ]  Versión.

13. El establecimiento de conexión en el protocolo TCP requiere la siguiente secuencia de señales en los primeros tres paquetes enviados: primero, la señales SYN/ACK; segundo, la señal SYN; y tercero, la señal ACK.
    - [ ]  Cierto
    - [x]  Falso

14. Un equipo que envío información mediante TCP, ¿cómo sabe que la información llegó?
    - [x]  Porque recibe una señal ACK del receptor de la información.
    - [ ]  Porque recibe un mensaje "ICMP de solicitud de eco" del receptor de la información.
    - [ ]  Porque recibe un mensaje "ICMP de datos recibidos" del receptor de la información.
    - [ ]  Porque recibe una señal SYN/ACK del receptor de la información.

15. Las tres partes de una conexión TCP son:
    - [ ]  Resolución del nombre, solicitud de eco, terminación de la sesión.
    - [x]  Establecimiento de sesión, transferencia de datos, terminación de la sesión.
    - [ ]  Resolución del nombre, búsqueda de puerto, terminación de la sesión.
    - [ ]  Establecimiento de sesión, negociación de sesión, interrupción de la sesión.

16. Las dos maneras de terminar una sesión TCP son mediante un mensaje "ICMP de solicitud de eco" y un mensaje "ICMP de respuesta de eco".
    - [ ]  Cierto
    - [x]  Falso

17. Cuando un cliente intenta una conexión y el servidor responde con las señales RST/ACK significa:
    - [ ]  El servidor está apagado o fuera de servicio.
    - [ ]  El servidor tiene abierto el puerto TCP donde se intenta establecer la conexión.
    - [x]  El servidor tiene cerrado el puerto TCP donde se intenta establecer la conexión.
    - [ ]  El servidor tiene cerrado el puerto UDP donde se intenta establecer la conexión.

18. Un servidor DNS:
    - [ ]  Sólo asocia direcciones IP a nombres de equipos.
    - [ ]  Sólo asocia nombres de equipos a direcciones IP.
    - [x]  Puede asociar direcciones IP a nombres de equipos y nombres de equipos a direcciones IP.
    - [ ]  Sólo asocia direcciones MAC a nombres de equipos.

19. Los puertos tienen un número que va desde 0 a 65535.
    - [x]  Cierto
    - [ ]  Falso

20. El puerto de un cliente se usa para una sesión de intercambio de datos y luego se libera para su reuso.
    - [x]  Cierto
    - [ ]  Falso

21. El puerto de un servicio es un número:
    - [ ]  Mayor que 1023.
    - [ ]  Entre 1 y 1023, y cambia muy frecuentemente.
    - [x]  Número bien conocido, y no suele cambiar.
    - [ ]  Diferente en cada equipo dependiendo del sistema operativo y del número de servicios que se ejecutan en el equipo.

22. ¿A qué servicio está asociado normalmente el puerto UDP o TCP 53?
    - [ ]  ICMP.
    - [ ]  IP.
    - [ ]  El troyano Back Orifice.
    - [x]  DNS.

23. ¿Qué hace un router?
    - [ ]  Determina el camino completo de un paquete IP, desde el origen hasta el destino.
    - [ ]  Utiliza el protocolo ARP para encaminar todos los paquetes.
    - [x]  Intenta llevar un poquito más cerca de su destino cada paquete IP que recibe.
    - [ ]  Utiliza el protocolo DNS para encaminar todos los paquetes.

24. ¿Qué protocolo TCP/IP está asociado con el enrutamiento de paquetes?
    - [x]  IP.
    - [ ]  DNS.
    - [ ]  ARP.
    - [ ]  TCP.

25. Algunos dominios DNS de alto nivel son .com, .edu, y .org.
    - [x]  Cierto
    - [ ]  Falso
