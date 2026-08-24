# Parte 1: El Estudio del Aprendiz – Preparándose para el Oficio

## Capítulo 2: La API como Producto: Diseñando APIs con Mentalidad de Producto

Este capítulo analiza cómo abordar las APIs con una mentalidad de producto, centrándose en el valor que la API proporciona a sus consumidores. Se enfoca en tratar las APIs como productos en lugar de meros componentes técnicos. Enfatiza la importancia de diseñar APIs teniendo en cuenta los objetivos de negocio y la experiencia del desarrollador, creando experiencias gratificantes para los consumidores de la API. Cubre las mejores prácticas para diseñar una monetización eficaz de APIs, el empaquetado de APIs y un portal de APIs. Proporciona información sobre cómo estos principios pueden conducir a APIs más robustas, eficientes y fáciles de usar.

Al final del capítulo, conocerás los bloques de construcción de una estrategia de API como producto y comprenderás su mentalidad y los beneficios asociados. Podrás diseñar una monetización eficaz de APIs y empaquetar tu API. Finalmente, aprenderás el papel del portal de APIs y del responsable de producto de API (*API product owner*).

En este capítulo, vamos a cubrir los siguientes temas principales:

- **Cambio de paradigma – Las APIs como productos**
- **Los bloques de construcción de una API como producto**
- **Estrategias de monetización de APIs**
- **Empaquetado de APIs (*API packaging*)**
- **Portal de APIs (*API portal*)**

---

### Cambio de paradigma – Las APIs como productos

Históricamente, muchas organizaciones poseen cientos o miles de interfaces de integración punto a punto. Adidas, por ejemplo, cuenta con miles de interfaces punto a punto que respaldan sus operaciones internas y la integración con terceros. Mantener un panorama tan extenso de APIs heredadas (*legacy*) tiene un coste tremendo. Por ejemplo, Adidas vio la oportunidad de cambiar la forma en que gestionaban estas interfaces punto a punto. Decidieron transformar el tratamiento de las APIs para lograr la excelencia operativa, acelerar la integración con sus socios, crear nuevas fuentes de ingresos y abrir las puertas a la innovación.

También hemos experimentado una explosión en los modelos de consumo de software. Los usuarios han ido rápidamente más allá de las aplicaciones web basadas en navegadores y ahora utilizan productos en múltiples dispositivos y entornos.

Etsy, por ejemplo, reconoció la creciente tendencia de usuarios que acceden a sus servicios a través de diversas plataformas. Para garantizar una experiencia fluida, necesitaron adaptar su API en consecuencia:

> «Todo el código que se construyó para el sitio web tuvo que ser reconstruido en nuestra API para ser utilizado por las aplicaciones de iOS y Android».  
> — *Stephanie Schirmer, Etsy*

Más allá de los modelos tradicionales de consumo de APIs, también hemos presenciado el auge de clientes autónomos, especialmente con agentes de Inteligencia Artificial. Esta nueva tendencia empuja a los equipos de ingeniería de producto a rediseñar sus APIs y a considerarlas como ciudadanos de primera clase en lugar de simples componentes técnicos.

Por lo tanto, la **API como producto** es la intención de tratar a las APIs como productos de software. Es un cambio de mentalidad que influye en cómo ves las APIs:

- De activos técnicos tradicionales a **activos de negocio**
- De soluciones basadas en proyectos a **soluciones basadas en productos**
- De ser gestionadas por gestores de proyectos a ser gestionadas por **gestores de producto de APIs (*API product managers*)**
- De una documentación tardía (*afterthought*) a una **documentación basada en prototipos**
- De una integración compleja a una **integración sencilla en autoservicio (*self-service*)**
- De generar valor cero a **generar un valor único para los clientes**
- De frenar tu innovación a **desbloquear nuevas funcionalidades**
- De ralentizar la colaboración de tu equipo a **escalar la organización de tu producto**

El cambio hacia el tratamiento de las APIs como productos enfatiza la necesidad de un enfoque centrado en el consumidor, lo cual es crucial para su éxito. Esto nos lleva a la siguiente sección, donde profundizamos en los bloques de construcción de una API como producto, explorando los requisitos clave y las estrategias prácticas para garantizar que las APIs satisfagan las necesidades de los usuarios y aporten valor. Profundicemos en los requisitos principales y veamos cómo moldean tu API como producto.

---

### Los bloques de construcción de una API como producto

En la práctica, tratar una API como un producto implica varios requisitos clave para garantizar que satisfaga las necesidades de sus usuarios y entregue el valor adecuado. Veamos los requisitos principales.

#### Centralidad en el cliente (*Customer centricity*)

La centralidad en el consumidor se refiere a un enfoque de negocio que prioriza las necesidades y los casos de uso de tus clientes. Este principio implica hablar con tus clientes, comprender y anticipar sus requisitos y diseñar las APIs conjuntamente. Por ejemplo, **Stripe** tiene una sólida cultura centrada en el consumidor, ya que recopila las opiniones de los clientes utilizando diversas vías y tácticas para generar empatía con sus usuarios y comprender sus necesidades. Como táctica, Stripe realiza investigaciones estructuradas sobre la experiencia del usuario para responder a preguntas como: *«¿A qué desafíos se enfrentan los desarrolladores al utilizar nuestras APIs?»*. Graban a los desarrolladores intentando integrarse utilizando la API de Stripe para encontrar áreas de fricción e identificar puntos de dolor imprevistos.

Además de hablar con tus clientes, tienes la intención de diseñar tus APIs como productos empaquetados, resolviendo problemas no solo para uno, sino para muchos clientes y, en última instancia, para una audiencia de API.

Comprender la audiencia de tu API te permitirá adaptar el diseño, la documentación, el soporte y los esfuerzos de marketing de la API para satisfacer las necesidades y expectativas de cada perfil de usuario (*persona*), que pueden clasificarse en los siguientes segmentos:

