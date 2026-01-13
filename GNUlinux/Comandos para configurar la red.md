
### Configuración de Red

1. **`ifconfig`**: Configura interfaces de red (aunque está obsoleto en muchas distribuciones, reemplazado por `ip`).
   - **Sintaxis**: `ifconfig interfaz opciones`
   - **Ejemplo**: `ifconfig eth0 up`

2. **`ip`**: Herramienta más moderna para configurar y mostrar interfaces de red.
   - **Sintaxis**: `ip comando opciones`
   - **Ejemplo**: `ip addr show` (muestra todas las interfaces de red y sus direcciones)

3. **`nmcli`**: Herramienta de línea de comandos para controlar NetworkManager.
   - **Sintaxis**: `nmcli comando opciones`
   - **Ejemplo**: `nmcli device status` (muestra el estado de todos los dispositivos)

4. **`nmtui`**: Interfaz de usuario basada en texto para NetworkManager.
   - **Sintaxis**: `nmtui`
   - **Ejemplo**: Simplemente ejecuta `nmtui` y sigue las instrucciones en pantalla para configurar la red.

5. **`dhclient`**: Cliente DHCP para configurar interfaces de red automáticamente.
   - **Sintaxis**: `dhclient interfaz`
   - **Ejemplo**: `dhclient eth0`

### Manipulación de Archivos de Red

1. **`scp`**: Copia archivos entre hosts en una red usando SSH.
   - **Sintaxis**: `scp [opciones] fuente destino`
   - **Ejemplo**: `scp file.txt user@remotehost:/path/to/destination`

2. **`rsync`**: Sincroniza archivos y directorios entre dos ubicaciones.
   - **Sintaxis**: `rsync [opciones] fuente destino`
   - **Ejemplo**: `rsync -avz /local/path user@remotehost:/remote/path`

3. **`sftp`**: Protocolo de transferencia de archivos sobre SSH.
   - **Sintaxis**: `sftp usuario@host`
   - **Ejemplo**: `sftp user@remotehost` (una vez conectado, usa comandos similares a `ftp`)

4. **`ftp`**: Cliente para el Protocolo de Transferencia de Archivos.
   - **Sintaxis**: `ftp host`
   - **Ejemplo**: `ftp ftp.example.com`

### Comandos para Ver y Gestionar Redes

1. **`ping`**: Comprueba la conectividad de red enviando paquetes ICMP.
   - **Sintaxis**: `ping dirección`
   - **Ejemplo**: `ping google.com`

2. **`traceroute`**: Rastrea la ruta que toman los paquetes hasta un host de destino.
   - **Sintaxis**: `traceroute dirección`
   - **Ejemplo**: `traceroute google.com`

3. **`netstat`** (reemplazado por `ss` en muchas distribuciones): Muestra las conexiones de red, tablas de enrutamiento, etc.
   - **Sintaxis**: `netstat [opciones]`
   - **Ejemplo**: `netstat -tuln` (muestra todas las conexiones de red y los puertos en escucha)

4. **`ss`**: Muestra sockets y conexiones de red.
   - **Sintaxis**: `ss [opciones]`
   - **Ejemplo**: `ss -tuln` (muestra todas las conexiones de red y los puertos en escucha)

5. **`iptables`**: Configura reglas del cortafuegos (firewall).
   - **Sintaxis**: `iptables comando opciones`
   - **Ejemplo**: `iptables -L` (lista todas las reglas del cortafuegos)

6. **`ufw`**: Cortafuegos sencillo para configurar reglas de `iptables` (más fácil de usar en Ubuntu).
   - **Sintaxis**: `ufw comando`
   - **Ejemplo**: `sudo ufw enable` (habilita el cortafuegos)

7. **`iwconfig`**: Configura interfaces de red inalámbrica.
   - **Sintaxis**: `iwconfig interfaz opciones`
   - **Ejemplo**: `iwconfig wlan0 essid "mi_red"`

8. **`curl`**: Transfiere datos desde o hacia un servidor.
   - **Sintaxis**: `curl [opciones] URL`
   - **Ejemplo**: `curl http://example.com`

9. **`wget`**: Descarga archivos desde la web.
   - **Sintaxis**: `wget URL`
   - **Ejemplo**: `wget http://example.com/file.zip`

10. **`ethtool`**: Muestra y cambia la configuración de una interfaz de red Ethernet.
    - **Sintaxis**: `ethtool opciones interfaz`
    - **Ejemplo**: `ethtool eth0` (muestra información sobre la interfaz eth0)

11. **`mtr`**: Combina la funcionalidad de `ping` y `traceroute`.
    - **Sintaxis**: `mtr [opciones] destino`
    - **Ejemplo**: `mtr google.com`

