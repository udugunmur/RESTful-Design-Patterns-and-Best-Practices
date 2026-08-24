# Parte 1: El Estudio del Aprendiz – Preparándose para el Oficio

## Capítulo 1: El «Por qué» del Desarrollo de APIs

Hoy en día, las APIs son indispensables para cualquier negocio digital. Son las carreteras, puentes, aceras, semáforos, señales, etc., de internet. Esto puede parecer una afirmación audaz, pero si lo piensas detenidamente, prácticamente cualquier interacción digital que tienes en tu vida cotidiana involucra el uso de APIs. Tu aplicación de mapas obtiene datos sobre la ruta y las condiciones del tráfico desde docenas de APIs; pagar con tu teléfono en una tienda involucra varias APIs que conectan al banco con la compañía de tarjetas de crédito y con la aplicación del teléfono móvil. Los ejemplos son infinitos.

En este libro, profundizaremos en cómo diseñar APIs REST, el estilo de API más común y robusto. Nuestro enfoque consiste en considerar las APIs no como sistemas aislados, sino desde una perspectiva más amplia. Recorreremos todo el proceso del ciclo de vida de una API, centrándonos también en cómo afectan a otros sistemas dentro de un ecosistema mayor.

Al finalizar el libro, serás capaz de diseñar tu API y los procesos que la rodean: desde argumentar adecuadamente por qué debe construirse, pasando por el diseño práctico utilizando herramientas líderes en la industria, hasta ponerla finalmente en producción y, eventualmente, planificar su retirada (*sunsetting*).

Antes de aventurarse en el ámbito del diseño y desarrollo de APIs, es crucial abordar la pregunta fundamental: «¿Por qué?». ¿El propósito es exponer funcionalidades a otras aplicaciones y ampliar la oferta de tu negocio, o es la columna vertebral de tu empresa? La creación de APIs también exige una comprensión clara del público objetivo al que van dirigidas. Identificar con precisión el grupo de consumidores es fundamental, ya que moldea la arquitectura de la API y fundamenta decisiones críticas sobre estrategias de gestión y protocolos de seguridad.

En este capítulo, cubriremos los siguientes temas principales:

- **El «Por qué» del desarrollo de APIs: Explorando las motivaciones fundamentales**
- **Identificación de la audiencia de tu API: Adaptando tu enfoque**
- **Las APIs como catalizadores del negocio: Impulsando el valor y la innovación**

Comenzaremos a crear nuestro propio proyecto, partiendo de una buena motivación.

---

### Beneficios gratuitos incluidos con tu libro

Tu compra incluye una copia gratuita en PDF de este libro junto con otros beneficios exclusivos. Consulta la sección *Beneficios gratuitos incluidos con tu libro* en el Prefacio para desbloquearlos al instante y maximizar tu experiencia de aprendizaje.

---

### El «Por qué» del desarrollo de APIs: Explorando las motivaciones fundamentales

Antes de adentrarnos en los dominios del diseño de APIs, debemos entender las razones detrás de ello. En esta etapa contamos con algún tipo de requerimiento de negocio o técnico que debemos cumplir. En lugar de sumergirnos directamente en el diseño o desarrollo de la API, primero comprendamos el ecosistema al que vamos a contribuir con nuestra nueva pieza de software. Es un sistema de vasos comunicantes y las actualizaciones aparentemente triviales pueden afectar a múltiples de sus elementos. Como primer ejercicio, exploremos las razones fundamentales que hacen necesaria la creación de APIs.

#### La esencia de las APIs

A menudo, las APIs se construyen para proporcionar datos a nuestras aplicaciones sin la necesidad de acoplar estrechamente la capa de presentación con la capa de datos. Sin embargo, las APIs no sirven únicamente para crear aplicaciones. Permiten la integración de datos a través de múltiples plataformas. Las APIs se utilizan habitualmente para brindar acceso a diversos conjuntos de datos. De esta manera, obtienes acceso a los datos sin ningún intermediario. Las APIs pueden conectarse directamente a bases de datos, hojas de cálculo u otras aplicaciones empresariales; básicamente, a cualquier dato legible por máquina para su procesamiento local.

La razón por la cual las APIs ganaron tanta tracción en los primeros días de la revolución de la Web 2.0 fue que garantizan que tu producto o servicio funcione sin interrupciones de principio a fin. Las APIs son los conectores que habilitan la mayor parte de las comunicaciones entre las aplicaciones web o *apps* que utilizamos hoy en día. Funcionan comunicándose e intercambiando datos con otros sistemas. Hoy en día, puedes integrarte fácilmente con la mayoría de los productos SaaS disponibles en el mercado a través de sus APIs y combinar (*mash-up*) datos o servicios de diferentes fuentes para crear un nuevo producto.

Así es también cómo las APIs potencian a las empresas. Al optimizar las operaciones, ofrecer integración con terceros o permitir el análisis de datos, las APIs impulsan el crecimiento del negocio, crean nuevas formas de desarrollar productos genuinamente útiles mediante la integración de aplicaciones de terceros, amplían la oferta y fomentan colaboraciones. Toma los datos de tus actividades deportivas, tu báscula inteligente conectada y una base de datos en línea de recetas de cocina, y podrás construir una aplicación que ayude a las personas a crear planes de alimentación de acuerdo con su gasto energético y objetivos deportivos.

