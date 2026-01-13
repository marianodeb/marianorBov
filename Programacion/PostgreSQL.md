

https://www.postgresql.org/

## Instalacion

```bash
apt install postgresql
```


### Desinstalación de PostgreSQL

```Bash
sudo apt-get remove --purge postgresql postgresql-contrib
sudo rm -r /var/lib/postgresql/data
sudo apt autoremove
```

sudo apt-get remove --purge postgresql postgresql-contrib: Elimina los paquetes principales de PostgreSQL y los paquetes adicionales.
sudo rm -r /var/lib/postgresql/data: Elimina el directorio de datos de PostgreSQL. ¡Ten mucho cuidado con este comando!
sudo apt autoremove: Elimina los paquetes que ya no son necesarios después de eliminar PostgreSQL.

## Acceso 

 Usuario por defecto postgres

```bash
sudo postgres
```

Conéctate a la base de datos PostgreSQL como superusuario:

```bash
sudo su - postgres
```

```Bash
sudo -u postgres psql
```
#### Ejemplo

Cómo ingresar al cliente psql:

Primero, cambia al usuario del sistema operativo postgres:

```bash
sudo su - postgres
```

Luego, abre el cliente psql:

```
psql
```

Una vez dentro, verás el prompt de psql, como este:

```sql
postgres=#
```

Para acceder a la consola de PostgreSQL desde la línea de comandos, el comando más común es:

```Bash
psql
```

#### Diferencias entre el shell y el cliente psql

Shell del sistema operativo **($ o postgres$)**: Aquí puedes ejecutar comandos de Linux, como ls, cd, etc. También puedes iniciar el cliente psql desde aquí escribiendo psql.