- **Desarrolladores**: Tienen diferentes niveles de experiencia, desde principiantes hasta avanzados; necesitan documentación clara y fácil de usar, código de ejemplo, kits de desarrollo de software (SDK) y una experiencia de desarrollador sin fricciones. Para dirigirte a este segmento, debes centrarte en la experiencia del desarrollador, una incorporación rápida (*onboarding*) y un soporte técnico robusto para la API.
- **Gestores de producto (*Product Managers*)**: Tienen una buena comprensión de los aspectos técnicos y de negocio; necesitan funcionalidades directas, información detallada, casos de uso y saber qué puede ofrecer tu API. Para dirigirte a este segmento, debes demostrar cómo puedes resolver sus problemas de negocio y mejorar sus productos.
- **Propietarios de negocio (*Business Owners*)**: Son expertos en diseñar estrategias de negocio y tomar decisiones; necesitan una propuesta de valor clara, retorno de la inversión (ROI), casos de estudio y un modelo de precios fácil de entender. Para dirigirte a este segmento, debes mostrar beneficios comerciales, ahorros potenciales de costes y generación de ingresos.
- **Ingenieros de DevOps y seguridad**: Son expertos en gestionar infraestructura, plataformas y asegurarlas. Necesitan características de API fiables, escalables, seguras y que cumplan con la normativa. Para dirigirte a ellos, debes centrarte en el rendimiento de la API, el tiempo de actividad (*uptime*) y la seguridad de la API.
- **Ingenieros de soporte**: Son responsables de la gestión de la comunidad y del soporte de la API. Necesitan una excelente documentación, guías de resolución de problemas y una comunidad activa. Para dirigirte a ellos, debes proporcionar ayuda, errores de API autoexplicativos y guías detalladas de solución de problemas.

Un desafío habitual al hablar con los clientes es saber exactamente qué necesitan y decidir si resolver sus problemas o no. Por ejemplo, podrías ser conocido por ofrecer un producto de API de geocodificación y algunos clientes podrían pedir funciones de mapas. El desafío consiste en equilibrar lo que necesitas resolver, aquello en lo que eres bueno y lo que el cliente necesita.

Para conectar los conceptos de centralidad en el cliente y el enfoque en el diseño en las APIs, es importante enfatizar la importancia de alinear los principios de diseño con las necesidades del usuario. El enfoque en la centralidad en el consumidor subraya la necesidad de comprender y abordar los diversos requerimientos de los usuarios, sentando las bases para un diseño de API eficaz. Al priorizar la reutilización y la consistencia en el diseño de APIs, podemos garantizar que las APIs no solo sean fáciles de consumir, sino que también cumplan con las diversas expectativas de los diferentes perfiles de usuario. Exploremos cómo la reutilización y la consistencia en el diseño mejoran la experiencia global de la API.

#### Enfoque en el diseño

Las APIs como productos son fáciles de consumir porque son reutilizables y consistentes. Veamos cada uno de estos principios en detalle.

##### Reutilización (*Reusability*)

La reutilización de APIs es un principio de diseño en el que las APIs se desarrollan para ser utilizadas en diferentes aplicaciones o servicios sin requerir modificaciones significativas. Piensa en la reutilización como las piezas de **LEGO**. Estos bloques de construcción están estandarizados y encajan perfectamente entre sí, lo que te permite construir una gran variedad de estructuras. Por ejemplo, la API de Twilio es altamente modular, lo que permite a los desarrolladores agregar funciones de comunicación a aplicaciones web, dispositivos móviles y dispositivos IoT utilizando diferentes lenguajes. Esta reutilización la convierte en la API de referencia para diversas necesidades de comunicación.

*Figura 2.1: Lego (imagen de Unsplash)*

Además de la reutilización, los productos de API deben ser consistentes. Al igual que las piezas de Lego, que siguen dimensiones estándar y puntos de conexión precisos, esto las hace compatibles con otras piezas de LEGO.

##### Consistencia (*Consistency*)

La consistencia en las APIs aporta predictibilidad a la forma en que se consumen, las hace fáciles de usar y reduce la fricción de los desarrolladores. Este principio mejora la experiencia del desarrollador de muchas maneras: reduce la curva de aprendizaje y disminuye el tiempo de integración y los fallos.

A continuación, se presentan algunos ejemplos que destacan el impacto de la falta de consistencia, lo que genera dificultades para los desarrolladores:

- **Convenciones de nomenclatura inconsistentes**: Nombres de *endpoints* y parámetros de API inconsistentes. Por ejemplo, algunos *endpoints* o campos de carga útil (*payload*) utilizan `snake_case` mientras que otros usan `camelCase`. Esta práctica causa descontento en los desarrolladores, ya que aumenta la probabilidad de cometer errores en sus integraciones de API.
- **Cambios frecuentes en el formato de datos**: Por ejemplo, una API tiene diferentes campos o estructuras anidadas en distintas versiones sin una documentación adecuada de la estrategia de versionado. Estos cambios imprevistos rompen los clientes existentes que dependen de un formato de datos estable, lo que genera frustración y un aumento en los costes de mantenimiento.
- **Límites de tasa (*rate limits*) y regulación (*throttling*) impredecibles**: Los límites de tasa de la API o las reglas de regulación son inconsistentes o no se comunican. Por ejemplo, ocultar un límite de tasa por motivos de seguridad o cambiar instantáneamente un límite sin previo aviso. Las integraciones que dependen de tu API dejarán de funcionar repentinamente, por lo que los desarrolladores perderán la confianza en ti al no poder construir aplicaciones fiables.

Si bien un diseño eficaz garantiza que las APIs sean reutilizables y consistentes, contar con un **responsable de producto de API (*API product owner*)** dedicado es esencial para mantener este enfoque e impulsar la estrategia de la API hacia adelante. El API Product Owner asegura que se mantengan los principios de reutilización y consistencia, alineando el desarrollo de la API con los objetivos comerciales y las necesidades de los clientes. Profundicemos ahora en las responsabilidades y el impacto de un API Product Owner.

#### Responsable de producto de API (*API product owner*)

Muchas organizaciones adoptan estrategias de API como producto sin designar responsables de producto de API dedicados, lo que pone en riesgo el éxito y la sostenibilidad de sus iniciativas de API. Para comprender el papel crucial y el impacto de un API Product Owner, exploraremos sus responsabilidades clave y los riesgos de no contar con este perfil. A continuación, analizaremos cómo las organizaciones pueden construir y desarrollar las capacidades del API Product Owner.

##### El rol de un API Product Owner

Un API Product Owner es una figura fundamental responsable de dirigir la estrategia de API como producto. Se asegura de que las APIs se desarrollen, mantengan y evolucionen con un enfoque centrado en el producto en lugar de una metodología tradicional y puntual (*ad hoc*). Sus responsabilidades incluyen las siguientes:

- **Defensa y patrocinio (*Advocacy and sponsorship*)**: Los API Product Owners defienden la propuesta de valor de las APIs, asegurando el patrocinio y la financiación empresarial necesarios. Comunican la importancia estratégica de las APIs a las partes interesadas (*stakeholders*), asegurando la alineación y el apoyo en toda la organización.
- **Comprensión del cliente e iteración (*Customer insight and iteration*)**: Al comprender e interpretar las opiniones y patrones de uso de los clientes de la API, los API Product Owners impulsan la iteración y mejora continua de las APIs. Apoyan al negocio en el aprovechamiento del potencial de la API para maximizar los ingresos y satisfacer las necesidades cambiantes de los clientes.
- **Definición del mapa de ruta (*API roadmap*)**: A partir de la información de los clientes, los API Product Owners pueden definir y priorizar las funcionalidades de la API, gestionar el *backlog* del producto de API y asegurar la alineación y el compromiso de los equipos de ingeniería para entregar valor a los clientes.
- **Gestión del ciclo de vida (*Lifecycle management*)**: Los API Product Owners actúan como los principales usuarios del ciclo de vida de la API, abogando por su implementación efectiva. Aseguran que los procesos del ciclo de vida produzcan APIs valiosas, gestionan los paquetes de productos de API y utilizan soluciones de gestión de APIs para obtener información sobre el uso, la seguridad y el acceso.

En resumen, el API Product Owner es crucial para cerrar la brecha entre el desarrollo técnico y la estrategia comercial. Garantizan que las APIs no solo sean técnicamente sólidas, sino que también estén alineadas con las necesidades del mercado y los objetivos organizacionales. Al defender el valor de la API, impulsar mejoras centradas en el cliente, gestionar un mapa de ruta claro y estratégico y supervisar la gestión del ciclo de vida, los API Product Owners desempeñan un papel esencial en el éxito y la sostenibilidad de las iniciativas de API. Su participación ayuda a prevenir los riesgos asociados con los enfoques de desarrollo tradicionales y *ad hoc*, asegurando que las APIs entreguen el máximo valor tanto al negocio como a sus clientes.

##### Riesgos de no contar con un API Product Owner

Sin un API Product Owner, las organizaciones se enfrentan a varios desafíos, tales como:

- **Enfoques de desarrollo tradicionales**: Sin API Product Owners, tus APIs se construirán utilizando formas tradicionales de trabajo, lo que significa posponerlas o tratarlas como documentación trivial que potencialmente terminará desactualizada. Los enfoques de desarrollo tradicionales a menudo implican crear APIs de manera *ad hoc* sin una estrategia a largo plazo, lo que genera inconsistencia y deuda técnica. Estos métodos tratan a las APIs como proyectos puntuales con documentación mínima y poca interacción con el cliente, lo que da como resultado APIs obsoletas y difíciles de usar. Además, hay poca planificación proactiva o gestión del ciclo de vida, lo que hace que las APIs se queden atrás a la hora de satisfacer las necesidades cambiantes de los usuarios.
- **APIs en silos (*Siloed APIs*)**: Las APIs pueden permanecer aisladas dentro de los silos organizacionales, lo que dificulta obtener patrocinio y financiación empresarial. El valor y el potencial de las APIs a menudo se malinterpretan o se pasan por alto.
- **Pérdida de información sobre el cliente (*Missed Customer Insights*)**: La falta de una persona que recopile y analice la información de los clientes de la API resulta en oportunidades perdidas para la iteración y la mejora, lo que limita el potencial de ingresos y la satisfacción del cliente.

En resumen, la ausencia de un API Product Owner puede provocar un desarrollo fragmentado, esfuerzos aislados y la pérdida de oportunidades para aprovechar el conocimiento sobre los clientes. Esto no solo obstaculiza el valor potencial de las APIs, sino que también afecta a su usabilidad, mantenimiento y eficacia general para impulsar el éxito del negocio.

##### Desarrollo de capacidades de API Product Owner

Encontrar y contratar API Product Owners cualificados puede ser un desafío debido a la naturaleza especializada del rol. Sin embargo, las organizaciones también pueden desarrollar esta capacidad internamente. Esto implica identificar a empleados actuales que posean un sólido entendimiento tanto de los aspectos comerciales como técnicos del desarrollo de APIs y proporcionarles la formación y los recursos necesarios para realizar la transición al rol de API Product Owner.

Por ejemplo, como parte de su iniciativa de API como producto, **Adidas** formó con éxito a *Product Owners* existentes para convertirlos en *API Product Owners*. Este enfoque les permitió escalar sus APIs centrales de comercio electrónico y construir equipos internos de APIs eficaces. Al aprovechar el conocimiento y la experiencia de su personal actual, Adidas pudo fomentar una comprensión profunda de sus necesidades específicas de API y de sus objetivos organizacionales, algo que a las contrataciones externas podría llevarles más tiempo lograr.

Para desarrollar internamente las capacidades de API Product Owner, las organizaciones pueden seguir varios pasos:

- **Programas de formación en APIs**: Implementar programas de formación integrales que cubran las responsabilidades clave de un API Product Owner, incluida la estrategia de API, el conocimiento del cliente, la gestión del ciclo de vida y la comunicación con las partes interesadas. Esto puede incluir talleres, cursos en línea y tutorías impartidas por profesionales experimentados en APIs.
- **Colaboración multifuncional**: Fomentar la colaboración entre diferentes equipos, como desarrollo, marketing y soporte al cliente, para proporcionar una comprensión integral de cómo las APIs impactan en varios aspectos del negocio. Esto ayuda a los futuros API Product Owners a ver el panorama general y entender la importancia de su función.
- **Experiencia práctica**: Brindar oportunidades para que los futuros API Product Owners adquieran experiencia práctica involucrándolos en proyectos de API en curso. Esto puede incluir participar en los procesos de diseño, desarrollo e iteración, así como interactuar con los clientes y recopilar retroalimentación.
- **Mentoría y apoyo**: Emparejar a los aspirantes a API Product Owners con mentores experimentados que puedan brindar orientación, compartir mejores prácticas y ofrecer apoyo durante su transición a sus nuevos roles. Esto ayuda a generar confianza y garantiza una transición fluida.
- **Aprendizaje continuo**: Fomentar una cultura de aprendizaje continuo en la que se aliente a los empleados a mantenerse actualizados con las últimas tendencias, herramientas y mejores prácticas en el desarrollo y la gestión de APIs. Esto se puede lograr mediante sesiones periódicas de capacitación, asistencia a conferencias del sector y participación en redes profesionales relevantes.

Al invertir en el desarrollo de capacidades internas de API Product Owner, las organizaciones pueden garantizar un suministro constante de profesionales cualificados que estén profundamente familiarizados con sus necesidades y objetivos específicos. Esto no solo ayuda a escalar las iniciativas de API de manera efectiva, sino que también promueve una cultura de innovación y mejora continua dentro de la organización.

Como hemos visto, el rol de un API Product Owner es crucial para alinear las estrategias de API con los objetivos comerciales y garantizar la entrega de APIs valiosas y centradas en el usuario. Sin embargo, el éxito de las APIs como productos también depende en gran medida de la experiencia de los desarrolladores que las utilizan. Una **Experiencia de Desarrollador (*Developer Experience* / DX)** positiva es esencial para la adopción y la utilización efectiva de las APIs.

