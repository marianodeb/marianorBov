1. **Escaneo Básico**:
   - `nmap <dirección IP>`: Escanea el host especificado para identificar puertos abiertos.

2. **Escaneo de Puertos**:
   - `nmap -p <puertos> <dirección IP>`: Escanea puertos específicos. Ejemplo: `nmap -p 22,80,443 <dirección IP>`.
   - `nmap -p- <dirección IP>`: Escanea todos los 65,535 puertos.

3. **Escaneo de Servicios y Versiones**:
   - `nmap -sV <dirección IP>`: Detecta versiones de los servicios que están corriendo en los puertos abiertos.

4. **Detección de Sistema Operativo**:
   - `nmap -O <dirección IP>`: Intenta identificar el sistema operativo del host.

5. **Escaneo Silencioso**:
   - `nmap -sS <dirección IP>`: Realiza un escaneo SYN (escaneo "stealth") que es menos probable que sea detectado por sistemas de prevención de intrusiones.

6. **Escaneo de Descubrimiento de Hosts**:
   - `nmap -sn <dirección IP>`: Realiza un escaneo de descubrimiento de hosts, sin realizar escaneo de puertos.

7. **Escaneo de Red**:
   - `nmap -sP <red>`: Escanea toda una subred para identificar qué hosts están activos. Ejemplo: `nmap -sP 192.168.1.0/24`.

8. **Escaneo de Scripts**:
   - `nmap -sC <dirección IP>`: Ejecuta una serie de scripts predeterminados para realizar tareas comunes de escaneo y detección.

9. **Escaneo de Firewall**:
   - `nmap -sA <dirección IP>`: Realiza un escaneo ACK para detectar si hay un firewall entre el host y el escáner.

10. **Escaneo de Puertos UDP**:
    - `nmap -sU <dirección IP>`: Realiza un escaneo de puertos UDP, que puede ser más lento y menos preciso que el escaneo de puertos TCP.

11. **Evitar Detección**:
    - `nmap -D RND:10 <dirección IP>`: Usa técnicas de evasión, como el spoofing de IP para ocultar el origen del escaneo.

12. **Resultados en Diferentes Formatos**:
    - `nmap -oN <archivo.txt> <dirección IP>`: Guarda los resultados en un archivo de texto.
    - `nmap -oX <archivo.xml> <dirección IP>`: Guarda los resultados en un archivo XML.
    - `nmap -oG <archivo.gnmap> <dirección IP>`: Guarda los resultados en formato grepable (para procesar con herramientas de línea de comandos).

13. **Escaneo Intensivo**:
    - `nmap -A <dirección IP>`: Realiza un escaneo agresivo que incluye detección de servicios, versiones, sistema operativo y más.

14. **Escaneo de Red con Más Opciones**:
    - `nmap -T<0-5> <dirección IP>`: Ajusta el timing template para el escaneo. Por ejemplo, `-T4` es más rápido pero más ruidoso, `-T0` es el más lento y sigiloso.

15. **Escaneo de IPs Aleatorias**:
    - `nmap -iR <número> <puerto>`: Escanea un número aleatorio de hosts. Por ejemplo, `nmap -iR 1000 -p 80` escanea 1000 hosts aleatorios en el puerto 80.

16. **Escaneo con Más Información de Detección**:
    - `nmap -sS -sU -T4 -A -v <dirección IP>`: Combina varios escaneos para obtener información detallada y ser más rápido. El flag `-v` aumenta la verbosidad de la salida.

17. **Escaneo de Redes Privadas**:
    - `nmap --unprivileged <dirección IP>`: Ejecuta Nmap con privilegios no elevados, lo que puede limitar algunas capacidades de escaneo.

18. **Escaneo de Hosts con TTL**:
    - `nmap --ttl <valor> <dirección IP>`: Establece el valor del Time To Live (TTL) en los paquetes para el escaneo, lo que puede ayudar a evadir algunos sistemas de detección.

19. **Escaneo de Puertos de Forma Rápida**:
    - `nmap --top-ports <número> <dirección IP>`: Escanea los puertos más comunes. Por ejemplo, `nmap --top-ports 10 <dirección IP>` escanea los 10 puertos más comunes.

20. **Escaneo de Hosts en una Red con Restricciones**:
    - `nmap -Pn <dirección IP>`: Desactiva el descubrimiento de hosts, lo que puede ser útil en redes donde los hosts no responden a los pings.

21. **Escaneo de Servicios con Script Personalizado**:
    - `nmap --script <nombre del script> <dirección IP>`: Ejecuta un script NSE (Nmap Scripting Engine) específico. Ejemplo: `nmap --script http-vuln-cve2014-3704 <dirección IP>`.

22. **Escaneo de Red con Opciones de Fragmentación**:
    - `nmap -f <dirección IP>`: Fragmenta los paquetes para evadir algunos sistemas de detección.

23. **Escaneo de Puertos con SSL/TLS**:
    - `nmap --script ssl-enum-ciphers <dirección IP>`: Ejecuta un script para enumerar los cifrados SSL/TLS disponibles en un puerto.


## Nmap 

Descubriendo sistemas
Uno de los primeros pasos en cualquier misión de reconocimiento de red es el de reducir muchas veces un enorme conjunto de rangos de direcciones IP en una lista de equipos activos o interesantes. 

Analizar cada puerto de cada una de las direcciones IP es lento, y usualmente innecesario. 

Por supuesto, lo que hace a un sistema interesante depende ampliamente del propósito del análisis. Los administradores de red pueden interesarse sólo en equipos que estén ejecutando un cierto servicio, mientras que los auditores de seguridad pueden interesarse en todos y cada uno de los dispositivos que tengan una dirección IP. 

Un administrador puede sentirse cómodo con obtener un listado de equipos en su red interna mediante un ping ICMP, mientras que un consultor en seguridad realizando un ataque externo puede llegar a utilizar un conjunto de docenas de sondas en su intento de saltarse las restricciones de los cortafuegos.

Siendo tan diversas las necesidades de descubrimiento de sistemas, Nmap ofrece una gran variedad de opciones para personalizar las técnicas utilizadas. 

Al descubrimiento de sistemas («Host Discovery») se lo suele llamar sondeo ping, pero va más allá de la simple solicitud ICMP echo-request de los paquetes asociados al querido y nunca bien ponderado ping. 

Los usuarios pueden evitar el paso de ping utilizando un sondeo de lista (-sL) o deshabilitando el ping (-P0), o enviando combinaciones arbitrarias de sondas TCP SYN/ACK, UDP e ICMP a múltiples puertos de la red remota. 

