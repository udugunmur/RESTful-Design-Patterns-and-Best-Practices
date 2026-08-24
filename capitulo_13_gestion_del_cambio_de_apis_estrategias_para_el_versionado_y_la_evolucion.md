# Parte 3: El Círculo del Archimago – Forjando y Haciendo Evolucionar los Contratos de API

## Capítulo 13: Gestión del Cambio de APIs: Estrategias para el Versionado y la Evolución

Las APIs son sistemas vivos y dinámicos que deben evolucionar para satisfacer las demandas cambiantes de la tecnología, los objetivos comerciales y las expectativas de los usuarios. Gestionar estos cambios es tanto un arte como una ciencia. Una gestión eficaz del cambio de API garantiza que las nuevas funciones y actualizaciones mejoren la experiencia sin romper las integraciones existentes. Este capítulo profundiza en las estrategias para la gestión del cambio de APIs, centrándose en el versionado y la evolución mientras se equilibra la estabilidad y la innovación. Enfatiza la importancia crítica de preservar la compatibilidad hacia atrás y mantener una experiencia fluida para los consumidores existentes.

Cubriremos los siguientes temas principales en este capítulo:

- **El porqué de la gestión del cambio de APIs**
- **Bloques de construcción de la gestión del cambio de APIs**
- **Implementación de un proceso de cambio de API para Magic Items Store**

Al seguir este capítulo, obtendrás un conocimiento profundo sobre cómo gestionar los cambios de API sin interrumpir a los usuarios. Aprenderás a diferenciar entre las estrategias de versionado y evolución, a evaluar cuándo los cambios requieren un incremento de versión y a desarrollar un proceso estructurado para implementar estas estrategias. Podrás navegar por las complejidades de los enfoques de versionado, los principios de la evolución de APIs y los pasos prácticos para aplicarlos en un escenario del mundo real. Además, explorarás cómo empresas como Stripe y Adidas adoptan la evolución de APIs como estrategia para gestionar sus cambios.

Con estas habilidades, estarás bien preparado para actualizar tu API ante nuevos requisitos sin romper las implementaciones existentes.

---

### El porqué de la gestión del cambio de APIs

El cambio es una parte inevitable del desarrollo de APIs. Las APIs evolucionan por varias razones, incluida la necesidad de modernizar los sistemas heredados (*legacy*), introducir nuevas capacidades y reforzar las medidas de seguridad. La modernización ayuda a reducir la deuda técnica, mejorar la escalabilidad y adoptar nuevos patrones arquitectónicos que impulsan el rendimiento y la experiencia del desarrollador. Al mismo tiempo, añadir nuevas funciones permite que las APIs satisfagan las demandas cambiantes de los usuarios, sigan siendo competitivas y desbloqueen nuevas oportunidades de negocio. Garantizar la seguridad es igualmente crucial, ya que protege los datos confidenciales, mitiga vulnerabilidades y asegura el cumplimiento de los estándares de la industria. Equilibrar estas necesidades requiere una planificación cuidadosa, una comunicación efectiva y una estrategia bien definida para gestionar el impacto en los consumidores de la API.

#### Modernización de APIs

Los esfuerzos de modernización desempeñan un papel crucial en la gestión de la deuda técnica y garantizan que las APIs sigan siendo relevantes y escalables en el panorama digital actual. Con el tiempo, el código heredado y las tecnologías obsoletas pueden convertirse en una carga importante, limitando la escalabilidad, ralentizando los ciclos de desarrollo y aumentando los costes de mantenimiento. Informes de analistas, incluidos los de Gartner y Deloitte, destacan desde hace tiempo que los sistemas heredados pueden representar una parte significativa de la tecnología empresarial, y que los costes de mantenimiento absorben entre el 60% y el 80% de los presupuestos de TI. Esto restringe la innovación y agota recursos que podrían utilizarse mejor para crear nuevas funciones o mejorar la experiencia del usuario.

Refactorizar o rediseñar la arquitectura de las APIs no es solo un ejercicio técnico: es un movimiento estratégico para mejorar la fiabilidad, reducir el riesgo y modernizar las prácticas.

La transición de sistemas monolíticos a APIs modulares RESTful o GraphQL, por ejemplo, no solo aumenta el rendimiento sino que también incrementa la flexibilidad y la compatibilidad de los servicios. Las APIs más pequeñas y bien definidas son más fáciles de integrar para equipos y terceros, lo que reduce el acoplamiento y acelera el desarrollo. En migraciones a gran escala, esta flexibilidad reduce sistemáticamente la sobrecarga de integración y prepara a los sistemas para futuros requisitos.

La modernización de APIs también abre la puerta a arquitecturas nativas de la nube (*cloud-native*). Las APIs ligeras y sin estado (*stateless*) pueden escalar horizontalmente, manejar grandes volúmenes de datos y admitir cargas de trabajo en tiempo real con un retrabajo mínimo. No se trata solo de manejar la carga actual, sino de construir sistemas que sigan siendo resistentes y adaptables a medida que crecen las demandas.

Por supuesto, las APIs modulares introducen sus propios desafíos: la gestión de esquemas, el manejo de errores y el versionado de clientes entre ellos. Sin embargo, las ganancias a largo plazo en escalabilidad, fiabilidad y velocidad de integración a menudo superan la complejidad.

Las APIs modernizadas se diseñan teniendo en cuenta la preparación para el futuro, lo que permite a las organizaciones cumplir con los estándares de seguridad en evolución, como la adopción de protocolos de autenticación más sólidos y medidas de seguridad basadas en tokens. Además, facilitan una mejor interoperabilidad del sistema, facilitando que diversos sistemas y aplicaciones se conecten y compartan datos sin problemas. Esta integración mejora el rendimiento general, reduce la latencia y crea una experiencia de usuario más intuitiva.

