### Que son los datos Estructurados, Semiestructurados y no Estructurados

**Datos Extructurados:**

Son aquellos que encuentras en la bases de datos relacionales, estan construidos por medio de tablas donde se almacena la informacion, puedes crear relaciones entre las diferentes tablas para crear relaciones entre los datos de una manera sencilla y debido a esa versatilidad pueden ser analizados de manera sencilla

**Datos No Estructurados:**

Datos que como el nombre lo indica no tiene estructura alguna un claro ejemplo tu correo electronico es una lista de datos no estructurados, las publicaciones de facebook, youtube etc, podría pensar en ellos como una lista del super donde solo vas almacenando artículos sin ninguna estructura


**Datos semi estructurados:**

Igual que los no estructurados no tiene estructura alguna, pero se logra relacionar los datos entre si usando algunas tecnicas para ese fin

## Analizando las bases de datos NoSqL

#### Esquema y modelos

Las bases de datos NoSQL usan esquemas dinámicos, esto quiere decir que puedes comenzar a desarrollar tu aplicación sin ningún esquema definido y como tu aplicación vaya creciendo o necesitando nuevas cosas puedes modificar el esquema de una manera sencilla, a su vez esta ventaja también puede llegar a ser una desventaja

#### Estructura de datos
Las bases de datos NoSQL pueden estar basadas en:

- Documentos
- Bases de datos de gráficos
- Pares clave-valor
- Almacenes de columnas anchas

#### Escalada

Pueden escalar con mucha facilidad debido a que los datos en su mayoría no depeden de otros datos una base de datos NoSQL puede ser dividida en pequeñas bases de datos donde solo se aloje un tipo de información


> Las bases de datos NoSQL pueden almacenas y procesar datos en tiempo real

**Ejemplos de bases de datos NoSQL:**

**Documento**: 

MongoDB y CouchDB: Propósito General

**Clave-Valor**: 
  
Redis y DynamoDB: Grandes cantidades de datos con consultas de búsquedas simples


**Columna ancha**: 

Cassandra y HBase: Grandes cantidades de datos con patrones de consulta predecibles

**Graph**: 

Neo4j y Amazon Neptune: Analizar y recorrer relaciones entre datos conectados


### Base de datos de documentos

Una base de datos donde se almacenan objetos similares a JSON, los cuales contiene la información 


#### Modelado de datos en bases NoSQL

Una base de datos NoSQL se organiza por medio de documentos que dentro contiene diferentes colecciones y a su vez esas colecciones contienen mas documentos podrias simplificarlo con un objeto en un codigo JS Ejemplo:


```javascript
const someDatabase = { // base de datos
    collectionUser: { // coleccion 1
        user1: {}, // documentos alojados dentro de la coleccion
        user2: {}
    },
    collectionTasks: { // coleccion 2
        
    }
}
```
El objeto de JS de la parte de arriba podría simular una database sencilla en MongoDB


## Diseño de modelado de datos

La consideración clave para la estructura de los documentos es la decision de incrustar o utilizar referencias a la hora de modelador los documentos

**Modelos de datos integrados:**

```javascript
const distroUbuntu = {
    _id: "<ObjectId1>", // id por defecto de MongoDB
    name: "Arnold", // campo nombre
    tasks: { // sub-documento
              name: 'run today',
              state: false
           },
    talents: { // sub-documento
                sing: 'good',
                jump: "not good"
              }       
}
```
El ejemplo de arriba es un modelo de datos integrados, ya que dentro de él se están agregando varios sub-documentos, donde se podrían hacer consultas más veloces, ya que con una consulta obtienes todos los datos necesarios

> A un modelo de datos integrados le puedes elaborar consultas atómicas que se refiere, a que con una consulta obtienes todos los datos necesarios, sin necesidad de elaborar mas consultas 

**Modelo de datos normalizados:**

En este tipo de modelos se describen relaciones utilizando referencias entre documentos ejemplo:

```
# user document
{
  _id: "<ObjectId1>", // agregado por mongodb
  name: "Jonh",
  lastname: "Carter",
}

# addres user document
{
    _id: "<ObjectId2>", // agregado por mongodb
    user_id: "<ObjectId1>", // se hace referencia al user document
    addres: "Calle buenaventura"
}

# contact document
{
    _id: "<ObjectId3>", // agregado por mongodb
    user_id: "<ObjectId1>", // se hace referencia al user document
    email: "example@example.com"
}
```