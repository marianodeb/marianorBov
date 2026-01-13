
## DEBIAN
### APT DPKG


Instalar / actualizar un paquete deb

```bash
dpkg -i package.deb 
```

Eliminar un paquete deb del sistema.

```bash
dpkg -r package_name
```

Mostrar todos los paquetes deb instalados en el sistema.

```bash
dpkg -l
```

Mostrar todos los paquetes deb con el nombre “httpd”

```bash
dpkg -l | grep httpd
```

Obtener información en un paquete específico instalado en el sistema.

```bash
dpkg -s package_name
```

Mostar lista de ficheros dados por un paquete instalado en el sistema.

```bash
dpkg -L package_name
```

Mostrar lista de ficheros dados por un paquete no instalado todavía.

```bash
dpkg –contents package.deb
```

Verificar cuál paquete pertenece a un fichero dado.

```bash
dpkg -S /bin/ping
```

Actualizador de paquetes APT (Debian, Ubuntu y derivados)

instalar 

```bash
apt-get install package_name 
```

Instalar / actualizar un paquete deb desde un cdrom.

```bash
apt-cdrom install package_name
```

Cuando instalamos algun pakete y faltan dependencias utilizar:

```bash
apt -f intall
```
Actualizar la lista de paquetes.

```bash
apt-get update
```

Actualizar todos los paquetes instalados.

```bash
apt-get upgrade
```

Permite que se instalen nuevas versiones de paquetes si son necesarias para resolver las dependencias.

```bash
sudo apt-get upgrade --with-new-pkgs
```

Esta opción es útil cuando te encuentras con paquetes retenidos que no se actualizan debido a dependencias faltantes. Al usar --with-new-pkgs, le das al sistema la oportunidad de resolver estas dependencias instalando los paquetes necesarios.


Eliminar un paquete deb del sistema.

```bash
apt-get remove package_name
```

```bash
apt-get remove --purge package_name
```

Verificar la correcta resolución de las dependencias.

```bash
apt-get check
```

Limpiar cache desde los paquetes descargados.

```bash
apt-get clean
```

Retorna lista de paquetes que corresponde a la serie «paquetes buscados».

```bash
apt-cache search searched-package
```



---


## Pquetes FLATPAK


flatpak


Lista los paquetes instalados

```bash
flatpak list
```

Actualiza los paquetes instalados

```bash
flatpak update
```

Ejemplo: $flatpak uninstall org.videolan.VLC

```bash
flatpak uninstall
```

Elimina todos los paquetes instalados

```bash
flatpak uninstall –all
```

--

## ARCH
### Paquetes PACMAN

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

### Paqutes yay

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

En una lista los encontrados y nos pedirá seleccionar el de nuestro interés.

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
$yay -Rs <package-name>
```

Para eliminar un paquete, sus dependencias y configuraciones, debemos de teclear:

```bash
yay -Rnsc <package-name>
```

---

## FEDORA 

### Paquetes RPM (Red Hat, Fedora y similares)

Instalar un paquete rpm.

```bash
rpm -ivh package.rpm 
```

Instalar un paquete rpm ignorando las peticiones de dependencias.

```bash
rpm -ivh –nodeeps package.rpm
```

Actualizar un paquete rpm sin cambiar la configuración de los ficheros.

```bash
rpm -U package.rpm
```

Actualizar un paquete rpm solamente si este está instalado.

```bash
rpm -F package.rpm
```

Eliminar un paquete rpm.

```bash
rpm -e package_name.rpm
```

Mostrar todos los paquetes rpm instalados en el sistema.

```bash
rpm -qa
```

Mostrar todos los paquetes rpm con el nombre “httpd”.

```bash
rpm -qa | grep httpd
```

Obtener información en un paquete específico instalado.

```bash
rpm -qi package_name
```

Mostar los paquetes rpm de un grupo software.

```bash
rpm -qg “System Environment/Daemons”
```

Mostrar lista de ficheros dados por un paquete rpm instalado.

```bash
rpm -ql package_name
```

Mostrar lista de configuración de ficheros dados por un paquete rpm instalado.

```bash
rpm -qc package_name# 
```

Mostrar lista de dependencias solicitada para un paquete rpm.

```bash
rpm -q package_name –whatrequires
```

Mostar la capacidad dada por un paquete rpm.

```bash
rpm -q package_name –whatprovides
```

Mostrar los scripts comenzados durante la instalación /eliminación.

```bash
rpm -q package_name –scripts
```

Mostar el historial de revisions de un paquete rpm.

```bash
rpm -q package_name –changelog
```

Verificar cuál paquete rpm pertenece a un fichero dado.

```bash
rpm -qf /etc/httpd/conf/httpd.conf
```

Mostrar lista de ficheros dados por un paquete rpm que aún no ha sido instalado.

```bash
rpm -qp package.rpm -l
```

Importar la firma digital de la llave pública.

```bash
rpm –import /media/cdrom/RPM-GPG-KEY
```

Verificar la integridad de un paquete rpm.

```bash
rpm –checksig package.rpm
```

Verificar la integridad de todos los paquetes rpm instalados.

```bash
rpm -qa gpg-pubkey
```

Chequear el tamaño del fichero, licencias, tipos, dueño, grupo, chequeo de resumen de MD5 y última modificación.

```bash
rpm -V package_name
```

Chequear todos los paquetes rpm instalados en el sistema. Usar con cuidado.

```bash
rpm -Va
```

Verificar un paquete rpm no instalado todavía.

```bash
rpm -Vp package.rpm
```

Extraer fichero ejecutable desde un paquete rpm.

```bash
rpm2cpio package.rpm | cpio –extract –make-directories *bin*
```

Instalar un paquete construido desde una fuente rpm.

```bash
rpm -ivh /usr/src/redhat/RPMS/`arch`/package.rpm
```

Construir un paquete rpm desde una fuente rpm.

```bash
rpmbuild –rebuild package_name.src.rpm 
```

### YUM 

Actualizador de paquetes YUM (Red Hat, Fedora y similares)

descargar e instalar un paquete rpm.

```bash
yum install package_name
```

Este instalará un RPM y tratará de resolver todas las dependencies para ti, usando tus repositorios.

```bash
yum localinstall package_name.rpm
```

Actualizar todos los paquetes rpm instalados en el sistema.

```bash
yum update package_name.rpm
```

Modernizar / actualizar un paquete rpm.

```bash
yum update package_name
```

Eliminar un paquete rpm.

```bash
yum remove package_name
```

Listar todos los paquetes instalados en el sistema.

```bash
yum list
```

Encontrar un paquete en repositorio rpm.

```bash
yum search package_name
```

Limpiar un caché rpm borrando los paquetes descargados.

```bash
yum clean packages
```

Eliminar todos los ficheros de encabezamiento que el sistema usa para resolver la dependencia.

```bash
yum clean headers
```

Eliminar desde los paquetes caché y ficheros de encabezado.

```bash
yum clean all

```



