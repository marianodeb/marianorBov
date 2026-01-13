

## Instalar Python

```
sudo apt install wget software-properties-common
```

Ir a la pag oficial de python y descargar la última versión gzipped source tarball

Descargar con wget , luego descomprimir con el siguiente comando

```
tar xvf nombre_del_archivo
```

Ingresar al directorio extraído y usar los siguientes comandos

```
./configure --enable-optimizations
sudo make altinstall
sudo apt install python3-pip
```



### Instalar SUDO

/etc/sudoers  archivo para cambiar opciones de sudo
/etc/apt/sources.list  archivo para agregar repositorios 

```
sudo apt-get install build-essential dkms 
sudo apt install linux-headers-$(uname -r)
sudo apt install wget software-properties-common
```

```
sudo apt install build-essential make automake cmake autoconf
sudo apt install  git wget curl
```

Eliminar repositorio 

sudo add-apt-repository --remove ppa:
ejemplo :   $sudo add-apt-repository --remove ppa:neovim-ppa/stable

Instalar fuentes 

copiar los archivos .otf -.ttf en el siguiente dir:
/usr/share/fonts/

sudo apt-get install manpages-es manpages-es-extra
sudo dpkg-reconfigure locales

Comandos

lspci

Driver graficos amd 

```
sudo apt install mesa-utils
dufo apt install firmware-amd-graphics
```

Codec y Driver audio

```bash
apt install alsa-firmware-loaders alsa-oss alsa-tools alsa-utils alsamixergui volumeicon-alsa paprefs pavumeter pulseaudio-utils sound-icons
```

```bash
apt install lame libdvdnav4 libfaac0 libmad0 libmp3lame0 libquicktime2 libstdc++5 libxvidcore4 twolame vorbis-tools x264
```

```bash
apt install gstreamer1.0-x  gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-alsa gstreamer1.0-pulseaudio gstreamer1.0-tools
```

Instarlar repdoructor de musica npd

```bash
sudo apt install mpd ncmpcpp
```

Editar el archivo 

```bash
sudo nano /etc/mpd.conf
```
---


---

## Guia bspwm  debian s/e


modificar repositorio /etc/apt/sources.list
deb-src http://deb.debian.org/debian bullseye main contrib non-free
bian.org/debian-security bullseye-security main contrib non-free
deb http://deb.debian.org/debian bullseye-updates main contrib non-free
deb http://deb.debian.org/debian bullseye-backports main contrib non-free
Eliminar repositorio 
sudo add-apt-repository --remove ppa:
ejemplo :   $sudo add-apt-repository --remove ppa:neovim-ppa/stable

#apt install sudo

Agregar usuario al grupo sudo

#usermode -aG oto

adduser tunombredeusuario sudo

modificar el archivo /etc/sudoers

sudo apt install xorg xterm

probamos el servidor gráfico con el siguiente comando

``` 
startx
```

```bash
sudo apt install bspwm suckless-tools
sudo apt install lightdm lightdm-gtk-greeter
sudo systemctl enable lightdm.service
sudo apt install lxappearance
```

```bash
sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev 
libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev 
libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev
```

```bash
$sudo apt -t bullseye-backports install polybar
$mkdir bspwm sxhkd polybar picom
```


copiar los siguientes archivos en los siguientes directorios

```bash
cp /usr/share/doc/bspwm/example/bspwmrc /home/@/.config/bspwm
```

bspwmrc tiene que tener permisos x

```bash
cp /usr/share/doc/bspwm/example/sxhkdrc /home/@/.config/sxhkd
```

En sxhdkrc cambiar la terminal por la que instalemos el atajo es super + return (enter), cambiar super + @space por super + d . elegir  (dmenu_run) o ( rofi -show drun)

```bash
sudo apt instal rofi            
rofi-theme-selector  alt+a guarda el tema
sudo apt install lxappearance   
```

```bash
sudo apt install feh
feh --bg-fill (archivo) para probar 
feh --bg-fill /home/usuario/Images/fondo.jpg
```

-  Instalamos lightdm gestor de inicio con el siguiente comando

```bash
sudo apt install lightdm lightdm-gtk-greeter
```

Para que arranque se utiliza el siguiente comando

```bash
$sudo systemctl enable lightdm.service
```

Elegir resolución con el siguiente comando

```bash
xrandr
```

Elegimos la resolución son el siguiente comando ejemplo:

```bash
xrandr -s 1920x1080
```
Para guardar la configuración de la resolución se copia el comando $xrandr -s 1920x1080 en el archivo :

```bash
~/.config/bspwm/bspwmrc
```

También agregar a bspwmrc la siguiente línea: 

```bash
$HOME/.config/polybar/launch.sh
bspc config focus_follows_pointer true
esto hace que el puntero marque la ventana
```

-  Configuración de polybar

Copiamos el archivo config que está en : que se encuentra en: /usr/share/doc/polybar/config en el directorio que creamos en ~.confi/polybar

```bash
cp /usr/share/doc/polybar/config ~/.config/polybar/
```

Probamos polybar con el siguiente comando

```bash
polybar example
```

Creamos un archivo en el directorio  ~/.config/polybar/ llamdo launch.sh (cambiar permisos +x) con el siguiente contenido:
esto se encuentra en : https://github.com/polybar/polybar/wiki

```bash
#!/usr/bin/env bash

# Terminate already running bar instances
killall -q polybar
# If all your bars have ipc enabled, you can also use 
# polybar-msg cmd quit
# Launch bar1 and bar2
echo "---" | tee -a /tmp/polybar1.log /tmp/polybar2.log
polybar bar1 2>&1 | tee -a /tmp/polybar1.log & disown
polybar bar2 2>&1 | tee -a /tmp/polybar2.log & disown

echo "Bars launched..."
```

Modificamos las siguientes líneas del archivo launch.sh

```bash
#!/usr/bin/env bash

killall -q polybar
echo "---" | tee -a /tmp/polybar1.log 
polybar bar1 2>&1 | tee -a /tmp/polybar1.log & disown

echo "Bars1 launched..."
```

