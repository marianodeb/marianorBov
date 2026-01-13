
## [[Comandos Redes y Herramientas]]

ip link show
tracert
ip addr
ipconfig
iwconfig
iw dev
ip link
[[NMap]]

### 1. `ping`
**Uso**: Verificar la conectividad con otro host.
   - `ping <dirección IP o nombre de host>`: Envía paquetes ICMP Echo Request al host y muestra las respuestas.
   - `ping -c <número>`: Envía un número específico de paquetes y luego termina. Ejemplo: `ping -c 4 <dirección IP>`.

### 2. `traceroute`
**Uso**: Rastrear la ruta que toma un paquete hasta un destino.
   - `traceroute <dirección IP o nombre de host>`: Muestra la ruta y el tiempo de tránsito de los paquetes a través de la red.
   - `traceroute -m <máx_hops>`: Establece el número máximo de saltos (hops) para rastrear. Ejemplo: `traceroute -m 20 <dirección IP>`.

### 3. `netstat`
**Uso**: Mostrar estadísticas de red y conexiones activas.
   - `netstat -tuln`: Muestra los puertos en escucha (listening) para TCP (`-t`), UDP (`-u`), sin resolver nombres de host (`-n`).
   - `netstat -an`: Muestra todas las conexiones y puertos en escucha en formato numérico.

### 4. `ss`
**Uso**: Herramienta avanzada para examinar sockets y conexiones de red.
   - `ss -tuln`: Muestra puertos en escucha para TCP (`-t`), UDP (`-u`).
   - `ss -s`: Muestra un resumen de las conexiones y el uso de los sockets.

### 5. `ifconfig`
**Uso**: Configurar y mostrar información de interfaces de red.
   - `ifconfig`: Muestra las interfaces de red y su configuración actual.
   - `ifconfig <interfaz> up/down`: Activa o desactiva una interfaz específica. Ejemplo: `ifconfig eth0 down`.

### 6. `ip`
**Uso**: Comando moderno para gestionar la configuración de red.
   - `ip a`: Muestra todas las interfaces de red y sus direcciones IP.
   - `ip link set <interfaz> up/down`: Activa o desactiva una interfaz. Ejemplo: `ip link set eth0 up`.
   - `ip route`: Muestra la tabla de rutas de red.

### 7. `route`
**Uso**: Mostrar y modificar la tabla de rutas IP.
   - `route -n`: Muestra la tabla de rutas IP en formato numérico.
   - `route add <destino> gw <puerta de enlace>`: Añade una ruta a la tabla de rutas. Ejemplo: `route add 192.168.1.0/24 gw 192.168.1.1`.

### 8. `arp`
**Uso**: Mostrar y manipular la caché ARP.
   - `arp -a`: Muestra la tabla ARP completa.
   - `arp -d <dirección IP>`: Elimina una entrada ARP específica. Ejemplo: `arp -d 192.168.1.1`.

### 9. `nmcli`
**Uso**: Herramienta de línea de comandos para NetworkManager.
   - `nmcli d`: Muestra el estado de los dispositivos de red.
   - `nmcli connection show`: Muestra las conexiones de red configuradas.
   - `nmcli device wifi list`: Muestra redes WiFi disponibles.

### 10. `iwconfig`
**Uso**: Configurar interfaces inalámbricas.
   - `iwconfig`: Muestra la configuración de las interfaces inalámbricas.
   - `iwconfig <interfaz> essid <nombre_red>`: Conecta a una red WiFi especificada por su SSID. Ejemplo: `iwconfig wlan0 essid MiRed`.

### 11. `ethtool`
**Uso**: Mostrar y modificar configuraciones de interfaces Ethernet.
   - `ethtool <interfaz>`: Muestra las capacidades y configuraciones actuales de la interfaz. Ejemplo: `ethtool eth0`.
   - `ethtool -s <interfaz> speed <velocidad> duplex <duplex>`: Configura la velocidad y el modo dúplex. Ejemplo: `ethtool -s eth0 speed 1000 duplex full`.

