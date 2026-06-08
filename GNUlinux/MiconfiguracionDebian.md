
## Aplicaciones lenguajes esenciales 

```bash
sudo apt install -y build-essential make
sudo apt install -y htop tree zip unzip
sudo apt install -y gcc g++ python3 python3-pip perl ruby
sudo apt install -y dysk # altervativa mejor al comando df 
sudo apt install -y git curl 
sudo apt install -y default-jre # java
sudo apt install -y mpv vlc #reproductores de videos

```
## Configuracion de **.bashcr**

### Alias

```
alias actualizarsistema="sudo apt update && sudo apt upgrade -y && flatpak update -y && sudo snap refresh"
alias apagar='sudo shutdown now'
alias reiniciar='sudo reboot now'
alias ff='fastfetch'
alias nv='~/AppimagePaketes/nvim-linux-x86_64.appimage'
alias p3='python3'
alias buscar='sudo apt search'
alias instalar='sudo apt install'
#alias l='ls -l'
alias l='lsd -l'
#alias ld='ls -l --group-directories-first'
alias ld='lsd -l --group-directories-first'
#alias ll='ls -la'
alias ll='lsd -la'
#alias lld='ls -la --group-directories-first'
alias lld='lsd -la --group-directories-first'
#alias nf='neofetch' desactualizado
alias e='exit'
alias act='sudo apt update && sudo apt upgrade -y'
alias eliminar='sudo apt-get --purge remove'

# --- Git Alias ---
alias gi='git init'
alias ga='git add'
alias gad='git add .'
alias gc='git commit'
alias gp='git push'
alias gs='git status'
alias gss='git status -s'
alias gl='git log'
alias glo='git log --oneline'
alias gb='git branch'
alias gcl='git clone'

# --- Otros ---
alias raspby='ssh minimini@192.168.0.27'
alias pingraspby='ping 192.168.0.27'
alias peke='ssh peke@192.168.0.41'
alias pingpeke='ping 192.168.0.41'
alias cerrarss='bspc quit' #cierra cesion de usuario

# --- flatpak ---
alias actflat='flatpak update' # actualiza todo
alias listaflat='flatpak list --app'
alias eliminarflat='flatpak uninstall' # mas el id de la aplicacion
alias eliminaflatt='flatpak uninstall --delete-data' # mas id elina todo + configuraciones
alias limpiarflat='flatpak uninstall --unused' # limpia archivos obsoletos

# --- snap ---
alias actsnap='sudo snap refresh' # actualiza todos los snap
alias listasnap='snap list'
alias eliminarsnap='sudo snap remove' # mas nombre del paquete
alias eliminasnapt='sudo snap remove --purge' # mas nombre del paquete elimina todo 


# ff ejecuta fastfecth
ff
```

### Prompt

```bash
export PS1='\[\033[01;36m\] \[\033[01;33m\]\u \[\033[01;31m\]@ \h  \[\033[01;34m\] \w \[\033[1;32m\]\n$(__git_ps1 "N_rama %s"" "" ")\[\033[1;36m\]\$\[\033[00m\]'
```

## Neovim 

Pagina release: https://github.com/neovim/neovim/releases

```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux-x86_64.appimage
chmod u+x nvim-linux-x86_64.appimage
```
#### NvChad

Pagina: https://nvchad.com/docs/quickstart/install/
Si el directorio ~/.config/nvim no esta creado, crearlo. Luego clonar el repositorio en ~/.config/nvim

```bash
mkdir -p ~/.config/nvim
git clone https://github.com/NvChad/starter ~/.config/nvim
```

Para eliminar nvcahd eliminar los siguientes directrorios:

```bash
rm -rf ~/.config/nvim
rm -rf ~/.local/state/nvim
rm -rf ~/.local/share/nvim
```

## Calculadora

```bash
sudo apt install kcalc
```

## Libre wolf

```
sudo apt install extrepo    # Repositorio Externos para librewolf
sudo extrepo enable librewolf    # Habilitamos 
sudo apt update
sudo apt install librewolf -y
```

## LSD

