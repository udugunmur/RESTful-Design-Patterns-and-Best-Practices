# Parte 3: El Círculo del Archimago – Forjando y Haciendo Evolucionar los Contratos de API

## Capítulo 12: No Odies tu Hipermedia: Creación de APIs para Humanos e IAs

En capítulos anteriores, presentamos las restricciones de REST, incluida la hipermedia, a menudo pasada por alto. Este capítulo explora cómo la hipermedia transforma las APIs estáticas en sistemas dinámicos y autodescriptivos donde los clientes descubren las acciones disponibles a partir de las respuestas de la API, en lugar de depender de un conocimiento codificado rígidamente (*hardcoded*) de la estructura de la API.

A medida que la IA generativa y los modelos de lenguaje grande (*LLMs*) remodelan la forma en que los sistemas interactúan, la importancia de la hipermedia crece exponencialmente. Estos sistemas de IA prosperan cuando pueden descubrir y navegar las capacidades de la API de forma dinámica, lo que convierte a la hipermedia en el compañero perfecto para las interacciones impulsadas por IA. Exploraremos implementaciones prácticas, patrones comunes y mejores prácticas para crear APIs verdaderamente RESTful que no solo sean amigables para los humanos, sino que también estén preparadas para la IA, tanto para las necesidades de hoy como para las innovaciones del mañana.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **El poder de la hipermedia como restricción de REST**
- **Navegando por la implementación de hipermedia: patrones, formatos y desafíos**
- **Diseño de APIs de hipermedia para el consumo de IA**

Al finalizar este capítulo, comprenderás mejor los fundamentos teóricos de la hipermedia, podrás implementar patrones prácticos de hipermedia en tus APIs, superarás los desafíos de implementación habituales y diseñarás APIs que tanto los desarrolladores humanos como los sistemas de IA puedan descubrir y navegar eficazmente.

---

### El poder de la hipermedia como restricción de REST

En capítulos anteriores, establecimos que la hipermedia es una restricción crítica para las APIs verdaderamente RESTful, pero conocer la teoría e implementarla de manera efectiva son dos desafíos muy diferentes. Aunque la API de la Tienda de Artículos Mágicos pueda ofrecer operaciones CRUD básicas sin hipermedia, aún carece de la información contextual necesaria para un uso eficaz. Es como darle a alguien un mapa del tesoro sin leyenda: tiene los datos, pero carece del contexto para navegar con éxito.

Los controles de hipermedia convierten tu API en un sistema dinámico y autodescriptivo donde los clientes descubren capacidades a través de la navegación. Los clientes pueden simplemente seguir los enlaces y controles proporcionados por tu API en lugar de codificar rígidamente el conocimiento sobre la cancelación de pedidos o la disponibilidad de artículos.

#### Más allá del REST básico: implementar la verdadera hipermedia

Podrías pensar que tu API de la Tienda de Artículos Mágicos es RESTful porque utiliza métodos HTTP y códigos de estado adecuados (`GET` para detalles de pociones, `POST` para añadir varitas a los carritos y `404` para artefactos inexistentes). Aunque es un gran comienzo, esto solo representa el **Nivel 2 del Modelo de Madurez de Richardson** analizado en el Capítulo 6. El verdadero REST requiere hipermedia (**Nivel 3**), lo que permite a los clientes navegar por tu API únicamente a través de los controles proporcionados en cada respuesta. Muchas APIs que afirman ser RESTful carecen de este ingrediente crítico, lo que resulta en lo que algunos llaman APIs «REST-ish» (cuasi-REST).

##### El papel fundamental de la hipermedia en REST

El Nivel 1 nos dio recursos y URLs adecuados, el Nivel 2 agregó métodos HTTP y códigos de estado correctos, pero es el **Nivel 3: Controles de Hipermedia (HATEOAS)** el que completa el rompecabezas de REST. Sin hipermedia, se construyen APIs que pierden el principio central y revolucionario de REST: la capacidad de los clientes para descubrir y navegar dinámicamente las capacidades de la API.