### 12. `mtr`
**Uso**: Herramienta de traceroute combinada con ping.
   - `mtr <dirección IP o nombre de host>`: Realiza un traceroute mientras muestra estadísticas de pérdida de paquetes y latencia en tiempo real.

### 13. `curl`
**Uso**: Transferir datos desde o hacia un servidor.
   - `curl <URL>`: Descarga o envía datos a una URL.
   - `curl -I <URL>`: Muestra solo las cabeceras HTTP de una respuesta.

### 14. `wget`
**Uso**: Descargar archivos de la web.
   - `wget <URL>`: Descarga un archivo desde una URL.
   - `wget -r <URL>`: Descarga un sitio web de forma recursiva.

### 15. `tcpdump`
**Uso**: Capturar y analizar tráfico de red.
   - `tcpdump -i <interfaz>`: Captura paquetes en una interfaz de red específica.
   - `tcpdump -i <interfaz> port 80`: Captura solo tráfico en el puerto 80 (HTTP).

### 16. `nmap`
**Uso**: Escanear redes para descubrir hosts y servicios.
   - `nmap <dirección IP>`: Escanea un host para puertos abiertos.
   - `nmap -sP <red>`: Realiza un escaneo de descubrimiento de hosts en una red. Ejemplo: `nmap -sP 192.168.1.0/24`.

### 17. `hostname`
**Uso**: Mostrar o establecer el nombre del host del sistema.
   - `hostname`: Muestra el nombre del host actual.
   - `hostname <nuevo_nombre>`: Cambia el nombre del host. Ejemplo: `hostname nuevo-host`.

### 18. `systemctl`
**Uso**: Administrar servicios y unidades del sistema.
   - `systemctl status <servicio>`: Muestra el estado de un servicio. Ejemplo: `systemctl status NetworkManager`.
   - `systemctl restart <servicio>`: Reinicia un servicio. Ejemplo: `systemctl restart networking`.

### 19. `netcat` (o `nc`)
**Uso**: Leer y escribir datos a través de conexiones de red utilizando TCP o UDP.
   - `nc -l <puerto>`: Escucha en el puerto especificado (modo servidor).
   - `nc <dirección IP> <puerto>`: Se conecta al puerto especificado en la dirección IP dada (modo cliente).
   - `nc -zv <dirección IP> <puertos>`: Escanea puertos en un host para ver si están abiertos. Ejemplo: `nc -zv 192.168.1.1 22 80 443`.

### 20. `iproute2` (suite de herramientas `ip`)
**Uso**: Conjunto de herramientas para manejar la configuración de red.
   - `ip addr show <interfaz>`: Muestra la configuración de la interfaz especificada.
   - `ip route show`: Muestra la tabla de rutas.
   - `ip neigh`: Muestra la tabla ARP/NDP.

### 21. `host`
**Uso**: Resolver nombres de dominio a direcciones IP y viceversa.
   - `host <nombre de dominio>`: Muestra la dirección IP asociada al nombre de dominio. Ejemplo: `host example.com`.
   - `host -t <tipo> <nombre de dominio>`: Realiza una consulta de un tipo específico. Ejemplo: `host -t MX example.com` para registros MX.

### 22. `dig`
**Uso**: Realizar consultas DNS y diagnosticar problemas DNS.
   - `dig <nombre de dominio>`: Realiza una consulta DNS. Ejemplo: `dig example.com`.
   - `dig @<servidor DNS> <nombre de dominio>`: Realiza una consulta DNS utilizando un servidor específico. Ejemplo: `dig @8.8.8.8 example.com`.

### 23. `sshd` (SSH Daemon)
**Uso**: Administrar el servicio de SSH.
   - `sshd -t`: Verifica la configuración de SSH sin iniciar el servicio.
   - `sshd -d`: Inicia el servidor SSH en modo de depuración.

