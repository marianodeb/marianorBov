
## 1. Definición y Significado
**nmcli** significa **Network Manager Command Line Interface**. 

Es una herramienta de línea de comandos utilizada para controlar el **NetworkManager**, que es el programa (demonio) encargado de gestionar las conexiones de red en la mayoría de las distribuciones modernas (Ubuntu, Debian, Fedora, CentOS, Arch, etc.).

* **¿Para qué sirve?** Permite crear, mostrar, editar, eliminar, activar y desactivar conexiones de red (WiFi, Ethernet, VPN, Puentes) sin necesidad de una interfaz gráfica.


## 2. Instalación (si no viene por defecto)
Normalmente viene instalado en versiones "Desktop", pero en versiones "Server" o "Minimal" podrías tener que instalarlo:

* **Debian / Ubuntu / Raspberry Pi OS:**
    `sudo apt update && sudo apt install network-manager`
* **RHEL / CentOS / Fedora:**
    `sudo dnf install NetworkManager`
* **Arch Linux:**
    `sudo pacman -S networkmanager`

> **Importante:** Después de instalarlo, debes asegurarte de que el servicio esté corriendo:
> `sudo systemctl enable --now NetworkManager`


## 3. Sintaxis General
La estructura de `nmcli` es muy lógica y jerárquica:

`nmcli [OPCIONES] OBJETO { COMANDO | help }`

Los **objetos** principales son:
* **device (dev):** Se refiere al hardware físico (la tarjeta de red, e.g., `eth0`, `wlan0`).
* **connection (con):** Se refiere a los "perfiles" de configuración (la configuración guardada para una red específica).


## 4. Opciones y Comandos Principales

### Para Dispositivos (`device`)
* `nmcli dev status`: Muestra qué tarjetas tienes y si están conectadas.
* `nmcli dev wifi list`: Escanea y muestra las redes WiFi disponibles.
* `nmcli dev show [interfaz]`: Muestra detalles técnicos (IP, MAC, DNS) de una tarjeta.

### Para Conexiones (`connection`)
* `nmcli con show`: Lista todos los perfiles guardados.
* `nmcli con up [nombre]`: Activa una conexión.
* `nmcli con down [nombre]`: Desactiva una conexión.
* `nmcli con add`: Crea una nueva conexión.
* `nmcli con mod`: Modifica una conexión existente.
* `nmcli con del`: Borra una conexión.



## 5. Ejemplos (Simples y Complejos)

### Ejemplos Simples
1.  **Ver tu IP actual rápido:**
    `nmcli device show wlan0 | grep IP4.ADDRESS`
2.  **Conectarse a un WiFi nuevo:**
    `nmcli dev wifi connect "MiRedWiFi" password "MiClave123"`
3.  **Apagar el WiFi por completo:**
    `nmcli radio wifi off`

### Ejemplos Complejos
1.  **Crear una IP estática desde cero (Ethernet):**
    ```bash
    sudo nmcli con add type ethernet con-name "MiServidor" ifname eth0 ip4 192.168.0.100/24 gw4 192.168.0.1
    ```
2.  **Cambiar el DNS de una conexión existente a los de Cloudflare:**
    ```bash
    sudo nmcli con mod "TeleCentro-ff00" ipv4.dns "1.1.1.1, 1.0.0.1"
    sudo nmcli con up "TeleCentro-ff00"
    ```
3.  **Crear un "Bridge" (Puente) para máquinas virtuales:**
    ```bash
    sudo nmcli con add type bridge con-name br0 ifname br0
    sudo nmcli con add type bridge-slave con-name br0-port ifname eth0 master br0
    ```


## 6. Consejos de "Pro"
* **Tabulación:** `nmcli` soporta el autocompletado con la tecla **TAB**. Si no sabes qué sigue, presiona TAB dos veces y te dará las opciones.
* **Abreviaturas:** No hace falta escribir todo. `nmcli connection show` es lo mismo que `nmcli con sh`.
* **Modo Interactivo:** Si pones `nmcli con edit "Nombre"`, entrarás en un menú interactivo tipo "consola" donde puedes cambiar valores paso a paso.
* **Cuidado con el SSH:** Siempre que cambies IPs o hagas un `con up`, hazlo sabiendo que tu sesión actual se cerrará si estás por red.


## 7. Información Adicional y Sustitutos

### ¿Hay algo más nuevo?
`nmcli` es actualmente el **estándar** moderno. Sin embargo, históricamente se usaban otros que quizás encuentres en tutoriales viejos:
1.  **`ifconfig` / `route` / `arp`:** (Paquete `net-tools`). Están obsoletos. No los uses a menos que sea una emergencia en un sistema muy viejo.
2.  **`ip` (comando):** (Paquete `iproute2`). Ejemplo: `ip addr`. Es excelente para ver estados rápido, pero **no guarda los cambios tras reiniciar**. `nmcli` sí los guarda.
3.  **`nmtui`:** Es el "hermano visual" de `nmcli`. Si escribes `sudo nmtui` en la terminal, verás una interfaz de cuadritos muy fácil de usar para configurar la red sin comandos largos.



### Comandos Relacionados
* **`hostnamectl`:** Para cambiar el nombre de tu Raspberry (el "hostname").
* **`ping`:** Para probar si tienes salida a internet.
* **`dig` o `nslookup`:** Para verificar si tus DNS están funcionando.

