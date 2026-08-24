# Parte 2: El Grimorio del Mago – Dominando los Fundamentos de REST

## Capítulo 6: Restricciones de Diseño REST y Modelos de Madurez

Este capítulo profundiza en los aspectos específicos del diseño de APIs, examinando los principios fundamentales que guían el diseño de APIs RESTful tal como fueron introducidos originalmente por **Roy Fielding**. Aquí exploraremos las principales restricciones de diseño REST que dan forma a las APIs eficaces en la actualidad y en los años venideros. Este capítulo también presentará el **Modelo de Madurez de Richardson (*Richardson Maturity Model* / RMM)** y el **Modelo de Madurez de Diseño de APIs Web (*Web API Design Maturity Model* / WADMM)**, proporcionando una hoja de ruta para evaluar y mejorar la madurez de los diseños de API. Es una lectura obligatoria para cualquiera que busque crear APIs robustas, escalables y fáciles de mantener.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **El protocolo HTTP**
- **Restricciones de diseño de APIs REST**
- **Modelos de madurez del diseño de APIs**
- **Cómo evaluar y mejorar la madurez de tu API**

Al finalizar este capítulo, serás capaz de determinar el conjunto de restricciones que te ayudarán a garantizar el diseño de una API madura.

---

### Requisitos técnicos

Para aprovechar al máximo este capítulo, debes estar familiarizado con el protocolo HTTP y con la Notación de Objetos de JavaScript (*JavaScript Object Notation* / JSON).

---

### El protocolo HTTP

El protocolo HTTP sirve como base para la comunicación de datos en la World Wide Web. Es el protocolo más extendido que se utiliza hoy en día para el intercambio de datos. Aunque no es formalmente obligatorio para las APIs REST, casi todas ellas utilizan HTTP como protocolo de intercambio. En este libro continuaremos con este enfoque. Comprender los fundamentos de HTTP es crucial para razonar sobre las restricciones de diseño REST y los modelos de madurez. Si bien asumimos que estás familiarizado con los conceptos básicos del protocolo HTTP, recapitulemos brevemente sus aspectos más importantes.

#### Características del protocolo HTTP

Echemos un vistazo más de cerca a las características del protocolo HTTP:

- **Comunicación cliente-servidor**: HTTP opera como un protocolo cliente-servidor. Las peticiones son iniciadas por el cliente —normalmente un navegador web o una aplicación— y se envían a un servidor. Luego, el servidor procesa la petición y responde al cliente. Esta característica enfatiza la independencia del cliente respecto del servidor, permitiendo que ambos evolucionen por separado.
- **Falta de estado (*Statelessness*)**: Cada petición del cliente al servidor contiene toda la información necesaria para completar la solicitud. El servidor no almacena ninguna información de sesión ni la requiere para el procesamiento.
- **Almacenamiento en caché (*Caching*)**: Las peticiones y respuestas pueden ser almacenadas en caché por el cliente para mejorar el rendimiento. Las respuestas en caché se pueden reutilizar cuando se realizan peticiones idénticas, lo que mejora el rendimiento general del sistema.
- **Interfaz uniforme**: HTTP se basa en una interfaz uniforme, lo que simplifica la arquitectura. Cada petición HTTP incluye un identificador de recurso, un método y metadatos. También puede contener otros elementos, como parámetros de consulta (*query parameters*).
- **Sistema en capas (*Layered system*)**: Los clientes no son conscientes del origen de la respuesta, ya sea que provenga directamente del servidor final, de un proxy inverso o de otro elemento intermediario. Este enfoque por capas permite flexibilidad y escalabilidad.
- **Extensibilidad**: HTTP es un protocolo extensible que ha evolucionado en múltiples ocasiones. Sirve para varios propósitos, incluida la recuperación de documentos HTML (sitios web), imágenes y videos, y permite la manipulación de contenido en servidores. Actualmente, varias iteraciones de HTTP conviven en paralelo, como HTTP/1.1, HTTP/2 y HTTP/3. Más adelante en este capítulo analizaremos los pros y los contras de estas versiones más nuevas.

En la sección de restricciones de diseño de APIs REST, exploraremos cuán estrechamente se alinean estas características. A continuación, profundizaremos en la estructura de una petición HTTP, destacando sus elementos principales.

#### La estructura de una petición y respuesta HTTP

El patrón de comunicación en HTTP se compone de una petición procedente del cliente, seguida de una respuesta del servidor, como se detalla en la Figura 6.1. Siempre siguen la misma estructura, y en esta sección repasaremos cada uno de ellos y nos centraremos en los detalles más importantes relativos a REST.

*Figura 6.1: Elementos del protocolo HTTP*

Si recordamos la característica de interfaz uniforme del protocolo HTTP, podemos ver cómo las peticiones y respuestas HTTP se relacionan con ella. Podemos distinguir los siguientes elementos en las peticiones y respuestas HTTP:

- Un **URI**, el identificador del recurso, que también puede contener parámetros de consulta
- Un **método HTTP** que especifica el tipo de operación realizada sobre el recurso
- **Cabeceras de petición (*Request headers*)** que contienen metadatos de la solicitud
- Un **cuerpo (*Payload*)**, que es el objeto de datos que enviamos al servidor
- **Códigos de respuesta (*Response codes*)** que indican el resultado de la petición

A continuación se muestra un ejemplo de una petición:

```http
POST https://api.magicstore.com/products
Content-Type: application/json
Authorization: Bearer your_access_token

{
  "name": "Magic Wand",
  "price": 29.99,
  "category": "Wands"
}
```

Aquí está la respuesta:

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: https://api.magicstore.com/products/12345

{
  "id": "12345",
  "name": "Magic Wand",
  "price": 29.99,
  "category": "Wands",
  "available": true
}
```

> **Consejo rápido**: Mejora tu experiencia de programación con las funciones AI Code Explainer y Quick Copy. Abre este libro en el lector Packt Reader de última generación. Haz clic en el botón Copiar (1) para copiar rápidamente el código en tu entorno de desarrollo, o haz clic en el botón Explicar (2) para que el asistente de IA te explique un bloque de código.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

##### URI

El Identificador Universal de Recursos (*Universal Resource Identifier* / URI) es la ubicación de red del recurso. Consta de cinco elementos:

- **Esquema (*Scheme*)**: Identifica el protocolo utilizado para acceder al recurso. En nuestro caso, será HTTPS, que es la versión segura del protocolo HTTP que utiliza SSL o TLS para cifrar los datos transferidos. HTTPS también utiliza un puerto predeterminado diferente para la comunicación (443 en lugar de 80).
- **Autoridad (*Authority*)**: Especifica el host bajo el cual nuestro recurso está disponible. La autoridad también puede contener información del usuario (seguida de `@`), pero esto no se utiliza en las APIs REST.
- **Puerto (*Port*)**: Otro elemento de la autoridad (precedido por `:`). También es opcional, ya que los protocolos HTTP y HTTPS utilizan un número de puerto predeterminado. Los números de puerto personalizados son principalmente relevantes en entornos locales y de preproducción.
- **Ruta (*Path*)**: Identifica el recurso específico al que apunta la URI. Siempre es relativa al host.
- **Parámetros de consulta (*Query parameters*)**: Precedidos por el carácter `?`. Se suelen utilizar para pasar parámetros en la solicitud, como filtros.

##### Métodos HTTP

Los métodos HTTP se utilizan en la interacción entre un cliente y un servidor. Especifican qué tipo de acción se va a realizar en el servidor. Por ejemplo, `GET https://api.magicstore.com/wizards` solicitará recuperar el conjunto de magos (el recurso) desde el host `api.magicstore.com`.

##### Idempotencia (*Idempotency*)

Antes de revisar cada método HTTP, debemos introducir un concepto importante: la **idempotencia**. Este concepto es fundamental en el contexto de las APIs, especialmente en lo que respecta a sus métodos. En resumen, las peticiones idempotentes se pueden realizar varias veces y darán los mismos resultados en cada ocasión. No afectan al servidor de una manera que dé lugar a un resultado diferente para una petición idéntica posterior. Esto es especialmente importante en el contexto de la seguridad, ya que mejora la tolerancia a fallos. También garantiza la alineación entre sistemas: sabemos que las mismas peticiones nos darán los mismos resultados.

Los siguientes son los métodos HTTP principales utilizados en el contexto de una API REST:

- **GET**: Se utiliza para recuperar datos de un servidor. Es una operación de solo lectura, por lo que no cambia nada en el servidor. `GET` es idempotente ya que no altera el estado del servidor de manera que dé resultados diferentes para los mismos datos.
- **HEAD**: Es muy similar a `GET`, con una diferencia crucial: no solicita el cuerpo (*payload*) de la respuesta y, en su lugar, se utiliza para recuperar solo los metadatos (cabeceras) de la petición. Al igual que `GET`, también es idempotente.
- **POST**: Se utiliza para enviar datos a un servidor con el fin de crear un nuevo recurso. Puede crear una nueva instancia de un recurso o iniciar un proceso. `POST` no es un método idempotente, ya que la creación de un nuevo recurso dará un resultado diferente en el servidor cada vez (por ejemplo, un nuevo ID).
- **PUT**: Se utiliza para actualizar o reemplazar un recurso en el servidor. La petición debe contener el objeto completo que se va a actualizar, ya que el cuerpo de `PUT` sobrescribirá el recurso existente con los datos que envía. Es un método idempotente, ya que siempre dará los mismos resultados, independientemente del estado actual del recurso que sobrescribe.
- **PATCH**: A diferencia de `PUT`, que sobrescribe completamente un objeto de recurso, este método se utiliza para aplicar modificaciones parciales a un recurso en el servidor. El cliente envía solo los cambios al servidor. En el contexto de las APIs, existen dos formas diferentes de implementar el método `PATCH`, las cuales se explicarán en breve. Este método no es idempotente por defecto, pero puede serlo si se implementa de manera idempotente.
- **DELETE**: Se utiliza para eliminar un recurso en el servidor. Una vez eliminado un recurso, no se puede eliminar de nuevo. Esto significa que el estado resultante del servidor no cambiará tras la eliminación inicial, lo que hace que `DELETE` sea idempotente.
- **OPTIONS**: Al igual que `GET`, recupera datos del servidor. Sin embargo, a diferencia de `GET`, que recupera una representación de un recurso, `OPTIONS` recupera qué tipo de otros métodos HTTP se pueden realizar sobre un recurso. Dado que esta operación no cambia el estado del servidor, también es idempotente.

##### JSON Patch y JSON Merge Patch

Son dos estándares diferentes para la implementación del método `PATCH`. JSON Patch (RFC 6902) y JSON Merge Patch (RFC 7396) se utilizan habitualmente en APIs REST para actualizar parcialmente recursos en formato JSON.

