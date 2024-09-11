# Casos de uso > Encontrar actores y Casos de Uso

## ¿Por qué?

En el desarrollo de software, entender las necesidades del usuario y del negocio es fundamental para el éxito del proyecto. Sin embargo, esta comprensión no siempre es intuitiva o directa. La disciplina de requisitos de la metodología Rational Unified Process (RUP) aborda este desafío mediante la identificación de actores y casos de uso. Estos elementos son cruciales para asegurar que el software desarrollado cumpla con las expectativas y necesidades reales de los usuarios finales y del negocio. Además, ayudan a establecer una comunicación clara y efectiva entre los desarrolladores y los stakeholders, evitando malentendidos y cambios costosos en etapas avanzadas del desarrollo.

## ¿Qué?

Encontrar Actores y Casos de Uso

### Actores

* Son entidades externas (pueden ser personas, sistemas, o dispositivos) que interactúan con el sistema.
* Representan roles que los usuarios (humanos o no) desempeñan al interactuar con el sistema.
* Los actores son clave para determinar las diversas formas en que el sistema será utilizado.

### Casos de Uso

* Son descripciones de cómo interactuará un actor con el sistema para lograr un objetivo específico.
* Proporcionan una secuencia de eventos y respuestas, creando una narrativa de cómo el sistema debe comportarse.
* Cada caso de uso es una situación específica dentro del alcance del sistema.

## ¿Para qué?

|||
|-|-|
Identificación de Requisitos Funcionales|Permite determinar qué debe hacer el sistema desde la perspectiva de los usuarios. Los actores y casos de uso exponen las funcionalidades requeridas en un lenguaje comprensible para todos los involucrados.
Comunicación Clara|Facilita la comunicación entre desarrolladores y stakeholders. Los casos de uso proporcionan un lenguaje común para discutir las necesidades y capacidades del sistema.
Priorización|Ayuda a identificar y priorizar las características del sistema basándose en la importancia de los casos de uso para los actores.
Base para Pruebas|Los casos de uso pueden ser utilizados como base para pruebas de aceptación, asegurando que el sistema cumple con las expectativas y necesidades del usuario.

## ¿Cómo?

<div align=center>

|Datos de entrada||Datos de salida|
|-|-|:-:|
Modelo del dominio||Modelo
Requisitos suplementarios||de
Lista de características||casos de uso

</div>

### Los actores

Un actor especifica un rol que adopta una entidad externa cuando interactúa con el sistema directamente (no en respuesta). Puede representar el rol de un usuario o el rol jugado por otro sistema que toca los límites de tu sistema. Los actores representan roles que personas o cosas juegan en relación con el sistema, no personas o cosas específicas (p.e. administrador, no Pepe).

* Realizar sesiones con el/los clientes para discutir quiénes interactuarán con el sistema.
* Identificar diferentes roles que los usuarios pueden tener al interactuar con el sistema.
* Documentar cada actor, incluyendo una breve descripción de su rol.

#### Identificación de actores

* ¿Quién o qué usa el sistema?
* ¿Quién obtiene y provee información al sistema?
* ¿Qué roles juegan en la interacción?

### Los Casos de Uso

Un caso de uso es una especificación de secuencias de acciones, incluyendo variaciones, que el sistema puede realizar y que dan un resultado observable de interés a un actor particular

* Para cada actor, identificar los objetivos o metas que desean alcanzar al usar el sistema.
* Describir brevemente (si hace falta) los casos de uso en un lenguaje claro y no técnico.

#### Identificación de Casos de Uso

* El actor típicamente necesitará casos de uso para soportar su trabajo para crear, cambiar, seguir, borrar o estudiar objetos de negocio
* Algunos de los casos de uso candidatos no llegarán a ser casos de uso en sí mismos. En vez de ello, mejor pueden ser partes de otros casos de uso
* Recordar que intentamos crear casos de uso que son fáciles de modificar, revisar, probar y gestionar como una unidad
* Es útil modelar la trazabilidad entre los requisitos y la lista de características

### Describir brevemente cada Caso de Uso

Usar unas pocas palabras para explicar cada caso de uso o incluso (**muy recomendado**) simplemente asignar bien el nombre del caso de uso, que a menudo comienza con un verbo

### Describir el modelo de casos de uso como un todo

Se debe lograr explicar el modelo de casos de uso en su conjunto, particularmente la forma en el que los casos de uso se relacionan:

* Con los actores, con diagramas de casos de uso.
* Entre sí, con diagramas de estado.

Este paso incluye preparar un glosario de términos

Es muy útil permitir a las personas que no son parte del equipo de desarrollo aprobar el modelo de casos de uso conducido con una entrevista informal

### Validación y revisión

* Revisar los casos de uso con los clientes para asegurar su exactitud y completitud.
* Ajustar según sea necesario para reflejar con precisión las necesidades del usuario y del negocio.

### Mantenimiento continuo

* A medida que el proyecto avanza, revisar y actualizar los actores y casos de uso para reflejar cualquier cambio en los requisitos o comprensión del sistema.

Al seguir estos pasos, la actividad de encontrar actores y casos de uso en RUP establece una base sólida para el desarrollo de software, asegurando que el producto final cumpla con las necesidades y expectativas de sus usuarios y de los clientes.
