#### **SQL** Strutured Query Language (Lenguaje de consulta esructurada)

---
#### **SGBD** Sistema Gestor de Base de Datos 

### BD Relacionales
##### **[[MariaDB]]**

##### **[[PostgreSQL]]**

##### **[[SQLite]]**


### BD No Relacionales
##### **[[MongoDB]]**

---
#### **RDBMS** Relational DataBase Management System

#Comentarios 

```sql
-- comentarios en una linea
```
```sql
/* 
comentarios en varias lineas 
*/  
```

Strutured Query Language (Lenguaje de consulta esructurada)

## Tipos de senctencias SQL

| Tipo               | Sentencia                                                                                                                   | Accion                                                                                                                                                                                                                                                                |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <br><br>DML        | Manipulacion de datos<br>**- SELCET**<br>**- INSERT**<br>**-UPDATE**<br>**-DELETE**                                         | <br>**-** Recupera datos de una o varias tablas.<br>**-** Inserta nuevas filas en una tabla.<br>**-** Actualiza datos existentes en una tabla.<br>**-** Elimina filas de una tabla.                                                                                   |
| <br><br><br>DDL    | Definicion de datos<br>**- Create** <br>(Database, table, view)<br>**- ALTER**<br>**- DROP**                                | <br>**-** Crea un objeto (database, table, view, etc).<br><br>**-** Modifica un objeto (database, table, view, etc).<br>**-** Elimina un objeto (database, table, view, etc).<br>                                                                                     |
| <br><br><br>DCL    | Control de acceso<br>**- GRANT**<br>**- REVOKE**<br>Control de transaccion<br>**- START**<br>**- COMMIT**<br>**- ROLLBACK** | <br>**-** Asigna permisos/privilegios de acceso a un objeto.<br>**-** Revoca/quita permisos/privilegios de acceso a un objeto.<br><br>**-**  Inica una transaccion.<br>**-** Confirma el resultado de una transacción<br>**-** Deshaceel resultado de una transaccion |
| <br><br><br>PL-SQL | Programacion SQL<br>**- DECLARE**<br><br>**- OPEN**<br>**- FETCH**<br>**- CLOSE**                                           | <br>**-** Crea un cursor a partir de los resultados de una consulta.<br>**-** Abre un cursor para recuperar los resultados.<br>**-** Recuperauna fila desde los resultados.<br>**-** Cerra un cursor.<br>                                                             |
|                    | **- Etc**                                                                                                                   | **-** Incluye sentencias de control de flujo  (if, Case, While, etc. ).                                                                                                                                                                                               |


### **DDL**  **L**enguaje de **D**efinicion de **D**atos en esta parte se encuetra el **CRUD** (create, retrieve, update, delete)
- CREATE
- ALTER
- DROP
- RENAME

Lenguaje de Definición de Datos o DDL, que es la parte de SQL que realiza
la función de definición de datos del sistema gestor de bases de datos.


### **DML**  **L**enguaje de **M**anipulacion de **D**atos
- SELECT  recupera datos de una o varias tablas
- INSERT  inserta nuevas filas en una tabla
- UPDATE  actualiza datos exitentes en una tabla
- DELETE  elimina filas de una tabla

Lenguaje de Manipulación de Datos o DML, que incluye las instrucciones
para consultar la base de datos y modificar valores de datos.

### **DCL**  **L**enguaje de **C**ontrol de **D**atos
- GRAND
- REVOKE

Lenguaje de Control de Datos o DCL, que incluye una serie de comandos
que ayudan a controlar el acceso a los datos.


### **TCL**  **L**enguaje **C**ontrol de **T**ransacciones
- COMMIT
- ROLLBACK

Control de Transacciones o TCL, que es un lenguaje de
programación para el control de transacciones en una base de datos.

| tipo de lenguaje | sentencia  | accion                                  |
| ---------------- | ---------- | --------------------------------------- |
|                  | **SELECT** | Recupera datos de una o varias salidas  |
| **DML**          | **INSERT** | Inserta nuevas filas en una tabla       |
|                  | **UPDATE** | Actualiza datos existentes en una tabla |
|                  | **DELETE** | Elinina filas de na tabla               |


| tipo de lenguaje | sentencia| accion |
|--- | --- | --- |
|| **CREATE** (database, table, view, etc) | Crea un objeto (database, view, etc) |
|**DDL**| **ALERT** | Modifica un objeto (Dtabase, table, viw, etc) |
|| **DROP** | Elimina un objeto (database, table, view, etc) |


