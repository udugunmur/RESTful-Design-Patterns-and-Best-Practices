# Parte 1: El Estudio del Aprendiz – Preparándose para el Oficio

## Capítulo 3: Comprensión de los Ciclos de Vida de Aplicaciones y APIs

Este capítulo explica cómo adoptar una visión holística de todo el ciclo de vida de la API (*API Lifecycle*) puede influir en su diseño. Cubriremos cómo los ciclos de vida de tu API y de tu aplicación están entrelazados y proporcionaremos una visión general integral de las etapas por las que pasan una aplicación y sus APIs, desde la concepción hasta la obsolescencia.

En este capítulo, vamos a cubrir los siguientes temas principales:

- **¿Qué es el ciclo de vida de una API y cómo se relaciona con el ciclo de vida de tu aplicación?**
- **¿Cuáles son las etapas principales del ciclo de vida de una API?**
- **Por qué pensar en el diseño de tu API desde la perspectiva de toda su vida útil la hará mejor**
- **Cómo planificar el ciclo de vida de tu API en función de la audiencia objetivo, el propósito y el modelo de negocio**

---

### ¿Qué es el ciclo de vida de una API?

El ciclo de vida de una API es simplemente el proceso por el que pasa una API desde el momento en que se toma la decisión de crearla hasta el momento en que debe ser retirada del servicio (*decommissioned*). El ciclo de vida de la API sigue el mismo proceso que el ciclo de vida de la aplicación. Las APIs exponen la funcionalidad y las capacidades de datos de una aplicación, y su ciclo de vida no debe tratarse como una entidad independiente. La API sigue el mismo ciclo de vida que la aplicación de la que forma parte. Un ciclo de vida de API bien gestionado contribuye al éxito de la aplicación. Comprender esto conduce a procesos de desarrollo más eficientes, productos de mejor calidad y, en última instancia, iniciativas exitosas de transformación digital.

El ciclo de vida de la API se define como una serie de pasos que los equipos siguen para diseñar, desarrollar, desplegar y consumir APIs con éxito. Es una de las partes fundamentales de cualquier estrategia de gobierno de APIs (*API governance*). Si no defines cómo será el ciclo de vida de tu API, resultará difícil establecer políticas adecuadas de diseño, procesos y publicación.

#### ¿Por qué conocer el ciclo de vida de tu API es importante para un buen diseño?

Un ciclo de vida de API bien definido establece un entendimiento y un vocabulario compartidos para el trabajo relacionado con las APIs. En el modelo que seguiremos en este libro, un equipo creará un diseño para una API, el cual podrá compartirse con otras partes interesadas (*stakeholders*) para iniciar una comunicación eficaz. Esto ayudará a los miembros del equipo a mantenerse alineados a lo largo de todo el ciclo de vida de la API. Este diseño actuará como punto de partida para implementar la API y como una única fuente de verdad para probar si el código funciona como se espera. Una aplicación bien probada puede desplegarse y publicarse para los usuarios finales. Con la retroalimentación proveniente de ellos y de nuestros esfuerzos de monitorización, podemos ampliar y actualizar el diseño y su implementación.

Esto promueve el enfoque **API-first**, que consiste en diseñar y construir aplicaciones como una colección de servicios internos y externos entregados a través de APIs. Hablamos de esto en detalle en el Capítulo 2.

#### ¿Cuáles son los beneficios de la gestión del ciclo de vida de las APIs?

Algunos de los beneficios de la gestión del ciclo de vida de las APIs incluyen una mayor productividad, una mayor visibilidad sobre la trayectoria de la API y la alineación organizacional. Esto te permite prepararte para cada etapa. La principal ventaja de establecer un ciclo de vida de API controlado es que puedes crear y hacer evolucionar todos los procesos por los que pasará la API a lo largo de su existencia. Esto reduce incertidumbres y establece restricciones creativas. También describe cómo configurar procesos adecuados de integración y despliegue continuos (CI/CD) para que podamos automatizar el control de calidad y verificar todos los pasos involucrados.

Comprender el ciclo de vida de la API e implementar buenas prácticas para gestionarlo es crucial para un buen diseño de API por varias razones:

- **Consistencia**: Seguir un ciclo de vida de API bien definido garantiza que todas las APIs sigan un proceso de diseño y desarrollo uniforme. Esto facilita que los desarrolladores comprendan y utilicen las APIs, lo que genera procesos de desarrollo más eficientes. Al comenzar con el diseño, establecemos expectativas públicamente dentro de nuestro equipo y nos abrimos a cualquier debate desde el principio. Al remitirnos al diseño como única fuente de verdad, podemos validar la implementación y comprobar si es consistente con él.
- **Garantía de calidad (*Quality Assurance*)**: Cada etapa del ciclo de vida de la API cuenta con controles de calidad. En un ciclo de vida bien establecido, utilizamos validaciones y pruebas dentro de nuestros flujos de CI/CD; por ejemplo, podemos realizar pruebas de contrato (*contract tests*) sobre nuestra implementación durante las fases de despliegue. También podemos publicar documentación actualizada cada vez que se implementa una nueva versión del documento de diseño.
- **Versionado y mantenimiento**: Comprender el ciclo de vida de la API ayuda a gestionar diferentes versiones de la API y a planificar actualizaciones futuras. Ayuda a evitar que se introduzcan cambios disruptivos (*breaking changes*) que puedan romper las integraciones de los clientes. Lo logra introduciendo un control de calidad adecuado entre cambios e implementando verificaciones de compatibilidad hacia atrás en el flujo del ciclo de vida. También ayuda a decidir cuándo depreciar (*deprecate*) o retirar (*retire*) una API.
- **Colaboración y comunicación**: Un ciclo de vida de API bien definido facilita una mejor colaboración entre los diferentes equipos involucrados en el proceso de desarrollo. Al estandarizar un proceso de ciclo de vida, podemos establecer un vocabulario común, herramientas, recursos y pasos para cada API. Al utilizar el concepto de nuestro diseño como la única fuente de verdad, maximizamos la cantidad de partes interesadas capaces de razonar sobre la API. De esta manera, podemos crear un lenguaje común para discutir el diseño, desarrollo y gestión de la API.
- **Alineación de negocio**: El ciclo de vida de la API comienza con la planificación y el diseño de la API en función de los requisitos comerciales. Esto garantiza que la API se alinee con los objetivos del negocio y aporte valor a la organización, aumentando la transparencia del proceso para las partes interesadas comerciales.

En resumen, comprender el ciclo de vida de la API es clave para diseñar APIs consistentes, de alta calidad, fáciles de mantener y alineadas con los objetivos de negocio. Ayuda a las organizaciones a maximizar el valor de su cartera de APIs y a avanzar en sus estrategias digitales.

A continuación, conoceremos las diversas etapas del ciclo de vida de la API.

---

### Definición de las etapas del ciclo de vida de la API

Ahora que hemos aprendido sobre los beneficios de un proceso de ciclo de vida de API bien estructurado, profundicemos un poco más en su estructura. Como se mencionó anteriormente, el ciclo de vida de la API consta de varias etapas. Es posible que hayas visto esta división en varios lugares y hayas notado que puede diferir según las fuentes y las personas. El número, la denominación y otros aspectos de las etapas son arbitrarios y dependen del enfoque del programa. Por ejemplo, nosotros nos centramos en la fase de diseño y en los procesos de gobierno, mientras que algunas organizaciones o equipos pueden centrarse en la observabilidad y la capacidad de prueba. 

En este libro utilizaremos un proceso de seis pasos, que comienza con el **diseño** y finaliza con la **actualización**. Este es un bucle iterativo que termina con un paso adicional y puntual: la **retirada**. Este libro se centrará casi exclusivamente en dos fases —diseño y actualización—, al tiempo que proporcionará comentarios importantes sobre otras etapas, que son el resultado del diseño de tu API o están conectadas con la calidad y fiabilidad de tu programa de gobierno de APIs basado en el diseño.

*Figura 3.1: Etapas del ciclo de vida de la API*

Antes de que puedas empezar a construir una API, debemos recopilar los requisitos y las restricciones. Es en este paso donde descubrimos y analizamos las motivaciones que tratamos en detalle en el Capítulo 1. Este es principalmente un paso puntual, pero cada vez que surgen nuevos requisitos comerciales, es posible que debamos reevaluar nuestras motivaciones y definir el rumbo para el desarrollo futuro.

Ahora, conozcamos en detalle cada paso de nuestro proceso de siete pasos, comenzando con el diseño.

#### Diseño (*Design*)