En el archivo:  ~/.config/polybar/config modificamos la línea:
42 donde dice:\[bar/example\]
Por: \[bar/bar1\]     (bar1 hace referencia al archivo launch.sh)

Agremamos en el archivo: 

~/.config/bspwm/bspwmrc (mismo archivo donde guardamos la configuración de pantalla) la siguiente línea :
 $HOME/.config/polybar/launch.sh

```bash
git clone https://github.com/VaughnValle/blue-sky.git
```

Instalar picom para transparencias

```bash
sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev
```

```bash
git clone https://github.com/ibhagwan/picom.git
cd picom/
git submodule update --init --recursive
meson --buildtype=release . build
ninja -C build
sudo ninja -C build install
mkdir ~/.config/picom  si no existe 
cp ~/Descargas/blue-sky/picom.conf ~/.config/picom
```

Editar el archivo 
picom.conf 'backend = "glx"' por 'backend = "xrender"', comentando el de glx. dejar el glx puesto se puede llegar a experimentar lentitud muy molesta sin gpu).también comentar las líneas “blur”

Posteriormente, ejecutamos los siguientes comandos para aplicar los bordeados:

```bash
echo 'picom --experimental-backends &' >> ~/.config/bspwm/bspwmrc 
echo 'bspc config border_width 0' >> ~/.config/bspwm/bspwmrc
```

```bash
sudo apt install pulseaudio
apt install alsa-firmware-loaders alsa-oss alsa-tools alsa-utils alsamixergui volumeicon-alsa paman paprefs pavumeter pulseaudio-utils pulseaudio-esound-compat ffmpeg2theora sound-icons
apt install lame libdvdnav4 libdvdread4 libfaac0 libmad0 libmp3lame0 libquicktime2 libstdc++5 libxvidcore4 twolame vorbis-tools x264
apt install gstreamer1.0-x gstreamer1.0-fluendo-mp3 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-alsa gstreamer1.0-pulseaudio gstreamer1.0-tools
```

Fuentes

```bash
sudo apt install unifont
```

instalar font siji

```bash
$git clone https://github.com/stark/siji && cd siji
./install.sh -d ~ /.local/share/fonts
sudo rm /etc/fonts/conf.d/70-no-bitmaps.conf && fc-cache -fv
https://github.com/stark/siji
```




---

### Guia bspwm 07/22

Agregar usuario al grupo sudo

```bash
usermode -aG oto
```

```bash
git clone --recursive https://github.com/polybar/polybar
git clone https://github.com/baskerville/bspwm.git
git clone https://github.com/baskerville/sxhkd.git
git clone https://github.com/VaughnValle/blue-sky.git
git clone https://github.com/ibhagwan/picom.git
```

Instalar Python

```bash
 sudo apt install wget software-properties-common
```

Ir a la pag oficial de python y descargar la última versión gzipped source tarball
Descargar con wget , luego descomprimir con el siguiente comando

```bash
tar xvf nombre_del_archivo
#Ingresar al directorio extraído y usar los siguientes comandos
 ./configure --enable-optimizations
sudo make altinstall
sudo apt install python3-pip
```
$kill -9 -1 

```bash
sudo apt install python-xcbgen
```

```bash
sudo apt install mpd
```

```bash
sudo apt install neofetch cmatrix cmus tilix
```

```bash
mkdir ~/.config/ bspwm sxhkd picom polybar
```

```bash
sudo apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev
```

```bash
sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev
```

### Instalar bspwm 

```bash
cd /home/$/Descargas/bspwm/
make
sudo make install
cd ../sxhkd/
make
sudo make install
sudo apt install bspwm
```

```bash
sudo apt install lxappearance
```

```bash
cd /home/$/Descargas/bspwm/
cp examples/bspwmrc ~/.config/bspwm/
chmod +x ~/.config/bspwm/bspwmrc 
cp examples/sxhkdrc ~/.config/sxhkd/
```
 
### Instalar polybar compilando

```bash
cd /home/$/Descargas/
cd polybar/
mkdir build
cd build/
cmake ..
make -j$(nproc)
sudo make install
cd ~/Descargas/blue-sky/polybar/
cp * -r ~/.config/polybar
echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
cd fonts
sudo cp * /usr/share/fonts/truetype/
fc-cache -v
```

### Instalar polybar desde los repo

cambiar los repositorios 

```bash
deb http://deb.debian.org/debian bullseye-backports main contrib non-free
deb-src http://deb.debian.org/debian bullseye-backports main contrib non-free
```

Usar el siguiente comando

```bash
sudo apt -t bullseye-backports install polybar
```

Creamos un archivo en el directorio  ~/.config/polybar/ llamdo launch.sh (cambiar permisos +x) con lo siguiente: 

```bash
#!/usr/bin/env bash

killall -q polybar
echo "---" | tee -a /tmp/polybar1.log 
polybar bar1 2>&1 | tee -a /tmp/polybar1.log & disown

echo "Bars1 launched..."
```


### Instalar rofi

```bash
sudo apt instal rofi
```

en sxhdkrc cambiar la terminal por la que instalemos el atajo es super + return (enter), cambiar super + @space por super + d . elegir  dmenu_run o  rofi -show run

para ver iconos en rofi poner en el archivo sxhkd lo siguiente

```bash
rofi -show drun -show-icons
```

para seleccionar thema                        

```bash
rofi-theme-selector # alt+a guarda el  tema
```

```bash
sudo apt instal suckless-tools        
```

para instalar dmenu

### Instalar feh

```bash
sudo apt install feh
```

```bash
feh --bg-fill (archivo) para probar 
feh --bg-fill /home/usuario/Imagenes/fondo.jpg    
#agregar en bspwmrc 
#esto carga el fondo de pantalla
```

```bash
$HOME/.config/polybar/launch.sh
#agregar en bspwmrc 
#esot carga polybar 
```

