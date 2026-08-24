# Parte 3: El Círculo del Archimago – Forjando y Haciendo Evolucionar los Contratos de API

## Capítulo 10: OpenAPI como Contrato: Buenas Prácticas e Implementación

Más allá de la documentación, OpenAPI sirve como un contrato ejecutable para el desarrollo de APIs. Este capítulo explora patrones prácticos de implementación, desde la validación de contratos hasta la integración de herramientas. Aprenderás a diseñar APIs intuitivas con recursos coherentes, manejo de errores y operaciones asíncronas, mientras descubres cómo los enfoques orientados al contrato (*contract-first*) transforman la colaboración en equipo.

En este capítulo, hablaremos de lo siguiente:

- **OpenAPI como contrato para tu API**
- **Buenas prácticas para el uso de la Especificación OpenAPI**

Al finalizar este capítulo, serás capaz de implementar OpenAPI como un contrato vinculante para tus APIs y aplicar las mejores prácticas de la industria para el diseño de APIs, incluyendo la estructuración de recursos, el manejo de errores y las operaciones asíncronas. También sabrás cómo aprovechar el ecosistema de OpenAPI para transformar tu flujo de trabajo de desarrollo mediante enfoques *contract-first* y herramientas automatizadas.

---

### OpenAPI como contrato para tu API

¿Recuerdas cuando hablamos de las APIs como productos en capítulos anteriores y de lo importante que es tratar el diseño de la API como un contrato entre tú y tus usuarios? La Especificación OpenAPI es donde esa idea cobra vida. No es solo documentación; es tu contrato de API en un formato que tanto las computadoras como los humanos pueden entender.

Piensa en tu documento OpenAPI como el reglamento oficial de tu API. Establece con claridad qué artículos pueden comprar los clientes, cómo pueden buscar en el inventario, qué información deben proporcionar al realizar un pedido y qué respuestas recibirán. Tanto tus desarrolladores como los usuarios de tu API pueden confiar en este contrato para saber exactamente qué esperar.

La belleza de OpenAPI radica en que, una vez que has creado este contrato, impulsa todo un conjunto de herramientas y soluciones útiles:
- Tu documento OAS único puede generar **documentación interactiva** que permite a los desarrolladores probar llamadas a la API directamente en su navegador (imagina permitir que los clientes potenciales exploren tu catálogo de Artículos Mágicos antes de escribir una sola línea de código).
- Puedes levantar **servidores simulados (*mock servers*)** que devuelvan respuestas de ejemplo, de modo que los desarrolladores de *frontend* puedan comenzar a construir la interfaz de compra antes de que el equipo de *backend* haya terminado de implementar la gestión del inventario.
- Cuando llega el momento de escribir código, el mismo contrato OAS puede **generar bibliotecas cliente (*SDKs*)** en diferentes lenguajes de programación, evitando que los usuarios escriban código repetitivo para llamar a tu API.
- Para tu propio equipo de desarrollo, puede **generar esqueletos de servidor (*server stubs*)** que coincidan exactamente con el diseño de la API, asegurando que tu implementación se mantenga fiel al contrato.
- Las **pruebas** también se vuelven mucho más sencillas: tu equipo de control de calidad (*QA*) puede usar el contrato OAS para generar casos de prueba automáticamente y validar que las respuestas de tu API coincidan con lo prometido. Si alguien cambia accidentalmente un *endpoint* para que devuelva datos diferentes, las pruebas automatizadas detectarán la violación del contrato antes de que afecte a los usuarios.

Esto significa que todos se mantienen en la misma página. Los especialistas en encantamientos que diseñan nuevos artículos mágicos, los administradores de inventario que supervisan los niveles de stock y los desarrolladores del portal orientado al cliente trabajan a partir del mismo contrato. Cuando se necesita un cambio (como añadir un nuevo campo de «puntuación de rareza» a cada artículo mágico), actualizas primero el contrato OpenAPI y todos pueden ver de inmediato cómo afecta a su parte del sistema.

