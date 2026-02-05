buscar el canal punto y coma
## Ficheros de configuracion de Red 


|Caracteristicas|Descripcion|
|---|---|
|/etc/hosts|Contiene informacion de los equipos conocidos y sus ip|
|/etc/services|Contiene informacion de los puertos asociados a cada uno de los servicios de red|
|/etc/nsswitch.conf|Contiene la configuracion del orden de busqueda para ciertos ficheros de configuracion|
|/etc/resolv.conf|Contiene la configuracion de uso del servidor de nombre DNS|
|/etc/network/interfaces|Contiene la informacion de la configuracion ip  del servidor dhcp, DNS y mas|
|/etc/init.d/networking|Es el script de reinicio de los servicios de red desde la terminal|



Manual de la herramienta ip

```bash
man ip
```


```bash
netstat -rn
```

```bash
ip route
```

Mostrar dispositivos de red y su configuración.

```bash
ip link show 
```

Activar una interfaz de red.

```bash
ip link set eth0 up
```

Desactivar una interfaz de red.

```bash
ip link set eth0 down
```

Establecer una dirección IP a una interfaz.

```bash
ip address add 192.168.1.1 dev eth0
```

Añadir una interfaz virtual.

```bash
ip addr add 10.0.0.1/8 dev eth0 label eth0:1
```

Añadir una entrada en la tabla ARP.

```bash
ip neigh add 192.168.0.1 lladdr 00:11:22:33:44:55 nud permanent dev eth0
```

Desconectar un dispositivo ARP.

```bash
ip link set dev eth0 arp off
```

Para configurar una tarjeta de red física

```bash
ip addr add 192.168.0.2/24 dev eth0
```



```bash

```

```bash

```


```bash

```

```bash

```

```bash

```








