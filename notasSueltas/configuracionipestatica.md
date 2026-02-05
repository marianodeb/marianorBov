


Configurar una IP estática en Debian 13 es esencial para servidores, dispositivos de red o cualquier equipo que requiera una dirección fija. Esta guía te muestra cómo hacerlo usando la herramienta clásica ifupdown y el archivo /etc/network/interfaces.



### Paso 1: Verificar la IP actual

ejecuta:

```bash
ip a
```

```bash
ip addr
```

Busca la interfaz activa (eje: `ens33`, `eth0`, `wlan0`) y su IP dinamica actual:


```bash
inet 192.168.0.1/24
```

### Paso 2: Hacer una copia de seguridad

```bash
sudo cp -a /etc/network/interfaces{.bkp}
```

### paso 3: Configurar la IP estatica

Edita el archivo de configuracion

```bash
sudo nano /etc/NETWORK/interfaces
```

Configuracion ejemplo para ens33

```bash


# Deshabilitar DHCP (comenta estas líneas)  
# allow-hotplug ens33  
# iface ens33 inet dhcp  

# Configurar IP estática  
auto ens33  
iface ens33 inet static  
    address 192.168.1.11  
    netmask 255.255.255.0  
    network 192.168.1.0  
    broadcast 192.168.1.255  
    gateway 192.168.1.1      # ¡Agrega tu gateway!  
    dns-nameservers 8.8.8.8   # DNS opcional  

```

      - **`address`**: La dirección IP estática que quieres asignar.
      - **`netmask`**: La máscara de subred. En redes domésticas, `255.255.255.0` es lo más común.
      - **`gateway`**: La dirección IP de tu router. **Sin esto, no tendrás conexión a internet.**
      - **`dns-nameservers`**: Servidores DNS para resolver nombres de dominio (ej. `google.com`). Puedes usar los de Google (`8.8.8.8` y `8.8.4.4`) o los de tu proveedor.


### Paso 4: Aplicar los cambios


```bash
sudo systemctl restart networking
```

Verifica la nueva IP:


```bash
ip a show ens33
```

### Consejos importantes



. Gateway y DNS: Asegúrate de agregar gateway y dns-nameservers para conectividad externa.

. Interfaz correcta: Usa el nombre de tu interfaz (no siempre ens33).

. Conexión remota: Si trabajas via SSH, ten cuidado: un error puede cortar la conexión.

### Alternativa moderna: NetworkManager

Si usas una instalacion con GUI, puedes configurar IP estatica con:
  * **NetworkManager (GUI):** Si tu sistema Debian tiene una interfaz gráfica, NetworkManager es la forma más moderna y sencilla de gestionar la red.
  * **Línea de comandos:** El comando `nmcli` te permite modificar la configuración sin usar la GUI.


```bash
nmcli connection modify "Conexión cableada 1" ipv4.method manual ipv4.addresses "192.168.1.11/24" ipv4.gateway "192.168.1.1"
```

```bash
        # Configurar IP estática
        nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses "192.168.1.11/24" ipv4.gateway "192.168.1.1" ipv4.dns "8.8.8.8,8.8.4.4"

        # Para volver a DHCP
        nmcli connection modify "Wired connection 1" ipv4.method auto
```

  * **Precaución con SSH:** Si configuras esto a través de una conexión SSH, asegúrate de que los datos de la IP sean correctos. Un error podría desconectarte permanentemente hasta que tengas acceso físico al equipo.
  * **`network` vs. `broadcast`:** Las líneas `network` y `broadcast` son técnicamente opcionales en las versiones modernas de Debian, ya que la máscara de red es suficiente para calcular esos valores. Sin embargo, incluirlas no causa problemas y puede añadir claridad.
  * **Direcciones IP de ejemplo:** Recuerda reemplazar **`192.168.1.11`**, **`192.168.1.1`**, y **`ens33`** con los valores que correspondan a tu red y dispositivo.


