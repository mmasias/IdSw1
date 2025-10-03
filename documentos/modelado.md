# Modelado++

## ¿Por qué?

En el modelado del dominio con UML, existe la tendencia común de representar todas las conexiones entre conceptos mediante relaciones similares. Esta práctica, influenciada por la familiaridad con los mapas mentales donde todo se conecta mediante líneas simples, produce diagramas que técnicamente son correctos pero semánticamente pobres.

El problema surge cuando se observa, por ejemplo, un sistema de gestión de horarios universitarios. Si se modela únicamente con relaciones de uso, el diagrama resultante sería:

<div align=center>

![](/images/modelosUML/modelado000.svg)

</div>

Este enfoque genera varios problemas fundamentales.

- Primero, se pierde la riqueza semántica: todas las conexiones se ven iguales, sin diferencias en su naturaleza o significado.
- Segundo, no se captura la multiplicidad de las relaciones: ¿cuántos profesores puede tener un curso? ¿cuántas aulas puede usar un horario?
- Tercero, la navegabilidad queda indefinida: ¿se puede navegar en ambas direcciones? ¿qué significa realmente cada conexión?

Además, se ocultan aspectos estructurales importantes como la composición y la agregación, que son fundamentales para entender cómo los objetos se relacionan en términos de todo-parte o dependencia existencial.

## ¿Qué?

El enriquecimiento del modelo consiste en el uso diferenciado de múltiples tipos de relaciones UML, cada una con su propio significado semántico específico. En lugar de depender exclusivamente de las relaciones de uso, se debe incorporar un vocabulario más amplio de conexiones.

Las relaciones disponibles incluyen la asociación simple para conexiones bidireccionales, la composición para relaciones todo-parte con dependencia existencial, la agregación para relaciones todo-parte sin dependencia existencial, y la herencia para relaciones de generalización-especialización.

Cada tipo de relación aporta información específica sobre la naturaleza de la conexión, permitiendo que el modelo comunique no solo que dos conceptos están relacionados, sino cómo están relacionados y qué implica esa relación en términos del dominio.

## ¿Para qué?

El uso diferenciado de relaciones resuelve directamente los problemas identificados en el modelo simple. La riqueza semántica se recupera al elegir la relación que mejor represente la naturaleza real de cada conexión. Un horario no solo "usa" un aula; está "asociado" con ella de manera específica durante ciertos períodos.

La multiplicidad se puede expresar claramente: un curso se asocia con exactamente un programa, pero un programa puede tener múltiples cursos. Un horario se compone de múltiples bloques horarios, y sin el horario, estos bloques no tienen sentido independiente.

La navegabilidad se vuelve explícita: desde un aula se puede navegar hacia los edificios que la contienen, y desde un profesor se puede acceder a los recursos que prefiere u ofrece. Cada flecha tiene un significado específico que enriquece la comprensión del dominio.

Los aspectos estructurales se capturan correctamente: el campus universitario está compuesto por edificios, y estos por aulas. Esta jerarquía de composición refleja la realidad física del dominio de manera que las simples dependencias no pueden expresar.

## ¿Cómo?

La transformación del modelo simple al enriquecido requiere analizar cada conexión individual y determinar su naturaleza real. El proceso comienza identificando las relaciones todo-parte verdaderas, donde la existencia de una parte depende del todo.

<div align=center>

![](/images/modelosUML/modelado001.svg)

</div>

Un horario está compuesto por bloques horarios. Sin el horario, los bloques no tienen sentido independiente. Esta es una relación de composición clara.

Para las relaciones estructurales físicas, se identifica la jerarquía de contención:

<div align=center>

![](/images/modelosUML/modelado002.svg)

</div>

Las asociaciones simples se usan para conexiones donde ambos objetos pueden existir independientemente:

<div align=center>

![](/images/modelosUML/modelado003.svg)

</div>

Las relaciones de preferencia o suministro se modelan como asociaciones con roles específicos:

<div align=center>

![](/images/modelosUML/modelado004.svg)

</div>

El modelo completo enriquecido combina todos estos tipos de relaciones:

<div align=center>

![](/images/modelosUML/modelado005.svg)

</div>

Un diagrama con relaciones diversificadas se encuentra mejor posicionado para el debate y la discusión entre diferentes opciones de modelado. Cuando las relaciones son semánticamente ricas, se puede debatir si una relación debe ser composición o agregación, si la navegabilidad es correcta, o si los roles están bien definidos.

Por ejemplo, consideremos esta alternativa de modelado para el mismo dominio:

<div align=center>

![](https://github.com/mmasias/pySigHor/raw/main/images/RUP/00-casos-uso/00-modelo-del-dominio/modelo-dominio.svg)

</div>

En este modelo alternativo se puede debatir si el CampusUniversitario debe agregarse directamente con Aula o si debe mantener la jerarquía através de Edificio. También se puede discutir si BloqueHorario debería ser composición o agregación con Horario, o si las relaciones del Profesor con Recurso requieren navegabilidad bidireccional.

La práctica con dominios diversos permite desarrollar la intuición para elegir el tipo de relación más apropiado en cada contexto.

## ¿Y ahora qué?

Una vez comprendida la importancia de diversificar las relaciones, se puede practicar con dominios más complejos que requieran mayor variedad de tipos de relaciones.

Consideremos el dominio de un videojuego clásico como Pacman.

<div align=center>

![](/images/modelosUML/modelado006-simple.svg)

</div>

Este modelo demuestra cómo un dominio aparentemente simple requiere múltiples tipos de relaciones para ser representado adecuadamente. La composición define las jerarquías estructurales, la agregación muestra contenido opcional, las asociaciones simples expresan conexiones dinámicas, y las dependencias conectan las clases con sus tipos enumerados.

<div align=center>

![](/images/modelosUML/modelado006-completo.svg)

</div>

### Antipatrones

Lo que sí recomiendo es evitar "contaminar" con notaciones técnicas el modelo del dominio. Los tipos de datos, modificadores de visibilidad y detalles de implementación distraen del propósito central: describir y debatir el escenario que se analiza. La contaminación técnica prematura desvía la discusión desde las decisiones de modelado del dominio hacia consideraciones de implementación que corresponden a fases posteriores.

<div align=center>

![](/images/modelosUML/modelado006-completo-erroneo.svg)

</div>

En esta línea, se proponen los siguientes antipatrones:

|Concreción prematura|Sobre·especificación del dominio|Confusión de capas|Modelo genérico|Validación diferida
|-|-|-|-|-
|Introducir detalles técnicos (tipos de datos, modificadores de visibilidad) antes de comprender el dominio.|Intentar capturar cada detalle antes de entender lo básico.|Tratar el modelo conceptual como tabla de base de datos.|Crear abstracciones "universales" ignorando particularidades organizacionales.|Construir modelos sin contrastar con expertos del dominio.
|Desvía discusión desde conceptos hacia implementación.|Produce "HistorialCambiosDireccionClienteConValidacion" antes de tener "Cliente".|Genera "VentaID" en lugar de "Venta" con atributos conceptuales.|Produce "EmpleadoGenerico" cuando existen roles específicos del contexto.|Modela "Hospital" sin consultar médicos, administradores o usuarios reales.

¿Qué tienen en común?: todos representan **decisiones válidas ejecutadas en fase, nivel o contexto incorrectos**.