```bash
bspc config focus_follows_pointer true            
#agregar en bspwmrc 
#esto hace que el puntero marque la ventana
```

```bash
$sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev
```

### Instalar picom

```bash
cd picom/
git submodule update --init --recursive
meson --buildtype=release . build
ninja -C build
sudo ninja -C build install
cp ~/Descargas/blue-sky/picom.conf ~/.config/picom
```

Editar el archivo picom.conf 'backend = "glx"' por 'backend = "xrender"', comentando el de glx. dejar el glx puesto se puede llegar a experimentar lentitud muy molesta sin gpu).también comentar las líneas “blur”

Posteriormente, ejecutamos los siguientes comandos para aplicar los bordeados:

```bash
echo 'picom --experimental-backends &' >> ~/.config/bspwm/bspwmrc 
echo 'bspc config border_width 0' >> ~/.config/bspwm/bspwmrc
```

estos últimos archivos se instalan si no funciona algo

```bash
sudo apt install pulseaudio
apt install alsa-firmware-loaders alsa-oss alsa-tools alsa-utils alsamixergui volumeicon-alsa paman paprefs pavumeter pulseaudio-utils pulseaudio-esound-compat ffmpeg2theora sound-icons
apt install lame libdvdnav4 libdvdread4 libfaac0 libmad0 libmp3lame0 libquicktime2 libstdc++5 libxvidcore4 twolame vorbis-tools x264
apt install gstreamer1.0-x gstreamer1.0-fluendo-mp3 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-alsa gstreamer1.0-pulseaudio gstreamer1.0-tools
```

Fuentes

```bash
sudo apt install unifont
instalar font siji
git clone https://github.com/stark/siji && cd siji
./install.sh -d ~ /.local/share/fonts
sudo rm /etc/fonts/conf.d/70-no-bitmaps.conf && fc-cache -fv
```

https://github.com/stark/siji

### Eliminar repositorio 

```bash
sudo add-apt-repository --remove ppa:
#ejemplo :   
sudo add-apt-repository --remove ppa:neovim-ppa/stable
```
### Drivers video


```bash
sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
```


ZSH

Después de instalar zsh, cambiar de shell con el siguiente comando:   

```bash
chsh -s $(which zsh)
https://github.com/zsh-users/zsh-syntax-highlighting
https://github.com/zsh-users/zsh-autosuggestions
https://github.com/romkatv/powerlevel10k
```

#### LSD

https://github.com/Peltoche/lsd

#### NERDFONT

https://www.nerdfonts.com/

#### NEOVIM

https://github.com/neovim/neovim

#### CAVA

https://github.com/karlstav/cava

comandos útiles

ffmpeg       corta y cambia de formato a videos

---

```bash
Atajos bspwm

program launcher
super + d
	rofi -show drun -show-icons

# make sxhkd reload its configuration files:
# hacer que sxhkd vuelva a cargar sus archivos de configuración:
super + Escape
	pkill -USR1 -x sxhkd

#
# bspwm hotkeys
#

# quit bspwm normally
# salir de bspwm normalmente
super + alt + Escape
	bspc quit

# close and kill
# cerrar y matar
super + {_,shift + }w
	bspc node -{c,k}

# alternate between the tiled and monocle layout
# alternar entre el diseño de mosaico y monóculo 
super + m
	bspc desktop -l next

# send the newest marked node to the newest preselected node
# enviar el nodo marcado más nuevo al nodo preseleccionado más nuevo
super + y
	bspc node newest.marked.local -n newest.!automatic.local
                     node newest.marked.local -n newest.!automatic.local

# swap the current node and the biggest node
# intercambiar el nodo actual y el nodo más grande
super + g
	bspc node -s biggest

#
# state/flags
#

# set the window state
# establecer el estado de la ventana
super + {t,shift + t,s,f}
	bspc node -t {tiled,pseudo_tiled,floating,fullscreen}

# set the node flags
# establecer las banderas de los nodos
super + ctrl + {m,x,y,z}
	bspc node -g {marked,locked,sticky,private}

#
# focus/swap
#

# focus the node in the given direction
# enfocar el nodo en la dirección dada
super + {_,shift + }{h,j,k,l}
	bspc node -{f,s} {west,south,north,east}

# focus the node for the given path jump
# enfocar el nodo para el salto de ruta dado
super + {p,b,comma,period}
	bspc node -f @{parent,brother,first,second}

# focus the next/previous node in the current desktop
# enfocar el nodo siguiente/anterior en el escritorio actual
super + {_,shift + }c
	bspc node -f {next,prev}.local

# focus the next/previous desktop in the current monitor
# enfocar el escritorio siguiente/anterior en el monitor actual
super + bracket{left,right}
	bspc desktop -f {prev,next}.local

# focus the last node/desktop
# enfocar el último nodo/escritorio
super + {grave,Tab}
	bspc {node,desktop} -f last

# focus the older or newer node in the focus history
# enfocar el nodo más antiguo o más nuevo en el historial de enfoque
super + {o,i}
	bspc wm -h off; \
	bspc node {older,newer} -f; \
	bspc wm -h on

# focus or send to the given desktop
# enfocar o enviar al escritorio dado
super + {_,shift + }{1-9,0}
	bspc {desktop -f,node -d} '^{1-9,10}'

#
# preselect
#

# preselect the direction
# preseleccionar la dirección
super + ctrl + {h,j,k,l}
	bspc node -p {west,south,north,east}

# preselect the ratio
# preseleccionar la relación
super + ctrl + {1-9}
	bspc node -o 0.{1-9}

# cancel the preselection for the focused node
# cancelar la preselección para el nodo enfocado
super + ctrl + space
	bspc node -p cancel

# cancel the preselection for the focused desktop
# cancelar la preselección para el escritorio enfocado
super + ctrl + shift + space
	bspc query -N -d | xargs -I id -n 1 bspc node id -p cancel

#
# move/resize
# movimiento de cambio de tamaño
#

# expand a window by moving one of its side outward
# expandir una ventana moviendo uno de sus lados hacia afuera
super + alt + {h,j,k,l}
	bspc node -z {left -20 0,bottom 0 20,top 0 -20,right 20 0}

# contract a window by moving one of its side inward
# contraer una ventana moviendo uno de sus lados hacia adentro
super + alt + shift + {h,j,k,l}
	bspc node -z {right -20 0,top 0 20,bottom 0 -20,left 20 0}

# move a floating window
# mover una ventana flotante
super + {Left,Down,Up,Right}
	bspc node -v {-20 0,0 20,0 -20,20 0}
```


