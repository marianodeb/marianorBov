





## ARCH


Actualiza el sistema

```bash
sudo pacman -Syu 
```

Sincroniza los paquetes de la base de datos


```bash
sudo pacman -Sy 
```

Fuerza la sincronización de los paquetes de la base de datos

```bash
sudo pacman -Syy
```

Permite buscar un paquete en los repositorios

```bash
sudo pacman -Ss paquete 
```

Obtiene información del paquete que está en los repositorios

```bash
sudo pacman -Si paquete 
```

Muestra la información de un paquete instalado

```bash
sudo pacman -Qi paquete 
```

Instalar y/o actualizar un paquete

```bash
sudo pacman -S paquete 
```

Eliminar un paquete

```bash
sudo pacman -R paquete 
```

Instalar un paquete local

```bash
sudo pacman -U /ruta/hacia/el/paquete 
```

Limpiar la caché de los paquetes

```bash
sudo pacman -Scc 
```

Eliminar un paquete y sus dependencias

```bash
sudo pacman -Rc paquete 
```

Eliminar un paquete, sus dependencias y configuraciones

```bash
sudo pacman -Rnsc paquete 
```

Muestra paquetes huérfanos

```bash
sudo pacman -Qdt 
```

Eliminar paquetes huerfanos

```bash
sudo pacman -Rs $(pacman -Qdtq) 
```

para instalar un paquete o aplicación

```bash
yay -S <package-name>
```

En caso de querer buscar una aplicación dentro de los repositorios oficiales y en AUR a la vez, añadimos la bandera “s”

```bash
yay -Ss <package-name>
```

Por ejemplo, otro caso, si solo requieren conocer la información de cierto paquete:

```bash
yay -Si <package-name>
```

Si queremos instalar un paquete local, basta con teclear:

```bash
yay -U ruta-del-paquete
```

También es posible solo colocar el nombre del paquete y este realizará una búsqueda de todos aquellos relacionados con el criterio y este nos mostrará 

en una lista los encontrados y nos pedirá seleccionar el de nuestro interés.

```bash
yay <package-name>
```

En caso de querer saber que actualizaciones tenemos disponibles, basta con teclear:

```bash
yay -Pu
```

En caso de solo requerir sincronizar los paquetes de la base de datos:

```bash
yay -Sy
```

Si quieren realizar una actualización del sistema debemos de teclear:

```bash
yay -Syu
```

Actualizar el sistema, incluyendo los paquetes instalados de AUR, solamente tecleamos:

```bash
yay -Syua
```

Para instalar cualquier paquete sin confirmaciones (sin intervención del usuario, por supuesto), utilice la opción de “-noconfirm”.

```bash
yay -S --noconfirm <package-name>
```

Para eliminar las dependencias no deseadas, basta con que teclemos lo siguiente:

```bash
yay -Yc
```

Si queremos realizar una limpieza del cache de las aplicaciones solamente tecleamos:

```bash
yay -Scc
```

En caso de querer eliminar “solo” un paquete o aplicación:

```bash
yay -R <package-name>
```

Para eliminar un paquete o aplicación junto con sus dependencias:

```bash
yay -Rs <package-name>
```

Para eliminar un paquete, sus dependencias y configuraciones, debemos de teclear:

```bash
yay -Rnsc <package-name>
```

Instalar visual studio code
Instalar herramientas para compilar
$sudo pacman -S base-devel      
Instalar git para clonar el repositorio de la página de aur
$sudo pacman -S git --noconfirm 
Clonar el repositorio
$git clone https://aur.archlinux.org/visual-studio-code-bin.git 
https://aur.archlinux.org/packages/visual-studio-code-bin
ingresar a la repo clonado y ejecutar:
$makepkg -si

Instalar libreoffice e idioma español

```bash
sudo pacman -Ss libreoffice-still-es
sudo pacman -S libreoffice-still-es
```

Instalar inkscape

