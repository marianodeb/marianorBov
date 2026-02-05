Estructura de las tablas:

La estructura de tus tablas dependerá de la profundidad con la que quieras analizar tus datos y qué tipo de reportes deseas generar. A continuación, te propongo una estructura básica que puedes adaptar a tus necesidades:

Tabla: Hortalizas

    id: Identificador único de la hortaliza.
    nombre_comun: Nombre común de la hortaliza (ej: Zapallito Veronez).
    nombre_cientifico: Nombre científico (opcional).
    tipo: Anual, perenne, bianual.
    variedad: Variedad específica (ej: Tradicional, Rústica).

Tabla: Cosechas

    id: Identificador único de la cosecha.
    fecha: Fecha de la cosecha.
    hortaliza_id: Clave foránea que relaciona la cosecha con la hortaliza.
    cantidad: Cantidad cosechada.
    peso_total: Peso total de la cosecha.
    peso_promedio: Peso promedio por unidad.
    condiciones_climaticas: Descripción de las condiciones climáticas.
    observaciones: Notas adicionales.

Tabla: CondicionesClimaticas

    id: Identificador único de la condición climática.
    fecha: Fecha de la medición.
    temperatura_max: Temperatura máxima.
    temperatura_min: Temperatura mínima.
    lluvia: Cantidad de lluvia.
    humedad: Humedad relativa.

Relaciones entre tablas:

    La tabla Cosechas se relaciona con la tabla Hortalizas a través del campo hortaliza_id. Esto permite conocer qué hortaliza se cosechó en cada fecha.
    La tabla Cosechas podría relacionarse con la tabla CondicionesClimaticas si deseas analizar cómo las condiciones climáticas afectan el rendimiento de tus cultivos.

¿Por qué relacionar las tablas?

    Organización: Evita la redundancia de datos y facilita la gestión de la información.
    Flexibilidad: Permite realizar consultas más complejas y obtener información detallada sobre tus cultivos.
    Integridad de los datos: Garantiza la consistencia de los datos al evitar valores duplicados o inconsistentes.
    
    
    
    Hortalizas:

    id_hortaliza (clave primaria)
    nombre_comun
    nombre_cientifico
    variedad
    ciclo_de_vida (anual, bianual, perenne)

Cosechas:

    id_cosecha (clave primaria)
    id_hortaliza (clave foránea, relacionada con la tabla Hortalizas)
    fecha_siembra
    fecha_cosecha
    cantidad
    peso_total
    condiciones_climaticas
    observaciones

Condiciones_climaticas:

    id_condicion (clave primaria)
    fecha
    temperatura_maxima
    temperatura_minima
    precipitacion
    humedad

Plagas_enfermedades:

    id_plaga (clave primaria)
    nombre
    descripcion
    tratamiento

Tratamientos:

    id_tratamiento (clave primaria)
    nombre
    fecha_aplicacion
    id_cosecha (clave foránea, relacionada con la tabla Cosechas)
    
    ¿Cómo relacionar las tablas?

Las claves foráneas son como puentes entre las tablas. Por ejemplo, en la tabla "Cosechas", la columna "id_hortaliza" es una clave foránea que se relaciona con la columna "id_hortaliza" de la tabla "Hortalizas". Esto significa que cada cosecha está asociada a una hortaliza específica.

¿Cómo crear las tablas?

La forma más común de crear tablas es utilizando el lenguaje SQL (Structured Query Language). Cada base de datos tiene su propia implementación de SQL, pero la sintaxis básica es similar. Por ejemplo, para crear la tabla "Hortalizas" en MySQL, usarías un comando como este:

```SQL

CREATE TABLE hortalizas (
  id_hortaliza INT PRIMARY KEY AUTO_INCREMENT,
  nombre_comun VARCHAR(50),
  nombre_cientifico VARCHAR(100),
  variedad VARCHAR(50),
  ciclo_de_vida ENUM('anual', 'bianual', 'perenne')
);
```


¿Puedo crear la base de datos ahora y usarla más tarde en la aplicación?

