

https://www.youtube.com/watch?v=1HEHNF7GVw8&list=PLRCCp0F8ypiB4kgFvszGIMtJ6vrXHT5kh&index=9


Crear un usuario administrador 

Por defecto teneemos un usuario super administrador qeu es el usuario postgres

```bash
minimini@raspby:$sudo su - postgres
```

sudo: contraseña para minimini


```bash
postgres@raspby:~$whoami
```
Resultaod: posrgres

```bash
pwd
```
Resultado /var/lib/postgresql 

Creamos un usuario para que no seas el usuario postgres y tener todos los privilegios

```bash
createuser rogelin -s -P
```
Pedira que le demos una contraseña para el nuevo usuario rogelin
Luego hay que configurar los permisos en los siguientes archivos:
 **/etc/postgres/15/main/pg_hba.conf** 

```
#type    DATABASE    USER    ADDRESS    MEHOD

local     all        all                password



#el metodo peer significa qeu puede acceder sin contraseña
```
Despues de cada configuracion se debe reiniciar (restart) o recargar (reload) con systemctl

```bash
systemctl reload postgresql.service
```
ahora luego de configurar el archivo prodremos ingresar como usuario rogeli

```bash
psql template -U rogelin
```

Para ver todos los comandos ejecutamos:

```bash
psql --help
```
ejemplo del comando -l que lista las bases de datos del ususario rogelin:

```bash
psql -l -U rogelin
```

Ver algunas funciones del comando createdb con help como -T que copia o crea el modelo de una tabla ya creada.

```bash
createdb --help
```

Entrar a bases de datos con psql nombre_bd -U nombre_usuario

```bash
psql based1 -U rogelin
```

Al ingresar a una bd el promp cambia con el nombre de la db seguido de =# ejemplo:
nombre_based1=#
Estando en una bd se puede crear otra bd esto le pertenecera al usuario de la primer db.
Para entra a la db creada se debe salir de la que esta para luego ingresar a la db creada.
Ejemplo:

Creamos la db based2

```sql
based1=#create database based2;
```

Ingresamos a based2 con el usuario rogelin, usuario que la creo

```bash
psql based2 -U rogelin
```
Una vez dentro de la db based2 el promp ya nos mostrara que estamos en la db based2

```sql
based2=#
```

Crear Tabalas


Para listar tablas utilizamos el siguiente comando based1=#\d

```sql
\d
```

Crearemos una tabala llamada "tablin1" con 3 campos: 
(campo1 int, campo2 varchar(100), camopo3 date)

```sql
CREATE TABLE tablin1 (campo1 int, campo2 varchar(100), camopo3 date);
```

Para ver la estructura y mas informacion utilizaremos los siguientes comantos:

```sql
\d+
```

```sql
\d tablin1
```

Muestra mas informacion que los anteriores comandos

```sql
\d+ tablin1
```

Probas las 4 maneras y verificar las diferencias que dan 

```sql
\d

\d+

\d tablin1

\d+ tablin1
```

Funcion que devuelve la hora

```sql
select now();
```


#### Sentencias DML Iinsert Select Update Delete

```sql
INSERT INTO nombre_tabla (campo1, campo2 ...) values (valor1, valor2)
```

Agregar columna a la tabla 

```sql
INSERT TABLE nombre_tabla ADD COLUMN campo4 float;
```
Observamos los cambios con los siguientes comandos:

```sql
\d nombre_tabla
```

```sql
SELECT * FROM nombre_tabla;
```

Insertando mas de un dato

```sql
INSERT TO nombre_tabla (campo1, campo2) VALUES (100, 'Bruno'), (13, 'Julia'); 
```

#### Agregando columna autoincrementable

```sql
ALTER TABLE nombre_tabla ADD COLUMN nombre_columna SERIAL;
```

Formula de paginacion de registros con OFFSET Y LIMIT

segundos ((2-1)\*5) terceros 5 ((3-1)\*5) 

ejemplo:

```sql
SELECT FROM nombre_tabla OFFSET 0 LIMIT 5;

```

```sql
SELECT FROM nombre_tabla OFFSET ((2-1)*5) LIMIT 5;

```

```sql
SELECT FROM nombre_tabla OFFSET ((3-1)*5) LIMIT 5;
```

Renombrar tabla

```sql
ALTER TABLE nombre_tabla RENAME TO nombre_nuevo;
```

## Creando PK Primary Key FK Foreign Key

Crear tabla con pirmary key

```sql
CREATE TABLE nombre_tabla (id INT PRIMARY KEY, nombre varchar(100));
```

Crear tabla con primary key autoincrementable

```sql
CREATE TABLE nombre_tabla (id SERIAL PRIMARY KEY, nombre VARCHAR(200));
```

Ingresar valores con primary key autoincrementable

```sql
INSERT TO nombre_tabla (nombre) VALUES(Osvaldito);
```

Creando tablas con columnas con mas de un contador

```sql
CREATE TABLA tabliya (id1 SERIAL PRIMARY KEY, id2 SERIAL, id3 SERIAL, nombre VARCHAR(100));
```

Ingreamos datos para ver como responden

```sql
INSERT TO tabliya (nombre) VALUES ('Charlys')
```

Modificando el contador de una columna

```sql
SELECT SETVAL('tabliya_id3_seq',100);
```

Esto hara que la columna id3, desde este momento siga o arranque desde el numero 100

```sql
INSERT TO tabliya (nombre) VALUES('Oto');
```

Creando tabla con FOREIGN KEY

Donde TABLA t1 se realciona con t3