---

### qemu


Comandos para usar QEMU

 - Modo live sin disco virtual

```bash
qemu-system-x86_64 -m 2G -smp 2 --enable-kvm -name "LOC-OS lsxd 64" -boot d -cdrom Descargas/loc-os-22-lsde_64.iso
```

 - Crear disco virtual

```bash
qemu-img create -f qcow2 hddloc-os.qcow2 14G
```

 - Comando para verificar la creación del disco

```bash
qemu-img info hddloc-os.qcow2
```

 - Crear maquina con disco

```bash
qemu-system-x86_64 -m 2G -smp 2 --enable-kvm -name "LOC-OS lsxd 64" -boot d -hda hddloc-os.qcow2 -cdrom Descargas/loc-os-22-lsde_64.iso
```

 - Después de instalar la máquina se utiliza el siguiente comando para arrancar la máquina

```bash
qemu-system-x86_64 -m 2G -smp 2 --enable-kvm -name "LOC-OS lsxd 64" -boot d -hda hddloc-os.qcow2
```


  -Para pasar archivos .vdmk a .qcow2 

```bash
qemu-img convert -p -f vmdk -O qcow2 centos6.9.vmdk centos6.9.qcow2
```

 - Para verificar el resultado

```bash
qemu-img info centos6.9.qcow2.
```



Instalar QEMU/KVM en DEBIAN 

