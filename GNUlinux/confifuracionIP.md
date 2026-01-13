

## Configurando ip estaticas y dinamicas.

### **1. Configuración en Distribuciones basadas en Debian/Ubuntu (usando `ifupdown`)**  

El archivo principal es `/etc/network/interfaces`.

### **Configuración IP Dinámica (DHCP):**

```bash
# Configuración para eth0 con DHCP
auto eth0
iface eth0 inet dhcp
```

### **Configuración IP Fija (Estática):**

```bash
# Configuración para eth0 con IP estática
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

**Explicación:**

- `auto eth0`: Activa la interfaz al iniciar el sistema.
- `inet static`: Indica que la IP es estática.
- `address`: Dirección IP.
- `netmask`: Máscara de red.
- `gateway`: Puerta de enlace predeterminada.
- `dns-nameservers`: Servidores DNS (separados por espacios).

---

## **2. Configuración en Distribuciones basadas en Red Hat/CentOS (usando `network-scripts`)**  

Los archivos de configuración están en `/etc/sysconfig/network-scripts/ifcfg-<interfaz>` (ej: `ifcfg-eth0`).

### **Configuración IP Dinámica (DHCP):**

```bash
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

### **Configuración IP Fija (Estática):**

```bash
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
ONBOOT=yes
```

**Explicación:**
- `BOOTPROTO`: `dhcp` o `static`.
- `ONBOOT=yes`: Activa la interfaz al inicio.
- `DNS1`, `DNS2`: Servidores DNS.

---

## **3. Configuración con `Netplan` (Ubuntu 18.04+ y derivadas)**  

Netplan usa archivos YAML en `/etc/netplan/` (ej: `01-netcfg.yaml`).

### **Configuración IP Dinámica (DHCP):**

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
```

### **Configuración IP Fija (Estática):**

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      addresses:
        - 192.168.1.100/24
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```

**Comandos clave:**

```bash
sudo netplan apply  # Aplica los cambios
sudo netplan try    # Prueba la configuración (revertirá si no se confirma)
```

---

## **4. Configuración con `systemd-networkd` (Distribuciones modernas)**  

Archivos en `/etc/systemd/network/` (ej: `20-wired.network`).

### **Configuración IP Dinámica (DHCP):**

```ini
[Match]
Name=eth0

[Network]
DHCP=ipv4
```

### **Configuración IP Fija (Estática):**

```ini
[Match]
Name=eth0

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
```

**Comandos clave:**

```bash
sudo systemctl restart systemd-networkd  # Reinicia el servicio
```

---

### **5. Configuración de DNS (Resolv.conf)**  

El archivo `/etc/resolv.conf` guarda los DNS, pero en sistemas modernos **no se edita manualmente** (se genera automáticamente).  
Para sobreescribirlo, usa:

- En Debian/Ubuntu: Agrega `dns-nameservers` en `/etc/network/interfaces`.
- En Red Hat/CentOS: Usa `DNS1`, `DNS2` en `/etc/sysconfig/network-scripts/ifcfg-eth0`.

---

### **6. Herramientas Adicionales**

- **`nmcli` (NetworkManager)**: Para entornos gráficos o consola.

```bash
  # IP estática
  sudo nmcli con mod "Conexión cableada 1" ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8"
  sudo nmcli con up "Conexión cableada 1"
```

- **`ip`**: Comando para ver/configurar interfaces temporalmente.

```bash
sudo ip addr add 192.168.1.100/24 dev eth0  # Asigna IP temporal
```

---

### **Resumen de Pasos**

1. Identifica la interfaz: `ip a` o `ifconfig -a`.
2. Edita el archivo de configuración según tu distribución.
3. Reinicia el servicio de red:
   - Debian/Ubuntu (ifupdown): `sudo systemctl restart networking`.
   - Red Hat/CentOS: `sudo systemctl restart network`.
   - Netplan: `sudo netplan apply`.
4. Verifica con `ip a` o `ping google.com`.


