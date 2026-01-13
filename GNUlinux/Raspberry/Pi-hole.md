
## instalacaion Pi-hole

https://docs.pi-hole.net/main/basic-install/


```bash
$curl -sSL https://install.pi-hole.net | bash
```
## desinstalar

```bash
$pihole uninstall
```
## actualizacion

```bash
$pihole -up
```
## cambiar password **QuiVX-Gj**

**usuario http://192.168.0.115/admin**

```bash
$pihole -a -p
```

Cambiar en el archivo */etc/resolve.conf* el dns por la ip de pi-hole
*nameserver 192.168.0.115*

Nombre del servicio y verificacion del estado

*pihole-FTL.service*

```bash
systemctl status pihole-FTL.service
sudo systemctl stop pihole-FTL.service
sudo systemctl disable pihole-FTL.service
```
## Manejando procesos

##### Desactivar Pi-hole (el servicio lighttpd o dnsmasq):

Pi-hole utiliza lighttpd (un servidor web ligero) para su interfaz web y dnsmasq para el servicio DNS. Dependiendo de tu configuración, podrías tener que detener ambos. Sin embargo, si seguiste las instrucciones anteriores y no instalaste Lighttpd, solo necesitas desactivar dnsmasq:

```bash
sudo systemctl stop dnsmasq   #Comentarios Detiene el servicio inmediatamente
sudo systemctl disable dnsmasq #Comentarios Evita que se inicie automáticamente al reiniciar
```

Si sí instalaste Lighttpd (lo cual no es recomendable si tienes Nginx), también tendrías que detenerlo:

```bash
sudo systemctl stop lighttpd
sudo systemctl disable lighttpd
```


### Para usar WordPress (y Nginx):

```bash
sudo systemctl stop dnsmasq #Comentarios (y sudo systemctl stop lighttpd si lo tienes)
sudo systemctl start nginx
Para usar Pi-hole:
```

### Activar Pi-hole (el servicio dnsmasq):


```bash
sudo systemctl start dnsmasq  #Comentarios Inicia el servicio
sudo systemctl enable dnsmasq  #Comentarios Permite que se inicie automáticamente al reiniciar (si lo necesitas)
```

Si instalaste Lighttpd, también tendrías que iniciarlo:

```bash
sudo systemctl start lighttpd
sudo systemctl enable lighttpd
```

```bash
sudo systemctl stop nginx
sudo systemctl start dnsmasq #Comentarios (y sudo systemctl start lighttpd si lo tienes)
```

## Alias activar y desactivar servicio de pihole y nginx

```bash
alias nginx_on='sudo systemctl stop dnsmasq && sudo systemctl start nginx'
alias nginx_off='sudo systemctl stop nginx'
alias pihole_on='sudo systemctl stop nginx && sudo systemctl start dnsmasq'
alias pihole_off='sudo systemctl stop dnsmasq'
```

### Para iniciar WordPress:

```bash
alias start_wordpress='sudo systemctl start mariadb && sudo systemctl start php7.4-fpm && sudo systemctl start nginx'
```
### Para detener WordPress:
```bash
alias stop_wordpress='sudo systemctl stop nginx && sudo systemctl stop php7.4-fpm && sudo systemctl stop mariadb'
```
### Para iniciar Pi-hole (asumiendo que solo tienes dnsmasq):
```bash
alias start_pihole='sudo systemctl start dnsmasq'
```
### Para detener Pi-hole:
alias stop_pihole='sudo systemctl stop dnsmasq'

### Para detener todo (excepto lo esencial del sistema):
alias stop_all='sudo systemctl stop nginx && sudo systemctl stop php7.4-fpm && sudo systemctl stop mariadb && sudo systemctl stop dnsmasq'


*systemctl is-enabled service*: Este comando verifica si un servicio está habilitado para iniciarse al arrancar el sistema y devuelve enabled o disabled.

*systemctl is-active service*: Este comando verifica si un servicio se está ejecutando actualmente y devuelve active o inactive.


##### Activar Pi-hole (el servicio dnsmasq):

Para volver a activar Pi-hole (el servicio dnsmasq), ejecuta:

```bash
sudo systemctl start dnsmasq  # Inicia el servicio
sudo systemctl enable dnsmasq  # Permite que se inicie automáticamente al reiniciar (si lo necesitas)
```

Si instalaste Lighttpd, también tendrías que iniciarlo:

```bash
sudo systemctl start lighttpd
sudo systemctl enable lighttpd
```

## Pi-hole con Docker

