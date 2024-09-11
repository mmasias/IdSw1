# Modelo del dominio

<div align=center>

![](/imagenes/modelosUML/mdd005.svg)

</div>

## ¿Por qué?

|||
|-|-|
Las soluciones de software se aplican **sobre una realidad existente**, con sus situaciones, procesos, particularidades, etc.|Entender esta realidad es fundamental para ser capaces de construir sistemas de software que cumplan con las necesidades del dominio.

## ¿Qué?

El modelo del dominio es la representación de las clases conceptuales más importantes del mundo real en el contexto de nuestra solución.

Se centra en vocabulario, abstracciones relevantes e información del dominio.

Punto de entrada de muchos artefactos que se construyen en un proceso de software

El modelo del dominio **no es** la representación de las clases del software, ni de los objetos.

|Se expresan|No dependen|No consideran|
|-|-|-|
En el lenguaje del cliente|De ningún entorno informático|Restricciones de implementación

## ¿Para qué?

- Comprender el **contexto** del sistema.
- Generar un **vocabulario común**.

## ¿Cómo?

En talleres/reuniones por parte de:

- Analistas del dominio,
- Expertos del dominio y
- personas con habilidad de modelar

### Propuesta de pasos

|Paso|
|-|
|1. Listar las clases conceptuales candidatas.|
|2. Representarlas en el modelo de dominio de partida.|
|3. Añadir las asociaciones necesarias para registrar las relaciones.|
|4. Añadir los atributos que satisfagan los requisitos de información.|
|5. Iterar...|

> ***clase conceptual:*** idea, cosa u objeto

|Recomendaciones|
|-|
Identificar unas pocas clases.
Añadirlo a medida que se conoce/estudia más el modelo.
Mejor especificar en exceso que quedarse corto.
Es normal pasar por alto identificación de clases.

### ¿Cómo hallar clases conceptuales?

- CTRL + C & CTRL + V **modulado…** [Ej.1](https://www.amazon.es/Analysis-Patterns-Reusable-Object-Models/dp/0201895420), [Ej.2](https://www.amazon.com/-/es/David-C-Hay/dp/0932633749), [Ej.3](https://www.amazon.es/Data-Model-Resource-Book-Enterprises/dp/0471380237), [Ej.4](https://www.hl7.org/fhir/)
- [Tesauro](https://es.wikipedia.org/wiki/Tesauro) / Categorías
  - Objetos físicos, lugares, transacciones, elemento de una transacción, roles, contenedores, otros sistemas.
- A mano...
  - Analizar la descripción textual de dominio, identificando sustantivos (nombres) y frases nominales, los que serán candidatos a clases, objetos y atributos. 

### ¿Cómo identificar [asociaciones](mdd.asociaciones.md)?

- Relación entre objetos que indica alguna conexión con significado e interesante.
- Conexión física o conceptual.
- *#SentidoComún* Ni tantas que confundan ni tan pocas que se pierda información.
- Agréguese (luego, sólo si hace falta) la cardinalidad y el detalle.

### ¿Cómo identificar atributos?

- Valor de datos lógico o propiedades relevantes de los objetos individuales.
- Información que debe recordarse.
- Viene bien pensarlos como tipos primitivos.
- Ante la duda: clases conceptual en lugar de colocar atributos.

### Autoevaluación del modelo del dominio

- Verifiquemos que sea correcto desde un punto de vista de [sintáctico](mddCorreccionSintactica.md) y [semántico](mddCorreccionSemantica.md).
- Que soporte todas las acciones a nivel de negocio que esté previsto realizar sobre dicho modelo de dominio.
- Que facilite la gestión de las reglas de negocio asociadas al dominio.
- Que facilite ciertas evoluciones razonablemente anticipables.
- Ordenado y con nombres significativos.

### Artefactos

[¡Diagramas!](diagramas001.md)

||||
|-|-|-|
Entidades / Estático / "Fotos"
||[Diagramas de clases](https://plantuml.com/es/class-diagram)|Clases de objetos y relaciones.
||[Diagrama de objetos](https://plantuml.com/es/object-diagram)|Muestra objetos y sus relaciones en un momento determinado.
Procesos / Dinámica / "Vídeos"
||[Diagrama de actividades](https://plantuml.com/es/activity-diagram-beta)|A.k.a. "diagrama de flujo"
||[Diagrama de estado](https://plantuml.com/es/state-diagram)|Representación visual de los distintos estados en los que puede encontrarse un sistema o un objeto, así como de las transiciones entre esos estados.
||[Diagrama de secuencia](https://plantuml.com/es/sequence-diagram)|Mensajes entre participantes

### Ejemplo

|Paso|Ejemplo|
|-|:-:|
|1. Listar las clases conceptuales candidatas.|Línea de venta, artículo, venta, tienda, registro, pago
|2. Representarlas en el modelo de dominio de partida.|![](/imagenes/modelosUML/mdd001.svg)
|3. Añadir las asociaciones necesarias para registrar las relaciones.|![](/imagenes/modelosUML/mdd002.svg)
|4. Añadir los atributos que satisfagan los requisitos de información.|![](/imagenes/modelosUML/mdd004.svg)
|5. Iterar...|![](/imagenes/modelosUML/mdd005.svg)

### Ejemplos en contexto

- [Fútbol](https://github.com/mmasias/futbol)
- [GoogleWave](https://github.com/mmasias/googleWave)