#### Experiencia de Desarrollador (*DX - Developer Experience*)

Para asegurar el éxito de tu estrategia de APIs, es crucial centrarse en la DX. Esta sección profundiza en la comprensión y mejora de cómo los desarrolladores interactúan y perciben tus APIs. Exploraremos los aspectos emocionales y psicológicos de los desarrolladores, el diseño de su recorrido (*journey*) y los pasos prácticos para mejorar sus interacciones con tu ecosistema de APIs. Al optimizar la DX, puedes fomentar emociones positivas y productividad, lo que conduce a una mayor adopción y satisfacción.

##### Comprensión de tu audiencia

La DX gira en torno a cómo los desarrolladores perciben e interactúan con tus APIs. Para optimizar esto, es esencial comprender sus emociones y qué desencadena sentimientos positivos como la fascinación y la satisfacción. Cuando los desarrolladores interactúan con tus APIs, se embarcan en un recorrido a través de tu entorno con el objetivo de lograr una meta o resultado específico. Este recorrido tiene dos facetas principales:

- **Compromiso con el desarrollo (*Development engagement*)**: Cómo los desarrolladores interactúan con tu entorno, como programas para desarrolladores y canales de soporte de la API.
- **Interacción con el sistema (*System interaction*)**: Cómo los desarrolladores interactúan con tu sistema para completar sus tareas, incluido el diseño de la API, la documentación, los SDKs y los tutoriales.

Cada interacción moldea la forma en que los desarrolladores perciben tu API. Tu objetivo es optimizar su recorrido, asegurando que lleguen a su destino de manera rápida y agradable. Las estrategias de API exitosas dependen del diseño de interacciones efectivas para los desarrolladores.

Además del compromiso y la interacción con el sistema, la **curva de aprendizaje** es una dimensión crítica. Optimizar para diferentes perfiles de desarrollador (principiante, intermedio y experto) es esencial para una DX integral:

- **Desarrolladores principiantes**: Estos usuarios se benefician de excelentes procesos de incorporación (*onboarding*) que los guían a través de sus primeras interacciones con la API. Optimizar el tiempo hasta el primer «Hola Mundo» (*first-time-to-hello-world*) garantiza que los principiantes puedan comprender y comenzar a usar la API rápidamente con la mínima fricción.
- **Desarrolladores intermedios**: Estos usuarios requieren documentación más profunda, ejemplos prácticos y tutoriales avanzados que les ayuden a integrar funcionalidades más complejas.
- **Desarrolladores expertos**: Si bien muchos productos de API destacan por atender a principiantes, a menudo se quedan cortos al proporcionar la flexibilidad que necesitan los expertos. Los expertos buscan materiales de referencia completos, opciones de personalización y la capacidad de realizar tareas sofisticadas. Es fundamental asegurarse de que tu API sea lo suficientemente flexible y robusta para gestionar los casos de uso de nivel experto.

Al comprender y optimizar los desencadenantes emocionales, los métodos de participación, las interacciones con el sistema y las curvas de aprendizaje para varios perfiles de desarrollador, puedes crear una DX convincente que impulse una mayor adopción y satisfacción. Cada punto de contacto en este recorrido debe diseñarse meticulosamente para reducir la fricción y mejorar la experiencia general. En la siguiente sección, profundizaremos en los detalles del diseño de la trayectoria del desarrollador.

##### Diseño de la trayectoria del desarrollador (*Designing your developer journey*)

Preparar la trayectoria del desarrollador para una API como producto es una tarea exigente: implica diferentes etapas. La naturaleza y el número de etapas pueden variar y estar estrechamente vinculadas con el segmento de audiencia al que te diriges; por ejemplo, tus desarrolladores internos experimentarán etapas diferentes a las de los desarrolladores externos.

Tomemos como ejemplo una API hipotética que acabas de lanzar; notarás que tienes al menos seis etapas:

| Etapa | Objetivo | Pasos | Métricas |
| :--- | :--- | :--- | :--- |
| **Conocimiento (*Awareness*)** | Dar a conocer a los desarrolladores las capacidades de tu API y sus beneficios mediante el lanzamiento de campañas de marketing *ad hoc*, participando en eventos para desarrolladores y publicando contenido que muestre lo que tu API puede hacer. | - Materiales de marketing<br>- Entradas de blog<br>- Redes sociales<br>- Presentaciones/webinars | - Número de visitas al sitio web<br>- Tasa de clics en anuncios (CTR)<br>- Número de menciones<br>- Asistencia a eventos/webinars |
| **Evaluación (*Evaluation*)** | Permitir a los desarrolladores probar tus APIs y asegurarse de que resuelven sus problemas proporcionando documentación completa y clara, ofreciendo código de ejemplo, mostrando casos de uso y manteniendo un soporte de API receptivo. | - Documentación de la API<br>- Código de ejemplo<br>- Guías de inicio rápido<br>- Foros de la comunidad, sección de preguntas frecuentes (FAQ)<br>- Soporte de la API | - Visitas a las páginas de documentación<br>- Número de descargas/ejecuciones de código de muestra<br>- Tiempo de permanencia en la página de documentación |
| **Incorporación (*Onboarding*)** | Reducir el tiempo que tardan los desarrolladores en obtener el primer valor de tu API optimizando el acceso a la API y la creación de cuentas, proporcionando una guía paso a paso para comenzar y ofreciendo consejos para problemas comunes. | - Acceso a la API<br>- Guía de primeros pasos<br>- Tutoriales prácticos<br>- Guía de solución de problemas | - Tiempo hasta el primer «Hola Mundo»<br>- Tasa de finalización de la configuración inicial<br>- Número de claves de API creadas<br>- *Net Promoter Score* (NPS) |
| **Adopción (*Adoption*)** | Reducir la fricción y generar confianza con tus desarrolladores asistiéndoles en su primera integración con guías detalladas, ofreciendo soporte técnico y haciendo que el soporte de tu API sea ágil. | - Documentación<br>- Entorno de pruebas (*Sandbox*)<br>- Depuración (*Debugging*)<br>- Gestión de errores<br>- Registro de cambios (*Changelog*) de la API<br>- Soporte de la API | - Uso activo de la API<br>- Número de aplicaciones cliente<br>- Tiempo necesario para que los usuarios solucionen errores<br>- NPS |
| **Retención (*Retention*)** | Mantener a los desarrolladores de la API comprometidos y conservar su confianza mejorando continuamente tu API en función de sus comentarios, manteniendo una comunicación activa y un soporte continuo de primer nivel. | - Registro de cambios (*Changelog*) de la API<br>- Boletín (*Newsletter*) de la API<br>- Foros de la comunidad<br>- Soporte de la API | - Tasa de abandono (*Churn rate*)<br>- Incidentes en la API<br>- Tasa de clics en el boletín<br>- NPS |
| **Prescripción / Defensa (*Advocacy*)** | Convertir a los desarrolladores de tu API en defensores de la misma, animándolos a compartir sus historias de éxito e interactuando con ellos a través de programas de reconocimiento y eventos. | - Envío de casos de estudio<br>- Programa de defensores (*Advocacy program*)<br>- Materiales para organización de eventos / *merchandising* | - Número de casos de estudio<br>- Tasa de participación en el programa de defensores<br>- Menciones en redes sociales |

