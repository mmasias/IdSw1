# RUP: Proceso Unificado de Desarrollo

<div align=center>

|MDD / Requisitos / Análisis|Diseño / Desarrollo / Pruebas|
|-:|:-|
|Hacer lo correcto|Hacerlo correcto|

</div>

## ¿Por qué?

En el mundo del desarrollo de software, la complejidad y la necesidad de adaptarse a cambios constantes son retos habituales. Para abordar estos desafíos, es esencial contar con un **marco de trabajo estructurado** que guíe a los equipos a través del proceso de desarrollo, minimizando los riesgos y maximizando la eficiencia y calidad del producto final. 

Aquí es donde entra en juego una metodología como RUP (Rational Unified Process), diseñada para proporcionar un enfoque disciplinado, pero adaptable, a la ingeniería de software.

## ¿Qué?

RUP es un proceso de desarrollo software basado en componentes

|||
|-|-|
Basado en componentes|El sistema es construido por [componentes](componentes.md) de software interconectados y bien definidos vía sus interfaces
Dirigido por Casos de Uso|
Centrado en la arquitectura|
Iterativo e incremental|

### Componente

Pieza de software pequeñas y manejables.

- Reutilización.
- Gestión de la complejidad.
- Modularidad, que facilita
  - Mantenimiento
  - Actualización
  - Escalabilidad..
- Desarrollo iterativo.
- Encapsulación.
- Interfaces bien definidas.

### Dirigido por casos de uso

- Usados como un artefacto primordial para establecer el comportamiento deseado del sistema y para comunicar este comportamiento entre los implicados en el sistema.
- Forma sistemática e intuitiva para capturar los requisitos funcionales, adecuadamente representados para los usuarios, clientes y desarrolladores
- Primera entrada para el análisis, diseño, implementación y pruebas del sistema, incluyendo la creación, verificación y validación de la arquitectura del sistema.
- Facilitan el mantenimiento de la aplicación gracias a la trazabilidad y ortogonalidad con las clases.
- Facilitan la planificación de actividades de los roles.

### Centrado en la arquitectura

La arquitectura del sistema es usada como un artefacto primordial para la conceptualización, construcción, gestión y evolución del sistema bajo desarrollo.

Esta clave incluye:

- Disciplina de Análisis
- Disciplina de Diseño
- Disciplina de Implementación
- Disciplina de Pruebas

### Iterativo e incremental

|Iterativo|Incremental|
|-|-|
El proceso involucra un flujo de entregas ejecutables|El proceso involucra la integración continua de la arquitectura del sistema para producir con cada nueva entrega un incremento que aumenta a otra anterior

Esto incluye:

- Disciplina de Gestión del Proyecto
- Disciplina de Entorno
- Disciplina de Configuración y Gestión de Cambios
- Disciplina de Despliegue

#### Conviene tener en cuenta

|||
|-|-|
El resultado de cada iteración es un sistema ejecutable, pero incompleto; no está preparado para ser puesto en producción. El sistema podría no estar listo para su puesta en producción hasta después de muchas iteraciones; por ejemplo, 10 ó 15.|La salida de una iteración no es un prototipo experimental o desechable, y el desarrollo iterativo no es prototipado. Más bien, la salida es un subconjunto con calidad de producción del sistema final.

Aunque, en general, cada iteración aborda nuevos requisitos y amplía el sistema incrementalmente, una iteración podría, ocasionalmente, volver sobre el software que ya existe y mejorarlo; por ejemplo, una iteración podría centrarse en mejorar el rendimiento de un subsistema, en lugar de extenderlo con nuevas características.

