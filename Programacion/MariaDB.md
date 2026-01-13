

## Instalar MariaDB en Linux

### Actualiza tu sistema:


```bash
sudo apt-get update
```

(para distribuciones basadas en Debian como Ubuntu) o

```bash
sudo yum update
```

(para distribuciones basadas en RedHat como Fedora).

### Instalar MariaDB:


```bash
sudo apt-get install mariadb-server
```

en sistemas Debian/Ubuntu o

```bash
sudo yum install mariadb-server
```

en sistemas RedHat.


### Desinstalación de MariaDB

```Bash
sudo apt-get remove --purge mariadb-server mariadb-client mariadb-common
sudo rm -r /var/lib/mysql
sudo apt autoremove
```

*sudo apt-get remove --purge mariadb-server mariadb-client mariadb-common*: Elimina los paquetes principales de MariaDB, incluyendo el servidor, el cliente y los archivos comunes. La opción *--purge* elimina también los archivos de configuración.
*sudo rm -r /var/lib/mysql*: Elimina el directorio de datos de MariaDB, donde se almacenan las bases de datos. ¡Ten mucho cuidado con este comando! Asegúrate de haber realizado una copia de seguridad si necesitas recuperar los datos.
*sudo apt autoremove*: Elimina los paquetes que ya no son necesarios después de eliminar MariaDB.

---
### Inicia y habilita el servicio:

Iniciar

```Bash
sudo systemctl start mariadb
```

Detener

```Bash
sudo systemctl stop mariadb
```

Reiniciar

```Bash
sudo systemctl restart mariadb
```

Ver estado

```Bash
sudo systemctl status mariadb
```

Habilitar inicio automático

```Bash
sudo systemctl enable mariadb
```

Deshabilitar inicio automático

```Bash
sudo systemctl disable mariadb
```


Para que MariaDB se inicie automáticamente al arrancar el sistema.

---
### Configuración de seguridad:

Es recomendable ejecutar

```bash
sudo mysql_secure_installation
```

para configurar aspectos básicos de seguridad, como la contraseña del root y la eliminación de usuarios anónimos.

---

## Conectarse al servidor MariaDB desde un terminal linux

Sintaxis:

#### ejemplos 1 Conectando directamente a la base de datos:

```bash
mysql -u mi_usuario -p mi_contraseña mi_base
```

#### ejemplo 2 Conectando al servidor y luego seleccionando la base de datos: 

```bash
mysql -u mi_usuario -p -h 192.168.1.100
USE mi_base;
```

```sql
mysql -u<usuario> -p<contraseña> <nombre_base_de_datos>
```

ejemplo:

```bash
mysql -umiusuario -pmicontrasena mibasededatos
```

#### Consideraciones:

Entre las opciones u y el usuario no debe haber espacios en blanco
Entre las opciones p y la contraseña no debe haber espacios en blanco
Dejar un espacio entre la contraseña y el nombre_de_la_base_de_datos 

Si solo utilizamos el siguiente comando nos dara un error

```bash
mysql
ERROR 1045 (28000): Access denied for user 'minimini'@'localhost' (using password: NO)
```

Esto nos mostrara si posee contraseña.
Este error se produce por que el acceso es denegado, requiere al usuario root.
Utilizaremos el sguientes comandos antes ya mensionados para ingresar y poder administrar su contraseña.

```bash
sudo mysql -u root
```

https://www.hostinet.com/formacion/general/guia-basica-mariadb/
https://mariadb.com/kb/es/


## Crear base de datos con utf8

```sql
CREATE DATABASE mi_base_de_datos CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'tu_nueva_contraseña';
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MiContraseña123';
```

### ¿Cómo proceder si no recuerdo la contraseña?

Existen varias opciones, pero la más común y segura implica restablecer la contraseña. El proceso exacto varía según tu sistema operativo y la configuración de MariaDB, pero generalmente implica los siguientes pasos:

Detener el servicio de MariaDB: Esto evita que otros procesos accedan a la base de datos mientras realizas los cambios.
Iniciar MariaDB en modo seguro: Esto permite iniciar el servidor sin requerir autenticación.
Conectarse a MariaDB: Puedes conectarte sin contraseña ya que estás en modo seguro.
Establecer una nueva contraseña: Utiliza el comando ALTER USER para cambiar la contraseña del usuario root.
Reiniciar MariaDB en modo normal: Una vez que hayas establecido la nueva contraseña, reinicia el servicio de MariaDB para que vuelva a funcionar con la nueva configuración.

Ejemplo (para sistemas basados en Debian/Ubuntu):

```Bash

sudo systemctl stop mariadb
sudo mysqld_safe --skip-grant-tables &
mysql -u root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'tu_nueva_contraseña';
flush privileges;
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Importante: Este es un ejemplo general. Los comandos y la ubicación de los archivos de configuración pueden variar según tu distribución de Linux. Te recomiendo consultar la documentación oficial de MariaDB para tu sistema operativo específico.

Consideraciones adicionales:

Riesgos: Restablecer la contraseña de esta manera puede ser arriesgado si no se realiza correctamente. Siempre realiza una copia de seguridad de tu base de datos antes de realizar cambios importantes.
Seguridad: Una vez que hayas establecido una nueva contraseña, asegúrate de cambiar la contraseña raíz y crear usuarios con privilegios limitados para mejorar la seguridad de tu base de datos.

