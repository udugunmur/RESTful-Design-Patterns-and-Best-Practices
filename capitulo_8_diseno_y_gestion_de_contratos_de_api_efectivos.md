# Parte 2: El Grimorio del Mago – Dominando los Fundamentos de REST

## Capítulo 8: Diseño y Gestión de Contratos de API Efectivos

En el ecosistema digital actual en rápida evolución, las APIs se han convertido en la piedra angular del desarrollo e integración de software. Permiten que diferentes sistemas de software se comuniquen sin problemas, fomentando la innovación y la eficiencia en todas las industrias. Sin embargo, a medida que crece la dependencia de las APIs, también lo hace la complejidad de gestionarlas de manera eficaz. Aquí es donde entra en juego el concepto de **contratos de API (*API contracts*)**.

Un contrato de API sirve como un acuerdo formal que define las expectativas y responsabilidades tanto de los proveedores como de los consumidores de la API. Describe cómo se comporta una API, los datos que expone, los protocolos que utiliza y los términos bajo los cuales opera. Elaborar un contrato de API eficaz no es solo una cuestión de especificaciones técnicas; se trata de establecer un entendimiento mutuo que garantice consistencia, seguridad y fiabilidad.

Este capítulo profundiza en la importancia de los contratos de API bien elaborados, explorando su definición e importancia en el ciclo de vida de la API. Nuestro objetivo es agilizar el uso futuro de la API y promover una comunicación abierta entre todas las partes interesadas desde el principio. Al anticipar aplicaciones futuras e incorporar conceptos como el diseño orientado al consumidor (*consumer-driven design*) y los modelos de madurez de APIs, podemos diseñar APIs robustas, escalables y adaptables a necesidades cambiantes. Este capítulo explora el porqué y el cómo de la elaboración de contratos de API sólidos. Aprenderás sobre lo siguiente:

- Por qué los contratos de API son esenciales para escalar los programas de API y reducir la fricción de integración
- Los bloques de construcción centrales de un contrato de API, incluidos *endpoints*, esquemas de petición/respuesta, métodos de autenticación y manejo de errores
- Buenas prácticas para gestionar contratos de API a lo largo del tiempo, incluido el versionado de contratos, pruebas de compatibilidad y adopción de pruebas de contratos orientadas al consumidor (*consumer-driven contract testing*)
- Cómo alinear tus contratos con el ciclo de vida de la API y los procesos de gobernanza, desde el diseño inicial hasta la desaprobación (*deprecation*)

Al finalizar este capítulo, comprenderás cómo los contratos de API moldean la experiencia del desarrollador, reducen los malentendidos y ayudan a que tus APIs evolucionen de forma segura manteniendo a tus consumidores sincronizados.

---

### Requisitos técnicos

- **Conocimientos básicos de APIs**: Familiaridad con tipos de APIs (REST, gRPC y GraphQL) y métodos HTTP.
- **Herramientas de especificación de APIs**: Experiencia con OpenAPI, AsyncAPI o gRPC, y comprensión de la sintaxis JSON/YAML.
- **Comprensión de conceptos de desarrollo de software**: Conocimiento de modelado de datos, validación de esquemas y prácticas de seguridad (autenticación y limitación de tasa).
- **Comprensión de control de versiones y CI/CD**: Conocimientos básicos de Git/GitHub y familiaridad con pruebas y validaciones automatizadas.
- **Contexto de negocio**: Comprensión de Acuerdos de Nivel de Servicio (*Service-Level Agreements* / SLAs), políticas de uso y cómo las APIs se alinean con los objetivos de negocio.

---

### Comprensión del concepto e importancia de los contratos de API

Los contratos de API son la columna vertebral de una comunicación de APIs eficaz. Definen cómo se comportan las APIs, los datos que exponen y las reglas sobre cómo deben interactuar los consumidores con ellas. Estos contratos aseguran que los proveedores y consumidores de la API tengan una comprensión compartida, reduciendo la ambigüedad y fomentando la colaboración.

En esta sección, desglosaremos los elementos clave de un contrato de API y explicaremos cómo cada componente contribuye a la coherencia, la seguridad y la fiabilidad. Comenzaremos explorando los bloques de construcción centrales que forman un contrato de API bien definido, como definiciones de recursos, modelos de datos y protocolos de seguridad. A continuación, analizaremos cómo la adopción de especificaciones estandarizadas como OpenAPI y AsyncAPI puede simplificar la gestión de APIs y garantizar la escalabilidad a largo plazo.

#### ¿Qué es un contrato de API?

Un contrato de API es un acuerdo detallado que define el comportamiento esperado, las capacidades y el uso de una API. Actúa como un plano directriz y un apretón de manos formal entre proveedores y consumidores, describiendo lo que ofrece la API y las pautas para su uso. En esencia, un contrato de API representa un diseño de API aprobado, lo que garantiza interacciones coherentes y predecibles.

*Figura 8.1: Contrato de API*

En su núcleo, un contrato de API incluye lo siguiente:

- **Detalles de invocación**: Descripciones detalladas de los *endpoints* de la API, incluidas URLs, métodos HTTP, parámetros de petición y formatos de respuesta.
- **Modelos de datos**: Esquemas que definen la estructura de los datos que se envían y reciben, incluidos tipos de campo, restricciones y reglas de validación.
- **Protocolos de seguridad y acceso**: Especificaciones de mecanismos de autenticación y autorización, estándares de cifrado y otras medidas de seguridad.
- **Políticas de uso**: Términos de servicio, límites de tasa (*rate limits*), cuotas y cualquier consideración legal o requisito de cumplimiento normativo.
- **Expectativas de rendimiento**: SLAs que describen garantías de tiempo de actividad (*uptime*), tiempos de respuesta y compromisos de soporte.

Los contratos de API adoptan frecuentemente especificaciones ampliamente utilizadas, tales como:

- OpenAPI
- gRPC
- GraphQL
- AsyncAPI

Estos estándares agilizan el proceso para los usuarios de la API al:

- Ofrecer directrices claras que reducen el esfuerzo requerido para diseñar y mantener contratos de API
- Proporcionar conjuntos de herramientas robustos y soporte comunitario activo, lo que los convierte en una opción práctica sobre soluciones personalizadas
- Mejorar la incorporación de desarrolladores (*onboarding*), permitiendo a nuevos desarrolladores comprender la estructura y funcionalidad de la API más fácilmente a través de convenciones familiares

Típicamente, estos estándares definen elementos clave como la funcionalidad de la API, estructuras de datos y esquemas, mecanismos de seguridad, respuestas de error y limitaciones de uso.

##### Extensibilidad de OpenAPI

Aprovechar una especificación de API suele ser suficiente para encapsular todos los aspectos de un contrato de API. Por ejemplo, la Especificación OpenAPI proporciona una potente extensibilidad a través de propiedades personalizadas conocidas como extensiones, que tienen el prefijo `x-`, como se muestra a continuación:

```yaml
openapi: 3.0.0
info:
  title: Example API
  version: 1.0.0
  x-business-owner: "Product Strategy Team"
  x-support-tier: "Premium"
  x-deprecation-timeline: "Q4 2025"
...
```

Estas extensiones te permiten capturar detalles o funcionalidades no cubiertas intrínsecamente por el estándar central, garantizando un contrato de API más completo.

Con una comprensión sólida de lo que constituye un contrato de API, el siguiente paso es explorar por qué estos contratos son tan vitales, examinando cómo fomentan la alineación entre equipos, mitigan riesgos y garantizan integraciones fluidas. Al comprender su valor, obtendrás conocimientos más profundos sobre cómo los contratos de API contribuyen al éxito tanto técnico como estratégico de las APIs.

#### La importancia de los contratos de API

Los contratos de API son fundamentales para el desarrollo de software moderno, ya que sirven como modelo de cómo funcionan, se comunican e integran las APIs en todos los sistemas. Su papel en el impulso de la coherencia, la colaboración, la seguridad y la eficiencia no puede subestimarse. Las organizaciones que priorizan los contratos de API bien definidos obtienen una ventaja competitiva al entregar software de alta calidad más rápido, reducir incidentes y fomentar una mejor colaboración.

##### Garantizar la coherencia y la previsibilidad