Tener retroalimentación en una etapa temprana vale su peso en oro; más que las especulaciones sobre los requisitos y diseños correctos, la retroalimentación, a partir de la construcción y prueba realista de algo, aporta un conocimiento práctico y crucial, y una oportunidad de modificar o adaptar la comprensión de los requisitos o el diseño. Los usuarios finales tienen la oportunidad de ver rápidamente una parte del sistema y decir: _“Sí, esto es lo que pedí, pero ahora que lo pruebo, lo que realmente quiero es algo un poco distinto”_. Este proceso de _“sí... pero”_ no es un signo de fallo; sino, ciclos estructurados frecuentes y tempranos de _“sí... peros”_, son un modo habilidoso de hacer progresar y descubrir qué es lo que tiene un valor real para el personal involucrado. 


## ¿Para qué?

> **Convertir los requisitos del cliente en un producto de software.**

|||
|-|-|
Gestionar riesgos|Mediante la entrega iterativa, los riesgos se identifican y resuelven progresivamente, evitando sorpresas al final del desarrollo.
Mejorar la calidad del software|Al enfocarse en la arquitectura y permitir revisiones constantes, se asegura la calidad y robustez del software.
Facilitar la adaptación a cambios|La naturaleza iterativa permite incorporar cambios en los requisitos o en la tecnología de manera más flexible y controlada.
Claridad en el proceso|Proporciona una guía clara para cada etapa del desarrollo, definiendo qué debe realizarse, por quién y cuándo.

## ¿Cómo?

<div align=center>

|||
|-|-|
Actividad|Unidad de trabajo solicitado por un rol y que produce un resultado significativo en el contexto del proyecto: habitualmente crear o modificar artefactos.
||Unidad de trabajo solicitado por o asignado a un rol y que produce un reultado significativo en el contexto del proyecto: habitualmente crear o modificar artefactos.
||Tiene un propósito claro, habitualmente crear o modificar artefactos.
Artefacto|Productos tangibles de un proyecto, compuestos por piezas de información que se produce, modifica o utiliza en un proceso.
||Suelen ser formales.
||Suelen ser resultado de las actividades.
||Suelen estar sujetos al CVS.
Rol|Comportamiento y responsabilidad de un equipo (1..* individuos).
||Utilizan artefactos para realizar actividades.
Proceso|Secuencia de actividades que modifican artefactos mediante interacciones entre roles.
Disciplinas|Organizan las actividades del proceso.

</div>

### Disciplinas

<div align=center>

|Técnicas|De soporte|
|-|-|
Modelado del dominio.|Gestión de proyecto
Requisitos.|Entorno
Análisis.|Configuración y gestión de cambios
Diseño.|Despliegue
Implementación.|
Pruebas.|

</div>

### Roles

<div align=center>

![](/images/modelosUML/RUProles.svg)

</div>

### Fases

#### Inicio

* Donde la idea inicial se llevará hasta el punto de ser suficientemente fundada.
  * Delimitar el ámbito del sistema propuesto
  * Demostrar a los potenciales usuarios y/o clientes que el sistema propuesto es capaz de solventar su problema o soportar los objetivos del negocio construyendo un prototipo como prueba de concepto
  * Describir o esbozar la arquitectura candidata
  * Identificar los riesgos críticos

#### Elaboración

* Donde se define la arquitectura
  * Identifica los riesgos significativos, lo que significa riesgos que podrían alterar los planes, costos y horarios de las fases posteriores
  * Crea una línea de base arquitectónica que cubre la funcionalidad significativa del sistema y las características importantes para los implicados
  * Especifica los niveles que deben alcanzar los atributos de calidad
  * Captura casos de uso a aproximadamente 80% de los requerimientos funcionales
  * Prepara una oferta que cubre horario, personal necesario y el costo en el plazo establecido por las prácticas comerciales

#### Construcción

* Donde el software se lleva su completitud
  * Extiende la identificación de casos de uso, la descripción y realización a todo el cuerpo de casos de uso
  * Acaba el análisis, diseño, implementación y pruebas
  * Mantiene la integridad de la arquitectura, modificando cuando sea necesario
  * Monitoriza los riesgos críticos y significatovos heredados de las dos primeras fases y, en caso de que se materialicen, mitigarlos

#### Transición

