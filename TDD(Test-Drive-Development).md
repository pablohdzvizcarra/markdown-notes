#TDD Test Drive Development

> Producimos código bien diseñado, probado y bien factorizado en pasos pequeños y verificables

El Test Drive Development lo podemos definir como una técnica en programación, donde antes de desarrollar el código funcional, primero creamos los test para dicho código y después crearemos la implementacion del código

> Puede comenzar a aprender TDD hoy es una de esas cosas que requiere momentos para aprender y toda una vida para dominar

En TDD se sigue un ciclo de 3 pasos:
- Red
- Green
- Refactor

### Paso 1: Think

Debes de pensar en el minimo codigo necesario para crear la prueba, en el cual la primera fase es una preuba fallida, aqui podriamos decir que es donde existe mayor complejidad ya que vas a pensar en algo que aun no existe, imaginaras trabajar sobre algo que no has construido

### Paso 2: Red

Aqui crearemos el test para dicha funcionalidad que aun no existe, deberemos de hacerlo de la manera mas abstracta posible, este test debe de fallar ya que el codigo sobre el cual se ejecutara dicho test aun no ha sido creado y por tal razon tendremos una prueba **red** que falla 

### Paso 3: Green

En este paso debemos de crear el codigo de produccion necesario, pero asegurandonos que solo sea el minimo codigo para que la prueba pase.
no te dedes de preocupar en este punto por escribir un codigo de calidad solo asegurate de que tu preuba tenga un **green** que quiere decir que a pasado dicha funcionalidad


### Pase 4: Refactor

En este paso podemos ahora si escribir un codigo de calidad y aplicar todas las practicas de buen codigo que deseemos, siempre y cuando ejecutemos la prueba cada vez que elaboremos algun cambio, tratando de hacer los cambios lo mas pequeños posibles, esto es importante ya que si al momento de refactorizar el codigo cometemos algun error el test deberia de fallar y podemos regresarlo a su estado anterior con facilidad podemos refactorizar el codigo tanto como querramos

*Recuerde las refactorizaciones no deben cambiar el comportamiento. el nuevo comportamiento requiere una prueba fallida*

### Paso 5: Repeat

Cuando este listo para agregar un nuevo comportamiento, comience el ciclo nuevamente
> La clave para TDD son pequeños incrementos

##### La velocidad importa

Asegurate de que tus pruebas se ejecuten de una manera rapida (menos de 10s), por que estaras ejecutandolas constantemente

- Unit Test: deben ejecutarse de manera muy rapida
- Integration Test: normalmente tardan mas tiempo en ejecutarse
- Test End To End: estas son las que tardan mas tiempo en ejecutarse ya que pruebas toda la aplicacion desde un punto a a un punto b

## Unit Test

Los test unitarios se ejecutan de una manera bastante rapida, si no se pueden ejecutar rapido no son test unitarios mas bien deberias considerarlos de integracion

Si un test unitario requiere hacer acciones tales como:
- comunicarse con una base de datos
- comunicarse con la red
- tener que operar con el sistema de archivos
- tener dependencias hacia bibliotecas de terceros

Deberia considerarlo como test de integraciona

Existen muchas maneras de aislar el codigo del test aunque tengas tales impedimentos para considerar tu test de tipo **unitario**, pero realmente deberias de hacer que la implementacion real no tenga tanto acoplamiento entre otras funcionalidades

## Integration Test

Siempre vamos a requerir pruebas de integracion para nuestro proyecto, debemos de escribirlas pensando en que solo deben de tener una interaccion con el mundo exterior

La cantidad de preubas de integracion que deberia tener su programa debe ser proporcional a las interacciones que tiene su programa con el mundo exterior, en cambio los test **unitarios** deben ser proporcionales al tamaño de la aplicacion

#### Pipeline compilation
> Build -> Test -> Provide infrastructure -> Deploy -> Test More


## Que es un prueba unitaria?

si se trabaja en una forma funcional podemos decir que una unidad es una funcion, las pruebas unitarias llamaran a la funcion con diferentes parametros y se verificaran los diferentes resultados.

En un lenguaje orientado a objetos una unidad puede varias desde un solo metodo hasta una clase completa

**Unitarias Solitarias:**

Son aquellas en las cuales todo lo que sea una dependencia es burlado 

**Unitarias Sociales:**

Aquellos en las cuales las dependencias se dejan en su implementacion original

Dependiendo del tipo de desarrollo que elabores deberas decidir si puedes ejecutar las dependencias reales o elaborar burlas a ellas

### Estructura de una buena prueba

Una buena estructura para todas sus pruebas sería la siguiente:
* configurar los datos de prueba
* llame a su method, class o function bajo prueba
* afirmar que se devuelven los resultados esperados

## ¿Qué es una Prueba de Integracion?

Esta pruebas son cuando nuestro codigo interacctua con elementos del mundo exterior tales como bases de datos, la red, el sistema de archivos

*Ejemplo de prueba de integracion con llamado a una base de datos:*

1. iniciar una base de datos
2. conecta tu aplicación a la base de datos
3. desencadena una function dentro del código que escriba los datos en la database
4. verifique que los datos esperados se hayan escrito en la base de datos leyendo los datos de la base de datos

Algunos ejemplos de pruebas de integracion
* Llamadas a las API REST de sus servicios
* Leer y escribir en la database
* Llamar a las API de otras aplicaciones
* Leer y escribir en colas
* Escribir en el sistema de archivos