¡Absolutamente! De hecho, es una buena práctica separar la creación y el diseño de la base de datos del desarrollo de la aplicación. Puedes crear tu base de datos, poblarla con datos iniciales y luego conectar tu aplicación a ella.






¿Qué es una clave foránea?

Una clave foránea es una columna (o conjunto de columnas) en una tabla que hace referencia a la clave primaria de otra tabla. 1  Esta relación establece un vínculo entre los datos de ambas tablas, asegurando la integridad referencial de la base de datos.   

Ejemplo con diagramas:

Imagina que tenemos dos tablas: "Hortalizas" y "Cosechas". Una hortaliza puede tener múltiples cosechas, por lo que estableceremos una relación entre ambas tablas.

    Hortalizas:
        id_hortaliza (clave primaria)
        nombre
    Cosechas:
        id_cosecha (clave primaria)
        id_hortaliza (clave foránea, referencia a id_hortaliza en la tabla Hortalizas)
        fecha
        cantidad

Sintaxis SQL para crear la clave foránea:


    Hortalizas:
        id_hortaliza (clave primaria)
        nombre
    Cosechas:
        id_cosecha (clave primaria)
        id_hortaliza (clave foránea, referencia a id_hortaliza en la tabla Hortalizas)
        fecha
        cantidad

Sintaxis SQL para crear la clave foránea:

```SQL

CREATE TABLE hortalizas (
  id_hortaliza INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(50)
);

CREATE TABLE cosechas (
  id_cosecha INT PRIMARY KEY AUTO_INCREMENT,
  id_hortaliza INT,
  fecha DATE,
  cantidad INT,
  FOREIGN KEY (id_hortaliza) REFERENCES hortalizas(id_hortaliza)
);
```
Explicación de la sintaxis SQL:

    CREATE TABLE: Crea una nueva tabla.
    PRIMARY KEY: Define la columna como clave primaria, asegurando que los valores sean únicos y no nulos.
    AUTO_INCREMENT: Incrementa automáticamente el valor de la clave primaria cada vez que se inserta un nuevo registro.
    FOREIGN KEY: Define una columna como clave foránea, estableciendo una relación con otra tabla.
    REFERENCES: Especifica la tabla y la columna a la que hace referencia la clave foránea.

¿Qué hay que tener en cuenta al crear claves foráneas?

    Integridad referencial: Los valores de la clave foránea deben existir en la tabla referenciada.
    Cascada: Puedes configurar acciones en cascada (DELETE, UPDATE) para que cuando se elimine o actualice un registro en la tabla principal, se actualicen o eliminen automáticamente los registros relacionados en la tabla secundaria.
    Índice: Crear un índice en la columna de la clave foránea mejora el rendimiento de las consultas.

Ejemplo con cascada DELETE:


```SQL
CREATE TABLE cosechas (
  id_cosecha INT PRIMARY KEY AUTO_INCREMENT,
  id_hortaliza INT,
  fecha DATE,
  cantidad INT,
  FOREIGN KEY (id_hortaliza) REFERENCES hortalizas(id_hortaliza) ON DELETE CASCADE
);
```
Con esta configuración, si eliminas una hortaliza, todas las cosechas asociadas a esa hortaliza también se eliminarán automáticamente.

En resumen:

Las claves foráneas son fundamentales para establecer relaciones entre tablas y garantizar la integridad de los datos en una base de datos. Al comprender cómo crear y utilizar claves foráneas, podrás diseñar bases de datos más robustas y eficientes para tus proyectos.


---
 mis tablas
---
Tabla: Hortalizas

    id: Identificador único de la hortaliza.
    nombre_comun: Nombre común de la hortaliza (ej: Zapallito Veronez).
    tipo: Anual, perenne, bianual.
    variedad: Variedad específica (ej: Tradicional, Rústica).

Tabla: Cosechas

    id: Identificador único de la cosecha.
    fecha: Fecha de la cosecha.
    hortaliza_id: Clave foránea que relaciona la cosecha con la hortaliza.
    cantidad: Cantidad cosechada.
    peso_total: Peso total de la cosecha.
    peso_promedio: Peso promedio por unidad.
    observaciones: Notas adicionales.