El propósito de estas sondas es el de solicitar respuestas que demuestren que una dirección IP se encuentra activa (está siendo utilizada por un equipo o dispositivo de red). 

En varias redes solo un pequeño porcentaje de direcciones IP se encuentran activos en cierto momento. Esto es particularmente común en las redes basadas en direccionamiento privado RFC1918, como la 10.0.0.0/8. Dicha red tiene más de 16 millones de direcciones IP, pero la he visto siendo utilizada por empresas con menos de mil máquinas. El descubrimiento de sistemas puede encontrar dichas máquinas en un rango tan grande como el indicado.

Si no se proveen opciones de descubrimiento de sistemas, Nmap envía un paquete TCP ACK al puerto 80 y un ICMP Echo Request a cada máquina objetivo. Una excepción a este comportamiento es cuando se utiliza un análisis ARP, para los objetivos que se encuentren en la red Ethernet local. 

Para usuarios de shell UNIX que no posean privilegios, un paquete SYN es enviado en vez del ACK, utilizando la llamada al sistema connect(). Estos valores por omisión son el equivalente a las opciones -PA -PE. Este descubrimiento de sistemas es generalmente suficiente cuando se analizan redes locales, pero para auditorías de seguridad se recomienda utilizar un conjunto más completo de sondas de descubrimiento.

Las opciones -P* (que permiten seleccionar los tipos de ping) pueden combinarse. Puede aumentar sus probabilidades de penetrar cortafuegos estrictos enviando muchos tipos de sondas utilizando diferentes puertos o banderas TCP y códigos ICMP. 

Recuerde que el ARP discovery (-PR) se realiza por omisión contra objetivos de la red Ethernet local incluso si se especifica otra de las opciones -P*, porque es generalmente más rápido y efectivo.



07

### HOST DISCOVERY:
  -sL: List Scan - simply list targets to scan
  -sn: Ping Scan - disable port scan
  -Pn: Treat all hosts as online -- skip host discovery
  -PS/PA/PU/PY\[portlist\]: TCP SYN/ACK, UDP or SCTP discovery to given ports
  -PE/PP/PM: ICMP echo, timestamp, and netmask request discovery probes
  -PO\[protocol list\]: IP Protocol Ping
  -n/-R: Never do DNS resolution/Always resolve \[default: sometimes\]
  --dns-servers serv1\[,serv2\],...: Specify custom DNS servers
  --system-dns: Use OS's DNS resolver
  --traceroute: Trace hop path to each host


### -sL (Sondeo de lista)
El sondeo de lista es un tipo de descubrimiento de sistemas que tan solo lista cada equipo de la/s red/es especificada/s, sin enviar paquetes de ningún tipo a los objetivos. Por omisión, Nmap va a realizar una resolución inversa DNS en los equipos, para obtener sus nombres. Es sorprendente cuanta información útil se puede obtener del nombre de un sistema. El sondeo de lista es una buena forma de asegurarse de que tenemos las direcciones IP correctas de nuestros objetivos. Si se encontraran nombres de dominio que no reconoces, vale la pena investigar un poco más, para evitar realizar un análisis de la red de la empresa equivocada.

Ya que la idea es simplemente emitir un listado de los sistemas objetivo, las opciones de mayor nivel de funcionalidad como análisis de puertos, detección de sistema operativo, o análisis ping no pueden combinarse con este sondeo. Si desea deshabilitar el análisis ping aún realizando dicha funcionalidad de mayor nivel, compruebe la documentación de la opción -P0.

### -sP (Sondeo ping) -sn
Esta opción le indica a Nmap que únicamente realice descubrimiento de sistemas mediante un sondeo ping, y que luego emita un listado de los equipos que respondieron al mismo. No se realizan más sondeos (como un análisis de puertos o detección de sistema operativo). A diferencia del sondeo de lista, el análisis ping es intrusivo, ya que envía paquetes a los objetivos, pero es usualmente utilizado con el mismo propósito. Permite un reconocimiento liviano de la red objetivo sin llamar mucho la atención. El saber cuántos equipos se encuentran activos es de mayor valor para los atacantes que el listado de cada una de las IP y nombres proporcionado por el sondeo de lista.

De la misma forma, los administradores de sistemas suelen encontrar valiosa esta opción. Puede ser fácilmente utilizada para contabilizar las máquinas disponibles en una red, o monitorizar servidores. A esto se lo suele llamar barrido ping, y es más fiable que hacer ping a la dirección de broadcast, ya que algunos equipos no responden a ese tipo de consultas.

La opción -sP envía una solicitud de eco ICMP y un paquete TCP al puerto 80 por omisión. Cuando un usuario sin privilegios ejecuta Nmap se envía un paquete SYN (utilizando la llamada connect()) al puerto 80 del objetivo. Cuando un usuario privilegiado intenta analizar objetivos en la red Ethernet local se utilizan solicitudes ARP (-PR) a no ser que se especifique la opción --send-ip.

La opción -sP puede combinarse con cualquiera de las opciones de sondas de descubrimiento (las opciones -P*, excepto -P0) para disponer de mayor flexibilidad. Si se utilizan cualquiera de las opciones de sondas de descubrimiento y número de puerto, se ignoran las sondas por omisión (ACK y solicitud de eco ICMP). Se recomienda utilizar estas técnicas si hay un cortafuegos con un filtrado estricto entre el sistema que ejecuta Nmap y la red objetivo. Si no se hace así pueden llegar a pasarse por alto ciertos equipos, ya que el cortafuegos anularía las sondas o las respuestas a las mismas.

-P0 (No realizar ping)
Con esta opción, Nmap no realiza la etapa de descubrimiento. Bajo circunstancias normales, Nmap utiliza dicha etapa para determinar qué máquinas se encuentran activas para hacer un análisis más agresivo. Por omisión, Nmap sólo realiza ese tipo de sondeos, como análisis de puertos, detección de versión o de sistema operativo contra los equipos que se están «vivos». Si se deshabilita el descubrimiento de sistemas con la opción -P0 entonces Nmap utilizará las funciones de análisis solicitadas contra todas las direcciones IP especificadas. Por lo tanto, si se especifica una red del tamaño de una clase B cuyo espacio de direccionamiento es de 16 bits, en la línea de órdenes, se analizará cada una de las 65.536 direcciones IP. El segundo carácter en la opción -P0 es un cero, y no la letra O. Al igual que con el sondeo de lista, se evita el descubrimiento apropiado de sistemas, pero, en vez de detenerse y emitir un listado de objetivos, Nmap continúa y realiza las funciones solicitadas como si cada IP objetivo se encontrara activa.



