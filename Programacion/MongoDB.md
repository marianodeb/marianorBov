
## Comandos básicos

### 1. Comprobación de la versión

El primer comando es para comprobar la versión instalada del servidor MongoDB y Mongo Shell. Ejecute este comando en el terminal en Linux o CMD prompt en windows.

`mongod --version`

```markup
C:\Windows\System32>mongod --version
versión db v4.2.7
versión git: 51d9fe12b5d19720e72dcd7db0f2f17dd9a19212
asignador: tcmalloc
módulos: ninguno
entorno de compilación:
    distmod: 2012plus
    distarch: x86_64
    target_arch: x86_64
```

También podemos utilizar el comando `mongod` para comprobar la versión, como se indica a continuación.

`mongo -version`

```markup
C:\Windows\System32>mongo --version
MongoDB shell versión v4.2.7
versión git: 51d9fe12b5d19720e72dcd7db0f2f17dd9a19212
asignador: tcmalloc
módulos: ninguno
entorno de compilación:
    distmod: 2012plus
    distarch: x86_64
    target_arch: x86_64
```

### 2. Listado de comandos de MongoDB

Este comando ayudará a los usuarios a averiguar todos los comandos que pueden utilizarse en MongoDB. Ejecute el comando en Mongo Shell.

`ayuda()`

```markup
mongo> db.help()
Métodos de DB:
        db.adminCommand(nameOrDocument) - cambia a la base de datos 'admin' y ejecuta el comando [simplemente llama a db.runCommand(...)]
        db.aggregate([pipeline], {options}) - realiza una agregación sin colección en esta base de datos; devuelve un cursor
        db.auth(nombreusuario, contraseña)
        db.cloneDatabase(fromhost) - sólo funcionará con MongoDB 4.0 e inferiores
        db.commandHelp(name) devuelve la ayuda del comando
        db.copyDatabase(fromdb, todb, fromhost) - sólo funcionará con MongoDB 4.0 e inferiores
        db.createCollection(name, {size: ..., capped: ..., max: ...})
        db.createUser(usuarioDocumento)
        db.createView(nombre, viewOn, [{$operador: {...}}, ...], {viewOptions})
        db.currentOp() muestra las operaciones actualmente en ejecución en la db
        db.dropBaseDeDatos(writeConcern)
        db.dropUser(nombredeusuario)
        db.eval() - obsoleto
        db.fsyncLock() vacía los datos en el disco y bloquea el servidor para las copias de seguridad
        db.fsyncUnlock() desbloquea el servidor tras un db.fsyncLock()
        db.getCollection(cname) igual que db['cname'] o db.cname
        db.getCollectionInfos([filter]) - devuelve una lista que contiene los nombres y opciones de las colecciones de la db
        db.getNombresDeColección()
        db.getLastError() - sólo devuelve la cadena msg del error
        db.getLastErrorObj() - devuelve el objeto de estado completo
        db.getLogComponents()
        db.getMongo() obtiene el objeto de conexión al servidor
        db.getMongo().setSlaveOk() permitir consultas en un servidor esclavo de replicación
        db.getName()
        db.getProfilingLevel() - obsoleto
        db.getProfilingStatus() - devuelve si el perfilado está activado y el umbral lento
        db.getReplicationInfo()
        db.getSiblingDB(name) obtiene la db en el mismo servidor que ésta
        db.getWriteConcern() - devuelve la preocupación de escritura utilizada para cualquier operación en esta db, heredada del objeto servidor si está establecida
        db.hostInfo() obtiene detalles sobre el host del servidor
        db.isMaster() comprueba el estado primario de la réplica
        db.killOp(opid) mata la operación actual en la db
        db.listCommands() lista todos los comandos de la db
        db.loadServerScripts() carga todos los scripts en db.system.js
        db.logout()
        db.printCollectionStats()
        db.printReplicationInfo()
        db.printShardingStatus()
        db.printSlaveReplicationInfo()
        db.resetError()
        db.runCommand(cmdObj) ejecuta un comando de la base de datos. si cmdObj es una cadena, la convierte en {cmdObj: 1}
        db.serverStatus()
        db.setLogLevel(level,<componente>)
        db.setProfilingLevel(level,slowms) 0=off 1=slow 2=all
        db.setVerboseShell(flag) mostrar información extra en la salida del shell
        db.setWriteConcern(<preocupaciónescritura doc>) - establece la preocupación de escritura para las escrituras en la db
        db.shutdownServer()
        db.stats()
        db.unsetWriteConcern(<preocupación por la escritura doc>) - anula la preocupación por la escritura para las escrituras en la base de datos
        db.version() versión actual del servidor
        db.watch() - abre un cursor de flujo de cambios para que una base de datos informe de todos los cambios en sus colecciones no pertenecientes al sistema.
```

### 3. Estadísticas de la BD

El comando siguiente dará detalles de las bases de datos junto con varias colecciones y parámetros relacionados de esa base de datos.

`db.stats()`

```markup
> db.stats()
{
        "db" : "test
        "colecciones" : 0
        "vistas" : 0
        "objetos" : 0
        "avgObjSize" : 0,
        "dataSize" : 0
        "storageSize" : 0
        "numExtents" : 0
        "indexes" : 0
        "indexSize" : 0
        "factorEscala" : 1
        "fileSize" : 0
        "fsUsedSize" : 0,
        "fsTotalSize" : 0,
        "ok" : 1
}
```

### 4. Crear nueva BD o cambiar a BD existente

Este simple comando ayuda a crear una nueva base de datos si no existe o ayuda a cambiar a la Base de Datos existente. En MongoDB «test» es la base de datos por defecto, por lo tanto los usuarios utilizan «**test**» DB una vez que Mongo Shell ha iniciado sesión.

`use Nombre_de_base_de_datos`

```markup
mongos> use geekFlareDB
cambiar a db geekFlareDB
```

### 5. Listado de todas las bases de datos

El comando mencionado se utiliza para listar todas las bases de datos.

`mostrar dbs`

```markup
mongo> show dbs
admin 0.000GB
config 0.002GB
geekFlareDB 0.000GB
prueba 0.000GB
```

### 6. Compruebe la BD actualmente en uso

Ejecute el siguiente comando en Mongo Shell para ver la BD actualmente en uso.

`db`

```markup
> db
GeekFlare
```

### 7. Soltar base de datos

El comando dado ayuda al usuario a soltar la base de datos requerida. Ejecute el comando en el cliente MongoDB. Por favor, asegúrese de seleccionar la Base de Datos antes de ejecutar el comando drop. De lo contrario, se eliminará la base de datos «**test**» por defecto.

`db.dropDatabase()`

Primero vamos a listar todas las bases de datos, cambiar a una de ellas y luego soltarla

```markup
> show dbs
admin 0.000GB
config 0.001GB
local 0.000GB
prueba 0.000GB
training 0.000GB
>
> usar formación
cambiar a db formación
>
> db.dropDatabase()
{ "dropped" : "training", "ok" : 1 }
```

### 8. Crear colección

Las colecciones son similares a las tablas en RDBMS.

