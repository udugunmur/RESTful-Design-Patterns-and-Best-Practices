# Parte 2: El Grimorio del Mago – Dominando los Fundamentos de REST

## Capítulo 7: Construcción de un Modelo de Dominio para el Diseño de APIs

El diseño de una API REST eficaz comienza con un modelo de dominio de diseño de API bien planificado. Este capítulo explora cómo abordar el modelado de APIs de manera estratégica, enfatizando su papel como paso fundamental para crear APIs que se alineen con los objetivos de negocio y brinden un valor significativo a los consumidores. En lugar de tratar el modelado de APIs como un simple ejercicio técnico, este capítulo destaca la importancia de comprender tu dominio de negocio, identificar las entidades clave y definir sus relaciones para crear APIs que vayan más allá de las operaciones básicas CRUD (*Create, Read, Update, Delete*).

Distinguiremos el modelado de APIs del modelado de bases de datos, abordando errores comunes como la dependencia excesiva del diseño centrado en la base de datos (*database-first*), que a menudo da como resultado APIs desconectadas de las necesidades reales del negocio. Además, el capítulo introduce principios como el principio de superficie mínima de API (*minimal API surface principle*), demostrando cómo estos enfoques dan lugar a APIs más seguras, fáciles de mantener e intuitivas para el usuario. Al finalizar, contarás con las herramientas y conocimientos necesarios para construir APIs que no solo sean funcionales, sino que también estén estratégicamente alineadas con los objetivos de tu organización.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **Comprensión del papel del modelado de APIs en el diseño de APIs**
- **Profundización en JSON Schema para el modelado de APIs**
- **Adopción del principio de superficie mínima de API**
- **Construcción de un modelo de dominio para el diseño de APIs a partir de un lenguaje ubicuo**

Al finalizar este capítulo, tendrás una sólida comprensión de cómo construir un modelo de API eficaz que se alinee con los objetivos de tu negocio y cumpla con altos estándares de calidad en el diseño.

---

### Requisitos técnicos

Para beneficiarse plenamente de este capítulo, los lectores deben contar con la siguiente base técnica:

- Conocimiento de los métodos y códigos de estado HTTP
- Conocimiento de JSON Schema
- Familiaridad con el Diseño Guiado por el Dominio (*Domain-Driven Design* / DDD)
- Conocimiento básico de la Especificación OpenAPI (*OpenAPI Specification*)

#### Ejemplo de la Tienda de Artículos Mágicos (*Magic Items Store*)

A lo largo de este capítulo, continuaremos utilizando la **Tienda de Artículos Mágicos (*Magic Items Store*)** como un ejemplo práctico para demostrar cómo un modelado de API eficaz conduce a un mejor diseño de API REST. Como minorista en línea ficticio que ofrece artículos mágicos —artefactos encantados, libros de hechizos y pociones místicas—, la Tienda de Artículos Mágicos proporciona un dominio sencillo pero rico para explorar conceptos clave de diseño de APIs.

Nos centraremos en modelar APIs que se alineen con los objetivos de negocio y ofrezcan una experiencia fluida a los usuarios. Este capítulo te guiará a través de la definición de recursos, el diseño de *endpoints* intuitivos y la estructuración de modelos de datos, todo ello arraigado en los principios de REST. La Tienda de Artículos Mágicos ayudará a ilustrar cómo un modelado reflexivo de APIs puede mejorar la funcionalidad, la escalabilidad y la mantenibilidad en aplicaciones del mundo real.

---

### Comprensión del papel del modelado de APIs en el diseño de APIs

En el ámbito del desarrollo de software, el modelado de APIs sirve como plano directriz para crear APIs que sean tanto eficientes como alineadas con los objetivos de negocio. Pero, ¿qué es exactamente el modelado de APIs y por qué es crucial?

#### ¿Qué es el modelado de APIs?

El modelado de APIs es el proceso sistemático de diseñar y definir la estructura de una API antes de escribir cualquier línea de código. Implica más que simplemente esbozar componentes técnicos; requiere la abstracción y especificación de elementos clave como estructuras de datos, *endpoints*, operaciones y relaciones que constituyen la API.

Este enfoque asegura que la API no solo sea funcional, sino también robusta, fácil de usar y alineada con los objetivos generales del negocio. Al centrarse en la estructura antes de la implementación, el modelado de APIs permite a los desarrolladores crear interfaces más efectivas y eficientes que satisfacen tanto los requisitos técnicos como los de negocio.

#### Componentes del modelado de APIs

Exploremos los componentes clave involucrados en el modelado de APIs: estructuras de datos, *endpoints*, operaciones y relaciones.

##### Estructuras de datos

El primer componente crucial del modelado de APIs son las estructuras de datos, a menudo denominadas modelos. Representan las entidades y recursos centrales dentro de un dominio de negocio. En la mayoría de los dominios, las entidades clave comunes pueden incluir usuarios, productos, pedidos, facturas y servicios. Cada una de estas entidades debe tener atributos claramente definidos y reglas de validación para garantizar que los datos se ajusten a los tipos, formatos y restricciones esperados.

Herramientas como **JSON Schema** se utilizan habitualmente para definir y validar estas estructuras de datos, lo que permite la coherencia y la integridad en toda la API.

En una plataforma de comercio electrónico hipotética como la Tienda de Artículos Mágicos, las estructuras de datos representan las entidades centrales. Para este ejemplo, consideremos tres entidades clave: `Product`, `Order` y `Customer`. Cada una de estas entidades tiene atributos que definen sus características, y las reglas de validación garantizan que los datos se ajusten a los tipos y formatos esperados.

Por ejemplo, podríamos definir una entidad de producto con los siguientes atributos:

- `productId` (string, UUID): Un identificador único para cada producto
- `name` (string): El nombre del producto
- `description` (string): Una breve descripción del producto
- `price` (number, positivo): El precio del producto; debe ser un valor no negativo
- `stock` (integer, no negativo): La cantidad del producto disponible en inventario
- `category` (string): La categoría a la que pertenece el producto (por ejemplo, «Ilusiones» o «Accesorios»)

Y podemos definir una entidad de producto con las siguientes reglas de validación:

- `productId`: Debe tener formato UUID
- `price`: Debe ser un número no negativo
- `stock`: Debe ser un número entero no negativo

