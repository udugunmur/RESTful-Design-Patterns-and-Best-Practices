# Parte 3: El Círculo del Archimago – Forjando y Haciendo Evolucionar los Contratos de API

## Capítulo 9: Comprensión de la Especificación OpenAPI

La Especificación OpenAPI proporciona una forma estandarizada de describir APIs REST. Este capítulo presenta los aspectos fundamentales de OpenAPI: su historia, su propósito y su estructura. A través de nuestro ejemplo de la Tienda de Artículos Mágicos (*Magic Items Store*), aprenderás cómo estructurar un documento OpenAPI y definir sus componentes centrales, desde los metadatos básicos hasta los *endpoints*, parámetros, respuestas y definiciones de seguridad.

Cubriremos los siguientes temas principales:

- **Los orígenes y el propósito de OpenAPI**
- **Diseño de APIs REST con la Especificación OpenAPI**
- **La estructura de la Especificación OpenAPI**

Al finalizar este capítulo, tendrás una comprensión clara de cómo describir de manera efectiva todos los aspectos clave del diseño de tu API y formalizarlos utilizando el formato de la Especificación OpenAPI. También obtendrás una visión detallada de la estructura de tu API y aprenderás a evitar errores comunes asociados con cada elemento.

---

### Los orígenes y el propósito de OpenAPI

La **Especificación OpenAPI (*OpenAPI Specification* / OAS)** es una forma estandarizada y agnóstica del lenguaje de programación para describir APIs RESTful. Piensa en los documentos OAS como contratos claros que detallan exactamente lo que tu API puede hacer, tal como hemos analizado en capítulos anteriores. OAS es una herramienta poderosa que respalda el concepto de la API como producto al proporcionar tanto a humanos como a computadoras una definición clara y legible de tu interfaz, sin necesidad de explorar el código fuente ni consultar documentación separada.

La historia de OAS comenzó en 2011 con el proyecto **Swagger**, creado por **Tony Tam** mientras trabajaba en el sitio de diccionarios Wordnik. Tam y su equipo estaban frustrados por los dolores de cabeza de la documentación y el desafío de generar SDKs de cliente, por lo que crearon Swagger como solución. A los desarrolladores les encantó cómo hacía que la documentación de las APIs fuera interactiva y más fácil de utilizar, y para 2014, **Swagger 2.0** llevó las cosas al siguiente nivel.

En 2015, **SmartBear Software** adquirió el proyecto Swagger de Reverb Technologies y, más tarde ese mismo año, tomó una decisión trascendental: donó la especificación a la recién creada **OpenAPI Initiative** bajo la **Fundación Linux**. Fue entonces cuando la Especificación Swagger se convirtió oficialmente en la **Especificación OpenAPI**, aunque ambos nombres convivieron durante un tiempo durante la transición.

Desde entonces, la OpenAPI Initiative ha continuado mejorando la especificación, lanzando la **versión 3.0 en 2017** y la **versión 3.1 en 2021**, la cual se integra mucho mejor con JSON Schema y maneja de forma superior los patrones de diseño de APIs modernos. Hoy en día, importantes referentes tecnológicos como **Google**, **IBM**, **Microsoft** y **Salesforce** respaldan la OpenAPI Initiative, lo que demuestra la relevancia fundamental que ha adquirido este estándar.

Este recorrido, desde una solución interna de un equipo hasta un estándar de la industria, demuestra cuán centrales se han vuelto las APIs en el desarrollo de software moderno y cómo la industria reconoce cada vez más la necesidad de contar con formas estandarizadas para diseñarlas y documentarlas.

#### ¿Por qué usar OAS?

En el mundo del desarrollo de APIs, la comunicación clara y la estandarización no son solo deseables; son esenciales para el éxito. OAS te brinda una herramienta poderosa que se comunica tanto con humanos como con máquinas, creando un lenguaje compartido para diseñar, construir y consumir APIs. OAS encaja perfectamente con el enfoque *design-first* que exploramos en el Capítulo 3, permitiéndote trazar la estructura de tu API antes de escribir una sola línea de código. Esto hace que la planificación sea más efectiva y te ayuda a evitar problemas dolorosos más adelante en el desarrollo.