El comando Crear una colección consta de dos parámetros. La colección consta de cero o más documentos. Por lo tanto, para crear una colección el parámetro obligatorio a utilizar en el comando es su nombre y [el parámetro opcional](https://docs.mongodb.com/manual/reference/method/db.createCollection/) puede incluir el nombre de los documentos, su tamaño y su índice.

- Creación de una colección simple.

**Sintaxis**: `db.createCollection(Nombre,Opciones)`

**Ejemplo**:

```markup
> usar geekFlare
cambiar a db geekFlare
>
> db.createCollection("geekFlareCollection")
{ "ok" : 1 }
>
> mostrar colecciones
geekFlareCollection
```

- Creación de una colección tapada

En ella se restringe el tamaño y el número de los documentos que se insertarán en la colección. La colección capada tiene una propiedad que permite eliminar los documentos más antiguos para dejar espacio a los nuevos documentos.

**Sintaxis**:

`db.createCollection(Nombre,{capped : true, size : sizeLimit , max : documentLimit })`

**Ejemplo:** Creemos una colección capada, insertemos un registro y recuperémoslo

```markup
> db.createCollection("Login",{capped:true,max:1,size:200})
{ "ok" : 1 }
>
> db.Login.insertMany([{"id":1,status: "Activo"},{"id":2,status: "Retenido"},{"id":3,status: "Pendiente"}])
{
        "acknowledged" : true
        "insertedIds" : [
                ObjectId("5edc5f4f411247725e75e52e"),
                ObjectId("5edc5f4f411247725e75e52f"),
                ObjectId("5edc5f4f411247725e75e530")
        ]
}
>
> db.Login.find()
{ "_id" : ObjectId("5edc5f4f411247725e75e530"), "id" : 3, "status" : "Pendiente" }
```

### 9. Drop Collection

El comando Drop Collection es similar al DDL en RDBMS. Adquiere bloqueos sobre la colección requerida hasta la ejecución del comando. Drop collection elimina la colección de la BD junto con todos los índices asociados a esa colección. Para soltar la colección se requiere el método drop().

Devuelve true en caso de drop exitoso y false en caso de algún error o si la BD no existe.

**Sintaxis**: `collectionName.drop()`

**Ejemplo**:

```markup
> use geekFlare
cambiado a db geekFlare
>
> mostrar colecciones
geekFlareCollection
>
> db.geekFlareCollection.drop()
true
>
> db.geekFlareCollection.drop()
false
```

## Operaciones CRUD relacionadas

### 10. Insertar documento en la colección

En MongoDB un documento es similar a una tupla en RDBMS.

Para crear un documento se utiliza el método insert `(` ). El método insert() crea uno o varios documentos en la colección existente. También crea la colección si no está presente en la BD. En MongoDB, el documento no tiene esquema, lo que significa que no hay restricción para insertar cualquier número de claves en un documento.

- **Inserción de un único registro**

Para insertar un registro se puede utilizar el método `insert()` o `insertOne()`.

**Sintaxis**: `collectionName.insertOne({documento})`

**Ejemplo**:

```markup
> db.geekFlareCollection.insertOne( {
 código: "P123", Cant: 200, estado: "Activo"
});
{
        "reconocido" : true
        "insertedId" : ObjectId("5ed309725429283aee2e134d")
}
```

- **Inserción de varios registros**

Para insertar varios registros, se pasará una lista de registros al método `insert()` o `insertMany()`.

**Sintaxis**:

`collectionName.insertMany([{documento1},{documento2},{documento3}....{documentn}])`

**Ejemplo**:

```markup
db.geekFlareCollection.insertMany([
... { código: "P1", Cant: 100, estado: "Activo"},
... { código: "P2", Cant: 200, estado: "Activo"},
... { código: "P3", Cant: 0, estado: "Dectivo"}
... ]);
{
        "reconocido" : true
        "insertIds" : [
                ObjectId("5edf7b4e18b2c26b9dfe8cac"),
                ObjectId("5edf7b4e18b2c26b9dfe8cad"),
                ObjectId("5edf7b4e18b2c26b9dfe8cae")
        ]
}
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5edf546fdfa12b33b7cb75b8"), "product" : "bottles", "Qty" : 100 }
{ "_id" : ObjectId("5edf546fdfa12b33b7cb75b9"), "product" : "pan", "Qty" : 20 }
{ "_id" : ObjectId("5edf546fdfa12b33b7cb75ba"), "producto" : "yogur", "Cantidad" : 30 }
{ "_id" : ObjectId("5edf7b4e18b2c26b9dfe8cac"), "code" : "P1", "Qty" : 100, "status" : "Activo" }
{ "_id" : ObjectId("5edf7b4e18b2c26b9dfe8cad"), "code" : "P2", "Qty" : 200, "status" : "Activo" }
{ "_id" : ObjectId("5edf7b4e18b2c26b9dfe8cae")), "code" : "P3", "Qty" : 0, "status" : "Dectivo" }
>
```

- **Inserción masiva de registros**

También se puede insertar un gran número de documentos de forma ordenada y desordenada ejecutando los métodos `initializeOrderedBulkOp()` e `initializeUnorderedBulkOp()`.

**Sintaxis**:

```markup
var bulk = db.collectionName.initializeUnorderedBulkOp();

bulk.insert({documento1} );

bulk.insert({documento2} );

bulk.insert({documentn} );

bulk.execute();
```

**Ejemplo:**

```markup
> var bulk = db.geekFlareCollection.initializeUnorderedBulkOp();
> bulk.insert({ código: "P1", Cant: 100, estado: "Activo"});
> bulk.insert({ código: "P2", Ctd: 200, estado: "Activo"});
> bulk.insert({ código: "P3", Ctd: 0, estado: "Dectivo"});
> bulk.execute();
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 3,
        "nUpserted" : 0,
        "nMatched" : 0
        "nModificado" : 0
        "nRemoved" : 0
        "upserted" : [ ]
})
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5edf7be318b2c26b9dfe8caf"), "code" : "P1", "Qty" : 100, "status" : "Activo" }
{ "_id" : ObjectId("5edf7be318b2c26b9dfe8cb0"), "code" : "P2", "Qty" : 200, "status" : "Activo" }
{ "_id" : ObjectId("5edf7be318b2c26b9dfe8cb1")), "code" : "P3", "Qty" : 0, "status" : "Dectivo" }
>
```

### 11. Recuperar un documento de una colección

Para buscar el documento almacenado en una colección se puede utilizar el método find(). El siguiente comando se utilizará para recuperar todos los documentos de la colección.

- el método**`find`**()puede utilizarse para recuperar todos los documentos almacenados en una colección.

**Sintaxis**: `collectionName.find()`

**Ejemplo**:

```markup
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5ed31186b6f2c2bb1edb86ce"), "code" : "P1", "Qty" : 200, "status" : "Activo" }
{ "_id" : ObjectId("5ed31186b6f2c2bb1edb86cf"), "code" : "P2", "Qty" : 200, "status" : "Activo" }
{ "_id" : ObjectId("5ed31186b6f2c2bb1edb86d0"), "code" : "P3", "Qty" : 200, "status" : "Activo" }
{ "_id" : ObjectId("5ed3159eb6f2c2bb1edb86d1"), "code" : "P4", "Qty" : 100, "status" : "Inactivo" }
```

