# Rest

Rest es el acronimo de Representation State Transfer

**Null Style:** es un conjunto vacio de restricciones, podria decirse que es un lugar donde tu puedes hacer lo que desees con la creacion y como la puedas crear

una API RestFull es aquella que satisface las 6 restricciones que se deben seguir para poder decir que tu API es REST

**Interfaz Uniforme:**

Todos los recursos deben ser accesibles a traves de un enfoque comun y deben modificarse de manera similar utilizando un enfoque coherente

**Servidor de cliente:**

el servidor y el cliente deben funcionar de manera separada, ninguno debe depender del otro para poder elaborar su trabajo de una manera correcta

**Stateless**

no se almacenara nada de estado del cliente en la aplicacion, supongamos como una sesion, no debe ser almacenada en el servidor por parte del cliente, cada vez que el cliente haga una peticion debe proporcionar todo lo necesario para que esa peticion se pueda ejecutar

**Cacheable**

debemos almacenar en cache recursos cuando estos puedan ser almacenados, ais reduciremos la carga del servidor y funcionara de una manera mas rapida

**Layered system**

almacenas datos en el servidor A, y se autentica en el servidor B.

**Code on demand (optional)**
