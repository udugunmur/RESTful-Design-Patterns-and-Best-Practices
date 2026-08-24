# Parte 1: El Estudio del Aprendiz – Preparándose para el Oficio

## Capítulo 4: Aplicación del Diseño Guiado por el Dominio (DDD) a las APIs

Este capítulo profundiza en cómo incorporar los principios del Diseño Guiado por el Dominio (*Domain-Driven Design* / DDD) en el desarrollo de APIs. Demuestra los beneficios de DDD para el diseño de APIs, ofreciendo una breve descripción general de DDD. Proporciona estrategias para alinear el diseño de APIs con los dominios de negocio, garantizando que las APIs reflejen y satisfagan con precisión las necesidades comerciales y el lenguaje ubicuo (*ubiquitous language*). Este capítulo es esencial para cualquiera que busque crear APIs que no solo sean técnicamente sólidas, sino también relevantes para el negocio.

Al finalizar el capítulo, comprenderás la importancia de alinear el vocabulario de negocio y cómo materializar tus dominios de negocio en tus APIs. También habrás aprendido a evitar las trampas de las APIs REST basadas en CRUD y los antipatrones de diseño de APIs.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **Visión general del diseño guiado por el dominio (*Domain-Driven Design*)**
- **Beneficios del diseño guiado por el dominio**
- **Aplicación del diseño guiado por el dominio en APIs REST**

---

### Visión general del diseño guiado por el dominio (*Domain-Driven Design*)

En esta sección presentaremos los conceptos fundamentales y los beneficios de DDD. DDD es un enfoque para el desarrollo de software que se centra en crear un entendimiento compartido de dominios de negocio complejos mediante la colaboración entre los equipos técnicos y de negocio. Al alinear los modelos de software con las necesidades y el lenguaje del negocio, DDD garantiza que el software refleje con precisión el dominio y respalde eficazmente los objetivos empresariales. Exploremos qué es DDD, por qué es importante y cómo se puede aplicar en el desarrollo de software moderno.

#### ¿Qué es el diseño guiado por el dominio?

DDD es un enfoque de desarrollo de software que enfatiza la colaboración entre los equipos técnicos y de negocio para crear una comprensión compartida del dominio del problema. Se centra en modelar el dominio de acuerdo con las necesidades y el lenguaje del negocio, asegurando que el software se alinee estrechamente con los objetivos y procesos empresariales. DDD fue inventado por **Eric Evans** y presentado en su libro fundamental *Domain-Driven Design: Tackling Complexity in the Heart of Software*, publicado en 2003.

DDD ha ganado popularidad debido a su eficacia para gestionar y abordar las complejidades del desarrollo de software. Al centrarse en el dominio central del negocio y sus complejidades, DDD garantiza que las soluciones de software estén estrechamente alineadas con las necesidades empresariales. Este enfoque es especialmente beneficioso para dominios complejos donde la lógica de negocio es intrincada y requiere una comprensión profunda y un modelado preciso. La naturaleza colaborativa de DDD, que involucra tanto a expertos del dominio (*domain experts*) como a desarrolladores, también asegura que el software se construya con un conocimiento exhaustivo de los procesos y requisitos del negocio, reduciendo malentendidos y mejorando la calidad del producto final.

Además, DDD respalda las prácticas de desarrollo ágil, lo que lo hace idóneo para las metodologías modernas de desarrollo de software. Su énfasis en el desarrollo iterativo, el refinamiento continuo del modelo de dominio y la descomposición de problemas complejos en subdominios y contextos delimitados (*bounded contexts*) manejables se alinea perfectamente con los principios ágiles. Esta compatibilidad con las metodologías ágiles ayuda a las organizaciones a adaptarse rápidamente a los cambios, mejorar sus procesos de desarrollo y entregar software de alta calidad de manera oportuna. Empresas como **Amazon**, **Netflix** y **LinkedIn** han implementado con éxito DDD para gestionar sus complejos sistemas, demostrando su valor práctico y eficacia en aplicaciones del mundo real.

#### ¿Por qué es importante el diseño guiado por el dominio?

DDD desempeña un papel crucial al cerrar la brecha entre los equipos técnicos y de negocio. Garantiza que los esfuerzos de desarrollo de software estén estrechamente alineados con los objetivos de negocio y las necesidades de los usuarios. Esta sección profundizará en las razones por las cuales DDD es esencial en el desarrollo de software moderno, destacando su impacto en la comunicación, la escalabilidad y la mantenibilidad a largo plazo.

##### Cerrar la brecha de comunicación

DDD aborda la brecha de comunicación entre los equipos técnicos y de negocio definiendo un **lenguaje ubicuo (*ubiquitous language*)**. Este lenguaje compartido facilita una comunicación clara y eficaz, asegurando que ambas partes se entiendan y puedan colaborar más eficientemente. Esta alineación ayuda a construir software que realmente satisfaga los requisitos de negocio.

##### Habilitar microservicios y escalabilidad organizacional

Muchas empresas utilizan DDD como motor e impulsor para migrar desde arquitecturas monolíticas hacia microservicios. Al descomponer el monolito en servicios más pequeños y manejables, las organizaciones pueden resolver problemas de escalabilidad y mejorar su agilidad. DDD proporciona las herramientas y metodologías para identificar y definir estos servicios más pequeños dentro del contexto del dominio general del negocio.

##### Reducir la deuda técnica