| tipo de lenguaje | sentencia| accion |
|--- | --- | --- |
|| Control de acceso | |
|| **GRANT** | Asigna permisos\/privilegios de acceso a un objeto |
|| **REVOKE** | Revoca\/quita permisos\/privilegios de acceso aun objeto |
| **DCL** | Control de transaccion | | 
|| **START**| Inicia transacciones |
|| **COMMIT** | Confirma el resultado de una transaccion | 
|| **ROLLBACK** | Deshace el resultado de una transaccion |



| Sentencias             | Accion                                                               |
| ---------------------- | -------------------------------------------------------------------- |
| **SELECT**             | selecciona la columna                                                |
| **SELECT\***           | (*) hace referencia a todas las columnas                             |
| **SELECT** **DISTINC** | no repite el registro con el mismo valor de columna SELEC DISTINC    |
| **FROM**               | ndica la tabla o tablas a consultar tambien admite alias             |
| **WHERE**              | para filtrar registros (filas) se utilizan operadores de comparacion |
| **AS**                 | renombra las columnas (as: como) es como un alias                    |
| **ORDER BY**           | sirve para ordenar las consultas [ASC] ascendente [DESC] descendente |
| **DESCRIBE**           | muestra la estructura de la tabla                                    |

## Operadores aritmeticos
| Operadores aritmeticos |          |
| ---------------------- | -------- |
| **\+**                 | Suma     |
| **\-**                 | Resta    |
| **\***                 | Producto |
| **/**                  | División |
| **\%**                 | Módulo   |
| **\=**                 | Igualdad |
 
## Operadores de comparacion


| Operadotres de comparacion   |                                                 |
| ---------------------------- | ----------------------------------------------- |
| **\=**                       | Igual que                                       |
| **\<>**                      | Distinto de                                     |
| **\>**                       | Mayor que                                       |
| **\<**                       | Menor que                                       |
| **\>=**                      | Mayor o igual que                               |
| **\<=**                      | Menor o igual que                               |
| **BETWEEN**<br>**...AND...** | Entre dos valores (ambos inclusive)             |
| **IN(set)**                  | Se corresponde con cualquier valor de una lista |
| **LIKE**                     | Se corresponde con un patron de caracteres      |
| **IS NULL**                  | Es un valor nulo                                |

## Operadores logicos

| Operadores logicos |                                             |
| ------------------ | ------------------------------------------- |
| **and**            | TRUE si ambas condiciones son verdaderas    |
| **or**             | TRUE si al menos una condicion es verdadera |
| **not**            | TRUE si la condicion es falsa               |

## Operadores de caractares

LIKE este operador nos permite utilizar los siguientes caracteres especiales en las cadenas de comparacion.

| Caracter | Accion                                                           |
| -------- | ---------------------------------------------------------------- |
| **%**    | Permite seleccionar cualquier cadena de caracteres (cero o mas). |
| **\_**   | permite seleccionar cualquier caracter (solo uno).               |


ejemplo:
```sql
SELECT nombre, apellidos
FROM clientes
WHERE nombre LIKE ‘P%’ or ’J%’;
```

## Reglas de proriedades

| Prioriedad | Operador                         |
| ---------- | -------------------------------- |
| 1          | operaodores aritmeticos          |
| 2          | operadores de concatenacion      |
| 3          | operadores de concatenacion      |
| 4          | is \[NOT\] NULL, LIKE,\[NOT\] IN |
| 5          | \[NOT\] BETWEEN                  |
| 6          | distinto                         |
| 7          | condicion logica NOT             |
| 8          | condicion logica AND             |
| 9          | condicion logica OR              |

## Funciones de agrupamiento

| Funciones     | Descripcion                                                                                                                           |     |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------- | --- |
| **AVG**       | Valor medio de n, se ignoran los valores nulos (proemdio).                                                                            |     |
| <br>**CONUT** | Numero de filas (cuenta todas las filas seleccionadas que utilizan \* , incluidas las duplicadas y las que contienen valores nulos ). |     |
| **MAX**       | Valor maximo, se ignoran los vlaores nulos.                                                                                           |     |
| **MIN**       | Valor minimo, se ignoran los valores nulos.                                                                                           |     |
| **SUM**       | Suma los valores de n, se ignoran los valores nulos.                                                                                  |     |


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

---
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