Al colocar a OpenAPI en el centro de tu proceso de desarrollo de APIs, generas confianza con tus usuarios. Saben exactamente qué esperar de tu API y pueden confiar en su coherencia. Esta fiabilidad es esencial tanto si vendes artefactos mágicos como cualquier otro tipo de producto API.

#### OAS como tu fuente única de verdad (*Single Source of Truth*)

Cuando hablamos de una «fuente única de verdad» en el desarrollo de APIs, abordamos uno de los mayores dolores de cabeza a los que se enfrentan los equipos: mantener alineados la documentación, el código y las expectativas. La Especificación OpenAPI resuelve este problema al ofrecerte una definición definitiva y ejecutable de tu contrato de API.

A diferencia de la documentación tradicional que puede desincronizarse con respecto a lo que el código hace realmente, un documento OAS sirve como el punto de referencia en el que todos pueden confiar: desarrolladores, evaluadores, gestores de producto y las personas que consumen tu API. Para nuestra tienda de Artículos Mágicos, esto significa que cuando definimos el *endpoint* `/items` en nuestra especificación, no es solo una sugerencia o documentación que podría quedar desactualizada; es un acuerdo vinculante que establece claramente qué parámetros pueden usar los clientes, qué respuestas obtendrán y qué errores podrían surgir.

Esta precisión elimina las frustrantes conversaciones de «pensé que funcionaba de otra manera» y crea una base donde las herramientas pueden comprobar automáticamente que tu API hace exactamente lo que prometiste.

#### Cómo OpenAPI implementa el concepto de contrato en la práctica

OpenAPI transforma los conceptos abstractos de un contrato en algo que realmente puedes hacer cumplir mediante esquemas, operaciones y patrones de respuesta definidos con precisión. Veamos cómo funciona esto con nuestra tienda de Artículos Mágicos.

Supongamos que definimos un *endpoint* como `/items/{itemId}` en nuestro documento OAS con sus operaciones, parámetros y respuestas:

```yaml
/items/{itemId}:
  get:
    parameters:
      - name: itemId
        in: path
        required: true
        schema:
          type: string
          pattern: "^[a-zA-Z0-9-]+$"
    responses:
      '200':
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/MagicItem'
      '404':
        $ref: '#/components/responses/NotFound'
```

Al hacer esto, no solo creamos documentación; creamos un contrato vinculante que establece claramente:

1. **Requisitos de entrada**: El parámetro `itemId` debe estar presente (ya que lo marcamos como `required: true`) y debe coincidir con el patrón especificado. Cualquier cliente que envíe identificadores no válidos (como `item@123`) está rompiendo las reglas del contrato.
2. **Garantías de salida**: Tu API promete devolver un objeto `MagicItem` para peticiones válidas. Si un desarrollador construye un cliente esperando un campo `price` porque está definido en el esquema `MagicItem`, ¡ese campo debe estar ahí!
3. **Manejo de errores**: El contrato declara explícitamente qué errores pueden ocurrir (en este caso, `404` si el artículo no existe).

Esta precisión contractual es fundamental en todo el sistema: la operación `POST` define qué propiedades son obligatorias para el inventario, el carrito de compras sabe cómo solicitar los detalles y el sistema de pedidos cuenta con una estructura coherente en todos los *endpoints*.

Este contrato se hace cumplir mediante herramientas de validación que verifican que tanto las peticiones como las respuestas coincidan con la especificación. Si una actualización de la API cambia accidentalmente la estructura de `MagicItem`, las herramientas de validación de contratos lo señalan de inmediato como un cambio incompatible (*breaking change*).

#### Traducción de contratos abstractos de API en documentos OAS ejecutables

¿Cómo se pasa de los requisitos abstractos de la API a un contrato OpenAPI concreto? Se trata de traducir tus conceptos y reglas de negocio en elementos estructurados de OAS:

- **Requisito de negocio**: *«Los clientes deben poder explorar artículos por rareza (común, poco común, raro, legendario)»*.  
  En tu documento OpenAPI, esto se traduce en:
```yaml
paths:
  /items:
    get:
      parameters:
        - name: rarity
          in: query
          schema:
            type: string
            enum: [common, uncommon, rare, legendary]
            description: Filter items by their magical rarity
```