**JSON Patch** representa la actualización como una serie de operaciones que deben aplicarse al documento de origen. Cada operación se representa como un objeto JSON y la serie de operaciones se representa como un array de estos objetos. He aquí un ejemplo:

```json
[
  { "op": "replace", "path": "/class", "value": "Wizard" },
  { "op": "remove", "path": "/hero/name" }
]
```

Este enfoque es muy flexible y puede representar modificaciones complejas, pero también puede ser más difícil de escribir y comprender. También puede dar lugar a cuerpos de solicitud muy extensos en el caso de actualizaciones grandes con muchas operaciones.

Sin embargo, JSON Patch no es inherentemente idempotente para varias operaciones. El uso de la operación `add` para agregar elementos a arrays sin especificar índices puede causar duplicación:

```json
{"op": "add", "path": "/effects", "value": "healing"}
```

Esto transforma `[]` en `["healing"]` la primera vez, y luego en `["healing", "healing"]` cuando se ejecuta de nuevo.

Asimismo, mover elementos repetidamente puede causar cambios en cascada:

```json
{ "op": "move", "from": "/powers", "path": "/effects" }
```

Esta operación no es idempotente, ya que una segunda aplicación fallaría dado que el origen ya no existe.

A pesar de estas limitaciones, JSON Patch se puede implementar de forma idempotente:
- Utiliza la operación `test` para verificar el estado actual antes de aplicar modificaciones:
```json
[
  { "op": "test", "path": "/powers", "value": "healing" },
  { "op": "move", "from": "/powers", "path": "/effects" }
]
```
Este enfoque garantiza que la operación `move` se realice únicamente cuando el valor de `powers` sea igual a `healing`, según lo establecido en la condición previa.
- Apunta a índices específicos al realizar la operación `add` en un array:
```json
{ "op": "add", "path": "/potions/0", "value": "Potion of Healing" }
```
Esto añade previsibilidad a las operaciones con arrays y garantiza que siempre sean idempotentes.

**JSON Merge Patch** aborda el cambio de manera diferente. En este enfoque, el cliente solo envía una parte del cuerpo JSON del recurso que desea actualizar. Esta parte solo incluye las actualizaciones que el cliente desea realizar: modificaciones, adiciones o eliminaciones. Los parámetros que el cliente desea eliminar se representan con un valor `null`. He aquí un ejemplo:

```json
{
  "class": "Wizard",
  "hero": {
    "name": null
  }
}
```

Este enfoque es más sencillo e intuitivo que JSON Patch. También es un enfoque mucho más común. Además, JSON Merge Patch es naturalmente idempotente. Sin embargo, también presenta algunas limitaciones, como la incapacidad de modificar valores dentro de un array.

En resumen, JSON Patch es más potente y flexible, mientras que JSON Merge Patch es más simple, fácil de usar e idempotente por defecto. La elección entre ambos depende de los requisitos específicos de tu aplicación, como la necesidad de operar sobre elementos específicos de un array.

##### Cabeceras HTTP (*HTTP Headers*)

Las cabeceras HTTP transportan los metadatos de las peticiones y de las respuestas. Su estructura consta de pares clave-valor. Podemos dividir las cabeceras en las siguientes áreas:

- **Cabeceras de petición (*Request headers*)**: Transportan información sobre el recurso que se va a recuperar o sobre el cliente.
- **Cabeceras de respuesta (*Response headers*)**: Contienen información como la ubicación de la respuesta y el servidor que la proporciona, así como la instancia del recurso (por ejemplo, `ETag`).
- **Cabeceras de representación (*Representation headers*)**: Proporcionan información sobre el cuerpo del recurso. Se utilizan para la negociación de contenido y propósitos similares.
- **Cabeceras de carga útil (*Payload headers*)**: Contienen información sobre el tamaño del cuerpo, la codificación y más.

Para las APIs REST, las cabeceras utilizadas para autorización y autenticación son especialmente comunes. Ten en cuenta que la negociación de contenido y el control de almacenamiento en caché también se pueden especificar mediante cabeceras.

##### Códigos de respuesta HTTP (*HTTP Response Codes*)

Los códigos de respuesta se encargan de indicar el resultado de la petición HTTP de una forma sencilla y estandarizada. Constan de un código de tres dígitos y una descripción de la naturaleza del código. Los códigos de respuesta se agrupan en cinco clases:

- **1xx (Informativo)**: Comunican información a nivel de protocolo de transferencia. No se utilizan en REST.
- **2xx (Éxito)**: Indican una petición procesada con éxito.
- **3xx (Redirección)**: Notifican al cliente sobre acciones adicionales requeridas para completar la petición (por ejemplo, un proceso de larga duración o una redirección a otro host).
- **4xx (Error del cliente)**: Notifican al cliente que hubo un problema con la petición en el lado del cliente (petición mal formada, falta de derechos de autorización, etc.).
- **5xx (Error del servidor)**: Especifican que el error fue causado por el servidor (excepción no controlada en el servidor, tiempo de espera agotado, etc.).

En general, estos códigos nos ayudan a comprender qué ha sucedido. Debido a su naturaleza estandarizada, facilitan la programación adecuada de la aplicación cliente para que pueda reaccionar correctamente según lo ocurrido con la petición.

##### HTTP/2 y más allá