Otras ventajas de las APIs incluyen la capacidad de alejarse del software monolítico y avanzar hacia componentes más pequeños y fáciles de mantener. Esto también permite que los equipos responsables de diferentes partes de la aplicación se dividan de una manera más funcional. Mantener una base de código gigante que necesita actualizarse con frecuencia es engorroso y puede conllevar muchos riesgos potenciales al desplegar una nueva versión.

Estos son solo un puñado de ejemplos de cómo las APIs mejoran las capacidades del negocio, no solo abriendo nuevas fuentes de ingresos potenciales, sino también tecnológicas, democratizando el acceso a los datos y a las funcionalidades de nuestras aplicaciones. Son el catalizador de una economía digital más distribuida y conectada.

En la siguiente sección, exploraremos cómo los diferentes tipos de audiencias definirán nuestro diseño de API y el enfoque de negocio.

#### Diseño de APIs centrado en la audiencia

Al construir una API, tenemos que definir su audiencia. Podemos clasificar a grandes rasgos las APIs dependiendo de si sus consumidores son internos o externos a nuestra organización. Podemos determinar si los consumidores son internos a nuestro equipo/departamento/empresa, compartidos con una lista selecta de socios (*partners*) o disponibles públicamente para cualquiera que se registre, en modalidad de autoservicio (*self-service*), en nuestra plataforma de APIs.

Crear APIs para una **audiencia interna** ayuda a reutilizar nuestras interfaces y datos con más sistemas, otorga visibilidad a dichas interfaces y nos permite construir un entorno más descentralizado y desacoplado.

Las motivaciones para las **APIs externas** se centran principalmente en las posibilidades de negocio que aportan. Cuando se exponen a terceros, no solo nos brindan la posibilidad de monetizar directamente el uso de los datos que almacenamos, sino que también abren nuestra organización a posibles integraciones con otras plataformas, exponiéndonos a más fuentes de ingresos.

También podemos identificar las motivaciones desde una perspectiva más técnica. ¿Qué tipo de dispositivo consumirá nuestras APIs? ¿Será una computadora, un teléfono móvil o tal vez un dispositivo IoT? Identificar a cuál de estos grupos (o tal vez a varios) pertenece nuestra audiencia tiene un impacto enorme en las restricciones de diseño de nuestra API. Esto impactará enormemente en nuestra estrategia de seguridad y aprovisionamiento de claves, así como en aspectos como la gestión y documentación de la API.

Tras identificar a nuestra audiencia principal, contamos con una posibilidad inmensamente poderosa: podemos trabajar en estrecha colaboración con algunos de nuestros futuros consumidores durante el proceso de diseño para crear prototipos rápidos y verificar nuestros diseños. De este modo, sabremos desde el principio cuáles son sus necesidades exactas y si nuestras suposiciones eran correctas. Esto mejora enormemente el ciclo de innovación y nos permite corregir cualquier error de diseño de forma temprana. Profundizaremos en este tema en la siguiente subsección.

#### Impulsores tecnológicos para la creación de APIs

Si vamos a construir una API dentro de una organización más grande, es casi seguro que ya existirán otros elementos funcionando dentro de tu ecosistema. Tu nueva API puede ser una extensión de uno de ellos o una entidad completamente nueva. En cualquier caso, si observamos el software desde la perspectiva de los datos, nos damos cuenta de que las aplicaciones son procesadores de datos que aplican funciones sobre datos almacenados y obtienen y transforman nuevos datos. Continuando bajo esta misma perspectiva, las APIs son interfaces para esos datos. Permiten la interoperabilidad entre los sistemas y sus elementos. Es como la transición de una oficina basada en cubículos a un espacio abierto (*open space*), donde la información y la cultura pueden fluir más libremente.

Dependiendo del nivel de transformación digital de tu organización, las APIs permitirán mejorar enormemente la eficiencia automatizando procesos previamente manuales. Considera el siguiente escenario real en un centro de investigación médica: el equipo generaba grandes cantidades de datos a partir de diversas fuentes y los investigadores debían solicitar con frecuencia conjuntos de datos específicos a su departamento de TI. Como puedes imaginar, este era un proceso muy arduo y manual, con largos tiempos de espera que afectaban la productividad y los costes. Una plataforma de APIs para acceder a los datos de forma estandarizada y en autoservicio les permitió obtener una disponibilidad de datos casi instantánea, con mayor seguridad (gracias a políticas de seguridad adecuadas) y la capacidad de crear presentaciones de datos en tiempo real.

El ejemplo anterior es también una fantástica demostración de cómo las APIs mejoran la **escalabilidad** de tu sistema. El caso fue bastante extremo, pasando de un enfoque manual a uno basado en APIs. Sin embargo, debido a las cualidades intrínsecas de las APIs, como la **falta de estado (*statelessness*)** y el **desacoplamiento débil (*loose coupling*)**, son fácilmente escalables por naturaleza:

- **Falta de estado (*Statelessness*)**: Garantiza que cada petición de los consumidores de la API contendrá toda la información necesaria para procesarla. Tu sistema no tendrá que almacenar información de sesión, lo que permitirá escalar fácilmente tu API de manera horizontal añadiendo más máquinas, ya que no se necesita el contexto de interacciones previas.
- **Desacoplamiento débil (*Loose coupling*)**: Significa que puedes escalar o cambiar cualquier elemento de tu API de manera independiente. Por ejemplo, puedes colocar una máquina más potente en el lado del servidor sin tocar tus pasarelas de API (*API gateways*), o cambiar tu método de autorización por uno más adecuado para usuarios externos sin afectar en absoluto al *backend* de tu API.