- el método**`find({condition})`** puede utilizarse para recuperar de la colección sólo los documentos necesarios basados en algunas condiciones. MongoDB proporciona una lista de [operadores de proyección y consulta](https://docs.mongodb.com/manual/reference/operator/query/) para recuperar valores de tipo BSON.

**Sintaxis**: `collectionName.find({condicion })`

**Ejemplo**:

```markup
> db.geekFlareCollection.find({ Cantidad: { $eq: 100 }});
{ "_id" : ObjectId("5ed3159eb6f2c2bb1edb86d1"), "code" : "P4", "Qty" : 100, "status" : "Inactivo" }
```

- Para recuperar un solo documento MongoDB proporciona el método `findOne`(). Proporciona una salida formateada.

**Sintaxis**: `collectionName.findOne()`

**Ejemplo**:

```markup
> db.geekFlareCollection.findOne();
{ 
	"_id" : ObjectId("5ed31186b6f2c2bb1edb86ce"), 
        "código" : "P1",
	"Cantidad" : 200 
	"estado" : "Inactivo" 
}
```

### 12. Embellecer salida de recuperación

El método `find(` ) da una salida desordenada. MongoDB proporciona comandos `pretty` () para obtener la salida formateada.

**Sintaxis**: `collectionName.find().pretty()`

**Ejemplo**:

```markup
> db.geekFlareCollection.find({ Cant: { $eq: 100 }}).pretty();
{
        "_id" : ObjectId("5ed3159eb6f2c2bb1edb86d1"),
        "code" : "P4",
        "Cantidad" : 100,
        "estado" : "Inactivo"
}
```

### 13. Actualizar documento en una colección

MongoDB proporciona el método `update()` para establecer nuevos valores para las claves existentes en los documentos. El comando update proporciona detalles de los documentos modificados y emparejados. La sintaxis del comando update es

**Sintaxis**: `collectionName.update({KeyToUpdate},{Set Command})`

**Ejemplo**:

```markup
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfb"), "product" : "bottles", "Qty" : 100 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfc"), "producto" : "pan", "Cantidad" : 20 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfd"), "producto" : "yogur", "Cantidad" : 30 }
>
> db.geekFlareCollection.update({"producto" : "botellas"},{$set : {"Cantidad": 10}} )
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
>
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfb"), "product" : "bottles", "Qty" : 10 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfc"), "product" : "pan", "Qty" : 20 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfd"), "producto" : "yogur", "Cantidad" : 30 }
>
> db.geekFlareCollection.find()
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfb"), "product" : "bottles", "Qty" : 10 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfc"), "product" : "pan", "Qty" : 20 }
{ "_id" : ObjectId("5edf3f67d6bfbd8125f58cfd"), "producto" : "yogur", "Cantidad" : 30 }
```

- **`updateOne()`:** Para actualizar un único documento existe el método `updateOne` (). `updateOne` () proporciona el recuento de documentos coincidentes y modificados.

**Sintaxis**: `collectionName.updateOne({SingleKeyToUpdate},{Set Command})`

**Ejemplo**:

```markup
> db.geekFlareCollection.updateOne({"producto" : "botellas"},{$set : {"Cantidad": 40}} )
{ "reconocido" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

- `<strong>updateMany(</strong>` ) : Para actualizar múltiples documentos bajo alguna condición MongoDB dispone del método updateMany( `)`.

**Sintaxis**: `collectionName.updateMany({filtro},{Comando})`

**Ejemplo**:

```markup
> db.geekFlareCollection.updateMany( { "Ctd" : { $lt: 30 } },{ $set: { "Ctd": "Inactivo"} } )
{ "reconocido" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

### 14. Borrar documento de una colección

Para eliminar el documento, MongoDB dispone de los métodos `deleteOne()` y `deleteMany()`. La sintaxis de los métodos delete son

- `<strong>deleteOne({condition}) </strong>`elimina el único documento que cumple los criterios de eliminación.

**Sintaxis**: `collectionName.deleteOne({CondicionDeBorrado})`

**Ejemplo**:

```markup
> db.geekFlareCollection.deleteOne({"producto" : "pan"})
{ "reconocido" : true, "deletedCount" : 1 }
```

- deleteMany`<strong>( </strong>`) elimina todos los documentos que coinciden con los criterios de borrado. Sin los criterios de borrado deleteMany( `{condition}` ) elimina todos los documentos.

**Sintaxis:** `collectionName.deleteMany`({Condition})

**Ejemplo**:

```markup
> db.geekFlareCollection.deleteMany({"producto" : "botellas"})
{ "reconocido" : true, "deletedCount" : 2 }
```

- `<strong>eliminar() </strong>`Existe otro método para eliminar todos los documentos que coincidan con los criterios de eliminación. El método eliminar() toma dos argumentos, uno es la condición de eliminación y el otro es sólo una bandera.

**Nota**: El método remove está obsoleto en las próximas versiones.

**Sintaxis**: `collectionName.remove({CondicionDeBorrado},1)`

**Ejemplo**:

```markup
> db.geekFlareCollection.remove({"producto" : "botellas"})
WriteResult({"nRemoved" : 1 })
```

### 15. Recuperar Distintos

El método `distinct(` ) se utiliza para obtener registros únicos.

- Para obtener registros distintos de un campo

**Sintaxis**: `nombrecoleccion.distinct(campo)`

**Ejemplo**:

```markup
> db.geekFlareCollection.distinct("producto")
[ "Queso", "Snacks2", "Snacks3", "pan", "ketchup" ]
```

- Para obtener registros distintos de un campo mientras especifica la consulta.

**Sintaxis**: `nombrecoleccion.distinct(campo,consulta)`

**Ejemplo**:

```markup
> db.geekFlareCollection.distinct('producto',{"Cant.":20})
[ "Snacks3", "pan" ]
```

### 16. Renombrar colección

MongoDB proporciona el método `renameCollection ()` para renombrar la colección.

**Sintaxis**: `colecciónNombre.renombrarColección(nuevaColecciónNombre)`

**Ejemplo**:

```markup
>db.geekFlareCollection.renameCollection('geekFlareCol')
{ "ok" : 1 }
> mostrar colecciones
geekFlareCol
```

## Indexación

### 17. Crear índice en el documento

Los índices son una estructura de datos especial que almacena una pequeña parte del conjunto de datos de la colección de forma fácil de recorrer. Los índices admiten la ordenación ascendente y descendente de los valores de los campos y, por tanto, facilitan un mejor rendimiento durante la recuperación.

MongoDB proporciona el índice `default_id`. Además, MongoDB admite la creación de índices definidos por el usuario. Los índices de MongoDB se definen a nivel de colecciones y proporciona soporte en campos o subcampos de un documento. La sintaxis de creación del índice es :

- Crear un índice sobre un único campo.

**Sintaxis**: `collectionName.createIndex({Key:1})`

En ella, la clave indica el campo sobre el que se crea el índice y 1 significa orden ascendente. Para crear un índice en orden descendente se puede utilizar -1.

**Ejemplo**:

```markup
> db.geekFlareCollection.createIndex({"producto" : 1})
{
        "createdCollectionAutomatically" : false
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

- Crear un índice en varios campos.

**Sintaxis**: `collectionName.createIndex({Clave1:1,clave2:1...keyn:1}`)

**Ejemplo**:

```markup
> db.geekFlareCollection.createIndex({"producto" : 1, "Ctd":-1})
{
        "createdCollectionAutomatically" : false
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

### 18. Mostrar índice en documento

MongoDB proporciona el método `getIndexes()` para listar todos los índices creados sobre un documento.

**Sintaxis**: `collectionName.getIndexes()`

**Ejemplo**:

```markup
> db.geekFlareCollection.getIndexes()
[
        {
                "v" : 2,
                "clave" : {
                        "_id" : 1
                },
                "nombre" : "_id_",
                "ns" : "geekFlareCollection.geekFlareCollection"
        }
]
```

### 19. Eliminar índice del documento

el método**`dropIndex(`** ) se utiliza para eliminar el índice único y el método dropIndexes() se utiliza para eliminar varios índices.

- Eliminar índice único

**Sintaxis**: `collectionName.dropIndex({key})`

**Ejemplo**:

```markup
> db.geekFlareCollection.dropIndex({"producto" : 1})
{ "nIndexesWas" : 3, "ok" : 1 }
```

- Eliminar varios índices.

**Sintaxis**: `collectionName.dropIndexes({clave1,clave2...,claveN})`

**Ejemplo**:

```markup
> db.geekFlareCollection.dropIndexes({"producto" : 1, "Ctd":-1})
{ "nIndexesWas" : 3, "ok" : 1 }
```

## Recuperación relacionada

### 20. Limitar la recuperación de documentos

el método**`limit`** () ayuda a limitar el número de documentos devueltos. El método limit() acepta argumentos numéricos.

**Sintaxis**: `collectionName.find().limit(number)`

**Ejemplo**:

```markup
> db.geekFlareCollection.find().limit(2)
{ "_id" : ObjectId("5ed3c9e7b6f2c2bb1edb8702"), "product" : "bottles", "Qty" : 100 }
{ "_id" : ObjectId("5ed3c9e7b6f2c2bb1edb8703"), "product" : "pan", "Qty" : 20 }
```

### 21. Omitir la recuperación de documentos

MongoDB admite el método `skip()`. Este método omite el número requerido de documentos. Acepta un argumento numérico.

**Sintaxis**: `collectionName.find().skip(number)`

**Ejemplo**:

```markup
> db.geekFlareCollection.find().skip(2)
{ "_id" : 3, "producto" : "yogur", "Cant" : 30 }
> db.geekFlareCollection.find().skip(3)
```

### 22. Ordenar la recuperación de documentos

El método `sort(` ) de MongoDB ordena los documentos de salida en orden ascendente o descendente. Este método acepta el nombre de las claves con el número para especificar el orden de ordenación 1 se utiliza para el orden ascendente mientras que -1 se utiliza para especificar el orden descendente.

**Sintaxis**: `collectionName.find().sort({key:1})`

**Ejemplo**:

```markup
> db.geekFlareCollection.find().sort({"Cant":1})
{ "_id" : 2, "product" : "bread", "Qty" : 20 }
{ "_id" : 3, "product" : "yogurt", "Qty" : 30 }
{ "_id" : 1, "product" : "botellas", "Qty" : 100 }
```

## Validación relacionada

### 23. Validación de documentos

Los validadores ayudan a restringir el tipo de datos que se insertan en los documentos. Los validadores se definen en la colección. Para crear un validador es necesario utilizar la palabra clave **validador** y, opcionalmente, el **nivel de validación** y la **acción de validación** para especificar el modo de validación. La validación de documentos no restringe la inserción del nuevo campo en el documento.

**Sintaxis**: `createCollection("collectionName",{validator:{ fields condition }})`

**Ejemplo:**

```markup
> db.createCollection( "Login",
...  { validador: { $and:
...       [
...          { teléfono: { $tipo: "cadena" } },
...          { email: { $regex: /@flares\.com$/ } },
...          { estado: { $in: [ "Registrado", "Desconocido" ] } }
...       ]
...    }
... } )
{ "ok" : 1 }
>
> db.Login.insert({phone:1234})
WriteResult({
        "nInserted" : 0
        "writeError" : {
                "code" : 121
                "errmsg" : "Falló la validación del documento"
        }
})
>
> db.Login.insert({phone: "1234",email: "abc@flares.com",status: "Desconocido",mode: "limitado"})
WriteResult({ "nInserted" : 1 })
```

### 24. Validadores de esquema en una nueva colección

Se requiere la palabra clave adicional **$jsonSchema** junto con el valor de **las propiedades adicionales** como **False** para poner una restricción a nivel de esquema. Impide que se añadan nuevos campos en el documento.

**Sintaxis**: `createCollection("collectionName",{validator: { $jsonSchema { schema condition } }})`

**Ejemplo**:

```markup
> db.createCollection( "Login", {
... validador: { $jsonSchema: {
... bsonTipo "object",
...        "additionalProperties": false,
... requerido: [ "email" ],
... propiedades: {
... correo electrónico: {
... bsonType : "cadena",
... patrón : "@flares\.com$",
... descripción: "cadena que cumple la expresión dada"
...          },
... estado: {
... enum: [ "registrado", "no válido" ],
... descripción: "el estado debe estar dentro de los valores del enum"
...          }
...       }
...    } },
... } )
{ "ok" : 1 }
>
> db.Login.insert({email: "abc@flares.com"})
WriteResult({
        "nInserted" : 0
        "writeError" : {
                "code" : 121
                "errmsg" : "Documento falló validación"
        }
})
```

### 25. Actualizar o crear validadores de esquema en una colección existente

Se puede crear un validador sobre una colección existente utilizando **`collMod`**

**Sintaxis**: `runCommand({collMod: "nombreColección",validador:{condición de esquema}})`

**Ejemplo:**

```markup
> db.runCommand( {
collMod: "Login",
   validador: { $jsonSchema: {
       bsonTipo: "object",
 "additionalProperties": false,
      requerido: [ "correo electrónico", "estado" ],
      propiedades: {
         correo electrónico: {
            bsonTipo : "cadena",
            patrón : "@flares\.com$",
            descripción: "cadena que cumple la expresión dada"
         },
         estado: {
            enum: [ "registrado", "no válido" ],
            descripción: "el estado debe estar dentro de los valores enum"
         }
      }
   } },
      validationAction: "error",
         validationLevel: "strict"
} )
{ "ok" : 1 }
```

### 26. Eliminar validadores de esquema en una colección existente

Para eliminar los validadores de esquema se requiere establecer `<strong>validationLevel</strong>` como off.

**Sintaxis**: `runCommand({collMod: "collectionName",validator:{ },validationLevel:off})`

**Ejemplo**:

```markup
> db.runCommand({
   collMod: "Inicio de sesión",
   validator:{},
   validationLevel: "off"
})
{ "ok" : 1 }
>
> db.Login.insert({"email": "abc"})
WriteResult({ "nInserted" : 1 })
```

### 27. Comprobar validadores en una colección existente

Para comprobar si la colección existente tiene validadores de esquema ejecute el siguiente comando. Sin especificar el nombre de la colección el método `db.getCollectionInfos(` ) da detalles de los validadores en todas las colecciones que residen dentro de una BD.

**Sintaxis**: `getCollectionInfos({name : "collectionName"})`

**Ejemplo**:

```markup
> db.getCollectionInfos({name: "Login"})
[
        {
                "name" : "Login",
                "tipo" : "colección",
                "opciones" : {
                        "validador" : {
                                "correo electrónico" : {
                                        "$regex" : /@flares\.com$/
                                }
                        }
                },
                "info" : {
                        "readOnly" : false
                        "uuid" : UUID("646674f6-4b06-466d-93b0-393b5f5cb4ff")
                },
                "idIndex" : {
                        "v" : 2,
                        "clave" : {
                                "_id" : 1
                        },
                        "name" : "_id_",
                        "ns" : "geekFlareDB.Login"
                }
        }
]
```

## Cursores relacionados

### 28. Cursores en MongoDB

