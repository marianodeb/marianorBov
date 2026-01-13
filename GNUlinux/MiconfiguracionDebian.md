
## Aplicaciones lenguajes esenciales 

```bash
sudo apt install -y build-essential make
sudo apt install -y htop tree zip unzip
sudo apt install -y gcc g++ python3 python3-pip perl ruby
```
## Configuracion de **.bashcr**

### Alias

```
alias nv='/media/user/bodzzy/AppimagePaketes/nvim-linux-x86_64.appimage'
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
alias nf='neofetch'
alias e='exit'
alias act='sudo apt update && sudo apt upgrade'
alias eliminar='sudo apt-get --purge remove'

alias gi='git init'
alias ga='git add'
alias gad='git add .'
alias gc='git commit'
alias gp='git push'
alias gs='git status'
alias gss='git status -s'
alias gl='git log'
alias glo='git log --oneline'
alias gb='git git branch'
alias gcl='git clone'
alias raspby='ssh minimini@192.168.0.27'
alias pingraspby='ping 192.168.0.27'
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
Si el directorio ~/.config/nvim no esta creado crearlo. Luego clonar el repositorio en ~/.config/nvim

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
O descar con curl:

```bash
curl -LO https://github.com/fastfetch-cli/fastfetch/releases/download/2.47.0/fastfetch-linux-amd64.deb
```

## BTOP

```bash
sudo apt install btop -y
```

## Juegos

```bash
sudo apt install ace-of-penguins -y
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






## Esta configuracion se encuentra en el siguiente repo:

https://github.com/marianodeb/Miconfigdeb.git
























