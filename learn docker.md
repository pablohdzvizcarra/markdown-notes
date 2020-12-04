# Aprendiendo a usar Docker

```docker search [name-image]```: se utiliza para buscar imagenes docker en el repositorio central de docker que es docker hub

```docker pull [name-image]```: descarga una imagen de docker hub

```docker pull --all-tags [name-image]```: extraera todas las imagenes del registro

```docker images```: muestra las imagenes que tengas en tu maquina de forma local

## Eliminar contenedores

Para pararlos puede usarse:

```docker stop $(docker ps -a -q)```

Y para eliminarlos:

```docker rm $(docker ps -a -q)```

## Crear nuevos contenedores

```docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]```

## Docker run
Corre un comando en un nuevo contenedor

```docker run [OPTIONS] IMAGE [COMMAND] [ARG...]```

```
docker run --name debian-test -it debian
// --name: lo usamos para darle un nombre al contenedor que creamos
// -it | -t -i: indica a docker que asigne un pseudo-TTY para crear un bash interactivo
// --rm: ejecuta el contenedor pero lo elimina cuando termina la ejecucion
// -w: establecer el directorio de trabajo
// --storage-opt size=10G: espacio maximo que puede usar el contenedor
// --tmpfs: monta un tmpfs
// -v: crea un directorio de volumen
// --read-only: no permite modificar archivos del contenedor
// --mount: para montar volumenes dentro de un contenedor
// -p: para exponer puertos
// --expose: exponer puertos pero sin publicarlos en las interfaces del sistema host
// -e: crear variables de entorno
// --env: variables de entorno
// --env-file: cargar un archivo de variables de entorno
// -l | --label: agregan etiquetas a los contenedores
// --network: conectar el contenedor a una red
// -a: le dice a docker que el STDIN | STDOUT | STDERR se unan al contenedor
```

### Example
```
  docker run --name second-nginx -v ~/Downloads/some-statis:/usr/share/nginx/html:ro -d -p 3500:80 nginx
```

--name: lo usamos para darle un nombre al contenedor para identificarlo

-v: le vamos a proporcioanr datos tenemos que poner un path absoluto ~/Downloads/some-static despues de : los puntos viene el path donde se copiaran los archivos en el contenedor

-d: le indicamos que se cree y se ejecute en modo segundo plano

-p: vamos a tenerlo disponible por el puerto 3500

IMAGE - nginx: la imagen que usaremos para crear el contenedor


## User Volumenes en Docker

volumenes: idealeas para almacenar informacion que cambiara constantemente

mount | montajes: es ideal para informacion que no necesita ser modificada constantemente

```docker volume create my-vol```: crea un volumen

```docker volume ls```: lista todos los volumenes

```docker volume inspect [name-volume]```: inspecciona un volumen

```docker volume rm [name-volume]```: elimina un volumen

#### Example
```
  docker run -d --name devtest -v myvo12:/app nginx

  // -d: para que el contenedor se ejecute en segundo plano
  // --name: damos un nombre al contenedor
  // -v: creamos un volumen o usamos uno existente : damos la ruta del contenedor donde usaremos el volumen
  // IMAGE: asignamos la imagen como base para crear el contenedor
```

### Dockerfiles

tips para crear Dockerfiles

```docker build .```: empezara a construir la imagen usando el contexto actual donde este ubicado

```dcoker build -f [path/example]```: creas una imagen usando un Dockerfile en un contexto diferente al actual

```docker build -t [name-image] .```: con la -t agregas un nombre a la imagen a crear

```
  # Formato de un Dockerfile

  # Comment
  INSTRUCTION arguments


  FROM: la imagen en la que se basara docker para construir
```

Examples Dockerfiles:
```
  # Establecemos la imagen base
  FROM busybox

  # agregamos una variable de entorno que apunta a un direcctorio
  ENV FOO=/bar

  # establecemos el directorio de trabajo
  WORKDIR ${FOO}

  # Agregamos archivos
  ADD . ${FOO}

  # copiamos datos
  COPY . /quuxing
```

```
  # .dockerignore

  # comment
  */temp*
  */*/temp*
  temp?
  **/*.js
  !module*.js

  # comment: es un comentario y es ignorado
  */temp*: encontrara cualquier archivo cuyos nombres comienzen con temp en cualquier subdirecion a la raiz
  **/*.js: excluira todos los archivos que terminen con la extension .js desde el directorio raiz
  !module*.js: es excluyen los archivos


```

**Tip:** cuando creas un contenedor con un Dockerfile y usas EXPOSE, expondras el puerto proporcionado, pero aun asi cuando tu usas **docker run** debes proporcionar el puerto con la bandera --publish | -p

ejemplo:
```
  EXPOSE 5000

  cuando corras ese contenedor
  docker run --publish 3000:5000 example-node

```

**Example Dockerfile:**

```
  # seleccionamos la imagen base
  FROM node:lts-alpine

  # agregamos una variable de entorno
  ENV NODE_ENV=production

  # asignamos el directorio de trabajo dentro del contenedor
  WORKDIR /app

  # copiamos archivos al contenedor
  COPY ["package.json", "package-lock.json", "./"]

  # instalamos las dependencias de npm
  RUN npm install --production

  # copiamos todos los archivos al contenedor en el workdir seleccionado
  COPY . .

  # ejecutamos el comando
  CMD [ "node", "server.js" ]

```

**Tip:** ```docker exec -it [name-node-container] sh``` para entrar en un contenedor docker

*Example*
**docker run:**
```
  docker run --detach --publish 2100:8000 --name rest-server node-docker

  --detach | -d : indica al contenedor que corra en modo independiente| segundo plano
  --publish | -p : asigna los puertos para acceder al contenedor [ puerto exterior : puerto dentro del contenedor]
  --name : da un nombre al contenedor
```