Como se mencionó anteriormente, HTTP es un protocolo extensible que continúa evolucionando. Aun así, la versión más común del protocolo HTTP, y la que sirve de base para todas las versiones posteriores hoy en día, es HTTP/1.1. HTTP/2 y HTTP/3 son versiones más recientes del protocolo HTTP que ofrecen mejoras de rendimiento con respecto a HTTP/1.1:

- **HTTP/2**: Introduce varias mejoras de rendimiento, como multiplexación, compresión de cabeceras y *server push*. La multiplexación permite enviar múltiples peticiones en paralelo a través de una única conexión TCP, la compresión de cabeceras reduce su tamaño y el *server push* permite que el servidor envíe al cliente recursos que aún no ha solicitado. En ciertos escenarios, estas características pueden generar ganancias significativas de rendimiento. Además, HTTP/2 y HTTP/3 son protocolos binarios (en lugar de textuales), lo que conduce a una mayor fiabilidad en la transferencia de datos.
- **HTTP/3**: Su principal diferencia respecto a HTTP/1.1 es el uso de **QUIC** como protocolo de capa de transporte. QUIC utiliza UDP en lugar de TCP. Esto puede resultar en tiempos de conexión más rápidos y un mejor manejo de la pérdida de paquetes, lo que puede resultar beneficioso para las APIs REST, especialmente en entornos móviles o de alta latencia.

Es importante destacar que adoptar HTTP/2 o HTTP/3 no requiere ningún trabajo adicional desde el punto de vista del diseño de APIs; esto lo gestionan el servidor de aplicaciones y la red.

En esta sección, hemos hablado sobre el protocolo HTTP y su importancia para las APIs REST. También hemos señalado que una petición y respuesta HTTP constan de:
- El identificador del recurso (URI)
- El método HTTP, que especifica la acción a tomar
- Las cabeceras HTTP, que contienen los metadatos
- Los cuerpos de petición y respuesta, que transportan los datos
- Los códigos de respuesta HTTP, que informan al cliente sobre los resultados de la petición

En la siguiente sección, nos centraremos en las restricciones de diseño de las APIs REST, donde veremos qué tan similares son la mayoría de estas restricciones a las características del protocolo HTTP.

---

### Restricciones de diseño de APIs REST

Tras haber revisado los entresijos del protocolo HTTP, podemos comenzar a analizar el estilo arquitectónico y las restricciones de las APIs REST. Esto actuará como base para todas las discusiones posteriores sobre el diseño de APIs REST.

De todos los estilos arquitectónicos de API disponibles, REST y sus derivados son los más comunes. Esto significa que también es el más probado y respaldado por la experiencia. Un gran ejemplo de una arquitectura de estilo REST implementada a gran escala es la **World Wide Web**. Creada en 1992, es anterior a REST. Puedes pensar en la World Wide Web como una implementación a gran escala de los principios de REST, utilizando HTTP como su protocolo y los navegadores web como clientes. REST se abstrajo de la arquitectura de la World Wide Web para describir un espectro más amplio de aplicaciones, pero utilizar la World Wide Web como ejemplo nos ayuda a razonar sobre REST.

Las APIs REST fueron propuestas originalmente por **Roy Thomas Fielding** en su disertación doctoral de 2000 titulada *Architectural Styles and the Design of Network-based Software Architectures*. Fue un trabajo fundamental que resultó ser el principio arquitectónico clave para la World Wide Web. En su documento, Fielding define REST utilizando el Estilo Nulo (*Null Style*) y construye sobre él un conjunto de restricciones que definen el estilo arquitectónico REST. Como se evidencia, las restricciones de REST son las mismas que las características del protocolo HTTP enumeradas anteriormente. Sin embargo, dado que el contexto de las APIs REST es más específico, examinemos cada una de estas restricciones una por una.

#### Cliente-servidor (*Client-server*)

Básicamente, esta restricción significa que las aplicaciones cliente y servidor deben poder evolucionar por separado, sin ninguna dependencia entre sí. Un cliente solo necesita conocer el identificador del recurso (dirección). Por ejemplo, una aplicación cliente, como una aplicación móvil, se conecta a un servidor para recuperar datos; la única información que necesita para iniciar el proceso de recuperación es la dirección del servidor y la ubicación del recurso que busca dentro del servidor. Esto permite la evolución independiente tanto del servidor como de las aplicaciones cliente. Los clientes pueden crecer en términos de funcionalidades mientras el servidor permanece igual. Los servidores y los clientes también pueden ser reemplazados y desarrollados de forma independiente siempre que la interfaz entre ellos no se altere. Esto promueve la flexibilidad y la escalabilidad en el sistema, respaldando así el requisito a escala de internet de múltiples dominios organizacionales.

#### Sin estado (*Stateless*)

Esta restricción significa que las peticiones de los clientes deben contener toda la información necesaria para que el servidor las entienda, sin aprovechar ningún tipo de contexto almacenado en el servidor. Esto también implica que los servidores deben incluir toda la información necesaria en su respuesta para que los clientes puedan mantener el estado en su lado si es necesario. *«Esta restricción induce las propiedades de visibilidad, fiabilidad y escalabilidad»*. Los sistemas de monitorización no tienen que recuperar ninguna información adicional sobre una petición individual, ya que es autónoma. La fiabilidad también mejora porque recuperarse de los fallos es más sencillo. Además, los sistemas sin estado son más fáciles de escalar debido a la gestión simplificada de estados y recursos.

#### Almacenable en caché (*Cacheable*)