Cliente psql **(postgres=#)**: Aquí puedes ejecutar comandos de PostgreSQL, como SELECT, CREATE TABLE, o los metacomandos (\?, \l, etc.).

Este comando te conectará a la base de datos postgres por defecto, utilizando el usuario postgres.


Conectarse a una base de datos específica:

Si deseas conectarte a una base de datos diferente, puedes especificar el nombre de la base de datos de la siguiente manera:


```Bash
psql mi_base_de_datos
```

Conectarse con un usuario específico:

Para conectarte con un usuario diferente, utiliza la opción -U o --username:

```Bash
psql -U mi_usuario mi_base_de_datos
```

### Conectarse a un servidor remoto:

Si tu base de datos está en un servidor remoto, indica la dirección del servidor con la opción -h o --host:

```Bash
psql -h mi_servidor -U mi_usuario mi_base_de_datos
```

Ejemplo completo:

```Bash
psql -h 192.168.1.100 -U myuser -d mydatabase
```

Este comando te conectará a la base de datos mydatabase en el servidor con dirección IP 192.168.1.100, utilizando el usuario myuser.

Otras opciones útiles:

-po--port: Especifica un puerto diferente al 5432 por defecto.
-Wo--password: Fuerza la solicitud de contraseña, incluso si está almacenada en algún archivo de configuración.


#### Conexión remota a PostgreSQL

Cuando quieres conectarte remotamente a un servidor PostgreSQL, la conexión es independiente del sistema operativo. Es decir, puedes conectarte a PostgreSQL sin estar dentro de la máquina por SSH. Solo necesitas saber:

La IP del servidor donde está instalado PostgreSQL.
El usuario de PostgreSQL con el que deseas acceder.
La base de datos a la que deseas acceder.
El puerto (por defecto, PostgreSQL usa el puerto 5432).

Comando para conectarte a PostgreSQL remotamente:

Si estás en una máquina diferente (por ejemplo, tu computadora local) y quieres conectarte al servidor PostgreSQL en tu Raspberry Pi (por ejemplo), usarías algo como esto:

```bash
psql -h <ip_del_servidor> -U <usuario_postgresql> -d <nombre_base_de_datos>
```

**-h** <ip_del_servidor>: La dirección IP de la Raspberry Pi o del servidor donde PostgreSQL está instalado.
**-U** <usuario_postgresql>: El usuario de PostgreSQL con el que te deseas autenticar.
**-d** <nombre_base_de_datos>: El nombre de la base de datos a la que deseas conectarte.

Ejemplo práctico de conexión remota:

Si la IP de tu Raspberry Pi es 192.168.1.100, y el usuario de PostgreSQL es postgres, y deseas acceder a la base de datos llamada empresa, el comando sería:

```bash
psql -h 192.168.1.100 -U postgres -d empresa
```

¿Cómo hacer esto posible?

Para que puedas acceder remotamente a PostgreSQL, debes asegurarte de que el servidor de bases de datos esté configurado para aceptar conexiones remotas. Esto se hace principalmente en dos archivos:

1 postgresql.conf: Debes asegurarte de que PostgreSQL esté configurado para escuchar en todas las interfaces o en la interfaz de red correcta (no solo en localhost).
En el archivo postgresql.conf, busca y modifica la siguiente línea:

```bash
listen_addresses = '*'
```

Esto hace que PostgreSQL escuche en todas las interfaces de red (no solo en localhost).

2 **pg_hba.conf**: Este archivo controla qué direcciones IP pueden conectarse a PostgreSQL y con qué métodos de autenticación. Debes permitir las conexiones desde la IP o rango de direcciones que deseas permitir.

Añade una línea similar a esta para permitir conexiones desde cualquier IP (aunque esto se debe restringir para mayor seguridad):

```
host    all             all             0.0.0.0/0               md5
```

O para permitir conexiones solo desde una IP específica:

```
host    all             all             192.168.1.100/32        md5
```

Después de hacer estos cambios, recuerda reiniciar PostgreSQL para que los cambios surtan efecto:

```
sudo systemctl restart postgresql
```

¿Cómo saber si PostgreSQL está configurado correctamente para conexiones remotas?

1 Revisa si PostgreSQL está escuchando en el puerto 5432: Puedes verificar si PostgreSQL está escuchando en el puerto correcto (por defecto 5432) usando el siguiente comando:

```
sudo netstat -plnt | grep 5432
```

2 Verifica si el firewall está permitiendo conexiones: Si tienes un firewall activo, asegúrate de que esté permitiendo las conexiones al puerto 5432. Si estás usando ufw (Uncomplicated Firewall), puedes habilitar el puerto 5432 con el siguiente comando:

```
sudo ufw allow 5432/tcp
```


### Crear usuario

Crea el usuario "marianito" con una shell restringida:

```Bash
CREATE USER marianito WITH PASSWORD 'tu_contraseña_fuerte';
```

Concede los permisos CRUD sobre la tabla "hortalizas" al usuario "marianito":

```SQL
GRANT ALL PRIVILEGES ON TABLE hortalizas TO marianito;
```



Ejemplo de conexión desde la línea de comandos como el usuario "marianito":

```Bash
psql -U marianito -d la_huerta
```

### Salir de psql:

Para salir de la consola de PostgreSQL, escribe \q y presiona Enter.

```postgresql
/q
```

Comando sudo su - postgres:

¿Qué hace? Este comando te permite cambiar de usuario a postgres. Esto significa que, una vez ejecutado, estarás dentro de la sesión del usuario postgres.
¿Cuándo usarlo? Es útil cuando necesitas ejecutar comandos directamente como el usuario postgres, por ejemplo, para crear bases de datos o usuarios, o para realizar tareas administrativas.

Comando psql:

¿Qué hace? Este comando te proporciona un intérprete de comandos interactivo para PostgreSQL, es decir, una consola donde puedes escribir y ejecutar consultas SQL directamente.
¿Cuándo usarlo? Es ideal cuando necesitas interactuar con una base de datos existente, ejecutar consultas, modificar datos, etc.

Diferencias clave:

|Caracteristicas|sudo su - postgres|psql|
|---|---|---|---|---|
|Objetivo|Cambiar de usuario a postgres|Proporcionar un interprete de comandos AQL|
|Contexto|Linea de comandos del sistema operativo|Entorno de la base de datos PostrgreSQL|
|Uso tipico|Tareas administrativas, creacion de bases de datos, usuarios, etc.|Ejecutar consultas SQL, grestionardatos|

| Característica            | PostgreSQL                                 | MariaDB                                     |
| ------------------------- | ------------------------------------------ | ------------------------------------------- |
| Usuario superusuario      | postgres                                   | root                                        |
| Conexión local            | psql                                       | mysql                                       |
| Conexión remota           | psql -h <ip>                               | mysql -h <ip>                               |
| Archivos de configuración | postgresql.conf, pg_hba.conf	my.cnf        |                                             |
| Comandos para gestionar   | GRANT, REVOKE, ALTER ROLE, CREATE DATABASE | GRANT, REVOKE, CREATE DATABASE, SHOW GRANTS |

¿Cuál usar?

Si quieres crear una nueva base de datos o usuario: sudo su - postgres y luego ejecutar los comandos correspondientes de PostgreSQL.
Si quieres interactuar con una base de datos existente: psql es la opción más directa.

Ejemplo:

Supongamos que quieres crear una nueva base de datos llamada mi_base_de_datos:

Con sudo su - postgres:

```Bash
sudo su - postgres
createdb mi_base_de_datos
```

Con psql: (Si ya estás conectado a un servidor PostgreSQL)

```SQL
  \c postgres  -- Conectarse a la base de datos 'postgres' (la base de datos maestra)
  CREATE DATABASE mi_base_de_datos;
```

En resumen:

sudo su - postgres te da acceso a nivel de sistema operativo para realizar tareas administrativas en PostgreSQL.
psql te proporciona un entorno interactivo para trabajar directamente con la base de datos.

¿Cuál es mejor?

Depende de lo que quieras hacer. Si necesitas realizar tareas administrativas a nivel de sistema, sudo su - postgres es una buena opción. Si simplemente quieres interactuar con la base de datos, psql es más directo.


### Crear base de datos y tablas

La siguiente instrucción SQL creará una tabla denominada cars en su base de datos PostgreSQL:

```
CREATE TABLE cars (
  brand VARCHAR(255),
  model VARCHAR(255),
  year INT
); 
```

```SQL
CREATE DATABASE la_huerta;
```

Crea la tabla "hortalizas":

```SQL
\c la_huerta
CREATE TABLE hortalizas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(50),
    tipo VARCHAR(50),
    cantidad INTEGER
);
```


### Ejemplo de crear usuario, BD, tabla  y acceso
 
```SQL
CREATE DATABASE la_huerta;
```

Conéctate como superusuario de PostgreSQL:

```Bash
sudo -u postgres psql
```

Conéctate a la base de datos "la_huerta":

```SQL
\c la_huerta
```

Crea el usuario "marianito" con contraseña y privilegios específicos:

```SQL
sudo -u postgres createuser marianito -s -P
```

Al ejecutar este comando, se te pedirá que ingreses y confirmes la contraseña para el nuevo usuario.

Otorgue todos los privilegios sobre la tabla "hortalizas" al usuario "marianito":

```SQL
GRANT ALL PRIVILEGES ON TABLE hortalizas TO marianito;
```

Crea la tabla "hortalizas" (si no existe):

```SQL
CREATE TABLE hortalizas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(50),
    tipo VARCHAR(50),
    cantidad INTEGER
);
```

Salir de la base de datos:

```SQL
    \q
```
Explicación del comando sudo -u postgres createuser marianito -s -P:

sudo -u postgres: Ejecuta el siguiente comando con los privilegios del usuario "postgres".
createuser marianito: Crea un nuevo usuario llamado "marianito" dentro de PostgreSQL.
-s: Especifica que el nuevo usuario debe tener una contraseña segura.
-P: Indica que se debe solicitar al usuario que ingrese una contraseña.

---

### Insertar 

Para insertar datos en una tabla en PostgreSQL, utilizamos la instrucción INSERT INTO.

La siguiente instrucción SQL insertará una fila de datos en la tabla cars que creó en el capítulo anterior.

```sql
INSERT INTO cars (brand, model, year)
VALUES ('Ford', 'Mustang', 1964); 
```

Insertar varias filas

Para insertar varias filas de datos, utilizamos la misma instrucción INSERT INTO, pero con varios valores:

```sql
INSERT INTO cars (brand, model, year)
VALUES
  ('Volvo', 'p1800', 1968),
  ('BMW', 'M1', 1978),
  ('Toyota', 'Celica', 1975); 
```


### La sentencia ALTER TABLE

Para agregar una columna a una tabla existente, debemos usar la sentencia ALTER TABLE.

La sentencia ALTER TABLE se usa para agregar, eliminar o modificar columnas en una tabla existente.

La sentencia ALTER TABLE también se usa para agregar y eliminar varias restricciones en una tabla existente.


### ADD COLUMN

Queremos agregar una columna llamada color a nuestra tabla cars.

Al agregar columnas, también debemos especificar el tipo de datos de la columna. Nuestra columna color será una cadena y especificamos los tipos de cadena con la palabra clave VARCHAR. También queremos restringir la cantidad de caracteres a 255:

```sql
ALTER TABLE cars
ADD color VARCHAR(255); 
```

### La instrucción UPDATE

La instrucción UPDATE se utiliza para modificar los valores de los registros existentes en una tabla.

```sql
UPDATE cars
SET color = 'red'
WHERE brand = 'Volvo'; 
```

¡Advertencia! Recuerde WHERE

Tenga cuidado al actualizar registros. Si omite la cláusula WHERE, ¡se actualizarán TODOS los registros!


Actualizar varias columnas

Para actualizar más de una columna, separe los pares nombre/valor con una coma:

```sql
UPDATE cars
SET color = 'white', year = 1970
WHERE brand = 'Toyota';
```

**La sentencia ALTER TABLE**

Para cambiar el tipo de datos o el tamaño de una columna de una tabla, debemos utilizar la sentencia ALTER TABLE.

La sentencia ALTER TABLE se utiliza para agregar, eliminar o modificar columnas en una tabla existente.

La sentencia ALTER TABLE también se utiliza para agregar y eliminar varias restricciones en una tabla existente.

### ALTER COLUMN

Queremos cambiar el tipo de datos de la columna de año de la tabla de autos de INT a VARCHAR(4).

Para modificar una columna, utilice la declaración ALTER COLUMN y la palabra clave TYPE seguida del nuevo tipo de datos:

```sql
ALTER TABLE cars
ALTER COLUMN year TYPE VARCHAR(4); 
```

Cambiar el número máximo de caracteres permitidos

También queremos cambiar el número máximo de caracteres permitidos en la columna de colores de la tabla de coches.

Utilice la misma sintaxis que la anterior, utilice la declaración ALTER COLUMN y la palabra clave TYPE seguida del nuevo tipo de datos:

```sql
ALTER TABLE cars
ALTER COLUMN color TYPE VARCHAR(30); 
```

La sentencia ALTER TABLE

Para eliminar una columna de una tabla, tenemos que utilizar la sentencia ALTER TABLE.

La sentencia ALTER TABLE se utiliza para añadir, eliminar o modificar columnas en una tabla existente.

La sentencia ALTER TABLE también se utiliza para añadir y eliminar varias restricciones en una tabla existente.


### DROP COLUMN

Queremos eliminar la columna denominada color de la tabla cars.

Para eliminar una columna, utilice la sentencia DROP COLUMN:

```sql
ALTER TABLE cars
DROP COLUMN color; 
```

### La sentencia DELETE

La sentencia DELETE se utiliza para eliminar registros existentes en una tabla.

Nota: ¡Tenga cuidado al eliminar registros de una tabla! Observe la cláusula WHERE en la sentencia DELETE. La cláusula WHERE especifica qué registro(s) se deben eliminar.

Si omite la cláusula WHERE,
se eliminarán todos los registros de la tabla.

```sql
DELETE FROM cars
WHERE brand = 'Volvo'; 
```

Eliminar todos los registros

Es posible eliminar todas las filas de una tabla sin eliminar la tabla. Esto significa que la estructura, los atributos y los índices de la tabla permanecerán intactos.

La siguiente declaración SQL elimina todas las filas de la tabla cars, sin eliminar la tabla:

```sql
 DELETE FROM cars; 
```

### TRUNCATE TABLE

Como omitimos la cláusula WHERE en la declaración DELETE anterior, se eliminarán todos los registros de la tabla cars.

Se habría logrado lo mismo utilizando la declaración TRUNCATE TABLE:

```sql
TRUNCATE TABLE cars; 
```

**La sentencia DROP TABLE**

Se utiliza para eliminar una tabla existente en una base de datos.

Nota: tenga cuidado antes de eliminar una tabla. Si elimina una tabla, perderá toda la información almacenada en ella.

La siguiente sentencia SQL elimina la tabla existente:

```sql
 DROP TABLE cars; 
```

### Operadores

**Operadores en la cláusula WHERE**

Podemos operar con diferentes operadores en la cláusula WHERE:

|Operadores|Sinificado|
|---|---|
|=| Igual a|
|<|Menor que|
|>| Mayor que|
|<=| Menor o igual que|
|>=| Mayor o igual que|
|<>| No igual a|
|!=| No igual a|
|LIKE| Comprueba si un valor coincide con un patrón (distingue entre mayúsculas y minúsculas)|
|ILIKE| Comprueba si un valor coincide con un patrón (no distingue entre mayúsculas y minúsculas)|
|AND| AND lógico|
|OR| OR lógico|
|IN| Comprueba si un valor está entre un rango de valores|
|BETWEEN| Comprueba si un valor está entre un rango de valores|
|IS NULL| Comprueba si un valor es NULL|
|NOT| Genera un resultado negativo, p. ej. NOT LIKE, NOT IN, NOT BETWEEN|




### Inicia y habilita el servicio:

**Iniciar:**

```Bash
sudo systemctl start postgresql
```

**Detener:**

```Bash
sudo systemctl stop postgresql
```

**Reiniciar:**

```Bash
sudo systemctl restart postgresql
```

**Ver estado:**

```Bash
sudo systemctl status postgresql
```

**Habilitar inicio automático:**

```Bash
sudo systemctl enable postgresql
```

**Deshabilitar inicio automático:**

```Bash
sudo systemctl disable postgresql
```

## [[Tutopostgresql]]



https://www.w3schools.com/postgresql/index.php