Una estrategia exitosa de modernización de APIs no consiste solo en reemplazar tecnología antigua: se trata de transformar las APIs en soluciones escalables, seguras y de alto rendimiento que impulsen la innovación empresarial. Con el enfoque correcto, las organizaciones pueden reducir la deuda técnica, mejorar la productividad de los desarrolladores y adaptarse más rápidamente a las cambiantes demandas de los usuarios y las condiciones del mercado.

> **Buenas prácticas**  
> Una buena práctica clave en la modernización de APIs es realizar una evaluación exhaustiva de la API y adoptar un enfoque de modernización iterativo. La evaluación ayuda a identificar puntos críticos como cuellos de botella en el rendimiento, vulnerabilidades de seguridad y componentes obsoletos, proporcionando una hoja de ruta clara para la modernización. En lugar de renovar todo a la vez, un enfoque iterativo se centra en mejoras incrementales, comenzando con áreas de alto impacto. Esto reduce riesgos, minimiza la interrupción del servicio y permite la entrega continua de valor mientras alinea los esfuerzos de modernización con las prioridades del negocio.

#### Nuevas capacidades de API

Para seguir siendo competitivas en el mercado actual, las empresas deben introducir continuamente nuevas capacidades de API que se alineen con las necesidades cambiantes de los usuarios y las demandas de la industria. Las nuevas características no solo mejoran el valor de las APIs, sino que también permiten a las empresas expandir su oferta de servicios, mejorar las integraciones con plataformas de terceros y desbloquear nuevas fuentes de ingresos. Por ejemplo, Stripe evoluciona continuamente su API para introducir nuevos métodos de pago y capacidades de detección de fraude, mientras que la API de Slack agrega regularmente funciones como hilos de mensajes y automatización de flujos de trabajo, ampliando sus posibilidades de integración para los desarrolladores.

Sin embargo, equilibrar la innovación con la estabilidad es fundamental para evitar interrupciones. Los cambios de API mal gestionados pueden provocar la rotura de integraciones de clientes, mayores costes de soporte y una pérdida de confianza por parte de desarrolladores y socios. Un ejemplo notable son los cambios en la API de Facebook, que causaron una interrupción significativa cuando restringió el acceso a los datos de los usuarios tras el escándalo de Cambridge Analytica. Si bien el cambio era necesario para la protección de la privacidad, se implementó con previo aviso mínimo y alternativas inadecuadas para los desarrolladores, lo que provocó frustración y llevó a muchos a abandonar sus integraciones.

Otro caso es la repentina depreciación del acceso gratuito a la API de X/Twitter, que tomó a muchos desarrolladores por sorpresa y los obligó a ajustar o cerrar rápidamente sus aplicaciones. Estos incidentes resaltan la importancia de las estrategias de gestión del cambio de APIs, la compatibilidad hacia atrás y la comunicación proactiva para mantener la confianza del usuario durante la evolución de la API.

Un proceso de gestión del cambio de API bien estructurado garantiza que las empresas puedan introducir nuevas capacidades con confianza mientras preservan una relación sólida con su comunidad de desarrolladores. La documentación clara, el tiempo de anticipación adecuado para los cambios y la comunicación transparente ayudan a suavizar las transiciones y fomentar la confianza a largo plazo.

#### Actualizaciones de seguridad

Las actualizaciones de seguridad son esenciales para garantizar que las APIs sigan siendo resistentes a las amenazas emergentes y cumplan con los estándares de seguridad en evolución. Estas actualizaciones protegen datos confidenciales, resguardan los sistemas contra la explotación y mantienen la confianza del usuario en el ecosistema de la API.

Un excelente ejemplo es la transición de Stripe de la API v1 a la API v2, que introdujo modelos de autenticación más sólidos y una validación de solicitudes mejorada. Al implementar métodos de acceso más seguros y mejorar el manejo de la idempotencia, Stripe redujo el riesgo de acceso no autorizado y aseguró un procesamiento de solicitudes más confiable. Estos cambios reflejan el compromiso de Stripe de mantenerse a la vanguardia de los riesgos de seguridad en evolución mientras mantiene una experiencia fluida para los desarrolladores.

De manera similar, el enfoque de Twilio para proteger los webhooks y los archivos multimedia demuestra cómo las actualizaciones de seguridad pueden proteger datos confidenciales en servicios de comunicación en tiempo real. Twilio recomienda el uso de cifrado HTTPS y TLS para proteger las comunicaciones y evitar ataques *man-in-the-middle*. Para los archivos multimedia, como grabaciones de llamadas o imágenes enviadas a través de servicios de mensajería, Twilio admite la autenticación básica HTTP, lo que garantiza que solo los usuarios autorizados puedan acceder a este contenido. Twilio también proporciona validación de solicitudes mediante firmas HMAC-SHA1, lo que permite a los desarrolladores verificar que las solicitudes entrantes provienen genuinamente de Twilio y no de actores maliciosos.

Estos ejemplos resaltan la importancia de las actualizaciones de seguridad proactivas para proteger las APIs de posibles vulnerabilidades. Las auditorías periódicas, la adopción de protocolos de seguridad modernos como OAuth 2.0 y la validación de solicitudes ayudan a las organizaciones a mantener un entorno de API seguro. La combinación de estas prácticas con documentación clara y herramientas para desarrolladores garantiza una implementación fluida de las actualizaciones de seguridad sin interrumpir las integraciones de los usuarios.

---

### Bloques de construcción de la gestión del cambio de APIs

La gestión del cambio de APIs es un proceso estratégico que equilibra la necesidad de innovación con la importancia de la estabilidad y la fiabilidad. Evolucionar una API no es simplemente una necesidad técnica; requiere una planificación cuidadosa, comunicación y una estrategia de cambio bien definida que se alinee con los objetivos comerciales y las expectativas de los usuarios. Cada cambio (ya sea introducir nuevas funciones, mejorar el rendimiento o abordar la seguridad) debe evaluarse según su impacto potencial en los consumidores para garantizar una transición fluida.