Si bien las actividades de diseño en DDD ciertamente requieren tiempo y esfuerzo, dan sus frutos al hacer que el software sea más fácil de hacer evolucionar en el futuro. Descuidar el diseño puede ahorrar tiempo a corto plazo, pero a menudo conduce a la acumulación de deuda técnica, lo que ralentiza la productividad más adelante. Invertir en el diseño de tu software mejora la resistencia (*stamina*) del proyecto, lo que permite una velocidad de desarrollo sostenida a largo plazo.

Esta compensación del diseño es bien conocida como la **hipótesis de la resistencia del diseño (*design stamina hypothesis*)**, visible en el siguiente pseudográfico:

*Figura 4.1: Hipótesis de la resistencia del diseño por Martin Fowler*

> **Consejo rápido**: ¿Necesitas ver una versión de alta resolución de esta imagen? Abre este libro en el lector Packt Reader de última generación o consúltalo en la copia en PDF/ePub.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

##### Mejorar la mantenibilidad

DDD mejora la mantenibilidad del software al proporcionar una estructura clara y una separación de responsabilidades. Al modelar el dominio con precisión y dividirlo en componentes bien definidos, el software se vuelve más fácil de entender, modificar y extender. Esta mantenibilidad es crucial para el éxito y la adaptabilidad del proyecto a largo plazo.

Ahora que hemos analizado la importancia de la mantenibilidad, profundicemos en los bloques de construcción fundamentales de DDD.

#### Bloques de construcción del diseño guiado por el dominio

DDD consta de varios bloques de construcción fundamentales que ayudan a estructurar y organizar el modelo de dominio. Estos bloques aseguran que el sistema sea modular, mantenible y esté alineado con los requisitos de negocio. Exploremos cada uno de ellos en detalle.

##### Dominio (*Domain*)

Un dominio es un área amplia y de alto nivel de conocimiento o actividad dentro de la cual opera un sistema de software. Abarca el espacio general del negocio o del problema que el sistema pretende abordar. Es donde se implementan las funcionalidades centrales del negocio y generalmente se divide en subdominios más pequeños para gestionar la complejidad. Un dominio también se denomina espacio del problema (*problem space*) o esfera de conocimiento.

En una aplicación bancaria, el dominio sería toda la industria bancaria, cubriendo aspectos como la gestión de cuentas, transacciones, préstamos, relaciones con clientes y cumplimiento normativo.

##### Subdominio (*Subdomain*)

Un subdominio es un área más enfocada y específica dentro del dominio mayor. Representa un segmento o aspecto particular del dominio general, correspondiendo a menudo a un conjunto diferenciado de procesos o funciones de negocio. Además, representa los bloques de construcción de un dominio, cada uno abordando un aspecto particular del negocio. Los subdominios permiten descomponer el dominio global en partes más manejables y comprensibles.

Podemos diferenciar tres tipos de subdominios:

- **Subdominios centrales (*Core subdomains*)**: Son las partes más críticas del dominio, las que proporcionan una ventaja competitiva o diferencian al negocio. A menudo requieren la mayor atención y personalización. Con frecuencia, estos subdominios no se externalizan (*outsourcing*) a terceros. Para una aplicación bancaria, el procesamiento de transacciones, la gestión de préstamos y la gestión de cuentas podrían ser subdominios centrales.
- **Subdominios de soporte (*Supporting subdomains*)**: Respaldan a los subdominios centrales, pero no son el eje de la ventaja competitiva del negocio. Pueden incluir funcionalidades genéricas o menos críticas. Por ejemplo, el cumplimiento normativo e informes, la gestión de relaciones con clientes (CRM) y la gestión documental pueden ser subdominios de soporte para la aplicación bancaria.
- **Subdominios genéricos (*Generic subdomains*)**: Son comunes a muchas empresas y no proporcionan ninguna ventaja competitiva. A menudo se pueden resolver con soluciones estándar del mercado (*off-the-shelf*). Para nuestra aplicación bancaria, estos podrían ser la autenticación y autorización, el sistema de notificaciones y la gestión de contenidos.

*Figura 4.2: Dominios y subdominios bancarios*

Definir todos tus subdominios de una vez es una tarea difícil. Mediante el uso de un proceso iterativo, puedes lograr una representación realista de tu espacio del problema. Además, este enfoque puede revelar que algunos subdominios todavía son demasiado grandes y requieren una mayor descomposición para alcanzar un tamaño manejable.

##### Contextos delimitados (*Bounded contexts*)

Un **contexto delimitado (*bounded context*)** es un patrón central en DDD que ayuda a gestionar la complejidad en grandes sistemas de software al definir claramente los límites dentro de los cuales un modelo de dominio particular está definido y es aplicable. Cada contexto delimitado tiene sus propios modelos diferenciados y es responsable de una parte específica de la lógica de negocio.

Desglosemos los conceptos clave de los contextos delimitados:

- **Contexto (*Context*)**: Es el entorno en el que aparece una palabra o declaración que determina su significado. En DDD, el contexto se refiere al ámbito en el que se define y utiliza un modelo específico.
- **Delimitado (*Bounded*)**: Son los límites definidos que restringen el alcance del contexto. Estos límites se definen explícitamente para garantizar la claridad y la separación.

Cada contexto delimitado debe proporcionar:

- **Límites claros**: Cada contexto delimitado tiene límites bien definidos que no se superponen con otros contextos. Esto asegura que el lenguaje y las reglas dentro de un contexto no se confundan con los de otro.
- **Lenguaje unificado**: Dentro de un contexto delimitado, se utiliza un lenguaje ubicuo de manera consistente. Este lenguaje es compartido entre desarrolladores y expertos del dominio para asegurar una comunicación clara.
- **Modelos independientes**: Cada contexto delimitado contiene su propio modelo que está aislado de los modelos en otros contextos. Los cambios en un contexto no afectan directamente a otro contexto.