-Verificar si la Virtualización está habilitada. Si devuelve el numero 0 quiere decir que no esta activada.

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
kvm-ok
```

-Instalar QEMU/KVM

```bash
sudo apt install qemu-kvm virt-manager virtinst libvirt-clients bridge-utils libvirt-daemon-system 
```

Iniciar y activar servicios

```bash
sudo systemctl enable --now libvirtd
sudo systemctl start libvirtd
```

-Verificar si está activo el servicio 

```bash
sudo systemctl status libvirtd
sudo usermod -aG kvm $USER 
sudo usermod -aG libvirt $USER
sudo virt-manager
sudo virsh net-list --all
sudo virsh net-start default
sudo virsh net-start default
sudo virsh net-list --all
sudo virsh net-autostart default
sudo virsh net-list --all
```



Pasos a seguir del tutorial: https://www.youtube.com/watch?v=N9AtdJjcE4A
 1.- Qué procesador tenemos en nuestro pc. 'vmx' intel - 'svm' amd:
```
grep -E --color 'vmx|svm' /proc/cpuinfo
```
 2.- Comprobar si tenemos la virtualización activada:
```
egrep -c 'vmx|svm' /proc/cpuinfo
```
 3.- Instalación de paquetes:
```
sudo apt install qemu-kvm libvirt-clients libvirt-daemon libvirt-daemon-system bridge-utils
virtinst virt-manager
```
 4.- Ver si tenemos el servicio de 'libvirt' activo con 'status' sino lo activamos:
```
sudo systemctl status libvirtd.service
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
```
 5.- Enumeramos redes disponibles para las máquinas virtuales y la activamos:
```
sudo virsh net-list --all
sudo virsh net-start default
sudo virsh net-autostart default
```
 6.- Añadimos nuestro usuario a los grupos 'libvirt' y 'libvirt-qemu':
```
sudo adduser [nuestro usuario] libvirt
sudo adduser [nuestro usuario] libvirt-qemu
```
 7.- Reiniciamos
```
sudo reboot
```


---

### notas gnu

### Montar unidades cd/dvd/ 

Tipo auto

```bash
sudo mount -t auto /dev/sr0 /media/cdrom
```

Solo lectura

```bash
sudo mount -t iso9660 /dev/sr0 /media/cdrom
```

Regrabable

```bash
sudo mount -t udf,iso9660 /dev/sr0 /media/cdrom
```

Desmontar con 

```bash
sudo umount /media/cdrom
```

## Cambio de contraseña root desde grub

1º) Pulsar ESC
2º) Seleccionar Recovery Mode y pulsar E
3º) Sustituir en linux /boot/vmlinuz... el final por: rw init=/bin/bash
(luego pulsar Ctrl+x o F10)
4º) passwd nombreusuario



Comando which - type - find
Comando which: muestra la ubicación donde está instalado el programa o comando
Comando type: muestra el tipo de comando que es. Si es binario o propio de la shell
Comando find: busca la ubicación de un directorio.
Ejemplo de which y type:

oto@pc:~$ which firefox
/usr/bin/firefox
oto@pc:~$ which cmatrix
/usr/bin/cmatrix
oto@pc:~$ which cd
oto@pc:~$ type cd
cd es una orden interna del shell
oto@pc:~$ type cp
cp is /usr/bin/cp
oto@pc:~$ which cp
/usr/bin/cp

Ejemplo del comando find
oto@pc:~$find ruta parámetro criterio
oto@pc:~$find -name nombre_del_archivo
oto@pc:~$find -type fd -name nombre_del_archivo
oto@pc:~$find -zise 10M
oto@pc:~$find -zise 1G
oto@pc:~/Escritorio/directorios$ find -type d -name 02_febrero
./año/2021/02_febrero
./año/2022/02_febrero
oto@pc:~/Escritorio/directorios$ find -type f -name mariano*
./hola/mariano.txt
oto@pc:~/Escritorio/directorios$
Comando grep
permite buscar coincidencias dentro de un archivo

Utilidades de red

ifconfig -muestra la configuración de las interfaces de red
netstat -muestra las conexiones de red
route -muestra la tabla de rutas ip
pin -realiza pin a un host
ifdown -desconecta el adaptador de red
ifup -conecta la interfaz de red
traceroute -muestra la ruta

Driver tarjetas red
Atheros

```bash
apt install firmware-atheros
```

Broadcom

```bash
apt install firmware-b43-installer
apt install broadcom-sta-dkms
apt install firmware-b43legacy-installer
apt install firmware-brcm80211
```

Intel

```bash
apt install Firmware-ipw2x00
apt install firmware-intelwimax
apt install firmware-iwlwifi
```

Realtek

```bash
apt install firmware-realtek
apt install firmware-ti-connectivity
```

ZyDas

```bash
apt install firmware-zd1211
```

Si después de hacer todo esto, no funciona, solo queda instalar el conjunto total de drivers privativos:

```
apt install firmware-linux firmware-linux-free firmware-linux-nonfree firmware-misc-nonfree
```

Información del sistema


arch: mostrar la arquitectura de la máquina (1).
uname -m: mostrar la arquitectura de la máquina (2).
uname -r: mostrar la versión del kernel usado.
dmidecode -q: mostrar los componentes (hardware) del sistema.
hdparm -i /dev/hda: mostrar las características de un disco duro.
hdparm -tT /dev/sda: realizar prueba de lectura en un disco duro.
cat /proc/cpuinfo: mostrar información de la CPU.
cat /proc/interrupts: mostrar las interrupciones.
cat /proc/meminfo: verificar el uso de memoria.
cat /proc/swaps: mostrar ficheros swap.
cat /proc/version: mostrar la versión del kernel.
cat /proc/net/dev: mostrar adaptadores de red y estadísticas.
cat /proc/mounts: mostrar el sistema de ficheros montado.
lspci -tv: mostrar los dispositivos PCI.
lsusb -tv: mostrar los dispositivos USB.
date: mostrar la fecha del sistema.
cal 2011: mostrar el almanaque de 2011.
cal 07 2011: mostrar el almanaque para el mes julio de 2011.
date 041217002011.00: colocar (declarar, ajustar) fecha y hora.
clock -w: guardar los cambios de fecha en la BIOS.

Driver bluetooth 
sudo apt install bluetooth bluez bluez-cups bluez-tools btscanner gnome-bluetooth python-bluez pulseaudio-module-bluetooth

Apagar (Reiniciar Sistema o Cerrar Sesión)
shutdown -h now: apagar el sistema (1).
init 0: apagar el sistema (2).
telinit 0: apagar el sistema (3).
halt: apagar el sistema (4).
shutdown -h hours:minutes &: apagado planificado del sistema.
shutdown -c: cancelar un apagado planificado del sistema.
shutdown -r now: reiniciar (1).
reboot: reiniciar (2).
logout: cerrar sesión.

Encontrar archivos



```bash
find / -name file1: buscar fichero y directorio a partir de la raíz del sistema.
```


```bash
find / -user user1: buscar ficheros y directorios pertenecientes al usuario ‘user1’.
```


```bash
find /home/user1 -name \*.bin: buscar ficheros con extensión ‘. bin’ dentro del directorio ‘/ home/user1’.
```



find /usr/bin -type f -atime +100: buscar ficheros binarios no usados en los últimos 100 días.



```bash
find /usr/bin -type f -mtime -10: buscar ficheros creados o cambiados dentro de los últimos 10 días.
```



```bash
find / -name \*.rpm -exec chmod 755 ‘{}’ \;: buscar ficheros con extensión ‘.rpm’ y modificar permisos.
```



```bash
find / -xdev -name \*.rpm: Buscar ficheros con extensión ‘.rpm’ ignorando los dispositivos removibles como cdrom, pen-drive, etc.…
```


```bash
locate \*.ps: encuentra ficheros con extensión ‘.ps’ ejecutados primeramente con el command ‘updatedb’.
```


```bash
whereis halt: mostrar la ubicación de un fichero binario, de ayuda o fuente. En este caso pregunta dónde está el comando ‘halt’.
```



```bash
which halt: mostrar la senda completa (el camino completo) a un binario / ejecutable.
```

## Montando un sistema de ficheros



```bash
mount /dev/hda2 /mnt/hda2: 
#montar un disco llamado hda2 
#Verifique primero la existencia del directorio ‘/ mnt/hda2’; si no está, debe crearlo.
```



```bash
umount /dev/hda2
#desmontar un disco llamado hda2. Salir primero desde el punto ‘/ mnt/hda2.
```



```bash
fuser -km /mnt/hda2
#forzar el desmontaje cuando el dispositivo está ocupado.
```



```bash
umount -n /mnt/hda2
#correr el desmontaje sin leer el fichero /etc/mtab. Útil cuando el fichero es de solo lectura o el disco duro está lleno.
```



```bash
mount /dev/fd0 /mnt/floppy
#montar un disco flexible (floppy).
```



```bash
mount /dev/cdrom /mnt/cdrom
#montar un cdrom / dvdrom.
```



```bash
mount /dev/hdc /mnt/cdrecorder
#montar un cd regrabable o un dvdrom.
```



```bash
mount /dev/hdb /mnt/cdrecorder
#montar un cd regrabable / dvdrom (un dvd).
```



```bash
mount -o loop file.iso /mnt/cdrom
#montar un fichero o una imagen iso.
```



```bash
mount -t vfat /dev/hda5 /mnt/hda5
#montar un sistema de ficheros FAT32.
```



```bash
mount /dev/sda1 /mnt/usbdisk
#montar un usb pen-drive o una memoria (sin especificar el tipo de sistema de ficheros).
```


Espacio de Disco

```bash
df -h: mostrar una lista de las particiones montadas.
```



```bash
ls -lSr |more: mostrar el tamaño de los ficheros y directorios ordenados por tamaño.
```



```bash
du -sh dir1: Estimar el espacio usado por el directorio ‘dir1’.
```



```
$du -sk * | sort -rn: mostrar el tamaño de los ficheros y directorios ordenados por tamaño.
```



```bash
rpm -q -a –qf ‘%10{SIZE}t%{NAME}n’ | sort -k1,1n: mostrar el espacio usado por los paquetes rpm instalados organizados por tamaño (Fedora, Redhat y otros).
```



```bash
dpkg-query -W -f=’${Installed-Size;10}t${Package}n’ | sort -k1,1n: mostrar el espacio usado por los paquetes instalados, organizados por tamaño (Ubuntu, Debian y otros).
```

Usuarios y Grupos

```bash
groupadd nombre_del_grupo: crear un nuevo grupo.
```



```bash
groupdel nombre_del_grupo: borrar un grupo.
```


```bash
groupmod -n nuevo_nombre_del_grupo viejo_nombre_del_grupo: renombrar un grupo.
```


```bash
useradd -c “Name Surname ” -g admin -d /home/user1 -s /bin/bash user1: Crear un nuevo usuario perteneciente al grupo “admin”.
```


```bash
$useradd user1: crear un nuevo usuario.
```



```bash
userdel -r user1: borrar un usuario (‘-r’ elimina el directorio Home).
```

```bash
usermod -c “User FTP” -g system -d /ftp/user1 -s /bin/nologin user1: cambiar los atributos del usuario.
```



```bash
passwd: cambiar contraseña.
```

```bash
passwd user1: cambiar la contraseña de un usuario (solamente por root).
```



```bash
chage -E 2011-12-31 user1: colocar un plazo para la contraseña del usuario. En este caso dice que la clave expira el 31 de diciembre de 2011.
```



```bash
pwck: chequear la sintaxis correcta el formato de fichero de ‘/etc/passwd’ y la existencia de usuarios.
```

```bash
grpck: chequear la sintaxis correcta y el formato del fichero ‘/etc/group’ y la existencia de grupos.
```

```bash
newgrp group_name: registra a un nuevo grupo para cambiar el grupo predeterminado de los ficheros creados recientemente.
```


Permisos en Ficheros (Usa ”+” para colocar permisos y ”-” para eliminar)


```bash
ls -lh: Mostrar permisos.
```

```bash
ls /tmp | pr -T5 -W$COLUMNS: dividir la terminal en 5 columnas.
```


```bash
chmod ugo+rwx directory1: colocar permisos de lectura ®, escritura (w) y ejecución(x) al propietario (u), al grupo (g) y a otros (o) sobre el 
directorio ‘directory1’.
```


```bash
chmod go-rwx directory1: quitar permiso de lectura ®, escritura (w) y (x) ejecución al grupo (g) y otros (o) sobre el directorio ‘directory1’.
```



```bash
chown user1 file1: cambiar el dueño de un fichero.
```



```bash
chown -R user1 directory1: cambiar el propietario de un directorio y de todos los ficheros y directorios contenidos dentro.
```



```bash
chgrp group1 file1: cambiar grupo de ficheros.
```



```bash
chown user1:group1 file1: cambiar usuario y el grupo propietario de un fichero.
```



```bash
find / -perm -u+s: visualizar todos los ficheros del sistema con SUID configurado.
```



```bash
chmod u+s /bin/file1: colocar el bit SUID en un fichero binario. El usuario que corriendo ese fichero adquiere los mismos privilegios como dueño.
```



```bash
chmod u-s /bin/file1: deshabilitar el bit SUID en un fichero binario.
```



```bash
chmod g+s /home/public: colocar un bit SGID en un directorio –similar al SUID pero por directorio.
```



```bash
chmod g-s /home/public: desabilitar un bit SGID en un directorio.
```



```bash
chmod o+t /home/public: colocar un bit STIKY en un directorio. Permite el borrado de ficheros solamente a los dueños legítimos.
```



```bash
chmod o-t /home/public: desabilitar un bit STIKY en un directorio.
```

Atributos especiales en ficheros (Usa ”+” para colocar permisos y ”-” para eliminar)

chattr +a file1: permite escribir abriendo un fichero solamente modo append.
chattr +c file1: permite que un fichero sea comprimido / descomprimido automaticamente.
chattr +d file1: asegura que el programa ignore borrar los ficheros durante la copia de seguridad.
chattr +i file1: convierte el fichero en invariable, por lo que no puede ser eliminado, alterado, renombrado, ni enlazado.
chattr +s file1: permite que un fichero sea borrado de forma segura.
chattr +S file1: asegura que un fichero sea modificado, los cambios son escritos en modo synchronous como con sync.
chattr +u file1: te permite recuperar el contenido de un fichero aún si este está cancelado.

lsattr: mostrar atributos especiales.




Ver el contenido de un fichero


cat file1: ver los contenidos de un fichero comenzando desde la primera hilera.
tac file1: ver los contenidos de un fichero comenzando desde la última línea.
more file1: ver el contenido a lo largo de un fichero.
less file1: parecido al commando ‘more’ pero permite salvar el movimiento en el fichero así como el movimiento hacia atrás.
head -2 file1: ver las dos primeras líneas de un fichero.
tail -2 file1: ver las dos últimas líneas de un fichero.
tail -f /var/log/messages: ver en tiempo real qué ha sido añadido al fichero.

Manipulación de texto

cat file1 file2 .. | command <> file1_in.txt_or_file1_out.txt: sintaxis general para la manipulación de texto utilizando PIPE, STDIN y STDOUT.
cat file1 | command( sed, grep, awk, grep, etc…) > result.txt: sintaxis general para manipular un texto de un fichero y escribir el resultado en un fichero nuevo.
cat file1 | command( sed, grep, awk, grep, etc…) » result.txt: sintaxis general para manipular un texto de un fichero y añadir resultado en un fichero existente.
grep Aug /var/log/messages: buscar palabras “Aug” en el fichero ‘/var/log/messages’.
grep ^Aug /var/log/messages: buscar palabras que comienzan con “Aug” en fichero ‘/var/log/messages’
grep [0-9] /var/log/messages: seleccionar todas las líneas del fichero ‘/var/log/messages’ que contienen números.
grep Aug -R /var/log/*: buscar la cadena “Aug” en el directorio ‘/var/log’ y debajo.
sed ‘s/stringa1/stringa2/g’ example.txt: reubicar “string1” con “string2” en ejemplo.txt
sed ‘/^$/d’ example.txt: eliminar todas las líneas en blanco desde el ejemplo.txt
sed ‘/ *#/d; /^$/d’ example.txt: eliminar comentarios y líneas en blanco de ejemplo.txt
echo ‘esempio’ | tr ‘[:lower:]’ ‘[:upper:]’: convertir minúsculas en mayúsculas.
sed -e ‘1d’ result.txt: elimina la primera línea del fichero ejemplo.txt
sed -n ‘/stringa1/p’: visualizar solamente las líneas que contienen la palabra “string1”.
Establecer caracter y conversión de ficheros
dos2unix filedos.txt fileunix.txt: convertir un formato de fichero texto desde MSDOS a UNIX.
unix2dos fileunix.txt filedos.txt: convertir un formato de fichero de texto desde UNIX a MSDOS.
recode ..HTML < page.txt > page.html: convertir un fichero de texto en html.
recode -l | more: mostrar todas las conversiones de formato disponibles.

Análisis del sistema de ficheros

badblocks -v /dev/hda1: Chequear los bloques defectuosos en el disco hda1.
fsck /dev/hda1: reparar / chequear la integridad del fichero del sistema Linux en el disco hda1.
fsck.ext2 /dev/hda1: reparar / chequear la integridad del fichero del sistema ext 2 en el disco hda1.
e2fsck /dev/hda1: reparar / chequear la integridad del fichero del sistema ext 2 en el disco hda1.
e2fsck -j /dev/hda1: reparar / chequear la integridad del fichero del sistema ext 3 en el disco hda1.
fsck.ext3 /dev/hda1: reparar / chequear la integridad del fichero del sistema ext 3 en el disco hda1.
fsck.vfat /dev/hda1: reparar / chequear la integridad del fichero sistema fat en el disco hda1.
fsck.msdos /dev/hda1: reparar / chequear la integridad de un fichero del sistema dos en el disco hda1.
dosfsck /dev/hda1: reparar / chequear la integridad de un fichero del sistema dos en el disco hda1.

Formatear un sistema de ficheros

mkfs /dev/hda1: crear un fichero de sistema tipo Linux en la partición hda1.
mke2fs /dev/hda1: crear un fichero de sistema tipo Linux ext 2 en hda1.
mke2fs -j /dev/hda1: crear un fichero de sistema tipo Linux ext3 (periódico) en la partición hda1.
mkfs -t vfat 32 -F /dev/hda1: crear un fichero de sistema FAT32 en hda1.
fdformat -n /dev/fd0: formatear un disco flooply.
mkswap /dev/hda3: crear un fichero de sistema swap.

Trabajo con la SWAP

mkswap /dev/hda3: crear fichero de sistema swap.
swapon /dev/hda3: activando una nueva partición swap.
swapon /dev/hda2 /dev/hdb3: activar dos particiones swap.
Salvas (Backup)
dump -0aj -f /tmp/home0.bak /home: hacer una salva completa del directorio ‘/home’.
dump -1aj -f /tmp/home0.bak /home: hacer una salva incremental del directorio ‘/home’.
restore -if /tmp/home0.bak: restaurando una salva interactivamente.
rsync -rogpav –delete /home /tmp: sincronización entre directorios.
rsync -rogpav -e ssh –delete /home ip_address:/tmp: rsync a través del túnel SSH.
rsync -az -e ssh –delete ip_addr:/home/public /home/local: sincronizar un directorio local con un directorio remoto a través de ssh y de compresión.
rsync -az -e ssh –delete /home/local ip_addr:/home/public: sincronizar un directorio remoto con un directorio local a través de ssh y de compresión.
dd bs=1M if=/dev/hda | gzip | ssh user@ip_addr ‘dd of=hda.gz’: hacer una salva de un disco duro en un host remoto a través de ssh.
dd if=/dev/sda of=/tmp/file1: salvar el contenido de un disco duro a un fichero. (En este caso el disco duro es “sda” y el fichero “file1”).
tar -Puf backup.tar /home/user: hacer una salva incremental del directorio ‘/home/user’.
( cd /tmp/local/ && tar c . ) | ssh -C user@ip_addr ‘cd /home/share/ && tar x -p’: copiar el contenido de un directorio en un directorio remoto a través de ssh.
( tar c /home ) | ssh -C user@ip_addr ‘cd /home/backup-home && tar x -p’: copiar un directorio local en un directorio remoto a través de ssh.
tar cf – . | (cd /tmp/backup ; tar xf – ): copia local conservando las licencias y enlaces desde un directorio a otro.
find /home/user1 -name ‘*.txt’ | xargs cp -av –target-directory=/home/backup/ –parents: encontrar y copiar todos los ficheros con extensión ‘.txt’ de un directorio a otro.
find /var/log -name ‘*.log’ | tar cv –files-from=- | bzip2 > log.tar.bz2: encontrar todos los ficheros con extensión ‘.log’ y hacer un archivo bzip.
dd if=/dev/hda of=/dev/fd0 bs=512 count=1: hacer una copia del MRB (Master Boot Record) a un disco floppy.
dd if=/dev/fd0 of=/dev/hda bs=512 count=1: restaurar la copia del MBR (Master Boot Record) salvada en un floppy.

CD-ROM

cdrecord -v gracetime=2 dev=/dev/cdrom -eject blank=fast -force: limpiar o borrar un cd regrabable.
mkisofs /dev/cdrom > cd.iso: crear una imagen iso de cdrom en disco.
mkisofs /dev/cdrom | gzip > cd_iso.gz: crear una imagen comprimida iso de cdrom en disco.
mkisofs -J -allow-leading-dots -R -V “Label CD” -iso-level 4 -o ./cd.iso data_cd: crear una imagen iso de un directorio.
cdrecord -v dev=/dev/cdrom cd.iso: quemar una imagen iso.
gzip -dc cd_iso.gz | cdrecord dev=/dev/cdrom –: quemar una imagen iso comprimida.
mount -o loop cd.iso /mnt/iso: montar una imagen iso.
cd-paranoia -B: llevar canciones de un cd a ficheros wav.
cd-paranoia – ”-3”: llevar las 3 primeras canciones de un cd a ficheros wav.
cdrecord –scanbus: escanear bus para identificar el canal scsi.
dd if=/dev/hdc | md5sum: hacer funcionar un md5sum en un dispositivo, como un CD.



Monitoreando y depurando

top: mostrar las tareas de linux usando la mayoría cpu.
ps -eafw: muestra las tareas Linux.
ps -e -o pid,args –forest: muestra las tareas Linux en un modo jerárquico.
pstree: mostrar un árbol sistema de procesos.
kill -9 ID_Processo: forzar el cierre de un proceso y terminarlo.
kill -1 ID_Processo: forzar un proceso para recargar la configuración.
lsof -p $$: mostrar una lista de ficheros abiertos por procesos.
lsof /home/user1: muestra una lista de ficheros abiertos en un camino dado del sistema.
strace -c ls >/dev/null: mostrar las llamadas del sistema hechas y recibidas por un proceso.
strace -f -e open ls >/dev/null: mostrar las llamadas a la biblioteca.
watch -n1 ‘cat /proc/interrupts’: mostrar interrupciones en tiempo real.
last reboot: mostrar historial de reinicio.
lsmod: mostrar el kernel cargado.
free -m: muestra el estado de la RAM en megabytes.
smartctl -A /dev/hda: monitorear la fiabilidad de un disco duro a través de SMART.
smartctl -i /dev/hda: chequear si SMART está activado en un disco duro.
tail /var/log/dmesg: mostrar eventos inherentes al proceso de carga del kernel.
tail /var/log/messages: mostrar los eventos del sistema.

Otros comandos útiles

apropos …keyword: mostrar una lista de comandos que pertenecen a las palabras claves de un programa; son útiles cuando tú sabes qué hace tu programa, pero de sconoces el nombre del comando.
man ping: mostrar las páginas del manual on-line; por ejemplo, en un comando ping, usar la opción ‘-k’ para encontrar cualquier comando relacionado.
whatis …keyword: muestra la descripción de lo que hace el programa.
mkbootdisk –device /dev/fd0 `uname -r`: crear un floppy boteable.
gpg -c file1: codificar un fichero con guardia de seguridad GNU.
gpg file1.gpg: decodificar un fichero con Guardia de seguridad GNU.
wget -r www.example.com: descargar un sitio web completo.
wget -c www.example.com/file.iso: descargar un fichero con la posibilidad de parar la descargar y reanudar más tarde.
echo ‘wget -c www.example.com/files.iso‘ | at 09:00: Comenzar una descarga a cualquier hora. En este caso empezaría a las 9 horas.
ldd /usr/bin/ssh: mostrar las bibliotecas compartidas requeridas por el programa ssh.
alias hh=’history’: colocar un alias para un comando –hh= Historial.
chsh: cambiar el comando Shell.
chsh –list-shells: es un comando adecuado para saber si tienes que hacer remoto en otra terminal.
who -a: mostrar quien está registrado, e imprimir hora del último sistema de importación, procesos muertos, procesos de registro de sistema, procesos activos producidos por init, funcionamiento actual y últimos cambios del reloj del sistema.



apt-cache show  nombre_programa
Muestra información del programa 

Soluciones a errores 

Libreoffice
Error :
no se pudo realizar la conexión con el origen de datos externos. No se encontró un controlador de SDBC para el URL “sdbc:embedded:hsqldb”.
Solución: 
sudo apt-get install libreoffice-sdbc-postgresql libreoffice-sdbc-hsqldb

-solucion al error :
error mountaing /dev/sd1 at /media/ unknown filesystem type exfat
$sudo apt install exfat-fuse exfat-utils

----




#### VSCODE  
 https://code.visualstudio.com/
configuracion y extensiones vs code
-cofig
cursor blinking - animacion para el cursor cambiar por expand    
bracket pair colorization - habilitar
bracket pairs   - poner en true 
linked editing  - habilitar es para editar apertura y cierre de etiquetas

-extensiones
live server -  ritwick dey
eslint   - microsoft
prettier
material icon theme
https://emmet.io/

themes   https://marketplace.visualstudio.com/search?term=theme&target=VSCode&category=All%20categories&sortBy=Relevance
one dark pro
Andromeda Mariana
Saklash-Theme
Blueberry Dark Theme


extensiones para python
python
pylint   marca errores
format document         abrir paleta con ctrl+shif+p   (minuto_ 32)
en configuracion (settings) buscar "formatOnSave"  marcar . esto cada ves que se guarda el documento corrige el formato

APP
neofetch vlc plank git curl wget

telegram zoom jdownloader
notas de app
configurar plank (ctrl+click derecho del raton)
https://jdownloader.org/es/home/index
antes de instalar jdownloader instalar:
$sudo apt install -y default-jre



QEMU:
solucion a error de qemu
1
$ sudo virsh net-start default
2
$ sudo ifconfig virbr0 down
$ sudo brctl delbr virbr0
$ sudo virsh net-start default


ICONS OS
Gruvbox Plus Icon Pack
https://www.xfce-look.org/p/1961046
https://github.com/SylEleuth/gruvbox-plus-icon-pack

utilidades app
Aplicacion para limpiar archivos huerfanos de faltpack
Flatsweep

ERRORES:
error al montar el sistema de archivo
not autorized to perform operation (udisks-error-quark,4)
sudo apt install gnome-disk-utility
sudo apt install policykit-1-gnome
/usr/lib/policykit-1-gnome/polkit-gnome-authentication-agent-1