08

### -PE; -PP; -PM (Tipos de ping ICMP)
Nmap puede enviar los paquetes estándar que envía el programa ping además de los tipos de descubrimiento de equipos con TCP y UDP. Nmap envía paquetes ICMP tipo 7 («echo request») a las direcciones IP objetivos y espera recibir un tipo 0 («Echo Reply») de los sistemas que estén disponibles. Lamentablemente para los exploradores de redes, muchos sistemas y cortafuegos ahora bloquean esos paquetes en lugar de responder como requiere el estándar RFC 1122. Por ésta razón los sondeos que sólo utilizan el protocolo ICMP no son muy fiables para analizar sistemas desconocidos en Internet. Aunque pueda ser una forma eficiente y práctica de hacerlo para administradores que tengan que monitorizar una red interna. Utilice la opción -PE para activar este comportamiento de solicitud de eco.

ME DISCULPAN EL AUDIO; NO SE QUE DIABLOS PASA CON MI MAQUINA QUE POR MOMENTO HACE ESE PROBLEMA.

Nmap no hace sólo ésto, aunque la solicitud eco es la consulta estándar de ping ICMP. El estándar ICMP (RFC 792) también específica solicitudes de huellas de tiempo, de información y de máscara de red, que corresponden con los códigos 13, 15 y 17 respectivamente. Aunque el objetivo de estas solicitudes es obtener la máscara de red o fecha actual de un sistema también pueden utilizarse para descubrir sistemas. Un sistema que responde es por que está vivo y disponible. Nmap no implementa los paquetes de solicitud de información en sí, ya que no están muy soportados. El estándar RFC 1122 insiste en que “un equipo NO DEBE implementar estos mensajes”. Las consultas de huella de tiempo y máscara de red se pueden enviar con las opciones -PP y -PM, respectivamente. Si se recibe una respuesta de huella de tiempo (código ICMP 14) o de máscara de red (código 18) entonces es que el sistema está disponible. Estas dos consultas pueden ser útiles cuando los administradores bloquean los paquetes de consulta eco explícitamente pero se olvidan de que se pueden utilizar otras consultas ICMP con el mismo fin.

-PR (Ping ARP)
Una de las formas de uso más comunes de Nmap es el sondeo de una red de área local Ethernet. En la mayoría de las redes locales hay muchas direcciones IP sin usar en un momento determinado. Esto es así especialmente en las que utilizan rangos de direcciones privadas definidas en el RFC1918. Cuando Nmap intenta enviar un paquete IP crudo, como pudiera ser una solicitud de eco ICMP, el sistema operativo debe determinar primero la dirección (ARP) correspondiente a la IP objetivo para poder dirigirse a ella en la trama Ethernet. Esto es habitualmente un proceso lento y problemático, dado que los sistemas operativos no se escribieron pensando en que tendrían que hacer millones de consultas ARP contra sistemas no disponibles en un corto periodo de tiempo.

El sondeo ARP hace que sea Nmap y su algoritmo optimizado el que se encargue de las solicitudes ARP. Si recibe una respuesta, no se tiene ni que preocupar de los paquetes basados en IP dado que ya sabe que el sistema está vivo. Esto hace que el sondeo ARP sea mucho más rápido y fiable que los sondeos basados en IP. Por ello se utiliza por omisión cuando se analizan sistemas Ethernet si Nmap detecta que están en la red local. Nmap utiliza ARP para objetivos en la misma red local aún cuando se utilicen distintos tipos de ping (como -PE o -PS). Si no quiere hacer un sondeo ARP tiene que especificar la opción --send-ip.



09

### -PE; -PP; -PM (Tipos de ping ICMP)
Nmap puede enviar los paquetes estándar que envía el programa ping además de los tipos de descubrimiento de equipos con TCP y UDP. Nmap envía paquetes ICMP tipo 7 («echo request») a las direcciones IP objetivos y espera recibir un tipo 0 («Echo Reply») de los sistemas que estén disponibles. Lamentablemente para los exploradores de redes, muchos sistemas y cortafuegos ahora bloquean esos paquetes en lugar de responder como requiere el estándar RFC 1122. Por ésta razón los sondeos que sólo utilizan el protocolo ICMP no son muy fiables para analizar sistemas desconocidos en Internet. Aunque pueda ser una forma eficiente y práctica de hacerlo para administradores que tengan que monitorizar una red interna. Utilice la opción -PE para activar este comportamiento de solicitud de eco.

Nmap no hace sólo ésto, aunque la solicitud eco es la consulta estándar de ping ICMP. El estándar ICMP (RFC 792) también específica solicitudes de huellas de tiempo, de información y de máscara de red, que corresponden con los códigos 13, 15 y 17 respectivamente. Aunque el objetivo de estas solicitudes es obtener la máscara de red o fecha actual de un sistema también pueden utilizarse para descubrir sistemas. Un sistema que responde es por que está vivo y disponible. Nmap no implementa los paquetes de solicitud de información en sí, ya que no están muy soportados. El estándar RFC 1122 insiste en que “un equipo NO DEBE implementar estos mensajes”. Las consultas de huella de tiempo y máscara de red se pueden enviar con las opciones -PP y -PM, respectivamente. Si se recibe una respuesta de huella de tiempo (código ICMP 14) o de máscara de red (código 18) entonces es que el sistema está disponible. Estas dos consultas pueden ser útiles cuando los administradores bloquean los paquetes de consulta eco explícitamente pero se olvidan de que se pueden utilizar otras consultas ICMP con el mismo fin.

-PR (Ping ARP)
Una de las formas de uso más comunes de Nmap es el sondeo de una red de área local Ethernet. En la mayoría de las redes locales hay muchas direcciones IP sin usar en un momento determinado. Esto es así especialmente en las que utilizan rangos de direcciones privadas definidas en el RFC1918. Cuando Nmap intenta enviar un paquete IP crudo, como pudiera ser una solicitud de eco ICMP, el sistema operativo debe determinar primero la dirección (ARP) correspondiente a la IP objetivo para poder dirigirse a ella en la trama Ethernet. Esto es habitualmente un proceso lento y problemático, dado que los sistemas operativos no se escribieron pensando en que tendrían que hacer millones de consultas ARP contra sistemas no disponibles en un corto periodo de tiempo.