En nuestro ejemplo de aplicación bancaria, podemos reconocer dos contextos delimitados:

*Figura 4.3: Contextos delimitados de transacciones y préstamos*

Diferentes contextos delimitados pueden tener modelos similares, pero estos modelos cumplen propósitos diferentes según el contexto al que pertenezcan. Por ejemplo, un modelo de *Cliente* (*Customer*) en un contexto de transacciones podría centrarse en atributos y métodos relacionados con la gestión de cuentas y el historial de transacciones. Mientras tanto, en el contexto de préstamos, el modelo de *Cliente* podría centrarse en atributos y métodos relacionados con solicitudes de préstamo e historial de amortizaciones.

A veces, un contexto delimitado puede abarcar múltiples subdominios cuando el equipo que trabaja dentro de ese contexto comparte una comprensión cohesionada de los conceptos a través de esos subdominios. Esta comprensión compartida garantiza la coherencia en cómo se aplican los modelos y el lenguaje, incluso cuando el contexto cubre un área más amplia del negocio. Dicho enfoque funciona bien cuando los equipos están alineados y colaboran eficazmente dentro de un límite definido.

En grandes organizaciones, es más común que cada contexto delimitado se alinee con un único subdominio. Esto se debe a que los equipos en estas empresas suelen ser especializados y enfocados, siendo dueños de sus modelos, datos y lenguaje sin una superposición significativa con otros equipos. La integración entre contextos delimitados se gestiona mediante estrategias deliberadas, asegurando que los equipos puedan trabajar de forma independiente manteniendo la coherencia general del sistema.

Las empresas más pequeñas, por otro lado, suelen tener equipos que manejan múltiples responsabilidades, lo que lleva a un único contexto delimitado que abarca varios subdominios. Estos equipos suelen tener una comprensión más amplia del negocio, lo que les permite gestionar áreas superpuestas de manera eficaz. Sin embargo, este enfoque requiere una gestión cuidadosa de los límites para evitar confusiones y mantener un enfoque claro en los objetivos de cada subdominio.

En el siguiente diagrama, el dominio abarca múltiples subdominios, cada uno albergando su propio conjunto de contextos delimitados. Esta estructura en capas muestra cómo DDD descompone la complejidad en partes manejables, promoviendo la escalabilidad, la mantenibilidad y la comunicación clara entre los equipos técnicos y de negocio.

*Figura 4.4: Dominios, subdominios y contextos delimitados*

##### Lenguaje ubicuo (*Ubiquitous language*)

El lenguaje ubicuo es un concepto crítico en DDD cuyo objetivo es crear un lenguaje común y compartido entre los desarrolladores de software y los expertos del dominio. Este lenguaje se utiliza de manera consistente en todo el proyecto para garantizar una comunicación clara y la comprensión mutua del dominio.

Un lenguaje ubicuo exitoso debe proporcionar tres características clave:

- **Terminología común**: El lenguaje se desarrolla colaborativamente entre expertos del dominio y desarrolladores, asegurando que los términos sean comprendidos por ambas partes.
- **Consistencia**: Se utilizan los mismos términos en todo el proyecto, incluidos el código, la documentación y las discusiones, para evitar ambigüedades.
- **Específico del dominio**: El lenguaje se adapta al dominio específico o contexto delimitado, capturando sus conceptos, procesos y reglas únicos.

El lenguaje ubicuo se puede implementar siguiendo estos pasos:

1. **Definición**: Los expertos del dominio trabajan junto con los desarrolladores para definir y refinar el lenguaje. Esto puede implicar reuniones periódicas, debates y retroalimentación asíncrona.
2. **Documentación**: El lenguaje se documenta de forma accesible para todos los miembros del equipo, incluyendo a menudo glosarios, diagramas conceptuales y ejemplos de uso. Además, el uso de documentación versionada hará que tu lenguaje ubicuo sea más flexible ante cambios futuros.
3. **Implementación técnica**: Los términos del lenguaje ubicuo se utilizan directamente en el código y en la API. Esto hace que tu implementación sea más legible y esté alineada con el dominio de negocio.

Ilustremos la fase de definición y documentación del lenguaje ubicuo con una aplicación bancaria centrada en el contexto delimitado de gestión de cuentas.

**Terminología de negocio:**
- **Cuenta (*Account*)**: Cuenta de un cliente con el banco
- **Cliente (*Customer*)**: Persona física o jurídica titular de una cuenta
- **Depósito (*Deposit*)**: Añadir dinero a una cuenta
- **Retirada (*Withdrawal*)**: Sacar dinero de una cuenta
- **Saldo (*Balance*)**: Cantidad de dinero actualmente en una cuenta

**Lenguaje ubicuo en uso:**
- **Definición**:
  - *Experto del dominio*: «Cuando un cliente realiza un depósito, actualizamos el saldo de la cuenta».
  - *Desarrollador*: «Entonces, necesitamos un *endpoint* de API `Deposit` que modifique el saldo de un objeto `Account`».
- **Documentación**:
  - **Glosario**:
    - `Account`: Representa la cuenta bancaria de un cliente
    - `Customer`: Entidad que representa a una persona física o jurídica titular de una cuenta
    - `Deposit`: Transacción que añade fondos a una cuenta
    - `Withdrawal`: Transacción que retira fondos de una cuenta
    - `Balance`: Cantidad actual de dinero en una cuenta