```bash
sudo pacman -S inkscape
```

```bash
yay hsqldb2-java
```



#### Instalar java 

```bash
sudo pacman -S jre
```

---

## guia_inst_Arch

- Para ver si tenes bios o efi

```bash
ls  /sys/firmware/efi/efivars
```
 - Con el comando ping verificamos si tenes internet
 - Configuramos el teclado a español con :

```bash
loadkeys es
loadkeys la-latin1
```

 - Verificar tipo de conexión :

```bash
ip link
```

-si es por wifi activar 

```bash
ip link set wlan0 up
```

 - Para escanear la señal, utilizar more para pasar el texto

```bash
iwlist wlan0 scan | more
```

 - Para guardar la señal y la contraseña (los números es la contraseña) se utiliza:

```bash
wpa_passphrase telecentro 119082345 > /etc/configuracionWIFI
```

 - Para comprobar si el archivo se creó

```bash
cat /etc/configuracionwifi
```

 - Para conectarse al wifi

```bash
wpa_supplicant -B -i wlan0 -D wext -c /etc/configuracionWIFI
```

 - Para ver si estamos conectados

```bash
dhclient
```

 - Establece fecha y hora desde la red

```bash
timedatectl set-ntp true
```

 - Para ver si tenemos efi o bios. si no encuentra el archivo es bios

```bash
ls /sys/firmware/efi/efiwars
```

 - Instalación con bios 
 - Ver discos y particiones  

```bash
fdisk -l
```

 - Particionar usando el disco que tenemos es vda porque el ej se realizó con virtualización
-          BIOS

```bash
cfdisk /dev/vda
```

 - De la lista que aparece elegir “dos”
 - Si es uefi elegir “gpt”

new 512M {primaria} {Bootable} {write} yes enter
new 8G   {primaria} {write} yes enter
new 3G   {primaria}  {write} yes enter
new 1G   {primaria} {type} seleccionar “swap” {write} yes enter
{quit}

 - Dar formato a las particiones el número va depender como creamos las particiones sda1 2 3 4 ...

```bash
mkfs.ext2 /dev/vda1           =boot
mkfs.ext4 /dev/vda2           =/
mkfs.ext4 /dev/vda3           =home
mkswap /dev/vda4              =swap
```

 - Montamos las particiones 
 - Montamos swap

```bash
swapon /dev/vda4
```

 - Montamos raiz

```bash
mount /dev/vda2 /mnt
```

 - Creamos la carpeta boot para montar la partición boot /dev/vda1

```bash
mkdir /mnt/boot
```

 - montamos sda1 =boot

```bash
mount /dev/vda1 /mnt/boot
```

 - Creamos la carpeta home para luego montarla

```bash
mkdir /mnt/home
```

 - Montamos home

```bash
mount /dev/vda3 /mnt/home
```

-          UEFI

```bash
cfdisk /dev/vda
```

 - Si es uefi elegir “gpt”

new 512M {type} seleccinar “efi system”  {write} yes enter
new 8G   {primaria} {write} yes enter
new 3G   {primaria}  {write} yes enter
new 1G   {primaria} {type} seleccionar swap {write} yes enter
{quit}
 - Dar formato a las particiones el número va depender como creamos las particiones sda1 2 3 4 ...

```bash
mkfs.vfat -F32 /dev/vda1           =boot EFI
mkfs.ext4 /dev/vda2           =/
mkfs.ext4 /dev/vda3           =home
mkswap /dev/vda4              =swap
```

 - Montamos las particiones 
 - Montamos swap

```bash
swapon 
```

 - Montamos raiz

```bash
mount /dev/vda2 /mnt
```

 - Creamos la carpeta boot para montar la partición boot /dev/vda1

```bash
mkdir /mnt/boot
mkdir /mnt/boot/efi
```

 -Montamos efi

```bash
mount /dev/vda1 /mnt/boot/efi
```

 - Creamos la carpeta home para luego montarla