#### Priorización estratégica y planificación

La gestión del cambio de APIs comienza con una estrategia clara y prioridades bien definidas. No todos los cambios de API son iguales: algunos son correcciones de seguridad urgentes, otros son optimizaciones de rendimiento y otros son mejoras de funciones impulsadas por el negocio. La planificación estratégica garantiza que los cambios se alineen tanto con la viabilidad técnica como con los objetivos comerciales, evitando interrupciones innecesarias y brindando el máximo valor. Una planificación exitosa implica la colaboración entre múltiples equipos, incluidos producto, ingeniería, seguridad y relaciones con desarrolladores (*DevRel*).

Uno de los aspectos críticos de la planificación es identificar el *porqué* detrás de cada cambio. Los cambios impulsados por objetivos comerciales pueden centrarse en ampliar las capacidades de la API para desbloquear nuevos mercados o satisfacer las cambiantes demandas de los clientes. Por ejemplo, una API de pagos podría necesitar admitir monedas adicionales o métodos de pago alternativos para ingresar a nuevas regiones. Por otro lado, las mejoras técnicas pueden apuntar a reducir la latencia, mejorar la escalabilidad o modernizar un componente heredado para reducir los costes de mantenimiento. Estas razones deben sopesarse y priorizarse en el contexto de los recursos disponibles y la deuda técnica.

La evaluación de riesgos desempeña un papel crucial en la planificación. Cada cambio introduce cierto nivel de riesgo, ya sea romper integraciones existentes, afectar el rendimiento o aumentar los costes de infraestructura. Al evaluar el impacto potencial de cada cambio, los equipos pueden decidir cuáles abordar primero y qué estrategias de mitigación implementar. Por ejemplo, implementar una nueva versión de una API puede requerir pruebas de rendimiento adicionales para garantizar que pueda manejar el tráfico esperado.

Una hoja de ruta (*roadmap*) es una herramienta esencial para la planificación estratégica. Proporciona un cronograma para los próximos cambios, ofreciendo visibilidad tanto a los equipos internos como a los desarrolladores externos sobre lo que vendrá a continuación. Esta hoja de ruta debe equilibrar las necesidades a corto plazo con los objetivos a largo plazo, garantizando que la API permanezca estable mientras evoluciona con el tiempo. También ayuda a gestionar las dependencias entre equipos, alineando los calendarios de lanzamiento y reduciendo las posibilidades de conflictos o retrasos.

#### Comunicación clara y compromiso con el desarrollador

La comunicación efectiva es la piedra angular del éxito en la gestión del cambio de APIs. Incluso el cambio mejor planificado puede resultar contraproducente si los desarrolladores son tomados por sorpresa. La comunicación debe ser oportuna, transparente y multicanal para llegar a todas las partes interesadas afectadas. No se trata solo de anunciar cambios, sino de explicar sus fundamentos, brindar orientación e interactuar con los desarrolladores durante todo el proceso.

Un componente clave de la comunicación es la notificación proactiva. Los proveedores de APIs deben notificar a los desarrolladores con mucha antelación sobre cualquier cambio significativo, especialmente en el caso de cambios que rompen la compatibilidad (*breaking changes*). Las notificaciones pueden adoptar diversas formas, incluidos registros de cambios (*changelogs*), actualizaciones por correo electrónico, publicaciones de blog y anuncios en el portal de desarrolladores. Por ejemplo, cuando GitHub introdujo nuevos límites de tasa (*rate limits*) para su API, comunicó el cambio con meses de anticipación a través de múltiples canales, asegurando que los desarrolladores tuvieran tiempo suficiente para adaptarse.

La documentación juega un papel crucial en la comunicación. Cada actualización de API debe ir acompañada de notas de la versión (*release notes*) detalladas, guías de migración y documentación de referencia actualizada. Estos recursos ayudan a los desarrolladores a comprender cómo ajustar sus integraciones y minimizan el riesgo de tiempo de inactividad. La documentación completa es especialmente crítica para cambios complejos, como aquellos que involucran autenticación o nuevos formatos de solicitud.

Otro aspecto del compromiso de los desarrolladores es el soporte comunitario. Proporcionar un entorno de pruebas (*sandbox*) o un programa de acceso temprano permite a los desarrolladores probar los cambios antes de que entren en producción. Ofrecer soporte directo a través de foros, canales de Slack o equipos dedicados de relaciones con desarrolladores también puede marcar una gran diferencia en la construcción de confianza y en garantizar transiciones fluidas.

#### Proceso de cambio de API

Un proceso de cambio de API eficaz comienza con una decisión estratégica: ¿deben gestionarse los cambios de su API mediante versionado, evolución continua o un enfoque híbrido? Cada estrategia tiene sus ventajas únicas, según el público objetivo de la API, su complejidad y la frecuencia con la que evoluciona. Seleccionar el enfoque adecuado ayuda a reducir la fricción y garantiza una experiencia fluida para los desarrolladores al tiempo que equilibra la innovación y la estabilidad.

El proceso de cambio de API se caracteriza inherentemente por compensaciones (*trade-offs*). Por ejemplo, al versionar una API, dos factores esenciales a considerar son el coste de la API y la calidad de la API:

- **Coste de la API**: Mantener múltiples versiones impone costes tanto a los proveedores como a los usuarios de la API. La actualización entre versiones puede requerir cambios significativos y algunos usuarios pueden tener dificultades para mantener el ritmo. Los proveedores se enfrentan al dilema de retirar versiones antiguas (lo que puede molestar a los usuarios) o mantenerlas indefinidamente, lo que aumenta la sobrecarga operativa.
- **Calidad de la API**: Una estrategia sólida de control de versiones facilita la mejora continua. Las nuevas versiones a menudo traen funcionalidades mejoradas, actualizaciones de seguridad y optimizaciones de rendimiento. Los usuarios que retrasan la actualización pueden perderse estos beneficios, pagando efectivamente un coste oculto por permanecer en una versión anterior.

Este acto de equilibrio allana el camino para identificar el proceso de cambio de API que mejor se alinea con sus requisitos.

#### Estrategia de versionado

El versionado es una estrategia fundamental en la gestión del cambio de APIs, que proporciona un marco estructurado para introducir cambios (especialmente los disruptivos o *breaking changes*) sin interrumpir a los consumidores existentes. Permite a los proveedores de APIs evolucionar sus ofertas manteniendo una experiencia estable y predecible para los desarrolladores. Cuando se realiza correctamente, el versionado garantiza que se puedan introducir nuevas características y mejoras con una fricción mínima, incluso mientras las versiones anteriores continúan sirviendo a integraciones a largo plazo.

Existen diferentes enfoques de control de versiones y seleccionar el correcto es esencial para el éxito de la API a largo plazo. Algunos proveedores adoptan el **versionado global**, donde toda la API se versiona de manera uniforme, a menudo a través de métodos basados en URI o encabezados. Este enfoque ofrece claridad y una ruta de actualización coherente para los consumidores, pero puede aumentar la complejidad operativa al administrar múltiples versiones activas. Por otro lado, el **versionado basado en recursos** permite que los recursos individuales evolucionen de forma independiente, ofreciendo más flexibilidad pero a costa de una mayor complejidad en la implementación y la gobernanza.

##### Versionado global de API

El versionado global de API asigna un único identificador de versión a toda la API, indicando qué conjunto principal de funcionalidades se entrega. Este enfoque es ideal cuando se introducen cambios importantes e incompatibles que requieren una demarcación clara entre versiones. Sin embargo, tiene compensaciones notables:

- **Versionado en URI**:  
  *Ejemplo*: `https://api.example.com/v1/products`  
  Aunque es explícito y claro, incrustar `v1` en la URL obliga a los consumidores a codificar rígidamente una versión específica. Este diseño dificulta las actualizaciones graduales porque la propia URL está vinculada a una versión particular.
- **Versionado por parámetro de consulta (*Query parameter*)**:  
  *Ejemplo*: `https://api.example.com/products?version=1`  
  Desacoplar el control de versiones de la estructura de la URL ofrece más flexibilidad. Sin embargo, puede complicar los mecanismos de almacenamiento en caché (*caching*) y requerir un análisis adicional en el lado del servidor.
- **Versionado basado en encabezados (*Header-based*)**:  
  *Ejemplo*: `Accept-Version: 1.0`  
  El uso de encabezados personalizados mantiene las URLs limpias y coherentes en todos los *endpoints*. La desventaja es que tanto los proveedores como los consumidores de APIs deben implementar un manejo de encabezados personalizado, y la información de versiones puede ser menos detectable para los nuevos usuarios.

> **Buenas prácticas**  
> El versionado global es eficaz para gestionar *breaking changes*, pero puede resultar costoso desde el punto de vista operativo a medida que la API evoluciona. Los proveedores deben equilibrar la necesidad de admitir versiones heredadas con los beneficios de implementar nuevas actualizaciones.  
> Una buena práctica fundamental es **evitar la inclusión de `v1` en las URLs base**. Cuando no se codifica rígidamente la versión en la URL base, el *endpoint* predeterminado siempre representa la última versión estable. Este enfoque fomenta un diseño en el que los consumidores interactúan con la versión más actual, segura y optimizada, reduce la deuda técnica al minimizar la fragmentación en la estructura de la API y simplifica la ruta de actualización, ya que los consumidores no necesitan cambiar su URL base con cada actualización de versión.

##### Versionado basado en recursos

El versionado basado en recursos permite que los *endpoints* o recursos individuales evolucionen de forma independiente en lugar de imponer una versión uniforme en toda la API. Este enfoque granular proporciona flexibilidad para actualizaciones incrementales:

- **Versionado basado en URI a nivel de recurso**:  
  *Ejemplo*: `https://api.example.com/products/v2`  
  En este modelo, solo se versiona el recurso específico (`products`). Otros recursos continúan operando en su versión actual hasta que se justifique una actualización.
- **Negociación de contenido (*Media type versioning*)**:  
  *Ejemplo utilizando tipos de medios personalizados*:
```http
Accept: application/vnd.example.products.v2+json
```
  Este método aprovecha las capacidades de negociación de contenido de HTTP. Mantiene la estructura de URL uniforme mientras permite al servidor determinar la versión adecuada del recurso según el encabezado `Accept`.

**Ventajas**:
- *Adopción incremental*: Los consumidores pueden actualizar recursos individuales según sea necesario, en lugar de cambiar toda la API.
- *Actualizaciones dirigidas*: Los cambios en un recurso no requieren modificaciones en otros, lo que reduce el riesgo de interrupciones generalizadas.

**Desafíos**:
- *Complejidad*: Gestionar diferentes versiones en varios recursos puede generar inconsistencias si no se coordina estrictamente.
- *Sobrecarga de documentación*: Es esencial contar con documentación detallada y específica de cada recurso para que los consumidores comprendan con qué versión de cada recurso interactúan.

El versionado no siempre es la respuesta para cada cambio de API. Muchos cambios (como mejoras de rendimiento o la adición de campos opcionales) pueden introducirse sin versionar si mantienen la compatibilidad hacia atrás. Sin embargo, los *breaking changes*, como alterar formatos de respuesta, modificar mecanismos de autenticación o eliminar campos, generalmente requieren una nueva versión. El desafío clave para los proveedores de APIs es distinguir entre estos tipos de cambios y aplicar el control de versiones con sensatez para evitar una fragmentación innecesaria.