```sql
CREATE TABLE t1 (id SERIAL PRIMARY KEY, nombre VARCHAR(100));
```

Agregamos algunos nombres a t1

```sql
INSERTE INTO t1 (nombre) VALUES ('Oto'), ('Tucho'), ('Body'), ('Ozzy'), '(Peke')
```

Miramos como quedo la tabla t1 con 

```sql
SELECT * FROM t1
```

```sql
CREATE TABLE t3 (nuevoid SERIAL PRIMARY KEY, id INTEGER REFERENCES t1(id), sueldos FLOAT);
```

Veamos como quedo la estructura de la tabla t3 y tabla t1

```sql
\d t3
```

```sql
\d t1
```

Igresando datos en la Tabla t3 

```sql
INSERT INTO t1 (id, sueldo) VALUES (1, 1000000), (2, 1100000), (3, 1300000), (4, 1250000), (5, 1150000);
```
 
Veamos como quedo  la tabla t3 y t1

```sql
SELECT * FROM t3
```

```sql
SELECT * FROM t1
```

Para eliminar datos de una tabla que esta relacionada se debe hacer con el comando: **TRUNCATE nombre_tabla CASCADE**
De lo contrario no se pueden eliminar datos. CASCADE hace una eliminacion de los datos de las tablas relacionadas. Esto queire decir que se perderan datos de todas las tablas que esten relacionadas.

### Cosulta JOINS

Crearemo 2 tablas nuevas para relacionarlas y luego realizar consultas con JOINS

```sql
CREATE TABLE tableta1 (id SERIAL PRIMARY KEY, nombre VARCHAR(100));
```

```sql
CREATE TABLE tableta2 (nuid SERIAL PRIMARY KEY, id INTERGER REFERENCES tableta1(id), sueldos FLOAT);
```

```sql
\d tableta1
```

```sql
\d tableta2
```

Cargamos datos 


```sql
INSERT INTO tableta1 (nombre) VALUES ('Thor'), ('Capitan'), ('Logan'), ('Optimus'), ('Frank');
```

```sql
INSERT INTO tableta2 (id, sueldo) VALUES (1, 1000), (2, 1100), (3, 2000), (4, 2100), (null, 4000);
```

Consulata con JOINS y alias como tableta1 A y tableta2 B
Esto mostrara solo los campos que esten en ambos conjuntos

```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A JOIN tableta2 B ON a.id = b.id;
```


Mostrara todo lo de la tabla A auque no tenga datos en la table B

```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A LEFT JOIN tableta2 B ON a.id = b.id;
```

RIGHY JOIN hara lo contrario de LEF JOINS 


```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A RIGHT JOIN tableta2 B ON a.id = b.id;
```

Para mostrar los empleados sin sueldos:

```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A LEFT JOIN tableta2 B ON a.id = b.id WHERE b.id IS NULL;
```

Para mostrar los sueldos sin empleado

```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A RIGHT JOIN tableta2 B ON a.id = b.id WHERE a.id IS NULL;
```

Para cruzar todos los datos tengan o no datos en ambas tablas:

```sql
SELECT a.id, a.nombre. b.sueldo FROM tableta1 A FULL OUTER JOIN tableta2 B ON a.id = b.id;
```

Para mostrar lo que estan en cada tabla y no comparten datos o no se tienen datos en una u otra.

```sql
SELECT a.id, a.nombre, b.sueldo FROM tableta1 A FULL OUTER JOIN tableta2 B ON a.id = b.id WHERE a.id IS NULL OR b.id IS NULL;
```

Otras consultas

```sql
SELECT * FROM tableta2 WHERE id IN (SELECT id FROM tableta1);
```

```sql
SELECT * FROM tableta2 WHERE id IN (SELECT id FROM tableta1 WHERE sueldo >= 1000);
```


```sql
SELECT * FROM tableta2 WHERE nueid IN (3, 4) AND id IN (SELECT id FROM tableta1 WHERE sueldo >= 2000);
```

Crearemos una tabla llamada tableta3 que copiara las columna de tableta1

```sql
CREATE TABLE tableta3 AS SELECT * FROM tableta1
```
Uniremos ambas tablas para ver como imprime los datos
Si los datos se repiten no los imprime.

```sql
SELECT id, nombre FROM tableta1 UNION SELECT id, nombre FROM tableta3
```
Insertaremos un nombre en la tableta3 para ver el resultado

```sql
INSERTE INTO tableta3 (id, nombre) VALUES (6, 'HULK');
```
Verificamos el resultado 

```sql
SELECT id, nombre FROM tableta1 UNION SELECT id, nombre FROM tableta3
```
Para ver todo auque este repetido

```sql
SELECT id, nombre FROM tableta1 UNION ALL SELECT id, nombre FROM tableta3;
```
Cambiar nombre a columnas

```sql
ALTER TABLE tableta3 RENAME id TO codigo;
```

```sql
ALTER TABLE tableta3 RENAME nombre TO alias;
```

```sql
SELECT id, nombre FROM tableta1 UNION ALL codigo, alias FROM tableta3;
```

Mostrar el origen de que tabla provienen los datos

```sql
SELECT 'tableta1', id as dni, nombre FROM tableta1 UNIO ALL SELECT 'tableta3', codigo, alias FROM tableta3 ORDER BY dni;
```

poner nombre a la columna del origen de los datos

```sql
SELECT 'tableta1' origen, id as dni, nombre FROM tableta1 UNIO ALL SELECT 'tableta3', codigo, alias FROM tableta3 ORDER BY dni;
```





Video 5
00:00:






