* Donde el software se pone en manos de la comunidad de usuarios
  * Actividades de preparación, como el sitio web
  * Asesorar al cliente sobre la actualización del entorno en el que el software operará
  * Elaboración de manuales y otros documentos para la entrega a producción
  * Ajuste del software para operar bajo los parámetros reales del entorno del usuario
  * Corrección de los defectos encontrados después de la retroalimentación de la prueba beta
  * Modificaciones del software a la luz de los problemas imprevistos

<div align=center>

||Inicio|Elaboración|Construcción|Transición|
|-|:-:|:-:|:-:|:-:|
**Duración**|10|30|50|10|
**Esfuerzo**|5|20|65|10

|![](/imagenes/porOrganizar/developmentIterative.png)
|:-:
|Desarrollo iterativo
|![](/imagenes/porOrganizar/desarrolloIterativo.gif)

</div>

### Iteraciones

<div align=center>

![](/images/modelosUML/RUPiteraciones.svg)

</div>

### Actividades

<div align=center>

|Disciplina|Actividades|
|-|-|
Disciplina de Requisitos|
||1. Encontrar Actores y Casos de Uso
||2. Priorizar Casos de Uso
||3. Detallar Caso de Uso
||4. Estructurar Casos de Uso
||5. Prototipar Interfaz de Usuario
Disciplina de Análisis
||6. Análisis de la Arquitectura
||7. Análisis de Caso de Uso
||8. Análisis de Clase
||9. Análisis de Paquete
Disciplina de Diseño
||10. Diseño de la Arquitectura
||11. Diseño de Caso de Uso
||12. Diseño de Clase
||13. Diseño de Paquete
Disciplina de Implementación
||14. Implementar la Arquitectura
||15. Integración de Sistemas
||16. Implementar Clase
||17. Pruebas Unitarias
||18. Implementar Subsistema
Disciplina de Pruebas
||19. Planificar Pruebas
||20. Diseñar Pruebas
||21. Implementar Pruebas
||22. Realizar Pruebas de Integración
||23. Realizar Pruebas de Sistemas
||24. Evaluar Pruebas

![](/images/modelosUML/RUPdisciplinas.svg)

</div>

## No se entendió este proceso unificado cuando...

Aquí presentamos algunos signos que indican que no se ha entendido lo que significa
adoptar el proceso unificado y el desarrollo iterativo con la idea de agilidad que se pretende.

- Se piensa que inicio = requisitos, elaboración = diseño, y construcción = implementación (esto es, imponiendo un ciclo de vida en espiral sobre el UP).
- Se piensa que el objetivo de la elaboración es definir modelos de manera completa y cuidadosa, los cuales se traducen a código durante la construcción.
- Se intenta definir la mayoría de los requisitos antes de comenzar el diseño o la implementación.
- Se intenta definir la mayoría del diseño antes de comenzar a implementar; se intenta definir completamente y acordar una arquitectura antes de programar y probar iterativamente.
- Se dedica mucho tiempo a realizar trabajo sobre los requisitos y el diseño antes de comenzar a programar.
- Se cree que una iteración adecuada es de cuatro meses de duración, en lugar de cuatro semanas (excluyendo proyectos de cientos de desarrolladores).
- Se piensa que realizar los diagramas UML y las actividades de diseño constituyen el momento para definir diseños y modelos de manera completa y precisa con gran detalle, y se cree que programar es una simple traducción mecánica de éstos en código.
- Se piensa que adoptar el UP significa hacer muchas de las actividades posibles y crear muchos documentos, y se piensa o experimenta el UP como un proceso formal y exigente con muchos pasos que seguir.
- Se intenta planificar un proyecto en detalle desde el principio hasta el final; intenta predecir, de manera especulativa, todas las iteraciones y lo que debería ocurrir en cada una de ellas.
- Se quieren planes y estimaciones creíbles para los proyectos antes de que termine la fase de elaboración.

[2DO](https://forms.gle/BNJ73QJecR85vFu59)