El cursor es un puntero para iterar sobre el conjunto de resultados. MongoDB utiliza los métodos `<strong>hasNext()</strong>` y `<strong>forEach()</strong>` para la iteración. Se ha proporcionado una lista de [métodos](https://docs.mongodb.com/manual/reference/method/js-cursor/) de cursor.

**Ejemplos**:

```markup
> var newCursor=db.geekFlareCollection.find()
> newCursor.forEach(printjson)
{ "_id" : 1, "producto" : "botellas", "Cant" : 100 }
{ "_id" : 2, "product" : "pan", "Qty" : 20 }
{ "_id" : 3, "product" : "yogurt", "Qty" : 30 }
>
> var nuevoCursor1=db.geekFlareCollection.find()
> while(nuevoCursor1.hasNext()){ printjson(nuevoCursor1.next())}
{ "_id" : 1, "producto" : "botellas", "Cant" : 100 }
{ "_id" : 2, "product" : "pan", "Qty" : 20 }
{ "_id" : 3, "product" : "yogurt", "Qty" : 30 
```

## Utilidad

### 29. Realizar una copia de seguridad de la base de datos

la utilidad`mongodump` se utiliza para exportar el contenido de la base de datos MongoDB como copia de seguridad. Este comando se ejecuta desde la consola del sistema y no desde el shell de mongo. Generará una copia de seguridad binaria junto con la información de metadatos.

**Sintaxis**:

`mongodump --db dbName --out outFile --host "IP:PORT" --username <user> --password <pass>`

**Ejemplo:**

```markup
C:\mongodb\dump>mongodump --db geekFlareDB --out "C:\mongodb\dump" --host "127.0.0.1:27017"
2020-06-02T12:26:34.428 0530 escribiendo geekFlareDB.myTable en
2020-06-02T12:26:34.430 0530 escribiendo geekFlareDB.geekFlareCollection en
2020-06-02T12:26:34.430 0530 escribiendo geekFlareDB.mCollection a
2020-06-02T12:26:34.433 0530 escribiendo geekFlareDB.users en
2020-06-02T12:26:34.434 0530 hecho el volcado de geekFlareDB.myTable (2 documentos)
2020-06-02T12:26:34.434 0530 hecho el volcado de geekFlareDB.geekFlareCollection (4 documentos)
2020-06-02T12:26:34.435 0530 escribiendo geekFlareDB.contacts2 en
2020-06-02T12:26:34.435 0530 escribiendo geekFlareDB.Login en
2020-06-02T12:26:34.436 0530 hecho el volcado de geekFlareDB.mCollection (2 documentos)
2020-06-02T12:26:34.437 0530 hecho el volcado de geekFlareDB.users (1 documento)
2020-06-02T12:26:34.437 0530 hecho el volcado geekFlareDB.Login (0 documentos)
2020-06-02T12:26:34.438 0530 realizado el volcado geekFlareDB.contacts2 (0 documentos)
```

### 30. Restaurando base de datos desde copia de seguridad

La utilidad `<strong>mongorestore</strong>` se utiliza para restaurar los datos binarios generados por `mongodump`.

**Sintaxis**: `mongorestore --db newDB "pathOfOldBackup"`

**Ejemplo**:

```markup
C:\Usuarios\asad.ali>mongorestore --db geekFlareNuevo "C:\mongodb\dump\geekFlare" --host "127.0.0.1:27017"
2020-06-09T15:49:35.147 0530 los argumentos --db y --collection sólo deben utilizarse al restaurar a partir de un archivo BSON. Otros usos son obsoletos y no existirán en el futuro; utilice --nsInclude en su lugar
2020-06-09T15:49:35.148 0530 construyendo una lista de colecciones para restaurar desde C:\mongodb\dump\geekFlare dir
2020-06-09T15:49:35.152 0530 leyendo metadatos para geekFlareNew.geekFlareCollection desde C:\mongodb\dump\geekFlare\geekFlareCollection.metadata.json
2020-06-09T15:49:35.321 0530 restaurando geekFlareNew.geekFlareCollection desde C:\mongodb\dump\geekFlare\geekFlareCollection.bson
2020-06-09T15:49:35.461 0530 no hay índices para restaurar
2020-06-09T15:49:35.462 0530 finalizada la restauración de geekFlareNew.geekFlareCollection (3 documentos, 0 fallos)
2020-06-09T15:49:35.467 0530 3 documento(s) restaurados con éxito. 0 documento(s) fallido(s) al restaurar.
```

### 31. Exportación de colecciones

Para exportar el contenido de una colección a un archivo (JSON o CSV) se ha proporcionado la utilidad `mongoexport`. Para ejecutar este comando utilice el terminal del sistema.

- Exporte una única colección a un archivo.

**Sintaxis**: `mongoexport --db dbName --collection collectionName --out outputFile`

**Ejemplo**:

```markup
C:³³mongodb³nueva carpeta>mongoexport --db geekFlareDB --coleccion geekFlareCol --out outFile.json
2020-06-06T19:02:29.994 0530 conectado a: mongodb://localhost/
2020-06-06T19:02:30.004 0530 exportados 6 registros
```

- Exportar un campo específico de la colección a un archivo.

**Sintaxis**: `mongoexport --db dbName --collection collectionName --out outputFile --fields fieldname`

**Ejemplo**:

```markup
C:³³mongodb³nueva carpeta>mongoexport --db geekFlareDB --coleccion geekFlareCol --out salidaArchivo.json --campos producto
2020-06-06T19:05:22.994 0530 conectado a: mongodb://localhost/
2020-06-06T19:05:23.004 0530 exportados 6 registros
```

### 32. Importando colecciones

Para importar datos desde un archivo (CSV o JSON) se puede utilizar la herramienta de línea de comandos `mongoimport`.

**Sintaxis**: mongoimport –db `dbName --collection collectionName --file inputFile`

```markup
C:\sers\asad.ali>mongoimport --db geekFlareDB --collection geekFlareNew --file outFile.json
2020-06-09T14:52:53.655 0530 conectado a: mongodb://localhost/
2020-06-09T14:52:53.924 0530 6 documento(s) importados con éxito. 0 documento(s) fallaron al importar.
```

## Relacionado con la réplica

> La replicación es diferente a la fragmentación, consulte esta guía para [implementar la fragmentación](https://geekflare.com/es/mongodb-sharding/).

### 33. Replicación MongoDB

La replicación es el proceso para sincronizar datos en múltiples servidores. Evita la pérdida de datos debida a un mal funcionamiento del hardware o del software. MongoDB consigue la replicación utilizando conjuntos de réplica. El conjunto de réplica consiste en conjuntos de datos Mongo primarios y secundarios en el clúster.

El conjunto de datos primario acepta todas las operaciones de escritura y el conjunto de datos secundario lee del primario. Se requiere un mínimo de 3 conjuntos de datos en el conjunto de réplica Mongo. El siguiente proceso es necesario para configurar un conjunto de réplica:

- Inicie el servidor `mongod` con la opción `replset` en un mínimo de 3 nodos.

`mongod --port 27017 --dbpath C:\data\data1 --replSet rs0 --oplogSize 128`

`mongod --port 27018 --dbpath C:\data\data1 --replSet rs0 --oplogSize 128`

`mongod --port 27019 --dbpath C:\data\data1 --replSet rs0 --oplogSize 128`

- Inicialice el conjunto de réplica.

`rs.initiate( { _id : "rs0", members: [ { _id: 0, host: "IP:27017" }, { _id: 1, host: "IP:27018" }, { _id: 2, host: "IP:27019" } ] })`

```markup
> rs.initiate( {
...    _id : "rs0",
... members: [
...   { _id: 0, host: "localhost:27017" },
...   { _id: 1, host: "localhost:27018" },
...   { _id: 2, host: "localhost:27019" }
...    ]
... })
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1591089166, 1),
                "firma" : {
                        "hash" : BinData(0, "AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1591089166, 1)
}
```

### 34. Compruebe el estado de la replicación

Ejecute el siguiente comando desde el nodo de réplica primario para obtener información completa del conjunto de réplicas.

`rs.conf()`

`rs.status()`

```markup
rs0:PRIMARIO> rs.conf()
{
        "_id" : "rs0",
        "version" : 2
        "protocolVersion" : NumberLong(1),
        "writeConcernMayorJournalDefault" : true,
        "miembros" : [
                {
                        "_id" : 0
                        "host" : "localhost:27017",
                        "arbiterOnly" : falso,
                        "buildIndexes" : true,
                        "oculto" : false
                        "priority" : 1,
                        "etiquetas" : {

                        },
                        "slaveDelay" : NumberLong(0),
                        "votos" : 1
                },
                {
                        "_id" : 1
                        "host" : "localhost:27018",
                        "arbiterOnly" : falso,
                        "buildIndexes" : true,
                        "oculto" : false
                        "priority" : 1,
                        "etiquetas" : {

                        },
                        "slaveDelay" : NumberLong(0),
                        "votos" : 1
                },
                {
                        "_id" : 2
                        "host" : "localhost:27019",
                        "arbiterOnly" : falso,
                        "buildIndexes" : true,
                        "oculto" : false
                        "priority" : 1,
                        "etiquetas" : {

                        },
                        "slaveDelay" : NumberLong(0),
                        "votos" : 1
                },
                {
                        "_id" : 3
                        "host" : "localhost:27016",
                        "arbiterOnly" : falso,
                        "buildIndexes" : true,
                        "oculto" : false
                        "priority" : 1,
                        "etiquetas" : {

                        },
                        "slaveDelay" : NumberLong(0),
                        "votos" : 1
                }
        ],
        "ajustes" : {
                "chainingAllowed" : verdadero,
                "heartbeatIntervalMillis" : 2000,
                "heartbeatTimeoutSecs" : 10,
                "electionTimeoutMillis" : 10000,
                "catchUpTimeoutMillis" : -1,
                "catchUpTakeoverDelayMillis" : 30000,
                "getLastErrorModes" : {

                },
                "getLastErrorDefaults" : {
                        "w" : 1,
                        "wtimeout" : 0
                },
                "replicaSetId" : ObjectId("5ed6180d01a39f2162335de5")
        }
}
```

### 35. Añadir nueva instancia de MongoDB a un conjunto de réplicas

Inicie el cliente primario de MongoDB y ejecute el siguiente comando

**Sintaxis**: `rs.add("nombrehost:puerto")`

**Ejemplo**:

```markup
rs0:PRIMARIO> rs.add("localhost:27016")
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1591094195, 1),
                "firma" : {
                        "hash" : BinData(0, "AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1591094195, 1)
}
```

### 36. Eliminar la instancia MongoDB existente del conjunto de réplicas

El siguiente comando eliminará el host secundario requerido del conjunto de réplica.

**Sintaxis**: `rs.remove("localhost:27017")`

**Ejemplo**:

```markup
rs0:PRIMARIO> rs.remove("localhost:27016")
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1591095681, 1),
                "firma" : {
                        "hash" : BinData(0, "AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1591095681, 1)
}
rs0:PRIMARY>
```

### 37. Hacer conjunto de réplica Primario como Secundario

MongoDB proporciona un comando para ordenar a la réplica primaria que se convierta en un conjunto de réplicas secundario.

**Sintaxis**: `rs.stepDown( stepDownSecs , secondaryCatchupSecs )`

**Ejemplo**:

```markup
rs0:PRIMARIO> rs.stepDown(12)
{
        "ok" : 1
        "$clusterTime" : {
                "clusterTime" : Timestamp(1591096055, 1),
                "firma" : {
                        "hash" : BinData(0, "AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1591096055, 1)
}
rs0:SECONDARY>
```

### 38. Compruebe el retardo de réplica entre el primario y el secundario

El siguiente comando se utilizará para comprobar el retardo de replicación entre todos los conjuntos de réplica del primario.

**Sintaxis**: `rs.printSlaveReplicationInfo()`

**Ejemplo**:

```markup
rs0:PRIMARIO> rs.printSlaveReplicationInfo()
origen: localhost:27018
        syncedTo: Tue Jun 02 2020 16:14:04 GMT 0530 (India Standard Time)
        0 segundos (0 horas) por detrás del primario
fuente: localhost:27019
        syncedTo: Thu Jan 01 1970 05:30:00 GMT 0530 (India Standard Time)
        1591094644 secs (441970.73 hrs) detrás del primario
fuente: localhost:27016
        syncedTo: Tue Jun 02 2020 16:14:04 GMT 0530 (India Standard Time)
        0 segs (0 hrs) detrás del primario
rs0:PRIMARIO>
```

## Transacciones relacionadas

### 39. Transacciones en MongoDB

MongoDB soporta propiedades ACID para transacciones sobre documentos.

Para iniciar una transacción, se requiere una sesión para comenzar y un commit para guardar los cambios en la base de datos. Las transacciones están soportadas en conjuntos de réplicas o mangos. Una vez que la sesión se ha comprometido con éxito, las operaciones realizadas dentro de la sesión serán visibles fuera de ella.

- Iniciar sesión

**Sintaxis**: `session =db``.getMongo().startSession()`

- Iniciar transacción,

**Sintaxis**: session `.startTransaction()`

- Confirmar transacción

**Sintaxis**: session `.commitTransaction()`

**Ejemplo**:

Creemos una sesión, iniciemos la transacción, realicemos alguna inserción/actualización y luego consignemos la transacción.

```markup
rs0:PRIMARY> session = db.getMongo().startSession()
sesión { "id" : UUID("f255a40d-81bd-49e7-b96c-9f1083cb4a29") }
rs0:PRIMARIO> session.startTransaction()
rs0:PRIMARY> session.getDatabase("geekFlareDB").geekFlareCollection.insert([
... {_id: 4 , producto: "ketchup"},
... {_id: 5 , producto: "queso"}
... ]);
BulkWriteResult({
        "escribirErrores" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 2,
        "nUpserted" : 0,
        "nMatched" : 0
        "nModificado" : 0
        "nRemoved" : 0
        "upserted" : [ ]
})
rs0:PRIMARY> session.getDatabase("geekFlareDB").geekFlareCollection.find()
{ "_id" : 1, "product" : "bread", "Qty" : 20 }
{ "_id" : 2, "product" : "bottles", "Qty" : 100 }
{ "_id" : 3, "product" : "pan", "Qty" : 20 }
{ "_id" : 4, "product" : "ketchup" }
{ "_id" : 5, "producto" : "Queso" }
rs0:PRIMARY> db.geekFlareCollection.find()
{ "_id" : 1, "product" : "pan", "Qty" : 20 }
{ "_id" : 2, "product" : "bottles", "Qty" : 100 }
{ "_id" : 3, "product" : "pan", "Qty" : 20 }
rs0:PRIMARY> session.commitTransaction()
rs0:PRIMARY> db.geekFlareCollection.find()
{ "_id" : 1, "product" : "bread", "Qty" : 20 }
{ "_id" : 2, "product" : "bottles", "Qty" : 100 }
{ "_id" : 3, "product" : "pan", "Qty" : 20 }
{ "_id" : 4, "product" : "ketchup" }
{ "_id" : 5, "product" : "Queso" }
rs0:PRIMARY> session.getDatabase("geekFlareDB").geekFlareCollection.find()
{ "_id" : 1, "product" : "pan", "Qty" : 20 }
{ "_id" : 2, "product" : "bottles", "Qty" : 100 }
{ "_id" : 3, "product" : "pan", "Qty" : 20 }
{ "_id" : 4, "product" : "ketchup" }
{ "_id" : 5, "product" : "Queso" }
```

### 40. Conflicto de transacciones de documento único

Si dos transacciones intentan actualizar el mismo documento, MongoDB lanza un error de conflicto de escritura.

- `session1.startTransaction()`
- `session2.startTransaction()`

Realice alguna inserción/actualización en Session1 seguida de en Session2. Ahora observe el error en el siguiente ejemplo

**Ejemplo**:

```markup
rs0:PRIMARIO> session1.startTransaction()
rs0:PRIMARIO> session2.startTransaction()
rs0:PRIMARY> session1.getDatabase("geekFlareDB").geekFlareCollection.update({_id:3},{$set:{ product: "Bread" }})
WriteResult({"nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
rs0:PRIMARY> session2.getDatabase("geekFlareDB").geekFlareCollection.update({_id:3},{$set:{ product: "Snacks" }})
WriteCommandError({
        "errorLabels" : [
                "TransientTransactionError"
        ],
        "operationTime" : Timestamp(1591174593, 1),
        "ok" : 0
        "errmsg" : "WriteConflict",
        "code" : 112
        "codeName" : "WriteConflict",
        "$clusterTime" : {
                "clusterTime" : Timestamp(1591174593, 1),
                "firma" : {
                        "hash" : BinData(0, "AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        }
})
rs0:PRIMARY>
```

### 41. Transacciones multidocumento

MongoDB soporta transacciones multi-documento en una única sesión.

- db.getMongo().startTransaction()

Realizar alguna inserción/actualización en múltiples documentos

- session.commitTransaction()

**Ejemplo**:

```markup
rs0:PRIMARIO> var session = db.getMongo().startSession()
rs0:PRIMARIO> session.startTransaction()
rs0:PRIMARY> session.getDatabase("geekFlareDB").geekFlareCollection.update({_id:3},{$set:{ product: "Snacks3" }})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 0 })
rs0:PRIMARY> session.getDatabase("geekFlareDB").geekFlareCollection.update({_id:2},{$set:{ product: "Snacks2" }})
WriteResult({"nMatched" : 1, "nUpserted" : 0, "nModified" : 0 })
rs0:PRIMARIO> session.commitTransaction()
rs0:PRIMARY> db.geekFlareCollection.find()
{ "_id" : 1, "product" : "bread", "Qty" : 20 }
{ "_id" : 2, "product" : "Snacks2", "Qty" : 100 }
{ "_id" : 3, "product" : "Snacks3", "Qty" : 20 }
{ "_id" : 4, "product" : "ketchup" }
{ "_id" : 5, "product" : "Queso" }
rs0:PRIMARY>
```

### 42. Creación de perfiles en MongoDB

La creación de perfiles ayuda a registrar las consultas lentas en la colección `system`.profile. El [nivel de](https://docs.mongodb.com/manual/reference/method/db.setProfilingLevel/) perfilado y la tasa de muestreo definen el porcentaje de consultas que se registrarán en la colección system `.` profile.

- Establecer/Obtener nivel de perfilado

**Sintaxis**:

`db.setProfilingLevel(profilingLevel,{"slowms":tiempo, "sampleRate":LoggingPercentage})`

```markup
> db.setProfilingLevel(2,{"slowms":1, "sampleRate":1})
{"era" : 1, "slowms" : 1, "sampleRate" : 0.5, "ok" : 1 }
>
> db.getProfilingLevel()
2
```

- Obtener el estado de los perfiles

**Sintaxis**: db.getProfilingStatus()

```markup
> db.getProfilingStatus()
{ "was" : 2, "slowms" : 1, "sampleRate" : 1 }
```

- Para habilitar el perfilado a nivel de instancia de MongoDB, inicie la instancia con información de perfilado o añada detalles de perfilado en el archivo de configuración.

**Sintaxis**:

`mongod --profile <Nivel> --slowms <tiempo> --slowOpSampleRate <%Logging>`

**Ejemplo**:

```markup
C:\Windows\System32>mongod --port 27017 --dbpath C:\data\data1 --profile 1 --slowms 25 --slowOpSampleRate 0.5
2020-06-09T02:34:41.110-0700 I CONTROL [ <x>main]</x> Deshabilitando automáticamente TLS 1.0, para forzar la habilitación de TLS 1.0 especifique --sslDisabledProtocols 'none'
2020-06-09T02:34:41.113-0700 W ASIO [ <x>main</x> ] No se ha configurado TransportLayer durante el inicio de NetworkInterface
2020-06-09T02:34:41.113-0700 I CONTROL [ <x><x><x>initandlisten]</x></x></x> MongoDB iniciándose : pid=22604 port=27017 dbpath=C:\data\data1 64-bit host=MCGL-4499
2020-06-09T02:34:41.114-0700 I CONTROL [ <x><x><x>initandlisten]</x></x></x> targetMinOS: Windows 7/Windows Server 2008 R2
2020-06-09T02:34:41.116-0700 I CONTROL [ <x><x><x>initandlisten</x></x></x> ] db version v4.2.7
2020-06-09T02:34:41.116-0700 I CONTROL [ <x><x><x>initandlisten</x></x></x> ] versión git: 51d9fe12b5d19720e72dcd7db0f2f17dd9a19212
```

### 43. MongoDB Explicar()

El método MongoDB `explains` () devuelve estadísticas y proporciona información para seleccionar un plan ganador y ejecutarlo hasta su finalización. Devuelve resultados según el plan de [verbosidad.](https://docs.mongodb.com/manual/reference/command/explain/)

**Sintaxis**: `collectionName.explain("verbosityName")`

Para ejecutar el método/comando explain(), creemos una **verbosidad** y luego ejecutemos el método explain(), eche un vistazo al siguiente ejemplo, donde se han ejecutado estos pasos.

**Ejemplo**:

```markup
> db.runCommand(
...    {
... explicar: { recuento: "producto", consulta: { Cant: { $gt: 10 } } },
... verbosidad: "executionStats"
...    }
... )
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "test.product",
                "indexFilterSet" : false,
                "winningPlan" : {
                        "stage" : "COUNT",
                        "inputStage" : {
                                "stage" : "EOF"
                        }
                },
                "rejectedPlans" : [ ]
        },
        "executionStats" : {
                "executionSuccess" : true
                "nReturned" : 0
                "executionTimeMillis" : 47,
                "totalClavesExaminadas" : 0,
                "totalDocsExaminados" : 0,
                "etapasDeEjecución" : {
                        "stage" : "COUNT",
                        "nReturned" : 0
                        "executionTimeMillisEstimate" : 0,
                        "trabajos" : 1
                        "avanzado" : 0
                        "needTime" : 0
                        "needYield" : 0
                        "saveState" : 0
                        "restoreState" : 0
                        "isEOF" : 1,
                        "nContado" : 0
                        "nSkipped" : 0,
                        "inputStage" : {
                                "stage" : "EOF",
                                "nReturned" : 0,
                                "executionTimeMillisEstimate" : 0,
                                "works" : 0
                                "avanzado" : 0
                                "needTime" : 0
                                "needYield" : 0
                                "saveState" : 0
                                "restoreState" : 0
                                "isEOF" : 1
                        }
                }
        },
        "serverInfo" : {
                "host" : "MCGL-4499",
                "puerto" : 27017
                "version" : "4.2.7",
                "gitVersion" : "51d9fe12b5d19720e72dcd7db0f2f17dd9a19212"
        },
        "ok" : 1
}
>
```

```markup
> var expv = db.geekFlareCol.explain("executionStats")
> expv.find( { producto: "pan"} )
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "geekFlareDB.geekFlareCol",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "producto" : {
                                "$eq" : "pan"
                        }
                },
                "winningPlan" : {
                        "etapa" : "COLLSCAN",
                        "filtro" : {
                                "producto" : {
                                        "$eq" : "pan"
                                }
                        },
                        "direction" : "forward"
                },
                "rejectedPlans" : [ ]
        },
        "executionStats" : {
                "executionSuccess" : true
                "nReturned" : 2
                "executionTimeMillis" : 0,
                "totalClavesExaminadas" : 0,
                "totalDocsExaminados" : 6,
                "etapasDeEjecución" : {
                        "etapa" : "COLLSCAN",
                        "filtro" : {
                                "producto" : {
                                        "$eq" : "pan"
                                }
                        },
                        "nReturned" : 2,
                        "executionTimeMillisEstimate" : 0,
                        "trabajos" : 8
                        "avanzado" : 2
                        "needTime" : 5
                        "needYield" : 0
                        "saveState" : 0
                        "restoreState" : 0
                        "isEOF" : 1,
                        "direction" : "forward",
                        "docsExaminado" : 6
                }
        },
        "serverInfo" : {
                "host" : "MCGL-4499",
                "puerto" : 27017
                "version" : "4.2.7",
                "gitVersion" : "51d9fe12b5d19720e72dcd7db0f2f17dd9a19212"
        },
        "ok" : 1
}
>
```

## Relacionados con el control de acceso

### 44. Control de acceso en MongoDB

Las funciones de control de acceso permiten el acceso de autenticación a los usuarios existentes. Para el control de acceso habilitado DB para asegurarse de crear un usuario admin rol en admin DB.

- Conecte la BD sin autenticación.
- Cambie a la base de datos

`utilizar admin`

- Cree un usuario como el siguiente

`db.createUser( {user: "UserAdmin", pwd: "password" ,role: [adminRole])`

**Ejemplo:**

```markup
db.createUser(
...   {
... usuario "AdminUsuario",
... pwd: passwordPrompt(),
... roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
...   }
... )
Introduzca la contraseña:
Usuario añadido con éxito: {
        "usuario" : "AdminUsuario",
        "roles" : [
                {
                        "rol" : "userAdminAnyDatabase",
                        "db" : "admin"
                },
                "readWriteAnyDatabase"
        ]
}
```

- Reinicie la instancia de `mongod`
- Acceda de nuevo con el usuario y la contraseña creados.

```markup
C:³³Usuarios>mongo --port 27017 --authenticationDatabase "admin" -u "AdminUser" -p
MongoDB shell versión v4.2.7
Introduzca la contraseña:
conectándose a: mongodb://127.0.0.1:27017/?authSource=admin&compressors=disabled&gssapiServiceName=mongodb
```

### 45. Recuperar y eliminar el usuario de control de acceso

El siguiente comando se puede utilizar para comprobar la información del usuario y eliminarlo.

- `db.getUser("AdminUser")`
- `db.dropUser("AdminUser")`

**Ejemplo**:

```markup
> db.getUser("AdminUser")
{
        "_id" : "admin.AdminUser",
        "userId" : UUID("78d2d5bb-0464-405e-b27e-643908a411ce"),
        "user" : "AdminUser",
        "db" : "admin",
        "roles" : [
                {
                        "rol" : "userAdminAnyDatabase",
                        "db" : "admin"
                },
                {
                        "role" : "readWriteAnyDatabase",
                        "db" : "admin"
                }
        ],
        "mecanismos" : [
                "SCRAM-SHA-1
                "SCRAM-SHA-256"
        ]
}
> db.dropUser("AdminUser")
true
> db.getUser("AdminUser")
null
>
```

### 46. Conceder roles definidos por el usuario

MongoDB proporciona el método `db.createRole()` para especificar los privilegios a un usuario y un array de roles heredados.

- Conecte la instancia de MongoDB con el usuario admin.
- Ejecute el siguiente comando para generar un nuevo rol.

**Sintaxis**:

`db.createRole({role: "roleName",privileges:[{privilegeName}],roles:[InheritedArray]})`

**Ejemplo**:

```markup
use admin
> db.createRole(
...    {
... rol: "abc",
... privilegios: [ { resource: { db: "geekFlareDB", colección: "geekFlareCol" }, acciones: [ "killop" , "inprog"] } ],
... roles: []
...    }
... )
{
        "rol" : "abc",
        "privilegios" : [
                {
                        "recurso" : {
                                "db" : "geekFlareDB",
                                "colección" : "geekFlareCol"
                        },
                        "acciones" : [
                                "killop"
                                "inprog"
                        ]
                }
        ],
        "roles" : [ ]
}
```

### 47. Revocar roles definidos por el usuario

Para modificar los roles existentes utilice el siguiente comando.

**Sintaxis**: `db.revokeRolesFromUser( userName, [{ "role" : roleName , db:dbName} ] )`

**Ejemplo**:

```markup
> db.getUser("AdminUser")
{
        "_id" : "admin.AdminUser",
        "userId" : UUID("fe716ed1-6771-459e-be13-0df869c91ab3"),
        "user" : "AdminUser",
        "db" : "admin",
        "roles" : [
                {
                        "rol" : "userAdminAnyDatabase",
                        "db" : "admin"
                },
                {
                        "role" : "readWriteAnyDatabase",
                        "db" : "admin"
                }
        ],
        "mecanismos" : [
                "SCRAM-SHA-1
                "SCRAM-SHA-256"
        ]
}
> db.revokeRolesFromUser( "AdminUser", [{ "role" : "userAdminAnyDatabase" , db: "admin"} ] )
> db.getUser("AdminUser")
{
        "_id" : "admin.AdminUser",
        "userId" : UUID("fe716ed1-6771-459e-be13-0df869c91ab3"),
        "user" : "AdminUser",
        "db" : "admin",
        "roles" : [
                {
                        "rol" : "readWriteAnyDatabase",
                        "db" : "admin"
                }
        ],
        "mecanismos" : [
                "SCRAM-SHA-1
                "SCRAM-SHA-256"
        ]
}
```

### 48. Conectividad MongoDB con Python

El paquete pymongo es necesario para conectar MongoDB desde la consola de python.

```markup
>>> from pymongo import MongoClient
>>> mClient=MongoClient("mongodb://127.0.0.1:27017/")
>>> mDB=mClient.geekFlareDB
>>> mRecord={"_id":4,"name":"XYZ"}
>>> mDB.geekFlareCollection.insert_one(mRecord)
<objetopymongo.results.InsertOneResult en 0x000002CC44256F48>
>>> for i in mDB.geekFlareCollection.find({"_id":4}):
... print(i)
...
{'_id': 4, 'name': 'XYZ'}
>>>
```