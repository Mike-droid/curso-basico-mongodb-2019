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