Esta restricción se añade para mejorar la eficiencia de red en la comunicación. Requiere que los datos en respuesta a una petición específica se etiqueten como almacenables o no almacenables en caché. Esto puede ser explícito o implícito:
- El etiquetado explícito se basa en establecer cabeceras de metadatos específicas.
- El etiquetado implícito se basa en las características del protocolo HTTP. Las respuestas a peticiones `GET` son almacenables en caché por defecto, mientras que las peticiones `POST` no lo son y requieren un etiquetado explícito. Las peticiones `PUT` y `DELETE` no son almacenables en caché en absoluto.

Los datos en caché se almacenan en varios lugares a lo largo de la ruta de petición-respuesta (caché local, caché de proxy o proxy inverso). Si alguna de las cachés contiene una copia actualizada de la representación solicitada, utiliza esa copia para satisfacer la petición; si ninguna puede satisfacerla, la petición viaja hasta el servicio (servidor de origen).

Aprovechar el almacenamiento en caché ofrece varios beneficios:
- Reduce el ancho de banda al utilizar la profundidad limitada de la red
- Reduce la latencia de petición-respuesta al servir los datos desde el elemento de red más cercano que contenga datos en caché
- Reduce la carga en los servidores utilizando datos en caché (no todas las peticiones llegarán al servidor)
- Oculta fallos de red sirviendo datos en caché en su lugar

> **Nota**  
> Las respuestas almacenables en caché (ya sea a una petición `GET` o `POST`) deben incluir un validador: una cabecera `ETag` o `Last-Modified`. Un `ETag` es una cabecera que contiene un valor de token que un servidor asocia con un estado específico de un recurso. Esto significa que si algo relacionado con el recurso solicitado cambia, el valor del `ETag` también cambia (piensa en ello como un sello único). Comparar los valores del `ETag` te dirá si dos representaciones del mismo recurso son idénticas. La cabecera `Last-Modified` cumple la misma función, pero su valor es una marca de tiempo (*timestamp*) en lugar de un token.

En resumen, la restricción de almacenamiento en caché promueve un diseño desacoplado y escalable, lo que mejora la usabilidad y el mantenimiento de las APIs.

#### Interfaz uniforme (*Uniform interface*)

Esta restricción simplifica y desacopla la arquitectura. Esto, a su vez, permite que cada parte de la arquitectura del sistema evolucione de forma independiente. Existen cuatro principios fundamentales de la interfaz uniforme:

1. **Identificación de recursos**: Cada recurso se identifica en las peticiones mediante un identificador único. En el caso de HTTP, este es un URI. Un recurso puede ser cualquier entidad sobre la cual la API pueda proporcionar información. Por ejemplo, en una tienda electrónica, podríamos tener un usuario, un pedido y un producto, y cada una de estas entidades sería un recurso. Los identificaríamos en el sistema como `Users`, `Orders` y `Products` y los almacenaríamos bajo URIs específicas, como `https://api.e-store.com/users`, `https://api.e-store.com/orders` y `https://api.e-store.com/products`. Esta restricción enfatiza que todas las interacciones con la API se realizan a través de estas URIs.
2. **Manipulación de recursos mediante representaciones**: REST se comunica transfiriendo una representación de un recurso en un formato que el cliente pueda entender. Esto significa que las respuestas del servidor coincidirán con el formato de metadatos incluido en la petición y la representación del recurso deseado. Esto suele proporcionarse a través de la **negociación de contenido** y se aplica tanto a la lectura de datos en un formato adecuado como a la escritura de datos en el servidor. La representación que se devuelve al cliente o se guarda en el servidor prácticamente nunca es idéntica a los datos almacenados en el servidor (una excepción podría ser recuperar o enviar archivos de registro específicos). Esto no solo es aplicable al formato de datos (por ejemplo, JSON, XML, CSV, etc.) o al idioma, sino también a los datos en sí. Las representaciones tienen como objetivo enviar solo el subconjunto de datos requerido por el cliente y no exponen ninguna información interna o específica de la implementación.
   > **Negociación de contenido (*Content negotiation*)**  
   > Permite que clientes y servidores acuerden la representación del recurso solicitado. Asegura que los clientes reciban datos en un formato comprensible. Suele ser guiada por el cliente mediante cabeceras como `Accept`, que especifica qué formatos comprende el cliente (JSON, XML, etc.), idioma deseado, formato de fechas, etc. Aprenderemos más sobre esto en el Capítulo 12.
