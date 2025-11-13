<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../02-detalle/README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../01-analisis/casos-uso/README.md)
|-:

</div>

# Reflexiones sobre estructurar de casos de uso en SigHor

## ¿Por qué?

En el desarrollo de software, a medida que un sistema crece, la cantidad de casos de uso puede volverse inmanejable. Si cada caso de uso se especifica de forma aislada, inevitablemente surgirá redundancia y el modelo general se volverá difícil de comprender y mantener.

La estructuración de casos de uso es necesaria para **gestionar la complejidad**, **reducir la duplicación** de especificaciones y **mejorar la mantenibilidad** del modelo de requisitos. Un modelo bien estructurado es más fácil de entender, validar y evolucionar.

## ¿Qué?

Ver [documento formal del temario](/temario/contenidos/00010-eCdU.md), nos proporciona tres herramientas principales para ello:

<div align=center>

|\<\<include>>|\<\<extend>>|Generalización|
|:-:|:-:|:-:|
Extrae comportamiento que es **común y obligatorio** para varios casos de uso.|Modela un comportamiento **opcional o condicional**.|Establece una relación de herencia.
El caso de uso base es incompleto sin el caso de uso incluido.|El caso de uso base es funcionalmente completo por sí mismo, y el caso de uso de extensión solo se ejecuta bajo ciertas condiciones en un punto de extensión definido.|Un caso de uso "hijo" (especializado) hereda, y puede aumentar o modificar, el comportamiento de un caso de uso "padre" (general).

</div>

## ¿Para qué?

El objetivo de este documento es ir más allá de la teoría y encontrar **ejemplos prácticos, orgánicos y didácticos** de estas relaciones dentro de un proyecto real como [pySigHor](https://github.com/mmasias/pysighor). 

No se trata de memorizar las definiciones, sino aprender a **identificar patrones de interacción** en un flujo de trabajo real que se presten a ser modelados con estas relaciones. 

Esta reflexión sirve como guía para conectar la teoría con la práctica de diseño de requisitos.

## ¿Cómo?

El método más efectivo es analizar el flujo de trabajo de la aplicación: aquí, el [diagrama de contexto del administrador](https://github.com/mmasias/pySigHor/blob/main/RUP/00-casos-uso/01-actores-casos-uso/diagrama-contexto-administrador.md) es nuestra herramienta clave, ya que nos muestra cómo se conectan los casos de uso para formar conversaciones completas.

Al observar este diagrama, podemos identificar los siguientes escenarios:

### Escenario 1: `<<include>>` y la confirmación de borrado

- **Relación**: `<<include>>` (Comportamiento repetido y obligatorio).
- **Contexto**: El administrador puede eliminar prácticamente cualquier entidad del sistema (`eliminarPrograma()`, `eliminarCurso()`, etc.). Por seguridad, toda operación de borrado destructiva debe solicitar una confirmación.
- **Propuesta**:
    - Se define un caso de uso abstracto: **`solicitarConfirmacion()`**.
    - Cada caso de uso `eliminar<Entidad>()` **incluye (`<<include>>`)** a `solicitarConfirmacion()` antes de proceder con la eliminación final.
- **Justificación**: Este es un patrón de diseño universal. El comportamiento de "solicitar confirmación y procesar la respuesta" es idéntico en todos los casos. Extraerlo con `<<include>>` evita la redundancia y asegura consistencia.

### Escenario 2: `<<extend>>` y el guardado opcional

- **Relación**: `<<extend>>` (Comportamiento opcional).
- **Contexto**: El administrador está trabajando con una entidad (ej. en el estado PROFESOR_ABIERTO) y trata de volver al menú (`completarGestion()`) sin haber guardado sus cambios.
- **Propuesta**:
    - Se define un caso de uso: **`guardarCambiosAntesDeSalir()`**.
    - Este caso de uso **extiende (`<<extend>>`)** a `completarGestion()`.
    - El punto de extensión se activa bajo la condición: `si existen cambios sin guardar`.
- **Justificación**: El caso de uso `completarGestion()` (volver al menú) es completo por sí mismo. El flujo de "guardar cambios" es un comportamiento adicional y condicional. Modela una interacción realista que no siempre ocurre, propósito ideal de la relación `<<extend>>`.

### Escenario 3: `generalization` y la edición de entidades

- **Relación**: `generalization` (Especialización).
- **Contexto**: Los casos de uso `crear<Entidad>()` y `editar<Entidad>()` son muy similares: ambos llevan a la misma pantalla de edición (ej. `EditPrograma`).
- **Propuesta**:
    - Se define un caso de uso abstracto y genérico: **`editarEntidadBase()`**, cuyo propósito es "iniciar la edición detallada de una entidad".
    - Los casos de uso `crear<Entidad>()` y `editar<Entidad>()` se modelan como **especializaciones (`generalization`)** de `editarEntidadBase()`.
- **Justificación**: Ambos son tipos de "manipulación de datos". El caso de uso padre define la acción común ("iniciar la edición"), y los hijos la especializan:
    - `crear<Entidad>()`: Especializa `editarEntidadBase()` para el escenario de una entidad **nueva**.
    - `editar<Entidad>()`: Especializa `editarEntidadBase()` para el escenario de una entidad **existente**.