El sondeo ARP hace que sea Nmap y su algoritmo optimizado el que se encargue de las solicitudes ARP. Si recibe una respuesta, no se tiene ni que preocupar de los paquetes basados en IP dado que ya sabe que el sistema está vivo. Esto hace que el sondeo ARP sea mucho más rápido y fiable que los sondeos basados en IP. Por ello se utiliza por omisión cuando se analizan sistemas Ethernet si Nmap detecta que están en la red local. Nmap utiliza ARP para objetivos en la misma red local aún cuando se utilicen distintos tipos de ping (como -PE o -PS). Si no quiere hacer un sondeo ARP tiene que especificar la opción: 
--send-ip.



10

### -PS \[lista de puertos\] (Ping TCP SYN)
Esta opción envía un paquete TCP vacío con la bandera SYN puesta. El puerto destino por omisión es el 80 (se puede configurar en tiempo de compilación cambiando el valor de DEFAULT_TCP_PROBE_PORT en nmap.h), pero se puede añadir un puerto alternativo como parámetro. También se puede especificar una lista de puertos separados por comas (p.ej. -PS22,23,25,80,113,1050,35000). Si hace esto se enviarán sondas en paralelo a cada uno de los puertos.

La bandera SYN indica al sistema remoto que quiere establecer una conexión. Normalmente, si el puerto destino está cerrado se recibirá un paquete RST (de «reset»). Si el puerto está abierto entonces el objetivo responderá con el segundo paso del saludo en tres pasos TCP respondiendo con un paquete TCP SYN/ACK. El sistema donde se ejecuta Nmap romperá la conexión que se está estableciendo enviando un paquete RST en lugar de enviar el paquete ACK que completaría el saludo TCP. Nmap no envía este paquete, sino que lo envía el núcleo del sistema donde se ejecuta Nmap respondiendo al paquete SYN/ACK que no esperaba.

A Nmap no le importa si el puerto está abierto o cerrado. Si, tal y como se acaba de describir, llega una respuesta RST ó SYN/ACK entonces Nmap sabrá que el sistema está disponible y responde.

En sistemas UNIX, generalmente sólo el usuario privilegiado root puede enviar paquetes TCP crudos. Los usuarios no privilegiados tienen una forma de evitar esta restricción utilizando la llamada al sistema «connect()» contra el puerto destino. Esto hace que se envíe el paquete SYN al sistema, para establecer la conexión. Si la llamada «connect()» devuelve un resultado de éxito rápidamente o un fallo ECONNREFUSED entonces se puede deducir que la pila TCP que tiene bajo ésta ha recibido un SYN/ACK o un RST y que puede marcar el sistema como disponible. El sistema se puede marcar como no disponible si el intento de conexión se mantiene parado hasta que vence un temporizador. 

-PA \[lista de puertos\] (Ping TCP ACK)
El ping TCP ACK es muy parecido al ping SYN que se acaba de tratar. La diferencia es que en este caso se envía un paquete con la bandera ACK en lugar de la SYN. Este paquete indica que se han recibido datos en una conexión TCP establecida, pero se envían sabiendo que la conexión no existe. En este caso los sistemas deberían responder con un paquete RST, lo que sirve para determinar que están vivos.

La opción -PA utiliza el mismo puerto por omisión que la sonda SYN (el puerto 80) y también puede tomar una lista de puertos destino en el mismo formato. Si un usuario sin privilegios intenta hacer esto, o se especifica un objetivo IPv6, se utiliza el procedimiento descrito anteriormente. Aunque en este caso el procedimiento no es perfecto porque la llamada «connect()» enviará un paquete SYN en lugar de un ACK.

Se ofrecen tanto mecanismos de sondeo con ping SYN y ACK para maximizar las posibilidades de atravesar cortafuegos. Muchos administradores configuran los enrutadores y algunos cortafuegos sencillos para que se bloqueen los paquetes SYN salvo para aquellos destinados a los servicios públicos, como pudieran ser el servidor web o el servidor de correo de la organización. Esto evita que se realicen otras conexiones entrantes al mismo tiempo que permite a los usuarios realizar conexiones salientes a Internet. Este acercamiento de filtrado sin estados toma pocos recursos de los cortafuegos/enrutadores y está ampliamente soportado por filtros hardware y software. El programa de cortafuegos Netfilter/iptables de Linux ofrece la opción --syn para implementar este acercamiento sin estados. Cuando se han implementado reglas de filtrado como éstas es posible que se bloqueen las sondas ping SYN (-PS) cuando éstas se envíen a un puerto cerrado. Sin embargo, en estos casos, las sondas ACK podrían saltarse las reglas y llegar a su destino.

Otros tipos de cortafuegos comunes utilizan reglas con estados que descartan paquetes no esperados. Esta funcionalidad se encontraba antes fundamentalmente en los cortafuegos de gama alta pero se ha hecho cada vez más común. El sistema Netfilter/iptables de Linux soporta esta posibilidad a través de la opción --state, que hace categorías de paquetes en base a su estado de conexión. Una solución a este dilema es enviar sondas SYN y ACK especificando tanto la opción -PS como -PA.

-PU \[lista de puertos\] (Ping UDP)
El ping UDP es otra opción para descubrir sistemas. Esta opción envía un paquete UDP vacío (salvo que se especifique --data-length) a los puertos indicados. La lista de puertos se debe dar en el mismo formato que se ha indicado anteriormente para las opciones -PS y -PA . Si no se especifica ningún puerto se utiliza el puerto 31338 por omisión. Se puede configurar este puerto por omisión en el momento de compilar cambiando DEFAULT_UDP_PROBE_PORT en nmap.h. Se utiliza un puerto alto y poco común por omisión porque no es deseable enviar este sondeo a otro tipo de puertos.



11

 Hacer mas rapido y eficaz el trabajo.
-n (No realizar resolución de nombres)
Le indica a Nmap que nunca debe realizar resolución DNS inversa de las direcciones IP activas que encuentre. Ya que DNS es generalmente lento, esto acelera un poco las cosas.

-R (Realizar resolución de nombres con todos los objetivos)
Le indica a Nmap que deberá realizar siempre la resolución DNS inversa de las direcciones IP objetivo. Normalmente se realiza esto sólo si se descubre que el objetivo se encuentra vivo.