```bash
mkdir /mnt/home
```

 - Montamos home

```bash
mount /dev/vda3 /mnt/home
```

 - Instalación de paquetes
-Si estamos con uefi agregar el paquete (efibootmgr)

```bash
pacstrap /mnt linux linux-firmware base base-devel nano grub networkmanager dhcpcd 
```

 - Para conectarse mediante wifi

```bash
pacstrap /mnt netctl wpa_supplicant dialog
```

 - Generar fstab

```bash
genfstab -pU /mnt >> /mnt/etc/fstab
```

 - Comprobar el archivo fstab

```bash
cat /mnt/etc/fstab
```

 - Entramos al sistema base instalado 

```bash
arch-chroot /mnt
```

 - Creamos el hostname

```bash
echo PC-Archlinux > /etc/hostname
```

 - Configuración zona horaria
 - Para listar 

```bash
timedatectl list-timezones (no me funciono)
```

 - Una vez que encontramos la zona ejecutar

```bash
ln -sf /usr/share/zoneinfo/America/Buenos_Aires /etc/localtime
```

  - Configurar idioma del sistema utilizamos nano

```bash
nano /etc/locale.gen
```

   - Para seleccionar el pis borramos el #es_AR.UTF-8 (es_AR.UTF-8)
   - Guardamos cambios 

```bash
echo LANG=es_AR.UTF8 > /etc/locale.conf   
```

 - Generamos el archivo locale.gen 

```bash
locale-gen
```

  _ Configuración del reloj

```bash
hwclock -w
```

  - Configuramos por definitivo el teclado

```bash
echo KEYMAP=la-latin1 > /etc/vconsole.conf
```

 - Instalar el grub
 - Con uefi

```bash
grub-install --efi-directory=/boot/efi --bootloader -id='arch linux' --target=x86_64-efi
```

 - Con bios

```bash
grub-install /dev/vda 
```

 - Configuración del grub

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

 - Usuario y pass
 - Pass de root

```bash
passwd
```

 - Agregamos usuario

```bash
useradd -m tucho
```

 - Creamos la clave del usuario tucho

```bash
passwd tucho
```

 - Salimos, desmontamos particiones y reiniciamos

```bash
exit
umount -R /mnt
reboot
```

- Habilitar network manager

```bash
systemctl start NetworkManager.service
systemctl enable NetworkManager.service
```

 - Activar antena wifi

```bash
ip link set wlan0 up
nmcli dev wifi connect telecentro password 119082345 
```

 - Instalar servidor gráfico

```bash
pacman -S xorg-server xorg-xinit xorg-xrandr
pacman -S mesa mesa-demos
```

- Instalar display manager

```bash
pacman -S lightdm lightdm-gtk-greeter
```

 - Iniciar el servicio y

```bash
systemctl enable lightdm.service
```

- Instalar XFCE4

```bash
pacman -S xfwm4 xfce4-panel xfdesktop thunar xfce4-session xfce4-settings xfce4-appfinder xfconf xfce4-goodies network-manager-applet pulseaudio
```

 - Instalar motores Gtk

```bash
pacman -S gtk-engines gtik-engine-murrine gnome-themes-standard
```

 - Crear directorios de usuario

```bash
pacman -S xdg-user-dirs
xdg-user-dirs-update
```

- Instalar una terminal

```bash
pacman -S tilix
```

---


### Instalar qemu en ARCH

```bash
sudo pacman -S qemu virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat
sudo pacman -S ebtable iptables
sudo pacman -S libguestfs
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
ystemctl status libvirtd.service
systemctl status libvirtd.service
sudo usermod -a -G libvirt $(whoami)
sudo systemctl restart libvirtd.service
sudo virsh net-list --all
virsh net-start default
sudo virsh net-start default
sudo virsh net-list --all
sudo virsh net-autostart default
sudo virsh net-list --all
```

### Comandos para usar QEMU

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