OAS aporta innumerables beneficios a lo largo del ciclo de vida de tu API:
- Te permite generar **documentación interactiva y amigable** que ayuda a los desarrolladores a comprender y usar tu API.
- Puedes **crear automáticamente esqueletos de servidor (*server stubs*) y bibliotecas cliente (*SDKs*)** en diferentes lenguajes de programación, acelerando sustancialmente el trabajo de desarrollo.
- Ayuda a los equipos y organizaciones a mantenerse alineados con prácticas consistentes que hacen que la colaboración sea más fluida.
- Te proporciona bases sólidas para la **gobernanza de APIs**, manteniendo la calidad y el cumplimiento normativo en toda tu cartera de APIs.

Estas ventajas se vuelven especialmente valiosas cuando manejas proyectos complejos que involucran múltiples equipos y partes interesadas.

#### Cómo usar OAS

OAS no es solo para documentación; es una herramienta versátil que mejora cada aspecto del ciclo de vida de tu API. Para aprovechar al máximo OAS, comienza utilizándolo como la descripción formal de tu API: define tus *endpoints*, operaciones, parámetros y respuestas de manera estructurada utilizando el formato JSON o YAML. Este enfoque estandarizado mantiene todo claro y consistente, facilitando el trabajo a tu equipo y a cualquiera que consuma tu API.

Aprovecha el fantástico ecosistema de herramientas compatibles con OAS para aumentar tu productividad:
- Genera documentación atractiva e interactiva utilizando herramientas como **Swagger UI** o **ReDoc**, que transforman tu documento OAS en interfaces amigables para el usuario.
- Utiliza generadores de código como **OpenAPI Generator** para crear bibliotecas cliente e implementaciones de servidor en varios lenguajes, manteniendo la coherencia y ahorrando tiempo de desarrollo.
- Utiliza OAS como un **contrato entre proveedores y consumidores de API**. Al detallar claramente las expectativas y capacidades, previene la confusión y reduce los dolores de cabeza de la integración. Este enfoque *contract-first* se alinea perfectamente con el concepto de la API como producto del Capítulo 2.
- Las **pruebas y la validación** son otra área donde destaca OAS: utiliza tu especificación para generar casos de prueba y validar las implementaciones frente al estándar definido. Esto te ayuda a detectar problemas de forma temprana siguiendo el enfoque *shift-left*. Herramientas como **Postman** y **SoapUI** pueden importar tus documentos OAS para crear suites de pruebas automatizadas.

Al convertir a OAS en el estándar de documentación de APIs de tu organización, garantizas la consistencia entre diferentes equipos y proyectos. Considera aplicar OAS a todo tu ecosistema de APIs —incluidas APIs internas, microservicios e integraciones con sistemas heredados (*legacy*)— para crear un catálogo de APIs integral que sirva como una fuente única de verdad para todo tu panorama de APIs.

Ahora que hemos cubierto el porqué y el cómo de OAS, pongámonos manos a la obra. En la siguiente sección, construiremos desde cero una especificación de API completa para la Tienda de Artículos Mágicos, poniendo en práctica todos los conceptos analizados.

---

### Diseño de APIs REST con la Especificación OpenAPI

En esta sección, nos sumergiremos en el uso de OAS diseñando una API para la Tienda de Artículos Mágicos. Aprenderás a configurar *endpoints*, estructurar datos para peticiones y respuestas, y agregar características como seguridad y componentes reutilizables.

#### OpenAPI y Swagger

Como mencionamos anteriormente, OAS solía llamarse Especificación Swagger. Esta terminología a menudo persiste hasta el día de hoy indistintamente. En este libro, al hablar de la especificación, siempre nos referiremos a ella como **Especificación OpenAPI (OAS)**. Existen diferencias notables y significativas entre ambas especificaciones: OpenAPI 3.x (la versión actual) ofrece más flexibilidad y funcionalidades en comparación con Swagger 2.0, tales como componentes reutilizables centralizados y soporte ampliado para JSON Schema. Siempre que nos refiramos a **Swagger**, estaremos hablando del conjunto de herramientas en torno a OAS desarrollado por SmartBear.

#### Presentación de la API de la Tienda de Artículos Mágicos