*Tabla 2.1: Ejemplo de trayectoria del desarrollador*

Ahora que hemos cubierto los bloques de construcción de las APIs como producto, profundicemos en cómo monetizar tus productos de API.

---

### Estrategias de monetización de APIs

A medida que profundizamos en las estrategias de monetización de APIs, es crucial comprender cómo transformar tu API en un activo generador de ingresos puede impactar significativamente en tu negocio. Esta sección explora el concepto de monetización de APIs, varios modelos de monetización y los pasos para diseñar una estrategia eficaz. Al alinear el valor de tu API con el modelo de precios adecuado, puedes crear un flujo de ingresos sostenible y alcanzar tus objetivos comerciales.

#### ¿Qué es la monetización de APIs?

La monetización de APIs consiste en convertir tu API en un flujo rentable de ingresos directos o indirectos. Abarca todo el proceso de generación de estos ingresos, desde la definición del modelo de monetización hasta su mantenimiento a lo largo del tiempo. Estos ingresos se generan principalmente mediante el acceso a la API por parte de desarrolladores externos, socios y usuarios finales. Te pagan porque estás resolviendo un problema que tienen y para el cual no disponen del tiempo o la experiencia técnica necesaria.

Definir el modelo de monetización de tu API depende de varios factores, incluida la audiencia objetivo, el valor que aporta la API y tu modelo de negocio general. A continuación, se presentan varios modelos entre los que puedes elegir:

- **Gratuito (*Free*)**: Este modelo te ayuda a impulsar la adopción de tus APIs, construir tu marca y fomentar la innovación.
- **El desarrollador paga (*Developer pays*)**: Puedes cobrar a los desarrolladores utilizando varios modelos de precios:
  - **Freemium**: En este modelo, ofreces una versión limitada de tu API. Por ejemplo, OpenAI ofrece un nivel gratuito limitado para permitir a los usuarios experimentar con sus APIs y convertirlos en usuarios de pago. Esto incluye una cantidad limitada de *tokens* o un período de tiempo determinado para utilizar la API.
  - **Pago por uso (*Pay-as-you-go*)**: Los consumidores de la API pagan por consumo (por ejemplo, número de llamadas a la API o volumen de datos). Este modelo ofrece límites de uso más altos y servicios adicionales para los clientes de pago. Puede resultar atractivo para los usuarios que desean evitar costes iniciales y pagar solo por lo que utilizan. Por ejemplo, la API de WhatsApp Business de Twilio ofrece un modelo de pago por uso y cobra \$0.0042 por el envío de un mensaje de WhatsApp.
  - **Por niveles (*Tiered*)**: Defines diferentes niveles de uso (por ejemplo, básico, estándar, premium, empresarial, etc.) con diferentes estructuras de precios según los límites de llamadas a la API o los conjuntos de funciones. Los consumidores de la API pueden subir a niveles superiores a medida que aumenta su uso. Por ejemplo, la API de Mailgun ofrece planes Basic, Foundation y Scale; cada plan está limitado por la cantidad de correos electrónicos permitidos al día y un conjunto de características. Este modelo se puede combinar con el pago por uso para crear una estructura de precios híbrida que ofrezca flexibilidad y previsibilidad a los consumidores, quienes pueden elegir un nivel de suscripción que se ajuste a su uso habitual y luego pagar tarifas adicionales por el uso extra.
  - **Tarifa por transacción (*Transaction fee*)**: Implica cobrar a los consumidores de la API en función del número o valor de las transacciones procesadas a través de tu API. Cada vez que ocurre una transacción (por ejemplo, un pago o una solicitud de préstamo), se aplica una tarifa. Este modelo es particularmente común en la banca, el comercio electrónico o algunas APIs de procesamiento de datos, donde el valor de la API está vinculado a la transacción en sí y no a la cantidad de llamadas a la API. La API de Stripe es un buen ejemplo: cobran 1.5% + 0.25 € para tarjetas estándar del Espacio Económico Europeo.
  - **Basado en puntos (*Points-based*)**: También llamado basado en *tokens* o unidades, consiste en cobrar a los usuarios según el consumo de puntos o fichas que se utilizan para consumir la API o realizar ciertas operaciones. Cada tipo de llamada consume una cantidad predeterminada de puntos que los usuarios pueden comprar por adelantado. Este modelo es muy popular en APIs que realizan un procesamiento computacional pesado entre bastidores. Por ejemplo, OpenAI utiliza un modelo de precios basado en *tokens* para sus servicios, particularmente para sus modelos de lenguaje, donde cada modelo cuenta con diferentes capacidades y valoración en puntos de *tokens*.
- **El desarrollador cobra (*Developers get paid*)**: Los desarrolladores reciben pagos por aprovechar tus APIs web a través de varios modelos de precios:
  - **Reparto de ingresos (*Revenue share*)**: Te asocias con el consumidor de tu API que la utiliza para generar ingresos y compartes un porcentaje de las ganancias obtenidas, lo que incentiva a ambas partes a maximizar los ingresos. Este modelo es común en *marketplaces* o plataformas. Por ejemplo, Shopify proporciona APIs que permiten a los desarrolladores crear aplicaciones para su plataforma de comercio electrónico: los desarrolladores obtienen ingresos de sus aplicaciones y Shopify cobra una comisión fija.
  - **Afiliación (*Affiliate*)**: Tus socios incluyen el contenido o la publicidad de tu API para vender tus productos o servicios, y tú los compensas con una comisión. Amazon Associates API es un ejemplo de un programa de afiliados que permite a los usuarios ganar comisiones sobre las ventas.
  - **Recomendación / Referidos (*Referral*)**: Similar a la afiliación, pero tus socios ganan dinero solo si el usuario final realiza una compra.

La monetización de APIs no se trata solo de obtener ingresos directos, sino también de alcanzar objetivos comerciales. Aquí es donde los **modelos indirectos de monetización de APIs** pueden potenciar el crecimiento de tu negocio:

- **Sindicación y adquisición de contenidos**: Donde los editores o usuarios toman tu contenido y lo distribuyen a otras plataformas, editores o usuarios. Este modelo se utiliza habitualmente en el ámbito de los medios de comunicación (por ejemplo, la API de YouTube).
- **Clientes y socios B2B**: Donde te concentras en desarrollar tu negocio mediante alianzas estratégicas.
- **Usuarios internos**: Que utilizan tu API para desarrollar otras capacidades empresariales, mejorar el rendimiento de la entrega de software y fomentar una colaboración ágil entre equipos.

La monetización de APIs no solo genera ingresos, sino que impulsa los objetivos comerciales a través de modelos indirectos como la sindicación de contenidos, las asociaciones B2B y la mejora de las capacidades internas del negocio.

Ahora que hemos cubierto los diferentes modelos de monetización de APIs, veamos en detalle cómo elegir el adecuado.

#### Diseño de tu modelo de monetización

Diseñar un modelo de monetización eficaz requiere un conocimiento profundo de las necesidades de tus clientes, del valor que aporta tu API y una consideración minuciosa de los modelos de precios mencionados anteriormente. Los siguientes pasos describen cómo diseñar un modelo de monetización exitoso:

1. **Comprender a tus clientes y definir el valor**: Interactúa directamente con ellos, comprende sus necesidades, sus puntos de dolor y su disposición a pagar por el valor que proporcionas.
2. **Definir la propuesta de valor**: Define claramente qué capacidades ofrece tu API para resolver los problemas de tus clientes, identificando los beneficios de ahorro de costes y las mejoras de eficiencia.
3. **Elegir un modelo de monetización**: Selecciona el modelo que se alinee con el valor comercial de tu API y coincida con los conocimientos recopilados de tus clientes. Muchas empresas exitosas de APIs utilizan una combinación de diferentes modelos. Por ejemplo, puedes ofrecer un modelo *freemium* para atraer usuarios, precios por niveles para obtener ingresos predecibles y pago por uso para la escalabilidad.
4. **Iterar y mejorar tu modelo de monetización**: Basa las iteraciones en los datos recopilados, los comentarios de los clientes y los patrones de consumo de la API.

Aunque pueda resultar tentador crear un modelo de monetización complejo, **la simplicidad es clave**. Tus clientes deben comprender con rapidez y transparencia tanto el coste como el valor que obtienen de tu API. Considera también que los consumidores de tu API son principalmente desarrolladores que no necesariamente poseen una tarjeta de crédito corporativa; prepárate para adaptar tu modelo a esta realidad y afrontar cierto abuso de uso de la API, ya que algunos desarrolladores podrían tener la tentación de crear múltiples claves de API para consumirla. Finalmente, fomenta la confianza ofreciendo precios transparentes y calculadoras que les ayuden a estimar los costes según el uso previsto.

En resumen, la monetización de APIs es un proceso estratégico que consiste en convertir tu API en un activo generador de ingresos. Al elegir el modelo adecuado e iterar continuamente en función de las opiniones de los clientes, puedes crear un flujo de ingresos sostenible y alcanzar objetivos comerciales más amplios. La simplicidad, la transparencia y la comprensión de las necesidades de los clientes son fundamentales para diseñar una estrategia de monetización eficaz.

---

### Empaquetado de APIs (*API bundling*)

Mientras que los modelos de monetización determinan cómo una API genera ingresos, los **paquetes (*bundles*) y planes de APIs** organizan su estructura y accesibilidad agrupando APIs relacionadas y definiendo límites de uso, características y términos para diferentes segmentos de clientes. Como cualquier producto, las APIs deben empaquetarse cuidadosamente para los desarrolladores a través de un portal de APIs, donde los paquetes y planes ayudan a agilizar el acceso, clarificar el valor y satisfacer diversas necesidades de los clientes.

Por ejemplo, una empresa podría crear paquetes diferenciados para APIs de analítica, aprendizaje automático (*machine learning*) y almacenamiento de datos, cada uno con modelos de precios personalizados. El paquete de analítica podría utilizar un modelo por niveles para obtener ingresos constantes y predecibles, mientras que el paquete de aprendizaje automático podría adoptar un modelo de pago por uso para adaptarse a un consumo computacional de alta intensidad. Este enfoque de empaquetado permite estrategias de precios más flexibles y específicas, maximizando el valor tanto para el proveedor como para el consumidor.

#### ¿Qué es un paquete de APIs (*API bundle*)?

Un paquete de APIs se refiere a una colección de APIs agrupadas que proporcionan capacidades similares; ayudan a los usuarios a acceder a APIs relacionadas, reducen la complejidad y mejoran la experiencia del desarrollador. Para los proveedores de APIs, agilizan la gestión, el acceso y la seguridad. Por ejemplo, **Google Cloud Platform** ofrece varios paquetes de APIs orientados a diferentes funcionalidades, como aprendizaje automático, almacenamiento en la nube y análisis de datos; el paquete de **Google Maps** incluye las APIs de Maps, Routes y Places, cada una con su propio conjunto de funciones y precios.

La mayoría de las soluciones de gestión de APIs y portales de APIs facilitan la implementación y estructuración de tus APIs en paquetes y planes, asegurando una monetización eficiente.

#### ¿Qué es un plan de API (*API plan*)?

Un plan de API es una oferta que define los términos y condiciones bajo los cuales se consumirán tus APIs; en detalle, define los límites de uso, precios, características, niveles de soporte y Acuerdos de Nivel de Servicio (SLAs):

- **Límites de uso (*Usage limits*)**: Incluye límites de tasa (*rate limits*) y cuotas (*quotas*). Un límite de tasa es normalmente el número máximo de peticiones de API permitidas por unidad de tiempo (por ejemplo, segundos o minutos). Una cuota es el número total de peticiones de API dentro de un período de facturación (por ejemplo, diario o mensual).
- **Precios (*Pricing*)**: Puede ser uno de los modelos de precios analizados anteriormente en la sección *¿Qué es la monetización de APIs?*.
- **Acceso a funciones (*Feature access*)**: Diferentes planes pueden tener acceso a distintas características de la API; puedes restringir el acceso a funciones avanzadas para los niveles de precios más altos.
- **Nivel de soporte (*Support level*)**: Según el nivel de precios, el soporte puede variar; un nivel superior puede ofrecer soporte 24x7, tiempos de respuesta más rápidos y, en última instancia, un gestor de cuenta dedicado.
- **SLAs**: Abarca las garantías que puedes ofrecer a tus clientes con respecto al rendimiento y la fiabilidad de tus APIs.