Tabla: CondicionesClimaticas

    id: Identificador único de la condición climática.
    fecha: Fecha de la medición.
    temperatura_max: Temperatura máxima.
    temperatura_min: Temperatura mínima.
    lluvia: Cantidad de lluvia.

    
    
    
---

### La sentencia SQL INSERT INTO

 INSERT INTO se utiliza para insertar nuevos registros en una tabla.
Sintaxis de INSERT INTO

La sentencia INSERT INTO se puede escribir de dos formas:

1. Especifique los nombres de las columnas y los valores que se insertarán:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```


2. Si está agregando valores para todas las columnas de la tabla, no necesita especificar los nombres de las columnas en la consulta SQL. Sin embargo, asegúrese de que el orden de los valores sea el mismo que el de las columnas de la tabla. En este caso, la sintaxis de INSERT INTO sería la siguiente:
    
```
INSERT INTO table_name
VALUES (value1, value2, value3, ...); 
```

Ejemplo de INSERT INTO

La siguiente instrucción SQL inserta un nuevo registro en la tabla "Clientes":


```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

Insertar datos solo en columnas específicas

También es posible insertar datos solo en columnas específicas.

La siguiente declaración SQL insertará un nuevo registro, pero solo insertará datos en las columnas "CustomerName", "City" y "Country" (CustomerID se actualizará automáticamente):


```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

Insertar varias filas

También es posible insertar varias filas en una sola instrucción.

Para insertar varias filas de datos, utilizamos la misma instrucción INSERT INTO, pero con varios valores:


```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```

---

### La sentencia UPDATE 

La sentencia UPDATE se utiliza para modificar los registros existentes en una tabla.
Sintaxis de UPDATE

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition; 
```
Nota: ¡Tenga cuidado al actualizar registros en una tabla! Observe la cláusula WHERE en la declaración UPDATE. La cláusula WHERE especifica qué registro(s) se deben actualizar. Si omite la cláusula WHERE, se actualizarán todos los registros de la tabla.

Tabla UPDATE

La siguiente instrucción SQL actualiza el primer cliente (CustomerID = 1) con una nueva persona de contacto y una nueva ciudad.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```
ACTUALIZAR varios registros

La cláusula WHERE es la que determina cuántos registros se actualizarán.

La siguiente instrucción SQL actualizará el nombre de contacto a "Juan" para todos los registros donde el país sea "México":

```sql
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';
```
Tenga cuidado al actualizar registros. Si omite la cláusula WHERE, se actualizarán TODOS los registros.


```sql

```

La selección de la tabla "Clientes" ahora se verá así:

 aca va la imagen "sentencia update.png"
 
---
 
### Sentencia DELETE de SQL

La sentencia DELETE se utiliza para eliminar registros existentes en una tabla.

Sintaxis de DELETE

```sql
DELETE FROM table_name WHERE condition;
```

Nota: ¡Tenga cuidado al eliminar registros de una tabla! Observe la cláusula WHERE en la declaración DELETE. La cláusula WHERE especifica qué registro(s) se deben eliminar. Si omite la cláusula WHERE, se eliminarán todos los registros de la tabla.
La clausula WHERE  es igual importante como en la sentencia UPDATE


La siguiente instrucción SQL elimina el cliente "Alfreds Futterkiste" de la tabla "Clientes":

```sql
 DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste'; 