### 24. `iptables`
**Uso**: Configurar las reglas del firewall de Linux.
   - `iptables -L`: Muestra las reglas actuales del firewall.
   - `iptables -A INPUT -p tcp --dport <puerto> -j ACCEPT`: Permite el tráfico TCP en el puerto especificado. Ejemplo: `iptables -A INPUT -p tcp --dport 22 -j ACCEPT`.

### 25. `ufw` (Uncomplicated Firewall)
**Uso**: Interfaz simplificada para configurar `iptables`.
   - `ufw status`: Muestra el estado del firewall.
   - `ufw allow <puerto>`: Permite el tráfico en el puerto especificado. Ejemplo: `ufw allow 22`.

### 26. `firewalld`
**Uso**: Gestión de firewall dinámica con soporte para zonas y servicios.
   - `firewall-cmd --list-all`: Muestra la configuración actual del firewall.
   - `firewall-cmd --add-port=<puerto>/tcp`: Permite el tráfico en el puerto especificado. Ejemplo: `firewall-cmd --add-port=22/tcp`.

### 27. `ncat`
**Uso**: Versión avanzada de `netcat` incluida en el paquete Nmap.
   - `ncat -l <puerto>`: Escucha en el puerto especificado.
   - `ncat <dirección IP> <puerto>`: Se conecta al puerto especificado en la dirección IP dada.

### 28. `tcpflow`
**Uso**: Capturar y reconstruir flujos de datos TCP.
   - `tcpflow -i <interfaz>`: Captura el tráfico TCP en la interfaz especificada.

### 29. `nethogs`
**Uso**: Monitorizar el uso del ancho de banda por aplicación.
   - `nethogs <interfaz>`: Muestra el uso del ancho de banda en tiempo real por aplicación. Ejemplo: `nethogs eth0`.

### 30. `iwlist`
**Uso**: Obtener información detallada sobre redes inalámbricas.
   - `iwlist <interfaz> scan`: Escanea redes inalámbricas cercanas y muestra información detallada. Ejemplo: `iwlist wlan0 scan`.

### 31. `iw`  [[iw]]
**Uso**: Herramienta para gestionar interfaces WiFi.
   - `iw dev <interfaz> scan`: Escanea redes inalámbricas cercanas. Ejemplo: `iw dev wlan0 scan`.
   - `iw dev <interfaz> connect <SSID>`: Conecta a una red WiFi especificada por su SSID. Ejemplo: `iw dev wlan0 connect MiRed`.

### 32. `dhclient`
**Uso**: Obtener una dirección IP de un servidor DHCP.
   - `dhclient <interfaz>`: Solicita una dirección IP a un servidor DHCP. Ejemplo: `dhclient eth0`.

### 33. `mii-tool`
**Uso**: Configurar y mostrar el estado de interfaces Ethernet.
   - `mii-tool <interfaz>`: Muestra el estado de la interfaz Ethernet. Ejemplo: `mii-tool eth0`.

### 34. `bmon`
**Uso**: Monitorizar el ancho de banda de la red.
   - `bmon`: Inicia una interfaz gráfica en modo texto para mostrar el uso del ancho de banda en tiempo real.

### 35. `netdiscover`
**Uso**: Descubrir dispositivos en la red local.
   - `netdiscover`: Escanea la red local y muestra una lista de dispositivos conectados.

### 36. `iperf3`
**Uso**: Medir el ancho de banda de la red entre dos hosts.
   - `iperf3 -s`: Inicia el servidor `iperf3`.
   - `iperf3 -c <dirección IP del servidor>`: Ejecuta una prueba de rendimiento como cliente contra un servidor `iperf3`.




Trabajo con la RED ( LAN y Wi-Fi)


mostrar la configuración de una tarjeta de red Ethernet.
```bash
ifconfig eth0: 
```

activar una interface ‘eth0’.

```bash
ifup eth0: 
```