Esto se puede representar mediante JSON Schema (exploraremos JSON Schema en profundidad en el Capítulo 11), como se muestra aquí:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "productId": {
      "type": "string",
      "format": "uuid"
    },
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "price": {
      "type": "number",
      "minimum": 0
    },
    "stock": {
      "type": "integer",
      "minimum": 0
    },
    "category": {
      "type": "string"
    }
  },
  "required": [
    "productId",
    "name",
    "price"
  ]
}
```

Definir tus estructuras de datos y reglas de validación en una etapa temprana del proceso de modelado garantiza que tu API sea robusta, coherente y fácil de mantener. Un modelo de datos bien estructurado mejora la usabilidad de la API y ayuda a los consumidores a comprender mejor cómo interactuar con ella. Al hacer cumplir la validación a nivel de esquema, puedes evitar que los datos no válidos se propaguen por el sistema, lo que en última instancia reduce los errores y mejora la integridad de los datos.

##### Endpoints

A continuación, debemos considerar los *endpoints*, que definen las rutas a través de las cuales los clientes acceden a los recursos en la API. Esto implica diseñar una estructura de URIs que sea coherente e intuitiva, facilitando a los consumidores de la API la interacción con el sistema.

Cada *endpoint* corresponde a un recurso específico y se combina con métodos HTTP como `GET`, `POST`, `PUT` y `DELETE`, según la operación deseada. Por ejemplo, recuperar una lista de productos se gestionaría con una petición `GET` a `/products`, mientras que actualizar un pedido existente requeriría una petición `PUT` a `/orders/{id}`.

##### Operaciones

Las operaciones que admite una API son otro aspecto clave del modelado de APIs. Estas se pueden clasificar a grandes rasgos en operaciones CRUD, que se ocupan de la manipulación de datos, y operaciones de lógica de negocio más complejas que representan acciones específicas del dominio. Por ejemplo, en una plataforma de comercio electrónico, operaciones como realizar un pedido, procesar un pago y enviar notificaciones son ejemplos de operaciones de lógica de negocio que van más allá de la funcionalidad básica de CRUD.

**Ejemplo: Realizar un pedido**

Cuando un cliente realiza un pedido en la Tienda de Artículos Mágicos, la API debe gestionar múltiples pasos para garantizar un proceso exitoso. Esta operación normalmente implica validar el inventario, calcular el precio total (incluidos impuestos y descuentos) y reservar artículos en stock. A continuación se muestra un ejemplo de petición para realizar un pedido:

Petición: `POST /orders`

```json
{
  "customerId": "123",
  "items": [
    {
      "productId": "32121",
      "quantity": 3
    },
    {
      "productId": "3454354",
      "quantity": 1
    }
  ],
  "paymentMethod": "credit_card"
}
```

Además, las operaciones de la API también pueden incluir procesos por lotes (*batch processes*), donde se manejan múltiples recursos en una sola petición, lo que aumenta la eficiencia para ciertos casos de uso. Definir adecuadamente estas operaciones garantiza que la API satisfaga tanto las necesidades de negocio básicas como las avanzadas.

##### Relaciones

Por último, las relaciones entre entidades son una parte integral del modelado de APIs, ya que definen cómo los recursos están conectados e interactúan entre sí. Estas relaciones pueden adoptar diferentes formas, como asociaciones uno a uno, uno a muchos o muchos a muchos. Por ejemplo, en la Tienda de Artículos Mágicos, un cliente puede tener muchos pedidos y cada pedido puede contener múltiples productos. Modelar estas relaciones permite que la API refleje las conexiones del mundo real entre las entidades de datos.

Además, se pueden emplear técnicas como los controles de hipermedia (**HATEOAS**) para ayudar a navegar entre recursos relacionados, ofreciendo a los clientes una forma fluida de recorrer la API. Decidir si incrustar recursos relacionados en las respuestas o proporcionar enlaces a ellos es otra consideración de diseño importante que afecta tanto a la eficiencia como a la usabilidad de la API.

En conclusión, el modelado de APIs es un proceso fundamental que ayuda a diseñar una API bien estructurada al definir sus componentes centrales: estructuras de datos, *endpoints*, operaciones y relaciones. Al modelar minuciosamente estos aspectos, los desarrolladores pueden crear APIs que sean fáciles de usar y estén alineadas con los objetivos de negocio. Este enfoque da como resultado APIs escalables, mantenibles y capaces de satisfacer las diversas necesidades de sus consumidores, mejorando en última instancia la experiencia general de la API.

Ahora que hemos cubierto la definición del modelado de APIs, profundicemos en la relación entre el modelado de APIs y el diseño de APIs.

#### Modelado de APIs y diseño de APIs

El modelado de APIs y el diseño de APIs son actividades estrechamente relacionadas pero diferenciadas que, en conjunto, garantizan el desarrollo de una API eficaz y de alta calidad. El modelado de APIs implica definir la estructura de una API, incluidos sus recursos, relaciones y modelos de datos, mientras que el diseño de APIs se centra en el proceso de toma de decisiones que guía cómo se exponen esos modelos y cómo interactúan con los clientes, haciendo hincapié en la usabilidad, las mejores prácticas y la experiencia del usuario.

El modelado de APIs sienta las bases para el diseño de APIs al definir los bloques de construcción —los recursos, relaciones y operaciones— que deben representarse. Una vez que estos elementos están bien definidos mediante el modelado, la fase de diseño se centra en cómo presentarlos de manera eficaz y elegante a los desarrolladores que utilizarán la API.

Además, el modelado de APIs sirve al diseño de APIs en los siguientes aspectos:

- **Establecer el plano directriz para el diseño de APIs**: El modelado de APIs sirve como plano directriz al proporcionar una representación conceptual de lo que debe contener la API y cómo deben interactuar los diferentes recursos. El proceso de diseño utiliza este plano para crear *endpoints*, elegir convenciones de nomenclatura y aplicar principios RESTful u otros estilos arquitectónicos.
- **Garantizar la coherencia en toda la API**: Una API bien modelada conduce a un diseño más coherente. Cuando los recursos, campos y relaciones se modelan adecuadamente, resulta más fácil aplicar un diseño uniforme en todos los *endpoints*, lo que hace que la API sea más predecible para sus usuarios.
- **Definir los límites de las operaciones**: El modelado de APIs define los límites y roles de los diferentes recursos, lo que fundamenta directamente el diseño de operaciones y *endpoints*. El modelado proporciona claridad sobre qué datos deben estar disponibles para cada recurso y cómo se debe acceder a ellos o manipularlos.
- **Mejorar la experiencia del usuario y la descubribilidad**: El modelado de APIs a menudo incluye definir relaciones y comportamientos de los recursos, lo que fundamenta el diseño de características como los controles de hipermedia. Estos controles guían a los usuarios a través de la API de forma descubrible, haciendo que la experiencia general del usuario sea más intuitiva.
- **Unir los requisitos técnicos y de negocio**: El modelado de APIs se centra en alinear la estructura de la API con las necesidades de negocio del dominio al representar con precisión los recursos y sus relaciones. El diseño de APIs conecta este modelo con los requisitos de usabilidad, asegurando que los desarrolladores puedan comprender y utilizar la API fácilmente.

El modelado de APIs y el diseño de APIs son procesos interdependientes que trabajan conjuntamente para crear APIs de alta calidad. El modelado de APIs proporciona el marco conceptual —la definición de recursos, relaciones y operaciones— que sustenta la API. El diseño de APIs toma este marco y determina la mejor manera de exponerlo a los clientes, centrándose en la usabilidad, la coherencia y el cumplimiento de las mejores prácticas.

Ahora que has comprendido el papel del modelado de APIs en la práctica del diseño, descubramos otras dimensiones del modelado de APIs.

#### Más allá del modelado físico de APIs

El modelado de APIs implica más que simplemente definir el modelo físico de estructuras de datos, *endpoints*, operaciones y relaciones. Abarca un contexto más amplio que incluye capturar metadatos esenciales y configuraciones que influyen en cómo se consume, protege y gestiona la API. Este alcance extendido del modelado de APIs conduce a un enfoque más integral, asegurando que la API sea adecuada para su audiencia prevista, escalable y capaz de evolucionar a medida que cambian los requisitos.

Exploremos algunos conceptos más allá del modelo físico, centrándonos en la importancia de los perfiles de API y sus aplicaciones.

##### Perfiles de API: Capturar un contexto más amplio

Los perfiles de API capturan la información necesaria sobre una API más allá de sus estructuras de datos y operaciones centrales, independientemente del estilo o estilos de API específicos (por ejemplo, REST, GraphQL) que admita. Un perfil de API incluye detalles como acuerdos de nivel de servicio (*Service-Level Agreements* / SLAs), requisitos de seguridad y el alcance de la API —ya sea pública, interna o destinada a socios—. Esto permite a los diseñadores de APIs crear APIs integrales que satisfagan eficazmente a diferentes grupos de usuarios y casos de uso.

En el contexto de la Tienda de Artículos Mágicos, la API Pública para Comerciantes (*Merchant Public API*) puede tener un perfil que incluya lo siguiente:

- **SLA**: Definir una disponibilidad garantizada del 99,9%, lo cual es crucial para los comerciantes que confían en la API para integrar su catálogo de productos y gestionar pedidos en tiempo real.
- **Seguridad**: Especificar OAuth 2.0 como mecanismo de autenticación, con diferentes alcances (*scopes*) para leer información de productos (`scope: products:read`) frente a la creación de pedidos (`scope: orders:create`). Estos detalles de seguridad garantizan que la API se utilice de forma segura y que las acciones sensibles requieran permisos explícitos.
- **Alcance de la API**: Indicar que esta API es de acceso público, disponible para todos los comerciantes registrados, mientras que otras APIs (como las APIs internas de gestión de inventario) pueden tener un acceso limitado.

El perfilado de APIs, por tanto, amplía el modelo de API para incluir estos requisitos no funcionales esenciales, asegurando que la API sea segura, fiable y adecuadamente orientada.

##### Modelos lógicos frente a físicos

El modelado de APIs también implica diferenciar entre modelos lógicos y físicos:

- **Modelo lógico**: Representa la definición abstracta de entidades y relaciones, independientemente de cualquier detalle específico de implementación. Por ejemplo, el modelo lógico para la Tienda de Artículos Mágicos podría definir entidades como `Product`, `Order` y `Merchant`, junto con sus relaciones (cada `Merchant` puede tener múltiples `Products`, y cada `Order` está asociado con un `Product` y un `Customer` específicos).
- **Modelo físico**: Toma estos conceptos abstractos y los traduce en *endpoints* concretos de la API, tales como `GET /merchants/{merchantId}/products` para recuperar todos los productos de un comerciante, o `POST /orders` para crear un nuevo pedido.

Al distinguir entre estos modelos, los diseñadores de APIs pueden centrarse primero en capturar los requisitos y las relaciones del negocio a alto nivel antes de sumergirse en los detalles concretos de la implementación.

##### Ampliación del modelo con reglas de negocio

Más allá de definir recursos y *endpoints*, el modelado de APIs también implica capturar las reglas y restricciones que rigen cómo se puede utilizar la API. Estas reglas de negocio garantizan que la API se alinee con los requisitos del dominio y las políticas operativas de la empresa.

En el contexto de la Tienda de Artículos Mágicos, la *Merchant Public API* representa una API externa que permite a comerciantes terceros gestionar sus listados de productos, inventario y pedidos dentro de la plataforma. Esta API permite a los comerciantes integrar sus sistemas con la tienda, brindándoles acceso programático para gestionar sus operaciones comerciales.

Ejemplos de reglas de negocio para la *Merchant Public API* podrían incluir los siguientes:

- **Límites de inventario de productos**: Los comerciantes no pueden publicar más de 1.000 productos activos a la vez. Esta regla garantiza el uso eficiente de los recursos y mantiene manejable el catálogo de productos.
- **Procesamiento de pedidos**: Los pedidos realizados a través de la API deben incluir información de pago válida y el estado debe actualizarse dentro de un plazo específico. Estas reglas refuerzan la integridad del proceso de pedidos y garantizan su cumplimiento oportuno.

Estas reglas van más allá de la estructura física básica de la API para garantizar que funcione de acuerdo con la lógica empresarial, manteniendo la coherencia y evitando el uso indebido.

##### Abordar múltiples estilos de API

Otro elemento crucial del modelado extendido de APIs es la planificación para diferentes estilos de API. Es posible que el mismo modelo subyacente deba admitir diferentes patrones de interacción según los requisitos del cliente: por ejemplo, REST para una aplicación web tradicional y GraphQL para un *frontend* moderno que necesita consultas flexibles.

En nuestro ejemplo de la Tienda de Artículos Mágicos:
- El *endpoint* REST `GET /products/{productId}` se utiliza para recuperar información detallada sobre un producto específico, identificado por su `productId` único. Este enfoque proporciona una estructura de respuesta predefinida que entrega detalles completos del producto.
- En contraste, una consulta GraphQL permite a los clientes solicitar solo los campos específicos que necesitan, como el nombre y el precio, a través de un *endpoint* flexible como `/graphql`. Esto permite que clientes con diferentes requisitos interactúen con el recurso de producto de una manera más personalizada y eficiente, reduciendo la transferencia innecesaria de datos y mejorando el rendimiento.

Tener un modelo lógico unificado que se pueda exponer a través de múltiples estilos de API garantiza la flexibilidad manteniendo al mismo tiempo la coherencia en todas las ofertas de la API.

El modelado de APIs va más allá de definir los aspectos físicos de una API, como estructuras de datos, *endpoints*, operaciones y relaciones. También implica capturar el contexto más amplio a través de perfiles de API, que detallan SLAs, medidas de seguridad y el alcance previsto de la API. Además, diferenciar entre modelos lógicos y físicos, definir reglas de negocio y adaptarse a múltiples estilos de API contribuyen a un enfoque más integral del modelado de APIs.

En el caso de la Tienda de Artículos Mágicos, estos conceptos de modelado extendido ayudan a crear una API que no solo es funcional y eficiente, sino que también está alineada con los objetivos estratégicos del negocio, es capaz de satisfacer diversas necesidades de los clientes y es resistente frente a cambios futuros. Al incorporar tanto los aspectos físicos como los lógicos, junto con la información de perfil más amplia, la *Merchant Public API* de la Tienda de Artículos Mágicos puede satisfacer diversas necesidades de manera eficaz manteniendo la coherencia y la escalabilidad.

Para dar vida a estos conceptos, ahora profundizaremos en JSON Schema: una potente herramienta para definir y validar estructuras de datos en APIs. JSON Schema proporciona una forma estándar de describir la forma de los datos de tu API, asegurando la coherencia y mejorando la experiencia del desarrollador. En esta siguiente sección, exploraremos cómo JSON Schema puede mejorar el diseño de tu API al permitir una validación de datos robusta, una documentación clara y compatibilidad con múltiples estilos de API.

---

### Profundización en JSON Schema para el modelado de APIs

JSON Schema es una potente herramienta que facilita la descripción y validación de documentos JSON, lo que la hace invaluable en el modelado de APIs. Esta inmersión profunda explora cómo JSON Schema puede mejorar el diseño de APIs REST y cómo sus principios se pueden aplicar a través de diferentes estilos de API, haciendo que tu API sea más robusta y amigable para los desarrolladores.

#### ¿Qué es JSON Schema?

JSON Schema es un vocabulario que te permite definir la estructura esperada, las restricciones y las reglas de validación para documentos JSON. En esencia, actúa como un plano directriz, asegurando que los datos JSON se ajusten a un formato predecible. Al proporcionar un contrato formal para los datos, JSON Schema no solo ayuda en la validación, sino también en la comunicación de la estructura de datos entre diferentes sistemas y equipos.

Los conceptos centrales de JSON Schema incluyen la especificación de tipos de datos, propiedades, reglas de validación y relaciones entre datos. Esto garantiza la coherencia y ayuda a detectar errores de forma temprana, especialmente cuando diferentes partes de una aplicación o diferentes aplicaciones interactúan con los mismos datos.

#### La importancia de JSON Schema en las APIs REST

En el contexto de las APIs REST, JSON Schema desempeña varios papeles cruciales que mejoran tanto el desarrollo como el consumo de APIs:

- **Validación de datos**: JSON Schema actúa como un guardián, asegurando que los datos enviados y recibidos se ajusten a formatos y reglas predefinidos. Esta validación es fundamental para mantener la integridad de los datos y ayuda a evitar que datos mal formados causen problemas en etapas posteriores.
- **Documentación**: JSON Schema sirve como documentación viva para tu API. A diferencia de los documentos estáticos, el esquema evoluciona con la API, proporcionando a los desarrolladores una representación precisa de qué esperar. Esto ayuda a reducir la confusión y garantiza que los consumidores de la API sepan con precisión qué datos enviar o esperar como respuesta.
- **Automatización y generación de código**: JSON Schema también facilita la automatización en el ciclo de vida de la API. Muchas herramientas pueden utilizar JSON Schema para generar automáticamente bibliotecas de cliente, realizar validación de datos e incluso crear servidores simulados (*mock servers*) para pruebas. Esto aumenta la productividad y permite a los desarrolladores centrarse más en la creación de funciones en lugar de escribir manualmente código de validación o mantener documentación redundante.

Considera el siguiente JSON Schema para una entidad de producto:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "format": "uuid"
    },
    "name": {
      "type": "string"
    },
    "price": {
      "type": "number",
      "minimum": 0
    }
  },
  "required": [
    "id",
    "name",
    "price"
  ]
}
```

