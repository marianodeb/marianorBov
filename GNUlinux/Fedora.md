## Paquetes RPM (Red Hat, Fedora y similares)


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

```
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
rpm -qc package_name
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


Actualizador de paquetes YUM (Red Hat, Fedora y similares)

Descargar e instalar un paquete rpm.

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
yum list: 
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