https://github.com/lsd-rs/lsd/releases

Bajar el archivo: lsd-musl_1.1.5_amd64.deb 
O descargarlo con curl:

```bash
curl -LO https://github.com/lsd-rs/lsd/releases/download/v1.1.5/lsd-musl_1.1.5_amd64.deb
```

## Fastfetch

pagina: https://github.com/fastfetch-cli/fastfetch
pagina release: https://github.com/fastfetch-cli/fastfetch/releases
O descargar con curl:

```bash
curl -LO https://github.com/fastfetch-cli/fastfetch/releases/download/2.47.0/fastfetch-linux-amd64.deb
```

## BTOP utilizando

```bash
sudo apt install btop -y
```

## Juegos

```bash
sudo apt install ace-of-penguins -y
```

## gtkpod
https://snapcraft.io/install/gtkpod/debian

```bash
sudo apt update

# si no esta instalado snap
sudo apt install snapd 
sudo snap install snapd
sudo snap install gtkpod
```
## Monitoreos del hard

### CPU-X

Herramienta para monitorear cpu

```bash
sudo apt install cpu-x
```
### gsmatcontrol

Herramienta para monitorear y testear estado de unidades de almacenamineto

```bash
sudo apt install gsmartcontrol
```
### MangoHud

Overlay de juegos: Muestra FPS, CPU/GPU temps, uso de RAM en tiempo real dentro de videojuegos.

```bash
sudo apt install mangohud
```

### lm-sensors

Lectura de sensores: Muestra temperaturas de CPU/GPU, voltajes y velocidad de ventiladores.

```bash
sudo apt install lm-sensors
```

### glances
Monitor todo-en-uno: CPU, RAM, red, discos y procesos en una sola pantalla (modo terminal).

```bash
sudo apt install glances
```

### hardinfo
Especificaciones técnicas: Detalla hardware (modelos de componentes) y hace tests básicos.

```bash
sudo apt install hardinfo
```

### hwinfo
Detective de hardware: Similar a hardinfo pero más técnico (info avanzada de dispositivos).

```bash
sudo apt install hwinfo
```