En este esquema, se define un objeto de producto con tres propiedades: `id`, `name` y `price`. Cada propiedad tiene restricciones que dictan el tipo de datos y los valores aceptables. Por ejemplo, `price` debe ser un número no negativo, lo que garantiza que no se puedan introducir datos no válidos como precios negativos.

#### JSON Schema más allá de REST: otros estilos de API

Si bien JSON Schema se asocia principalmente con las APIs REST, su utilidad se extiende a otros estilos y paradigmas de API, demostrando su flexibilidad:

- **AsyncAPI y arquitecturas orientadas a eventos**: En sistemas orientados a eventos, JSON Schema se utiliza para definir los cuerpos (*payloads*) de los mensajes. Esto ayuda a estandarizar la comunicación en modelos de publicación-suscripción, garantizando que los eventos emitidos por los productores sean interpretados correctamente por los consumidores.
- **GraphQL**: Aunque GraphQL utiliza su propio lenguaje de definición de esquemas (SDL), la idea central de especificar estructuras de datos se alinea estrechamente con JSON Schema. Esta similitud facilita la transición entre diferentes estilos de API para los equipos, ya que el concepto de definir y aplicar datos estructurados se mantiene constante.
- **gRPC y Protobuf**: Los conceptos de JSON Schema se pueden comparar con Protobuf en gRPC, donde la definición de formatos de mensaje estrictos garantiza contratos claros entre el cliente y el servidor. La flexibilidad de JSON Schema para manejar validaciones complejas lo convierte en una referencia valiosa, incluso cuando se trabaja con protocolos binarios como gRPC.