deshabilitar una interface ‘eth0’.

```bash
ifdown eth0: 
```

configurar una dirección IP.

```bash
ifconfig eth0 192.168.1.1 netmask 255.255.255.0: 


configurar ‘eth0’en modo común para obtener los paquetes (sniffing).

```bash
ifconfig eth0 promisc: 
```

activar la interface ‘eth0’ en modo dhcp.

```bash
dhclient eth0: 
```

mostrar mesa de recorrido.

```bash
route -n: 
```

configurar entrada predeterminada.

```bash
route add -net 0/0 gw IP_Gateway: 
```

configurar ruta estática para buscar la red ‘192.168.0.0/16’.

```bash
route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1
```

eliminar la ruta estática.

```bash
route del 0/0 gw IP_gateway: 
```

activar el recorrido ip.

```bash
echo “1” > /proc/sys/net/ipv4/ip_forward: 
```

mostrar el nombre del host del sistema.

```bash
hostname: 
```

buscar el nombre del host para resolver el nombre a una dirección ip(1).

```bash
host www.example.com: 
```

buscar el nombre del host para resolver el nombre a una direccióm ip y viceversa(2).

```bash
nslookup www.example.com: 
```

mostar el estado de enlace de todas las interfaces.

```bash
ip link show: 
```

mostar el estado de enlace de ‘eth0’.

```bash
mii-tool eth0: 
```

mostrar las estadísticas de tarjeta de red ‘eth0’.

```bash
ethtool eth0: 
```

mostrar todas las conexiones de red activas y sus PID.

```bash
netstat -tup: 
```

mostrar todos los servicios de escucha de red en el sistema y sus PID.

```bash
netstat -tupl: 
```

mostrar todo el tráfico HTTP.

```bash
tcpdump tcp port 80: 
```

mostrar las redes inalámbricas.

```bash
iwlist scan: 
```

mostrar la configuración de una tarjeta de red inalámbrica.

```bash
iwconfig eth1: 
```

buscar en base de datos Whois.

```bash
whois www.example.com: 
```




Redes de Microsoft Windows (SAMBA)


resolución de nombre de red bios.

```bash
nbtscan ip_addr: 
```

resolución de nombre de red bios.

```bash
nmblookup -A ip_addr: 
```

mostrar acciones remotas de un host en windows.

```bash
smbclient -L ip_addr/hostname: 
```

Tablas IP (CORTAFUEGOS)

iptables -t filter -L: mostrar todas las cadenas de la tabla de filtro.


iptables -t nat -L: mostrar todas las cadenas de la tabla nat.


iptables -t filter -F: limpiar todas las reglas de la tabla de filtro.


iptables -t nat -F: limpiar todas las reglas de la tabla nat.


iptables -t filter -X: borrar cualquier cadena creada por el usuario.


iptables -t filter -A INPUT -p tcp –dport telnet -j ACCEPT: permitir las conexiones telnet para entar.


iptables -t filter -A OUTPUT -p tcp –dport http -j DROP: bloquear las conexiones HTTP para salir.
iptables -t filter -A FORWARD -p tcp –dport pop3 -j ACCEPT: permitir las conexiones POP a una cadena delantera.
iptables -t filter -A INPUT -j LOG –log-prefix “DROP INPUT”: registrando una cadena de entrada.
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE: configurar un PAT (Puerto de traducción de dirección) en eth0, ocultando los paquetes de salida forzada.
iptables -t nat -A PREROUTING -d 192.168.0.1 -p tcp -m tcp –dport 22 -j DNAT –to-destination 10.0.0.2:22: redireccionar los paquetes diriguidos de un host a otro.

## [[Diccionario ,  Abreviaturas]]



## WIFI

Comandos para poner antena modo mononitor


iw dev wlan0 set type monitor
iw dev wlan0 set type managed

airmong-ng 

airmong-ng start wlan0
airmong-ng stop wlan0
airmong-ng check kill
