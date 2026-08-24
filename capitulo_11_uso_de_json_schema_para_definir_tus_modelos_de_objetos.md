# Parte 3: El Círculo del Archimago – Forjando y Haciendo Evolucionar los Contratos de API

## Capítulo 11: Uso de JSON Schema para Definir tus Modelos de Objetos

Este capítulo explora el uso de JSON Schema en el diseño de APIs REST, basándose en el modelo de dominio establecido en capítulos anteriores. Nos centramos en definir los modelos de datos utilizados en la Especificación OpenAPI analizados en los dos capítulos previos. El capítulo cubre la creación, validación y documentación de estructuras JSON complejas para garantizar la coherencia y fiabilidad en el diseño de tu API.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **Comprensión de JSON Schema**
- **JSON Schema en acción**
- **Buenas prácticas para el uso de JSON Schema**

Al finalizar este capítulo, conocerás todos los detalles de JSON Schema para crear definiciones avanzadas de modelos para los recursos de tu API. También habrás explorado cómo abordar la evolución de un esquema y cómo integrarlo en tu flujo de trabajo de desarrollo, así como las mejores prácticas a considerar al crear esquemas.

---

### Requisitos técnicos

Para trabajar eficazmente en este capítulo sobre JSON Schema, necesitarás varias tecnologías e instalaciones clave para practicar los conceptos y ejemplos presentados. Es fundamental contar con un editor de texto moderno o un IDE con soporte para JSON y YAML, como Visual Studio Code con la extensión JSON Schema Store. El entorno también debe admitir Git para el control de versiones al trabajar con los ejemplos. Todo el código incluido en este capítulo está disponible en GitHub en [https://github.com/API-Peak/RESTful-Design-Patterns/blob/main/Chapter10-JSON-Schema](https://github.com/API-Peak/RESTful-Design-Patterns/blob/main/Chapter10-JSON-Schema).

---

### Comprensión de JSON Schema

Hoy en día, casi todas las APIs REST exponen datos en formato JSON. Es crucial definir estos datos de forma estricta para garantizar que nuestro contrato, documentado como un archivo de la Especificación OpenAPI, permanezca libre de ambigüedades. Comprender cómo utilizar JSON Schema es esencial para crear APIs bien definidas. En esta sección, exploraremos su propósito y cómo crear archivos de esquema de manera eficaz.

#### Naturaleza abierta (*Open nature*)

A diferencia de los esquemas XML, que son cerrados por naturaleza, JSON Schema se considera **abierto**. Esto significa que JSON Schema permite de forma inherente definiciones flexibles que pueden admitir propiedades adicionales no definidas explícitamente en el esquema. Esta apertura promueve la extensibilidad y la interoperabilidad, pero también puede introducir ambigüedad, lo que requiere definir cuidadosamente todas las restricciones necesarias. Por el contrario, los esquemas cerrados garantizan que solo se permitan los elementos definidos explícitamente en tu código.

#### Introducción a JSON Schema

JSON Schema es un lenguaje descriptivo utilizado para definir la estructura y el contenido de los datos JSON. Ofrece un método claro y conciso para especificar el formato esperado, los tipos y las restricciones de los objetos JSON, asegurando que los datos se adhieran a un esquema predefinido. JSON Schema está escrito en el propio JSON, lo que facilita su lectura y comprensión para cualquiera que ya esté familiarizado con la notación JSON. JSON Schema desempeña un papel clave en la descripción de APIs REST, ya que la Especificación OpenAPI lo aprovecha para describir todos los modelos de datos.

> **OpenAPI y JSON Schema**  
> Es importante tener en cuenta que el soporte completo para JSON Schema se introdujo en la versión 3.1.0 de OpenAPI. Antes de esto, especialmente en la versión 2.0, OpenAPI utilizaba un subconjunto de JSON Schema con ciertas peculiaridades que no existían en el JSON Schema estándar. Esto podía dar lugar a casos extremos que no eran totalmente compatibles.

El propósito de JSON Schema es proporcionar una forma estandarizada de describir la estructura, restricciones y relaciones de los datos descritos en formato JSON. Específicamente, nos permite garantizar varias cualidades importantes de los datos JSON:

- **Validar datos JSON contra un esquema predefinido**: De esta manera, aseguramos que los datos estén bien formados y dentro de todas las restricciones requeridas. Esta cualidad es especialmente importante para las APIs REST, ya que los formatos de datos coherentes son cruciales para la interoperabilidad.
- **Servir como documentación para estructuras de datos JSON**: Proporciona una descripción clara e inequívoca del formato de datos esperado, facilitando que los desarrolladores comprendan y trabajen con los datos. Al ser legible por máquina, se puede generar documentación comprensible tanto para desarrolladores como para cualquier otra parte interesada.
- **Promover la interoperabilidad**: Permite que diferentes sistemas y aplicaciones acuerden un formato de datos común, reduciendo el riesgo de inconsistencias al intercambiar información.
- **Automatizar procesos de desarrollo**: Puede usarse para generar código, crear casos de prueba y validar datos automáticamente, mejorando la eficiencia y reduciendo la probabilidad de errores.

#### Conceptos básicos

##### Tipos de datos

Especificar tipos de datos en JSON Schema es esencial para garantizar la consistencia y fiabilidad de los datos. Definir los tipos esperados para cada campo establece reglas claras que evitan el procesamiento de datos no válidos o inesperados.

JSON Schema define varios tipos de datos centrales:

- **`string`**: Representa una secuencia de caracteres Unicode. Permite validaciones adicionales como restricciones de longitud (`minLength`, `maxLength`), comprobaciones de formato (`date-time`, `email`, `uri`) y restricciones mediante expresiones regulares (`pattern`).
- **`number`**: Representa cualquier valor numérico, incluidos enteros y números de punto flotante. Permite especificar restricciones como valores mínimos y máximos (`minimum`, `maximum`, `exclusiveMinimum`, `exclusiveMaximum`).
- **`integer`**: Subtipo de `number` que solo acepta números enteros. Admite restricciones como `multipleOf` para garantizar la divisibilidad por un valor específico.
- **`boolean`**: Representa un valor `true` o `false`. Se utiliza frecuentemente para indicadores (*flags*) o interruptores (*toggles*).
- **`array`**: Representa una lista ordenada de elementos. Permite especificar el tipo de elementos (`items`), el número mínimo/máximo de elementos (`minItems`, `maxItems`) y si los elementos deben ser únicos (`uniqueItems`).
- **`object`**: Representa una colección de pares clave-valor (claves como cadenas y valores de cualquier tipo). Permite definir propiedades requeridas (`required`), dependencias de propiedades y restricciones sobre propiedades adicionales (`additionalProperties`).
- **`null`**: Representa la ausencia de un valor. A menudo se usa en combinación con otros tipos para indicar que un campo puede ser de un tipo específico o nulo.

> **Lectura adicional**  
> Para obtener más información sobre los tipos de datos de JSON Schema, consulta el sitio web oficial: [https://json-schema.org/understanding-json-schema/reference/type](https://json-schema.org/understanding-json-schema/reference/type).

##### Estructura básica de un JSON Schema

Un JSON Schema es en sí mismo un objeto JSON que contiene un conjunto de palabras clave:

- **`$schema`**: Define la versión de la especificación de JSON Schema que se está utilizando:
```json
{
  "$schema": "http://json-schema.org/2020-12/schema#"
}
```

- **`title` y `description`**: Proporcionan un título y una descripción legibles por humanos:
```json
{
  "title": "Magic Item Schema",
  "description": "A schema definition for a Magic Item data object."
}
```

- **`type`**: Especifica el tipo de datos descrito por el esquema (`object`, `array`, `string`, etc.).
- **`properties`**: Define las propiedades de un objeto:
```json
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "weight": {
      "type": "number"
    }
  }
}
```

- **`items`**: Define el esquema para los elementos dentro de un array:
```json
{
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

- **`required`**: Especifica un array de nombres de propiedades que son obligatorias:
```json
{
  "required": [
    "name",
    "age"
  ]
}
```

- **`additionalProperties`**: Especifica si se permiten propiedades adicionales no definidas explícitamente:
```json
{
  "additionalProperties": false
}
```

> **Ejemplo de un JSON Schema completo**:  
> [https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/basic-structure.json](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/basic-structure.json)

#### Conceptos avanzados

##### Combinación de esquemas (`allOf`, `anyOf`, `oneOf` y `not`)

JSON Schema proporciona palabras clave potentes para combinar múltiples esquemas:

- **`allOf`**: Garantiza que los datos deben validarse contra **todos** los esquemas especificados (operación lógica AND / herencia):
```json
{
  "allOf": [
    {
      "properties": {
        "name": {
          "type": "string"
        }
      },
      "required": [
        "name"
      ]
    },
    {
      "properties": {
        "weight": {
          "type": "number",
          "minimum": 0.1
        }
      }
    }
  ]
}
```

> **Buenas prácticas**: Usa `allOf` para crear esquemas base con propiedades comunes y extenderlos para casos de uso específicos, reduciendo la duplicación.  
> **Aviso**: Solo `allOf` es compatible para combinar esquemas en OpenAPI 2.0 (Swagger 2.0).

- **`anyOf`**: Garantiza que los datos deben validarse contra **al menos uno** de los esquemas especificados (operación lógica OR):
```json
{
  "anyOf": [
    {
      "type": "string"
    },
    {
      "type": "number"
    }
  ]
}
```

- **`oneOf`**: Garantiza que los datos deben validarse contra **exactamente uno** de los esquemas especificados (OR exclusivo):
```json
{
  "oneOf": [
    {
      "type": "string"
    },
    {
      "type": "number"
    }
  ]
}
```

- **`not`**: Garantiza que los datos **no deben** validarse contra el esquema especificado:
```json
{
  "not": {
    "type": "null"
  }
}
```

> **Compatibilidad con OpenAPI**: La Especificación OpenAPI no admite plenamente la palabra clave `not` en versiones inferiores a 3.1.0.

> **Ejemplo práctico de esquemas combinados**:  
> [https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/combining-schemas.json](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/combining-schemas.json)

##### Subesquemas condicionales (`if`, `then`, `else`)

JSON Schema permite aplicar reglas de validación basadas en el valor o presencia de ciertas propiedades:

```json
{
  "type": "object",
  "properties": {
    "type": {
      "type": "string"
    },
    "grade": {
      "type": "string"
    },
    "position": {
      "type": "string"
    }
  },
  "if": {
    "properties": {
      "type": {
        "const": "student"
      }
    }
  },
  "then": {
    "required": [
      "grade"
    ]
  },
  "else": {
    "required": [
      "position"
    ]
  }
}
```

> **Ejemplo práctico de esquemas condicionales**:  
> [https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/conditional.json](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/conditional.json)

##### Referencias y reutilización (`$ref`)

La palabra clave `$ref` permite referenciar esquemas definidos internamente o de forma externa:

- **Referencia interna**:
```json
{
  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street": {
          "type": "string"
        },
        "city": {
          "type": "string"
        },
        "zipcode": {
          "type": "string"
        }
      },
      "required": [
        "street",
        "city",
        "zipcode"
      ]
    }
  },
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "address": {
      "$ref": "#/definitions/address"
    }
  },
  "required": [
    "name",
    "address"
  ]
}
```

- **Referencia externa**:
```json
{
  "type": "object",
  "properties": {
    "address": {
      "$ref": "http://api.magicstore.com/schemas/address.json"
    }
  },
  "required": [
    "address"
  ]
}
```

> **Ejemplo completo de conceptos avanzados**:  
> [https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/advanced-concepts.json](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/advanced-concepts.json)

##### JSON Hyper-Schema

JSON Hyper-Schema permite anotar documentos JSON con hipervínculos que describen cómo manipular e interactuar con recursos remotos:

```json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "number"
    }
  },
  "links": [
    {
      "rel": "self",
      "href": "/resource/{id}",
      "method": "GET"
    }
  ]
}
```

Con plantillas dinámicas de URI:

```json
{
  "links": [
    {
      "rel": "next",
      "href": "/resources?cursor={nextCursor}"
    }
  ]
}
```

El atributo `rel` define la relación con el recurso de destino (`self`, `item`, `collection`).

> **Ejemplo de JSON Hyper-Schema**:  
> [https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/json-hyper-schema.json](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/json-hyper-schema.json)

---

### JSON Schema en acción

#### Evolución del esquema

La evolución de esquemas se refiere al proceso de modificar un esquema a lo largo del tiempo para adaptarse a nuevos requisitos:

- **Cambios compatibles hacia atrás (*Backward-compatible*)**: No requieren que los consumidores modifiquen su código existente (por ejemplo, agregar un nuevo campo opcional, expandir valores permitidos o ampliar restricciones como `maxLength`).
- **Cambios incompatibles hacia atrás (*Backward-incompatible*)**: Rompen potencialmente a los consumidores (por ejemplo, eliminar o renombrar campos, cambiar tipos de datos o restringir restricciones como reducir `maxLength` de 50 a 20).

Dado que JSON Schema no proporciona metadatos explícitos para indicar la versión, un enfoque común es versionar los archivos que contienen los modelos de JSON Schema y referenciar estas versiones en los documentos OpenAPI (explorado en profundidad en el Capítulo 13).

#### Integración con los flujos de trabajo de desarrollo

La adopción de un enfoque *schema-first* garantiza que todos los miembros del equipo tengan una comprensión compartida de los datos desde el principio.

##### Automatización de la validación de esquemas en pipelines de CI/CD

Integrar la validación de JSON Schema en pipelines de integración continua garantiza que los cambios cumplan con las estructuras predefinidas antes de ser desplegados.

Ejemplo de flujo de trabajo en GitHub Actions:

```yaml
name: JSON Schema Validation
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]
jobs:
  validate-schemas:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
      # 1. Install JSON Schema validation tool
      - name: Install AJV CLI
        run: npm install -g ajv-cli
      # 2. Validate schema files are correct
      - name: Validate schema syntax
        run: |
          for schema in schemas/*.json; do
            echo "Validating schema: $schema"
            ajv compile -s "$schema"
          done
      # 3. Validate test data against schemas
      - name: Validate sample data
        run: |
          ajv validate -s schemas/user-schema.json -d test-data/valid-user.json
          ajv validate -s schemas/product-schema.json -d test-data/valid-product.json
```

Este pipeline realiza tres pasos esenciales:
1. Instala `ajv-cli` como herramienta de validación rápida y actualizada.
2. Compila y valida la sintaxis de todos los archivos de esquema en `schemas/*.json`.
3. Valida datos de prueba reales frente a los esquemas correspondientes.

---

### Buenas prácticas para el uso de JSON Schema

#### Principios de diseño de esquemas

- **Mantenerlo simple y legible**: Diseña esquemas comprensibles y aplana estructuras donde sea posible en lugar de anidar múltiples niveles de objetos ([Ver ejemplo](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/keep-it-simple-and-readable.json)).
- **Evitar la sobrevalidación (*Over-validation*)**: Permite cierta flexibilidad para cambios futuros utilizando `additionalProperties: true` cuando convenga:
```json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    }
  },
  "additionalProperties": true
}
```
Esto permite cuerpos de datos como:
```json
{
  "id": "456",
  "name": "John",
  "age": 30
}
```
- **Usar descripciones claras**: Proporciona explicaciones significativas con `description`:
```json
{
  "type": "object",
  "properties": {
    "itemName": {
      "type": "string",
      "description": "The unique identifier for a magic item"
    }
  }
}
```
- **Aprovechar la reutilización con `$ref`**:
```json
{
  "$ref": "#/definitions/commonProperties"
}
```
- **Garantizar la compatibilidad hacia atrás**: Añade campos opcionales en lugar de eliminar o alterar tipos existentes.

#### Documentación y comunicación

- Documentar el propósito de cada campo, sus restricciones y comentarios dentro de los archivos ([Ver ejemplo](https://github.com/PacktPublishing/RESTful-Design-Patterns-and-Best-Practices/blob/main/Chapter-11/documentation-and-communication.json)).
- Utilizar JSON Schema dentro de OpenAPI para generar documentación técnica automatizada interactiva.

#### Consideraciones de rendimiento

- **Optimizar la validación**: Cargar y compilar el esquema una sola vez y reutilizarlo en múltiples validaciones.
- **Validar documentos grandes de forma incremental**.
- **Simplificar expresiones regulares (`pattern`)** complejas que puedan degradar el rendimiento.
- **Equilibrar rigor y rendimiento**: Aplicar validaciones estrictas solo a campos críticos de negocio o seguridad:
```json
{
  "type": "object",
  "properties": {
    "email": {
      "type": "string",
      "format": "email",
      "maxLength": 255
    },
    "password": {
      "type": "string",
      "minLength": 8
    }
  },
  "required": [
    "email",
    "password"
  ]
}
```
Y permitir flexibilidad en campos opcionales o secundarios:
```json
{
  "type": "object",
  "properties": {
    "nickname": {
      "type": "string"
    },
    "profilePictureUrl": {
      "type": [
        "string",
        "null"
      ],
      "format": "uri"
    }
  }
}
```
- Usar `anyOf` y `oneOf` con cautela para no perjudicar la complejidad de cálculo:
```json
{
  "anyOf": [
    {
      "$ref": "#/definitions/basicUser"
    },
    {
      "$ref": "#/definitions/adminUser"
    }
  ]
}
```

#### Implicaciones de seguridad

- **Prevenir inyecciones y datos malformados**: Exigir restricciones estrictas en entradas de usuario:
```json
{
  "type": "object",
  "properties": {
    "username": {
      "type": "string",
      "minLength": 3,
      "maxLength": 20,
      "pattern": "^[a-zA-Z0-9_]+$"
    },
    "email": {
      "type": "string",
      "format": "email"
    }
  },
  "required": [
    "username",
    "email"
  ]
}
```
- **Evitar esquemas recursivos sin límite**: Para mitigar ataques de denegación de servicio (DoS), define una profundidad máxima estricta.
- **Usar `additionalProperties: false` para bloquear datos inesperados o maliciosos**.
- **Establecer límites numéricos realistas**:
```json
{
  "type": "object",
  "properties": {
    "age": {
      "type": "integer",
      "minimum": 0,
      "maximum": 150
    }
  }
}
```

---

### Resumen

En este capítulo, hemos explorado el uso de JSON Schema en el diseño de APIs REST, basándonos en la base establecida por la Especificación OpenAPI. Profundizamos en cómo JSON Schema proporciona una forma estructurada de definir, validar y documentar modelos de datos JSON, garantizando la consistencia y la fiabilidad en tus APIs.

Las lecciones clave incluyeron la comprensión de la naturaleza abierta de JSON Schema, su integración con OpenAPI y las mejores prácticas para el diseño de esquemas (mantenerlos simples, evitar la sobrevalidación, optimizar el rendimiento y reforzar la seguridad). El uso de JSON Schema mejora la interoperabilidad entre sistemas, reduce las inconsistencias de datos y respalda la automatización en procesos de desarrollo como la generación de código y las pruebas.

En el próximo capítulo, exploraremos el aprovechamiento de la **hipermedia** en el diseño de APIs, permitiendo a los clientes descubrir y navegar recursos dinámicamente mediante enlaces embebidos.