El diseño de la API es el primer paso que atravesamos durante nuestro recorrido por el ciclo de vida y es el paso en el que se centra este libro. A lo largo de esta obra, argumentaremos que este es, sin duda, el paso más crucial y el que definirá los pasos que le siguen.

En la fase de diseño, definimos nuestro modelo de datos, así como los recursos, interfaces y acciones que admite. También nos encargamos del diseño del modelo de seguridad. El resultado de este paso será un documento que describa formalmente el diseño de nuestra API. En este libro utilizaremos la **Especificación OpenAPI (OAS)** para lograr este objetivo.

##### La especificación OpenAPI (*The OAS*)

OAS es una especificación para describir el diseño de APIs de manera legible por máquina. Al utilizarla, habilitamos una verdadera definición del ciclo de vida de la API y un enfoque *design-first* para el desarrollo de APIs. En el Capítulo 10, exploraremos OAS en detalle y trabajaremos en ejemplos concretos de cómo aprovecharla tanto en el diseño de APIs como en otras etapas del ciclo de vida.

De esta manera, durante el proceso de diseño, dispondremos de un resultado tangible que no solo se puede utilizar para generar código o documentación, sino que también sirve como la **única fuente de verdad** para las partes interesadas. Dicho enfoque se denomina desarrollo *design-first* o guiado por contratos (*contract-driven development*). Profundizamos en esto en el Capítulo 2 y exploraremos la importancia del desarrollo guiado por contratos en el Capítulo 8.

> **Buenas prácticas**  
> Si es posible, colabora con tus consumidores durante el proceso de diseño de la API. Comparte tus documentos de diseño de forma temprana para que puedan crear prototipos y aplicaciones iniciales de prueba de concepto. De este modo, podrás detectar posibles problemas técnicos de forma anticipada, incluso antes de que tu API haya sido completamente diseñada o implementada. Puedes trabajar utilizando únicamente documentos de diseño de API y servidores simulados (*mock servers*) para exponer el diseño de tu API.

#### Desarrollo y pruebas (*Development and testing*)

Esta fase trata sobre el proceso de implementación de nuestro diseño. Dado que ya disponemos de un documento que describe formalmente nuestra API, podremos validar y comprobar si nuestra implementación se ajusta a lo que hemos diseñado. Esta es una de las grandes ventajas del desarrollo guiado por contratos. Por supuesto, también realizaremos otros tipos de pruebas, como pruebas unitarias y, en el caso de APIs interdependientes, pruebas de integración. El resultado de este paso es una pieza de código funcional que se ejecuta en un entorno de desarrollo y que más tarde podremos desplegar en servidores de producción y publicar para los consumidores.

#### Despliegue (*Deployment*)

Durante esta etapa, la implementación de nuestra API se despliega en el entorno de producción. Gracias a que disponemos de nuestro documento de contrato, podemos crear barreras de control (*gatekeepers*) para garantizar que solo se desplieguen aquellas APIs correctamente implementadas. Esto se logra aprovechando el documento de diseño de la API y procesos adecuados de CI/CD con herramientas que ejecuten nuestras pruebas de contrato y cualquier otra comprobación importante para la garantía de calidad.

#### Publicación (*Publishing*)

En esta etapa, exponemos nuestra API a los consumidores. Esto significa que configuraremos aspectos asociados con la gestión de APIs, tales como:

- **Configuración de la pasarela de APIs (*API Gateway*)**: Aquí configurarás el *API gateway* o cualquier otro elemento de infraestructura a nivel de red que procesará las peticiones entrantes a tu API.
- **Autenticación y autorización**: Están descritas en parte en tu documento de diseño de API, y la implementación de esta funcionalidad suele ser cubierta por tu plataforma de gestión de APIs y/o *API gateway*.
- **Control de acceso, informes y limitación de tasa (*Rate Limiting*)**: Este es el proceso de establecer qué tipos de usuarios tienen acceso a qué recursos y si tienen algún límite en su acceso.
- **Monetización**: Implica definir el modelo de negocio para las APIs externas. Configurarás cómo se cobrará a los consumidores por su uso: tarifas planas, pago por llamada o algún tipo de modelo híbrido por niveles.

Dado que podremos consumir nuestra API desde el exterior una vez publicada, este es también el paso donde realizaremos **pruebas de integración** con nuestra API. Esto garantiza que todo el esfuerzo de configuración invertido aquí funcione como se espera.