--system-dns (Utilizar resolución DNS del sistema)
Por omisión, Nmap resuelve direcciones IP por si mismo enviando las consultas directamente a los servidores de nombres configurados en el sistema, y luego espera las respuestas. Varias solicitudes (generalmente docenas) son realizadas en paralelo para mejorar el rendimiento. Especifica esta opción si desea que sí utilice la resolución del sistema (una IP por vez utilizando la llamada getnameinfo()). Este método es más lento y raramente útil, a no ser que hubiera un error en el código DNS de Nmap (por favor, notifíquelo si ese fuera el caso). Éste es el método por omisión para los sondeos IPv6.

--dns-servers servidor1\[,servidor2\],... (Servidores a utilizar para las consultas DNS)
Nmap generalmente determina los servidores DNS de su archivo resolv.conf (UNIX) o del registro (Win32). Puede utilizar esta opción para especificar sus propios servidores. Esta opción no se utiliza si utiliza la opción --system-dns o está realizando un sondeo IPv6. La resolución a través de más de un servidor de DNS es generalmente más rápida que la consulta a uno solo.

--traceroute
La bandera "--traceroute" en un proceso de descubrimiento de hosts o dispositivos de red permite realizar un seguimiento del camino que toma un paquete de datos a través de la red para alcanzar su destino. Esto se hace enviando paquetes de datos con incrementos de tiempo de vida (TTL) progresivamente mayores y observando las respuestas de los diferentes routers o nodos de la red a medida que el paquete pasa por ellos.

Al utilizar esta bandera en un proceso de descubrimiento de hosts, se puede obtener información adicional sobre la topología de la red, identificar los routers intermedios y estimar el tiempo que tarda un paquete en llegar a cada nodo. Esto puede ser útil para entender la estructura de la red y para identificar posibles cuellos de botella o puntos de fallo.


12

Introducción al análisis de puertos
Nmap comenzó como un analizador de puertos eficiente, aunque ha aumentado su funcionalidad a través de los años, aquella sigue siendo su función primaria. La sencilla orden nmap objetivo analiza más de 1660 puertos TCP del equipo objetivo. Aunque muchos analizadores de puertos han agrupado tradicionalmente los puertos en dos estados: abierto o cerrado, Nmap es mucho más descriptivo. Se dividen a los puertos en seis estados distintos: abierto, cerrado, filtrado, no filtrado, abierto  filtrado, o cerrado|filtrado.

Estos estados no son propiedades intrínsecas del puerto en sí, pero describen cómo los ve Nmap. Por ejemplo, un análisis con Nmap desde la misma red en la que se encuentra el objetivo puede mostrar el puerto 135 / tcp como abierto, mientras que un análisis realizado al mismo tiempo y con las mismas opciones, pero desde Internet, puede presentarlo como filtrado.

### Los seis estados de un puerto, según Nmap
#### abierto - open
Una aplicación acepta conexiones TCP o paquetes UDP en este puerto. El encontrar esta clase de puertos es generalmente el objetivo primario de realizar un sondeo de puertos. Las personas orientadas a la seguridad saben que cada puerto abierto es un vector de ataque. Los atacantes y las personas que realizan pruebas de intrusión intentan aprovechar puertos abiertos, por lo que los administradores intentan cerrarlos, o protegerlos con cortafuegos, pero sin que los usuarios legítimos pierdan acceso al servicio. Los puertos abiertos también son interesantes en sondeos que no están relacionados con la seguridad porque indican qué servicios están disponibles para ser utilizados en una red.

#### cerrado - close
Un puerto cerrado es accesible: recibe y responde a las sondas de Nmap, pero no tiene una aplicación escuchando en él. Pueden ser útiles para determinar si un equipo está activo en cierta dirección IP (mediante descubrimiento de sistemas, o sondeo ping), y es parte del proceso de detección de sistema operativo. Como los puertos cerrados son alcanzables, o sea, no se encuentran filtrados, puede merecer la pena analizarlos pasado un tiempo, en caso de que alguno se habrá. Los administradores pueden querer considerar bloquear estos puertos con un cortafuegos. Si se bloquean aparecen filtrados, como se discute a continuación.

#### filtrado - filtered
Nmap no puede determinar si el puerto se encuentra abierto porque un filtrado de paquetes previene que sus sondas alcancen el puerto. El filtrado puede provenir de un dispositivo de cortafuegos dedicado, de las reglas de un enrutador, o por una aplicación de cortafuegos instalada en el propio equipo. Estos puertos suelen frustrar a los atacantes, porque proporcionan muy poca información. A veces responden con mensajes de error ICMP del tipo 3, código 13 (destino inalcanzable: comunicación prohibida por administradores), pero los filtros que sencillamente descartan las sondas sin responder son mucho más comunes. Esto fuerza a Nmap a reintentar varias veces, considerando que la sonda pueda haberse descartado por congestión en la red en vez de haberse filtrado. Esto ralentiza drásticamente los sondeos.

#### no filtrado
Este estado indica que el puerto es accesible, pero que Nmap no puede determinar si se encuentra abierto o cerrado. Solamente el sondeo ACK, utilizado para determinar las reglas de un cortafuegos, clasifica a los puertos según este estado. El analizar puertos no filtrados con otros tipos de análisis, como el sondeo Window, SYN o FIN, pueden ayudar a determinar si el puerto se encuentra abierto.

#### abierto | filtrado
Nmap marca a los puertos en este estado cuando no puede determinar si el puerto se encuentra abierto o filtrado. Esto ocurre para tipos de análisis donde no responden los puertos abiertos. La ausencia de respuesta puede también significar que un filtro de paquetes ha descartado la sonda, o que se elimina cualquier respuesta asociada. De esta forma, Nmap no puede saber con certeza si el puerto se encuentra abierto o filtrado. Los sondeos UDP, protocolo IP, FIN, Null y Xmas clasifican a los puertos de esta manera.

#### cerrado | filtrado
Este estado se utiliza cuando Nmap no puede determinar si un puerto se encuentra cerrado o filtrado, y puede aparecer sólo durante un sondeo IPID pasivo.

La identificación de IP (IPID) es un campo dentro del encabezado IP que generalmente incrementa con cada paquete enviado desde un host. Un sondeo IPID pasivo en Nmap implica la observación de cómo un sistema responde a paquetes enviados desde otra máquina. Esto se hace sin interactuar directamente con el sistema objetivo, sino simplemente observando las respuestas de los paquetes que se envían.



13