Las APIs también promueven la **reutilización de funcionalidades** a través de múltiples aplicaciones, reduciendo la redundancia y mejorando la mantenibilidad. No necesitas construir un *backend* para cada tipo de aplicación con la que operen tus consumidores, sino aprovechar las APIs para suministrar datos a todas las diferentes aplicaciones cliente, asegurando los mismos datos en cada dispositivo.

Por último, pero no menos importante, las APIs funcionan realmente bien para cualquier sistema modularizado y distribuido. Representan un cambio de paradigma en la forma en que ocurre la comunicación entre los componentes del sistema: de un sistema centralizado a uno descentralizado, y eventualmente a uno distribuido y en evolución orgánica. Técnicamente, las APIs son agnósticas respecto a si tu sistema es un monolito o está basado en microservicios. No obstante, si deseas realizar una transición desde un monolito tradicional hacia microservicios o un sistema modularizado, probablemente necesitarás comenzar construyendo APIs para tus interacciones de datos centrales.

#### APIs: Los catalizadores del cambio empresarial (*The Business Game Changers*)

Como bien sabemos, las motivaciones tecnológicas rara vez son los principales impulsores para construir APIs. Sin embargo, las APIs aportan una gran cantidad de beneficios extraordinarios para el negocio. Por un lado, permiten a las empresas innovar exponiendo datos y funcionalidades que pueden utilizarse para crear nuevos productos y servicios. 

Un gran ejemplo de esto es **Twilio**. Al exponer sus diversos servicios de comunicación a través de APIs, impulsaron a una gran cantidad de empresas a aprovechar sus sistemas internos y generar un valor real para sus consumidores. Por ejemplo, **Airbnb** utilizó la API de Twilio para agilizar la comunicación entre los huéspedes y los anfitriones de los alojamientos. Al automatizar la mensajería SMS, Airbnb facilitó la conexión de los anfitriones con los huéspedes, proporcionando una mejor experiencia para ambas partes. Esto también abrió nuevas fuentes de ingresos para Twilio al monetizar sus APIs, siendo este su principal motor de ingresos.

Las APIs también pueden facilitar alianzas estratégicas (*partnerships*) al proporcionar un medio para que los socios integren sus servicios. Por ejemplo, **Adidas** se integra, mediante APIs, con revendedores en línea como Amazon o Zalando para crear nuevas fuentes de ingresos y obtener acceso a grandes plataformas de venta online, ampliando así su mercado al aprovechar el alcance de estas grandes plataformas. Adidas también pudo mejorar el compromiso del cliente (*customer engagement*) integrando realidad aumentada en su aplicación móvil a través de APIs. De este modo, sus clientes, sin necesidad de acudir a una tienda física para probarse zapatillas, pueden comprobar desde casa si les gusta el estilo del producto de Adidas y luego realizar el pedido en línea.

Cuando un negocio opera principalmente a través de APIs, nos referimos a esto como participar en la **Economía de las APIs (*API Economy*)**. Profundizaremos en el tema de la Economía de las APIs en la última sección de este capítulo: *Las APIs como catalizadores del negocio: Impulsando el valor y la innovación*.

#### El acto de equilibrio: Crear nuevas APIs frente a extender las existentes

Tenemos a nuestro negocio y a los ingenieros convencidos de construir una API. Sin embargo, construir una API desde cero no siempre es el mejor curso de acción. ¿Quizás ya tenemos una API aparentemente similar en nuestro ecosistema? Si es así, planteémonos las siguientes preguntas:

1. **¿Qué estilo o paradigma utiliza la API?** ¿Es el mismo que estábamos planeando construir?
2. **¿Qué pila tecnológica (*tech stack*) utiliza?** ¿Aún disponemos de recursos humanos para darle soporte y mantenerla a largo plazo?
3. **¿La API existente pertenece al mismo dominio que la que deseamos construir?** Tal vez operen sobre recursos similares, pero en un dominio completamente diferente. Por ejemplo, un *pedido* (*order*) será algo muy diferente cuando hablamos de la parte de comercio electrónico de tu negocio frente al dominio de fabricación o logística.
4. **¿Son tus nuevos requisitos de negocio una extensión de lo que tu API actual ya suministra?** ¿Eres capaz de entregar ya un subconjunto de la funcionalidad requerida con ella?
5. **¿Extender tu API actual rompería los clientes existentes?** Esta es una pregunta delicada, ya que con precauciones especiales podemos evitar este riesgo. Sin embargo, existen situaciones que definitivamente no serán retrocompatibles, como la necesidad de un nuevo patrón de autorización o la implementación de límites previamente inexistentes en la estructura de las peticiones.

Recuerda que estas decisiones deben tomarse en el contexto de tu situación y necesidades específicas. También es importante considerar el impacto potencial en tus usuarios y asegurarse de que cualquier cambio sea comunicado con claridad y esté bien documentado. Evalúa siempre las compensaciones (*trade-offs*) entre construir de nuevo, extender y reutilizar. No se trata solo de la necesidad inmediata, sino también del mantenimiento y la escalabilidad a largo plazo.