#### Buenas prácticas para utilizar JSON Schema en el modelado de APIs

Para aprovechar JSON Schema de manera eficaz en el diseño de APIs, considera las siguientes buenas prácticas:

- **Mantenlo simple**: Evita esquemas excesivamente complejos que se vuelvan difíciles de mantener. Busca la simplicidad y la claridad para que a los desarrolladores les resulte más fácil comprender la estructura de datos esperada.
- **Diseño de esquemas modulares**: Divide los esquemas grandes en componentes reutilizables. Esto ayuda a gestionar los esquemas de forma más eficaz y promueve la coherencia en diferentes partes de la API.
- **Integración con la documentación**: Integra JSON Schema en la documentación de tu API. Herramientas como Swagger y OpenAPI pueden utilizar JSON Schema para proporcionar documentación interactiva, lo que permite a los desarrolladores experimentar con sus APIs sin necesidad de explicaciones extensas.
- **Validación y pruebas**: Haz que la validación de JSON Schema forme parte de tu proceso de integración continua (CI). Esto asegura que cualquier cambio en las estructuras de datos se detecte a tiempo, reduciendo posibles problemas de integración.

JSON Schema es más que una simple herramienta de validación: proporciona un contrato formal, mejora la documentación y respalda la automatización en el modelado de APIs. Ya sea que estés diseñando APIs REST o arquitecturas orientadas a eventos, o trabajando con otros estilos de API, comprender y aprovechar JSON Schema conducirá a APIs más fiables, mantenibles y fáciles de usar.

A continuación, exploraremos el concepto del principio de superficie mínima de API, centrándonos en cómo evitar la sobreingeniería y mantener tus APIs eficientes y fáciles de usar.

---

### Adopción del principio de superficie mínima de API

En el diseño de APIs, a menudo menos es más. Buscar la simplicidad y centrarse en los aspectos esenciales de una API puede conducir a una interfaz más robusta, escalable y amigable para el usuario. Esta es la idea central detrás del **principio de superficie mínima de API (*minimal API surface principle*)**: una filosofía de diseño que aboga por limitar la superficie expuesta de una API a lo estrictamente necesario para lograr su propósito previsto. Al aplicar este principio, los diseñadores de APIs pueden reducir la complejidad, mejorar la seguridad y optimizar la experiencia del desarrollador.

Este principio sirve como contrapeso a la sobreingeniería, donde las APIs se sobrecargan con funciones innecesarias en un esfuerzo por abordar cada caso de uso concebible. En cambio, minimizar la superficie de la API obliga a los diseñadores a centrarse en las operaciones y los datos comerciales más críticos, haciendo que la API sea más fácil de usar y mantener.

En las siguientes secciones, exploraremos las trampas comunes de la sobreingeniería y cómo la adopción del principio de superficie mínima de API puede abordar estos desafíos.

#### El problema de la sobreingeniería