Un contrato de API bien elaborado acelera la entrega de aplicaciones al tiempo que reduce los incidentes relacionados con las APIs. Según el informe *State of API Report 2023* de Postman ([https://www.postman.com/state-of-api/2023/](https://www.postman.com/state-of-api/2023/)), las organizaciones con contratos de API formales reportan un tiempo de comercialización hasta un **70% más rápido** para nuevas funciones. Esta velocidad se atribuye a la reducción de la ambigüedad en el comportamiento de la API, lo que permite a los desarrolladores centrarse en crear funciones en lugar de solucionar problemas de integración. Por ejemplo, **Netflix** utiliza contratos de API ampliamente para agilizar el lanzamiento de funciones en su plataforma global, asegurando una integración fluida entre microservicios.

Esta aceleración se debe en gran medida a la estandarización que los contratos de API aportan a los flujos de trabajo de desarrollo. Al establecer definiciones coherentes de las estructuras de petición y respuesta, los contratos de API permiten a los desarrolladores predecir el comportamiento de la API con confianza, eliminando la necesidad de aclaraciones que consumen mucho tiempo entre equipos. Considera el contrato de API de **Stripe**, que proporciona especificaciones detalladas sobre *endpoints* y códigos de error, lo que permite a los desarrolladores integrar sistemas de pago sin problemas y sin un constante ida y vuelta con el equipo de soporte. Esta previsibilidad se vuelve especialmente valiosa al gestionar integraciones complejas entre múltiples servicios.

La coherencia proporcionada por los contratos de API también se traduce directamente en una reducción de la sobrecarga operativa. Los equipos con contratos de API estandarizados experimentan una **reducción del 65% en incidentes relacionados con APIs**, y el tiempo promedio de resolución de incidentes disminuye en un **45%**. Por ejemplo, el uso de contratos de API por parte de **Shopify** garantiza la detección temprana de errores durante las pruebas de integración, lo que les permite evitar tiempos de inactividad para sus comerciantes en todo el mundo. Este enfoque proactivo para la prevención de incidentes es posible gracias a la validación estructurada que permiten los contratos.

A partir de esta base de estandarización, los contratos de API facilitan procesos de validación automatizados que mantienen la fiabilidad del ecosistema. Al definir las entradas y salidas esperadas, los contratos permiten que las herramientas de prueba verifiquen el cumplimiento antes del despliegue, creando una red de seguridad que detecta problemas antes de que lleguen a los entornos de producción.

Estas capacidades de validación se extienden de forma natural a prácticas mejoradas de monitorización y observabilidad. Al definir explícitamente qué constituye un comportamiento normal frente a anomalías, los contratos facilitan la configuración de alertas y paneles que proporcionan información significativa. Por ejemplo, **Amazon API Gateway** aprovecha los contratos de API para habilitar la monitorización en tiempo real, lo que ayuda a las organizaciones a identificar y abordar cuellos de botella de rendimiento de manera más eficaz.

Más allá de los beneficios técnicos, los contratos de API fomentan relaciones más sólidas entre proveedores y consumidores de API al establecer expectativas claras y confianza mutua. Cuando **Twilio** publica contratos detallados para sus APIs de comunicación, los desarrolladores de todo el mundo ganan confianza al integrar servicios de voz, mensajería y video, sabiendo que las especificaciones son fiables y precisas. Esta confianza se convierte en la base para una colaboración más amplia entre equipos y organizaciones.

Establecer coherencia y previsibilidad en las APIs hace más que agilizar el desarrollo: fomenta un entorno donde la colaboración puede prosperar. Cuando el comportamiento de la API está bien definido y es predecible, los equipos pueden alinearse más fácilmente, reduciendo la confusión y generando confianza en cómo interactúan los diferentes servicios. Esta claridad sirve como una base poderosa para la colaboración entre equipos, asegurando que tanto las partes interesadas internas como externas puedan contribuir eficazmente a los proyectos de API.

##### Facilitar la colaboración

Los contratos de API mejoran significativamente la colaboración al actuar como un punto de referencia compartido para todas las partes interesadas, incluidos los desarrolladores de *backend* y *frontend*, los equipos de control de calidad (*QA*) y los analistas de negocio. Al proporcionar claridad sobre las capacidades de la API, los contratos **reducen la sobrecarga de comunicación en un 40%** y **reducen las preguntas relacionadas con la integración en un 50%**. Por ejemplo, **Amazon** utiliza contratos de API para alinear a los equipos durante el desarrollo de funciones, minimizando malentendidos y retrasos.

Esta base colaborativa se vuelve aún más esencial a medida que las organizaciones escalan sus ecosistemas de APIs. En arquitecturas de microservicios, donde decenas o cientos de equipos gestionan servicios independientes, los contratos de API sirven como una fuente única de verdad que elimina la ambigüedad y asegura que todos trabajen hacia los mismos objetivos. La adopción de contratos de API por parte de **adidas** ejemplifica este enfoque, permitiendo que sus equipos de ingeniería escalen de manera eficiente manteniendo una comunicación coherente entre servicios.

Los beneficios de este enfoque unificado se extienden más allá de los equipos internos para abarcar también las asociaciones externas. Las empresas que adoptan contratos de API integrales reportan una **reducción del 60% en el tiempo de incorporación (*onboarding*)** para nuevos consumidores de API, ya que las especificaciones claras eliminan las conjeturas y aceleran los procesos de integración. Por ejemplo, la documentación detallada de la API de **HubSpot**, basada en contratos robustos, permite a los socios integrar capacidades de CRM más rápido y con menos errores.

Dentro de los flujos de trabajo de desarrollo internos, las diferentes partes interesadas aprovechan los contratos de API de maneras especializadas que respaldan sus responsabilidades únicas:

- Los equipos de **control de calidad (QA)** utilizan los contratos como base para pruebas y validaciones automatizadas, lo que les permite identificar problemas de integración en una etapa temprana del ciclo de desarrollo. **GitHub Actions** demuestra este enfoque de manera efectiva, con flujos de trabajo que aprovechan los contratos de API para validar las integraciones de la API de GitHub antes del despliegue.
- Los **analistas de negocio** encuentran valor en los contratos de API, ya que brindan información clara sobre la funcionalidad de la API y las posibles oportunidades comerciales. Los analistas de **Spotify**, por ejemplo, utilizan contratos de API para identificar oportunidades para nuevas integraciones y evaluar el impacto potencial en el negocio, asegurando que el ecosistema de APIs se alinee con los objetivos estratégicos y genere resultados comerciales significativos.

Este enfoque integral para la alineación de las partes interesadas crea en última instancia un entorno en el que los consumidores externos pueden construir con confianza. Empresas como **Slack** han aprovechado contratos sólidos para crear prósperos ecosistemas de desarrolladores, donde terceros pueden crear aplicaciones e integraciones con confianza sabiendo que tienen una referencia fiable para el comportamiento esperado de la API. Esta confianza constituye la columna vertebral de las asociaciones exitosas y del crecimiento de la plataforma.

Si bien la colaboración es clave para desarrollar y escalar APIs exitosas, hacer evolucionar las APIs a lo largo del tiempo sin romper las integraciones existentes es igualmente importante. Las estrategias efectivas de gestión de versiones y control de cambios son esenciales para equilibrar la innovación con la estabilidad. Al integrar políticas de versionado en los contratos de API, los equipos pueden introducir nuevas funciones manteniendo la compatibilidad, lo que garantiza una transición fluida para todos los consumidores.

##### Mitigar el cambio y gestionar versiones

Gestionar los cambios en las APIs es una tarea compleja pero crítica. Los contratos de API ayudan a mitigar los riesgos asociados con el cambio al incorporar estrategias de versionado sólidas. Por ejemplo, el uso que hace **Stripe** de contratos de API versionados garantiza que los desarrolladores puedan continuar usando versiones anteriores mientras se adaptan a las nuevas funciones a lo largo del tiempo.

*Figura 8.2: Versionado de la API de Stripe*

> **Consejo rápido**: ¿Necesitas ver una versión de alta resolución de esta imagen? Abre este libro en el lector Packt Reader de última generación o consúltalo en la copia en PDF/ePub.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

El **versionado semántico (*Semantic Versioning*)**, comunicado a través de contratos de API, es otra estrategia común para gestionar cambios. Indica si las actualizaciones son correcciones menores a nivel de parche o cambios importantes que rompen la compatibilidad (*breaking changes*). **GitHub** emplea el versionado semántico en sus actualizaciones de API, lo que brinda a los desarrolladores expectativas claras sobre la compatibilidad con versiones anteriores y los plazos de adaptación.

A partir de este enfoque de comunicación transparente, muchas organizaciones extienden su estrategia de versionado para incluir programas de acceso temprano que avisan a los consumidores con anticipación sobre los próximos cambios. El acceso avanzado a nuevas versiones de los contratos de API permite a los consumidores planificar y probar integraciones de forma proactiva, convirtiendo las posibles interrupciones en transiciones controladas. Por ejemplo, la API de **Google Maps** proporciona contratos beta detallados para las próximas funciones, lo que permite a los desarrolladores probar y adaptar sus aplicaciones antes de los lanzamientos públicos.

Los contratos de API también agilizan las políticas de desaprobación (*deprecation*), asegurando que los consumidores tengan tiempo suficiente para migrar a nuevas versiones. **AWS** ofrece avisos de desaprobación integrados en los contratos de API, lo que permite a los desarrolladores realizar la transición sin interrupciones.

En arquitecturas de microservicios, el versionado se vuelve aún más crítico. Los contratos aseguran que los cambios en un servicio no rompan inadvertidamente las dependencias en otros. La implementación de contratos de API por parte de **Netflix** en sus microservicios garantiza actualizaciones fluidas sin afectar la experiencia general del usuario.

Finalmente, una sólida gestión del cambio posibilitada por los contratos de API reduce el riesgo de fallos en la integración. Por ejemplo, los contratos de API versionados de **Shopify** ayudan a los comerciantes a actualizar sus aplicaciones sin problemas, manteniendo la continuidad del negocio durante los cambios en la plataforma.

Gestionar eficazmente los cambios en la API garantiza estabilidad y adaptabilidad, pero es solo una parte de la ecuación. La seguridad y la fiabilidad son igualmente críticas para mantener un ecosistema de APIs exitoso. Los contratos de API desempeñan un papel vital en la protección de datos confidenciales y en el cumplimiento de las normativas de la industria. Más allá de la gestión de cambios, estos contratos sientan las bases para prácticas de seguridad sólidas, monitorización proactiva y una fiabilidad mejorada.

##### Mejorar la seguridad y la fiabilidad

Las APIs son puertas de entrada a datos confidenciales, lo que convierte a la seguridad en una prioridad absoluta. Los contratos de API describen métodos de autenticación, alcances de autorización y estándares de cifrado, actuando como una salvaguarda contra el acceso no autorizado y las filtraciones de datos. El informe de Postman revela que los equipos que aprovechan los contratos de API reportan un **55% menos de incidentes de seguridad**, lo que subraya su importancia en la gestión proactiva de la seguridad.

Los contratos de API también especifican límites de tasa y expectativas de rendimiento, lo que reduce la probabilidad de abusos o interrupciones. Los contratos de la API de **GitHub** incluyen detalles sobre la limitación de tasa, protegiendo la plataforma de peticiones excesivas y garantizando al mismo tiempo un uso justo para todos los desarrolladores.

Para industrias sensibles al cumplimiento normativo, como las finanzas o la salud, los contratos de API son indispensables. Los contratos describen explícitamente las prácticas de manejo de datos y los requisitos de cumplimiento, como **GDPR** o **HIPAA**.

La monitorización y la observabilidad mejoran significativamente con contratos de API establecidos. Al definir SLAs y métricas dentro de los contratos, las organizaciones pueden garantizar la fiabilidad y la disponibilidad.

Por último, los contratos de API permiten revisiones de seguridad coherentes durante el ciclo de vida del desarrollo. Al integrar herramientas de seguridad de API *ad hoc*, las organizaciones pueden automatizar las pruebas de seguridad e identificar vulnerabilidades de forma temprana.

Si bien la seguridad y la fiabilidad son esenciales para proteger tu ecosistema de APIs, un enfoque *API-first* va un paso más allá al hacer que el contrato de API sea la base del desarrollo. Esta estrategia proactiva permite a los equipos colaborar eficazmente y entregar funciones más rápido sin comprometer la estabilidad ni la calidad. Los contratos de API no solo agilizan el desarrollo, sino que también fomentan la innovación al alinear la implementación técnica con los objetivos de negocio desde el principio.

##### Respaldar el diseño y desarrollo orientado a la API (*API-First*)

En un enfoque *API-first*, el contrato de API sirve como base para el desarrollo y, a menudo, se crea antes de escribir cualquier línea de código. Esto permite a los equipos posteriores crear simulaciones (*mocks*) y prototipos, lo que permite el desarrollo en paralelo y un tiempo de comercialización más rápido. Por ejemplo, la estrategia *API-first* de **adidas** permite a sus equipos lanzar nuevas características de producto rápidamente.

Los contratos de API aseguran la alineación entre equipos, reduciendo el retrabajo y los retrasos. Al establecer expectativas claras desde el principio, los desarrolladores pueden construir contra una especificación coherente. **Spotify**, por ejemplo, utiliza contratos de API para mantener la alineación entre sus servicios de *backend* y las integraciones de terceros.

Los contratos de API también facilitan la aceptación de las partes interesadas al principio del proceso. Al proporcionar un artefacto tangible para revisión, los equipos pueden recopilar comentarios e iterar antes de comprometerse con el desarrollo.

Finalmente, un enfoque *API-first* respaldado por contratos acelera la innovación. Al desacoplar los ciclos de desarrollo, los equipos pueden experimentar con nuevas ideas manteniendo la estabilidad.

Para aprovechar todo el potencial de los contratos de API, es crucial comprender sus elementos fundamentales. Los contratos de API se crean utilizando una combinación de especificaciones, herramientas y mejores prácticas que garantizan su fiabilidad y eficacia a lo largo de los ciclos de vida del desarrollo. En la siguiente sección, exploraremos estos componentes clave.

---

### Introducción a los bloques de construcción del contrato de API

Un contrato de API eficaz se compone de varios componentes clave que definen colectivamente cada aspecto de la funcionalidad, el uso y la gobernanza de la API. Comprender estos bloques de construcción es esencial para crear contratos que sean a la vez completos y manejables. En esta sección, me centraré en las APIs REST y en OpenAPI como los marcos principales para definir y estandarizar contratos de API, ofreciendo ideas prácticas sobre sus características únicas y las mejores prácticas para su implementación.

#### Especificaciones técnicas

La especificación técnica de un contrato de API sirve como una guía completa para desarrolladores, que describe instrucciones precisas sobre cómo interactuar con la API. Proporciona esquemas de modelos detallados, lo que permite a los desarrolladores implementar un manejo de datos robusto en sus aplicaciones al tiempo que garantiza coherencia y precisión. Además, la especificación define claramente los requisitos de seguridad, lo que ayuda a prevenir el acceso no autorizado y a proteger los datos confidenciales de manera eficaz.

##### Definición de endpoints

La descripción de la API resume los aspectos técnicos de la API, incluyendo lo siguiente:

- **Endpoints y métodos**: Información detallada sobre cada *endpoint*, incluidas las URLs y los métodos HTTP admitidos (`GET`, `POST`, `PUT`, `DELETE`, etc.).
- **Parámetros de petición**: Definiciones de parámetros obligatorios y opcionales para cada *endpoint*, incluidos parámetros de ruta, parámetros de consulta, cabeceras y contenido del cuerpo.
- **Formatos de respuesta**: Descripciones de las respuestas esperadas, incluidos códigos de estado, cabeceras y cuerpos de respuesta.

Este es un ejemplo de la definición del *endpoint* `/users`, que devuelve una lista de usuarios. El *endpoint* acepta parámetros de filtro y paginación, lo que permite a los desarrolladores refinar sus consultas. Responde con un array de objetos `User` en formato `application/json`:

```yaml
...
paths:
  /users:
    get:
      summary: "Retrieve a list of users"
      description: "Returns an array of users with basic information."
      parameters:
        - name: page
          in: query
          description: "Page number for pagination"
          required: false
          schema:
            type: integer
            example: 1
        - name: limit
          in: query
          description: "Maximum number of items to return per page"
          required: false
          schema:
            type: integer
            example: 10
        - name: filter
          in: query
          description: "Filter criteria for the list of users (e.g., by role, status)"
          required: false
          schema:
            type: string
            example: "role=admin"
      responses:
        '200':
          description: "A list of users"
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
```

Después de definir los *endpoints* del contrato de API, el siguiente componente técnico crítico que se debe describir son los modelos de datos y sus esquemas.

##### Modelos de datos y esquemas

Definir modelos de datos y esquemas es crucial para garantizar que los datos intercambiados a través de la API se estructuren y validen de manera coherente. Esto incluye:

- **Definiciones de campos**: Nombres, tipos de datos y restricciones para cada campo en los cuerpos de petición y respuesta.
- **Reglas de validación**: Condiciones que deben cumplir los datos, como valores mínimos y máximos, longitudes de cadenas y coincidencia de patrones.
- **Cuerpos de ejemplo (*Example payloads*)**: Peticiones y respuestas de muestra que ilustran los formatos de datos esperados.

Este es un ejemplo de definición de un modelo de datos `User`, incluidas sus propiedades:

```yaml
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: string
          description: "Unique identifier for the user"
        name:
          type: string
          description: "Full name of the user"
        email:
          type: string
          format: email
          description: "Email address of the user"
        createdAt:
          type: string
          format: date-time
          description: "Timestamp when the user was created"
      required:
        - id
        - name
        - email
```

> **Nota**  
> Utilizamos principalmente JSON Schema para definir estos modelos. Para una comprensión más profunda de JSON Schema, consulta el Capítulo 11.

##### Marco de seguridad (*Security framework*)

Los protocolos de seguridad son un componente crítico del contrato de API. Definen lo siguiente:

- **Métodos de autenticación**: Si la API utiliza claves de API (*API keys*), OAuth 2.0, tokens JWT u otros mecanismos de autenticación.
- **Alcances de autorización (*Scopes*)**: Permisos y niveles de acceso otorgados a diferentes usuarios o aplicaciones.
- **Estándares de cifrado**: Requisitos para el cifrado de datos en tránsito y en reposo.

Como ejemplo, un contrato de API puede definir múltiples métodos de seguridad. Algunos *endpoints* pueden protegerse mediante una clave de API y otros mediante el protocolo OAuth 2.0. Ambos se muestran a continuación:

```yaml
components:
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://example.com/oauth/authorize
          tokenUrl: https://example.com/oauth/token
          scopes:
            read: "Read access to protected resources"
            write: "Write access to protected resources"
security:
  - ApiKeyAuth: []
  - OAuth2:
      - read
      - write
```

Habiendo comprendido el bloque de construcción de especificaciones técnicas de un contrato de API, exploremos el segundo bloque de construcción, que se centra en definir los aspectos de negocio de un contrato de API.

#### Compromisos comerciales (*Business commitments*)

Más allá de los aspectos técnicos, los contratos de API también deben abordar su uso desde una perspectiva de negocio, un área que a menudo está poco representada hoy en día. Este descuido suele ocurrir porque los contratos de API se consideran tradicionalmente artefactos puramente técnicos centrados en *endpoints*, modelos de datos y protocolos de seguridad. Sin embargo, descuidar elementos relacionados con el negocio, como SLAs, políticas de uso y modelos de monetización, puede generar brechas en las expectativas del consumidor, lo que lleva a desalineaciones y a una menor confianza.

Documentar los aspectos de negocio en los contratos de API fomenta una mejor colaboración entre proveedores y consumidores al establecer expectativas claras sobre el rendimiento, los límites de uso y las políticas operativas. Esta transparencia genera confianza y ayuda a los consumidores a planificar su integración de manera más efectiva, asegurando que la API satisfaga tanto las necesidades técnicas como las comerciales.

##### Acuerdos de Nivel de Servicio (SLAs)

El contrato de API debe describir cómo se pretende utilizar la API desde una perspectiva de negocio. Esto incluye:

- **Modelos de monetización**: Información sobre precios, ciclos de facturación y métodos de pago si la API se ofrece como un servicio de pago.
- **Límites de uso**: Límites de tasa, cuotas y políticas de regulación (*throttling*) que rigen con qué frecuencia se puede llamar a la API.
- **Procesos de incorporación**: Pasos requeridos para obtener acceso a la API, como registro, aprobación de solicitudes y emisión de claves de API.

Ahí es donde entran los **SLAs**. Definen las expectativas de rendimiento y fiabilidad de la API, incluyendo:

- **Garantías de tiempo de actividad (*Uptime guarantees*)**: La disponibilidad esperada de la API, a menudo expresada como un porcentaje (por ejemplo, 99,9% de tiempo de actividad).
- **Tiempos de respuesta**: Latencia máxima aceptable para las respuestas de la API.
- **Soporte y mantenimiento**: Detalles sobre disponibilidad de soporte técnico, ventanas de mantenimiento y tiempos de respuesta ante incidentes.

Aunque OpenAPI no admite de forma nativa descripciones de SLA, la especificación **SLA4OAI** ofrece un marco preliminar para definir SLAs junto con OpenAPI. Esto permite a los proveedores detallar los SLAs en un formato legible por máquina, mejorando la transparencia y la confianza con los consumidores.

El siguiente ejemplo demuestra cómo SLA4OAI puede definir tres planes distintos para una API:

```yaml
sla: 1.0.0
context:
  id: magicstore-sample
  type: plans
  api:
    $ref: ./magicstore-service.yml
  provider: ISAGroup
metrics:
  requests:
    type: "int64"
    description: "Number of requests"
plans:
  base:
    availability: R/00:00:00Z/23:00:00Z
  free:
    rates:
      /products/{id}:
        get:
          requests:
            - max: 1
              period: second
    quotas:
      /products:
        post:
          requests:
            - max: 10
              period: minute
  pro:
    pricing:
      cost: 5
      currency: EUR
      billing: monthly
    rates:
      /products/{id}:
        get:
          requests:
            - max: 100
              period: second
```

Esta estructura permite a los proveedores de API definir SLAs de forma transparente:
- **base**: Garantiza la disponibilidad diaria pero no impone límites de uso específicos ni precios. Adecuado para uso general o de prueba.
- **free**: Ofrece un uso limitado con límites de tasa estrictos, como 1 petición por segundo para operaciones `GET` y 10 peticiones por minuto para operaciones `POST`.
- **pro**: Introduce límites de uso más altos, como 100 peticiones por segundo para operaciones `GET`, e incluye una suscripción mensual de pago a un precio de 5 EUR.

> **Nota**  
> Si no estás listo para adoptar SLA4OAI, existen métodos alternativos para incorporar SLAs en los contratos de API:
> - **Extensiones OpenAPI personalizadas**: Utiliza campos `x-` para agregar detalles relacionados con SLA, como garantías de tiempo de actividad y límites de tasa.
> - **Plataformas de gestión de APIs**: Plataformas como Apigee, Amazon API Gateway y Azure API Management admiten la aplicación de SLAs mediante herramientas integradas.

##### Políticas operativas (*Operational policies*)

Las políticas operativas establecen los procesos y estándares necesarios para garantizar que la API funcione de manera eficiente, segura y coherente. Los componentes clave de las políticas operativas incluyen:

- **Limitación de tasa y regulación (*Rate limiting and throttling*)**: Mecanismos para controlar el flujo de tráfico, prevenir abusos y garantizar un uso justo entre los consumidores de la API.
- **Versionado**: Pautas claras para gestionar las actualizaciones del ciclo de vida de la API, incluidas estrategias para introducir nuevas versiones, desaprobar las antiguas y mantener la compatibilidad hacia atrás.
- **Manejo de errores**: Enfoques estandarizados para comunicar errores, incluidos códigos de error consistentes, mensajes significativos y orientación para resolver problemas.

El siguiente ejemplo demuestra una respuesta `429 Too Many Requests` para el *endpoint* `/users`. Esta respuesta se devuelve cuando un consumidor de la API excede los límites de uso permitidos:

```yaml
paths:
  /users:
    get:
      responses:
        '429':
          description: "Too Many Requests"
          content:
            application/json:
              schema:
                type: object
                properties:
                  error:
                    type: string
                    example: "Rate limit exceeded"
```

##### Cumplimiento normativo y requisitos legales

Dependiendo de la naturaleza de los datos y de la industria, el contrato de API puede necesitar abordar el cumplimiento de regulaciones tales como:

- **Reglamento General de Protección de Datos (GDPR)**: Para el manejo de datos personales en la Unión Europea
- **Ley de Portabilidad y Responsabilidad del Seguro Médico (HIPAA)**: Para información de salud en los Estados Unidos
- **Estándar de Seguridad de Datos para la Industria de Tarjeta de Pago (PCI DSS)**: Para el procesamiento de información de tarjetas de crédito

La sección legal del contrato de API cubre:

- **Términos de servicio**: Reglas que rigen cómo se puede utilizar la API, incluidas las actividades prohibidas.
- **Derechos de propiedad intelectual**: Propiedad de la API y cualquier trabajo derivado.
- **Responsabilidad e indemnización**: Limitaciones de responsabilidad y responsabilidades en caso de violaciones de datos u otros problemas.

El campo `termsOfService` en OpenAPI te permite vincular a un documento externo de Términos de Servicio que define los términos legales para usar la API:

```yaml
openapi: 3.0.3
info:
  title: User management API
  version: 1.0.0
  termsOfService: "https://example.com/terms"
  contact:
    name: API Support
    email: support@example.com
    url: "https://example.com/support"
...
```

En este ejemplo, el campo `termsOfService` enlaza a `https://example.com/terms`, que contiene el acuerdo legal completo. El contrato de API en sí no incluye estos términos legales directamente, sino que se refiere al documento externo, lo que garantiza que los consumidores tengan fácil acceso al marco legal completo.

---

### Gestión de tus contratos de API

La gestión eficaz de los contratos de API es fundamental para construir un ecosistema de APIs resistente, escalable y seguro. Sin una gestión adecuada, la proliferación de APIs puede generar desafíos importantes, como duplicación, inconsistencia y vulnerabilidades de seguridad.

#### El desafío de la proliferación de APIs (*API Sprawl*)

Uno de los riesgos más importantes de una mala gestión de contratos de API es la **proliferación descontrolada de APIs (*API sprawl*)**. Esto ocurre cuando una organización crea numerosas APIs sin una estrategia centralizada ni gobernanza. Con el tiempo, estas APIs se convierten en un ecosistema fragmentado, creando ineficiencias operativas y erosionando la experiencia del desarrollador:

- **Duplicación**: Los equipos a menudo reinventan la rueda desarrollando APIs redundantes con funcionalidades idénticas o superpuestas, lo que aumenta la sobrecarga de mantenimiento y desperdicia recursos.
- **Falta de estandarización**: Los ecosistemas fragmentados carecen de protocolos uniformes, presentan una calidad de documentación dispar y patrones de diseño divergentes, lo que fractura la experiencia del desarrollador.
- **Riesgos de seguridad**: Sin una estrategia unificada, resulta difícil hacer cumplir prácticas de seguridad consistentes en todo el ecosistema.
- **Menor descubribilidad**: Los desarrolladores tienen dificultades para encontrar o comprender las APIs que necesitan, lo que resulta en una infrautilización de los recursos disponibles.

#### Cómo abordar la proliferación de APIs

Hacer frente a la proliferación de APIs requiere un enfoque proactivo y estructurado:

##### Fuente Única de Verdad de la API (*Single Source of API Truth* / SSOT)

En el corazón de esta estrategia se encuentra el concepto de una **Fuente Única de Verdad de la API (SSOT)**. Un SSOT sirve como el punto de referencia autorizado para toda la información relacionada con la API dentro de una organización. Para las organizaciones *API-first*, el SSOT es típicamente la **especificación de la API**, mientras que para otras, la implementación puede tener prioridad.

Consolidar las APIs en un único punto de referencia elimina los silos y fomenta la alineación entre equipos. Un ejemplo destacado de este enfoque es **adidas**, que mejoró la entrega de sus APIs al establecer una sólida fuente única de verdad para las APIs. Según las directrices de API de adidas ([https://adidas.gitbook.io/api-guidelines](https://adidas.gitbook.io/api-guidelines)), la organización sigue un principio *API-first* que extiende el enfoque *design-first*. Para adidas, el diseño de la API (su descripción y esquema) sirve como el maestro de la verdad, no la implementación. Cada implementación de API debe adherirse estrictamente al diseño de la API, que actúa como el contrato vinculante entre la API y sus consumidores.

*Figura 8.3: Extracto de las directrices de API de adidas*

##### Implementación de un repositorio central de diseño de APIs

Un repositorio central de diseño de APIs sirve como una plataforma dedicada para gestionar y compartir contratos de API, actuando como la columna vertebral de la gestión del ciclo de vida de las APIs.

Los beneficios clave incluyen:
- **Descubribilidad mejorada**: Almacenar contratos en una ubicación accesible permite a los desarrolladores localizarlos rápidamente y fomenta la reutilización.
- **Control de versiones robusto**: El seguimiento de los cambios a lo largo del tiempo ayuda a gestionar múltiples versiones y a mantener la compatibilidad hacia atrás.
- **Colaboración**: Proporciona un espacio compartido para que los productores y consumidores de la API brinden retroalimentación antes de que comience la implementación.
- **Automatización de CI/CD**: Permite la validación automatizada mediante *pipelines* para garantizar que cada API cumpla con los estándares organizacionales antes del despliegue.

Un ejemplo notable es **Back Market**, un mercado en línea de productos electrónicos reacondicionados que mejoró significativamente la entrega y la seguridad de sus APIs mediante la implementación de un repositorio de diseño de APIs ([https://engineering.backmarket.com/leveling-up-apis-at-back-market-659e43d7e063](https://engineering.backmarket.com/leveling-up-apis-at-back-market-659e43d7e063)).

#### Gestión de contratos de API con GitHub: Caso de uso de la Tienda de Artículos Mágicos

La Tienda de Artículos Mágicos ha escalado a cientos de equipos. Para evitar la proliferación descontrolada de APIs, adopta GitHub como su repositorio central de diseño de APIs:

1. **Almacenar especificaciones de API**: Aloja todas sus especificaciones OpenAPI y AsyncAPI en repositorios de GitHub con control de versiones.
2. **Colaborar mediante Pull Requests (PRs)**: Exige la presentación de PRs para introducir cambios en los contratos de API, permitiendo discusiones y revisiones de diseño entre productores y consumidores antes de la aprobación.
3. **Validación automatizada**: Integra herramientas de código abierto como **Spectral** (para análisis estático / *linting*) y **Prism** (para simulación / *mocking*) en sus flujos de trabajo de GitHub Actions.

A continuación se muestra el flujo de trabajo automatizado de validación:

```yaml
name: API Spec Validation
on:
  pull_request:
    paths:
      - "apis/**.yaml"
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
      - name: Install Spectral
        run: npm install -g @stoplight/spectral-cli
      - name: Lint API Specification
        run: spectral lint apis/magic-inventory-api.yaml
```

En este ejemplo, el flujo de trabajo se activa en cada PR que involucra cambios en las especificaciones de API bajo la ruta `apis/**.yaml`. Los pasos incluyen descargar el código, instalar Spectral y ejecutar el proceso de análisis estático sobre el archivo `magic-inventory-api.yaml`. Esta validación automatizada garantiza que la especificación de la API se adhiera a los estándares organizacionales y reduce el riesgo de que se introduzcan errores o inconsistencias.

---

### Resumen

Elaborar y gestionar contratos de API eficaces es fundamental para construir un ecosistema de APIs robusto, escalable y eficiente. Este capítulo exploró el concepto de los contratos de API, enfatizando su papel como acuerdos formales que definen las expectativas y responsabilidades de los proveedores y consumidores de APIs. Con pautas claras para detalles de invocación, modelos de datos, protocolos de seguridad, políticas de uso y expectativas de rendimiento, los contratos de API garantizan coherencia, fiabilidad y alineación entre las partes interesadas.

La importancia de los contratos de API se extiende más allá de las especificaciones técnicas para incluir beneficios estratégicos como fomentar la colaboración, mitigar riesgos, gestionar cambios y mejorar la seguridad. Al permitir la validación automatizada, optimizar la generación de documentación e integrar sistemas de aprovisionamiento, los flujos de trabajo de contratos de API reducen el esfuerzo manual, minimizan los problemas de comunicación y aceleran la innovación. Además, centralizar las especificaciones de API en un repositorio de diseño ayuda a abordar la proliferación descontrolada de APIs, asegurando la descubribilidad, reduciendo la duplicación y mejorando la gobernanza.

En conclusión, los contratos de API bien definidos y bien administrados no son solo artefactos técnicos, sino herramientas estratégicas que permiten a las organizaciones escalar eficientemente, mantener la calidad y respaldar la innovación. Al adoptar buenas prácticas como pruebas de contratos, repositorios centralizados y flujos de trabajo automatizados, las organizaciones pueden transformar sus ecosistemas de APIs en activos que impulsen la colaboración, reduzcan el tiempo de comercialización y fomenten la confianza entre todas las partes interesadas.

En el próximo capítulo, nos centraremos en comprender la Especificación OpenAPI (*OpenAPI Specification*). Exploraremos sus orígenes y propósito, examinaremos cómo respalda el diseño eficaz de APIs REST y analizaremos la estructura que la convierte en una herramienta tan poderosa.