La documentación puede incluir cualquier diagrama relevante que ayude a los usuarios a comprender profundamente los diferentes términos utilizados.

##### Entidades (*Entities*)

Una **entidad** es un objeto que se define no solo por sus atributos, sino también por una **identidad distintiva** que perdura a través del tiempo y en diferentes estados. Las entidades tienen un identificador único y un ciclo de vida, y su identidad permanece constante incluso si otros atributos cambian.

Cada entidad tiene un identificador distinto que la diferencia de otras entidades. Este identificador suele ser inmutable; las entidades tienen un ciclo de vida que incluye creación, modificación y eliminación. Además, encapsulan tanto datos como comportamiento.

Como ejemplo, consideremos la entidad de transacción en el contexto delimitado de transacciones:

- **Atributos**: `transactionId`, `accountId`, `transactionType`, `amount`, `transactionDate`, `status`, `description` y `currency`
- **Identidad única**: `transactionId`
- **Ciclo de vida**: Se crea una transacción cuando ocurre una operación de cuenta y puede cambiar de estado durante el procesamiento (por ejemplo, pendiente, completada o revertida)
- **Comportamiento**: `process()`, `validate()`, `rollback()` y `generateReceipt()`

##### Objetos de valor (*Value objects*)

Los **objetos de valor (*value objects*)** son otro bloque de construcción esencial. A diferencia de las entidades, los objetos de valor no tienen una identidad única. En su lugar, se definen por sus atributos y son inmutables. Los objetos de valor se utilizan para representar un aspecto descriptivo del dominio sin identidad conceptual, lo que significa que dos objetos de valor con los mismos atributos se consideran iguales.

Los objetos de valor se identifican únicamente por sus atributos. Una vez creado, un objeto de valor no se puede modificar; si se necesita un cambio, se debe crear una nueva instancia. Dos objetos de valor con los mismos valores para sus atributos se consideran iguales. Por último, los objetos de valor pueden garantizar su propia validez y coherencia.

Para ilustrar los objetos de valor, consideremos el objeto de valor `Money` en el contexto de préstamos:

- **Atributos**: `amount` y `currency`
- **Comportamiento**: `add(Money)`, `subtract(Money)`, `multiply(factor)` y `equals(Money)`

##### Agregados (*Aggregates*)

Los **agregados** son una agrupación de objetos de dominio que se pueden tratar como una sola unidad. Un agregado consta de una o más entidades y objetos de valor que están estrechamente relacionados. Garantiza la coherencia dentro de sus límites imponiendo invariantes y reglas de negocio. Los agregados ayudan a gestionar y encapsular la complejidad dentro de un contexto delimitado.

Los agregados tienen las siguientes características:

- **Entidad raíz (*Aggregate root*)**: Cada agregado tiene una entidad raíz, llamada raíz del agregado, que es el único punto de entrada para interactuar con el agregado.
- **Límite de consistencia**: Los agregados definen un límite de consistencia. Los cambios dentro de un agregado son consistentes y transaccionales.
- **Encapsulación**: Los agregados encapsulan entidades internas y objetos de valor, proporcionando una interfaz clara a través de la raíz del agregado.
- **Gestión de transacciones**: Los agregados gestionan su propia coherencia transaccional, garantizando que los cambios sean coherentes y válidos.

Por ejemplo, en el contexto de préstamos, el agregado `LoanApplication` consta de una solicitud de préstamo y entidades relacionadas. La entidad `LoanApplication` es la raíz del agregado:

- **LoanApplication (raíz del agregado)**:
  - **Atributos**: `applicationId`, `customerId`, `loanType`, `requestedAmount`, `applicationDate` y `status`
  - **Métodos**: `submitApplication()`, `approveApplication()` y `rejectApplication()`
- **LoanTerms (objeto de valor)**:
  - **Atributos**: `principalAmount`, `interestRate`, `termLength` y `startDate`
  - **Métodos**: `calculateTotalRepayment()` y `equals(LoanTerms)`

##### Repositorios (*Repositories*)

Los repositorios actúan como un puente entre la lógica de negocio y el almacenamiento de datos. Ayudan a mantener nuestro código organizado y facilitan la gestión de cómo guardamos y recuperamos datos. Los repositorios proporcionan una forma limpia y sencilla de interactuar con la base de datos, de modo que el resto de nuestro código no necesite preocuparse por los detalles de cómo se almacenan los datos.

A continuación se presentan algunos puntos clave sobre los repositorios:

- **Acceso simplificado**: Los repositorios facilitan la obtención y el almacenamiento de datos sin necesidad de conocer los detalles de la base de datos.
- **Comportamiento similar a colecciones**: Actúan como una colección de objetos de dominio, lo que nos permite agregar, eliminar y buscar dichos objetos.
- **Enfoque en la lógica de negocio**: Al utilizar repositorios, nuestra lógica de negocio puede mantenerse limpia y enfocada, sin verse sobrecargada por código de acceso a datos.
- **Garantizar la coherencia**: Los repositorios aseguran que los datos con los que trabajamos sean consistentes y válidos.

Por ejemplo, en el contexto de transacciones, `AccountRepository` nos ayuda a gestionar cuentas bancarias. Nos permite buscar cuentas por su ID, guardar nuevas cuentas, eliminar cuentas y encontrar todas las cuentas pertenecientes a un cliente:

```python
class AccountRepository:
    def __init__(self):
        self.accounts = {}

    def find_by_id(self, account_id):
        return self.accounts.get(account_id)

    def save(self, account):
        self.accounts[account.account_id] = account

    def delete(self, account_id):
        if account_id in self.accounts:
            del self.accounts[account_id]

    def findBycustomerId(self, customer_id):
        return [
            account
            for account in self.accounts.values()
            if account.customer_id == customer_id
        ]
```

> **Consejo rápido**: Mejora tu experiencia de programación con las funciones AI Code Explainer y Quick Copy. Abre este libro en el lector Packt Reader de última generación. Haz clic en el botón Copiar (1) para copiar rápidamente el código en tu entorno de desarrollo, o haz clic en el botón Explicar (2) para que el asistente de IA te explique un bloque de código.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

Con una sólida comprensión de DDD y sus conceptos centrales —tales como dominios, subdominios, contextos delimitados y lenguaje ubicuo— podemos comenzar a ver cómo se aplican estos principios a los desafíos de desarrollo del mundo real. Pero, ¿por qué deberían los diseñadores de APIs preocuparse por DDD? ¿Qué ventajas únicas aporta al diseño de APIs?

---

### ¿Cómo puede beneficiar el diseño guiado por el dominio a las APIs?

En el panorama tecnológico actual en rápida evolución, diseñar APIs que sean tanto efectivas como fáciles de usar es primordial. DDD ofrece un enfoque estratégico para el desarrollo de APIs que se alinea estrechamente con los objetivos de negocio y las necesidades de los usuarios. Al centrarse en el dominio central del negocio y las relaciones dentro de él, DDD garantiza que las APIs sean intuitivas, mantenibles y capaces de respaldar flujos de trabajo empresariales complejos.

En esta sección, exploraremos los numerosos beneficios de aplicar los principios de DDD al diseño de APIs. Analizaremos cómo DDD permite la creación de APIs basadas en la experiencia (*experience-based APIs*), ayuda a evitar la complejidad accidental y mejora la seguridad de las APIs. A través de ejemplos prácticos y explicaciones detalladas, ilustraremos cómo DDD puede transformar tu proceso de desarrollo de APIs y, en última instancia, ofrecer un mejor valor a tus usuarios.

#### Habilitación de APIs basadas en la experiencia (*Experience-based APIs*)

DDD potencia tanto las **APIs de dominio (*domain APIs*)** como las **APIs basadas en la experiencia (*experience-based APIs*)**, cada una cumpliendo propósitos distintos pero complementarios:

- **APIs de dominio (*Domain APIs*)**: Como una *Inventory API* utilizada por proveedores externos, reflejan directamente las entidades y operaciones centrales del negocio, beneficiándose de los contextos delimitados y del lenguaje ubicuo de DDD para crear interfaces claras y bien estructuradas.
- **APIs basadas en la experiencia (*Experience-based APIs*)**: Como una *Checkout API* en una plataforma de comercio electrónico, aprovechan el enfoque de DDD en los procesos de negocio para orquestar flujos de trabajo de usuario complejos en lugar de exponer operaciones de datos puras.

La fortaleza de DDD radica en su capacidad para respaldar y conectar ambos enfoques: ayuda a mantener la integridad de tu modelo de dominio al tiempo que posibilita experiencias de usuario intuitivas. Por ejemplo, una plataforma de comercio electrónico podría exponer tanto APIs de dominio para la gestión de inventario como APIs basadas en la experiencia que guíen a los usuarios a través del proceso de compra, con DDD garantizando límites claros y relaciones bien definidas entre ellas.

*Figura 4.5: APIs basadas en la experiencia y APIs de dominio*

A pesar de las restricciones de las APIs REST, tales como URLs, *endpoints* y verbos HTTP, pensar en términos de DDD ofrece estrategias para definir flujos de trabajo y procesos de manera efectiva. Los recursos REST no necesitan limitarse a entidades del dominio; pueden representar flujos de trabajo de negocio, permitiendo una experiencia enriquecida y fluida para tus clientes. Además, habilitas una experiencia multicanal uniforme por diseño, lo que significa que tus clientes disfrutarán de una interacción coherente con la API a través de diversas plataformas y dispositivos.

DDD fomenta una definición reflexiva de los límites de la API, dando como resultado APIs con propósitos claros. Los límites bien diseñados mejoran el descubrimiento y la documentación de las APIs, facilitando a los desarrolladores su comprensión y uso efectivo. Al integrar el lenguaje de negocio en las APIs, DDD garantiza que la funcionalidad de la API se alinee con los objetivos empresariales, mejorando la usabilidad y la flexibilidad. Esta capa de abstracción evita cambios disruptivos cuando los modelos de dominio internos evolucionan.

Además de habilitar APIs basadas en la experiencia, DDD te protege de la **complejidad accidental**.

#### Evitar la complejidad accidental

La complejidad accidental proviene de decisiones de diseño e implementación que añaden complicaciones innecesarias, en lugar de provenir de la dificultad intrínseca del problema en sí. Esto suele ocurrir debido a malas elecciones de diseño, sobreingeniería o al uso indebido de la tecnología.

Las APIs diseñadas como simples operaciones **CRUD** (*Create, Read, Update, Delete*) a menudo reflejan modelos y esquemas internos de bases de datos, lo que obliga a los usuarios a leer documentación extensa y realizar múltiples llamadas a la API para completar una sola tarea. Esto incrementa la curva de aprendizaje y dificulta el uso y mantenimiento de la API. Además, diferentes partes de la API pueden utilizar un vocabulario de negocio inconsistente, lo que genera confusión y errores.