Nuestro objetivo es diseñar una API para gestionar el inventario y los procesos básicos de una tienda de artículos mágicos. A partir de la etapa inicial de recopilación de requisitos, sabemos que nuestra tienda:
- Mostrará un catálogo de los artículos que vende la tienda, así como información detallada sobre cada artículo
- Gestionará el inventario de los artículos en el catálogo
- Procesará pedidos

Estas acciones son las **posibilidades de acción (*affordances*)** de nuestra aplicación. Esta API será consumida por nuestro *frontend* web y por nuestra aplicación móvil. Además, queremos habilitar el acceso público a los datos sobre nuestro catálogo de artículos mágicos.

Con ese conocimiento, podemos comenzar a diseñar nuestra API en un nivel de madurez adecuado:
- Decidimos apuntar al **Nivel 3 del Modelo de Madurez de Diseño de APIs Web (WADMM)**: una API centrada en la asequibilidad/posibilidad de acción (*affordance-centric*), creada en torno a las acciones que expone.
- También apuntaremos al **Nivel 2 del Modelo de Madurez de Richardson (RMM)**: una API diseñada de acuerdo con la semántica del protocolo HTTP. En el Capítulo 12, introduciremos controles de hipermedia para elevarla al Nivel 3 de RMM.

#### JSON Schema en este capítulo

Cubrimos JSON Schema y el modelado de objetos en detalle en el Capítulo 11, por lo que no nos centraremos en los detalles específicos del esquema en este capítulo. Vale la pena señalar que OAS aprovecha JSON Schema para definir sus modelos de datos, convirtiéndolos en una parte crucial de tu contrato de API.

Ahora que hemos establecido los requisitos y objetivos para nuestra API de la Tienda de Artículos Mágicos, veamos cómo representaremos este diseño utilizando OAS.

---

### La estructura de la Especificación OpenAPI

Todo documento OAS sigue una estructura coherente, ya sea que elijas el formato YAML o JSON (la mayoría de los desarrolladores prefieren YAML por su legibilidad). Comencemos con el esqueleto básico:

```yaml
openapi: 3.1.0
info:
servers:
paths:
components:
security:
```

> **Consejo rápido**: Mejora tu experiencia de programación con las funciones AI Code Explainer y Quick Copy. Abre este libro en el lector Packt Reader de última generación. Haz clic en el botón Copiar (1) para copiar rápidamente el código en tu entorno de desarrollo, o haz clic en el botón Explicar (2) para que el asistente de IA te explique un bloque de código.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

Este esquema muestra los seis bloques de construcción principales de un documento OpenAPI:

- **openapi**: Especifica qué versión de OAS estás utilizando (por ejemplo, `3.1.0`). Señala qué características y reglas de sintaxis se aplican a tu documento para que las herramientas lo procesen correctamente sin errores de compatibilidad.
- **info**: Es la tarjeta de identificación de tu API. Contiene metadatos esenciales como el título, la versión, la descripción y los datos de contacto.
- **servers**: Enumera las URLs donde se puede acceder a tu API.
- **paths**: El núcleo del documento. Aquí defines todos los *endpoints* de tu API y los métodos HTTP que admiten.
- **components**: Tu caja de herramientas de partes predefinidas que puedes referenciar en toda tu API (esquemas de datos, plantillas de respuesta, parámetros y esquemas de seguridad) para mantener tu especificación DRY (*Don't Repeat Yourself*).
- **security**: Define cómo está protegida tu API (claves de API, OAuth2, etc.).

> **La especificación completa**  
> Si deseas la referencia completa y exhaustiva, visita el sitio web oficial de la especificación: [https://spec.openapis.org/oas/latest](https://spec.openapis.org/oas/latest).

#### El objeto info: la primera impresión de tu API

El objeto `info` actúa como la tarjeta de presentación de tu API, ofreciendo metadatos esenciales que presentan a todos lo que hace tu API, quién es su propietario y en qué punto de su ciclo de vida se encuentra:

```yaml
openapi: 3.1.0
info:
  title: Magic Items Store API
  version: 1.2.0
  description: |
    # Welcome to the Magic Items E-store API
    Manage magical inventory and orders.
    Supports filtering by item type, rarity, and enchantment level.
  termsOfService: https://magic-store.com/terms
  contact:
    name: Arcane Support Team
    email: support@magic-store.com
    url: https://magic-store.com/contact
  license:
    name: Magical Commons License v2.0
    url: https://magic-store.com/license
```

Desglosemos cada parte de este objeto `info`:

- **title** (Obligatorio): El nombre único de tu API. Debe ser conciso pero descriptivo.
- **version** (Obligatorio): Muestra la versión semántica actual de tu API (como `1.2.0`). Es crítico para el seguimiento de compatibilidad (ver Capítulo 13).
- **description** (Opcional pero recomendado): Un resumen en formato Markdown de las capacidades de tu API, requisitos de autenticación o reglas del dominio.
- **termsOfService** (Opcional): Una URL que enlaza con los términos legales de uso.
- **contact** (Opcional): Datos de soporte técnico (nombre, correo electrónico, URL).
- **license** (Opcional): Aclara los términos de licencia bajo los cuales otros pueden usar tu API.

#### El objeto paths: mapear las capacidades de tu API

El objeto `paths` es donde toma forma la funcionalidad de tu API. Define no solo los *endpoints* y los métodos HTTP, sino también el modelo de interacción preciso entre los clientes y tu servicio:

```yaml
paths:
  /items:
    summary: Manage items collection
    description: Operations for managing the collection of magical items.
    get:
      tags: [Inventory]
      summary: List all magic items
      description: |
        Retrieve a paginated list of magical items.
        Supports filtering by rarity, spell type, and price range.
        Maximum of 100 items per response.
      operationId: listItems
      parameters:
        - $ref: '#/components/parameters/RarityFilter'
        - $ref: '#/components/parameters/Page'
        - $ref: '#/components/parameters/PageSize'
      responses:
        '200':
          $ref: '#/components/schemas/Items'
        '400':
          $ref: '#/components/responses/BadRequest'
        '500':
          $ref: '#/components/responses/InternalError'
```

Desglosemos cada parte:

- **/items** (Obligatorio): Un objeto de elemento de ruta (*path item object*). Es una ruta relativa a un *endpoint* individual. Siempre debe comenzar con una barra diagonal `/`. Utiliza rutas basadas en sustantivos que se refieran a recursos (`/items`) y evita rutas basadas en acciones (`/getItems`). Utiliza parámetros de ruta para identificadores (`/items/{itemId}`).
- **get** (Obligatorio): Un objeto de operación (*operation object*) que define lo que sucede cuando alguien realiza una petición `GET` a `/items`. Puede ser cualquier método HTTP (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`, etc.).
- **summary** (Opcional): Una explicación breve de para qué sirve este recurso.
- **description** (Opcional): Documentación más detallada con soporte de Markdown.
- **tags** (Opcional): Agrupa operaciones relacionadas en la documentación (por ejemplo, `[Inventory]`).
- **operationId** (Opcional pero recomendado): Un identificador único utilizado por herramientas de generación de código para crear nombres limpios de métodos en SDKs. Debe ser único en toda la especificación.
- **parameters** (Condicional): Define las entradas del *endpoint* (parámetros de ruta, consulta o cabecera).
- **responses** (Obligatorio): Declara todos los posibles resultados al invocar la operación (incluidos escenarios de error `4xx` y `5xx`).

> **Especificación Arazzo**  
> La especificación Arazzo es un nuevo estándar que complementa a OpenAPI definiendo flujos de trabajo (*workflows*) de API: secuencias de llamadas a la API relacionadas que trabajan juntas para lograr objetivos de negocio específicos. Lanzada en 2024 por la OpenAPI Initiative, Arazzo permite documentar interacciones complejas de múltiples pasos en un formato legible por máquina (YAML o JSON), facilitando la documentación interactiva, la generación de código y el consumo de APIs por sistemas basados en IA ([https://www.openapis.org/arazzo](https://www.openapis.org/arazzo)).

#### El objeto parameters: configurar las entradas de tu API

OpenAPI proporciona cuatro ubicaciones diferentes para los parámetros, especificadas mediante el campo `in`:

##### Tipos y ubicaciones de parámetros

- **Parámetros de ruta (`in: path`)**: Son partes variables de la ruta URL (por ejemplo, `/items/{itemId}`). Siempre son obligatorios (`required: true`) y deben aparecer en la ruta entre llaves:
```yaml
parameters:
  - name: itemId
    in: path
    required: true # Always required for path parameters
    description: Unique identifier of the magical item
    schema:
      type: string
```
- **Parámetros de consulta (`in: query`)**: Se añaden a la URL después del signo de interrogación `?`. Son ideales para filtrado, ordenación y paginación:
```yaml
parameters:
  - name: rarity
    in: query
    description: Filter items by rarity level
    required: false
    schema:
      type: string
      enum: [common, uncommon, rare, legendary]
```
- **Parámetros de cabecera (`in: header`)**: Son cabeceras HTTP personalizadas o estándar enviadas con la petición:
```yaml
parameters:
  - name: X-Magical-Realm
    in: header
    description: Restrict search to a specific magical realm
    required: false
    schema:
      type: string
```
- **Parámetros de cookie (`in: cookie`)**: Valores pasados en la cabecera `Cookie`, a menudo utilizados para gestionar sesiones:
```yaml
parameters:
  - name: session-id
    in: cookie
    description: Session identifier
    schema:
      type: string
```

##### Campos del objeto parameter

- `name`: Identificador sensible a mayúsculas y minúsculas
- `in`: Ubicación (`path`, `query`, `header`, `cookie`)
- `description`: Explicación en texto o Markdown
- `required`: Booleano (por defecto `false`, excepto en `path` que es `true`)
- `deprecated`: Marca si el parámetro está en proceso de retirada
- `schema`: Define el tipo de datos y restricciones mediante JSON Schema

##### Manejo de objetos y arrays en parámetros

OpenAPI proporciona las propiedades `style` y `explode` para controlar cómo se serializan los datos estructurados en la URL:

```yaml
parameters:
  - name: filter
    in: query
    description: Complex filter criteria
    schema:
      type: object
      properties:
        minPower:
          type: integer
        elementType:
          type: string
    style: deepObject # Serializes as filter[minPower]=5&filter[elementType]=fire
    explode: true
```

#### El objeto requestBody: estructurar los cuerpos de datos de tu API

El objeto `requestBody` define los datos estructurados que los clientes envían en operaciones como `POST`, `PUT` y `PATCH`:

```yaml
requestBody:
  description: Magical item to add to the inventory
  required: true
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/MagicItemCreate'
```

##### Múltiples tipos de contenido

Tu API puede aceptar diferentes tipos de medios para la misma operación:

```yaml
requestBody:
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/MagicItemCreate'
    application/xml:
      schema:
        $ref: '#/components/schemas/MagicItemCreate'
    multipart/form-data:
      schema:
        $ref: '#/components/schemas/MagicItemUpload'
```

##### La importancia crítica de los ejemplos

Los ejemplos transforman definiciones de esquema abstractas en ilustraciones concretas:

```yaml
requestBody:
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/PotionCreate'
      examples:
        healingPotion:
          summary: Basic healing potion
          value:
            name: "Minor Healing Potion"
            effect: "Restores 25 health points"
            duration: 30
            ingredients: ["Herbs", "Fairy Dust"]
        strengthPotion:
          summary: Strength enhancement potion
          value:
            name: "Giant's Strength"
            effect: "Increases strength by 50%"
            duration: 120
            ingredients: ["Troll Blood", "Mountain Herbs"]
```

#### El objeto responses: definir los contratos de salida de tu API

El objeto `responses` define lo que los consumidores recibirán a cambio tras realizar una petición:

```yaml
responses:
  '200':
    description: The magical item was successfully retrieved
  '404':
    description: The requested magical item could not be found
```

Campos clave de las respuestas:
- **description** (Obligatorio): Explicación legible por humanos (admite Markdown).
- **headers**: Cabeceras de respuesta (como directivas de caché o identificadores de versión):
```yaml
headers:
  Cache-Control:
    description: Directives for caching mechanisms
    schema:
      type: string
      example: "max-age=3600, must-revalidate"
  ETag:
    description: Version identifier for the resource
    schema:
      type: string
      example: "W/\"12345\""
```
- **content**: Mapea tipos de medios a sus esquemas de datos:
```yaml
content:
  application/json:
    # Schema definition goes here
  application/xml:
    # Alternative schema for XML format
```
- **links**: Define enlaces a otras operaciones (HATEOAS, ver Capítulo 12).

##### Códigos de estado HTTP en el mapa de respuestas

```yaml
responses:
  '200':
    description: Successful retrieval of magical items
  '4XX':
    description: Client error
  '500':
    description: Server error
```

> **¿Por qué evitar la respuesta `default`?**  
> Recomendamos evitar la respuesta comodín `default` en la mayoría de los casos. Genera ambigüedad en el contrato, reduce la precisión de las pruebas automatizadas y deja a los desarrolladores con dudas sobre qué códigos de estado reales esperar. Es preferible documentar explícitamente cada código de estado o usar rangos como `4XX` y `5XX`.

#### El objeto security: proteger los recursos de tu API

La seguridad se puede configurar de dos maneras:
- **Seguridad global**: Aplicada en la raíz del documento para todos los *endpoints*.
- **Seguridad por operación**: Definida a nivel de operación, sobrescribiendo la configuración global.

```yaml
# Global security definition (applied to all endpoints)
security:
  - OAuth2: [read:items]

paths:
  /items:
    get:
      # Inherits global security
    post:
      # Override for this specific operation
      security:
        - OAuth2: [write:items]
```

##### Esquemas de seguridad en `components/securitySchemes`

- **API Keys**:
```yaml
components:
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key
```
- **Autenticación HTTP (Basic / Bearer JWT)**:
```yaml
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
- **OAuth 2.0**:
```yaml
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://auth.magicitems.com/oauth/authorize
          tokenUrl: https://auth.magicitems.com/oauth/token
          refreshUrl: https://auth.magicitems.com/oauth/refresh
          scopes:
            read:items: Read magical items
            write:items: Create or modify items
            delete:items: Remove items from inventory
```
- **OpenID Connect**:
```yaml
components:
  securitySchemes:
    OpenIDConnect:
      type: openIdConnect
      openIdConnectUrl: https://auth.magicitems.com/.well-known/openid-configuration
```

#### El objeto components: bloques de construcción reutilizables de tu API

El objeto `components` es el repositorio central para almacenar elementos reutilizables que puedes referenciar en toda tu especificación OpenAPI:

```yaml
components:
  schemas:
    MagicItem: { }
  parameters:
    RarityParameter: { }
  responses:
    NotFoundError: { }
  examples:
    SamplePotion: { }
  requestBodies:
    CreateItemRequest: { }
  headers:
    RateLimit: { }
  securitySchemes:
    OAuth2: { }
  links:
    GetRelatedItems: { }
  callbacks:
    ItemCreated: { }
```

##### Comprensión de `$ref`: el pegamento que une los componentes

La palabra clave `$ref` es una referencia JSON que apunta a definiciones de componentes:

- **Referencia local**:
```yaml
/items:
  get:
    parameters:
      - $ref: '#/components/parameters/RarityFilter'
    responses:
      '200':
        description: A list of magical items
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/MagicItem'
      '404':
        $ref: '#/components/responses/NotFound'
```
- **Referencia externa**:
```yaml
$ref: './common.yaml#/components/parameters/userId'
```

---

### Resumen

En este capítulo, hemos explorado los fundamentos de la Especificación OpenAPI (OAS) y sus componentes principales. Rastreamos su evolución desde Swagger hasta su estandarización bajo la Fundación Linux, comprendiendo por qué se ha vuelto esencial en el desarrollo moderno de APIs. Utilizando la Tienda de Artículos Mágicos como ejemplo práctico, examinamos la estructura central de los documentos OAS: desde el objeto `info` con sus metadatos hasta el objeto `paths` con sus *endpoints* y operaciones.

Profundizamos en los bloques de construcción clave de un documento OpenAPI: `parameters` para configurar entradas, `requestBody` para cuerpos estructurados, `responses` para definir contratos de salida, mecanismos de `security` para proteger recursos y `components` para crear elementos reutilizables vinculados mediante `$ref`.

Con esta base sobre la estructura y sintaxis de OpenAPI, estás preparado para explorar cómo funciona como un contrato vivo entre proveedores y consumidores de APIs en el próximo capítulo.
