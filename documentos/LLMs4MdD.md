# LLMs & MdD

## ¿Por qué?

*Porque nos conocemos...*

## ¿Qué?

> ¿Se recomienda el uso de modelos de lenguaje para hallar las clases conceptuales o generar modelos del dominio?

NO como herramienta principal, pero sí como apoyo complementario con muchas precauciones.

## ¿Por qué NO como herramienta principal?

1. Falta de contexto real
    - Los LLMs no conocen las particularidades organizacionales
    - No captan la cultura empresarial específica
    - Generan modelos "genéricos" que no reflejan la realidad del cliente
1. Riesgo de sobreingeniería
    - Tienden a crear modelos demasiado complejos desde el inicio
    - Incluyen conceptos que "suenan bien" pero no son relevantes
    - Caen en el antipatrón de "parálisis por análisis"
1. Validación imposible
    - El LLM no puede contrastar con expertos del dominio
    - No puede observar procesos reales
    - No detecta inconsistencias entre lo que se dice y lo que se hace

## ¿Dónde sí?

Posibles usos complementarios

- **Como asistente de brainstorming**: Usar como punto de partida, no como verdad absoluta
  - "Dame ideas de clases conceptuales para un sistema hospitalario"
- **Para revisión y mejora**: Puede sugerir conceptos olvidados o relaciones faltantes
  - "Revisa este modelo del dominio de una librería: *DocumentoModelo*"
- **Para explicación y documentación**: Ayuda a documentar decisiones de modelado
  - "Explica por qué la clase 'Reserva' debería relacionarse con 'Recurso'"

## ¿Cómo?

1. Úsalo para prepararte antes de las reuniones con expertos
2. Nunca lo uses como sustituto de la interacción humana
3. Siempre valida sus sugerencias con stakeholders reales
4. Trátalo como un junior que necesita supervisión constante

## *2Think*:

<div align=center>

|*Un LLM puede sugerir qué preguntar, pero nunca puede reemplazar el acto de preguntar*|*Si crees que un LLM puede sustituir una tarde tomando café con el cliente, probablemente no has tomado suficientes cafés con clientes.*|
|-|-|

</div>

El valor real sigue estando en esas conversaciones incómodas con el cliente donde descubres que "factura" significa algo completamente distinto a lo que pensabas.