Veamos cómo se traduce esto en la práctica:

Respuesta de API de Nivel 2 (sin hipermedia):

```json
// Level 2 API response 
{ 
  "id": "wand-1", 
  "name": "Oak Wand with Dragon Heartstring", 
  "price": 75.0, 
  "inStock": true, 
  "powerLevel": 8 
}
```

> **Consejo rápido**: Mejora tu experiencia de programación con las funciones AI Code Explainer y Quick Copy en el lector Packt Reader de última generación ([https://packtpub.com/unlock](https://packtpub.com/unlock)).

Esta respuesta proporciona datos, pero ninguna indicación de qué hacer a continuación. ¿Deberían los clientes adivinar que pueden añadir este artículo a su carrito en `/cart/items`? ¿Qué pasa si luego cambiamos ese *endpoint*?

En contraste, la verdadera hipermedia incluye controles que guían al cliente:

```json
// Level 3 API response with hypermedia controls 
{ 
  "id": "wand-1", 
  "name": "Oak Wand with Dragon Heartstring", 
  "price": 75.0, 
  "inStock": true, 
  "powerLevel": 8, 
  "_links": { 
    "self": { 
      "href": "/items/wand-1" 
    }, 
    "add-to-cart": { 
      "href": "/cart/items", 
      "method": "POST" 
    }, 
    "similar-items": { 
      "href": "/items?type=wand&powerLevel=8" 
    }, 
    "compatible-potions": { 
      "href": "/items/wand-1/compatible-potions" 
    } 
  } 
}
```

Otro error común es creer que simplemente incluir URLs en tu respuesta cuenta como hipermedia. La verdadera hipermedia proporciona no solo enlaces, sino también **contexto sobre lo que representan esos enlaces y cómo interactuar con ellos** (como el método HTTP a utilizar).

#### Evaluación de la madurez de la hipermedia de tu API

¿Cómo de madura es la implementación de hipermedia de tu API? Hazte estas preguntas prácticas:

1. **¿Puede un cliente navegar por toda tu API comenzando desde un único punto de entrada?** Intenta acceder a tu *endpoint* raíz (`/`) y comprueba si puedes descubrir cómo realizar acciones clave sin conocimiento previo.
2. **¿Incluyen las transiciones de estado toda la información necesaria?** Cuando se crea o actualiza un recurso, ¿incluye la respuesta enlaces para ver su estado, modificarlo o acceder a recursos relacionados?
3. **¿Son los tipos de relación de enlace (*link relations*) coherentes y significativos?**

Veamos qué podría devolver una implementación inmadura al realizar un pedido:

```json
{ 
  "orderId": "order-1234", 
  "status": "confirmed", 
  "total": 125.0, 
  "link": "/orders/order-1234" 
}
```

El cliente tiene que adivinar qué hacer a continuación. ¿Puede cancelar? ¿Ver los artículos? ¿Comprobar el envío? ¡No lo sabe!

#### De la teoría a la práctica: implementar la hipermedia

1. **Comienza con un índice de API**: Crea un punto de entrada detectable que enumere los recursos y acciones disponibles:
```http
GET https://magic-items.com/
```
```json
{ 
  "_links": { 
    "items": { 
      "href": "/items" 
    }, 
    "potions": { 
      "href": "/items?type=potion" 
    }, 
    "wands": { 
      "href": "/items?type=wand" 
    }, 
    "cart": { 
      "href": "/cart" 
    }, 
    "orders": { 
      "href": "/orders" 
    } 
  } 
}
```

2. **Añade enlaces contextuales a cada respuesta**: No te limites a devolver datos en bruto; incluye acciones relevantes:
```json
{ 
  "orderId": "order-1234", 
  "status": "confirmed", 
  "total": 125.0, 
  "_links": { 
    "self": { 
      "href": "/orders/order-1234" 
    }, 
    "cancel": { 
      "href": "/orders/order-1234/cancel", 
      "method": "POST" 
    }, 
    "items": { 
      "href": "/orders/order-1234/items" 
    }, 
    "payment": { 
      "href": "/orders/order-1234/payment" 
    } 
  } 
}
```

3. **Representa las transiciones de estado de forma explícita**: Si el estado de un pedido cambia a `shipped`, el enlace `cancel` debe desaparecer y aparecer un enlace `track`.
4. **Utiliza relaciones de enlace estandarizadas**: Consulta el registro de IANA ([https://www.iana.org/assignments/link-relations/link-relations.xhtml](https://www.iana.org/assignments/link-relations/link-relations.xhtml)) para relaciones estándar (`self`, `next`, `prev`, `collection`) y mantén la consistencia en relaciones de dominio (`brew-potion`, `enchant-item`).

#### Controles de hipermedia en la práctica

##### Implementación efectiva de relaciones de enlace (*Link Relations*)

```json
{ 
  "id": "crystal-wand-7", 
  "name": "Crystal Wand of Illumination", 
  "_links": { 
    "self": { 
      "href": "/items/crystal-wand-7" 
    }, 
    "next": { 
      "href": "/items/phoenix-feather-8" 
    }, 
    "collection": { 
      "href": "/items?type=wand" 
    }, 
    "enchant": { 
      "href": "/items/crystal-wand-7/enchantments" 
    } 
  } 
}
```

Nombra las relaciones describiendo la **relación**, no el destino (por ejemplo, `compatible-potions` es mucho mejor que `potions`).

##### Transiciones de estado como controles de hipermedia

Considera una poción mágica en estado `brewing` (elaborándose):

```json
{ 
  "id": "healing-potion-42", 
  "name": "Greater Healing Potion", 
  "state": "brewing", 
  "completionTime": "2023-09-15T14:30:00Z", 
  "_links": { 
    "self": { 
      "href": "/potions/healing-potion-42" 
    }, 
    "cancel-brewing": { 
      "href": "/potions/healing-potion-42/cancel", 
      "method": "POST" 
    }, 
    "check-status": { 
      "href": "/brewing-status/healing-potion-42" 
    } 
  } 
}
```

Cuando la poción pasa a estado `ready` (lista), sus enlaces cambian dinámicamente:

```json
{ 
  "id": "healing-potion-42", 
  "name": "Greater Healing Potion", 
  "state": "ready", 
  "_links": { 
    "self": { 
      "href": "/potions/healing-potion-42" 
    }, 
    "test-quality": { 
      "href": "/potions/healing-potion-42/test", 
      "method": "POST" 
    }, 
    "put-for-sale": { 
      "href": "/potions/healing-potion-42/sell", 
      "method": "POST" 
    } 
  } 
}
```

##### Acciones sensibles al contexto

Los controles de hipermedia se adaptan al rol del usuario que realiza la petición:

- **Vista del cliente**:
```json
{ 
  "name": "Crystal Wand of the Ancients", 
  "price": 500.0, 
  "_links": { 
    "self": { 
      "href": "/items/rare-crystal-wand" 
    }, 
    "add-to-cart": { 
      "href": "/cart/items", 
      "method": "POST" 
    } 
  } 
}
```

- **Vista del administrador**:
```json
{ 
  "name": "Crystal Wand of the Ancients", 
  "price": 500.0, 
  "cost": 250.0, 
  "_links": { 
    "self": { 
      "href": "/items/rare-crystal-wand" 
    }, 
    "update": { 
      "href": "/admin/items/rare-crystal-wand", 
      "method": "PUT" 
    }, 
    "adjust-inventory": { 
      "href": "/admin/inventory/rare-crystal-wand" 
    } 
  } 
}
```

##### Equilibrio entre riqueza y simplicidad

No sobrecargues cada respuesta con todos los enlaces posibles. Incluye solo los enlaces más probables para el siguiente paso del cliente:

```json
{ 
  "id": "healing-potion-42", 
  "name": "Greater Healing Potion", 
  "_links": { 
    "self": { 
      "href": "/potions/healing-potion-42" 
    }, 
    "collection": { 
      "href": "/potions" 
    }, 
    "similar-potions": { 
      "href": "/potions?similar-to=healing-potion-42" 
    }, 
    "details": { 
      "href": "/potions/healing-potion-42/details" 
    } 
  } 
}
```

---

### Navegando por la implementación de hipermedia: patrones, formatos y desafíos

#### Patrones esenciales de diseño de hipermedia

##### Navegación en colecciones: paginación, filtrado y ordenación

- **Enlaces de paginación**:
```json
{ 
  "items": [ 
    { 
      "id": "product-123", 
      "name": "Healing Potion" 
    } // More items... 
  ], 
  "_links": { 
    "self": { 
      "href": "/products?page=2" 
    }, 
    "next": { 
      "href": "/products?page=3" 
    }, 
    "prev": { 
      "href": "/products?page=1" 
    } 
  } 
}
```

- **Metadatos de la colección**:
```json
{ 
  "page": { 
    "size": 10, 
    "totalElements": 118, 
    "totalPages": 12, 
    "number": 2 
  } 
}
```

- **Filtrado y ordenación con enlaces con plantilla (*URI Templates*)**:
```json
{ 
  "_links": { 
    "filter": { 
      "href": "/products{?category,min_price}", 
      "templated": true 
    } 
  } 
}
```

```json
{ 
  "_links": { 
    "sort": { 
      "href": "/products{?sort}", 
      "templated": true, 
      "options": ["price_asc", "price_desc", "name"] 
    } 
  } 
}
```

##### Patrones de descubrimiento de recursos relacionados

```json
{ 
  "id": "product-123", 
  "name": "Healing Potion", 
  "_links": { 
    "self": { 
      "href": "/products/123" 
    }, 
    "similar": { 
      "href": "/products/123/similar" 
    }, 
    "ingredients": { 
      "href": "/products/123/ingredients" 
    } 
  } 
}
```

O incrustando recursos mediante vistas previas (`_embedded`):

```json
{ 
  "id": "cart-456", 
  "_embedded": { 
    "items": [ 
      { 
        "name": "Healing Potion", 
        "quantity": 2, 
        "_links": { 
          "self": { 
            "href": "/products/123" 
          } 
        } 
      } 
    ] 
  } 
}
```

##### Vías dinámicas: acciones condicionales y disponibilidad

- **Omitir enlaces no disponibles**:
```json
{ 
  "name": "Healing Potion", 
  "inStock": false, 
  "_links": { 
    "self": { 
      "href": "/products/123" 
    }, 
    "notify": { 
      "href": "/notifications/product-123", 
      "method": "POST" 
    } // No "add-to-cart" link when out of stock 
  } 
}
```

- **Incluir acciones marcando explícitamente su indisponibilidad**:
```json
{ 
  "id": "order-456", 
  "_links": { 
    "cancel": { 
      "href": "/orders/456/cancel", 
      "method": "POST", 
      "available": false, 
      "reason": "Order already shipped" 
    } 
  } 
}
```

> **Reutilización**: Las acciones contextuales deben expresar las capacidades de la aplicación en el estado actual, independientemente de si el cliente es web, móvil o de escritorio.

#### Elección del formato de hipermedia adecuado

Formatos estándar de hipermedia más extendidos:
- **HAL (*Hypertext Application Language*)**: [https://datatracker.ietf.org/doc/html/draft-kelly-json-hal-11](https://datatracker.ietf.org/doc/html/draft-kelly-json-hal-11)
- **JSON-LD**: [https://json-ld.org/](https://json-ld.org/)
- **Siren**: [https://github.com/kevinswiber/siren](https://github.com/kevinswiber/siren)
- **JSON:API**: [https://jsonapi.org/](https://jsonapi.org/)
- **Problem Details para manejo de errores (`application/problem+json`)**: [https://www.rfc-editor.org/rfc/rfc9457](https://www.rfc-editor.org/rfc/rfc9457)

#### Superar los desafíos de implementación

##### Consideraciones sobre bibliotecas cliente

Diseña bibliotecas cliente para que descubran enlaces dinámicamente y permitan una degradación gradual (*graceful degradation*) si ciertos controles están ausentes.

##### Estrategias de adopción incremental y compatibilidad hacia atrás

Comienza con un enfoque «hypermedia-lite» añadiendo `_links` a tus respuestas JSON existentes:

```json
{ 
  "name": "Healing Potion", 
  "price": 29.99, 
  "_links": { 
    "self": { 
      "href": "/products/potion-123" 
    } 
  } 
}
```

Utiliza la **negociación de contenido** para admitir clientes antiguos y nuevos simultáneamente:

```http
Accept: application/vnd.magicitems.v1+json 
Accept: application/vnd.magicitems.hypermedia+json
```

---

### Diseño de APIs de hipermedia para el consumo de IA

A medida que los agentes de IA se convierten en consumidores clave de APIs, la naturaleza autodescriptiva de la hipermedia se vuelve indispensable para permitir la navegación y la toma de decisiones autónomas sin necesidad de rutas codificadas rígidamente.

#### Comprensión de los patrones de consumo de API por parte de la IA

- **Humanos frente a IA**: Los humanos se apoyan en el contexto implícito y la documentación; la IA requiere estructuras legibles por máquina, metadatos explícitos (métodos HTTP, descripciones) y transiciones de estado accionables.
- **Capacidades de la IA**:
  - *Reconocimiento de patrones*: Detección de anomalías y tendencias en el historial de compras.
  - *Comprensión del contexto*: Interpretación de intenciones y roles.
  - *Razonamiento*: Inferencia de necesidades (por ejemplo, sugerir un caldero si se añaden ingredientes sin equipo de preparación).

#### Limitaciones actuales y evolución esperada

- **Barreras de contexto**: La IA puede no entender relaciones implícitas de flujo de trabajo si no se declaran explícitamente.
- **Descubrimiento y navegación**: La combinación de hipermedia con cargas semánticas estandarizadas permite a los agentes autónomos ejecutar procesos de negocio complejos de principio a fin.

#### APIs navegables por IA: diseñando para el consumo de máquinas

- **Punto de entrada raíz estructurado con introspección (`/schema`)**:
```http
GET /
```
```json
{ 
  "name": "Magic Items Store API", 
  "_links": { 
    "products": { 
      "href": "/products" 
    }, 
    "orders": { 
      "href": "/orders" 
    }, 
    "schema": { 
      "href": "/schema" 
    } 
  } 
}
```

- **Divulgación progresiva (*Progressive Disclosure*)**:
```http
GET /products/healing-potion
```
```json
{ 
  "id": "healing-potion", 
  "name": "Healing Potion", 
  "_links": { 
    "add-to-cart": { 
      "href": "/cart/items", 
      "method": "POST" 
    }, 
    "similar-products": { 
      "href": "/products/healing-potion/similar" 
    } 
  } 
}
```

- **Consistencia en los controles de paginación**:
```http
GET /products?page=2
```
```json
{ 
  "items": [ 
    { 
      "id": "invisibility-potion", 
      "name": "Invisibility Potion" 
    } 
  ], 
  "_links": { 
    "self": { 
      "href": "/products?page=2" 
    }, 
    "first": { 
      "href": "/products?page=1" 
    }, 
    "prev": { 
      "href": "/products?page=1" 
    }, 
    "next": { 
      "href": "/products?page=3" 
    } 
  }, 
  "page": { 
    "size": 10, 
    "totalElements": 128, 
    "totalPages": 13, 
    "number": 2 
  } 
}
```

- **Documentación enriquecida en OpenAPI para IAs**:
```yaml
paths:
  /products/{productId}:
    get:
      summary: Retrieve a specific product
      description: >
        Returns detailed information about a magical item in the inventory…
      parameters:
        - name: productId
          in: path
          required: true
          description: The unique id of the magical item
          schema:
            type: string
            example: healing-potion
      responses:
        200:
          description: Successfully retrieved product details
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
              example:
                id: healing-potion
                name: Healing Potion
                description: Restores 50 hp instantly
                price: 29.99
                category: potions
```

#### Máquinas de estado y árboles de decisión en el diseño de APIs

- **Modelar flujos de trabajo complejos como máquinas de estado**.
- **Preservación del contexto en procesos de múltiples pasos** (evitando reingresar datos como métodos de pago o direcciones de envío).
- **Guiar a la IA a través de árboles de decisión estructurados**.

> **Modelado de flujos de trabajo con Arazzo**:  
> La Especificación Arazzo ([https://www.openapis.org/arazzo](https://www.openapis.org/arazzo)) documenta flujos de trabajo estáticos deterministas en OpenAPI para desarrolladores e IAs, complementando el descubrimiento en tiempo de ejecución de la hipermedia.

#### Ejemplos prácticos y preparación para el futuro

- **Estructura unificada de recursos**:
```json
{ 
  "id": "potion-123", 
  "type": "product", 
  "attributes": { 
    "name": "Healing Potion", 
    "price": 29.99, 
    "category": "potions", 
    "tags": ["health", "restoration"] 
  }, 
  "_links": { 
    "self": { 
      "href": "/products/potion-123" 
    }, 
    "related": { 
      "href": "/products/potion-123/related" 
    } 
  }
}
```

- **Descubrimiento y manipulación de contenido**:
```json
{ 
  "_links": { 
    "search": { 
      "href": "/search{?q,category}", 
      "templated": true 
    } 
  }, 
  "_templates": { 
    "fields": [ 
      { 
        "name": "q", 
        "type": "string", 
        "description": "Search query" 
      }, 
      { 
        "name": "category", 
        "type": "string", 
        "description": "Product category" 
      } 
    ]
  }
}
```

- **Búsqueda y filtrado para consumo de IA**:
```http
GET /products?category=potions&page=2
```
```json
{ 
  "_links": { 
    "self": {
      "href": "/products?category=potions&page=2"
    }, 
    "next": {
      "href": "/products?category=potions&page=3"
    }, 
    "prev": {
      "href": "/products?category=potions&page=1"
    } 
  }, 
  "_embedded": { 
    "items": [ 
      { 
        "id": "potion-456", 
        "name": "Mana Potion", 
        "price": 25.99 
      }
    ]
  }
}
```

- **Adaptación a capacidades emergentes de IA con árboles de acción (`_actions`)**:
```json
{ 
  "_actions": [ 
    { 
      "name": "reorder-stock", 
      "method": "POST", 
      "href": "/inventory/reorder", 
      "fields": [ 
        { 
          "name": "productId", 
          "value": "item-789" 
        }, 
        { 
          "name": "quantity", 
          "value": 50 
        } 
      ]
    }
  ]
}
```

---

### Resumen

En este capítulo, hemos explorado cómo las APIs con hipermedia cierran la brecha entre los desarrolladores humanos y los sistemas de IA. Comenzando con los principios de diseño verdaderamente RESTful (HATEOAS / Nivel 3 de RMM), abordamos el lado práctico de la implementación de hipermedia: paginación, filtrado, relaciones de enlace y gestión de colecciones.

Analizamos cómo la IA navega por las estructuras de las APIs, destacando la importancia de la claridad semántica y los patrones consistentes. Al modelar flujos de trabajo como máquinas de estado y árboles de decisión dinámicos, demostramos cómo guiar a los agentes de IA a través de procesos complejos de forma autónoma.

En el próximo capítulo, nos sumergiremos en la **gestión del cambio de APIs** y exploraremos estrategias para el versionado y la evolución sin romper las integraciones existentes.