DDD mitiga la complejidad accidental centrándose en el dominio de negocio y reduciendo los detalles de bajo nivel. Los desarrolladores interactúan con conceptos y flujos de trabajo de alto nivel, sin necesidad de un conocimiento profundo de los dominios internos. Esta simplificación hace que la API sea más intuitiva y fácil de mantener.

#### Mejorar la seguridad de la API

La aplicación de los principios de DDD puede mejorar la seguridad de las APIs al promover una estructura de API clara, cohesiva y bien definida. Este enfoque mitiga varias vulnerabilidades señaladas en el **OWASP API Security Top 10**:

- **Autorización de nivel de objeto rota (*Broken Object-Level Authorization* / BOLA)**: Al definir límites y responsabilidades claras en el dominio, DDD garantiza que el acceso a los objetos se controle a través de servicios y repositorios bien definidos. Cada entidad de dominio aplica su propio control de acceso, reduciendo el riesgo de accesos no autorizados.
- **Autenticación rota (*Broken authentication*)**: DDD aboga por un dominio independiente de gestión de identidades y accesos (IAM). La implementación de mecanismos de autenticación robustos como OAuth y JWT dentro de este dominio garantiza un tratamiento consistente y seguro de las credenciales de usuario en toda la aplicación.
- **Autorización de nivel de propiedad de objeto rota (*Broken object property-level authorization*)**: DDD promueve la encapsulación y los límites de contexto, lo que limita la exposición de datos. Las APIs diseñadas con principios de DDD devuelven solo la información necesaria, minimizando la exposición de datos sensibles. Los agregados y objetos de valor encapsulan los estados internos, evitando su manipulación directa.
- **Acceso no restringido a flujos de negocio sensibles (*Unrestricted access to sensitive business flows*)**: DDD ayuda a gestionar riesgos enfatizando una comprensión profunda del dominio de negocio e implementando controles robustos y específicos según el contexto.