#### Consumo y monitorización (*Consuming and monitoring*)

Esta es la etapa en la que nuestra API publicada es consumida por aplicaciones cliente. Dado que nos basamos en documentos de diseño de API, nuestros consumidores pueden comenzar a crear aplicaciones cliente antes de que nuestra implementación esté completamente lista en producción. Al remitirse a una única fuente de verdad, no hay ambigüedad entre el diseño y la implementación, por lo que podemos acelerar ciertos procesos sin temor a discrepancias.

Una vez que tenemos nuestra API ejecutándose en producción y las aplicaciones cliente realizan llamadas a nuestro sistema, necesitamos poder observar el tráfico. Configurar sistemas de monitorización adecuados es crucial para el éxito de tu API. Gracias a buenos sistemas de monitorización, podemos ver datos relacionados con el consumo de nuestras APIs, su rendimiento y si existen problemas con el tráfico. Al saber qué errores de tráfico se producen, podemos determinar fácilmente cuál es la causa. De esta manera, podemos detectar rápidamente cualquier ataque potencial o amenaza de seguridad, errores no capturados, posibles problemas con las cargas útiles (*payloads*) y mucho más. Este paso, aunque su configuración no sea el aspecto que más recursos o tiempo consume en el ciclo de vida de la API, es el que más dura y, junto con el diseño, es crucial para el éxito.

El nivel de detalle proporcionado con respecto a la monitorización del tráfico también depende de la calidad del diseño de tu API. Un diseño adecuado del cuerpo del objeto de error, el uso correcto del protocolo HTTP y las definiciones de seguridad determinarán la calidad de la información transmitida a tus sistemas de monitorización. Cuanto más claros y exactos sean, menor ambigüedad existirá en el tráfico.

#### Actualización (*Update*)

La última etapa de nuestro bucle de ciclo de vida iterativo es la fase de actualización. Pasamos por la fase de actualización tanto durante la fase de construcción como durante la fase de producción de nuestra API. Al construir y diseñar la API, si estás creando prototipos con futuros consumidores, lo más probable es que estos aporten comentarios respecto a tu diseño actual. En la fase de producción, este paso se produce tanto por los comentarios de los usuarios como por los cambios o actualizaciones introducidos en los requisitos comerciales.

La regla más importante al actualizar el diseño de tu API es **no romper los clientes existentes**. Esto supone un problema mucho menor si tu API aún no está en producción, pero una vez que disponemos de tráfico real, otros sistemas dependen de nuestra API y del hecho de que pueda cumplir con las reglas previas.

Debemos seguir una serie de reglas sencillas para garantizar que nuestras actualizaciones de diseño no sean incompatibles hacia atrás:

1. **No debes eliminar nada** (relacionado con el principio de superficie mínima y el principio de robustez).
2. **No debes cambiar las reglas de procesamiento**.
3. **No debes convertir elementos opcionales en obligatorios**.
4. **Cualquier cosa que agregues debe ser opcional** (relacionado con el principio de robustez).

Seguir estas reglas minimizará la posibilidad de introducir cambios disruptivos para tu cliente. Discutiremos el proceso de actualización de tu API en detalle en el Capítulo 13.

