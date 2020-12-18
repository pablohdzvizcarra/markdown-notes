# El modelo de madurez de Richardson

### Glory of Rest

Podemos pensar en esto como niveles de tu API Rest, los niveles dependen de la implementacion de tu API 
- **Level 0:** The Swamp of POX
- **Level 1:** Resources
- **Level 2:** HTTP Verbs
- **Level 3:** Hypermedia Controls

## Nivel 0

El punto de partida de los modelos es utilizar HTTP como sistema de transporte para interacciones remotas, pero sin utilizar ninguno de los mecanismos de la web.

**Example:**
```javascript
//Imaginemos que tenemos una aplicacion de tareas de usuarios para crear un simple tarea
//podemos hacer una peticion POST

// ejemplo tarea
const task = {name: 'buy milk', state: false}
POST /api/tasks
// crearia una tarea en esa uri, pero que pasa si el nombre de las tareas debe ser unico?
// otro usuario no podria crear una tarea con ese mismo nombre
```

## Nivel 1 Recursos

En este punto todos nuestros endpoint apuntarán a un recurso específico para realizar las operaciones

**Example:**
```javascript
// mismo ejemplo de la tarea, pero ahora buscamos asignar la tarea a un recurso de usuario existente
// ejemplo tarea
const task = {name: 'buy milk', state: false}
POST /api/tasks/user123
// creara una tarea pero en el recurso del usuario *user123* que existe en la database
// y de esta manera podemos tener tareas con nombre identicos
```

## Nivel 2 Verbos HTTP

Debemos usar los verbos HTTP existentes para ingresar a los recursos de las URI en la API y debemos responder con Status Code HTTP similares al comportamiento que estamos creando en el URI, ya sea un resultado exitoso o un error

**Ejemplos:**

```javascript
// hacemos un GET para obtener las tasks
const task = {name: 'buy milk', state: false}
POST /api/tasks/user123

const response = {
    statusCode: 404,
    message: 'user not found'
}

// el verbo POST lo usamos para agregar datos 
// si el recurso que solitamos no existe el status code correcto seria 404 (no encontrado)
// y la solicitud no se puede completar
```


```javascript
// hacemos un GET para obtener las tasks
GET /api/tasks

const response = {
    statusCode: 200,
    tasks: [
        {name: 'taks1'},
        {name: 'task2'}
    ]
}

// el verbo GET se usa para obtener recursos de API mediante el URI si no hay ningun error
// el status code apropiado seria 200
```


## Nivel 3 Controles Hipermedia

Podemos imaginar este nivel como preguntar al API primero antes de crear, o lo podemos ver como verificar la disponibilidad del recurso antes de tratar de usarlo

**Example:**
```javascript
// imaginemos que tenemos esat URI
// /api/user/tasks

// podemos elaborar un post a ese endpoint para crear una tarea en ese usuario
const task = {name: 'buy milk', state: false}
POST /api/user/tasks

// podemos responder por hipermedia con links hacia acciones que se pueden llevar a cabo
// despues de crear la tarea en dicho usuario

// POST /api/user/tasks/:idtask/completed
// DELETE /api/user/tasks/:idtask
// PATCH /api/user/tasks/:idtask
```

De esta manera le proporcionamos información adicional sobre las siguientes acciones que podemos elaborar después de crear la tarea