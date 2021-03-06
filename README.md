# Cursó Básico de Mongo DB

## Qué aprenderás sobre MongoDB

[MongoDB University](https://university.mongodb.com/)

[MongoDB vs PostgreSQL](https://bytescout.com/blog/mongodb-vs-postgresql.html)

[10 MongoDB tutorials for beginners](https://medium.com/quick-code/top-tutorials-to-learn-mongo-db-f1e52bee7445)

[Documentación oficial de MongoDB](https://docs.mongodb.com/manual/introduction/)

### Bases de datos NoSQL

En NoSQL tenemos 4 grandes familias:

- Key-value stores -> Por ejemplo, redis. Son muy usadas para guardar información en caché. Son muy rápidas para consultar. No son convenientes para modelos complejos.
- Graph databases -> Por ejemplo, Neo4J. Nos permiten establecer relaciones en nuestras entidades. Como con Twitter. Nos permiten hacer consultas mucho más eficientes que las típicas consultas de SQL.
- Wide-column stores -> Por ejemplo, cassandra. Nos permiten hacer queries mucho más rápidas. Poseen 2 llaves, una de fila y otra de columna. Son usadas en Big Data. Modelar datos dentro de estas estructuras es más complicado.
- Document databases -> Por ejemplo, MongoDB. Nos permiten guardar documentos dentro de las colecciones. Podemos modelar casos de la vida real de manera más sencilla. Es como un JSON.

### Definición de MongoDB y su ecosistema (herramientas de uso)

MongoDB es una base de datos NoSQL, basada en documentos que nos permite guardar gran cantidad de documentos de forma distribuida.

MongoDB nos permite guardar estructuras tipo JSON (realmente es BSON). MongoDB es distribuida (tiene varios servidores, entonces hablamos de un clúster). Podemos escalar de forma **horizontal** (más servidores/nodos).

MongoDB es schema less. Podemos guardar documentos con diferentes estructuras. Con JavaScript podemos hacer uso de MongoDB.

¡MongoDB es gratis y de código abierto! 😀

### MongoDB Atlas

Creamos nuestra cuenta en [MongoDB](https://mongodb.com)

Es importante seleccionar un Cluster compartido y con la ubicación geográfica más cercana a nuestra dirección, para que sea gratis y rápido. En este caso usaremos un clúster de AWS.

Es importante crear un usuario con el rol "Atlas Admin" que básicamente tiene todos los privilegios. También es **muy importante** agregar nuestra dirección IP a las listas de direcciones IP que pueden acceder a este servidor.

### Instalación de MongoDB en Windows

Debemos descargar [MongoDB Community Server](https://www.mongodb.com/try/download/community) y ejecutar el instalador.

### Instalación de MongoDB en Mac/Linux

### Mongo Shell, configuración de clientes

Si usamos windows, es importante añadir mongo.exe al PATH.

Nos conectamos con nustro servidor haciendo `mongo 'urlDelServidor' --user 'nombre-usuario'` y luego escribimos la contraseña. Si todo está bien, deberemos tener un `0:PRIMARY>`.

En MongoDB Atlas, solamente debemos hacer `mongodb+srv://'nombreUsuario':<password>@'urlDelServidor'/`

- `show dbs` -> Lista de bases de datos.
- `use 'nombreBD'` -> Creamos una base de datos (o la usamos si ya existe).
- `db` -> Muestra en cuál base de datos estamos.
- Rápidamente podemos insertar documentos, por ejemplo: `db.inventory.insertOne(
        { item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } }
)`
- `db.'nombreColeccion'.findOne()` -> Muestra un documento de la colección.

### MongoDB + Drivers

Los drivers son las librerías que usamos para comunicar nuestra aplicación con nuestra base de datos.

Existen algunos drivers oficiales:

- C
- C++
- C#
- Go
- Java
- Node.js
- Perl
- PHP
- Python
- Motor (Python Async)
- Ruby
- Mongoid (Ruby ODM)
- Scala

Para agregar los drivers al proyecto usamos un gestor de dependencias. Con Java usamos Maven.

Con Python usamos Pip, por ejemplo: `python -m pip install pymongo`

Con NodeJS usamos NPM, por ejemplo: `npm install mongodb --save`

#### Inicio rápido transversal a la mayoría de los lenguajes (POO)

1. Crear conexión MongoClient
2. Obtener la base de datos MongoDatabase
3. Acceder a una colección MongoCollection
4. CRUD

## Operaciones CRUD

### Bases de datos, Colecciones y Documentos en MongoDB

- Bases de datos
  - Contenedor físico de colecciones
  - Cada base de datos tiene su archivo propio en el sistema de archivos
  - Un clúster puede tener múltiples bases de datos
- Colecciones
  - Agrupación de documentos
  - Equivalente a una tabla en las bases de datos relaciones
  - No impone un esquema (las colecciones no deben tener la misma estructura necesariamente)
- Documentos
  - Un registro dentro de una colección
  - Es análogo a un JSON (pero es un BSON)
  - La unidad básica de MongoDB

### Operaciones CRUD desde la consola de MongoDB

MongoDB no crea bases de datos vacías. "_id" es un campo obligatorio.

[Apuntes extra del curso](https://static.platzi.com/media/public/uploads/crud_0540220d-88e9-447c-9e03-681375363137.txt)

**Mucho cuidado con esta instrucción:** `db.nombreColeccion.deleteMany({})` porque borrará TODA la base de datos.

### Operaciones CRUD desde Compass

Es más fácil.

## Esquemas y relaciones

### Tipos de datos

Nuestros documentos no pueden exceder el tamaño de 16MB.

- Strings -> "Texto"
- Boolean -> true/false
- ObjectId -> Son identificadores únicos en BSON
- Date -> ISODate('AAAA-MM-DDTHH:MM:SS.SSSZ')
- Number:
  - Double
  - Integer 32 bits
  - Integer 64 bits
  - Decimal -> Más enfocado a información financiera
- Documentos embebidos -> Es como un JSON dentro de otro (y así tantos como quieras)
- Arrays

### ¿Qué son los esquemas y las relaciones?

Los esquemas son las formas en que nosotros organizamos nuestros documentos dentro de nuestras colecciones.

MongoDB no impone ningún esquema.

```JSON
{
  "_id": ObjectId(<ObjectId>),
  "userName": "Miguel",
  "age": 23
},
{
  "_id": ObjectId(<ObjectId>),
  "name": "José
  "city": "Los Ángeles"
}
```

Las relaciones son las formas en que las entidades/documentos se encuentran enlazados unos con otros.

### Relaciones entre documentos

```JSON
{
  _id: "joe",
  name: "Joe Bookreader"
},
{
  patron_id: "joe",
  street: "123 Fake Street",
  city: "Faketon",
  state: "MA",zip: 12345
}
```

Esto de arriba es muy SQL. Mejor hacemos uso de documentos embebidos:

```JSON
{
  _id: "joe",
  name: "Joe Bookreader",
  address: {
    street: "123 Fake Street",
    city: "Faketon",
    state: "MA",
    zip: 12345
  }
}
```

Relaciones uno a muchos usando documentos embebidos:

```JSON
{
  _id: "joe",
  name: "Joe Bookreader",
  address: [
    {
      street: "123 Fake Street",
      city: "Faketon",
      state: "MA",
      zip: 12345
    },
    {
      street: "456 Fake Street",
      city: "Boston",
      state: "MA",
      zip: 12345
    }
  ]
}
```

**Importante:** La operación `update` en MongoDB **NO** es transaccional.

## Profundización de queries dentro de MongoDB

### Operadores para realizar queries y proyecciones

Filtros:

```javascript
db.inventory.find({ status: { $in: [ "A", "D" ] } })
```

Proyecciones:

`db.inventory.findOne({status: "A"})`

```JSON
{
  "_id": ObjectId("23d23d23fr23f23f"),
  "item": "journal",
  "status": "A",
  "size": {
    "h": 14,
    "w": 21,
    "uom": "cm"
  },
  "inStock": [
    {
      "warehouse": "A",
      "qty": 5
    }
  ]
}
```

Podemos ser más específicos:

`db.inventory.findOne({status: "A"}, {item: 1, status: 1})`

Ese 1 es valor booleano, así que le decimos que queremos solo los campos `item` y `status`.

```JSON
{
  "_id": ObjectId("23d23d23fr23f23f"),
  "item": "journal",
  "status": "A"
}
```

Operadores de comparación:

| Nombre | Descripción       |
| ------ | ----------------- |
| $eq    | Igual a           |
| $ne    | Distinto a        |
| $gt    | Mayor que         |
| $gte   | Mayor o igual que |
| $lt    | Menor que         |
| $lte   | Menor o igual que |
| $in    | En un conjunto    |
| $nin   | No en un conjunto |

Operadores lógicos:

| Nombre | Descripción |
| ------ | ----------- |
| $and   | Y           |
| $or    | O           |
| $not   | No          |
| $nor   | No o        |

Operadores por elemento:

| Nombre  | Descripción                                           |
| ------- | ----------------------------------------------------- |
| $exists | Documentos que cuentan con un campo específico        |
| $type   | Documentos que cuentan un campo de un tipo específico |

Operadores para arreglos:

| Nombre     | Descripción                                                                |
| ---------- | -------------------------------------------------------------------------- |
| $all       | Arreglos que contengan todos los elementos de la query                     |
| $elemMatch | Documentos que cumplen la condición del $elemMatch en uno de sus elementos |
| $size      | Documentos que contienen un campo tipo arreglo de un tamaño específico     |

### Usando operadores para realizar Updates en arreglos

[Documentación sobre operadores de MongoDB](https://docs.mongodb.com/manual/reference/operator/)

[Artículo en Platzi](https://platzi.com/clases/1533-mongodb/18555-usando-operadores-para-realizar-updates-en-arreglo/)

### Operaciones avanzadas con Agregaciones

Las agregacions son operaciones más avanzadas.

[Documentación sobre operadores de MongoDB](https://docs.mongodb.com/manual/reference/operator/)

[Tutorial MongoDB 4.2 Parte 10 Agregaciones : Instrucción Aggregate $match $group $sum $avg $multip](https://www.youtube.com/watch?v=OV2byyfKHlw&list=PLpk46uAL3qUG3NYfYJkmREZGCX5yM3P7u&index=11)

## Python con MongoDB

### Configuración e instalación de dependencias para el proyecto PlatziMongo

[Artículo en Platzi](https://platzi.com/clases/1533-mongodb/18554-configuracion-e-instalacion-de-dependencias-para-e/)

### Operaciones CRUD con Python y Pymongo

El proyecto ya cuenta con el código de Python para hacer un CRUD y ponerlo a prueba con Postman (aunque yo usé ThunderClient de VS Code).

### Diseñando el esquema de clases, cursos y carreras

Creamos carreras.json:

```JSON
{
  "_id": "614bf442809a5509c0203abb",
  "nombre": "Carrera de AWS",
  "descripcion": "En esta carrera aprenderas AWS",
  "cursos": [
    {
      "_id": "",
      "nombre": "Nombre del curso"
    },
    {
      "_id": "",
      "nombre": "Nombre del curso"
    }
  ]
}
```

cursos.json:

```JSON
{
  "_id": "",
  "nombre": "",
  "descripcion": "",
  "clases": [
    {
      "_id": "",
      "orden": 1,
      "nombre": "",
      "video": ["url1"]
    },
    {
      "_id": "",
      "orden": 1,
      "nombre": "",
      "video": ["url1"]
    }
  ]
}
```

### Ejecución de queries

### Relaciones

### Consultas más rápidas con Índices

En MongoDB los índices ayudan a que las consultas sean más rápidas. Sin índices, MongoDB debe hacer un escaneo de toda la colección.

Existen varios tipos de índices:

- De un solo campo
- Compuestos
- Multillave
- Geoespaciales
- De texto
- Hashed

## Recomendaciones para poner en producción tu cluster de Atlas

### Recomendaciones de Arquitectura y Paso a Producción

Usa un Backend basadoe en la nube como AWS, GCP o Azure.

Usa MongoDB Atlas como servicio.

Guarda las credenciales en variables de entorno o archivos de configuración fuera del proyecto.

Asegura que tu clúster se encuetre en la misma región del proveedor que tu aplicación.

Has [VPC peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) entre la VPC de tu aplicación y la VPC de tu clúster.

Cuida tu lista de IP's blancas.

Habilitar autenticación de dos pasos.

Actualiza constantemente tu versión de MongoDB.

Ten separados tus ambientes de dev/test/prod.

Habilita la opción de storage encriptado.

- [14 Things I Wish I'd Known When Starting with MongoDB](https://www.infoq.com/articles/Starting-With-MongoDB)
- [Performance Best Practices for MongoDB](https://www.mongodb.com/collateral/mongodb-performance-best-practices)
- [What is MongoDB Sharding and the Best Practices](https://geekflare.com/mongodb-sharding-best-practices/)

## Fin del curso

### Resumen y conclusiones

[MongoDB Workbook](http://nicholasjohnson.com/mongo/course/workbook/)