La sobreingeniería en el diseño de APIs a menudo surge del deseo de crear una solución integral que anticipe todos los posibles casos de uso, lo que lleva a la inclusión de funciones innecesarias. Si bien esto puede parecer un enfoque proactivo, introduce una **complejidad accidental** que puede socavar la utilidad y la mantenibilidad de la API. Las APIs sobreingeniadas tienden a exponer propiedades excesivas, lo que da como resultado una interfaz enrevesada que resulta más difícil de entender y utilizar para los desarrolladores. Al intentar satisfacer todos los requisitos posibles por adelantado, la API se sobrecarga, volviéndose menos accesible y eficiente para los clientes.

Uno de los riesgos más significativos de la sobreingeniería es el mal diseño de la API, especialmente cuando está impulsado por un enfoque CRUD simplista. Cuando los desarrolladores piensan únicamente en términos de campos de bases de datos e intentan exponer todas las propiedades de los datos, la API resultante carece de una representación significativa de la lógica de negocio. Se convierte en un mero reflejo de la estructura de datos interna, en lugar de una interfaz reflexiva diseñada para resolver problemas comerciales específicos. Este tipo de diseño suele traducirse en una mala usabilidad, donde la API no comunica eficazmente su propósito ni permite a los clientes alcanzar sus objetivos con facilidad.

Otra consecuencia importante de la sobreingeniería es el aumento de los riesgos de seguridad asociados con la exposición excesiva de datos. Al incluir todas las propiedades en una respuesta de API, los desarrolladores pueden exponer inadvertidamente información confidencial que debería permanecer interna. Esta exposición convierte a la API en un blanco mayor para las vulnerabilidades de seguridad, ya que los atacantes disponen de más datos para explotar. Minimizar la superficie de la API seleccionando cuidadosamente qué propiedades y *endpoints* son necesarios puede reducir significativamente estos riesgos, dando lugar a una implementación más segura y protegida.

#### El principio de superficie mínima de API

Al diseñar APIs, resulta tentador incluir todas las propiedades y *endpoints* posibles para cubrir necesidades futuras. Sin embargo, este enfoque a menudo conduce a APIs sobrecargadas e ineficientes. El principio de superficie mínima de API promueve diseñar APIs con solo los componentes necesarios para cumplir con los requisitos actuales del producto, sin comprometerse en exceso con características futuras que quizás nunca se necesiten.

Como se destaca en las directrices de API de Adidas:

> «Todo diseño de API DEBE aspirar a una superficie mínima de API sin sacrificar los requisitos del producto. El diseño de la API NO DEBE incluir recursos, relaciones, acciones o datos innecesarios. El diseño de la API NO DEBE agregar funcionalidad hasta que se considere necesario (principio YAGNI)»  
> — *Directrices de API de Adidas ([https://adidas.gitbook.io/api-guidelines](https://adidas.gitbook.io/api-guidelines))*

Este principio hace hincapié en centrarse en las características esenciales, mantener la API austera y evitar la complejidad innecesaria que pueda obstaculizar su usabilidad y mantenibilidad.

Una estrategia clave para lograr esto es adoptar el principio **YAGNI (*You Aren’t Gonna Need It* / No lo vas a necesitar)**. Este principio anima a los desarrolladores a resistir el impulso de agregar características o funcionalidades hasta que sean genuinamente requeridas. Al centrarse únicamente en los requisitos actuales, YAGNI ayuda a mantener la API concisa y directa, facilitando su comprensión y uso. Adherirse a YAGNI a menudo da como resultado APIs más robustas y menos propensas a problemas causados por una complejidad innecesaria, ya que el alcance se limita a resolver el problema inmediato de manera efectiva.

Seguir el principio YAGNI no solo simplifica la API, sino que también conduce a un desarrollo más rápido y a una menor sobrecarga de mantenimiento. Los desarrolladores pueden dedicar su tiempo a abordar necesidades reales y tangibles en lugar de construir funciones basadas en suposiciones sobre requisitos futuros. Este enfoque minimiza el riesgo de desperdiciar esfuerzos en funcionalidades que tal vez nunca se utilicen, al tiempo que garantiza que la API evolucione de forma natural junto con el producto. Al mantener el enfoque en lo que se necesita hoy, YAGNI ayuda a los equipos a aportar valor de manera más eficiente y a evitar las trampas del desarrollo especulativo.

Ahora que hemos comprendido el concepto de una superficie mínima de API, profundicemos en un ejemplo.

#### Ejemplos de una superficie mínima de API frente a una API sobreingeniada

Considera los siguientes dos cuerpos de respuesta (*payloads*) para un objeto de producto en una API de comercio electrónico.

##### Ejemplo 1: Superficie mínima de API

```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "name": "Running Shoes",
  "price": 99.99,
  "url": "https://example.com/products/123e4567-e89b-12d3-a456-426614174000"
}
```

En este ejemplo, la respuesta contiene únicamente las propiedades esenciales: `id`, `name`, `price` y `url`. Estos son los atributos clave necesarios para un producto, proporcionando una respuesta concisa y eficiente adecuada para clientes que solo requieren detalles básicos del producto. Esto se alinea perfectamente con el principio de superficie mínima de API, asegurando que la API sea simple, segura y fácil de mantener.

##### Ejemplo 2: API sobreingeniada

```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "name": "Running Shoes",
  "description": "High-performance running shoes for all terrains.",
  "price": 99.99,
  "currency": "USD",
  "stock_quantity": 50,
  "supplier": {
    "id": "supplier-7890",
    "name": "Sports Gear Inc."
  },
  "relatedProducts": [
    {
      "id": "related-4567",
      "name": "Running Socks",
      "...." : "...."
    }
  ],
  "...." : "...."
}
```

Aquí, la respuesta está sobrecargada con detalles adicionales —como la descripción del producto, la cantidad en stock, la información del proveedor y los productos relacionados— que pueden no ser relevantes para la mayoría de los clientes. Si bien estas propiedades podrían ser útiles en contextos específicos, exponerlas todas en una sola respuesta de API agrega una complejidad innecesaria. Esta respuesta sobrecargada aumenta el tamaño del cuerpo, reduce la eficiencia e introduce posibles riesgos de seguridad al exponer información confidencial.

El principio de superficie mínima de API resalta el equilibrio entre funcionalidad y simplicidad. Al centrarse en las propiedades esenciales y evitar elementos innecesarios, las APIs se vuelven más ligeras, seguras y fáciles de mantener. Este enfoque minimalista mejora la usabilidad y permite que las APIs evolucionen según las necesidades reales, evitando la carga de funciones especulativas. Con estos principios en mente, apliquémoslos paso a paso para construir un modelo de dominio de diseño de API utilizando nuestro ejemplo de la Tienda de Artículos Mágicos.

---

### Construcción de un modelo de dominio para el diseño de APIs a partir de un lenguaje ubicuo

En esta sección, te guiaremos a través del proceso de construcción de un modelo de API para la Tienda de Artículos Mágicos utilizando los principios del Diseño Guiado por el Dominio. Este enfoque asegura que la implementación técnica se alinee estrechamente con el dominio de negocio, facilitando una comunicación clara entre desarrolladores y partes interesadas (*stakeholders*).

#### Paso 1: Definir el lenguaje ubicuo

El primer paso en el diseño guiado por el dominio es establecer un lenguaje ubicuo: un vocabulario común compartido entre desarrolladores y expertos del dominio. Este lenguaje compartido elimina malentendidos y asegura que todos los involucrados tengan una comprensión coherente de los conceptos y entidades clave dentro del dominio.

Comienza recopilando y definiendo los términos clave del dominio utilizados en el contexto de la Tienda de Artículos Mágicos, tales como «Producto», «Pedido», «Cliente» e «Inventario». Esto implica revisar historias de usuario, requisitos y sistemas existentes, seguido de la colaboración con los interesados para asegurar que todos compartan una comprensión coherente de cada término. Establecer un vocabulario claro y compartido es esencial para un modelado preciso y una comunicación eficaz, ayudando a que la API se alinee tanto con las necesidades del negocio como con las expectativas de los desarrolladores. Recopilaremos la terminología de diversas fuentes, revisaremos y definiremos cada término y luego obtendremos el acuerdo de los interesados sobre las definiciones finales. Así es como podría desarrollarse este proceso.

Al construir un vocabulario compartido para la Tienda de Artículos Mágicos, los términos clave del dominio se pueden identificar a partir de diversas fuentes:

- **Historias de usuario (*User stories*)**: Un ejemplo de historia de usuario podría ser: *«Como cliente, quiero explorar los libros de hechizos disponibles y agregarlos a mi carrito para poder comprarlos más tarde»*. En base a esto, podemos identificar los siguientes términos clave:
  - **Cliente (*Customer*)**: Una persona que explora o compra artículos mágicos en la Tienda de Artículos Mágicos.
  - **Libro de hechizos (*Spellbook*)**: Un tipo de artículo mágico disponible para la venta en la tienda.
  - **Carrito (*Cart*)**: Un área de retención temporal para los artículos que el cliente tiene intención de comprar.
  - **Compra (*Purchase*)**: La acción de completar una transacción para los artículos en el carrito.
- **Documentos de requisitos**: *«El sistema debe admitir una función de gestión de inventario para permitir a los administradores de la tienda agregar, eliminar o actualizar artículos mágicos»*. En base a esto, podemos identificar los siguientes términos clave:
  - **Inventario (*Inventory*)**: La colección de todos los artículos mágicos disponibles para la venta.
  - **Administrador de la tienda (*Store admin*)**: Un empleado responsable de gestionar productos y preparar pedidos.
  - **Agregar artículo / Eliminar artículo / Actualizar artículo**: Acciones realizadas por los administradores de la tienda para gestionar artículos en el inventario.
- **Interfaces de sistemas existentes**: Por ejemplo, *«Un sistema de catálogo interno que clasifica artículos mágicos»*, con los siguientes términos identificados:
  - **ID de producto (*Product ID*)**: Un identificador único asignado a cada artículo mágico.
  - **Nivel de stock (*Stock level*)**: La cantidad de un artículo mágico específico disponible para la compra.
  - **Precio (*Price*)**: El coste de cada artículo en la tienda.
- **Bocetos y maquetas (*Wireframes & mockups*)**: Un ejemplo de maqueta podría ser *«Una página de pago que muestra una lista de deseos, el carrito y opciones de pago»*, donde podemos identificar:
  - **Lista de deseos (*Wishlist*)**: Una función que permite a los clientes guardar artículos para su consideración futura.
  - **Pago / Proceso de compra (*Checkout*)**: El proceso que sigue un cliente para completar una compra.
  - **Opciones de pago (*Payment options*)**: Métodos disponibles (por ejemplo, tarjeta de crédito, ficha mágica, etc.) para finalizar una transacción.
- **Registros de atención al cliente**: Podemos considerar la consulta de ejemplo *«¿Cómo puedo verificar el estado de mi pedido o solicitar una devolución?»*, donde identificamos:
  - **Estado del pedido (*Order status*)**: El estado actual de un pedido, que puede ser «Pendiente», «Enviado» o «Entregado».
  - **Solicitud de devolución (*Return request*)**: La acción de un cliente para iniciar la devolución de un artículo.

Después de recopilar y revisar los términos de todos los artefactos, esto resultará en un vocabulario unificado y bien definido:

- **Cliente (*Customer*)**: Un usuario que explora o compra artículos en la Tienda de Artículos Mágicos.
- **Administrador de la tienda (*Store admin*)**: Un empleado responsable de gestionar artículos y pedidos.
- **Producto (*Product*)**: Cualquier artículo mágico, como un libro de hechizos, poción o talismán, disponible para la venta.
- **Inventario (*Inventory*)**: Toda la colección de productos en la tienda.
- **Carrito (*Cart*)**: Almacenamiento temporal para los artículos que un cliente tiene la intención de comprar.
- **Lista de deseos (*Wishlist*)**: Una lista donde los clientes pueden guardar artículos que podrían comprar más adelante.
- **Estado del pedido (*Order status*)**: El progreso actual del pedido de un cliente.
- **Solicitud de devolución (*Return request*)**: La solicitud de un cliente para devolver un artículo.
- **Proceso de compra (*Checkout*)**: El proceso final para completar una compra.
- **Opciones de pago (*Payment options*)**: Métodos disponibles para el pago.

Con este diccionario, todos los interesados y desarrolladores tienen ahora una comprensión compartida de los términos que darán forma a la API de la Tienda de Artículos Mágicos, asegurando claridad y coherencia en todo el proceso de diseño y desarrollo.

> **Nota**  
> Para profundizar en el diseño guiado por el dominio y la importancia de un lenguaje ubicuo, consulta el Capítulo 5. Al desarrollar un vocabulario compartido, no solo identificarás las entidades y conceptos clave dentro de tu dominio, sino que también sentarás una base sólida para los pasos posteriores en el proceso de diseño de la API.

Al definir un lenguaje ubicuo, hemos establecido un vocabulario compartido que alinea las perspectivas técnicas y de negocio. Esto asegura que todas las partes interesadas estén en la misma sintonía, eliminando la ambigüedad y formando una base sólida para el diseño de la API. Con estos términos fundamentales establecidos, el siguiente paso es pasar de la terminología a la definición de casos de uso, donde nos centraremos en cómo los usuarios interactúan con el sistema y traduciremos esas interacciones en requisitos de API accionables.

#### Paso 2: Definir los casos de uso

Comprender lo que tus clientes pretenden lograr es crucial para diseñar una API que satisfaga sus necesidades. En este paso, definirás los casos de uso que representan las diversas formas en que los usuarios interactúan con la Tienda de Artículos Mágicos. Los casos de uso comunes pueden incluir explorar productos, realizar pedidos y gestionar el inventario.

Comienza documentando todas las acciones que los usuarios realizarán dentro del sistema, desde la perspectiva tanto de los clientes como de los administradores de la tienda. Cada caso de uso debe describirse en términos de **requisitos de negocio**, que definen lo que el sistema debe lograr, y **especificaciones técnicas**, que traducen estos requisitos en operaciones concretas de la API. Una vez que hayas enumerado todos los casos de uso, priorízalos en función de su importancia y frecuencia de uso. Centrarse primero en los casos de uso más críticos asegura que la funcionalidad esencial se aborde de forma temprana en el proceso de diseño y proporciona una hoja de ruta clara para implementar los *endpoints* correspondientes.

Así es como abordaríamos esto para la Tienda de Artículos Mágicos. Primero, veamos algunos **casos de uso de los clientes**:

- **Explorar productos (*Browse products*)**: Los clientes desean explorar los artículos mágicos de la tienda, filtrando por tipo, rango de precios y propiedades mágicas:
  - *Requisito de negocio*: Hacer que todos los productos sean fáciles de buscar y filtrar.
  - *Especificación técnica*: Diseñar *endpoints* como `GET /products` con parámetros de consulta opcionales para el filtrado.
- **Ver detalles del producto (*View product details*)**: Los clientes pueden desear ver información detallada sobre un artículo específico antes de comprarlo:
  - *Requisito de negocio*: Proporcionar descripciones detalladas para cada artículo, incluidos atributos como precio, nivel de stock y efectos mágicos.
  - *Especificación técnica*: Implementar `GET /products/{productId}` para obtener detalles de productos individuales.
- **Agregar al carrito (*Add to cart*)**: Los clientes deben poder agregar artículos a un carrito para futuras compras:
  - *Requisito de negocio*: Permitir a los usuarios preparar múltiples artículos para el pago, con la opción de ajustar cantidades.
  - *Especificación técnica*: Utilizar *endpoints* como `POST /cart/items` para agregar artículos y `PUT /cart/items/{itemId}` para actualizar cantidades.
- **Tramitar pedido y pagar (*Check out and place order*)**: Cuando estén listos, los clientes proceden al pago, finalizan su compra y proporcionan los detalles de pago:
  - *Requisito de negocio*: Permitir a los usuarios completar compras de forma segura, con opciones de pago y envío.
  - *Especificación técnica*: Implementar `POST /orders` para la realización de pedidos, con campos para opciones de pago y entrega.
- **Seguimiento del estado del pedido (*Track order status*)**: Los clientes deben poder ver el estado de su pedido en cualquier momento:
  - *Requisito de negocio*: Mantener informados a los clientes sobre el progreso del pedido.
  - *Especificación técnica*: Utilizar `GET /orders/{orderId}/status` para recuperar el estado actual.

En segundo lugar, veamos algunos **casos de uso de los administradores de la tienda**:

- **Gestionar inventario (*Manage inventory*)**: Los administradores necesitan agregar, actualizar y eliminar productos del catálogo de la tienda:
  - *Requisito de negocio*: Garantizar que el inventario se pueda modificar para reflejar niveles de stock, nuevos artículos y productos descatalogados.
  - *Especificación técnica*: Implementar `POST /inventory`, `PUT /inventory/{productId}` y `DELETE /inventory/{productId}`.
- **Procesar pedidos (*Process orders*)**: Los administradores deben tener la capacidad de ver, confirmar y actualizar los estados de los pedidos:
  - *Requisito de negocio*: Proporcionar herramientas para procesar pedidos de manera eficiente a fin de mantener la satisfacción del cliente.
  - *Especificación técnica*: Utilizar `PUT /orders/{orderId}/status` para actualizar los estados de los pedidos de pendiente a confirmado, enviado o entregado.
- **Gestionar devoluciones y reembolsos (*Handle returns and refunds*)**: En los casos en que un cliente inicia una devolución, los administradores deben gestionar los reembolsos y el procesamiento de la devolución:
  - *Requisito de negocio*: Permitir una gestión flexible de las devoluciones de los clientes manteniendo un inventario preciso.
  - *Especificación técnica*: Implementar `POST /orders/{orderId}/return` para iniciar una devolución y `POST /orders/{orderId}/refund` para los reembolsos.

Al analizar los casos de uso, podemos priorizarlos según la importancia y la frecuencia del usuario:

- **Prioridad alta (esencial para el lanzamiento inicial)**:
  - Explorar productos
  - Ver detalles del producto
  - Agregar al carrito
  - Tramitar pedido y pagar
  - Gestionar inventario (administradores)
  - Procesar pedidos (administradores)
- **Prioridad media**:
  - Seguimiento del estado del pedido (clientes)
  - Gestionar devoluciones y reembolsos (administradores)
- **Prioridad baja**:
  - Lista de deseos (función futura que permite a los clientes guardar artículos que les interesan)

Al traducir los requisitos de negocio en especificaciones técnicas, obtienes una comprensión más clara de cómo debe comportarse el sistema. Este paso también ayuda a priorizar las funciones según las necesidades del usuario, lo cual es vital para entregar un producto que proporcione valor real.

#### Paso 3: Mapear casos de uso a verbos de la API REST

Con una comprensión clara de los casos de uso, el siguiente paso es mapear estas acciones a *endpoints* de API RESTful utilizando verbos HTTP. Las APIs RESTful aprovechan verbos HTTP como `GET`, `POST`, `PUT` y `DELETE` para representar acciones sobre los recursos.

Al definir los *endpoints*, también establecemos un marco claro sobre cómo se accede y se modifican los diferentes recursos (como productos, pedidos e inventario). Cada *endpoint* corresponde a una acción específica dentro del sistema, asegurando que todas las funciones principales estén cubiertas.

En cuanto a la Tienda de Artículos Mágicos, mapeemos algunos **endpoints de clientes**:

- **Explorar productos**:
  - *Endpoint*: `GET /products`
  - *Propósito*: Recupera una lista de productos con filtros opcionales (por ejemplo, por categoría, precio).
- **Ver detalles del producto**:
  - *Endpoint*: `GET /products/{productId}`
  - *Propósito*: Obtiene detalles de un solo producto, identificado por su ID único.
- **Agregar al carrito**:
  - *Endpoint*: `POST /cart/items`
  - *Propósito*: Añade un artículo al carrito del cliente.
- **Actualizar artículo del carrito**:
  - *Endpoint*: `PUT /cart/items/{itemId}`
  - *Propósito*: Actualiza la cantidad de un artículo en el carrito.
- **Tramitar pedido y pagar**:
  - *Endpoint*: `POST /orders`
  - *Propósito*: Realiza un nuevo pedido con detalles de pago y envío.
- **Seguimiento del estado del pedido**:
  - *Endpoint*: `GET /orders/{orderId}/status`
  - *Propósito*: Recupera el estado actual del pedido especificado.

Y ahora, mapeemos algunos **endpoints de administradores de la tienda**:

- **Gestionar inventario**:
  - *Agregar producto*:
    - *Endpoint*: `POST /inventory`
    - *Propósito*: Añade un nuevo producto al inventario.
  - *Actualizar producto*:
    - *Endpoint*: `PUT /inventory/{productId}`
    - *Propósito*: Actualiza los detalles de un producto existente.
  - *Eliminar producto*:
    - *Endpoint*: `DELETE /inventory/{productId}`
    - *Propósito*: Elimina un producto del inventario.
- **Procesar pedidos**:
  - *Confirmar pedido*:
    - *Endpoint*: `PUT /orders/{orderId}/status`
    - *Propósito*: Actualiza el estado de un pedido a «confirmado» tras el pago exitoso.
  - *Enviar pedido*:
    - *Endpoint*: `PUT /orders/{orderId}/status`
    - *Propósito*: Cambia el estado de un pedido a «enviado» una vez despachado.
- **Gestionar devoluciones**:
  - *Devolver producto*:
    - *Endpoint*: `POST /orders/{orderId}/return`
    - *Propósito*: Inicia el proceso de devolución de un pedido.
  - *Emitir reembolso*:
    - *Endpoint*: `POST /orders/{orderId}/refund`
    - *Propósito*: Procesa un reembolso para un pedido devuelto.

Al mapear directamente los casos de uso a métodos HTTP, alineamos la estructura de la API con las necesidades de negocio del mundo real, permitiendo que refleje intuitivamente la lógica del dominio. Este enfoque no solo asegura la cobertura de todas las funciones esenciales, sino que también hace que la API sea fácil de navegar y entender para los desarrolladores. El uso de diagramas de máquinas de estado para entidades como pedidos respalda aún más esta estructura al proporcionar una guía visual de las transiciones y los *endpoints* necesarios, lo que permite una API bien organizada y fácil de mantener.

#### Paso 4: Definir el modelo de recursos utilizando JSON Schema

Una vez definidos los *endpoints* de la API, es fundamental especificar la estructura de los datos que se intercambiarán.

Crea esquemas JSON para cada recurso de tu API. Por ejemplo, el recurso `Product` puede tener propiedades como `productId`, `name`, `description`, `price` y `stock`. Al definir los tipos de datos y las restricciones para cada propiedad, estableces expectativas claras tanto para los clientes como para los servidores que interactúan con la API.

He aquí un ejemplo de un JSON Schema para el recurso `Product`:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "productId": {
      "type": "string",
      "format": "uuid"
    },
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "price": {
      "type": "number",
      "minimum": 0
    },
    "stock": {
      "type": "integer",
      "minimum": 0
    }
  },
  "required": [
    "productId",
    "name",
    "price"
  ]
}
```

Definir estructuras de datos mediante JSON Schema no solo garantiza que los datos se validen, sino que también promueve la coherencia en diferentes partes de la aplicación. Este paso es fundamental para prevenir errores relacionados con los datos y facilitar la integración con otros sistemas.

#### Paso 5: Definir transiciones de estado y modelos de entrada

Comprender cómo cambian de estado las entidades a lo largo del tiempo es esencial para definir *endpoints* y cuerpos de datos que reflejen con precisión los procesos de negocio. Al modelar los ciclos de vida de las entidades, puedes asegurarte de que tu API admita todas las operaciones necesarias y maneje adecuadamente los cambios de estado.

Tomemos, por ejemplo, la entidad `Order`. Un pedido puede pasar por varios estados:

- **Pendiente (*Pending*)**: El pedido ha sido creado pero aún no procesado
- **Confirmado (*Confirmed*)**: El pago ha sido recibido y el pedido está confirmado
- **Enviado (*Shipped*)**: El pedido ha sido despachado al cliente
- **Entregado (*Delivered*)**: El cliente ha recibido el pedido

Al definir estas transiciones de estado, puedes identificar las acciones que provocan cambios de estado y las operaciones de API correspondientes necesarias para respaldarlas. Los modelos de entrada especifican los datos requeridos para cada operación. Por ejemplo, crear un pedido requeriría datos del cliente y una lista de artículos, mientras que actualizar el estado de un pedido podría ser una acción administrativa que cambie el estado del pedido.

Al modelar los ciclos de vida de las entidades y definir modelos de entrada y salida para las operaciones de la API, te aseguras de que tu API pueda manejar todos los escenarios necesarios y proporcionar una experiencia fluida tanto para los usuarios como para los administradores.

#### Paso 6: Compilar todo en la Especificación OpenAPI

El paso final es documentar el diseño de tu API con la Especificación OpenAPI (*OpenAPI Specification*). Si bien los capítulos 9 y 10 explorarán OpenAPI en detalle, es importante comprender ahora que OpenAPI proporciona un formato estandarizado y legible por máquina para describir tu API. Esta descripción sirve como base para la documentación, la generación de código y las pruebas.

En tu archivo OpenAPI, definirás las rutas (*endpoints*) y las operaciones (métodos HTTP) que admite tu API. También especificarás componentes como esquemas reutilizables, parámetros y respuestas. Además, puedes definir esquemas de seguridad para detallar los requisitos de autenticación y autorización.

A continuación se muestra un fragmento de ejemplo de un archivo OpenAPI para la API de la Tienda de Artículos Mágicos:

```yaml
openapi: 3.0.0
info:
  title: Magic Items Store API
  version: 1.0.0
