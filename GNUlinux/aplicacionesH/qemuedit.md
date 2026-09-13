
# Guía Completa de QEMU/KVM - Actualizada 2026

## 📋 Requisitos y Verificaciones Previas

### 1. Verificar Soporte de Virtualización del Procesador

```bash
# Verificar si el procesador soporta virtualización
# Si es Intel debe aparecer 'vmx' y si es AMD 'svm'
grep -E --color '(vmx|svm)' /proc/cpuinfo

# Contar cuántos núcleos soportan virtualización
# Si devuelve 0, la virtualización NO está activada
egrep -c '(vmx|svm)' /proc/cpuinfo

# Verificar estado de KVM (más detallado)
kvm-ok
```

**Qué hace cada comando:**

* `grep -E --color`: Busca y resalta los flags de virtualización en los núcleos del procesador.
* `egrep -c`: Cuenta cuántas líneas contienen los flags (número de núcleos con soporte).
* `kvm-ok`: Herramienta que verifica si KVM está disponible y funcionando correctamente.

### 2. Verificar Activación en BIOS/UEFI

Si el comando anterior devuelve 0, debes activar la virtualización en la BIOS/UEFI:

**Pasos comunes:**

1. Reiniciar tu PC.
2. Presionar F2, Del, F10, Esc o F12 durante el arranque (depende del fabricante).
3. Buscar la configuración avanzada (Advanced) o CPU.
4. Activar: Intel Virtualization Technology (VT-x) o AMD SVM.
5. Guardar los cambios y salir.

**Verificar nuevamente:**

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
# Debe devolver un número mayor a 0
```

## 🚀 Instalación de QEMU/KVM

### Método 1: Instalación Completa (Recomendado)

```bash
# Actualizar repositorios
sudo apt update

# Instalar todos los paquetes necesarios
sudo apt install -y qemu-kvm \
    libvirt-clients \
    libvirt-daemon-system \
    libvirt-daemon \
    bridge-utils \
    virt-manager \
    virtinst \
    ovmf \
    qemu-utils \
    qemu-system-x86

# Instalar para mejor soporte gráfico si no funciona probar la de mas abajo
sudo apt install -y spice-client-gtk \
    gir1.2-spice-client-gtk-3.0 \
    libspice-client-gtk-3.0-5

# probar esta si la de arriba no anda *
sudo apt install -y spice-client-gtk gir1.2-spiceclientgtk-3.0 virt-viewer
```

**Explicación de paquetes:**

* `qemu-kvm`: Núcleo del emulador con soporte KVM.
* `libvirt-clients`: Herramientas cliente para libvirt.
* `libvirt-daemon-system`: Demonio de libvirt y configuración del sistema.
* `bridge-utils`: Herramientas para crear puentes de red.
* `virt-manager`: Interfaz gráfica para gestionar máquinas virtuales.
* `virtinst`: Herramientas para instalar VMs desde la línea de comandos.
* `ovmf`: Soporte UEFI para VMs.
* `qemu-utils`: Utilidades adicionales de QEMU.
* `spice-*`: Mejor rendimiento gráfico y portapapeles compartido.

### Método 2: Instalación Mínima

```bash
# Solo componentes esenciales
sudo apt install -y qemu-kvm libvirt-daemon-system virtinst
```

## ⚙️ Configuración y Servicios

### 1. Iniciar y Habilitar Servicios

```bash
# Habilitar e iniciar libvirtd (se ejecuta al inicio automáticamente)
sudo systemctl enable --now libvirtd

# Verificar estado del servicio
sudo systemctl status libvirtd

# Habilitar servicios adicionales si es necesario
sudo systemctl enable --now virtlogd
sudo systemctl enable --now virtlockd
```

### 2. Configurar Red Virtual

```bash
# Ver todas las redes disponibles
sudo virsh net-list --all

# Iniciar la red 'default' (proporciona NAT)
sudo virsh net-start default

# Verificar que la red esté activa
sudo virsh net-list --all

# Configurar la red para que se inicie automáticamente
sudo virsh net-autostart default