3. **Mensajes autodescriptivos (*Self-descriptive messages*)**: Cada mensaje debe incluir suficiente información para describir cómo procesarlo. Dicha información debe incluirse en los metadatos de las cabeceras. Esto se relaciona estrechamente con la restricción sin estado. Un mensaje autodescriptivo normalmente incluye el método HTTP que describe la acción a realizar sobre el recurso, el identificador del recurso, cabeceras que proporcionan metadatos sobre el mensaje y un cuerpo que contiene la representación del recurso (si corresponde).
4. **Hipermedia como Motor del Estado de la Aplicación (*Hypermedia as the Engine of Application State* / HATEOAS)**: Este principio garantiza que una API REST proporcione enlaces de hipermedia a recursos y acciones relacionados dentro de las respuestas de los recursos. Su objetivo es hacer que las APIs sean más autodescriptivas y descubribles. HATEOAS permite a los clientes navegar por la API sin ningún conocimiento previo de la misma. Este principio es el más divisivo y ha generado mucho debate sobre qué puede llamarse una verdadera API REST y qué no. La mayoría de las APIs REST que vemos no incluyen controles de hipermedia, principalmente por dos razones:
   - Es más difícil diseñar APIs de hipermedia, ya que todas las representaciones de recursos deben proporcionar información relevante sobre los recursos relacionados, cubriendo todo el espacio de la API.
   - Surgen complicaciones adicionales con el control de acceso granular y la complejidad de crear clientes que aprovechen bien los controles HATEOAS.  
   HATEOAS ofrece muchos beneficios, pero tiene un costo. Te recomendamos diseñar tus APIs teniendo en cuenta la hipermedia, pero teniendo siempre presentes los casos de uso específicos. Dedicamos el Capítulo 12 a las APIs de hipermedia.
   > **HATEOAS y la Inteligencia Artificial**  
   > A pesar de su historial conflictivo, las APIs de hipermedia serán especialmente importantes en los próximos años. Su mayor inconveniente —ser difíciles de aprovechar por los clientes humanos/tradicionales— se está volviendo irrelevante rápidamente con la aparición de IAs que utilizan modelos de lenguaje grandes (LLMs). Además, dado que una de las funcionalidades centrales de esos sistemas de IA proviene de conectarse a varias APIs Web, los sistemas que sean fácilmente descubribles y navegables jugarán un papel mucho más importante (ver Capítulo 11).

#### Sistema en capas (*Layered system*)

Esta restricción establece que puede haber múltiples capas entre el cliente y el servidor que aloja el recurso (elementos de red como caché, balanceador de carga, proxy, firewall, etc.). El cliente no puede saber si la respuesta proviene directamente del servidor o si ha sido entregada a través de capas intermediarias. Este enfoque arquitectónico proporciona los siguientes beneficios:

- **Modularidad**: Las capas se pueden agregar, eliminar, actualizar o reemplazar de forma independiente sin afectar al tráfico.
- **Escalabilidad**: Los balanceadores de carga pueden distribuir las peticiones entre múltiples instancias de servidor, lo que hace posible el escalado horizontal.
- **Seguridad**: Los firewalls pueden proporcionar una capa adicional de seguridad.
- **Almacenamiento en caché**: La capa de caché permite cumplir la restricción de almacenamiento en caché en la capa de red.

Sin embargo, tener demasiadas capas puede añadir latencia adicional y complejidad. La mayoría de las APIs actuales cuentan con una capa de proxy inverso en forma de **API Gateway** y un balanceador de carga entre los servidores y el proxy inverso (ver Capítulo 13).

#### Código bajo demanda (*Code on demand* - opcional)

Esta restricción opcional permite a los servidores ampliar o personalizar la funcionalidad del cliente respondiendo con código ejecutable. Este código se envía habitualmente en forma de scripts (por ejemplo, JavaScript) para que los ejecute la aplicación cliente. Puede simplificar el cliente reduciendo la cantidad de funcionalidades a implementar. Sin embargo, puede reducir la visibilidad en el lado del cliente al depender demasiado del servidor, aumentando el acoplamiento. Esta restricción es muy poco común en las APIs actuales, especialmente en APIs públicas.

---

### Madurez de las APIs (*API Maturity*)

Al diseñar APIs, nos adherimos a un determinado conjunto de reglas: las restricciones de diseño del estilo arquitectónico elegido (en nuestro caso, REST) y directrices adicionales como buenas prácticas de la industria o reglas internas de la organización.

En esta sección examinamos dos modelos para evaluar la madurez del diseño de APIs:
1. **Modelo de Madurez de Richardson (*Richardson Maturity Model* / RMM)**: Evalúa qué tan estrechamente se alinea una API con las restricciones del estilo arquitectónico REST.
2. **Modelo de Madurez de Diseño de APIs Web (*Web API Design Maturity Model* / WADMM)**: Se centra en evaluar qué tan centrada en el cliente es una API mediante el diseño de su modelo de documentos.

#### ¿Por qué es importante?

Tener un conjunto de reglas que vaya más allá de las meras restricciones arquitectónicas es muy importante para el diseño de APIs. Seguir directrices estrictas hace que nuestras APIs sean más predecibles, estandarizadas y ofrezcan una mejor experiencia de desarrollador (DX). El modelo de diseño influye en la estabilidad y usabilidad de la API a lo largo del tiempo. En un ecosistema compuesto por múltiples APIs interdependientes, la fiabilidad depende tanto de los aspectos técnicos como de la previsibilidad.

#### RMM: Modelo de Madurez de Richardson

RMM es un modelo propuesto por **Leonard Richardson** en 2008. Evalúa si las APIs se ajustan a las restricciones de diseño del estilo REST analizando tres factores centrales:

- Identificadores de recursos (URIs)
- Métodos HTTP
- Controles de hipermedia

