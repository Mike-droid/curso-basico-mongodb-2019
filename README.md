# Cursó Básico de Mongo DB

## Qué aprenderás sobre MongoDB

[MongoDB University](https://university.mongodb.com/)

[MongoDB vs PostgreSQL](https://bytescout.com/blog/mongodb-vs-postgresql.html)

[10 MongoDB tutorials for beginners](https://medium.com/quick-code/top-tutorials-to-learn-mongo-db-f1e52bee7445)

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
