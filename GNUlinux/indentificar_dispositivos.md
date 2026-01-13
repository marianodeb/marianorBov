# 🐧 Guía Completa: Identificar Dispositivos en Linux

## 📋 Índice
1. [Dispositivos USB](#usb)
2. [Dispositivos PCI/PCIe](#pci)
3. [Dispositivos Bluetooth](#bluetooth)
4. [Dispositivos de Almacenamiento](#almacenamiento)
5. [Dispositivos de Red](#red)
6. [Comandos Universales](#universales)

---

## 🔌 USB {#usb}

### **`lsusb` - Listar dispositivos USB**

```bash
# Lista básica
lsusb

# Lista con detalles
lsusb -v

# Información específica de un dispositivo
lsusb -d vendor:producto
lsusb -s bus:dispositivo
```

**Ejemplo práctico:**

```bash
$ lsusb
Bus 003 Device 004: ID 1d57:130f Xenta 2.4Ghz wireless optical mouse receiver
#          ↑           ↑    ↑     ↑
#       Dispositivo   VID  PID   Descripción
```

**Leer la información:**
- **VID**: Vendor ID (Identificador del fabricante)
- **PID**: Product ID (Identificador del producto)
- **Bus**: Número de bus USB
- **Device**: Número de dispositivo en ese bus

### **`usb-devices` - Información detallada**

```bash
usb-devices
```

### **`dmesg` - Ver detección en tiempo real**

```bash
dmesg | grep -i usb
dmesg | grep -i "1d57:130f"  # Para un dispositivo específico
```

---

## 🖥️ PCI/PCIe {#pci}

### **`lspci` - Listar dispositivos PCI/PCIe**

```bash
# Lista básica
lspci

# Lista detallada
lspci -v
lspci -vv  # Más detalles
lspci -vvv # Máximos detalles

# Por categoría
lspci | grep -i network  # Tarjetas de red
lspci | grep -i audio    # Audio
lspci | grep -i vga      # Gráficos
```

**Ejemplo:**

```bash
$ lspci
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620
01:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59)
#   ↑       ↑                          ↑                     ↑
#  ID PCI  Tipo                    Fabricante           Modelo
```

### **Información específica:**

```bash
lspci -s 00:02.0      # Dispositivo específico
lspci -s 01:00.0 -vv  # Detalles completos de WiFi
```

---

## 📡 Bluetooth {#bluetooth}

### **Instalación primero:**

```bash
sudo apt install bluetooth bluez bluez-tools blueman
```

### **Comandos Bluetooth:**

#### **`hciconfig` - Controladores Bluetooth**

```bash
hciconfig          # Lista básica
hciconfig -a       # Información completa
hciconfig hci0 up  # Activar interfaz
```

#### **`bluetoothctl` - Control principal**

```bash
bluetoothctl
[bluetooth]# list                 # Ver adaptadores
[bluetooth]# power on            # Encender
[bluetooth]# agent on            # Activar agente
[bluetooth]# scan on             # Buscar dispositivos
[bluetooth]# devices             # Listar encontrados
[bluetooth]# info [MAC]          # Info dispositivo
[bluetooth]# pair [MAC]          # Emparejar
[bluetooth]# connect [MAC]       # Conectar
[bluetooth]# trust [MAC]         # Confiar automáticamente
```

#### **GUI Recomendado:**

```bash
sudo apt install blueman
blueman-manager    # Abre el administrador gráfico
```

---

## 💾 Almacenamiento {#almacenamiento}

### **`lsblk` - Listar bloques (discos/particiones)**

```bash
lsblk              # Lista básica
lsblk -f           # Con sistemas de archivos
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,FSTYPE  # Personalizado
```

**Ejemplo:**

```bash
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 465.8G  0 disk 
├─sda1   8:1    0   512M  0 part /boot/efi
└─sda2   8:2    0 465.3G  0 part /
```

### **`fdisk` - Información de particiones**

```bash
sudo fdisk -l      # Listar todos los discos
sudo fdisk -l /dev/sda  # Disco específico
```

### **`hdparm` - Información de discos duros**

```bash
sudo hdparm -I /dev/sda    # Información detallada del disco
```

### **`smartctl` - Salud de discos (SMART)**

```bash
sudo apt install smartmontools
sudo smartctl -a /dev/sda  # Información completa SMART
```

### **Para NVMe específicamente:**

```bash
sudo nvme list              # Listar NVMe
sudo nvme id-ctrl /dev/nvme0  # Información del controlador
```

---

## 🌐 Red {#red}

### **`ip link` - Interfaces de red**

```bash
ip link show               # Todas las interfaces
ip addr show               # Con direcciones IP
```

### **`iwconfig` - WiFi específico**

```bash
iwconfig                   # Interfaces inalámbricas
iwlist scan                # Escanear redes WiFi
```

### **`nmcli` - Network Manager**

```bash
nmcli dev status           # Estado dispositivos
nmcli dev wifi list        # Listar redes WiFi
nmcli con show             # Conexiones configuradas
```

### **`rfkill` - Bloqueo radiofrecuencias**

```bash
rfkill list                # Ver WiFi/Bluetooth bloqueados
rfkill unblock all         # Desbloquear todos
```

---

## 🔍 Comandos Universales {#universales}

### **`dmesg` - Mensajes del kernel**

```bash
dmesg | tail -20           # Últimos 20 mensajes
dmesg | grep -i usb        # Filtrar por USB
dmesg | grep -i bluetooth  # Filtrar por Bluetooth
```

### **`lshw` - Hardware completo**

```bash
sudo lshw                  # Todo el hardware
sudo lshw -short           # Resumen
sudo lshw -class network   # Solo red
```

### **`inxi` - Información completa del sistema**

```bash
sudo apt install inxi
inxi -Fxz                  # Información completa
inxi -A                    # Audio
inxi -N                    # Red
inxi -D                    # Almacenamiento
```

### **`udevadm` - Información de dispositivos**

```bash
udevadm info /dev/sda      # Información dispositivo
udevadm monitor            # Monitorear en tiempo real
```

---

## 🎯 Flujo de Trabajo Recomendado

### **Cuando conectas un dispositivo nuevo:**

1. **Ver detección inmediata:**

```bash
   dmesg | tail -20
```

2. **Identificar tipo:**

```bash
   lsusb                    # Si es USB
   lspci                    # Si es PCIe
   lsblk                    # Si es almacenamiento
```

3. **Obtener detalles específicos:**

```bash
   lsusb -d vid:pid -v      # USB detallado
   lspci -s id -vv          # PCIe detallado
```

4. **Verificar drivers:**

```bash
   lsmod | grep driver_name
   dmesg | grep driver_name
```

---

## 📝 Ejemplos Prácticos para Obsidian

### **Plantilla para dispositivos USB:**


## [[Dispositivo USB]]

**Comando:** `lsusb -d vid:pid -v`

**Información clave:**

- Vendor ID: `vid`
- Product ID: `pid` 
- Fabricante: 
- Descripción:
- Bus: 
- Dispositivo:
- Driver: 


### **Plantilla para almacenamiento:**


## [[Dispositivo Almacenamiento]]

**Comandos:**

```bash
lsblk -f
sudo fdisk -l /dev/sdX
```

**Información:**

- Dispositivo: `/dev/sdX`
- Tamaño: 
- Particiones:
- Sistema archivos:
- Puntos montaje:

---

## 🚀 Comandos Rápidos de Consulta

```bash
# Ver TODO el hardware rápidamente
inxi -Fxz

# Solo dispositivos conectados ahora
lsusb; lspci; lsblk; ip addr

# Salud del sistema completo
sudo lshw -short
```

---


## **GUI para Bluetooth** en Debian:

### 🖥️ Interfaces Gráficas para Bluetooth

#### **1. Blueman (EL MEJOR - Recomendado)**

```bash
# Instalación
sudo apt update
sudo apt install blueman

# Ejecución
blueman-manager
# O buscar "Bluetooth Manager" en el menú de aplicaciones
```

**Características:**

- ✅ Icono en la bandeja del sistema
- ✅ Emparejamiento fácil con un clic
- ✅ Transferencia de archivos
- ✅ Gestión de dispositivos emparejados
- ✅ Configuración de perfiles (audio, entrada, etc.)
- ✅ Compatible con todos los escritorios

**Ventajas:**

- Más completo que las alternativas
- Desarrollado específicamente para Bluetooth
- Interfaz intuitiva

---

#### **2. GNOME Bluetooth (Para GNOME)**

```bash
# Instalación
sudo apt install gnome-bluetooth

# Se integra automáticamente en Ajustes de GNOME
# Ir a Ajustes → Bluetooth
```

**Características:**
- ✅ Integración nativa con GNOME
- ✅ Interfaz minimalista
- ✅ Emparejamiento simple
- ❌ Menos opciones avanzadas

---

#### **3. KDE Bluetooth (Para KDE Plasma)**

```bash
# Instalación
sudo apt install bluedevil

# Se integra en Configuración del Sistema de KDE
```

**Características:**

- ✅ Integración nativa con KDE
- ✅ Interfaz KDE-style
- ✅ Buenas opciones de gestión

---

### 🎯 Instalación Completa Recomendada

```bash
# Paquetes esenciales de Bluetooth
sudo apt install bluetooth bluez bluez-tools

# GUI principal (Blueman)
sudo apt install blueman

# Soporte adicional
sudo apt install pulseaudio-module-bluetooth  # Para audio
sudo apt install obexftp obex-data-server     # Para transferencia archivos
```

---

### 🔧 Configuración Post-Instalación

#### **Habilitar servicios:**

```bash
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

#### **Verificar estado:**

```bash
systemctl status bluetooth
hciconfig -a
```

---

### 📱 Cómo Usar Blueman

#### **Flujo básico:**

1. **Abrir Blueman:** `blueman-manager` o click en el ícono de la bandeja
2. **Buscar dispositivos:** Click en "Search" o "Buscar"
3. **Emparejar:** Click derecho en el dispositivo → "Pair" o "Emparejar"
4. **Conectar:** Click derecho → "Connect" o "Conectar"

#### **Funciones principales:**

- **🔄 Search:** Buscar dispositivos cercanos
- **📋 Adapters:** Configurar adaptadores Bluetooth
- **📊 Local Services:** Servicios Bluetooth locales
- **⚙️ Preferences:** Configuración avanzada

---

### 🎧 Para Audio Bluetooth (Extra)

```bash
# Instalar soporte de audio
sudo apt install pulseaudio-module-bluetooth

# Recargar PulseAudio
pulseaudio -k
pulseaudio --start
```

**En Blueman:** Los auriculares aparecerán automáticamente y podrás seleccionar el perfil de audio (A2DP para calidad, HSP/HFP para llamadas).

---

### ❓ Solución de Problemas Comunes

#### **Si no aparece el ícono en la bandeja:**

```bash
# Ejecutar manualmente
blueman-applet &
```

#### **Si no detecta dispositivos:**

```bash
# Verificar que el adaptador esté activo
bluetoothctl
[bluetooth]# power on
[bluetooth]# scan on
```

#### **Si no se instala correctamente:**

```bash
# Reinstalar completo
sudo apt remove --purge blueman bluetooth bluez
sudo apt autoremove
sudo apt install bluetooth bluez blueman
```

---

### 📋 Resumen Rápido para Obsidian

```markdown
## [[GUI Bluetooth Debian]]

### **Blueman (Recomendado)**
```bash
sudo apt install blueman
blueman-manager
```

#### **GNOME Bluetooth**

```bash
sudo apt install gnome-bluetooth
# Ir a Ajustes → Bluetooth
```

#### **KDE Bluetooth**

```bash
sudo apt install bluedevil
# Ir a Configuración del Sistema → Bluetooth
```

**Comando terminal alternativo:** `bluetoothctl`