#### Adhesión a estándares en el desarrollo de APIs

Uno de los aspectos más importantes a considerar al construir o extender una API existente es qué tipo de estándares estamos siguiendo. Podemos distinguir dos clases de estándares para el diseño de APIs: **singulares** y **globales**.

##### Estándares singulares (*Singular standards*)

Los estándares singulares describen exactamente lo que debe ser una API y no dejan mucho margen para interpretaciones. Estándares como **SCIM** (*System for Cross-domain Identity Management*) para la gestión de identidades y accesos definen estrictamente cómo debe verse una API que se adhiera a ellos. Especifican todos los *endpoints* requeridos, los modelos de datos para tus recursos, la estructura de las respuestas, etc.

> **Más información**  
> Encuentra más información sobre SCIM aquí: [https://simplecloud.info/](https://simplecloud.info/)

Al construir este tipo de APIs no tienes mucho que decidir en términos de diseño. Es importante adherirse al estándar lo más estrechamente posible, incluso si eso significa desviarse de las políticas de diseño de tu organización. De esta manera garantizamos la interoperabilidad con otros sistemas que entiendan dicho estándar, minimizamos la curva de aprendizaje para los desarrolladores y reducimos la complejidad del diseño. Estos estándares también suelen contar con secciones donde puedes extenderlos para adaptarlos a tus necesidades específicas; sin embargo, todo lo que esté formalmente definido debe permanecer sin cambios. Ten en cuenta que nos referimos a la parte de diseño: aspectos como el control de acceso, la seguridad, etc., deben seguir cumpliendo las políticas habituales.

##### Estándares globales (*Global standards*)

Los estándares globales son aquellos que proporcionan una estructura básica y pautas sobre cómo adaptarse a ellos, pero dejando un gran margen de flexibilidad. Funcionan de forma excelente como políticas aplicadas a escala en todas tus APIs. Algunos ejemplos de estos son:

- **HAL** (*Hypertext Application Language*): Para la estructura de los documentos JSON de tus APIs de hipermedia.
- **Problem Details** para APIs HTTP: Define la estructura de los archivos de error adhiriéndose a la restricción de hipermedia de las APIs REST.

> **Más información**  
> Para obtener más información, visita los siguientes enlaces:  
> - HAL: [https://stateless.group/hal_specification.html](https://stateless.group/hal_specification.html)  
> - Problem Details: [https://www.rfc-editor.org/rfc/rfc9457](https://www.rfc-editor.org/rfc/rfc9457)

Entonces, ¿cuándo seguir un determinado estándar o incluso múltiples estándares? Veámoslo a continuación.

##### Selección del estándar relevante

- Los **estándares singulares** son ideales si intentas abordar un problema bien conocido y deseas abrir tu negocio a socios u otros desarrolladores que esperan una estructura determinada para tu API. Este tipo de estándares ayuda enormemente a acelerar el proceso de diseño y a pasar directamente a la creación de prototipos y al desarrollo. Cualquier característica adicional se puede agregar más adelante mediante un proceso iterativo.
- Los **estándares globales** son excelentes si deseas ofrecer una experiencia uniforme en todas tus APIs. De manera similar, aunque en menor medida, también facilitan el proceso de diseño al añadir una restricción creativa al proceso y limitar el número de opciones que debes tomar. En el caso de estándares ampliamente adoptados, como *Problem Details*, esto también mejorará potencialmente el tiempo de integración y te dará acceso a herramientas de terceros.

Sin embargo, los estándares no siempre son el mejor camino a seguir. Los estándares globales que tienden a ser excesivamente restrictivos e intentan definir demasiados aspectos de tu API terminan limitando tu libertad creativa en lugar de facilitar el proceso de diseño y desarrollo, por lo que debes intentar evitarlos. Por otro lado, los estándares singulares de API que son muy vagos no aceleran realmente el proceso de diseño de tu API ni simplifican el proceso de integración, ya que la variabilidad de las APIs que se adhieren a ellos puede ser muy amplia.

#### Saber cuándo contenerse: Cuándo no crear una API

Este libro trata sobre cómo diseñar una API, lo sé. Sin embargo, un paso crucial en este proceso es saber cuándo **no** diseñar una. Ya hemos cubierto algunas de esas motivaciones en los pasos anteriores. En caso de que estemos duplicando la funcionalidad de una API existente, generalmente es mejor idea extender la API ya existente con los nuevos casos de negocio que necesitamos, a menos que los requisitos técnicos sean lo suficientemente estrictos como para restringir esta opción.

Otras razones importantes para no diseñar una API son:

- **Alto coste**: Si el coste de crear y mantener una API no aporta suficiente valor a la experiencia del usuario o a los ingresos, sería prudente reevaluar las motivaciones.
- **Gran aumento de la complejidad general del sistema**: Este punto es engañoso, ya que por lo general uno se da cuenta de ello demasiado tarde. Un buen indicador de esto es cuando tu sistema requiere múltiples llamadas internas y referencias a otras APIs, creando muchas dependencias o, peor aún, recursiones. Este es un problema común en servicios que se ejecutan sobre arquitecturas de microservicios o *serverless*, donde la coherencia general del sistema no se puede garantizar en ningún momento dado.
  > **Más información**  
  > Encuentra más información sobre consistencia eventual (*Eventual consistency*) aquí: [https://www.wikiwand.com/en/Eventual_consistency](https://www.wikiwand.com/en/Eventual_consistency)
- **Modas (*Trendiness*)**: El simple hecho de que las APIs estén de moda no significa que sean la solución adecuada para cada problema. Construir una API solo por seguir una tendencia puede acarrear una complejidad innecesaria. Esto también aplica a tecnologías o estilos específicos: solo porque alguna tecnología, como GraphQL, sea popular en un momento dado, no significa que sea una buena decisión crear una API utilizándola.
- **Sobreingeniería (*Overengineering*)**: Si tu software es simple y no está destinado a interactuar con otros sistemas, construir una API puede resultar excesivo.
- **Cumplimiento normativo (*Regulatory Compliance*)**: En ciertas industrias pueden existir regulaciones que restrinjan qué datos pueden exponerse a través de APIs. Es importante asegurarse de que cualquier API cumpla con todas las normativas pertinentes. Por ejemplo, exponer cualquier dato relacionado con la salud es sumamente delicado y requerirá un análisis profundo de qué se puede y qué no se puede compartir.
- **Monetización**: Si bien no es intrínsecamente malo monetizar una API, hacerlo sin proporcionar suficiente valor al usuario puede provocar una mala experiencia y un rechazo potencial. Cuando monetices los datos que posees a través de una API, asegúrate de que su calidad sea lo suficientemente alta y recuerda que esto no solo añadirá el esfuerzo requerido en documentación y demás, sino que también exigirá una solución de gestión de APIs más compleja.

Crear una nueva API suele ser una buena idea. Sin embargo, como hemos aprendido en esta sección, existen razones legítimas para no hacerlo. Repasar una lista corta como la anterior y verificar nuestro razonamiento y restricciones detrás de esta nueva API puede ahorrarnos dolores de cabeza en el futuro.

#### Abordar la proliferación descontrolada de APIs (*API Sprawl*)

El último problema que discutiremos en esta sección es el llamado **API Sprawl** (proliferación descontrolada de APIs). Es un fenómeno común en grandes organizaciones donde se crea un gran número de APIs con poco o ningún gobierno sobre ellas y sin seguir las mejores prácticas de diseño y gestión. Si una organización tiene problemas para hacer cualquiera de las siguientes cosas:

- Especificar qué APIs tiene en su ecosistema
- Saber cuántas APIs posee
- Saber dónde están desplegadas las APIs y cómo acceder a ellas
- Disponer de datos de monitorización en tiempo real sobre todas sus APIs
- Saber por qué fallan sus APIs

Entonces es muy probable que esté lidiando con *API Sprawl*.

Por tanto, el *API Sprawl* no es realmente el resultado de tener demasiadas APIs; es una deficiencia en el programa de gobierno de APIs. En caso de que tu organización esté luchando en cierta medida contra la proliferación de APIs y realmente necesite esa nueva API, esta también puede ser el heraldo del cambio que demuestre cómo iniciar un buen programa de gobierno para abordar los problemas existentes. Si el gobierno y la gestión se realizan correctamente, tener demasiadas APIs es un problema mucho mejor que tener muy pocas.

> **Más información**  
> Más información sobre API Sprawl aquí: [https://nordicapis.com/api-futures-api-sprawl-to-be-a-pressing-concern-in-2024/](https://nordicapis.com/api-futures-api-sprawl-to-be-a-pressing-concern-in-2024/)

Para reiterar: en la rara ocasión en que tu organización pueda estar luchando con la calidad de sus APIs, el problema no proviene realmente de la cantidad de APIs existentes en el ecosistema, sino más bien de la falta de control de calidad, observabilidad y gestión de políticas. El primer paso para solucionarlo es tomar conciencia de la magnitud del problema. Con ello, nuestra nueva API puede ser un faro de esperanza y la primera API en introducir nuevos estándares de gobierno de APIs. Superar el reto del gobierno de APIs se basa en los patrones de comunicación dentro de una organización. La siguiente sección explora en detalle cómo abordar el diseño de APIs centrado en tu audiencia y cómo aprovechar buenos patrones de comunicación para lograrlo.

---

### Identificación de la audiencia de tu API: Adaptando tu enfoque

En la sección anterior hemos hablado brevemente sobre la diferencia entre audiencia interna y externa. Ahora profundicemos en el tema de identificar el público objetivo de tu API y cómo esto afecta al diseño y a nuestras motivaciones.

Como ya hemos mencionado, las APIs internas y externas aportan muchas ventajas empresariales y tecnológicas: podremos reutilizar las interfaces de datos, dar mayor visibilidad a la información, añadir más fuentes de ingresos o monetizar nuestra plataforma. Ahora bien, ¿en qué se diferencia el enfoque del diseño de APIs para audiencias internas y externas?

#### Diseño de APIs centrado en la comunicación y la prestancia (*Affordance*)

Los requisitos con los que solemos empezar a construir nuestra nueva API habitualmente nos indican qué necesidades de negocio vamos a satisfacer y cómo deberíamos hacerlo. Sin embargo, rara vez son producto de una interacción cercana con el futuro consumidor. Una gran posibilidad que las APIs internas suelen ofrecer desde el principio es que ya conocemos quién va a ser nuestro consumidor: podemos trabajar con ellos desde el inicio para diseñar la solución óptima para sus necesidades.

Esto ayudará a crear una **API centrada en la prestancia (*affordance-centric API*)**. Esto significa una API cuyas operaciones corresponden lo más fielmente posible a las necesidades de tu consumidor. Este es el aspecto más importante para el diseño de APIs REST y lo que permite minimizar problemas potenciales como la **excesiva locuacidad (*chattiness*)**, el almacenamiento en caché, etc. Podrás crear los modelos de datos de tu API basados en los requerimientos del usuario y así evitar el envío de datos innecesarios o insuficientes, o exponer modelos de bases de datos o de implementación.

La comunicación cercana con los futuros consumidores también es crucial para descubrir limitaciones en aspectos no específicos del diseño, tales como rendimiento, seguridad o complejidad. Considera asimismo con qué sistemas o aplicaciones integrará tu audiencia la API, ya que esto puede influir en su diseño. Si es posible, realiza un ejercicio similar con los consumidores externos o socios: trabaja lo antes posible con quienes estén interesados en usar tus APIs y diseña en consecuencia. También puedes crear **arquetipos de usuario (*personas*)** para diferentes tipos de consumidores y establecer un proceso de diseño guiado por los requerimientos de cada arquetipo.

Considera igualmente qué tipo de sistemas utilizarán tus consumidores para integrar tu API. Por ejemplo, en epidemiología los investigadores comúnmente realizan análisis de datos sobre información presentada en formato de archivo `.csv`, por lo que podría tener sentido que tu API proporcione este tipo de contenido. Ciertos sistemas esperan que los datos se proporcionen en formatos específicos: por ejemplo, el formato de fecha es diferente en EE. UU. y en Europa, de igual manera que los números decimales; las unidades pueden proporcionarse en sistema métrico o imperial. Hay muchas consideraciones de este tipo y son realmente importantes para el éxito de tu API. Haz todo lo posible por satisfacer las necesidades de tus consumidores proporcionando los datos esperados.

> **Buenas prácticas**  
> Trabaja siempre con tu futuro consumidor. Si ya sabes quién es, acércate, conoce sus requisitos y comprende cómo y para qué desea utilizar tu API. Si no tienes esta posibilidad, crea arquetipos de usuario (*personas*) para representar las diferentes clases de consumidores y trabaja en el diseño de tu API adaptado a sus necesidades. Recuerda que tus consumidores, así como esos arquetipos, pueden evolucionar y evolucionarán con el tiempo a medida que ambos comprendan mejor la materia en cuestión. El proceso iterativo y la comunicación eficaz son cruciales para un buen diseño de API.

#### Más allá del diseño

También existen diferencias importantes entre las APIs internas y externas que van más allá del diseño puro de la API. Estas incluyen:

- **Seguridad**: Las APIs internas pueden residir dentro de una zona desmilitarizada (DMZ) estrictamente controlada y sin acceso externo, lo que limita enormemente la posibilidad de una brecha. En general, las APIs internas pueden utilizar mecanismos de autorización interna más sencillos; no obstante, sigues necesitando uno para gestionar los niveles de control de acceso, rastrear el uso de las diferentes APIs y sus operaciones, y obtener observabilidad sobre cualquier problema potencial que ocurra en ellas.
- **Control de acceso**: Las APIs externas requieren un control granular de quién tiene acceso a qué operaciones en tu API. Esto es especialmente importante en conjunción con estrategias adecuadas de limitación de tasa (*rate limiting*), donde restringirás el uso de tu API para diferentes tipos de usuarios.
- **Documentación**: Las APIs externas, al ser un producto expuesto a consumidores externos, requieren una excelente documentación para minimizar las confusiones sobre cómo integrarse y obtener el valor necesario de ella. Esto funciona de manera excelente en combinación con un mecanismo de aprovisionamiento de claves fácil de usar. Juntos, permiten reducir al mínimo el tiempo hasta la primera llamada (*time to first call*) a tu API y garantizan un proceso de integración sin fricciones. La mejor práctica es crear la documentación de tu API de la misma manera tanto para APIs internas como externas: piensa en tu API como un producto; tus consumidores, sin importar si son internos o externos, merecen una experiencia fantástica al usarla. Cuanto más fáciles de usar y autosuficientes sean tus consumidores, más sencillo será el mantenimiento de tu API y podrán aprovecharla al máximo.

> **Buenas prácticas**  
> Prepara la documentación, los canales de retroalimentación, las políticas de diseño, el control de acceso y la monitorización para las APIs internas de la misma manera que lo harías para las APIs externas. De este modo asegurarás estándares más altos y homogéneos para todas las APIs, una mejor experiencia de desarrollador (*Developer Experience*) y un proceso de incorporación (*onboarding*) superior, además de hacer mucho más fácil el proceso de externalización de tus APIs, ya que no requerirá un rediseño completo de la estrategia de gestión de APIs.

Como hemos podido observar, el enfoque centrado en la audiencia para diseñar y construir tu API es crucial para su éxito: reforzará tanto el valor de negocio de tu API como su eficiencia técnica. Participar en la comunicación con los consumidores desde las primeras etapas del ciclo de vida de la API también resolverá dudas sobre los mecanismos de seguridad que puedes o debes implementar o sobre cómo organizar tu documentación para aportar el mayor valor añadido. En la siguiente sección, exploraremos cómo las APIs impulsan el valor de tu negocio y habilitan la innovación.

---

### Las APIs como catalizadores del negocio: Impulsando el valor y la innovación

En este capítulo profundizamos en las motivaciones de negocio detrás de la creación de APIs, posiblemente el impulsor más significativo de todos. La industria comenzó a innovar verdaderamente cuando las empresas se dieron cuenta del potencial de las APIs para aumentar los ingresos y ampliar el alcance en el mercado. Aunque las tecnologías que habilitan las APIs han existido durante mucho tiempo, no fue hasta su implementación a gran escala que comenzamos a ver su verdadero potencial. Entonces, ¿qué constituye una motivación de negocio convincente? Mencionamos algunas en la primera sección de este capítulo: *El «Por qué» del desarrollo de APIs: Explorando las motivaciones fundamentales*. Exploremos esto con mayor detalle.

Si tu objetivo es externalizar tus capacidades y fomentar una economía alrededor de tus servicios y datos, las APIs ofrecen la libertad creativa para construir soluciones únicas adaptadas a las necesidades específicas de los usuarios, todo a través de conexiones de API sencillas. Facilitan el desarrollo de nuevas aplicaciones que de otro modo serían demasiado complejas o requerirían demasiado tiempo. Las APIs agilizan la integración entre sistemas intrincados, independientemente del lenguaje de programación y los marcos de trabajo (*frameworks*) empleados. Esto erradica los silos de datos, garantizando un acceso fácil a la información. En consecuencia, el mercado potencial de consumidores para tu API se amplía, ya que la barrera de entrada es relativamente baja.

#### Cómo las APIs generan innovación

En esta sección, repasaremos varios ejemplos de diferentes industrias sobre cómo las APIs ayudaron a generar innovación y mejorar productos:

- **Inteligencia Artificial**: Actualmente estamos experimentando un enorme aumento en la popularidad y las capacidades de los sistemas de IA. La IA se está incorporando en todas partes, en la mayoría de los servicios con los que tratamos. Este auge de la IA ha sido posible gracias a los avances en los modelos de lenguaje de gran tamaño (*LLMs*), pero también gracias a las APIs. Los sistemas de IA pueden obtener nuevos datos de manera eficiente y acceder a funcionalidades o interfaces externas precisamente debido a las APIs a las que tienen acceso. Podemos afirmar con seguridad que no existirían los sistemas modernos de IA tal como los conocemos si no existieran las APIs web. Es más, la IA puede aprovechar ciertas cualidades del diseño de APIs de manera más eficiente de lo que jamás fue posible. Las APIs de hipermedia, que son autodescubribles y autodocumentadas mediante el uso de hipervínculos dentro de sus modelos de datos, son una característica increíble para sistemas que pueden explorarlas sin la necesidad de una tediosa implementación de controles de hipermedia.
- **Industria automotriz**: En el sector automotriz, las APIs se utilizan para integrar datos de eficiencia, estadísticas de conducción, información cartográfica y mucho más. Este tipo de datos es especialmente crucial para el auge de la movilidad eléctrica. Las estaciones de carga, según el país, pueden no ser muy comunes en algunos lugares, y la capacidad de planificar tu ruta para tener la seguridad de no quedarte sin batería es clave. Para construir una solución de planificación de rutas, los fabricantes de automóviles tuvieron que integrar varias APIs: datos de mapas con estaciones de carga, distancias, inclinaciones y límites de velocidad para planificar el trayecto; datos meteorológicos para ajustarlo según la temperatura, el viento y la humedad. Tu coche también puede aprender tu estilo de conducción y ajustar estas predicciones en función de él. Todo eso proviene de varios servicios, tanto de los propios fabricantes como de terceros.
- **Comercio minorista (*Retail*)**: **Adidas** es un buen ejemplo de cómo aprovechar la Economía de las APIs en su beneficio. Lograron pasar de múltiples canales mayoristas y minoristas a una solución más enfocada y multiplataforma al integrarse con algunos de los grandes mercados en línea (*marketplaces*) y sus APIs. También utilizan una gran cantidad de APIs internas para rastrear la logística del proceso de fabricación y envío de prendas. Sus herramientas de diseño de indumentaria utilizan APIs para obtener datos sobre materiales y sus cualidades, colores, piezas, etc., de modo que los diseñadores puedan obtener fácilmente información sobre qué es factible y qué creará un buen producto. Esta es solo una instantánea de una parte de la economía de APIs de Adidas, pero ya demuestra cómo su adopción les permitió atravesar con éxito la transformación digital y ser mucho más ágiles en la forma en que se comparten los datos dentro de la organización y con sus socios.
- **Banca y Servicios Financieros (*Fintech*)**: En los últimos años, la banca, una industria tradicionalmente resistente a los cambios, ha estado experimentando una gran revolución. Con la adopción de la directiva europea PSD2, estamos presenciando el nacimiento del *Open Banking* (Banca Abierta), que a su vez revoluciona los negocios *fintech*. Al tener ahora los clientes de los bancos el derecho a acceder a sus datos de forma programática, las empresas *fintech* pueden aprovecharlos para ofrecer a las personas una gran cantidad de nuevos servicios. Con solo tener acceso a tus datos bancarios de gastos e ingresos, pueden realizar tareas como planificar presupuestos o sugerir estrategias de inversión. Combina estos datos con algunas fuentes externas y podrás crear aplicaciones aún más útiles que te ayuden a ahorrar dinero o a invertirlo adecuadamente.

#### Cómo un buen diseño de API impacta en la Economía de las APIs

Pero, ¿cómo puede un buen diseño de API impactar en la Economía de las APIs? Después de todo, este libro trata sobre el diseño de APIs y no propiamente sobre cómo los negocios pueden beneficiarse de ellas. Repasemos rápidamente algunos ejemplos de cómo un buen diseño de API ayuda a hacer crecer el negocio:

- **Usabilidad**: Un buen diseño hace que las APIs sean fáciles de entender y utilizar. Esto anima a más desarrolladores a utilizar la API, lo que conduce a más integraciones y a una base de usuarios más amplia.
- **Eficiencia**: Las APIs bien diseñadas pueden mejorar la eficiencia facilitando a los desarrolladores la integración con otros sistemas. Esto se traduce en una entrega más rápida de productos y mayor innovación.
- **Seguridad**: Un buen diseño de API también incluye medidas de seguridad sólidas, las cuales son cruciales para proteger datos sensibles y mantener la confianza de los usuarios.
- **Escalabilidad**: Las APIs diseñadas pensando en la escalabilidad pueden gestionar un gran volumen de peticiones, permitiendo a los negocios crecer sin preocuparse por el rendimiento de la API.
- **Interoperabilidad**: Una API bien diseñada puede funcionar sin problemas con otros sistemas, independientemente del lenguaje de programación o de la plataforma. Esta interoperabilidad fomenta mayores integraciones y colaboraciones.

Como podemos apreciar, el diseño de APIs es absolutamente crucial para el éxito de tu API. Sabemos muy bien lo importante que es la experiencia de usuario (*User Experience* / UX) en las aplicaciones de consumo. En el caso de las APIs, los consumidores son desarrolladores, arquitectos de software y otros perfiles técnicos. La experiencia de usuario en este caso se denomina **Experiencia de Desarrollador (*Developer Experience* / DX)** y describe la facilidad para integrarse con tu API, mantener dicha integración durante mucho tiempo y la capacidad de mejorarla y monitorizarla. 

El diseño de APIs, al igual que el diseño de productos clásico o el diseño de juegos en el caso de los videojuegos, es lo que habilita un bucle de retroalimentación positivo para los consumidores de APIs. Una API bien diseñada, que ofrezca interfaces de gran valor y con la que sea fácil trabajar, garantizará una larga vida útil para tu negocio. Ahora, recapitulemos lo aprendido en este capítulo.

---

### Resumen

En este capítulo hemos profundizado en las motivaciones fundamentales detrás de la creación de APIs. Una de las conclusiones clave es que las APIs se elaboran como productos para grupos de consumidores específicos. Los productos más eficaces surgen de una comunicación sólida entre los proveedores de la API (quienes las construyen y mantienen) y los consumidores de la API. Incluso al crear una API totalmente novedosa, resulta beneficioso interactuar con los usuarios potenciales para comprender sus necesidades y métodos de interacción.

Hemos analizado cómo las APIs internas pueden aumentar la eficiencia operativa y la seguridad, mientras que las APIs externas pueden generar ingresos y mejorar la calidad de la propia API. Ambos tipos de APIs desempeñan un papel importante en la economía de las APIs, ayudando a las empresas a aprovechar su lógica de negocio y datos únicos para nuevos usos, aportar valor a los consumidores de APIs, potenciar su ventaja competitiva y acelerar el tiempo de comercialización (*time-to-market*). La comunicación estrecha durante el proceso de diseño de la API es clave, independientemente de si tu API es para uso interno o externo. Aunque las motivaciones de negocio puedan diferir según sea interna o externa, los objetivos de calidad, facilidad de uso, mantenibilidad y observabilidad son comunes a todas las APIs.

También exploramos escenarios en los que podría ser más ventajoso actualizar una API existente en lugar de construir una nueva. Básicamente, si estás considerando crear una nueva API cuando ya existe una similar, vale la pena evaluar la diferencia de costes, tanto económicos como tecnológicos, entre construir y mantener una nueva solución frente a la actual. Considera el impacto en tus clientes actuales, si interrumpirá sus integraciones y si tu nueva solución satisface sus necesidades. Por último, analiza si tu organización está experimentando proliferación descontrolada de APIs (*API Sprawl*): tal vez tu nueva API pueda ser un paso hacia la resolución de la falta de un gobierno adecuado en torno a tus APIs.

Examinamos varios casos de estudio que demuestran que la creación de APIs es clave para hacer crecer digitalmente a tu organización, abrir más fuentes de ingresos y mejorar la eficiencia interna. La importancia de un buen diseño de API es ahora más crucial que nunca con el auge de los sistemas de Inteligencia Artificial basados en modelos de lenguaje de gran tamaño, que pueden aprovecharla en un grado aún mayor.

En el próximo capítulo, analizaremos el enfoque de **La API como Producto**. Mostraremos cómo esto representa un cambio de paradigma en la forma en que las organizaciones piensan sobre las APIs y el valor que entregan. Desglosaremos los bloques de construcción que hacen que este enfoque funcione en la práctica y exploraremos estrategias para la monetización de APIs, el empaquetado (*packaging*) y el papel del portal de APIs para habilitar la adopción. También continuaremos desarrollando nuestro pequeño proyecto de API y planificaremos su estrategia.
