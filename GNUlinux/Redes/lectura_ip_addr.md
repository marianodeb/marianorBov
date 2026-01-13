
## Lectura de `ip addr` y definiciones de abreviaturas


```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master br0 state UP group default qlen 1000
    link/ether 10:ff:e0:da:39:e9 brd ff:ff:ff:ff:ff:ff
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether fa:8a:ac:7f:b2:82 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.31/24 brd 192.168.0.255 scope global dynamic br0
       valid_lft 3094sec preferred_lft 3094sec
    inet6 fdaa:bbcc:ddee:0:f88a:acff:fe7f:b282/64 scope global dynamic mngtmpaddr 
       valid_lft 2006054623sec preferred_lft 2006054623sec
    inet6 2800:810:429:8c80:f88a:acff:fe7f:b282/64 scope global dynamic mngtmpaddr 
       valid_lft 2705279sec preferred_lft 2705279sec
    inet6 fe80::f88a:acff:fe7f:b282/64 scope link 
       valid_lft forever preferred_lft forever
4: lxcbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 00:16:3e:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 10.0.3.1/24 brd 10.0.3.255 scope global lxcbr0
       valid_lft forever preferred_lft forever
5: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 52:54:00:4d:7f:e5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0
       valid_lft forever preferred_lft forever
```


### **1. Interfaz `lo` (Loopback)**

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
```

- **Función**:  
  Interfaz virtual para comunicaciones internas de la máquina (no requiere hardware físico).
- **Detalles**:
  - **Flags**: `LOOPBACK` (tráfico local), `UP` (activada), `LOWER_UP` (enlace físico activo).
  - **MTU 65536**: Tamaño máximo de paquete permitido.
  - **Dirección IPv4**: `127.0.0.1/8` (rango reservado para localhost).  
    - `scope host`: Solo accesible desde este equipo.
  - **Dirección IPv6**: `::1/128` (equivalente a localhost en IPv6).  
    - `noprefixroute`: No crea rutas adicionales.


### **2. Interfaz `enp3s0` (Física/Ethernet)**
```bash
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel master br0 state UP group default qlen 1000
    link/ether 10:ff:e0:da:39:e9 brd ff:ff:ff:ff:ff:ff
```
- **Función**:  
  Interfaz de red física (ej: tarjeta Ethernet). No tiene IP asignada directamente.
- **Detalles**:
  - **Flags**: `BROADCAST` (envía difusiones), `MULTICAST` (soporta multidifusión), `UP` (activada), `LOWER_UP` (cable conectado).
  - **MTU 1500**: Tamaño estándar para Ethernet.
  - **`master br0`**: Está esclavizada al bridge `br0` (su tráfico se gestiona a través de él).
  - **MAC**: `10:ff:e0:da:39:e9` (dirección física de la tarjeta).


### **3. Bridge `br0` (Puente de Red)**

```bash
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether fa:8a:ac:7f:b2:82 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.31/24 brd 192.168.0.255 scope global dynamic br0
       valid_lft 1864sec preferred_lft 1864sec
    inet6 fdaa:bbcc:ddee:0:f88a:acff:fe7f:b282/64 scope global dynamic mngtmpaddr 
       valid_lft 2006054645sec preferred_lft 2006054645sec
    inet6 2800:810:429:8c80:f88a:acff:fe7f:b282/64 scope global dynamic mngtmpaddr 
       valid_lft 2705301sec preferred_lft 2705301sec
    inet6 fe80::f88a:acff:fe7f:b282/64 scope link 
       valid_lft forever preferred_lft forever
```

- **Función**:  
  Bridge (puente) que conecta interfaces (como `enp3s0`) y gestiona su tráfico. Actúa como interfaz de red principal.
- **Detalles**:
  - **Dirección IPv4**: `192.168.0.31/24` (dinámica, asignada por DHCP).  
    - `scope global`: Accesible desde otras redes.
    - `valid_lft 1864sec`: Tiempo restante de validez (DHCP).
  - **Direcciones IPv6**:
    - 2 direcciones globales dinámicas (con prefijos diferentes).
    - 1 dirección `fe80::...`: Enlace-local (solo para red local).
  - **MAC**: `fa:8a:ac:7f:b2:82` (dirección del bridge).


### **4. Bridge `lxcbr0` (Para contenedores LXC)**

```bash
4: lxcbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 00:16:3e:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 10.0.3.1/24 brd 10.0.3.255 scope global lxcbr0
       valid_lft forever preferred_lft forever