> **Buenas prácticas**  
> Una estrategia de versionado sólida debe complementarse con una comunicación y una gobernanza claras. Los desarrolladores necesitan saber cuándo hay una nueva versión disponible, en qué se diferencia de la actual y cómo migrar sin problemas. Esto implica anuncios proactivos, documentación completa y políticas de depreciación bien estructuradas. Sin estos elementos, incluso la estrategia de control de versiones más cuidadosamente planificada puede generar confusión y frustración entre los consumidores.

#### Enfoque basado únicamente en la evolución (*Evolution-only approach*)

El enfoque de solo evolución para la gestión del cambio de APIs prioriza la mejora continua manteniendo la compatibilidad hacia atrás. En esta estrategia, las APIs evolucionan sin introducir nuevas versiones, lo que permite a los proveedores implementar mejoras de forma incremental. Al gestionar cuidadosamente los cambios no disruptivos, como agregar campos opcionales o mejorar los formatos de respuesta, el enfoque de solo evolución garantiza que las integraciones existentes permanezcan intactas y no se vean afectadas. Este enfoque es particularmente eficaz cuando la estabilidad y las actualizaciones fluidas son fundamentales para mantener la confianza del usuario.

Una de las principales ventajas del modelo de solo evolución es su capacidad para evitar la fragmentación. Todos los consumidores permanecen en la misma versión de la API, lo que simplifica el soporte y el mantenimiento y reduce la necesidad de una infraestructura compleja de versionado. Dado que no se crean nuevas versiones, los proveedores pueden concentrarse en mejorar la API actual sin administrar múltiples versiones activas. Sin embargo, esta simplicidad conlleva la responsabilidad añadida de prevenir rigurosamente los cambios disruptivos accidentales, que pueden tener consecuencias importantes para los consumidores.

Para que las APIs basadas únicamente en la evolución tengan éxito, se debe seguir un conjunto de **reglas estrictas de extensión** para mantener la compatibilidad:
- Ningún campo ni funcionalidad debe ser eliminado.
- Ninguna regla de procesamiento existente debe ser alterada.
- Cualquier característica nueva introducida debe ser opcional.

Esta disciplina minimiza el riesgo de romper a los clientes existentes y mantiene manejable la superficie de la API a lo largo del tiempo. También exige que los clientes adopten una implementación flexible y tolerante, ignorando campos desconocidos y manejando datos inesperados de manera elegante, lo que a menudo se conoce como la **Ley de Postel**.

> **Nota: Ley de Postel**  
> La Ley de Postel, también conocida como el *principio de robustez*, es una guía de diseño para sistemas informáticos, particularmente en protocolos de red. Aconseja que el software debe ser **conservador en lo que envía** (la salida debe adherirse estrictamente a los estándares y especificaciones relevantes) y **liberal en lo que acepta** (la entrada puede ser más flexible, permitiendo a los sistemas procesar datos incluso si se desvían ligeramente del estándar estricto).  
> Articulado originalmente por Jon Postel, este principio ha sido fundamental en el desarrollo de Internet, ayudando a garantizar la interoperabilidad entre diversos sistemas mientras mantiene una comunicación sólida.

Cuando un *breaking change* es inevitable, la estrategia de solo evolución requiere **crear una nueva variante de recurso** en lugar de alterar el recurso existente. Esto preserva la compatibilidad hacia atrás mientras ofrece nueva funcionalidad. Por ejemplo, si un parámetro de consulta opcional debe volverse obligatorio, el nuevo recurso podría tener un URI diferente (`/new-resource`) mientras que el recurso antiguo permanece disponible. Esto garantiza que los clientes existentes puedan continuar utilizando el recurso original sin interrupción mientras que los nuevos clientes adoptan la variante actualizada.

En el modelo de solo evolución, la depreciación (*deprecation*) y el retiro definitivo (*sunsetting*) son componentes críticos para administrar las variantes de recursos a lo largo del tiempo. Las variantes obsoletas deben marcarse claramente en la documentación y en tiempo de ejecución, con suficiente aviso y orientación para que los consumidores migren. El monitoreo regular de los recursos obsoletos garantiza una transición sin problemas antes de que finalmente se eliminen.

#### Modelo híbrido (combinación de versionado y evolución)

El modelo híbrido es una de las estrategias más flexibles en la gestión del cambio de APIs. Combina la evolución continua para cambios compatibles hacia atrás con el control de versiones para cambios disruptivos (*breaking changes*), ofreciendo lo mejor de ambos mundos. Este enfoque permite que las APIs evolucionen a un ritmo rápido mientras mantienen un proceso estructurado para manejar actualizaciones significativas que pueden interrumpir las integraciones existentes.

En un modelo híbrido:
- Los cambios compatibles hacia atrás (como añadir campos opcionales, ampliar las respuestas o mejorar el rendimiento) se introducen dentro de la versión existente. Estas mejoras incrementales permiten a los desarrolladores adoptar cambios sin requerir acciones inmediatas ni arriesgar interrupciones del servicio. La evolución continua mantiene la API actualizada y adaptable, satisfaciendo las demandas de los usuarios sin la sobrecarga de administrar múltiples versiones.
- Cuando un *breaking change* se vuelve necesario (como eliminar campos, modificar mecanismos de autenticación o alterar formatos de respuesta), se introduce una nueva versión. Esto proporciona a los desarrolladores una ruta de migración clara y tiempo suficiente para ajustar sus integraciones. Al proporcionar una comunicación transparente y guías de migración detalladas, los proveedores de APIs pueden minimizar la fricción y mantener la confianza de los desarrolladores durante estas transiciones.