```

Eliminar todos los registros

Es posible eliminar todas las filas de una tabla sin eliminar la tabla en sí. Esto significa que la estructura, los atributos y los índices de la tabla permanecerán intactos:

```sql
DELETE FROM table_name;
```

La siguiente declaración SQL elimina todas las filas de la tabla "Customers" (clientes), sin eliminar la tabla:

```sql
DELETE FROM Customers; 
```

### Eliminar una tabla

Para eliminar la tabla por completo, utilice la instrucción DROP TABLE:

```sql
DROP TABLE Customers; 
```
---

### Sentencia SQL CREATE DATABASE

La sentencia CREATE DATABASE de SQL

La sentencia CREATE DATABASE se utiliza para crear una nueva base de datos SQL.

Sintaxis
    
```sql
CREATE DATABASE databasename;
```

Ejemplo de CREAR BASE DE DATOS

La siguiente instrucción SQL crea una base de datos denominada "testDB":

```sql
CREATE DATABASE testDB;
```

Consejo: Asegúrese de tener privilegios de administrador antes de crear cualquier base de datos. Una vez creada una base de datos, puede comprobarla en la lista de bases de datos con el siguiente comando SQL: SHOW DATABASES;

---

### La sentencia BACKUP DATABASE de SQL

La sentencia BACKUP DATABASE se utiliza en SQL Server para crear una copia de seguridad completa de una base de datos SQL existente.
Sintaxis

```sql
BACKUP DATABASE databasename
TO DISK = 'filepath'; 
```


La instrucción SQL BACKUP WITH DIFFERENTIAL

Una copia de seguridad diferencial solo realiza una copia de seguridad de las partes de la base de datos que han cambiado desde la última copia de seguridad completa de la base de datos.
Sintaxis

```sql
BACKUP DATABASE databasename
TO DISK = 'filepath'
WITH DIFFERENTIAL; 
```

Ejemplo de COPIA DE SEGURIDAD DE LA BASE DE DATOS

La siguiente instrucción SQL crea una copia de seguridad completa de la base de datos existente "testDB" en el disco D:

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak';
```

Consejo: Realice siempre una copia de seguridad de la base de datos en una unidad distinta a la de la base de datos real. De este modo, si se produce un fallo en el disco, no perderá el archivo de copia de seguridad junto con la base de datos.

Ejemplo de COPIA DE SEGURIDAD DIFERENCIAL

La siguiente sentencia SQL crea una copia de seguridad diferencial de la base de datos "testDB":

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak'
WITH DIFFERENTIAL;
```
Consejo: una copia de seguridad diferencial reduce el tiempo de copia de seguridad (ya que solo se respaldan los cambios).

---

### La sentencia CREATE TABLE de SQL

La sentencia CREATE TABLE se utiliza para crear una nueva tabla en una base de datos.
Sintaxis

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
); 
```

Los parámetros de columna especifican los nombres de las columnas de la tabla.

El parámetro de tipo de datos especifica el tipo de datos que puede contener la columna (por ejemplo, varchar, entero, fecha, etc.).

Sugerencia: Para obtener una descripción general de los tipos de datos disponibles, consulte nuestra Referencia de tipos de datos completa.


Ejemplo de CREATE TABLE de SQL

El siguiente ejemplo crea una tabla denominada "Persons" que contiene cinco columnas: PersonID, LastName, FirstName, Address y City:

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

La columna PersonID es de tipo int y contendrá un número entero.

Las columnas LastName, FirstName, Address y City son de tipo varchar y contendrán caracteres, y la longitud máxima para estos campos es de 255 caracteres.

La tabla "Persons" vacía ahora se verá así:

aca va la imagen "creando_tabla_vaciapng"

Consejo: La tabla vacía "Personas" ahora se puede llenar con datos con la instrucción SQL INSERT INTO.


### Crear una tabla a partir de otra tabla

También se puede crear una copia de una tabla existente mediante CREATE TABLE.

La nueva tabla obtiene las mismas definiciones de columnas. Se pueden seleccionar todas las columnas o columnas específicas.

Si crea una nueva tabla a partir de una tabla existente, la nueva tabla se completará con los valores existentes de la tabla anterior.
Sintaxis

```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....; 
```

El siguiente SQL crea una nueva tabla llamada "TestTable" (que es una copia de la tabla "Customers"):

```sql
CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers; 
```
---

Ejemplo de SQL DROP TABLE

La siguiente instrucción SQL elimina la tabla existente "Shippers":

```sql
 DROP TABLE Shippers; 
```

SQL TRUNCATE TABLE

La sentencia TRUNCATE TABLE se utiliza para eliminar los datos dentro de una tabla, pero no la tabla en sí.
Sintaxis

```sql
TRUNCATE TABLE table_name;
```



```sql

```