Diseñar un plan de API integral garantiza que tus clientes comprendan qué están adquiriendo y qué pueden esperar de tu oferta. Al definir claramente estos elementos, puedes atender diferentes necesidades de los clientes y crear un enfoque estructurado para el consumo de la API.

En resumen, un plan de API es esencial para gestionar cómo se consumen tus APIs, brindando claridad sobre límites de uso, precios, características, niveles de soporte y SLAs. Este enfoque estructurado no solo te ayuda a satisfacer diversas necesidades, sino que también contribuye a mantener la calidad y la fiabilidad de tus servicios de API.

A continuación, exploraremos cómo implementar eficazmente paquetes y planes de APIs a través de un ejemplo.

#### Ejemplo – Empaquetado de APIs en Magic Cloud

Para ayudarte a comprender los conceptos de paquetes y planes de APIs, tomemos un ejemplo hipotético: **Magic Cloud** es un proveedor en la nube que ofrece diversos productos de API:

- Compute API
- AI and Machine Learning API
- Storage API
- Networking API
- IoT API

Podrían estructurar los paquetes y planes de API de la siguiente manera:

- **Paquete básico en la nube (*Basic cloud package*)**: APIs de Cómputo (VMs), Almacenamiento (almacenamiento de objetos) y Red (VPC).
- **Paquete avanzado en la nube (*Advanced cloud package*)**: APIs de Cómputo (VMs y orquestación de contenedores), Almacenamiento (almacenamiento de objetos y bloques), Base de datos (SQL) y Red (VPC y balanceo de carga).
- **Paquete de IA y analítica de datos (*AI and data analytics package*)**: APIs de IA y Aprendizaje Automático (reconocimiento de imágenes y PLN), Bases de datos (NoSQL, en memoria y vectorial) y Almacenamiento (almacenamiento de archivos).
- **Paquete de IoT (*IoT package*)**: APIs de IoT (gestión de dispositivos, ingesta de datos y computación en el borde), Red (CDN), Almacenamiento (almacenamiento de objetos) y Base de datos (SQL).

Cada paquete puede incluir uno o varios planes. Por ejemplo, el paquete **Basic Cloud API** incluye tres planes:

- **Nivel gratuito (*Free tier*)**:
  - **Límites de uso**: 1 VM, 10 GB de almacenamiento de objetos, VPC básica con ancho de banda limitado.
  - **Características**: Funciones básicas para pruebas y desarrollo.
  - **Soporte**: Comunidad.
  - **Precio**: Gratuito.
- **Plan estándar (*Standard plan*)**:
  - **Límites de uso**: 10 VMs, 100 GB de almacenamiento de objetos, VPC estándar con ancho de banda moderado.
  - **Características**: Acceso a la mayoría de los servicios con SLA estándar.
  - **Soporte**: Comunidad + soporte por correo electrónico.
  - **Precio**: \$49 al mes.
- **Plan premium (*Premium plan*)**:
  - **Límites de uso**: 50 VMs, 1 TB de almacenamiento de objetos, VPC básica con alto ancho de banda.
  - **Características**: Todas las funciones estándar además de funciones premium.
  - **Soporte**: Comunidad + soporte por correo electrónico.
  - **Precio**: \$149 al mes.

A continuación, veamos cómo se aplican los conceptos de paquete y plan de API en el mundo real según un caso de uso práctico.

#### Caso de uso real – SendGrid Email API de Twilio

La API de correo electrónico **SendGrid de Twilio** proporciona un ejemplo claro de cómo los paquetes y planes de APIs funcionan junto con un modelo de monetización para maximizar el valor tanto para el proveedor como para el consumidor. SendGrid ofrece un conjunto de planes por niveles —Free, Essentials, Pro y Premier—, cada uno diseñado con límites de uso específicos, conjuntos de funciones y precios adaptados a diferentes segmentos de usuarios y tamaños de empresa.

*Figura 2.2: Página de precios de Twilio Email API*