# Ver información detallada de la red
sudo virsh net-info default
```

**Qué hace la red default:**

* Proporciona conexión NAT a Internet.
* Asigna IPs en el rango 192.168.122.x.
* Permite a las VMs salir a Internet, pero no ser accesibles desde fuera.

### 3. Agregar Usuario a Grupos

```bash
# Agregar usuario a los grupos necesarios
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
sudo usermod -aG libvirt-qemu $USER

# Verificar grupos del usuario
groups $USER
```

**Qué hacen estos grupos:**

* `kvm`: Permite usar el módulo KVM para aceleración por hardware.
* `libvirt`: Acceso a la gestión de libvirt.
* `libvirt-qemu`: Permite administrar procesos de QEMU.

### 4. Reiniciar Sistema

```bash
# Reiniciar para aplicar los cambios de grupos
sudo reboot
```

**Nota:** Después del reinicio, todos los cambios de permisos surtirán efecto correctamente.

## 📁 Estructura de Directorios

### Crear Directorios para Organización

```bash
# Crear directorio base para VMs
mkdir -p ~/vms

# Crear directorio para ISOs
mkdir -p ~/vms/iso

# Crear directorio para discos virtuales
mkdir -p ~/vms/disks

# Crear directorio para imágenes
mkdir -p ~/vms/images

# Verificar la estructura creada
tree ~/vms
```

**Estructura resultante:**

```
~/vms/
├── iso/      # Archivos .iso de sistemas operativos
├── disks/    # Discos virtuales .qcow2
└── images/   # Otras imágenes o snapshots
```

### Configurar Almacenamiento en Virt-Manager

1. Abrir Virt-Manager.
2. Ir a `Edit` → `Connection Details`.
3. Seleccionar la pestaña `Storage`.
4. Hacer clic en `+` para agregar un nuevo pool.
5. Configurar:
* **Name:** `vms-pool`
* **Type:** `dir: Filesystem Directory`
* **Target Path:** `/home/[tu_usuario]/vms`

6. Hacer clic en `Finish`.

**Ventajas del pool de almacenamiento:**

* Organización centralizada.
* Fácil gestión desde la interfaz gráfica.
* Soporte para diferentes tipos de almacenamiento.

## 🖥️ Crear VM desde Interfaz Gráfica (Virt-Manager)

### Paso 1: Abrir Virt-Manager

```bash
# Desde terminal
virt-manager