### inxi
Resumen express: Da un reporte compacto de sistema (ideal para foros/troubleshoot


```bash
sudo apt install inxi
```

### htop
"Top" mejorado: Monitor de procesos con interfaz interactiva (más amigable que top).

```bash
sudo apt install htop
```

### bpytop
Glances con esteroides: Versión mejorada con gráficos y más detalle (colorido y personalizable).

```bash
sudo apt install bpytop
```

### nvtop 
Monitor de GPU NVIDIA: Muestra uso VRAM, temperatura y clocks (también soporta AMD/Intel).

```bash
sudo apt install nvtop
```

### iotop
Vigilante de discos: Detecta qué programas están matando tu SSD/HDD (I/O en tiempo real).

```bash
sudo apt install iotop
```

## WAYDROID

Herramineta basado en contenedores para iniciar un sistema Android completo en sistemas GNU/Linux 

https://waydro.id/
https://docs.waydro.id/usage/install-on-desktops

```bash
sudo apt install curl ca-certificates -y
```

```bash
curl -s https://repo.waydro.id | sudo bash
```

```bash
sudo apt install waydroid -y
```
Pasos adicionales a la instalacion de waydroid

pagina: https://planetatecno.com.uy/planeta/2024/02/23/como-instalar-android-en-linux-y-con-cualquier-entorno-de-escritorio-xfce-gnome-cinnamon-etc/
video tutorial: https://www.youtube.com/watch?v=Gt-5bFwXg0g
instalar weston :

```bash
sudo apt install weston -y
```
Levantar el servicio waydroid-container

```bash
sudo systemctl start waydroid-container 
```

EJecutar weston desde la terminal.Abrir la terminal de weston y ejecutar el siguiente comando:

```bash
waydroid show-full-ui
```

Para terminar de usar Waydroid realizar los siguientes pasos:

1- Cerrar la ventana de Weston (la que tiene Lineage OS)
2- terminar el servicio de Waydroid con el siguiente comando (libera la memoria RAM): 

```bash
sudo systemctl stop waydroid-container.service 
```

Para activar sertificados realizar los siguentes pasos:
Abrir la terminal y ejecutar:

```bash
sudo waydroid shell
```

Luego ahi mismo pegar el siguiente comando:

```bash
ANDROID_RUNTIME_ROOT=/apex/com.android.runtime ANDROID_DATA=/data ANDROID_TZDATA_ROOT=/apex/com.android.tzdata ANDROID_I18N_ROOT=/apex/com.android.i18n sqlite3 /data/data/com.google.android.gsf/databases/gservices.db "select * from main where name = \"android_id\";"
```

Luego no dara un id como el siguiente: android_id|4423610646080920156
luego ir al enlace que aparece en la pagina https://docs.waydro.id/faq/google-play-certification y pegar el id, osea los numeros.

## VPN RiseupVPN

https://riseup.net/es
https://riseup.net/es/linux#debian

```bash
sudo apt install riseup-vpn
```



```bash
sudo apt install 
```


---


## 🛠️ Guía de Rescate: Bluetooth en Linux

### 1. Verificación de Hardware (¿Está conectado?)
Antes de instalar nada, hay que ver si el sistema detecta el "fierro".
* **Comando:** `lsusb`
* **Qué buscar:** Una línea que diga algo como `Cambridge Silicon Radio` o `Bluetooth Dongle`. 
* **Tip:** Si no aparece, cambia de puerto USB (los 2.0 suelen ser más compatibles que los 3.0 para estos adaptadores baratos).

### 2. Verificación de Software y Errores
Para ver si el sistema está intentando usarlo y falla:
* **Ver logs del sistema:** `dmesg | grep -i bluetooth`
    * *Errores comunes:* "firmware file not found" o "command tx timeout" (indican falta de drivers o clones chinos).
* **Verificar bloqueos:** `rfkill list`
    * Si dice `Soft blocked: yes`, se arregla con: `sudo rfkill unblock bluetooth`.

### 3. Instalación de Drivers y Herramientas

#### Opción A: Sistemas modernos (Tu caso actual)
```bash
sudo apt update
sudo apt install bluetooth bluez bluez-tools bluez-firmware rfkill blueman
```

#### Opción B: Sistemas antiguos o "viejitos"
A veces los paquetes tenían otros nombres:
```bash
sudo apt install bluez bluez-utils bluez-firmware
```

### 4. Gestión del Servicio (El "Motor")
Sin el servicio corriendo, el Bluetooth no existe para el sistema.
* **Ver estado:** `sudo systemctl status bluetooth`
* **Activar y arrancar:** `sudo systemctl enable --now bluetooth`
* **Reiniciar si falla:** `sudo systemctl restart bluetooth`

### 5. Permisos de Usuario
Fundamental para que tu usuario pueda manejar el adaptador sin ser "root".
* **Ver tus grupos:** `groups` o `id`
* **Añadirte al grupo:** `sudo usermod -aG bluetooth $USER`
* **Verificar cambio:** `grep "bluetooth" /etc/group`
* *Nota:* Requiere cerrar sesión o reiniciar para que surta efecto.

### 6. Interfaz Gráfica (El Ícono)
Si el Bluetooth funciona pero no ves el ícono en la barra:
* **Instalar el gestor:** `sudo apt install blueman`
* **Lanzarlo manualmente:** Presiona `Alt + F2` y escribe `blueman-applet`, luego Enter.
* **Abrir el panel de control:** Escribe `blueman-manager` en la terminal o búscalo como "Gestor de Bluetooth".


> [!TIP]
> **Resumen cuando no tenemos instaldo el servicio :**
> El problema era que el sistema no tenía instalado el servicio (`bluez`) ni el gestor gráfico (`blueman`). Al instalar `bluez-firmware`, le diste las instrucciones necesarias al chip "Cambridge" para que sepa cómo operar en Linux.

¡Cualquier otra duda con la terminal, acá estamos, chamaco!

---



## Esta configuracion se encuentra en el siguiente repo:

https://github.com/marianodeb/Miconfigdeb.git
