paths:
  /products:
    get:
      summary: Retrieve a list of products
      responses:
        '200':
          description: A list of products
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductList'
components:
  schemas:
    ProductList:
      type: array
      items:
        $ref: '#/components/schemas/Product'
    Product:
      # JSON Schema for Product
```

Compilar las definiciones de tu API en el formato OpenAPI no solo estandariza tu documentación, sino que también permite el uso de diversas herramientas compatibles con OpenAPI. Estas herramientas pueden ayudar con la generación de código, las pruebas y la creación de documentación interactiva de APIs, agilizando significativamente el proceso de desarrollo.

Al utilizar la Especificación OpenAPI, aseguras que tu API esté bien documentada y sea accesible para otros desarrolladores, facilitando la integración y la colaboración.

#### Integración de todos los elementos (*Bringing it all together*)

Siguiendo estos pasos, has construido un modelo de dominio de diseño de API integral para la Tienda de Artículos Mágicos. Has establecido un vocabulario compartido, definido casos de uso, mapeado los mismos a *endpoints* RESTful, especificado modelos de datos con JSON Schema y documentado todo mediante OpenAPI. Este proceso no solo garantiza que tu API se alinee con las necesidades del negocio, sino que también sienta las bases para un desarrollo y mantenimiento eficientes. En la siguiente sección, resumiremos las conclusiones clave y exploraremos cómo estos elementos contribuyen a un diseño de API cohesivo.

---

### Resumen

En este capítulo, hemos explorado cómo crear un modelo de API que sirva como una base sólida para el diseño de APIs RESTful. Enfatizamos la importancia estratégica del modelado de APIs para alinearlas con los objetivos de negocio y proporcionar valor real a los consumidores. Utilizando el ejemplo de la Tienda de Artículos Mágicos, demostramos cómo transformar el conocimiento del dominio en una estructura de API robusta mediante la definición de entidades clave, relaciones y casos de uso del mundo real.

También presentamos el principio de superficie mínima de API como una técnica para simplificar el diseño, reducir la complejidad y mejorar la seguridad. Se destacó a JSON Schema como una herramienta potente para la validación orientada a esquemas, asegurando la coherencia, mejorando la documentación y proporcionando un contrato fiable entre los productores y consumidores de la API.

Al seguir un enfoque estructurado —definir un lenguaje ubicuo, identificar casos de uso e integrar estos elementos en una especificación OpenAPI—, puedes garantizar que tu modelo de API se mantenga claro, adaptable y amigable para el usuario. En el próximo capítulo, el Capítulo 8, nos centraremos en cómo los documentos de diseño formalizan tu modelo de API en un contrato práctico que garantiza coherencia, fiabilidad y transparencia para todas las partes interesadas.
