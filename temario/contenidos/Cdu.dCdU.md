# Casos de Uso > Detallar casos de uso

## ¿Por qué?

Esta actividad provee un medio para comunicar claramente las expectativas del sistema y las funcionalidades a implementar. 

A través de esta es posible entender no solo qué hará el sistema, sino **cómo interactuarán** los actores con él, lo cual es crucial para satisfacer sus necesidades y requerimientos.

## ¿Qué?

Detallar casos de uso implica el proceso de elaborar y **especificar** cada caso de uso identificado durante la disciplina de requisitos en RUP. 

Un caso de uso detallado describe la secuencia de pasos que el sistema y los actores llevarán a cabo para completar un proceso específico o alcanzar un objetivo particular. Esta descripción incluye el flujo principal de eventos (happy path), así como flujos alternativos y excepciones, asegurando que se contemple la totalidad de interacciones posibles.

## ¿Para qué?

|||
|-|-|
Clarificar el alcance del sistema|Definiendo exactamente qué se espera que haga el sistema y qué no.
Facilitar la comunicación|Creando un lenguaje común y entendible entre los desarrolladores y los stakeholders no técnicos.
Guiar el diseño y la implementación|Sirviendo como una base para el desarrollo posterior y las pruebas del sistema.
Documentar requisitos funcionales|Ofreciendo una descripción precisa de las funcionalidades que se deben implementar.

## ¿Cómo?

- **Identificación de los actores**: Determinar quiénes interactuarán con el sistema dentro del contexto del caso de uso.
- **Definición del escenario**: Describir el escenario o situación en la que se utiliza el caso de uso.
- **Documentación del flujo de eventos principal**: Describir la interacción estándar entre el actor y el sistema que lleva al resultado deseado.
- **Especificación de flujos alternativos y excepciones**: Describir los caminos alternativos que pueden surgir durante la interacción, y cómo el sistema debe manejarlos.
- **Precondiciones y postcondiciones**: Establecer lo que se debe cumplir antes de que se inicie el caso de uso y el estado en el que el sistema debe quedar después de su ejecución.
- **Requisitos especiales**: Incluir consideraciones especiales como restricciones de tiempo, condiciones de error y requerimientos de interfaz de usuario.

Este proceso se documenta generalmente en un documento de especificación de casos de uso o en un sistema de seguimiento de requisitos, donde cada caso de uso tiene su propia plantilla detallada.

Además se han de especificar los **requisitos no funcionales** (p.ej. velocidad, disponibilidad, precisión, tiempo de respuesta, tiempo de recuperación, …) con los que el sistema debe realizar el caso de uso detallado.

<div align=center>

|Se usan|
|-|
***Diagramas de estados***
Diagramas de actividad 
Diagramas de secuencia

</div>

### Indicaciones

<div align=center>

|El actor únicamente|El sistema únicamente|
|-|-|
introduce|permite introducir
solicita introducir|permite solicitar
||presenta / muestra / visualiza

</div>

### Contraindicaciones

Se debe evitar incluir términos referentes al "pensamiento o intenciones" del actor (*el jugador mira* …, *el jugador decide* …,) porque **no atañe** a nuestro sistema, es decir, no se van a programar.

Se debe evitar incluir términos referentes a la ejecución del software (*se graba en la base de datos* …,) porque esto **no atañe** a los requisitos: pertenece a la disciplina de análisis/diseño, por lo que  serían decisiones prematuras.

Se debe evitar incluir términos referentes al diseño de la interfaz de usuario (p.e. *se pulsa un botón* …, *arrastra el ratón* …, *ventana de* …,) porque no atañe a esta actividad: se verá en la última actividad de requisitos.