*Figura 6.2: RMM (https://martinfowler.com/articles/richardsonMaturityModel.html)*

RMM clasifica las APIs en cuatro niveles de madurez:

##### Nivel 0: El pantano de POX (*The Swamp of POX*)

POX significa *Plain Old XML* y se refiere a la clase de APIs que operan en un único *endpoint*. Estas APIs aceptan todas las operaciones admitidas por el servicio en cada recurso de la API. Las APIs SOAP y GraphQL caen bajo esta categoría (suelen tener un solo *endpoint*, utilizan únicamente el método `POST` para todas las operaciones y siempre devuelven una respuesta `200 OK`, rompiendo la semántica del protocolo HTTP). Los sistemas de Nivel 0 no se clasifican como RESTful.

Petición de ejemplo:
```http
POST https://api.magicstore.com/shop
Content-Type: application/json

{
  "function": "readProducts",
  "arguments": [
    "available"
  ]
}
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "result": {
    "products": [
      "wizard hat",
      "magic weapon"
    ]
  }
}
```

##### Nivel 1: Recursos (*Resources*)

En el Nivel 1, comenzamos a operar sobre recursos. Una API en este nivel introduce URIs diferenciadas para recursos individuales, pero sigue violando las restricciones del protocolo HTTP al depender exclusivamente de `POST` para todas las acciones e ignorar los códigos de respuesta estándar (muy común en APIs RPC, que también favorecen URIs orientadas a la acción como `/purchase-order/start`). Aunque el Nivel 1 comienza a organizar los recursos, aún no cumple con las restricciones arquitectónicas de REST.

Petición de ejemplo:
```http
POST https://api.magicstore.com/products
Content-Type: application/json

{
  "op": "read",
  "arguments": ["available"]
}
```

Respuesta:
```http
HTTP/1.1 200 OK

{
  "products": ["wizard hat", "magic weapon"]
}
```

##### Nivel 2: Verbos HTTP (*HTTP Verbs*)

Aquí es donde comenzamos a hablar de APIs que normalmente denominamos **RESTful**. Las APIs de Nivel 2 de RMM aprovechan la estructura del protocolo HTTP más plenamente mediante el uso de URIs específicas de recursos, métodos HTTP apropiados (`GET` para leer, `PUT` para reemplazar, etc.) y respuestas significativas con códigos de estado estandarizados.

Existe un debate continuo sobre si las APIs en este nivel pueden considerarse REST o no, ya que no siguen la restricción HATEOAS. Sin embargo, el consenso predominante es que las APIs de Nivel 2 de RMM se denominan comúnmente RESTful en la práctica.

Petición de ejemplo:
```http
GET https://api.magicstore.com/products?available=true
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "products": [
    "wizard hat",
    "magic weapon"
  ]
}
```

Al utilizar `GET`, la respuesta puede ser almacenada en caché por navegadores, proxies y otros intermediarios, mejorando el rendimiento. Sin embargo, aún carece de controles de hipermedia, por lo que los clientes deben recurrir a documentación externa para descubrir acciones posteriores.

##### Nivel 3: Controles de hipermedia (*Hypermedia Controls* / HATEOAS)

Este es el nivel del «santo grial» para las APIs REST. Una API en este nivel cumple con todas las restricciones de diseño de APIs REST, incluido el uso de controles de hipermedia.

Además del uso adecuado de métodos HTTP y URIs de recursos (Nivel 2), las APIs de Nivel 3 incrustan enlaces en sus respuestas, lo que permite a los clientes descubrir recursos relacionados y acciones disponibles de forma dinámica. Esto reduce el acoplamiento entre clientes y servidores y permite una navegación fluida, paginación descubrible y transiciones de estado.

Petición de ejemplo:
```http
GET https://api.magicstore.com/products?available=true
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://api.magicstore.com/products?available=true>; rel="self", <https://api.magicstore.com/products?available=true&page=2>; rel="next"

{
  "products": [
    {
      "name": "wizard hat",
      "_links": {
        "self": {"href": "/products/wizardhat"},
        "reviews": {"href": "/products/wizardhat/reviews"}
      }
    }
  ]
}
```

---

#### WADMM: Modelo de Madurez de Diseño de APIs Web

Mientras que RMM se centra en los documentos de respuesta y la adopción de elementos específicos del protocolo HTTP, no cubre el diseño de los modelos de datos expuestos. En 2016, **Mike Amundsen** introdujo WADMM como complemento a RMM para servicios RESTful, enfocándose en la adopción de una descripción de modelo específica para exponer la API. Se relaciona estrechamente con la restricción de la interfaz uniforme: *Manipulación de recursos mediante representaciones*.

*Figura 6.3: WADMM (http://amundsen.com/talks/2016-11-apistrat-wadmm/2016-11-apistrat-wadmm.pdf)*

WADMM clasifica las APIs REST en cuatro niveles de madurez:

##### Nivel 0: Centrado en la base de datos (*Database-centric*)

La API es simplemente el modelo de datos expuesto del servicio (datos sin procesar de la base de datos, incluidos IDs internos, esquemas o información de seguridad). Acopla estrechamente la API con el modelo de base de datos interno; cualquier cambio interno rompe a los clientes.

Petición de ejemplo:
```http
GET https://api.magicstore.com/products?id=98765
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "product_id": "98765",
  "name": "Wizard Hat",
  "price": 15.99,
  "category": "Accessories",
  "db_internal_id": "db12345",
  "business_model_id": "bm67890",
  "security_info": {
    "created_by": "admin",
    "last_modified": "2024-09-28T12:00:00Z"
  },
  "itemCreator": "Pierre O'Gui The Magnificent"
}
```

##### Nivel 1: Centrado en el objeto (*Object-centric*)

Expone el modelo de objetos interno tal como está definido en el lenguaje de programación elegido. Aunque no expone directamente la base de datos, todavía incluye detalles de implementación y sufre de un fuerte acoplamiento entre la implementación y la interfaz de la API.

Petición de ejemplo:
```http
GET https://api.magicstore.com/products/98765
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "product_id": "98765",
  "name": "Wizard Hat",
  "price": 15.99,
  "category": "Accessories",
  "createdBy": "Pierre O'Gui The Magnificent",
  "model": "Product",
  "schema_version": "1.0",
  "_type": "com.magicstore.Product"
}
```

##### Nivel 2: Centrado en el recurso (*Resource-centric*)

Opera en un diseño de interfaz externa que desacopla la API de los modelos de datos internos. Las APIs en este nivel operan sobre un conjunto de recursos HTTP abstractos. Es el nivel habitual de las APIs REST documentadas con OpenAPI Specification (OAS). Sin embargo, muchas APIs en este nivel todavía reproducen operaciones CRUD básicas basadas en la implementación en lugar de orientarse a casos de uso reales del cliente.

Petición de ejemplo:
```http
GET https://api.magicstore.com/products/98765
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "product_id": "98765",
  "name": "Wizard Hat",
  "price": 15.99,
  "category": "Accessories",
  "itemEnchanter": "Pierre O'Gui The Magnificent"
}
```

##### Nivel 3: Centrado en la asequibilidad/posibilidad de acción (*Affordance-centric*)

Es el nivel más alto de madurez en WADMM. Se basa en un modelo de datos completamente externo y desacoplado, enfocado en casos de uso, mensajes y acciones en lugar de simples operaciones CRUD. En las APIs de Nivel 3 de WADMM, *«la información se convierte en la asequibilidad (*affordance*) a través de la cual el usuario obtiene opciones y selecciona acciones»*.

Petición de ejemplo:
```http
GET https://api.magicstore.com/itemEnchanter?product="wizardhat"
```

Respuesta:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "name": "Pierre O'Gui The Magnificent",
  "occupation": "Magic Items Designer",
  "itemsCreated": [
    {
      "_link": "https://api.magicstore.com/products/98765",
      "name": "Wizard Hat"
    }
  ]
}
```

---

### Cómo evaluar y mejorar la madurez de tu API

A continuación se presenta un proceso estructurado en pasos prácticos para evaluar y mejorar la madurez de una API en producción (considerando que los niveles 2 y 3 en ambos modelos son los válidos para REST):

1. **Evalúa tu estado actual**:
   - **Diseño de recursos y URIs**: Satisface la manipulación de recursos mediante representaciones desacopladas del almacenamiento interno (Nivel 2), orientándose a casos de uso del cliente (Nivel 3):
     ```http
     GET /checkout/cart
     ```
   - **Verbos HTTP**: Asegura que los métodos HTTP reflejen su semántica (`GET` para leer, `POST` para crear, `PUT` para reemplazar, `PATCH` para actualizar, `DELETE` para eliminar):
     ```http
     DELETE /orders/98765 # Correcto (RMM L2)
     ```
     Evita situaciones como:
     ```http
     POST /deleteOrder # Incorrecto (RMM L0)
     ```
   - **Códigos de respuesta**: Utiliza códigos HTTP estándar y significativos:
     ```http
     POST /orders # Creación de recurso
     HTTP/1.1 201 Created # Tras la creación
     Location: /orders/98765
     ```
   - **Uso de hipermedia**: Incluye enlaces en las respuestas para alcanzar RMM Nivel 3:
     ```json
     {
       "_links": {
         "self": {
           "href": "/orders/98765"
         },
         "customer": {
           "href": "/customers/456"
         }
       }
     }
     ```
   - **Asequibilidad (*Affordance*)**: Adapta el modelo a las necesidades del cliente y aprovecha la negociación de contenido (WADMM Nivel 3):
     ```http
     GET /products/98765 HTTP/1.1
     Accept: application/xml
     ```
2. **Identifica áreas de mejora**: Compara el estado actual con los objetivos organizacionales para establecer una línea base de actualización.
3. **Crea un plan**: Desarrolla una hoja de ruta según el ciclo de vida de la API.
4. **Implementa los cambios**: Aplica cambios graduales (por ejemplo, Fase 1: añadir enlaces de hipermedia en *endpoints* de alto tráfico como `{"_links": {"next": "/orders?page=2"}}`; Fase 2: declarar obsoletos *endpoints* no RESTful como `/getOrder`).
5. **Monitoriza e itera**: Mide métricas reales (adopción de nuevos *endpoints*, reducción de errores) y ajusta continuamente.

---

### Resumen

Este capítulo ha servido como base para ayudarte a comprender los principios del diseño de APIs REST. Para ello, nos centramos en el protocolo HTTP, que es la base de prácticamente toda la comunicación de APIs REST. Luego cubrimos las restricciones de diseño de APIs REST, sentando las bases de lo que significa crear una API RESTful. Con este trabajo previo, recorrimos RMM y WADMM para evaluar si nuestros diseños cumplen con las restricciones de diseño REST y en qué medida. Finalmente, propusimos un enfoque para actualizar tu API de modo que alcance el nivel de madurez requerido y sea más fiable y amigable para el consumidor.

En el próximo capítulo, analizaremos la construcción de un modelo de dominio para el diseño de APIs y cómo este conforma la base de un diseño de API eficaz. Exploraremos el papel del modelado de APIs, examinaremos de cerca JSON Schema como herramienta de modelado y destacaremos la importancia de adoptar el principio de superficie mínima de API. Por último, uniremos estas ideas construyendo un modelo de dominio de diseño de API basado en un lenguaje ubicuo.