### Técnicas de sondeo de puertos
Cuando intento realizar un arreglo de mi coche, siendo novato, puedo pasarme horas intentando utilizar mis herramientas rudimentarias (martillo, cinta aislante, llave inglesa, etc.). Cuando fallo miserablemente y llevo mi coche antiguo en grúa al taller a un mecánico de verdad siempre pasa lo mismo: busca en su gran cajón de herramientas hasta que saca una herramienta que hace que la tarea se haga sin esfuerzo. El arte de sondear puertos es parecido. Los expertos conocen docenas de técnicas de sondeo y eligen la más apropiada (o una combinación de éstas) para la tarea que están realizando. Los usuarios sin experiencia y los "script kiddies", sin embargo, intentan resolver cada problema con el sondeo SYN por omisión. Dado que Nmap es libre, la única barrera que existe para ser un experto en el sondeo de puertos es el conocimiento. Esto es mucho mejor que el mundo del automóvil, donde puedes llegar a saber que necesitas un compresor de tuerca, pero tendrás que pagar mil dólares por él.

La mayoría de los distintos tipos de sondeo disponibles sólo los puede llevar a cabo un usuario privilegiado. Esto es debido a que envían y reciben paquetes en crudo, lo que hace necesario tener acceso como administrador (root) en la mayoría de los sistemas UNIX. En los entornos Windows es recomendable utilizar una cuenta de administrador, aunque Nmap algunas veces funciona para usuarios no privilegiados en aquellas plataformas donde ya se haya instalado WinPcap. La necesidad de privilegios como usuario administrador era una limitación importante cuando se empezó a distribuir Nmap en 1997, ya que muchos usuarios sólo tenían acceso a cuentas compartidas en sistemas como usuarios normales. Ahora, las cosas son muy distintas. Los ordenadores son más baratos, hay más personas que tienen acceso permanente a Internet, y los sistemas UNIX (incluyendo Linux y MAC OS X) son más comunes. 

Aunque Nmap intenta generar resultados precisos, hay que tener en cuenta que estos resultados se basan en los paquetes que devuelve el sistema objetivo (o los cortafuegos que están delante de éstos). Estos sistemas pueden no ser fiables y envíar respuestas cuyo objetivo sea confundir a Nmap. Son aún más comunes los sistemas que no cumplen con los estándares RFC, que no responden como deberían a las sondas de Nmap. Son especialmente susceptibles a este problema los sondeos FIN, Null y Xmas. Hay algunos problemas específicos a algunos tipos de sondeos que se discuten en las entradas dedicadas a sondeos concretos.

Esta sección documenta las aproximadamente doce técnicas de sondeos de puertos que soporta Nmap. Sólo puede utilizarse un método en un momento concreto, salvo por el sondeo UDP (-sU) que puede combinarse con cualquiera de los sondeos TCP. 

Nmap hace un sondeo SYN por omisión, aunque lo cambia a un sondeo Connect() si el usuario no tiene los suficientes privilegios para enviar paquetes en crudo (requiere acceso de administrador en UNIX) o si se especificaron objetivos IPv6. De los sondeos que se listan en esta sección los usuarios sin privilegios sólo pueden ejecutar el sondeo Connect().

ESCANEAMOS A:
scanme.nmap.com

### -sS (sondeo TCP SYN)
El sondeo SYN es el utilizado por omisión y el más popular por buenas razones. Puede realizarse rápidamente, sondeando miles de puertos por segundo en una red rápida en la que no existan cortafuegos. El sondeo SYN es relativamente sigiloso y poco molesto, ya que no llega a completar las conexiones TCP. También funciona contra cualquier pila TCP en lugar de depender de la idiosincrasia específica de una plataforma concreta, al contrario de lo que pasa con los sondeos de Nmap Fin/Null/Xmas, Maimon o pasivo. También muestra una clara y fiable diferenciación entre los estados abierto, cerrado, y filtrado.

A esta técnica se la conoce habitualmente como sondeo medio abierto, porque no se llega a abrir una conexión TCP completa. Se envía un paquete SYN, como si se fuera a abrir una conexión real y después se espera una respuesta. Si se recibe un paquete SYN/ACK esto indica que el puerto está en escucha (abierto), mientras que si se recibe un RST (reset) indica que no hay nada escuchando en el puerto. Si no se recibe ninguna respuesta después de realizar algunas retransmisiones entonces el puerto se marca como filtrado. También se marca el puerto como filtrado si se recibe un error de tipo ICMP no alcanzable (tipo 3, códigos 1,2, 3, 9, 10, ó 13).



14

### -sN (Sondeo NULL):
Este sondeo envía un paquete TCP sin ningún indicador de control establecido. Básicamente, es como si estuvieras tocando la puerta de un dispositivo sin hacer ningún ruido.
Se utiliza para intentar evadir los sistemas de detección de intrusos, ya que el sondeo NULL no activa ningún indicador en el dispositivo objetivo. Es útil para ver si un dispositivo puede ser "invisible" para ciertos tipos de escaneos.

### -sF (Sondeo FIN):
Similar al sondeo NULL, este envía un paquete TCP con el indicador FIN establecido. Es como si estuvieras cerrando una conexión TCP de forma abrupta.
También se utiliza para evadir la detección, ya que el sondeo FIN puede pasar desapercibido para algunos sistemas de seguridad. Es útil para identificar dispositivos que pueden estar ocultos o que tienen configuraciones de seguridad específicas.

### -sX (Sondeo Xmas):
Este sondeo envía un paquete TCP con los indicadores FIN, PSH y URG establecidos, iluminando la "Xmas tree" del paquete TCP. Es como si decoramos un árbol de Navidad con luces brillantes.
Al igual que los sondeos NULL y FIN, se utiliza para evadir la detección. Puede ser útil para encontrar dispositivos que están configurados de manera diferente o que tienen medidas de seguridad específicas.

Puedes combinar estos sondeos con otros en Nmap para obtener resultados más completos. Por ejemplo, puedes usar "-sN" y "-sF" junto con otros parámetros de escaneo para realizar un escaneo más exhaustivo de una red y detectar posibles vulnerabilidades o configuraciones de seguridad débiles.

### Sondeo Null(-sN)
No fija ningún bit (la cabecera de banderas TCP es 0)

### sondeo FIN (-sF)
Solo fija el bit TCP FIN.

### sondeo Xmas (-sX)
Fija los bits de FIN, PSH, y URG flags, iluminando el paquete como si fuera un árbol de Navidad.

Estos tres tipos de sondeos son exactamente los mismos en comportamiento salvo por las banderas TCP que se fijen en los paquetes de la sonda. Si se recibe un paquete RST entonces se considera que el puerto está cerrado. Si no se recibe ninguna respuesta el puerto se marca como abierto | filtrado. El puerto se marca filtrado si se recibe un error ICMP no alcanzable (tipo 3, código 1, 2, 3, 9, 10, o 13).