- **Restricciones de dominio**: *«Los precios de los artículos mágicos deben ser números positivos con hasta 2 decimales»*.  
  Se convierte en una regla de validación de esquema:
```yaml
components:
  schemas:
    MagicItem:
      properties:
        price:
          type: number
          minimum: 0.01
          multipleOf: 0.01
          description: Item price in gold coins
```

- **Requisitos de seguridad**: *«Solo los propietarios de tiendas autenticados pueden aplicar descuentos a los artículos»*.  
  Se traduce en definiciones de seguridad de OAS:
```yaml
paths:
  /items/{itemId}/discount:
    post:
      security:
        - OAuth2: [items:write]
      requestBody:
        content:
          application/json:
            schema:
              properties:
                discountPercentage:
                  type: number
                  minimum: 1
                  maximum: 75
```

- **Reglas de negocio complejas**: *«Cuando se compra un artículo, el stock de inventario debe actualizarse y devolver error si no hay disponibilidad»*.  
  Se documenta con los códigos de estado adecuados:
```yaml
paths:
  /orders:
    post:
      responses:
        '201':
          description: Purchase successful
        '409':
          description: Item no longer in stock
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/OutOfStockError'
```

Lo que hace que estas traducciones de OAS sean tan poderosas es que son **ejecutables**: las herramientas pueden hacer cumplir estas reglas automáticamente (validadores de esquemas, puertas de enlace de API, *frameworks* de prueba y servidores simulados).

#### Elementos clave que hacen que OAS sea eficaz como acuerdo vinculante

Varios elementos críticos otorgan a OpenAPI su poder como contrato vinculante:

1. **Definiciones de esquemas con reglas de validación**: En `components/schemas`, defines estructuras de datos con restricciones precisas (`minLength`, `maxLength`, `enum`, `minimum`, `maximum`):
```yaml
components:
  schemas:
    MagicWand:
      type: object
      required: [name, wandType, powerLevel]
      properties:
        name:
          type: string
          minLength: 3
          maxLength: 50
        wandType:
          type: string
          enum: [oak, elder, phoenix, dragon]
        powerLevel:
          type: integer
          minimum: 1
          maximum: 10
```

2. **Obligatoriedad frente a opcionalidad explícita**: Marcar claramente lo que es requerido (`required: true` o listas `required: [...]`) y los valores por defecto (`default: false`):
```yaml
/orders:
  post:
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [itemId, quantity]
            properties:
              itemId:
                type: string
              quantity:
                type: integer
                minimum: 1
              giftWrap:
                type: boolean
                default: false
```

3. **Estructuras y códigos de estado de respuesta definidos**: Especificar todos los resultados posibles:
```yaml
/items/{itemId}:
  get:
    responses:
      '200':
        description: Successful retrieval of magic item
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/MagicItem'
      '404':
        description: Item not found
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Error'
```

4. **Restricciones de parámetros**: Delimitar de forma estricta los valores de entrada aceptables:
```yaml
/spells:
  get:
    parameters:
      - name: elemType
        in: query
        schema:
          type: string
          enum: [fire, water, earth, air]
      - name: minPower
        in: query
        schema:
          type: integer
          minimum: 1
          maximum: 10
```

5. **Ejemplos y valores predeterminados**: Proporcionar ilustraciones concretas del comportamiento esperado:
```yaml
/potions:
  get:
    responses:
      '200':
        content:
          application/json:
            example:
              - id: "health-potion"
                name: "Minor Healing Potion"
                effect: "Restores 25 health points"
                price: 50
```

#### Herramientas basadas en OAS en todo tu flujo de trabajo

Tener una API definida en formato OAS impulsa la automatización a lo largo de todo el proceso de desarrollo:

- **Generadores de documentación**: Transforman especificaciones en portales interactivos con consolas *Try it out* (ejemplos: **Swagger UI**, **Redoc**, **GitBook**).
- **Servidores simulados (*Mock servers*)**: Crean una API ficticia funcional que devuelve datos realistas a partir de los esquemas, permitiendo el desarrollo en paralelo de *frontend* y *backend* (ejemplos: **Stoplight Prism**, **Microcks**, **WireMock**).
- **Validadores (*Linters* y verificadores de cumplimiento)**: Comprueban que tanto el documento OAS como la implementación cumplan con los estándares y esquemas (ejemplos: **Spectral**, **Open Policy Agent**).
- **Generadores de código**: Crean implementaciones base de servidor con validación integrada y bibliotecas cliente (*SDKs*) tipadas y seguras (ejemplo: **OpenAPI Generator**).
- **Configuraciones de API Gateways**: Automatizan la configuración de enrutamiento, autenticación, cuotas y limitación de tasa (*rate limiting*) directamente desde OAS (ejemplos: **Apigee**, **Amazon API Gateway**, **Kong**).
- **Frameworks de pruebas**: Generan suites de pruebas automatizadas y verifican escenarios de éxito y error contra el contrato (ejemplos: **Prism**, **Schemathesis**).

#### Desplazamiento a la izquierda (*Shift-Left*): Detectar problemas de API antes de que ocurran

«Desplazarse a la izquierda» significa mover las actividades de validación a las fases más tempranas del ciclo de vida del desarrollo:

1. **Validación del contrato durante el diseño**:
```bash
# Conceptual: Validating the contract itself using spectral
spectral lint magic-items-api.yaml
```

2. **Validación en tiempo de ejecución durante el desarrollo**: Validación estricta de peticiones entrantes y respuestas generadas.
3. **Pruebas integrales contra el contrato**: Generación de casos de prueba basados en esquemas y rangos.
4. **Barreras de validación (*Validation Gates*) en CI/CD**:
   - Validación de la especificación (*linting*)
   - Análisis estático para detectar cambios incompatibles (*breaking changes*)
   - Pruebas de contrato en entornos de prueba
   - Validación de esquemas de respuesta

A continuación se muestra un flujo de trabajo de GitHub Actions que aplica estas comprobaciones:

```yaml
name: API Contract Validation
on:
  push:
    branches: [ main ]
jobs:
  validate-contract:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - name: Install dependencies
        run: npm ci
      # 1. Specification validation with Spectral
      - name: Lint OpenAPI spec
        run: npx @stoplight/spectral lint api/magic-items-api.yaml
      # 2. Static analysis (breaking-change detection) with openapi-changes
      - name: Check for breaking changes
        run: npx openapi-changes api/openapi-prev.yaml api/openapi.yaml --fail-on breaking
      # 3. Contract testing with Prism
      - name: Start test environment
        run: docker-compose -f docker-compose.test.yml up -d
      - name: Validate contract with Prism
        run: npx @stoplight/prism validate api/magic-items-api.yaml http://localhost:3000
      # 4. Schema validation in responses with Schemathesis
      - name: Validate response schemas
        run: npx schemathesis run api/magic-items-api.yaml --checks all
      - name: Tear down test environment
        if: always()
        run: docker-compose -f docker-compose.test.yml down
```

#### Transformación de equipos con la adopción de OAS

OAS actúa como un catalizador para el cambio organizacional:
- **Decisiones de diseño claras y consistentes**: Nombres de recursos coherentes, patrones de parámetros predecibles y manejo de errores uniforme mediante estándares objetivos y automatizados.
- **Un lenguaje común para todos**: Conecta las historias de usuario de los *Product Managers*, las maquetas de los diseñadores, el código de los desarrolladores y las pruebas de *QA*.
- **Desarrollo impulsado por contratos (*Contract-First*)**:
  $$\text{Requisitos de Negocio} \longrightarrow \text{Contrato OAS} \longrightarrow \text{Implementación}$$
  Permite el trabajo desacoplado y en paralelo entre equipos, eliminando bloqueos y acelerando los tiempos de entrega.

---

### Buenas prácticas para el uso de la Especificación OpenAPI

#### Diseño de estructuras de API claras y coherentes

##### Organización lógica de los recursos

Estructura los recursos reflejando las relaciones naturales del dominio:

```yaml
paths:
  /items:
    description: Collection of all magical items in the store
    # Operations on the collection   
  /items/{itemId}:
    description: Individual magical item identified by its unique ID
    # Operations on a specific item   
  /categories:
    description: Types of magical items (potions, wands, scrolls, etc.)
    # Operations on the collection of categories   
  /categories/{categoryId}:
    description: A specific category of magical items
    # Operations on a specific category   
  /items/{itemId}/effects:
    description: Magical effects associated with a specific item
    # Operations related to a specific item's effects
```

##### Establecimiento de patrones de URL consistentes

- Usar **sustantivos en plural** para recursos de colección (`/items`, no `/item`).
- Usar nombres **concretos y específicos** (`/potions` en lugar de `/products`).
- Usar **guiones** para nombres compuestos (`/brewing-ingredients`).
- Usar **minúsculas** en todos los segmentos de URL.
- Usar identificadores de recursos en parámetros de ruta (`/items/{itemId}`).

##### Definición de operaciones significativas

Alinea los métodos HTTP con la semántica REST:

```yaml
paths:
  /items:
    get:
      summary: List all magical items
      description: Returns a paginated list of magical items with optional filtering
      operationId: listItems
      # Parameters, responses, etc.     
    post:
      summary: Create a new magical item
      description: Adds a new item to the magical inventory
      operationId: createItem
      # Request body, responses, etc.     
  /items/{itemId}:
    get:
      summary: Get a specific magical item
      description: Returns detailed information about a magical item
      operationId: getItem
      # Parameters, responses, etc.     
    put:
      summary: Update a magical item
      description: Replaces all properties of an existing magical item
      operationId: updateItem
      # Parameters, request body, responses, etc.     
    patch:
      summary: Partially update a magical item
      description: Updates specific properties of an existing magical item
      operationId: patchItem
      # Parameters, request body, responses, etc.     
    delete:
      summary: Remove a magical item
      description: Deletes a magical item from the inventory
      operationId: deleteItem
      # Parameters, responses, etc.
```

##### Convenciones de nomenclatura

- `camelCase` para `operationId` (ej. `listItems`, `createPotion`).
- `snake_case` para nombres de parámetros y propiedades de esquemas.
- `PascalCase` para nombres de esquemas (ej. `MagicItem`).
- `Hyphenated-Pascal-Case` para cabeceras HTTP (ej. `Content-Type`).
- Prefijar parámetros de consulta con su propósito (ej. `filter_rarity`).
- Verbos consistentes en `operationId` (`list`, `get`, `create`, `update`, `patch`, `delete`).

Ejemplo en esquema:

```yaml
components:
  schemas:
    MagicItem:
      type: object
      properties:
        id:
          type: string
          readOnly: true
          description: Unique identifier for the item
        name:
          type: string
          description: The name of the magical item
        rarity:
          type: string
          enum: [common, uncommon, rare, very_rare, legendary, artifact]
          description: The rarity classification of the item
        magic_type:
          type: string
          description: The type of magic imbued in the item
```

##### Creación de patrones de recursos coherentes

```yaml
paths:
  /potions:
    get:
      summary: List all potions
      parameters:
        - $ref: '#/components/parameters/Page'
        - $ref: '#/components/parameters/PageSize'
        - name: filter_effect
          in: query
          schema:
            type: string
        - name: sort_price
          in: query
          schema:
            type: string
            enum: [asc, desc]
            default: asc
      # Responses, etc.
  /wands:
    get:
      summary: List all wands
      parameters:
        - $ref: '#/components/parameters/Page'
        - $ref: '#/components/parameters/PageSize'
        - name: filter_wood_type
          in: query
          schema:
            type: string
        - name: sort_price
          in: query
          schema:
            type: string
            enum: [asc, desc]
            default: asc
      # Responses, etc.
```

##### Paginación, filtrado y ordenación

Define parámetros comunes reutilizables:

```yaml
components:
  parameters:
    Page:
      name: page
      in: query
      description: Page number for pagination
      schema:
        type: integer
        default: 1
        minimum: 1     
    PageSize:
      name: page_size
      in: query
      description: Number of items per page
      schema:
        type: integer
        default: 20
        minimum: 1
        maximum: 100     
    SortDirection:
      name: sort_direction
      in: query
      description: Direction to sort results
      schema:
        type: string
        enum: [asc, desc]
        default: asc
```

#### Aprovechamiento de componentes reutilizables

##### Creación de esquemas de componentes para estructuras comunes

```yaml
components:
  schemas:
    Rarity:
      type: string
      enum: [common, uncommon, rare, very_rare, legendary]
    MagicalEffect:
      type: object
      properties:
        name:
          type: string
        duration:
          type: string
```

Y su reutilización en otros esquemas:

```yaml
    Potion:
      properties:
        name:
          type: string
        rarity:
          $ref: '#/components/schemas/Rarity'
        effects:
          type: array
          items:
            $ref: '#/components/schemas/MagicalEffect'
```

##### Organización de componentes para la mantenibilidad

Agrupar esquemas de forma lógica por dominio o herencia (`allOf`):

```yaml
components:
  schemas:
    # Base structures
    MagicItemBase:
      type: object
      properties:
        id:
          type: string
        name:
          type: string         
    # Item type definitions
    Potion:
      allOf:
        - $ref: '#/components/schemas/MagicItemBase'
        - type: object
          # Potion-specific properties
    # Common structures
    PaginationInfo:
      type: object
      properties:
        total:
          type: integer
```

Para especificaciones grandes, considera la **modularización en múltiples archivos** vinculados mediante `$ref`.

#### Implementación de patrones comunes de API

##### Manejo robusto de errores con Problem Details (RFC 9457 / RFC 7807)

```yaml
components:
  schemas:
    Problem:
      type: object
      properties:
        type:
          type: string
          format: uri
          description: URI reference identifying the problem type
        title:
          type: string
          description: Short, human-readable summary of the problem
        status:
          type: integer
          description: HTTP status code
        detail:
          type: string
          description: Human-readable explanation specific to this occurrence
        instance:
          type: string
          format: uri
          description: URI reference identifying the specific occurrence
```

Y su uso en respuestas de error:

```yaml
responses:
  '400':
    description: Bad Request
    content:
      application/problem+json:
        schema:
          $ref: '#/components/schemas/Problem'
        example:
          type: "https://api.magicitems.com/problems/insufficient-magic"
          title: "Insufficient magical energy"
          status: 400
          detail: "This enchantment requires 50 mana, but only 30 is available"
          instance: "/enchantments/failed/12345"
```

##### Manejo de paginación
- **Basada en *offsets***: Adecuada para datos estables.
- **Basada en cursores**: Ideal para colecciones grandes y datos en tiempo real.

##### Evitar operaciones masivas (*bulk operations*) sincrónicas
Evita operaciones masivas sincrónicas que impliquen transacciones distribuidas. Prefiere peticiones individuales o procesamiento asíncrono.

##### Importancia de los ejemplos

```yaml
MagicPotion:
  type: object
  properties:
    # Properties definition
  example:
    id: "healing-potion-001"
    name: "Minor Healing Potion"
    effect: "Restores 25 health points"
    duration: "30 seconds"
```

##### Documentación de códigos de error y uso de `default`

Documenta explícitamente todos los códigos conocidos y reserva `default` para errores inesperados:

```yaml
responses:
  '400':
    # Specific 400 error documentation
  '404':
    # Specific 404 error documentation
  default:
    description: Unexpected error
    content:
      application/problem+json:
        schema:
          $ref: '#/components/schemas/Problem'
```

#### Implementación de operaciones de larga duración en APIs REST

##### Uso de 202 Accepted para procesamiento asíncrono

```yaml
/orders/bulk-import:
  post:
    summary: Import multiple orders in a single operation
    description: |
      Starts an asynchronous bulk import process.
      Returns 202 Accepted with a Location header pointing to status resource.
    requestBody:
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/BulkOrderImport'
    responses:
      '202':
        description: Import job accepted for processing
        headers:
          Location:
            schema:
              type: string
              format: uri
            description: URI to check the status of the import job
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JobStatus'
```

