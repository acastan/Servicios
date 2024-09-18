Para saber como funciona cualquier comando, debes buscar ayuda escribiendo `man nombre_del_comando`.

Puedes encontrar un buen curso sobre el funcionamiento de Linux y sus comandos en <https://linuxjourney.com/>

¿Qué deberías saber en tu carrera como administrador/a de Linux? Esto: <https://roadmap.sh/linux>

Puedes encontrar más ejercicios en línea en <https://cmdchallenge.com/>

Cuando te consideres un experto/a, intenta superar los retos de <https://overthewire.org/wargames/bandit/> y los CTF de <https://sadservers.com/scenarios>

Recuerda que algunos comandos necesitan permisos de superusuario para ser ejecutados:

![sudo](https://imgs.xkcd.com/comics/sandwich.png)


___



LISTADO DE ARCHIVOS
-------------------

Estudia el comando ls.

 01. Lista recursivamente todos los archivos bajo el directorio /etc deteniendo el despliegue en cada pantalla.

 02. Prueba otras opciones del comando ls usando el directorio /etc o /bin.

 03. Lista archivos visibles e invisibles bajo el directorio actual, en formato largo.

 04. Interpreta las siguientes líneas de salida del formato largo de salida del comando ls:

         drwxr-xr-x 5 pedroso prod     512 Sep 11 15:09 articulos
         -rw-r--r-- 1 pedroso prod    1430 Ago 10 07:56 docum1.prod
         -rwxr-xr-x 3 admin1  adminfo 2330 Jan  7 09:34 rv
         lrwxr--r-- 1 nicasio almacen 9500 Sep 11 10:56 listado.partes


___



REDIRECCION ENTRADA/SALIDA
--------------------------

 05. Sin editor de texto, mediante redirección, crea el archivo cap1 con el contenido “Este es el capítulo 1”. Repite con cap2 y cap3. Verifica mostrando cada uno con el comando cat.

 06. Añade al final de un archivo llamado libro el contenido de los archivos cap1, cap2 y cap3.

 07. Crea un archivo llamado amigotes que contiene las líneas del archivo /etc/passwd ordenadas en orden descendente utilizando el comando sort y redirección de entrada y salida.

 08. Muestra las líneas del fichero amigotes que tienen la palabra home, filtrando el resto mediante el comando grep.


___



EDITOR DE TEXTO
---------------

El editor por excelencia de UNIX es vi, presente en todas las variedades de UNIX. En todas las instalaciones de LINUX, además de vi también encontramos el editor nano, que es más sencillo de utilizar.

 09. Invócalo escribiendo vi o nano. Interpreta la ayuda y experimenta con él creando y modificando textos breves. ¿Cuál es la combinación de teclas para borrar toda una línea? ¿ Cuál es la combinación de teclas para cortar-copiar-pegar?

 10. Crea en tu directorio personal con el procesador de textos una carta a un amigo. A la carta llámala micarta.txt.


___



SISTEMA DE ARCHIVOS
-------------------

 11. Trasládate al directorio bin, dentro del directorio usr, dentro del directorio raíz. Muestra el directorio actual y los archivos contenidos en él.

 12. Trasládate al directorio propio del usuario desde cualquier otro directorio.

 13. Crea un directorio que se llame amigos dentro de tu directorio personal, de forma que cuando listes los contenidos con el comando ls veas tu carta y /home/tunombredeusuario/amigos.

 14. Copia la carta micarta.txt en el directorio que acabas de crear, manteniendo permisos y propietario.

 15. Crea un enlace o atajo llamado carta al fichero micarta.txt.

 16. Renombra /home/tunombredeusuario/amigos, por /home/tunombredeusuario/mis_amigos.

 17. Busca todos los ficheros acabados en bak mediante el comando find, borrándolos.

 18. Calcula cuanto ocupa el directorio /home mediante el comando du.


___



CARPETAS DE UNIX
----------------

 19. ¿Qué se guarda en las siguientes carpetas: /bin y /sbin, /mnt y /media, /usr/sbin, /var, /dev, /proc, /boot?

 20. ¿En qué carpeta se guardan los ficheros de configuración de un programa?

 21. ¿En qué carpeta se guardan los ficheros de configuración de un programa para un usuario determinado?


___



DISCOS, PARTICIONES, MONTAR Y DESMONTAR
---------------------------------------

 22. Lista las particiones del primer disco duro.

 23. Monta la partición del disco duro donde reside Windows. (-En caso de no disponer de una segunda partición con Windows, monta a mano una memoria usb o un disco duro externo-).

 24. Copia un fichero cualquiera de la partición Windows (-o de la memoria usb-) al directorio mis_amigos dentro de tu directorio personal.

 25. ¿Con qué comandos se cambiarían los permisos, el propietario y el grupo de estos ficheros?

 26. Desmonta la partición del disco duro donde reside Windows (-o la memoria usb-).

 27. Borra el directorio que has creado para montar la partición con Windows (-o la memoria usb-).

 28. ¿Qué hay en los ficheros /etc/fstab y /etc/mtab?

 29. ¿Cómo puedes saber el UUID de una partición? ¿Qué es el UUID y para qué se utiliza?


___



USUARIOS
--------

 30. Muestra el nombre del usuario en la sesión actual, y después el nombre de la máquina.

 31. Muestra qué usuarios hay en el sistema en el momento actual.

 32. Crea un usuario llamado pepito con contraseña grillo, y añádelo al grupo admin. Después bórralo.


___



SEGURIDAD
---------

 33. El usuario acastan desea cambiar su contraseña. ¿Cómo lo hace? ¿Qué ayuda debe pedir al administrador?

 34. El usuario acastan olvidó su contraseña. ¿Qué puede hacer por sí mismo? ¿Necesita ayuda del administrador? ¿Cómo puede el administrador averiguar la contraseña que el usuario olvidó? ¿Cómo hace el administrador para cambiar la contraseña del usuario acastan?


___



PROCESOS
--------

 35. Muestra los procesos de tu sesión actual que se están ejecutando.

 36. Muestra todos los procesos en tu sistema que se están ejecutando.

 37. Crea un nuevo proceso al ejecutar el comando more /etc/passwd y páralo con CTRL+Z. Comprueba que aunque estés de nuevo en la línea de comandos dicho proceso sigue activo. Elimina definitivamente dicho proceso con el comando kill.

 38. ¿Cómo se lanza un proceso o comando y, sin que éste haya terminado, accedemos de nuevo a la línea de comandos.

 39. Comprueba el consumo de recursos del sistema por los procesos mediante el comando top.

 40. Visualiza la configuración TCP/IP de tus tarjetas de red.

 41. Visualiza todas las conexiones abiertas con internet, y qué procesos las han generado.

 42. Monitoriza los puertos abiertos a la escucha en tu ordenador.

 43. ¿Qué versión del núcleo Linux tenemos? ¿Cómo podemos ver sus mensajes?

 44. ¿Qué comandos apagan el sistema?


___



SERVICIOS Y FICHEROS DE CONFIGURACIÓN
-------------------------------------

 45. ¿Cómo se detiene o inicia un servicio?

 46. ¿Dónde está guardada la información de los repositorios de programas disponibles?

 47. ¿Dónde está guardada la configuración de las tarjetas de red?

 48. ¿Dónde está guardados los servidores de DNS que utiliza el equipo?

 49. ¿Dónde está guardada la información de ejecución periódica de procesos? ¿Con qué comando se añaden nuevos procesos? ¿Qué formato tienen las líneas de dichos ficheros?

 50. ¿En qué ficheros se guarda información relativa a los usuarios del sistema?


___



EXPRESIONES REGULARES (EXTRA)
-----------------------------

Recordando los diferentes operadores de las expresiones regulares:

  - `.`   cualquier carácter

  - `?`   0 ó 1 veces el carácter o la expresión anterior

  - `*`   0 ó más veces el carácter o la expresión anterior

  - `+`   1 ó más veces el carácter o la expresión anterior

  - `{n,m}`   entre n y m veces el carácter o la expresión anterior

  - `|`   escoger entre una u otra expresión

  - `^`   inicio de línea

  - `$`   final de línea

  - `-`   rango de letras o números

  - `[]` `()`   agrupar

  - `^`   negación

  - `[:alnum:]` `[:alpha:]` `[:digit:]` `[:upper:]` `[:lower:]` `[:blank:]`   conjunto de caracteres

Responde a las siguientes preguntas sobre un fichero de palabras suficientemente grande (por ejemplo <ftp://ftp.cerias.purdue.edu/pub/dict/wordlists/spanish/>)

 01. Palabras que tienen una a más b o una a más d seguidas de una n

 02. Palabras que tienen dos o más a seguidas

 03. Palabras cuya tercera letra es b

 04. Palabras que contienen pan o plan

 05. Palabras que acaban en cial

 06. ¿Cuantas líneas vacías?

 07. Palabras que contienen un número del 0 al 5

 08. Palabras que acaban en o, más una letra que no sea n

 09. Contraseñas que tienen seis letras seguidas de dos números

 10. El nombre de un fichero con extensión .txt , .odt o .pdf

 11. Una fecha con el formato dd/mm/aaaa

 12. Una dirección de correo electrónico con el formato nombre@dominio.xxx
