# Casos de Uso > Estructurar casos de uso

**Identificar descripciones de funcionalidad compartida**

- Para reducir la redundancia, deberíamos mirar por las acciones o partes de acciones que son comunes o compartidas por varios casos de uso
  - Una generalización de un caso de uso A aun caso de uso B indica que una instancia del caso de uso A también incluiría el comportamiento especificado por B
  - Los casos de uso concretos son iniciados por un actor y sus instancias constituyen una secuencia completa de acciones realizadas por el sistema
  - Los casos de uso abstractos no serán instanciados por sí mismos, existen solo por otros casos de uso para su reusabilidad

**Identificar descripciones opcionales y adicionales de funcionalidad**

- Una inclusión/extensión se comporta como si fuera algo que se añade en la descripción original de un caso de uso
  - Una relación de extensión desde un caso de uso A aun caso de uso B indica que una instancia del caso de uso B puede incluir el comportamiento especificado por A. Incluye una condición para la extensión
  - Una relación de inclusión puede pensarse simplemente como la inversa de la relación de extensión que provee una explícita e incondicional extensión a un caso de uso
  - En ambos casos, incluye una referencia al punto de extensión en el caso de uso destino, esto es, una posición (sujeto a las condiciones establecidas en la extensión) en el caso de uso donde la extensión puede ser hecha

|||
|-|-|
![](/images/modelosUML/eCdUv000.svg)|![](/images/modelosUML/eCdUv001.svg)

> [Ejemplo](ejemplo-eCdU.md)