La ventaja fundamental de este tipo de sondeos es que pueden atravesar algunos cortafuegos que no hagan inspección de estados o encaminadores que hagan filtrado de paquetes. Otra ventaja es que este tipo de sondeos son algo más sigilosos que, incluso, un sondeo SYN. 

Sin embargo, no cuente con que pase siempre esto ya que la mayoría de los productos IDS pueden configurarse para detectarlos. El problema es que no todos los sistemas siguen el estándar RFC 793 al pie de la letra. 

Algunos sistemas envían respuestas RST a las sondas independientemente de si el puerto está o no cerrado. Esto hace que la mayoría de los puertos se marquen como cerrados. Algunos sistemas operativos muy utilizados que hacen ésto son Microsoft Windows, muchos dispositivos Cisco, BSDI, e IBM OS/400. 

Este sondeo no funciona contra sistemas basados en UNIX. Otro problema de estos sondeos es que no se puede distinguir los puertos abiertos de algunos puertos filtrados, lo que resulta en la respuesta abierto | filtrado.

Abierto | Filtrado:
Esta respuesta indica que el puerto puede estar abierto, pero el firewall u otro dispositivo de red está bloqueando los intentos de conexión de Nmap. En otras palabras, no se ha recibido ninguna respuesta del dispositivo objetivo (ni una confirmación de conexión ni un mensaje indicando que el puerto está bloqueado). Esto puede ser debido a configuraciones de firewall que bloquean o limitan el acceso desde ciertas direcciones IP.
Los puertos marcados como "abierto | filtrado" son potencialmente accesibles, pero también están protegidos por algún tipo de filtro de red, lo que dificulta la determinación precisa de su estado.
Filtrado:
Cuando Nmap muestra simplemente "filtrado", significa que el escáner no ha recibido ninguna respuesta del puerto en absoluto. Esto puede indicar que el puerto está bloqueado por un firewall que está configurado para ignorar los intentos de conexión, lo que hace que sea imposible para Nmap determinar si el puerto está abierto o cerrado.
Los puertos marcados como "filtrado" son menos susceptibles a ataques porque el firewall o el dispositivo de red no está proporcionando ninguna información sobre su estado. Esto dificulta que un atacante determine si el puerto está realmente abierto y, por lo tanto, dificulta el desarrollo de un ataque efectivo.




15

### -sA (sondeo TCP ACK)
Este sondeo es distinto de otros que se han discutido hasta ahora en que no puede determinar puertos abiertos (o incluso abiertos | filtrados). Se utiliza para mapear reglas de cortafuegos, y para determinar si son cortafuegos con inspección de estados y qué puertos están filtrados.

MIL PERDONES POR EL AUDIO PERO VOLVIO A FALLAR.

La sonda de un sondeo ACK sólo tiene fijada la bandera ACK (a menos que utilice --scanflags). Cuando se sondean sistemas no filtrados los puertos abiertos y cerrados devolverán un paquete RST. Nmap marca el puerto como no filtrado, lo que significa que son alcanzables por el paquete ACK, pero no se puede determinar si están abiertos o cerrados. Los puertos que no responden o que envían mensajes de error ICMP en respuesta (tipo 3, código 1, 2, 3, 9, 10, o 13), se marcan como filtrados.

Puertos abiertos o cerrados RESPONDEN RST → Nmap los marca como NO FILTRADO
Puertos no responden o dan error ICMP → Nmap los marca como FILTRADOS



16

### -sT (sondeo TCP connect ())
El sondeo TCP Connect () es el sondeo TCP por omisión cuando no se puede utilizar el sondeo SYN. Esto sucede, por ejemplo, cuando el usuario no tiene privilegios para enviar paquetes en crudo o cuando se están sondeando redes IPv6. Nmap le pide al sistema operativo subyacente que establezcan una conexión con el sistema objetivo en el puerto indicado utilizando la llamada del sistema connect (), a diferencia de otros tipos de sondeo, que escriben los paquetes a bajo nivel. Ésta es la misma llamada del sistema de alto nivel que la mayoría de las aplicaciones de red, como los navegadores web o los clientes P2P, utilizan para establecer una conexión. 

Generalmente es mejor utilizar un sondeo SYN, si éste está disponible. Nmap tiene menos control sobre la llamada de alto nivel Connect () que cuando utiliza paquetes en crudo, lo que hace que sea menos eficiente. La llamada al sistema completa las conexiones para abrir los puertos objetivo, en lugar de realizar el reseteo de la conexión medio abierta como hace el sondeo SYN. Esto significa que se tarda más tiempo y son necesarios más paquetes para obtener la información, pero también significa que los sistemas objetivos van a registrar probablemente la conexión. Un IDS decente detectará cualquiera de los dos, pero la mayoría de los equipos no tienen este tipo de sistemas de alarma. Sin embargo, muchos servicios de los sistemas UNIX habituales añadirán una nota en el syslog, y algunas veces con un mensaje de error extraño, dado que Nmap realiza la conexión y luego la cierra sin enviar ningún dato. Los servicios realmente patéticos morirán cuando ésto pasa, aunque esto no es habitual. Un administrador que vea muchos intentos de conexión en sus registros que provengan de un único sistema debería saber que ha sido sondeado con este método.

### -sU (sondeos UDP)
AL FINAL DEL VIDEO COMETI UN ERROR, los puertos estan abiertos filtrados porque el FIREWALL no respondio con nada, no se recibio un mensaje de error ICMP.

Aunque la mayoría de los servicios más habituales en Internet utilizan el protocolo TCP, los servicios UDP también son muy comunes. Tres de los más comunes son los servicios DNS, SNMP, y DHCP (puertos registrados 53, 161 / 162, y 67 / 68 respectivamente). Dado que el sondeo UDP es generalmente más lento y más difícil que TCP, algunos auditores de seguridad ignoran estos puertos. Esto es un error, porque es muy frecuente encontrarse servicios UDP vulnerables y los atacantes no ignoran estos protocolos. Afortunadamente, Nmap puede utilizarse para hacer un inventario de puertos UDP.

El sondeo UDP se activa con la opción -sU. Puede combinarse con un tipo de sondeo TCP como el sondeo SYN (-sS) para comprobar ambos protocolos al mismo tiempo.