# O desde el menú de aplicaciones → System Tools → Virtual Machine Manager
```

### Paso 2: Crear Nueva VM

1. Hacer clic en el icono del monitor con una estrella 📺✨ (Create a new virtual machine).
2. Seleccionar método de instalación:
   - **Local install media (ISO image or CDROM)** → Seleccionar esto.
3. Hacer clic en `Forward`.

### Paso 3: Seleccionar ISO

1. Hacer clic en `Browse...`.
2. Navegar a `~/vms/iso/`.
3. Seleccionar tu archivo .iso.
4. También puedes elegir `Use CDROM` si tienes un disco físico.
5. Hacer clic en `Forward`.

**Si no ves la ISO:**

```bash
# Asegúrate de que la ISO tenga los permisos correctos
chmod 644 ~/vms/iso/*.iso
```

### Paso 4: Configurar Recursos

* **Memory (RAM):**
* Mínimo recomendado: 2048 MB (2 GB).
* Para servidores: 4096 MB (4 GB) o más.
* Windows 10/11: 4096 MB mínimo.


* **CPUs:**
* 1 o 2 para uso básico.
* Más para servidores o aplicaciones pesadas.
* No excedas el número de núcleos físicos de tu procesador.

### Paso 5: Configurar Almacenamiento

1. Seleccionar `Create a disk image for the virtual machine`.
2. **Size:** Especificar el tamaño (ej: 20 GB).
3. **Storage format:**
* `qcow2` (recomendado) → Soporta snapshots y compresión.
* `raw` → Más rápido pero ocupa todo el espacio asignado desde el principio.

**Opciones avanzadas:**

* `Customize configuration before install` → Para realizar cambios avanzados.
* `Select managed or other existing storage` → Para usar un disco existente.

### Paso 6: Configuración Avanzada (Opcional)

Si seleccionaste `Customize configuration before install`:

1. **Overview:**
* Firmware: `BIOS` o `UEFI`.
* Chipset: `Q35` (moderno) o `i440FX` (clásico).

2. **CPU:**
* Topology: Configurar núcleos, hilos y sockets.
* Model: `host-passthrough` para máximo rendimiento.

3. **Memory:**
* `Enable shared memory` para mejor rendimiento.

4. **Display:**
* Type: `VNC` o `SPICE`.
* SPICE ofrece una mejor experiencia general.

5. **Video:**
* Model: `virtio` (recomendado) o `QXL`.
* RAM: Aumentarla para mejor rendimiento gráfico.

6. **Network:**
* Source: `default` (NAT).
* Device model: `virtio` (recomendado).

7. **Boot Options:**
* Prioridad: CDROM primero, luego disco duro.

### Paso 7: Iniciar Instalación

1. Hacer clic en `Begin Installation` (Comenzar instalación).
2. Seguir el proceso de instalación del SO seleccionado.
3. Después de instalar, la VM se reiniciará automáticamente.

### Paso 8: Post-Instalación

```bash
# Verificar que la VM está corriendo
sudo virsh list --all

# Conectarse a la VM después de la instalación
virt-manager  # Seleccionar la VM y abrir la consola
```

## 💻 Crear VM desde Línea de Comandos

### Método 1: Usando virt-install (Recomendado)

#### Paso 1: Crear Disco Virtual

```bash
# Crear disco de 20GB en formato qcow2
virt-install --disk path=~/vms/disks/mi-vm.qcow2,size=20,format=qcow2 \
    --virt-type kvm \
    --os-variant=ubuntu22.04 \
    --network network=default,model=virtio \
    --graphics spice \
    --video qxl \
    --metadata name=mi-vm

# Verificar la creación del disco
qemu-img info ~/vms/disks/mi-vm.qcow2

```

#### Paso 2: Iniciar Instalación

```bash
# Instalación completa con ISO
sudo virt-install \
    --name "mi-vm" \
    --memory 2048 \
    --vcpus 2 \
    --disk path=~/vms/disks/mi-vm.qcow2,size=20,format=qcow2 \
    --cdrom ~/vms/iso/ubuntu-22.04-desktop-amd64.iso \
    --os-variant ubuntu22.04 \
    --network bridge=virbr0,model=virtio \
    --graphics spice,listen=0.0.0.0,port=5900 \
    --video qxl \
    --virt-type kvm \
    --boot cdrom,hd \
    --noautoconsole

```

#### Paso 3: Conectar a la VM

```bash
# Conectarse usando SPICE
virt-viewer --connect qemu:///system mi-vm

# O usando VNC
virt-viewer --connect qemu:///system --direct mi-vm
```

### Método 2: Usando QEMU Directo

#### Crear VM Básica

```bash
# Crear disco
qemu-img create -f qcow2 ~/vms/disks/mi-vm.qcow2 20G

# Verificar
qemu-img info ~/vms/disks/mi-vm.qcow2

# Iniciar VM con ISO
qemu-system-x86_64 \
    -machine type=pc,accel=kvm \
    -m 2048 \
    -smp cores=2,threads=1,sockets=1 \
    -name "mi-vm" \
    -drive file=~/vms/disks/mi-vm.qcow2,format=qcow2 \
    -cdrom ~/vms/iso/ubuntu-22.04-desktop-amd64.iso \
    -netdev user,id=net0 \
    -device virtio-net-pci,netdev=net0 \
    -vga qxl \
    -display gtk,gl=on \
    -device intel-hda -device hda-duplex
```

### Método 3: Clonar VM Existente

```bash
# Clonar disco
qemu-img convert -f qcow2 -O qcow2 ~/vms/disks/vm-original.qcow2 ~/vms/disks/vm-clonada.qcow2

# Crear nueva VM desde el clon
sudo virt-install \
    --name "vm-clonada" \
    --memory 2048 \
    --vcpus 2 \
    --disk path=~/vms/disks/vm-clonada.qcow2 \
    --import \
    --os-variant ubuntu22.04 \
    --network network=default \
    --graphics spice
```

## 🛠️ Comandos Útiles de Gestión

### Gestión de Discos

```bash
# Crear disco
qemu-img create -f qcow2 disco.qcow2 10G

# Convertir discos (VMDK → QCOW2)
qemu-img convert -p -f vmdk -O qcow2 vmware.vmdk vmware.qcow2

# Redimensionar disco (añadir 10G)
qemu-img resize disco.qcow2 +10G

# Ver información del disco
qemu-img info disco.qcow2

# Crear snapshot del disco
qemu-img snapshot -c "snapshot-antes-actualizacion" disco.qcow2

# Ver snapshots
qemu-img snapshot -l disco.qcow2

# Revertir snapshot
qemu-img snapshot -a "snapshot-antes-actualizacion" disco.qcow2
```

### Gestión de VMs con virsh

```bash
# Listar VMs
virsh list --all

# Iniciar VM
virsh start mi-vm

# Apagar VM (apagado seguro/graceful)
virsh shutdown mi-vm

# Forzar apagado (como desenchufar)
virsh destroy mi-vm

# Reiniciar VM
virsh reboot mi-vm

# Suspender y reanudar
virsh suspend mi-vm
virsh resume mi-vm

# Ver información de VM
virsh dominfo mi-vm

# Ver estado de la VM
virsh domstate mi-vm

# Editar configuración XML
virsh edit mi-vm

# Eliminar VM (borra la configuración, no el disco)
virsh undefine mi-vm

# Snapshot de VM
virsh snapshot-create-as mi-vm mi-snapshot
virsh snapshot-list mi-vm
virsh snapshot-revert mi-vm mi-snapshot
```

### Gestión de Redes

```bash
# Ver redes
virsh net-list --all

# Crear red personalizada (desde un archivo XML)
virsh net-define network.xml
virsh net-start mi-red
virsh net-autostart mi-red

# Ver dirección IP asignada a la VM
virsh domifaddr mi-vm

# Ver detalles de la red
virsh net-info default
```

### Gestión de Recursos

```bash
# Ver uso de recursos de la VM
virsh dominfo mi-vm

# Ver estadísticas
virsh domstats mi-vm

# Cambiar recursos en tiempo real
virsh setmem mi-vm 3072  # Cambiar RAM a 3GB
virsh setvcpus mi-vm 4   # Cambiar a 4 vCPUs
```

## 📊 Comandos de Monitoreo

```bash
# Ver estado del módulo KVM
lsmod | grep kvm

# Ver procesos QEMU
ps aux | grep qemu

# Ver uso de CPU de VMs
top -c | grep qemu

# Ver uso de memoria de VMs
smem -P qemu

# Ver información de validación del sistema para VMs
virt-host-validate
```

## 🔧 Solución de Problemas Comunes

### 1. Error: "KVM is not available"

```bash
# Verificar módulos KVM
lsmod | grep kvm

# Cargar módulos manualmente
sudo modprobe kvm
sudo modprobe kvm_intel   # Para procesadores Intel
sudo modprobe kvm_amd     # Para procesadores AMD

# Verificar permisos
sudo chmod 666 /dev/kvm
```

### 2. Error: "Permission denied"

```bash
# Verificar grupos a los que perteneces
groups $USER

# Asegurar que estás en los grupos correctos
sudo usermod -aG kvm,libvirt,libvirt-qemu $USER

# Aplicar grupos sin reiniciar (o simplemente reinicia la PC)
newgrp libvirt
```

### 3. Error: "Network default not found" o "not active"

```bash
# Ver estado
virsh net-list --all

# Definir e iniciar red por defecto
sudo virsh net-define /usr/share/libvirt/networks/default.xml
sudo virsh net-start default
sudo virsh net-autostart default
```

### 4. Error: "No free USB ports"

```bash
# En la configuración de VM (línea de comandos), agregar:
-device usb-ehci -device usb-tablet

# En virt-manager:
# Ir a "Add Hardware" → "USB Host Device"
```

### 5. Rendimiento Lento

```bash
# Asegurarse de que KVM está activo.
# En virt-manager: CPU configuration → CPU model → host-passthrough
# En parámetros de QEMU: -cpu host

# Para mejor rendimiento gráfico usar:
# -vga qxl
# -device virtio-gpu
```

## 🎯 Tutorial Completo Paso a Paso

### Escenario: Crear Ubuntu 22.04 Desktop

#### Paso 1: Preparación

```bash
# Crear estructura de directorios
mkdir -p ~/vms/{iso,disks,snapshots}

# Descargar ISO (si no la tienes)
wget -P ~/vms/iso https://releases.ubuntu.com/22.04/ubuntu-22.04.3-desktop-amd64.iso
```

#### Paso 2: Crear VM

```bash
# Crear disco
qemu-img create -f qcow2 ~/vms/disks/ubuntu-desktop.qcow2 30G

# Verificar
qemu-img info ~/vms/disks/ubuntu-desktop.qcow2
```

#### Paso 3: Instalar usando virt-install

```bash
sudo virt-install \
    --name "ubuntu-desktop" \
    --memory 4096 \
    --vcpus 4 \
    --disk path=~/vms/disks/ubuntu-desktop.qcow2,size=30,format=qcow2 \
    --cdrom ~/vms/iso/ubuntu-22.04.3-desktop-amd64.iso \
    --os-variant ubuntu22.04 \
    --network network=default,model=virtio \
    --graphics spice,listen=0.0.0.0 \
    --video qxl \
    --virt-type kvm \
    --boot cdrom,hd \
    --features acpi=on,apic=on
```

#### Paso 4: Conectar e Instalar

```bash
# Conectarse a la VM
virt-viewer --connect qemu:///system ubuntu-desktop
```

#### Paso 5: Post-Instalación

```bash
# Detener VM después de la instalación
virsh shutdown ubuntu-desktop

# Iniciar sin ISO (arranca solo desde el disco)
sudo virsh start ubuntu-desktop

# Conectar
virt-viewer --connect qemu:///system ubuntu-desktop

```

#### Paso 6: Configurar Auto-Inicio

```bash
# Configurar para que inicie automáticamente con el sistema
virsh autostart ubuntu-desktop

# Verificar
virsh dominfo ubuntu-desktop | grep Autostart
```

#### Paso 7: Crear Snapshot antes de actualizar

```bash
# Crear snapshot
virsh snapshot-create-as ubuntu-desktop \
    --name "estable-antes-update" \
    --description "Snapshot antes de actualizar el sistema"

# Listar snapshots
virsh snapshot-list ubuntu-desktop
```

## 📝 Resumen de Comandos Rápidos

### Comandos Diarios

```bash
# Iniciar virt-manager
virt-manager

# Ver máquinas
virsh list --all

# Iniciar máquina
virsh start nombre-vm

# Apagar máquina
virsh shutdown nombre-vm

# Conectarse a la máquina
virt-viewer nombre-vm

# Estado de servicios
sudo systemctl status libvirtd
```

### Comandos de Recuperación

```bash
# Si algo sale mal, forzar apagado
virsh destroy nombre-vm

# Reconstruir red virtual
sudo virsh net-destroy default
sudo virsh net-start default

# Reconstruir VM desde un snapshot
virsh snapshot-revert nombre-vm estable-antes-update
```

## 🔒 Recomendaciones de Seguridad

1. **Aislar VMs críticas**: Usar redes separadas.
2. **Actualizar regularmente**: Tanto el sistema anfitrión (host) como las VMs.
3. **Hacer snapshots**: Siempre antes de cambios importantes o actualizaciones masivas.
4. **Monitorear recursos**: Evitar la sobrecarga de CPU y RAM del host.
5. **Backups**: Respaldar discos importantes en unidades externas.

```bash
# Backups simples (exportar configuración y copiar disco)
sudo virsh dumpxml nombre-vm > ~/backups/nombre-vm.xml
cp ~/vms/disks/nombre-vm.qcow2 ~/backups/
```

## 📚 Recursos Adicionales

```bash
# Documentación del sistema
man qemu-kvm
man virt-install
man virsh

# Información de validación del sistema
virt-host-validate

# Probando versiones de la instalación
virsh version
qemu-img --version

```


## qemu (nota borrador)


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