```

- **Función**:  
  Bridge para contenedores LXC (Linux Containers). Actualmente inactivo.
- **Detalles**:
  - **Estado**: `DOWN` y `NO-CARRIER` (no hay dispositivos conectados).
  - **Dirección IPv4**: `10.0.3.1/24` (estática, configuración NAT para contenedores).
  - **MAC**: `00:16:3e:00:00:00` (rango reservado para máquinas virtuales).



### **5. Bridge `virbr0` (Para virtualización libvirt/KVM)**

```bash
5: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 52:54:00:4d:7f:e5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0
       valid_lft forever preferred_lft forever
```

- **Función**:  
  Bridge predeterminado para máquinas virtuales (libvirt/KVM). Actualmente inactivo.
- **Detalles**:
  - **Estado**: `DOWN` y `NO-CARRIER` (sin VMs conectadas).
  - **Dirección IPv4**: `192.168.122.1/24` (estática, sirve como gateway para VMs).
  - **MAC**: `52:54:00:...` (rango estándar para virtualización).


### **Resumen de Funciones Clave**
| **Interfaz** | **Tipo**      | **Función Principal**                              | **Estado** |
|--------------|---------------|----------------------------------------------------|------------|
| `lo`         | Loopback      | Comunicaciones internas del sistema.               | UP         |
| `enp3s0`     | Física        | Conexión Ethernet física (esclava de `br0`).       | UP         |
| `br0`        | Bridge        | Interfaz principal (maneja tráfico de `enp3s0`).  | UP         |
| `lxcbr0`     | Bridge (LXC)  | Red para contenedores LXC.                         | DOWN       |
| `virbr0`     | Bridge (KVM)  | Red para máquinas virtuales KVM/libvirt.           | DOWN       |


## Tabla de Términos/Abreviaturas

### Diccionario Completo de Términos/Abreviaturas en Salidas de `ip addr`

| **Término**          | **Significado**                                                                                                                                 | **Ejemplo/Tipo**                                                                 |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **`lo`**             | **Loopback**: Interfaz virtual para tráfico interno del sistema.                                                                               | `lo`                                                                            |
| **`en`**             | **Ethernet**: Prefijo para interfaces físicas cableadas.                                                                                       | `enp3s0`, `ens1`                                                                |
| **`wl`**             | **Wireless LAN**: Prefijo para interfaces inalámbricas.                                                                                        | `wlp2s0` (Wi-Fi)                                                                |
| **`ww`**             | **Wireless WAN**: Prefijo para interfaces móviles (4G/5G).                                                                                     | `wwp0s20u2` (Módem USB)                                                         |
| **`br`**             | **Bridge**: Dispositivo que une redes (físicas/virtuales).                                                                                     | `br0`, `br-lan`                                                                 |
| **`virbr`**          | **Virtualization Bridge**: Bridge para máquinas virtuales (libvirt/KVM).                                                                       | `virbr0`, `virbr1`                                                              |
| **`lxcbr`**          | **LXC Bridge**: Bridge para contenedores Linux (LXC).                                                                                          | `lxcbr0`                                                                        |
| **`veth`**           | **Virtual Ethernet**: Interfaces virtuales emparejadas (común en contenedores).                                                                | `veth0`, `vetha1b2`                                                             |
| **`bond`**           | **Bonding**: Agrupación de interfaces para redundancia/rendimiento.                                                                            | `bond0`                                                                         |
| **`tun`/`tap`**      | **Túnel/TAP**: Interfaces para VPN/virtualización.                                                                                             | `tun0`, `tap0`                                                                  |
| **`pX`**             | **Bus PCI**: Número de ranura PCI donde está el hardware.                                                                                      | `p3` en `enp3s0`                                                                |
| **`sY`**             | **Slot**: Índice del slot en el bus PCI.                                                                                                       | `s0` en `enp3s0`                                                                |
| **`mtu`**            | **Maximum Transmission Unit**: Tamaño máximo de paquete (bytes).                                                                               | `mtu 1500` (estándar), `mtu 9000` (jumbo frames)                                |
| **`qdisc`**          | **Queueing Discipline**: Algoritmo de gestión de tráfico.                                                                                      | `qdisc fq_codel` (justo), `qdisc pfifo_fast` (predeterminado)                   |
| **`state`**          | **Estado operativo**: `UP` (activa), `DOWN` (inactiva), `UNKNOWN` (sin dirección IP).                                                         | `state UP`, `state DOWN`                                                        |
| **`group`**          | **Grupo de interfaces**: Agrupación lógica (ej: `default`).                                                                                    | `group default`                                                                 |
| **`qlen`**           | **Queue Length**: Máximo paquetes en cola de espera.                                                                                           | `qlen 1000`                                                                     |
| **`link/ether`**     | **Dirección MAC**: Identificador físico de hardware.                                                                                           | `link/ether 00:11:22:33:44:55`                                                  |
| **`brd`**            | **Broadcast MAC**: Dirección MAC para difusión.                                                                                                | `brd ff:ff:ff:ff:ff:ff`                                                         |
| **`inet`**           | **Dirección IPv4**.                                                                                                                            | `inet 192.168.1.10/24`                                                          |
| **`inet6`**          | **Dirección IPv6**.                                                                                                                            | `inet6 2001:db8::1/64`                                                          |
| **`scope`**          | **Alcance de IP**:                                                                                                                                 ||
| &nbsp;&nbsp;`host`   | Solo accesible localmente (ej: `127.0.0.1`).                                                                                                   | `scope host`                                                                    |
| &nbsp;&nbsp;`global` | Accesible desde redes externas.                                                                                                                | `scope global`                                                                  |
| &nbsp;&nbsp;`link`   | Solo enlace local (IPv6).                                                                                                                      | `scope link`                                                                    |
| **`valid_lft`**      | **Valid Lifetime**: Tiempo restante de validez de IP (segundos).                                                                               | `valid_lft 86000sec`                                                            |
| **`preferred_lft`**  | **Preferred Lifetime**: Tiempo preferente de uso de IP (segundos).                                                                             | `preferred_lft 14400sec`                                                        |
| **`master`**         | Dispositivo maestro al que está esclavizada la interfaz (ej: bridge, bond).                                                                    | `master br0`                                                                    |
| **`noprefixroute`**  | **No Prefix Route**: Evita crear rutas automáticas para el prefijo (común en IPv6).                                                            | `noprefixroute`                                                                 |
| **`mngtmpaddr`**     | **Managed Temporary Address**: Dirección IPv6 temporal gestionada por el sistema.                                                              | `mngtmpaddr`                                                                    |
| **`dynamic`**        | IP asignada dinámicamente (DHCP/SLAAC).                                                                                                        | `dynamic` en `inet 192.168.1.10/24`                                             |
| **`NO-CARRIER`**     | Sin señal física (cable desconectado).                                                                                                         | Aparece en flags: `<NO-CARRIER,...>`                                            |
| **`LOWER_UP`**       | Enlace físico activo (cable conectado).                                                                                                        | `<...,LOWER_UP>`                                                                |
| **`BROADCAST`**      | Soporta transmisión a todos los dispositivos en la red.                                                                                        | `<BROADCAST,...>`                                                               |
| **`MULTICAST`**      | Soporta transmisión a múltiples dispositivos (grupos).                                                                                         | `<...,MULTICAST>`                                                               |
| **`POINTOPOINT`**    | Conexión punto a punto (ej: VPN).                                                                                                              | `<POINTOPOINT>` (no aparece en captura)                                         |
| **`SLAVE`**          | Interfaz esclava en agrupaciones (bonding).                                                                                                    | Aparece en flags                                                                |
| **`ff:ff:ff:ff:ff:ff`** | **MAC Broadcast**: Dirección para enviar a todos los dispositivos.                                                                          | Siempre en `brd`                                                                |
| **`00:00:00:00:00:00`** | **MAC Null**: Usada en loopback o interfaces no inicializadas.                                                                             | `lo` en `link/loopback`                                                         |



### Explicación Clave:

1. **Nomenclatura de interfaces**:
   - **Físicas**: `en*` (Ethernet), `wl*` (Wi-Fi), `ww*` (móvil).
   - **Virtuales**: `br*` (bridges), `veth*` (Ethernet virtual), `tun*` (túneles).
   - **Asignación automática**: 
     - `eth0`, `wlan0` (antiguo estilo).
     - `enp3s0`, `wlp2s0` (predictible, basado en hardware).

2. **Por qué `enp3s0` es esclava de `br0`**:
   - El bridge (`br0`) actúa como un **switch virtual**.
   - La interfaz física (`enp3s0`) se "conecta" a este switch para permitir que otros dispositivos virtuales (VM/contenedores) compartan la conexión física.

3. **Diferencias entre bridges**:
   - `br0`: Bridge genérico (usado para red principal).
   - `virbr0`: Bridge para virtualización (NAT automático en libvirt).
   - `lxcbr0`: Bridge para contenedores LXC (configuración por defecto).

4. **Estados clave**:
   - **`UP`**: Interfaz operativa.
   - **`LOWER_UP`**: Cable/conexión física activa.
   - **`NO-CARRIER`**: Cable desconectado o sin señal.
   - **`state DOWN`**: Interfaz administrativamente desactivada.