El cliente sondea (*polls*) el recurso de estado:

```yaml
/tasks/{taskId}:
  get:
    summary: Check the status of a long-running task
    parameters:
      # properties definition
    responses:
      '200':
        description: Current status of the task
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TaskStatus'
      '303':
        description: Task completed, redirect to result
        headers:
          Location:
            schema:
              type: string
              format: uri
            description: URI of the completed resource
```

##### Uso de 303 See Other para redirección tras la finalización

1. El cliente sondea el *endpoint* de estado de la tarea.
2. Al finalizar, el servidor responde con `303 See Other`.
3. La cabecera `Location` apunta al recurso del resultado final.
4. El cliente sigue la redirección usando `GET`.

*Figura 10.1: Tarea de larga duración*

> **Consejo rápido**: ¿Necesitas ver una versión de alta resolución de esta imagen? Abre este libro en el lector Packt Reader de última generación o consúltalo en la copia en PDF/ePub ([https://packtpub.com/unlock](https://packtpub.com/unlock)).

##### Callbacks y Webhooks para notificaciones

- **Callbacks**: El cliente proporciona una URL en la petición inicial para recibir la notificación de finalización:
```yaml
/enchantments:
  post:
    summary: Start an enchantment process
    requestBody:
      content:
        application/json:
          schema:
            type: object
            properties:
              # properties definition
              callback_url:
                type: string
                format: uri
                description: URL to be called when enchantment completes
    responses:
      '202':
        description: Enchantment process initiated
    callbacks:
      enchantmentComplete:
        '{$request.body#/callback_url}':
          post:
            requestBody:
              content:
                application/json:
                  schema:
                    $ref: '#/components/schemas/EnchantmentResult'
            responses:
              '200':
                description: Callback received successfully
```

- **Webhooks**: Registro persistente para flujos continuos de eventos:
```yaml
/webhook-registrations:
  post:
    summary: Register a webhook for magical item events
    requestBody:
      content:
        application/json:
          schema:
            type: object
            properties:
              url:
                type: string
                format: uri
              events:
                type: array
                items:
                  type: string
                  enum: [item.created, item.sold, enchantment.completed]
```

##### Buenas prácticas para operaciones de larga duración

- Usar siempre `202 Accepted` para peticiones asíncronas.
- Proporcionar un recurso de estado mediante la cabecera `Location` o en el cuerpo de la respuesta.
- Incluir un tiempo estimado de finalización mediante la cabecera `Retry-After`.
- Diseñar pensando en la **idempotencia**.
- Ofrecer mecanismos de cancelación.
- Considerar admitir tanto sondeo (*polling*) como *callbacks*.

#### Enfoques de versionado de APIs

La regla de oro del versionado es: **ningún cambio en tu API debe romper a los clientes existentes**. OpenAPI te permite documentar qué elementos son estables y cuáles están sujetos a evolución, manteniendo la compatibilidad hacia atrás (ver Capítulo 13 para más detalles).

---

### Resumen

En este capítulo, hemos explorado cómo la Especificación OpenAPI pasa de ser mera documentación a convertirse en un contrato vinculante para el desarrollo de APIs. Examinamos cómo OAS sirve como una fuente única de verdad que traduce requisitos abstractos de negocio en especificaciones ejecutables. A través del ejemplo de la Tienda de Artículos Mágicos, descubrimos cómo este enfoque centrado en contratos impulsa un potente ecosistema de herramientas para documentación, simulación (*mocking*), validación, generación de código y pruebas.

Investigamos las mejores prácticas para diseñar APIs claras y coherentes: estructuras lógicas de recursos, convenciones de nomenclatura uniformes y componentes reutilizables. También analizamos patrones de implementación para desafíos comunes como el manejo de errores (RFC 9457), la paginación y las operaciones de larga duración (asíncronas con `202 Accepted`, `303 See Other`, *callbacks* y *webhooks*).

En el próximo capítulo, profundizaremos en **JSON Schema**, explorando técnicas avanzadas de modelado y estrategias de validación para tus APIs.