> **Más información**  
> - Principio de superficie mínima (*Minimal surface principle*): [martinfowler.com](https://martinfowler.com)  
> - Principio de robustez (*Robustness principle*): [https://datatracker.ietf.org/doc/html/rfc761#section-2.10](https://datatracker.ietf.org/doc/html/rfc761#section-2.10)

#### Retirada (*Retirement*)

Con el tiempo, llegará el momento en que necesitarás desactivar tu API. Esto puede suceder por múltiples razones, como la existencia de una API nueva y más eficiente con la misma funcionalidad, una deuda técnica que obligue a rehacer la API desde cero, un cambio en los objetivos o requisitos del negocio, entre otras. Al igual que en la fase de actualización, intentamos asegurarnos de que este paso afecte a nuestros consumidores lo menos posible. Ten en cuenta que esto no se puede eliminar por completo, ya que, al fin y al cabo, estamos cerrando nuestro servicio. Esta fase consiste principalmente en una comunicación clara, y debe ser gradual y no instantánea. El proceso de retirar gradualmente un servicio suele denominarse **retirada progresiva (*sunsetting*)**. Discutiremos esta etapa en detalle en el Capítulo 13.

---

### ¿Por qué la etapa de diseño es la que lo impacta todo?

Como se mencionó anteriormente, el documento de diseño de la API es un documento formal y legible por máquina que actúa como un recurso de referencia para todas las partes interesadas. Lo utilizamos como la **única fuente de verdad** durante nuestro proceso de ciclo de vida de la API. El uso de documentos estructurados, inequívocos y legibles por máquina también nos ayuda a probar la implementación, crear documentación, desplegar y publicar nuestras APIs, monitorizar y mucho más.

El uso del documento de diseño de API como única fuente de verdad aporta múltiples beneficios:

- **Define expectativas**: La etapa de diseño de la API establece las expectativas sobre qué hará la API, cómo se comportará y qué entregará. Describe los recursos, operaciones y modelos de datos que expondrá la API.
- **Facilita la comunicación**: Una API bien diseñada sirve como contrato entre el proveedor de la API y los consumidores. Comunica la funcionalidad de la API a desarrolladores, gestores de producto y otras partes interesadas, asegurando que todos tengan una comprensión clara de sus capacidades.
- **Impulsa la consistencia**: Un buen diseño de API promueve la consistencia en todas las APIs de una organización. Esto facilita a los desarrolladores comprender y utilizar las APIs, lo que genera procesos de desarrollo más eficientes.
- **Impacta en la experiencia del usuario**: El diseño de la API repercute directamente en la experiencia de usuario de las aplicaciones que la consumen. Una API mal diseñada puede provocar una experiencia de usuario deficiente, mientras que una API bien diseñada puede posibilitar una experiencia fluida e intuitiva. La capacidad de consultar el diseño de la API desde el principio y disponer de una vía para proporcionar retroalimentación al proveedor es también crucial para un diseño de API de calidad y centrado en la prestancia (*affordance*).
- **Prepara tu API para el futuro**: Un diseño de API bien meditado puede dar cabida a cambios y adiciones futuras sin romper la funcionalidad existente. Esto hace que tu API sea más resistente a los cambios y garantiza su longevidad.

En resumen, la etapa de diseño de la API es crucial porque sienta las bases para todas las etapas posteriores del ciclo de vida de la API. Sirve como la única fuente de verdad que guía el desarrollo, despliegue y mantenimiento de la API. Por lo tanto, invertir tiempo y esfuerzo en la etapa de diseño puede generar grandes beneficios en forma de una API robusta, fácil de usar y preparada para el futuro.

#### ¿Por qué el diseño y no el código?

Si eres principalmente un desarrollador o ingeniero, es posible que sientas la tentación de utilizar el código como la única fuente de verdad. Tiene algunos beneficios al principio, como reducir el tiempo dedicado al diseño al no tener que crear un documento de diseño específico. Además, dado que el código es en esencia tu aplicación, no puede haber discrepancias entre el código y el diseño. 

Sin embargo, estos beneficios disminuyen rápidamente a largo plazo: por ejemplo, es mucho más difícil para otras partes interesadas razonar sobre tu API únicamente a partir del código. El código también tiende a carecer de herramientas específicas para generar documentación clara y eficiente; puede que no resulte evidente a partir de la base de código cómo se pretende utilizar la API. Por su propia naturaleza, el código también cambiará con mucha más frecuencia, lo que dificultará versionar adecuadamente tu API y mantener actualizadas la documentación y las implementaciones de los clientes.

A continuación, investigaremos cómo gestionar con éxito los ciclos de vida de tu aplicación y de tu API.

---

### Gestión exitosa de los ciclos de vida de aplicaciones y APIs

Crear un proceso adecuado dentro del ciclo de vida de la API implica varios pasos clave. Veámoslos en detalle:

1. **Definición clara de objetivos**: Construir una API alineada con el modelo de negocio principal. Por ejemplo, una tienda electrónica accesible vía web y dispositivos nativos, que se integre con mercados externos.
2. **Adoptar un enfoque «design-first»**: Diseñar la API antes de escribir cualquier línea de código. Utiliza un lenguaje de descripción de APIs como la Especificación OpenAPI (que cubriremos en detalle en el Capítulo 10) para definir los recursos, operaciones, modelos de datos y esquemas de seguridad de la API. Esto servirá como contrato entre los desarrolladores y consumidores de la API.
3. **Involucrar a las partes interesadas clave**: Al involucrarlas en el ciclo de vida de la API, obtienes información valiosa que mejora la usabilidad y efectividad de la API, al tiempo que coincide con los objetivos comerciales de tu organización. Esto incluye no solo a desarrolladores, sino también a gestores de producto, analistas de negocio e incluso usuarios finales.
4. **Generar documentación durante la fase de diseño**: Al utilizar documentos de diseño como OAS, puedes generar tu documentación durante la etapa de diseño. Proporcionar documentación completa para tu API mejora la capacidad de razonar sobre ella ante un grupo más amplio de partes interesadas. Esto debe incluir descripciones detalladas de los recursos, operaciones y modelos de datos de la API, así como ejemplos de uso y el contexto en el que operan.
   > **Más información**  
   > Puedes leer más sobre OAS aquí: [https://www.openapis.org/](https://www.openapis.org/)
5. **Implementar estándares de API**: Son estándares para el diseño, desarrollo y documentación de APIs que garantizan la coherencia en todas las APIs y facilitan su uso. Los desarrolladores suelen tener una mejor experiencia trabajando con sistemas familiares.
6. **Implementar medidas de seguridad robustas**: Proteger tu API es crucial. Esto incluye autenticación, autorización y cifrado. Además, aprovechar esquemas de seguridad y patrones de diseño probados mejorará la estabilidad general de tu sistema.
7. **Planificar cambios y adiciones**: Define cuál será tu enfoque ante este proceso. Utiliza un versionado adecuado del documento de diseño para gestionar estos cambios y evitar interrupciones a los consumidores, y planifica si necesitarás versionado de API en producción. Son dos conceptos distintos y hablaremos de ellos en profundidad en los Capítulos 10 y 13.
8. **Utilizar pruebas automatizadas desde la fase de diseño**: Automatiza tanto como sea posible el proceso de pruebas. Esto incluye pruebas funcionales, de rendimiento y de seguridad. También debe incluir validaciones de diseño durante la creación del documento de diseño. De esta forma, garantizas el cumplimiento de los estándares de diseño (tanto externos como internos de tu organización). Las pruebas automatizadas ahorran tiempo y ayudan a detectar problemas de forma temprana.
9. **Monitorizar el uso y rendimiento**: Una vez desplegada la API, monitoriza su uso y rendimiento. Utiliza estos datos para iterar sobre la API y realizar mejoras. Es un proceso continuo a lo largo de todo el ciclo de vida y resulta crucial para su éxito: no puedes razonar sobre datos que no puedes medir.
10. **Planificar la retirada de forma ordenada**: Cuando llegue el momento de retirar una API, hazlo de manera que se minimicen las interrupciones a los consumidores. Proporciona avisos con suficiente antelación y ofrece alternativas si es posible.

Recuerda que el ciclo de vida de la API es un **proceso continuo**. Incluso después de desplegar una API, debes continuar monitorizando su rendimiento, recopilando comentarios y realizando mejoras. El ciclo de vida de la API es **iterativo**: no es un proceso de una sola vez, sino un ciclo continuo de etapas que se repiten con el tiempo. Una vez retirada la API, el ciclo de vida puede comenzar nuevamente con la planificación y el diseño de una nueva API. Esta naturaleza iterativa permite que la API mejore continuamente y se adapte a nuevos requisitos y tecnologías, asegurando que permanezca relevante, útil y eficaz. 

La retroalimentación de los consumidores es una parte crucial de este proceso iterativo, ya que fundamenta las mejoras y los cambios en cada iteración. Así, el ciclo de vida de la API no es simplemente un proceso lineal, sino un bucle de retroalimentación que promueve el aprendizaje y la mejora continuos. Entendamos esto considerando nuestra tienda electrónica.

#### Ejemplo de un modelo de ciclo de vida para una tienda electrónica

Para mostrar una aplicación más concreta del enfoque descrito anteriormente, apliquémoslo a una plataforma de comercio electrónico que vende artículos mágicos:

- **Definición clara de objetivos**: Construimos una API para nuestra *Magic e-Store*, la cual es central para nuestro modelo de negocio. La tienda electrónica será accesible a través de la web y dispositivos nativos, y se integrará con mercados externos (*marketplaces*).
- **Design-first**: Hemos elegido un enfoque *design-first*, lo que significa que nuestro desarrollo comenzará con el diseño de la API. Esto se cubrirá en los Capítulos 9 y 10.
- **Elección de estándares**: Decidimos utilizar **JSON** como formato de datos predeterminado. Además, adoptaremos el estándar **Problem Details (RFC 9457)** para transmitir detalles de error legibles por máquina. Dado que nuestro objetivo es construir una API guiada por hipermedia (tratada en el Capítulo 6), utilizaremos **HAL** (*Hypertext Application Language*), que ofrece una solución ligera adaptada a nuestras necesidades.
  > **Más información**  
  > - Problem Details: [https://www.rfc-editor.org/rfc/rfc9457.html](https://www.rfc-editor.org/rfc/rfc9457.html)  
  > - HAL: [https://datatracker.ietf.org/doc/html/draft-kelly-json-hal-11](https://datatracker.ietf.org/doc/html/draft-kelly-json-hal-11)
- **Implementación de seguridad**: Para la autorización utilizaremos **OAuth 2.0**, mientras que para la autenticación emplearemos **OpenID Connect**. Todo el tráfico estará cifrado mediante **HTTPS**. También planeamos publicar nuestra API a través de una plataforma de gestión de APIs, que gestionará el control de acceso, la limitación de tasa (*rate limiting*) y la regulación (*throttling*). El Capítulo 7 cubre la seguridad de APIs en detalle.
- **Planificación de cambios**: Hemos decidido no versionar la API ni sus *endpoints* en la URL para no romper a los consumidores existentes. Si se necesitan nuevas versiones, se introducirán como nuevos *endpoints*. Seguiremos el principio **YAGNI** (*You Aren’t Gonna Need It*) para mantener una superficie de API mínima sin dejar de cumplir los requisitos del producto. Las estrategias de versionado de APIs se explorarán más a fondo en el Capítulo 13.
  > **Más información**  
  > Principio YAGNI: [https://martinfowler.com/bliki/Yagni.html](https://martinfowler.com/bliki/Yagni.html)
- **Pruebas automatizadas**: Nuestro primer paso será asegurar que el diseño de nuestra API cumpla con los estándares elegidos mediante la validación del diseño. También realizaremos pruebas de contrato para verificar que la implementación coincida con el diseño. Esto complementará otros tipos de pruebas automatizadas no relacionadas con el diseño en sí. El Capítulo 12 ofrece más detalles sobre las técnicas de prueba de APIs.
- **Monitorización**: Queremos que nuestra plataforma de gestión de APIs registre todas las llamadas a la API, proporcionando visibilidad sobre el tráfico entrante. Se discutirán estrategias de monitorización adicionales en el Capítulo 13.
- **Planificación para la retirada**: Al depreciar *endpoints* o retirar la API (*sunsetting*), es crucial comunicarse eficazmente con los consumidores de la API. Estos temas se tratarán en detalle en el Capítulo 13.

De esta manera, podemos planificar el enfoque que queremos tener para nuestra API a lo largo de su ciclo de vida. Sin embargo, falta un elemento fundamental que une todo el proceso: la comunicación entre las diferentes partes interesadas y equipos. Conozcamos más al respecto.

#### La importancia de la comunicación

La comunicación desempeña un papel fundamental en el ciclo de vida de la API por varias razones:

1. **Habilita una colaboración eficaz**: Las APIs son desarrolladas por equipos, no por individuos. Una comunicación clara y efectiva ayuda a garantizar que todos en el equipo comprendan el diseño, la funcionalidad y los objetivos de la API. Esto promueve la colaboración y ayuda a prevenir malentendidos que pueden derivar en errores, retrasos o discrepancias de funcionalidad.
2. **Esencial para una documentación clara y completa**: Esta documentación sirve como guía para los desarrolladores que utilizarán la API, ayudándoles a integrarla eficazmente en sus aplicaciones. También proporciona contexto a los responsables de la toma de decisiones sobre qué tipo de funcionalidad suministra tu API y en qué escenarios se utilizará. Una buena documentación también debe potenciar el bucle de retroalimentación entre los desarrolladores y los consumidores de la API, permitiendo recopilar información valiosa para mejorar la API en futuras iteraciones.
3. **Crucial en producción**: Las APIs experimentan cambios y actualizaciones con frecuencia. Comunicar estos cambios de manera efectiva a todas las partes interesadas (desarrolladores, usuarios finales y líderes empresariales) es vital para gestionar las modificaciones y asegurar que la API continúe cumpliendo sus objetivos. Asimismo, los canales de comunicación deben utilizarse para notificar periodos de inactividad programada en los servidores e información sobre obsolescencia o retirada de servicios. Cuando una API va a ser retirada, comunicarlo con suficiente antelación otorga a los afectados tiempo para realizar los ajustes necesarios y evitar interrupciones operativas.

Como hemos visto, la comunicación es un aspecto clave del ciclo de vida de la API: facilita la colaboración, ayuda a gestionar los cambios y garantiza que la API satisfaga las necesidades de sus consumidores. Sin una comunicación eficaz, el ciclo de vida de la API puede volverse desarticulado e ineficiente, dando lugar a APIs de calidad inadecuada y consumidores insatisfechos.

#### Creación de prototipos y bucle rápido de retroalimentación

La capacidad de validar rápidamente tu diseño con tus futuros consumidores es de un valor incalculable:

*Figura 3.2: Un bucle rápido de retroalimentación en el ciclo de vida de la API*

Esta es la aplicación práctica del proceso de diseño de APIs centrado en la prestancia (*affordance-centric*), donde el equipo de diseño colabora estrechamente con los futuros consumidores. Al adoptar un enfoque *design-first* y disponer de un documento de diseño desde el principio, podemos recopilar comentarios durante el propio proceso de diseño:

*Figura 3.3: OAS es una parte fundamental de todo el ciclo de vida y desarrollo de la API*

Por ejemplo, la especificación OAS es un documento JSON o YAML y, por tanto, es legible por máquina y determinista. Esto nos permite aprovecharla para generar un servidor simulado (*mock server*) con datos y llamadas de prueba. También podemos generar la documentación de nuestra API para todas las partes interesadas. Además, podemos generar los SDKs de la API y colaborar con los consumidores para que puedan comenzar a desarrollar sus aplicaciones cliente. Obtendremos un tipo de retroalimentación al razonar sobre la API a partir de su documentación diferente de la que obtendremos al implementar una aplicación cliente; ambas son igualmente valiosas.

Cuando involucramos a nuestros futuros clientes en el proceso de diseño, podemos modificar nuestro trabajo rápidamente para satisfacer sus necesidades. Utilizar un documento OAS hace que nuestro trabajo sea más visible para los demás involucrados y acelera la creación de prototipos mediante APIs simuladas (*mocks*) para pruebas o SDKs que agilicen la integración. No existen desventajas en esta forma de trabajar.

---

### Resumen

En este capítulo, hemos profundizado en el concepto del ciclo de vida de la API, subrayando su importancia. Enfatizamos la relevancia de considerar el ciclo de vida de la API y el ciclo de vida de la aplicación como entidades entrelazadas, reconociendo a las APIs como la capacidad fundamental de cualquier aplicación.

También aprendimos sobre las diversas etapas del ciclo de vida de la API, desde la creación hasta la retirada de servicio. Un ciclo de vida de API bien definido establece un entendimiento y un vocabulario compartidos para el trabajo relacionado con las APIs. Sirve como punto de partida para implementar la API y como única fuente de verdad para las pruebas. Esto promueve el enfoque *API-first*, que conduce a una mayor productividad, mayor visibilidad y alineación organizacional.

Asimismo, destacamos la importancia de la comunicación en los procesos del ciclo de vida de la API. El ciclo de vida de la API no es un proceso puntual, sino un ciclo continuo de etapas que se repiten a lo largo del tiempo. Por lo tanto, comprender el ciclo de vida de la API es clave para diseñar APIs consistentes, de alta calidad, fáciles de mantener y alineadas con los objetivos comerciales.

En el próximo capítulo, presentaremos los conceptos del **Diseño Guiado por el Dominio (*Domain-Driven Design* / DDD)** en el contexto del diseño de APIs REST. Repasaremos los conceptos centrales de DDD y te ayudaremos a comprender cómo alinear la funcionalidad de tu API con el dominio de negocio en el que se ubica. También aprenderemos a aplicar el diseño de APIs guiado por el dominio en la práctica y a evitar antipatrones.