> **Consejo rápido**: ¿Necesitas ver una versión de alta resolución de esta imagen? Abre este libro en el lector Packt Reader de última generación o consúltalo en la copia en PDF/ePub.  
> El lector Packt Reader de última generación se incluye de forma gratuita con la compra de este libro. Escanea el código QR O ve a [https://packtpub.com/unlock](https://packtpub.com/unlock), luego utiliza la barra de búsqueda para encontrar este libro por su nombre. Verifica bien la edición mostrada para asegurarte de obtener la correcta.

A continuación, se detalla el desglose del ejemplo de la API de correo electrónico SendGrid de Twilio, especificando el modelo de monetización, paquetes y planes:

- **Modelo de monetización**:
  - **Modelo freemium y de precios por niveles**: Twilio utiliza un modelo *freemium* para atraer usuarios con un plan gratuito que les permite enviar hasta 100 correos electrónicos al día sin coste alguno. Este enfoque fomenta la adopción inicial y ofrece una vía para que los usuarios exploren las funciones básicas.
  - **Precios por niveles**: Más allá del plan gratuito, Twilio aplica un modelo de precios por niveles para los planes de pago, cada uno con funciones adicionales, mayores volúmenes de correo electrónico y distintos niveles de soporte para atender a diferentes necesidades y escalas.
- **Paquete (*Bundle*)**:
  - **Email API bundle**: El paquete SendGrid Email API abarca todos los servicios esenciales relacionados con el correo electrónico (como envío de correos, analítica y validación de correo electrónico) que los desarrolladores y las empresas necesitan para su comunicación por email. Este paquete está estructurado para proporcionar una variedad de servicios de correo electrónico dentro de un paquete cohesivo, adecuado para empresas de todos los tamaños.
- **Planes (*Plans*)**:
  - **Plan Free**: Proporciona acceso básico, permitiendo hasta 100 correos electrónicos por día con funciones limitadas.
  - **Plan Essentials (desde \$19.95/mes)**: Incluye acceso para enviar de 50.000 a 100.000 correos electrónicos al mes, ofreciendo funciones añadidas como *webhooks* adicionales y analíticas, pero sin IPs dedicadas.
  - **Plan Pro (desde \$89.95/mes)**: Admite hasta 2,5 millones de correos electrónicos al mes y agrega funciones premium como IPs dedicadas, administración de subusuarios y análisis avanzados.
  - **Plan Premier (precio personalizado)**: Para empresas de gran volumen, este plan personalizable ofrece análisis exhaustivos, IPs dedicadas, seguridad de alto nivel y hasta 1.000 miembros de equipo, con precios ajustados según el volumen y las necesidades corporativas específicas.

Esta estructura aprovecha un modelo de precios *freemium* y por niveles para realizar ventas adicionales (*upsell*) progresivas a los usuarios en función de sus necesidades de correo electrónico, con el paquete Email API proporcionando las funcionalidades esenciales en una variedad de planes orientados a diferentes segmentos de clientes y niveles de uso.

En resumen, los paquetes y planes de APIs son pasos cruciales para estructurar tus ofertas de API con el fin de satisfacer las diversas necesidades de los clientes, garantizando al mismo tiempo una gestión y monetización eficientes. Los paquetes y planes claramente definidos ayudan a optimizar el acceso, mejorar la experiencia del desarrollador y alinear el consumo de la API con los objetivos del negocio.

Ahora que sabes cómo estructurar tu oferta de APIs, veamos dónde exponerla utilizando un portal de APIs.

---

### Portal de APIs (*API portal*)

Un **portal de APIs** es un centro neurálgico (*hub*) que sirve de puente entre tú y los consumidores de tu API. Por lo general, es una interfaz web que aloja la documentación necesaria de la API, herramientas, un entorno de pruebas (*sandbox*) para interactuar con tu API, aprovisionamiento de acceso a la API y soporte técnico.

Un portal de APIs es fundamental para tu estrategia de API como producto. Hace que tus APIs sean fácilmente localizables al proporcionar un catálogo categorizado y con capacidad de búsqueda de las APIs disponibles, donde los usuarios pueden navegar a través de diferentes productos de API y comprender sus funcionalidades. Una vez que los usuarios encuentran la API que necesitan utilizar, les proporcionas una sección de documentación detallada y fácil de usar, para que puedan comprender rápidamente cómo funcionan tus APIs, probarlas mediante un *sandbox* o *playground*, y encontrar la documentación necesaria para resolver sus incidencias.

Los portales de APIs eficaces ofrecen los siguientes pilares:

- **Transparencia**: La transparencia es crucial, especialmente en lo relativo a los precios. El portal debe proporcionar información clara y detallada sobre los planes de precios, junto con un registro de cambios (*changelog*) de la API para comunicar cualquier posible cambio disruptivo (*breaking change*). Además, una página de estado (*status page*) que muestre el estado operativo de la API es esencial para mantener informados a los usuarios sobre cualquier incidente o mantenimiento programado.
- **Inclusividad**: Un portal de APIs debe atender a una amplia gama de perfiles de usuario, no solo a desarrolladores. Esto significa comprender y abordar las necesidades de los gestores de producto, las partes interesadas del negocio y otros usuarios no técnicos para garantizar que todos puedan comprender y utilizar tu oferta de APIs.
- **Habilitación de la colaboración**: Al actuar como un centro neurálgico, un portal de APIs eficaz debe facilitar la colaboración entre el proveedor de la API y sus usuarios. Debe proporcionar foros, herramientas de chat y canales de soporte para posibilitar una comunicación fluida y minimizar las frustraciones de los usuarios.

Decidir si **construir o comprar** tu portal de APIs implica sopesar diversas compensaciones:

- **Construir (*Build*)**: Ofrece los beneficios de una personalización y control totales, lo que te permite adaptar las funciones a tus necesidades específicas; sin embargo, conlleva mayores costes iniciales, tiempos de desarrollo más prolongados y requisitos de mantenimiento continuo. Por ejemplo, empresas como **Stripe** y **Twilio** construyeron sus propios portales para proporcionar una experiencia altamente personalizada a sus usuarios.
- **Comprar (*Buy*)**: Ofrece la ventaja de un despliegue más rápido, menores costes iniciales y soporte continuo. Muchos proveedores de gestión de APIs y plataformas de APIs incluyen portales de APIs integrados, lo que facilita que las organizaciones comiencen rápidamente. Sin embargo, estas opciones pueden ofrecer menor personalización, posible dependencia del proveedor (*vendor lock-in*) y costes recurrentes.

En resumen, un portal de APIs es un componente vital para gestionar y presentar eficazmente tus APIs a los consumidores. Al garantizar la transparencia, la inclusividad y habilitar la colaboración, un portal de APIs bien diseñado puede mejorar significativamente la experiencia del desarrollador e impulsar la adopción de la API. Ya sea que elijas construir o comprar, la decisión debe alinearse con tus necesidades específicas y objetivos estratégicos.

---

### Resumen

En este capítulo, has explorado el concepto de la mentalidad de **API como producto**, enfatizando la importancia de considerar a las APIs como valiosos activos de negocio en lugar de meros componentes técnicos. Has aprendido cómo pasar de soluciones tradicionales basadas en proyectos a un enfoque basado en productos puede potenciar los objetivos comerciales y mejorar la experiencia del desarrollador. Al tratar las APIs como productos, puedes crear interfaces más intuitivas y eficientes, entregando en última instancia un valor único a los clientes y fomentando la innovación.

Has obtenido conocimientos sobre la importancia de comprender las necesidades de los diferentes consumidores de APIs, incluidos desarrolladores, gestores de producto, propietarios de negocio e ingenieros de soporte. Este capítulo destacó el valor del diseño centrado en el consumidor, que implica interactuar con los clientes para recopilar información y codiseñar APIs que aborden sus requisitos. También aprendiste sobre la relevancia de la reutilización y la consistencia de las APIs, que pueden reducir la fricción de los desarrolladores y mejorar la experiencia general del usuario, de manera similar a cómo las piezas estandarizadas de LEGO encajan a la perfección.

Comprendiste los riesgos de no contar con un API Product Owner dedicado, tales como las APIs aisladas en silos y la pérdida de oportunidades de mejora. Además, se te proporcionaron pautas para desarrollar una capacidad eficaz de API Product Owner internamente, ya sea contratando o capacitando a los miembros actuales del equipo.

Finalmente, aprendiste sobre las estrategias de monetización y empaquetado de APIs. Se exploraron varios modelos de monetización, incluidos los modelos *freemium*, pago por uso y precios por niveles, enfatizando la necesidad de simplicidad y transparencia en los precios para generar confianza con los usuarios. Aprendiste el concepto de empaquetado de APIs, donde las APIs relacionadas se agrupan para mejorar la experiencia del usuario y optimizar la gestión. El capítulo concluye con el papel del portal de APIs, que sirve como un centro neurálgico para documentación, herramientas y soporte, asegurando que las APIs sean fácilmente localizables y accesibles para una amplia variedad de usuarios.

En el próximo capítulo, obtendremos una comprensión integral de cómo una visión holística de todo el ciclo de vida de la API influye en su diseño. Aprenderás sobre la interconexión entre el ciclo de vida de la API y el ciclo de vida de la aplicación, y cómo se impactan mutuamente a lo largo de sus diversas etapas.