Un componente esencial del modelo híbrido es la estrategia de depreciación y retiro definitivo (*sunsetting*). Cuando se lanza una nueva versión, la versión anterior debe eliminarse gradualmente con cuidado. Las políticas claras de depreciación garantizan que los desarrolladores sepan cuánto tiempo se admitirá la versión anterior y les brindan las herramientas y el tiempo necesarios para migrar.

#### Caso de uso: Proceso de gestión del cambio de la API de Stripe

El proceso de lanzamiento de la API de Stripe es un referente de planificación eficaz y gestión estratégica del cambio. A lo largo de los años, Stripe ha mejorado continuamente su API para cumplir con los estándares de pago globales en evolución, manteniendo la compatibilidad con versiones anteriores y minimizando las interrupciones para su vasto ecosistema de desarrolladores. La reciente introducción de una cadencia de lanzamiento predecible y un sistema de control de versiones demuestra aún más el enfoque reflexivo de Stripe hacia la evolución de la API.

Bajo el nuevo modelo, Stripe combina lanzamientos semestrales importantes (*major releases*) con actualizaciones mensuales de funciones (*monthly feature updates*), logrando un equilibrio entre estabilidad e innovación:
- Cada lanzamiento principal incluye cambios disruptivos y recibe deliberadamente el nombre de una planta (por ejemplo, *Acacia*), lo que refleja la idea de que las APIs son sistemas en crecimiento que deben cuidarse y mantenerse con esmero.
- Los lanzamientos mensuales, por el contrario, son compatibles con versiones anteriores y permiten una adopción segura de nuevas funciones sin requerir que los desarrolladores revisen sus integraciones.

El lanzamiento *Acacia*, la primera versión de la API bajo este nuevo proceso, ejemplifica el enfoque de Stripe en la previsibilidad. Los desarrolladores ahora pueden planificar sus ciclos de ingeniería de manera más efectiva, sabiendo cuándo esperar cambios importantes y cuánto tiempo tienen para implementarlos. El proceso de lanzamiento está estrechamente integrado con los SDKs de Stripe para cada lenguaje compatible, lo que garantiza que las versiones del SDK permanezcan directamente asociadas con las versiones de la API. Esto elimina confusiones y simplifica la gestión de dependencias para los equipos de desarrollo.

Otro pilar del éxito de Stripe es su rediseñado registro de cambios (*changelog*) para desarrolladores. A diferencia de los registros de cambios tradicionales que enumeran todas las actualizaciones, el nuevo changelog de Stripe ayuda a los desarrolladores a comprender qué cambios se aplican a su versión específica de la API. Ofrece orientación de actualización paso a paso, resúmenes detallados de las actualizaciones de la plataforma y opciones de filtrado para centrarse en los cambios relevantes.

#### Depreciación (*Deprecation*) y Retiro definitivo (*Sunsetting*)

La depreciación y el retiro definitivo son fases indispensables del ciclo de vida de la API, lo que garantiza que las APIs evolucionen de forma sostenible sin sacrificar la confianza del usuario ni la estabilidad del sistema. Si bien el cambio es inevitable, forzar transiciones abruptas corre el riesgo de alienar a los desarrolladores e interrumpir las operaciones comerciales. Una estrategia bien orquestada de depreciación y retiro definitivo equilibra la necesidad de progreso con el deber de diligencia debido a los consumidores existentes.

En un nivel alto:
- **Depreciación (*Deprecation*)**: Señala que una función o versión de la API está entrando en su fase de final de vida útil (*end-of-life*), lo que brinda a los desarrolladores amplio tiempo y orientación para migrar.
- **Retiro definitivo (*Sunsetting*)**: Marca la eliminación irreversible de la funcionalidad en desuso.

Ambos requieren un diseño cuidadoso: no solo ajustes técnicos, sino comunicación reflexiva, monitoreo y soporte de migración. Sin una política de depreciación deliberada, las APIs se calcifican (paralizadas por el miedo a los *breaking changes*) o decaen (fragmentadas con versiones heredadas a medio mantener).

##### Marcar la característica o recurso como obsoleto (*Deprecated*)

El primer paso crítico en el proceso de depreciación y retiro definitivo es anunciar formalmente el comienzo del viaje de final de vida útil para un recurso, característica o versión. En esta etapa, la depreciación ya no es una decisión técnica interna: se convierte en una señal pública y contractual para sus desarrolladores y su ecosistema.

> **Un principio rector**  
> Si un cliente aún puede descubrir o integrarse con una característica obsoleta sin una advertencia clara, el proceso de depreciación ha fallado.

Para evitar esto, la señalización de depreciación debe ocurrir en dos superficies esenciales:
1. **En tiempo de ejecución (*runtime*)**, para la detección automatizada por parte de sistemas, herramientas e infraestructura de monitoreo.
2. **En la documentación**, para desarrolladores humanos que buscan comprensión, orientación y los siguientes pasos.

###### Señalización en tiempo de ejecución (*Runtime*)

A nivel de protocolo, las APIs deben incrustar señales legibles por máquina que indiquen que un recurso o característica está en desuso y programado para su eliminación:

- **Encabezado HTTP `Sunset`**: Agregue un encabezado `Sunset` a todas las respuestas del recurso obsoleto. Este encabezado especifica la fecha prevista de apagado, proporcionando a los clientes una fecha límite concreta y predecible para actuar:
```http
Sunset: Wed, 30 Sep 2025 23:59:59 GMT
```
  Los clientes que monitorean las respuestas de la API pueden mostrar estos encabezados en sus herramientas de observabilidad o canalizaciones de CI, lo que desencadena esfuerzos de migración proactivos ([RFC 8594](https://datatracker.ietf.org/doc/html/rfc8594)).
- **Encabezado HTTP `Deprecation`**: Además de especificar una fecha de puesta de sol, considere incluir un encabezado `Deprecation` marcado simplemente como `true`:
```http
Deprecation: true
```
- **Encabezado `Link` hacia la guía de migración**: Utilice un encabezado `Link` con un tipo de relación `rel="migration-guide"` o `rel="deprecation-guide"`, que apunte a la documentación de migración o las instrucciones de actualización:
```http
Link: <https://developer.example.com/migrate-api-v2>; rel="migration-guide"
```

> **Buenas prácticas**  
> Utilice los tres encabezados combinados (`Sunset`, `Deprecation` y `Link`) para lograr la máxima claridad y accesibilidad mecánica, y trate los encabezados de depreciación en tiempo de ejecución como parte de su contrato de API durante el período de migración.

###### Señalización en la documentación

- **Etiquetas claras de depreciación**: Todo recurso, método, campo u operación obsoleto debe estar etiquetado de manera destacada como *Deprecated* con insignias visuales, advertencias de color o carteles publicitarios (*banners*).
- **Notas de depreciación detalladas**: Explicación del motivo, enlace directo a la alternativa recomendada y fecha prevista de retiro.
- **Anotaciones en SDKs y bibliotecas de cliente**: Marque métodos o clases obsoletos con anotaciones estándar de cada lenguaje (por ejemplo, etiquetas `@deprecated` en Java, Python o TypeScript) para advertir en IDEs y *linters*.
- **Notas de lanzamiento y registros de cambios (*Release notes* & *Changelogs*)**.

> **Buenas prácticas**  
> La documentación no debe limitarse a mencionar la depreciación: debe guiar la acción. Cada característica obsoleta debe responder a tres preguntas para los desarrolladores:  
> 1. *¿Qué está pasando?*  
> 2. *¿Por qué está pasando?*  
> 3. *¿Qué debo hacer en su lugar?*

###### Depreciar la unidad viable más reducida (*Narrowest viable unit*)

Una disciplina crítica en la depreciación es delimitar el alcance de las depreciaciones de la forma más estricta posible:
- Si solo se elimina o reemplaza un campo específico en una carga útil, marque solo ese campo como obsoleto, no todo el recurso.
- Si solo un parámetro de consulta u operación en particular está obsoleto, deprecie solo esa parte específica.

Las depreciaciones demasiado amplias provocan migraciones innecesarias, inflan la carga de trabajo de los desarrolladores y generan escepticismo sobre futuros avisos de depreciación.

##### Informar y educar a los consumidores

La comunicación efectiva durante la depreciación debe ser multicanal, empática y orientada a la acción. Con demasiada frecuencia, los equipos de API subestiman la necesidad de una divulgación activa, asumiendo que los desarrolladores revisarán periódicamente los registros de cambios. En realidad, la mayoría de las integraciones son «fuera de la vista, fuera de la mente»: los desarrolladores se integran una vez y rara vez vuelven a visitar el código a menos que se les solicite.

Los cuatro resultados que debe lograr la comunicación de depreciación son:
1. Los desarrolladores son conscientes del cambio.
2. Los desarrolladores comprenden los motivos y las implicaciones.
3. Los desarrolladores conocen la ruta de migración.
4. Los desarrolladores se sienten respaldados durante la transición.

- **Notificación proactiva a través de múltiples canales**: Correos electrónicos dirigidos, anuncios en el portal de desarrolladores, notificaciones dentro del producto, advertencias en SDK/CLI, participación en la comunidad y notas de la versión.
- **Guía de migración accionable**: Ruta de migración, diferencias de comportamiento, ejemplos de código comparativos (antes/después) y casos extremos.
- **Personalización para consumidores de alto impacto**: Identifique los principales consumidores mediante análisis de API y asigne administradores de cuentas (*account managers*) o defensores de desarrolladores (*developer advocates*) para comunicarse directamente con ellos.
- **Canales de soporte y redes de seguridad**: Canales de Slack dedicados, colas prioritarias de tickets y horas de oficina (*office hours*) con el equipo de ingeniería.

> **El tono de las comunicaciones de depreciación**  
> El tono debe ser empático, claro y de apoyo, no conflictivo ni defensivo. El mensaje no es «Debes migrar o te atienes a las consecuencias», sino «Estamos evolucionando la plataforma para servirte mejor. He aquí cómo te ayudaremos a tener éxito».

###### Ejemplo práctico: Migración de SDKs y APIs en Apideck

En 2025, Apideck llevó a cabo la renovación de sus SDKs de API Unificada, pasando de SDKs generados automáticamente a una nueva generación impulsada por Speakeasy. Apideck abordó la comunicación con una estrategia integral:
1. **Enmarcar el cambio a través del valor**: Destacar mejoras tangibles en ergonomía, nombres de métodos, paginación y seguridad de tipos en lugar de centrarse únicamente en la depreciación técnica ([Blog de Apideck](https://www.apideck.com/blog/redefining-our-sdks-developer-experience)).
2. **Proporcionar rutas de migración detalladas**: Guías de migración paso a paso para Node.js, Python, PHP y .NET ([Guías de Apideck](https://developers.apideck.com/guides/sdk-migration)).
3. **Advertencias visibles dentro del producto**.
4. **Mensajería de depreciación dentro de los propios SDKs existentes**.
5. **Comunicación multicanal y recordatorios periódicos**.
6. **Monitoreo activo del progreso de la migración** a través de analíticas de uso de los SDKs.

---

### Implementación de un proceso de cambio de API para Magic Items Store

Para asentar los principios analizados en un contexto del mundo real, veamos cómo se implementó un proceso de cambio de API en Magic Items Store.

#### Antecedentes: tratamiento de problemas de diseño de API tempranos

La API de primera generación de Magic Items Store se desarrolló con plazos ajustados, priorizando el lanzamiento rápido sobre la consistencia del diseño. A medida que el negocio creció, surgieron problemas:
- **Nombres de recursos inconsistentes**: El *endpoint* `/catalog` se usaba para recuperar productos, lo que generó confusión cuando la API se amplió para admitir banners y promociones.
- **Modelos de datos no estructurados**: Distintos *endpoints* mezclaban convenciones de nomenclatura (`camelCase` y `snake_case`).
- **Falta de una estrategia formal de versionado o gestión del cambio**: Los cambios se realizaban *ad hoc*, lo que provocaba *breaking changes* inesperados.

#### Fase 1: Establecimiento de un proceso de cambio de API

##### Paso 1: Definición de la política de cambios

1. **Compatibilidad hacia atrás primero**: Cualquier cambio que rompa a los consumidores existentes debe manejarse a través de una nueva variante de recurso, nunca modificando los recursos existentes.
2. **Reglas de extensión consistentes**: La adición de nueva funcionalidad debe ser siempre no disruptiva.
3. **Proceso de depreciación transparente**: Notificación suficiente y guías claras de migración.

##### Paso 2: Creación de una nueva variante de recurso para productos

Se introdujo un nuevo recurso dedicado `/products` que devuelve exclusivamente artículos comprables, mientras que `/catalog` se mantuvo para elementos más amplios del catálogo y se marcó como obsoleto.

Ejemplo de llamada a la API antes y después:

Llamada a `/catalog` heredado (ahora obsoleto):
```http
GET /catalog?filter=active
```
```json
{ 
  "items": [ 
    { 
      "id": "123", 
      "title": "Running Shoes", 
      "status": "active", 
      "category": "footwear" 
    }, 
    { 
      "id": "124", 
      "title": "Promotional Banner", 
      "status": "marketing", 
      "category": "misc" 
    } 
  ] 
}
```

Llamada al nuevo *endpoint* `/products`:
```http
GET /products
```
```json
{ 
  "products": [ 
    { 
      "id": "123", 
      "name": "Running Shoes", 
      "category": "footwear" 
    } 
  ] 
}
```

#### Fase 2: Gestión de la depreciación de `/catalog`

##### Paso 1: Anuncio de la depreciación con comunicación clara

- Actualización de la documentación de la API marcando `/catalog` como obsoleto.
- Entrada en el registro de cambios con enlaces a las guías de migración.
- Carteles de advertencia en los paneles de desarrolladores.
- Notificaciones por correo electrónico a los titulares de claves de API activas.

##### Paso 2: Implementación de una estrategia de retiro definitivo (*Sunset*) para `/catalog`

1. **Aviso de depreciación en las respuestas de la API**:
```http
Sunset: Wed, 30 Sep 2025 23:59:59 GMT 
Deprecation: true 
Link: <https://developer.magicstore.com/migrate-products>; rel="deprecation-guide"
```
2. **Período de gracia para que los desarrolladores realicen la transición**: Ventana de transición de seis meses con soporte y analíticas de seguimiento.
3. **Retiro final (*Sunset*) y eliminación de `/catalog`**: Tras el periodo de gracia, cualquier petición a `/catalog` devuelve un código de estado `410 Gone`:
```http
HTTP/1.1 410 Gone 
Content-Type: application/json 
```
```json
{ 
  "error": "The `/catalog` endpoint has been removed. Please use `/products`." 
}
```

#### Fase 3: Preparación para el futuro de la estrategia de APIs

Con el éxito de la migración de `/catalog`, Magic Items Store estableció prácticas de gobernanza a largo plazo:
- Los cambios en la API deben seguir un proceso de gobernanza estructurado.
- Todos los *breaking changes* requieren una nueva variante de recurso.
- Se adoptó un enfoque de evolución de API híbrido (evolución continua para cambios no disruptivos y nuevas versiones únicamente cuando sea estrictamente necesario).
- Pautas estrictas de depreciación y retiro definitivo para mantener una experiencia de desarrollador fluida.

---

### Resumen

En este capítulo, exploramos cómo gestionar los cambios de API de manera eficaz, equilibrando la necesidad de innovación con la responsabilidad de preservar la estabilidad y la confianza de los desarrolladores. La gestión del cambio de API no es solo un ejercicio técnico; es una disciplina estratégica que garantiza que su plataforma evolucione sin interrumpir a los usuarios existentes.

Comenzamos comprendiendo por qué el cambio es inevitable, ya sea debido a la modernización, la introducción de nuevas capacidades o el refuerzo de la seguridad. Cada factor exige una planificación cuidadosa para evitar integraciones rotas y mantener una ventaja competitiva.

Presentamos los bloques de construcción de la gestión del cambio de APIs y analizamos las estrategias de versionado (modelos globales, basados en recursos y basados exclusivamente en la evolución) y cuándo aplicar cada uno. Destacamos cómo empresas como Stripe equilibran con éxito la innovación rápida con la previsibilidad al combinar la evolución continua con ciclos estructurados de versionado.

Un tema clave fue la importancia de la depreciación y el retiro definitivo (*sunsetting*). La señalización adecuada de los recursos obsoletos a través de encabezados en tiempo de ejecución, documentación y divulgación proactiva garantiza que los desarrolladores tengan el tiempo y el apoyo necesarios para migrar con confianza, minimizando la fricción.

El estudio de caso de Magic Items Store mostró estos principios en acción, demostrando cómo una API que alguna vez fue inconsistente evolucionó hasta convertirse en una plataforma estructurada y escalable mediante una gestión disciplinada del cambio, rutas de migración claras y una comunicación transparente.

Al dominar estas estrategias, puedes guiar tu API a través de una evolución continua, convirtiendo el cambio inevitable en un catalizador para el crecimiento y relaciones más sólidas con los desarrolladores.