Los sondeos UDP funcionan mediante el envío (sin datos) de una cabecera UDP para cada puerto objetivo. Si se obtiene un error ICMP que indica que el puerto no es alcanzable (tipo 3, código 3) entonces se marca el puerto como cerrado. Si se recibe cualquier error ICMP no alcanzable (tipo 3, códigos 1, 2, 9, 10, o 13) se marca el puerto como filtrado. En algunas ocasiones se recibirá una respuesta al paquete UDP, lo que prueba que el puerto está abierto. Si no se ha recibido ninguna respuesta después de algunas retransmisiones entonces se clasifica el puerto como abierto | filtrado. Esto significa que el puerto podría estar abierto o que hay un filtro de paquetes bloqueando la comunicación. Puede utilizarse el sondeo de versión (-sV) para diferenciar de verdad los puertos abiertos de los filtrados.

Uno de los grandes problemas con el sondeo UDP es hacerlo rápidamente. Pocas veces llega una respuesta de un puerto abierto o filtrado, lo que obliga a expirar a Nmap y luego a retransmitir los paquetes en caso de que la sonda o la respuesta se perdieron. Los puertos cerrados son aún más comunes y son un problema mayor. Generalmente envían un error ICMP de puerto no alcanzable. Pero, a diferencia de los paquetes RST que envían los puertos TCP cerrados cuando responden a un sondeo SYN o Connect, muchos sistemas imponen una tasa máxima de mensajes ICMP de puerto inalcanzable por omisión. Linux y Solaris son muy estrictos con esto. Por ejemplo, el núcleo de Linux versión 2.4.20 limita la tasa de envío de mensajes de destino no alcanzable a uno por segundo.

Nmap detecta las limitaciones de tasa y se ralentiza para no inundar la red con paquetes inútiles que el equipo destino acabará descartando. Desafortunadamente, un límite como el que hace el núcleo de Linux de un paquete por segundo hace que un sondeo de 65536 puertos tarde más de 18 horas. Puede acelerar sus sondeos UDP incluyendo más de un sistema para sondearlos en paralelo, haciendo un sondeo rápido inicial de los puertos más comunes, sondeando detrás de un cortafuegos, o utilizando la opción --host-timeout para omitir los sistemas que responda con lentitud.



17

### Detección de servicios y de versiones
Si le indica a Nmap que mire un sistema remoto le podrá decir que tiene abiertos los puertos 25/tcp, 80/tcp y 53/udp. Informará que esos puertos se corresponden habitualmente con un servidor de correo (SMTP), servidor de web (HTTP) o servidor de nombres (DNS), respectivamente, si utilizas su base de datos nmap-services con más de 2.200 puertos conocidos. Generalmente este informe es correo dado que la gran mayoría de demonios que escuchan en el puerto 25 TCP son, en realidad, servidores de correo. ¡Pero no debe confiar su seguridad en este hecho! La gente ejecuta a veces servicios distintos en puertos inesperados

Aún en el caso de que Nmap tenga razón y el servidor de ejemplo indicado arriba está ejecutando servidores de SMTP, HTTP y DNS ésto no dice mucho. Cuando haga un análisis de vulnerabilidades (o tan sólo un inventario de red) en su propia empresa o en su cliente lo que habitualmente también quiere saber es qué versión se está utilizando del servidor de correcto y de DNS. Puede ayudar mucho a la hora de determinar qué ataques pueden afectar a un servidor el saber el número de versión exacto de éste. La detección de versiones le ayuda a obtener esta información.

Por supuesto, la mayoría de los servicios no ofrecen toda esta información. 

Si se ha compilado Nmap con soporte OpenSSL se conectará también a servidores SSL para determinar qué servicio escucha detrás de la capa de cifrado. Se utiliza la herramienta de pruebas RPC de Nmap (-sR) de forma automática para determinar el programa RPC y el número de versión si se descubren servicios RPC. 

Algunos puertos UDP se quedan en estado open|filtered, si un barrido de puertos UDP no puede determinar si el puerto está abierto o filtrado. La detección de versiones intentará obtener una respuesta de estos puertos (igual que hace con puertos abiertos) y cambiará el estado a abierto si lo consigue. 

Los puertos TCP en estado open|filtered se tratan de forma similar. Tenga en cuenta que la opción -A de Nmap actualiza la detección de versiones entre otras cosas. Puede encontrar un documento describiendo el funcionamiento, modo de uso, y particularización de la detección de versiones en https://nmap.org/vscan/.

La detección de versiones se activa y controla con la siguientes opciones:

### -sV (Detección de versiones)
Activa la detección de versiones como se ha descrito previamente. Puede utilizar la opción -A en su lugar para activar tanto la detección de versiones como la detección de sistema operativo.

--allports (No excluir ningún puerto de la detección de versiones)
La detección de versiones de Nmap omite el puerto TCP 9100 por omisión porque algunas impresoras imprimen cualquier cosa que reciben en este puerto, lo que da lugar a la impresión de múltiples páginas con solicitudes HTTP get, intentos de conexión de SSL, etc. Este comportamiento puede cambiarse modificando o eliminando la directiva Exclude en nmap-service-probes, o especificando --allports para sondear todos los puertos independientemente de lo definido en la directiva Exclude.

--version-intensity intensidad (Fijar la intensidad de la detección de versiones)
Nmap envía una serie de sondas cuando se activa la detección de versiones (-sV) con un nivel de rareza pre asignado y variable de 1 a 9. Las sondas con un número bajo son efectivas contra un amplio número de servicios comunes, mientras que las de números más altos se utilizan rara vez. El nivel de intensidad indica que sondas deberían utilizarse. Cuanto más alto sea el número, mayor las probabilidades de identificar el servicio. Sin embargo, los sondeos de alta intensidad tardan más tiempo. El valor de intensidad puede variar de 0 a 9. El valor por omisión es 7. Se probará una sonda independientemente del nivel de intensidad cuando ésta se registra para el puerto objetivo a través de la directiva nmap-service-probes ports. De esta forma se asegura que las sondas de DNS se probarán contra cualquier puerto abierto 53, las sondas SSL contra el puerto 443, etc.

--version-light (Activar modo ligero)
Éste es un alias conveniente para --version-intensity 2. Este modo ligero hace que la detección de versiones sea más rápida pero también hace que sea menos probable identificar algunos servicios.

--version-all (Utilizar todas las sondas)
Éste es un alias para --version-intensity 9, hace que se utilicen todas las sondas contra cada puerto.

--version-trace (Trazar actividad de sondeo de versiones)
Esta opción hace que Nmap imprima información de depuración detallada explicando lo que está haciendo el sondeo de versiones. Es un conjunto de lo que obtendría si utilizara la opción --packet-trace.
