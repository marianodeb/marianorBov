# rfkill 


##  Guía Maestra del Comando `rfkill`

### 1. Definición y Significado
**RFKILL** significa **Radio Frequency Kill**. Es una herramienta del kernel de Linux que permite consultar, habilitar y deshabilitar los dispositivos de emisión de radiofrecuencia (Wi-Fi, Bluetooth, NFC, etc.).

Su función principal es evitar que los dispositivos inalámbricos consuman energía o emitan señales cuando no se necesitan, actuando como un interruptor de seguridad a nivel de software.

### 2. Instalación (Si no viene por defecto)
En la mayoría de las distros modernas viene instalado, pero si te falta (como nos pasó antes), se instala así:

* **Debian / Ubuntu / Mint:** `sudo apt install rfkill`
* **Arch Linux:** `sudo pacman -S util-linux` (viene dentro de las utilidades básicas).
* **Fedora / Red Hat:** `sudo dnf install util-linux`

### 3. Sintaxis básica
La estructura del comando es muy sencilla:
`rfkill [opción] [acción] [ID o tipo]`

### 4. Todas sus opciones y acciones

| Acción / Opción | Descripción |
| :--- | :--- |
| **`list`** (u `ok`) | Muestra todos los dispositivos de radio y su estado de bloqueo. |
| **`block`** | Desactiva (bloquea) el dispositivo. |
| **`unblock`** | Activa (desbloquea) el dispositivo. |
| **`help`** | Muestra la ayuda rápida del comando. |
| **`--json`** | Muestra la salida en formato JSON (ideal para programar scripts). |
| **`--output`** | Permite elegir qué columnas ver (ID, TYPE, DEVICE, SOFT, HARD). |

---

### 5. Ejemplos de uso

#### Ejemplos Simples:
* **Listar todo:**
    `rfkill list`
* **Bloquear el Bluetooth:**
    `rfkill block bluetooth`
* **Desbloquear todo el Wi-Fi:**
    `rfkill unblock wlan`

#### Ejemplos Complejos:
* **Bloquear un dispositivo específico por su ID:**
    Si al hacer `rfkill list` el Bluetooth tiene el **ID 1**, puedes apagar solo ese:
    `rfkill block 1`
* **Modo Avión total (Bloqueo total):**
    `rfkill block all`
* **Ver solo el estado de bloqueo en una tabla limpia:**
    `rfkill --output ID,TYPE,SOFT,HARD`


### 6. Consejos de experto
1.  **Diferencia entre Soft y Hard Block:**
    * **Soft Block:** Es un bloqueo por software. Tú tienes el control. Si dice "yes", lo arreglas con `rfkill unblock`.
    * **Hard Block:** Es un bloqueo físico. Puede ser un botón en el gabinete o una tecla `Fn`. Si dice "yes", **ningún comando de Linux podrá activarlo** hasta que toques el botón físico.
2.  **Uso de sudo:** Para listar (`list`) no necesitas permisos, pero para bloquear o desbloquear (`block/unblock`) **siempre** debes usar `sudo`.
3.  **Persistencia:** A veces, al reiniciar, el sistema vuelve a bloquear el Bluetooth. Si te pasa, puedes agregar `rfkill unblock bluetooth` a tus scripts de inicio.


### 7. Información Adicional y Detalles
* **Ubicación en el sistema:** `rfkill` interactúa directamente con el sistema de archivos de dispositivos en `/dev/rfkill`.
* **¿Sustituto más nuevo?:** No hay un sustituto directo que lo haya "matado", pero herramientas modernas como **NetworkManager** (`nmcli`) tienen sus propios comandos para esto. Sin embargo, `rfkill` sigue siendo la herramienta de nivel más bajo y confiable.

#### Comandos relacionados:
* **`nmcli` (Network Manager CLI):**
    * `nmcli radio wifi off` (apaga el wifi).
    * `nmcli radio bluetooth on` (enciende el bluetooth).
* **`bluetoothctl`:** Es la herramienta específica para gestionar conexiones de dispositivos Bluetooth (emparejar, conectar, escanear). Mientras `rfkill` enciende la antena, `bluetoothctl` gestiona qué conectas a ella.
* **`ip link`:** Para ver el estado de las interfaces de red a nivel de red, no de radiofrecuencia.



### Resumen de la "Línea de Vida" del Bluetooth:
1.  **`lsusb`**: ¿El hardware está conectado?
2.  **`rfkill`**: ¿La antena tiene permiso para emitir señal?
3.  **`systemctl`**: ¿El software (servicio) está corriendo?
4.  **`blueman` / `bluetoothctl`**: ¿Puedo buscar y conectar un dispositivo?