> **Más información**  
> OWASP significa *Open Web Application Security Project*. Es una fundación sin ánimo de lucro que trabaja para mejorar la seguridad del software. OWASP proporciona una gran cantidad de recursos, herramientas y directrices gratuitos y abiertos para organizaciones, desarrolladores y profesionales de seguridad para ayudarles a proteger las aplicaciones web y el desarrollo de software. Para obtener más información, visita [https://owasp.org/www-project-api-security/](https://owasp.org/www-project-api-security/).

Como ejemplo, imagina una empresa de tecnología que lanza un producto de alta demanda, como una consola de videojuegos: esta empresa puede prevenir abusos definiendo un contexto delimitado para el flujo de compra. Los agregados aplican límites a las cantidades de compra y las políticas de dominio restringen la cantidad de artículos que un usuario puede comprar dentro de un marco de tiempo. Monitorizar y ajustar las políticas en función de eventos del dominio ayuda a detectar y responder a actividades inusuales. Al aprovechar DDD, esta empresa puede beneficiarse de:

- **Diseño colaborativo de APIs**: Involucrar a expertos del dominio para modelar los procesos de negocio con precisión, equilibrando funcionalidad y seguridad.
- **Contextos delimitados y agregados**: Definir contextos delimitados para flujos sensibles, aplicando reglas y restricciones de negocio.
- **Políticas de dominio e invariantes**: Implementar reglas que limiten las compras de artículos de alta demanda, encapsuladas dentro de la capa de dominio.
- **Monitorizar y ajustar**: Monitorizar continuamente los *endpoints* sensibles, utilizando eventos del dominio para detectar anomalías y ajustar políticas.

Ahora que hemos cubierto los beneficios de DDD, es momento de explorar cómo se pueden aplicar estos principios a las APIs REST. La siguiente sección te guiará a través del proceso de integración de DDD con servicios RESTful, centrándose en cómo diseñar APIs que sean tanto centradas en el usuario como alineadas con los objetivos de negocio. Analizaremos estrategias para definir límites de API, crear *endpoints* significativos y garantizar que tus APIs sean mantenibles y escalables. Sumerjámonos en la aplicación práctica de DDD en el ámbito de las APIs REST.

---

### Aplicación del diseño guiado por el dominio a las APIs REST

Aplicar DDD a las APIs REST garantiza que las APIs estén estrechamente alineadas con los objetivos y procesos de negocio. Esta alineación ayuda a crear APIs intuitivas, mantenibles y escalables.

Si bien DDD es un enfoque integral que se aplica a varias capas del desarrollo de software, esta sección se centra únicamente en cómo sus principios pueden dar forma al diseño de APIs. El objetivo es mostrar cómo conceptos como el lenguaje ubicuo, los contextos delimitados y los flujos de trabajo basados en la experiencia pueden guiar el diseño de APIs, sin profundizar en los detalles de la implementación completa de DDD en la aplicación subyacente o base de código. Al acotar el enfoque, pretendemos proporcionar directrices prácticas y accionables para diseñadores y desarrolladores de APIs que desean alinear sus interfaces con los objetivos de negocio.

En esta sección, exploraremos varios aspectos clave de la integración de DDD con servicios RESTful, incluida la alineación de las APIs con el lenguaje ubicuo, la definición de contextos delimitados para APIs, el diseño de APIs basadas en la experiencia y cómo hacer que tu API sea descubrible.

#### Alinear las APIs con el lenguaje ubicuo

Alinear tus APIs con el lenguaje ubicuo de tu dominio garantiza consistencia, claridad y una comprensión compartida tanto en los equipos técnicos como en los de negocio.

Consideremos un ejemplo concreto en el contexto de un dominio bancario. Supongamos que el dominio de negocio incluye conceptos como `Account`, `Transaction` y `Loan`, con acciones específicas como `OpenAccount`, `DepositMoney` y `ApplyForLoan`.

A continuación se presentan los conceptos incluidos en el dominio de negocio:

- **Account**: Representa la cuenta bancaria de un cliente
- **Transaction**: Representa una transacción financiera
- **Loan**: Representa un proceso de solicitud y gestión de préstamos

La Tabla 4.1 describe los *endpoints* de API, acciones y operaciones correspondientes a estos tres conceptos:

| Término de negocio | Endpoints de API | Acciones | Operación de API |
| :--- | :--- | :--- | :--- |
| **Account** | `/accounts` | `OpenAccount` | `POST /accounts` |
| **Transaction** | `/transactions`<br>`/accounts/{accountId}/transactions` | `DepositMoney` | `POST /accounts/{accountId}/transactions/deposit` |
| **Loan** | `/loan`<br>`/loan/{loanId}` | `ApplyForLoan`<br>`ApproveLoan`<br>`RejectLoan` | `POST /loan`<br>`POST /loan/{loanId}/approve`<br>`POST /loan/{loanId}/reject` |

*Tabla 4.1: Ejemplo de terminología de negocio en una API*

#### Definición de contextos delimitados para APIs

Definir contextos delimitados en tus APIs es crucial para mantener una estructura de API limpia y organizada, lo que repercute significativamente en la experiencia del desarrollador. Los contextos delimitados garantizan que cada parte de la API tenga una responsabilidad clara y se alinee con una parte específica del dominio. Esta separación reduce la complejidad, evita colisiones de nombres y facilita la navegación por la API. Por ejemplo, tener contextos separados para operaciones de transacciones y préstamos en una API bancaria garantiza que cada conjunto de *endpoints* sea enfocado y relevante.

Al implementar contextos delimitados en tus APIs, te beneficias de:

- **Separación clara de responsabilidades**: Los contextos delimitados ayudan a separar diferentes áreas del dominio de negocio, asegurando que cada contexto tenga sus propias responsabilidades bien definidas.
- **Mayor escalabilidad y mantenibilidad**: Al aislar cada contexto, los cambios en un contexto no afectan a otros, lo que hace que el sistema sea más fácil de mantener y escalar.
- **Experiencia de desarrollador mejorada**: Los desarrolladores pueden trabajar en contextos específicos sin necesidad de comprender todo el sistema, lo que se traduce en un desarrollo más rápido y menos errores.
- **Flexibilidad**: Los contextos delimitados proporcionan una forma estructurada de gestionar la complejidad al dividir un sistema grande en partes más pequeñas y manejables. Esta separación ayuda a diseñar APIs que son a la vez flexibles y mantenibles, adaptándose a una amplia gama de casos de uso y escenarios de integración.

Los contextos delimitados se pueden reflejar en tu API en dos lugares:

1. **Tus endpoints de API**: Por ejemplo, en el dominio bancario, podrías definir `/accounts`, `/transactions` y `/loans` como contextos delimitados independientes. Cada contexto gestionaría sus operaciones específicas, tales como `/accounts/{accountId}`, `/transactions/{transactionId}` y `/loans/{loanId}`, garantizando una separación y enfoque claros.
2. **Tu documentación de API**: Mantén paquetes de API como producto independientes para cada contexto delimitado para evitar confusiones y facilitar la navegación. La documentación de Stripe es un excelente ejemplo de ello.

Ahora que hemos definido contextos delimitados para tus APIs, exploremos cómo diseñar APIs basadas en la experiencia.

#### Diseño de APIs basadas en la experiencia (*Experience-based APIs*)

Como se mencionó en la primera sección, pensar en términos de DDD te ayuda a pensar en las experiencias y flujos de trabajo del usuario en lugar de limitarse puramente a entidades de datos.

Como ejemplo, considera un proceso de compra (*checkout*) de comercio electrónico. En lugar de realizar múltiples llamadas a la API para agregar artículos a un carrito, calcular el envío, aplicar descuentos y procesar pagos, una única **Checkout API** optimiza la experiencia del usuario, integrando todos los pasos necesarios en un flujo de trabajo coherente.

Sin una API basada en la experiencia, tendrías la siguiente especificación OpenAPI:

```yaml
openapi: 3.0.0
info:
  title: Checkout API
  version: 1.0.0
paths:
  /cart/add:
    post:
      summary: Add item to cart
      ...
  /shipping/cost:
    post:
      summary: Get shipping cost
      ...
  /discount/apply:
    post:
      summary: Apply discount code
      ...
  /payment/process:
    post:
      summary: Process payment
      ...
```

Los clientes de tu API tendrían que realizar al menos cuatro llamadas a la API para completar un proceso de compra:

- **Primera llamada a la API**:
```http
POST /cart/add
Content-Type: application/json

{
  "items": [
    {
      "itemId": "123",
      "quantity": 2
    }
  ]
}
```

- **Segunda llamada a la API**:
```http
POST /shipping/cost
Content-Type: application/json

{
  "cartId": "452",
  "address": {
    "street": "39 Rue de la paix",
    "city": "Paris",
    "zip": "75006"
  }
}
```

- **Tercera llamada a la API**:
```http
POST /discount/apply
Content-Type: application/json

{
  "cartId": "452",
  "discountCode": "SAVE20"
}
```

- **Cuarta llamada a la API**:
```http
POST /payment/process
Content-Type: application/json

{
  "cartId": "452",
  "paymentType": "Card",
  "paymentDetails": {
    "cardNumber": "232132132423423432423",
    "expirationDate": "02/29",
    "cvv": "123"
  }
}
```

Si aprovechas DDD y las APIs basadas en la experiencia, puedes combinar todos los pasos en una sola llamada, simplificando la implementación del cliente y encapsulando todo el proceso de pago en una sola transacción, haciéndolo más robusto y fácil de mantener:

```yaml
openapi: 3.0.0
info:
  title: Checkout API
  version: 2.0.0
paths:
  /checkout:
    post:
      summary: Complete checkout process
      requestBody:
        ...
```

La llamada requerida a la API será la siguiente:

```http
POST /checkout
Content-Type: application/json

{
  "items": [
    {
      "itemId": "123",
      "quantity": 2
    }
  ],
  "address": {
    "street": "39 Rue de la paix",
    "city": "Paris",
    "zip": "75006"
  },
  "discountCode": "SAVE30",
  "paymentDetails": {
    "cardNumber": "232132132423423432423",
    "expirationDate": "02/29",
    "cvv": "123"
  }
}
```

#### Hacer que tu API sea descubrible

La hipermedia y las APIs basadas en la experiencia son dos enfoques poderosos para diseñar APIs flexibles, intuitivas y fáciles de usar. Mientras que las APIs basadas en la experiencia se centran en adaptar la API a experiencias de usuario específicas, la **hipermedia** (a menudo denominada **HATEOAS**, que significa *Hypermedia as the Engine of Application State*) enfatiza el descubrimiento dinámico de acciones del dominio a través de enlaces y controles incrustados dentro de las respuestas de la API. Ambos enfoques pueden mejorar significativamente el diseño de APIs cuando se combinan.

Roy Fielding enfatiza que HATEOAS permite a los clientes navegar e interactuar dinámicamente con la aplicación, mejorando la flexibilidad y la capacidad de evolución:

> «La característica central que distingue el estilo arquitectónico REST de otros estilos basados en red es su énfasis en una interfaz uniforme entre componentes, lo que simplifica y desacopla la arquitectura, permitiendo que cada parte evolucione de forma independiente».  
> — *Roy Fielding (2000)*

En el Capítulo 6, discutiremos en detalle cómo hacer que tu API sea descubrible utilizando los modelos de madurez de APIs de Amundsen y Richardson.

---

### Resumen

En este capítulo, has aprendido los fundamentos y conocimientos profundos sobre cómo aplicar DDD al diseño de APIs. Este capítulo comenzó con una descripción general de DDD, destacando su importancia para alinear el desarrollo de software con los objetivos de negocio a través de la colaboración entre equipos técnicos y de negocio. Exploramos los beneficios de incorporar los principios de DDD en las APIs, enfatizando cómo este enfoque puede crear APIs basadas en la experiencia que mejoran los flujos de trabajo de los usuarios y mantienen un lenguaje de negocio consistente a través de múltiples plataformas.

Luego profundizamos en los conceptos clave de DDD, como dominios, subdominios, contextos delimitados y lenguaje ubicuo. Estos bloques de construcción son cruciales para estructurar y organizar tu modelo de dominio, asegurando que el sistema sea modular, mantenible y esté alineado con los requisitos de negocio. Al utilizar un lenguaje compartido y límites claramente definidos, DDD facilita una mejor comunicación y comprensión entre desarrolladores y expertos del dominio, lo que finalmente conduce a soluciones de software más efectivas.

El capítulo también cubrió la aplicación práctica de DDD a las APIs REST, ilustrando cómo alinear las APIs con el lenguaje ubicuo del dominio. Al hacerlo, aseguramos la consistencia y la claridad, haciendo que las APIs sean más fáciles de entender y utilizar. Discutimos cómo los contextos delimitados pueden reflejarse en los *endpoints* y en la documentación de la API, mejorando la escalabilidad, la mantenibilidad y la experiencia del desarrollador. Esta separación de responsabilidades ayuda a gestionar la complejidad de sistemas grandes dividiéndolos en partes más pequeñas y manejables.

Además, exploramos el concepto de diseñar APIs basadas en la experiencia, centrándonos en las experiencias y flujos de trabajo del usuario en lugar de solo en entidades de datos. Este enfoque simplifica la implementación del cliente y encapsula procesos completos en transacciones individuales, haciendo que las APIs sean más robustas y fáciles de mantener. Proporcionamos un ejemplo concreto de cómo un proceso de compra de comercio electrónico se puede simplificar en una sola llamada a la API, mejorando la experiencia global del usuario.

Finalmente, este capítulo destacó la importancia de hacer que las APIs sean descubribles utilizando principios de hipermedia. Al incrustar enlaces y controles dentro de las respuestas de la API, permitimos el descubrimiento dinámico de acciones del dominio, mejorando la flexibilidad y la capacidad de evolución. La combinación de APIs basadas en la experiencia con principios de hipermedia crea un diseño de API potente e intuitivo que se alinea estrechamente con los objetivos de negocio, al tiempo que proporciona una experiencia de usuario fluida y consistente en diversas plataformas.

En el próximo capítulo, exploraremos las APIs RESTful y compararemos los diferentes estilos de API. Profundizaremos en la popularidad y las características únicas de las APIs RESTful, comparándolas con otros estilos de API como GraphQL, SOAP, gRPC y APIs asíncronas.
