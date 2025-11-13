# Reflexiones sobre estructurar de casos de uso en SigHor

## ¿Por qué?

En el desarrollo de software, a medida que un sistema crece, la cantidad de casos de uso puede volverse inmanejable. Si cada caso de uso se especifica de forma aislada, inevitablemente surgirá redundancia y el modelo general se volverá difícil de comprender y mantener.

La estructuración de casos de uso es necesaria para **gestionar la complejidad**, **reducir la duplicación** de especificaciones y **mejorar la mantenibilidad** del modelo de requisitos. Un modelo bien estructurado es más fácil de entender, validar y evolucionar.

## ¿Qué?

El [documento formal del temario](/temario/contenidos/00010-eCdU.md) nos proporciona tres herramientas principales para ello:

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

### Escenario 2: El Rol Múltiple de `guardarCambiosDePrograma()`

Este escenario es más complejo y potente, ya que involucra dos tipos de relaciones (`<<include>>` y `<<extend>>`) para un mismo caso de uso, demostrando un alto nivel de reutilización de la lógica de negocio.

- **Relación Principal 1: `<<include>>` (Guardado Explícito)**
    - **Contexto**: La lógica para persistir los datos de un `Programa` es necesaria en dos momentos: al crear la entidad mínima (filosofía "delgado") y al guardar las modificaciones en el modo de edición (filosofía "gordo").
    - **Propuesta**:
        - Se define un caso de uso específico: **`guardarCambiosDePrograma()`**, que encapsula toda la lógica de validación y persistencia de un programa.
        - Los casos de uso `crearPrograma()` y `editarPrograma()` **incluyen (`<<include>>`)** a `guardarCambiosDePrograma()` para ejecutar la acción de guardado.
    - **Justificación**: Se centraliza la responsabilidad de guardar un programa en un único lugar, haciéndolo reutilizable y fácil de mantener. `crearPrograma()` y `editarPrograma()` dependen de esta lógica para completar su flujo.

- **Relación Principal 2: `<<extend>>` (Guardado Implícito/Opcional)**
    - **Contexto**: Cuando el administrador está en el estado de edición (`PROGRAMA_ABIERTO`) y trata de navegar hacia atrás (ej. `abrirProgramas()`) teniendo cambios sin guardar.
    - **Propuesta**:
        - El mismo caso de uso, **`guardarCambiosDePrograma()`**, **extiende (`<<extend>>`)** al caso de uso de navegación `abrirProgramas()`.
    - **Justificación**: El guardado aquí es un flujo opcional, condicionado a que existan cambios. El caso de uso `abrirProgramas()` es completo por sí mismo, pero bajo esta condición, se le "extiende" la funcionalidad de guardar.

- **Conclusión del Escenario**: Este modelo muestra cómo un mismo componente de lógica de negocio (`guardarCambiosDePrograma()`) puede ser invocado de manera **obligatoria** desde los casos de uso que lo necesitan para su flujo principal (`crear` y `editar`), y de manera **opcional y condicional** para extender el comportamiento de otros casos de uso (`abrirProgramas`), demostrando un diseño de requisitos robusto y modular.

---

### Escenario 3: `generalization` y el patrón de gestión de listas

Este escenario demuestra el uso de **generalización** (herencia) para modelar casos de uso que son conceptualmente la misma operación aplicada a diferentes entidades, donde las diferencias son puramente paramétricas.

- **Relación**: `generalization` (Herencia/Especialización)
- **Contexto**: El administrador puede "abrir y gestionar" seis tipos de entidades diferentes: Programas, Cursos, Profesores, Aulas, Edificios y Recursos. En todos los casos, el flujo es idéntico:
    1. Presentar lista completa de entidades
    2. Permitir filtrado por campos específicos
    3. Ofrecer navegación a operaciones CRUD (crear, editar, eliminar)
    4. Retornar al menú principal
- **Propuesta**:
    - Se define un **caso de uso abstracto** (patrón): **`abrirEntidad(TipoEntidad)`**, que encapsula el comportamiento genérico de "gestionar una lista".
    - Los casos de uso concretos **especializan (`generalization`)** este patrón:
        - `abrirProgramas()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Programas", CamposFiltrable=[código, nombre, descripción]]
        - `abrirCursos()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Cursos", CamposFiltrable=[código, nombre, descripción]]
        - `abrirProfesores()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Profesores", CamposFiltrable=[código, nombre, apellidos]]
        - `abrirAulas()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Aulas", CamposFiltrable=[ID, nombre, edificio]]
        - `abrirEdificios()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Edificios", CamposFiltrable=[ID, nombre]]
        - `abrirRecursos()` especializa `abrirEntidad()` con parámetros: [TipoEntidad="Recursos", CamposFiltrable=[ID, nombre, descripción]]
- **Justificación**:
    - **Similitud estructural**: Los 6 casos siguen exactamente la misma máquina de estados (MostrandoLista → FiltrandoLista).
    - **Perspectiva del actor**: El Administrador conceptualmente hace "lo mismo" en todos los casos: "Quiero ver y gestionar un catálogo de cosas". La diferencia está en qué tipo de cosa gestiona, no en cómo la gestiona.
    - **Diferencias paramétricas**: Solo cambian los datos específicos (nombres de entidades, campos a filtrar), no la lógica del flujo.
    - **Reducción de redundancia**: Sin generalización, cada caso requeriría ~170 líneas de especificación casi idénticas. Con generalización, el patrón abstracto tiene ~170 líneas y cada especialización solo ~30 líneas de parámetros concretos.
    - **Mantenibilidad**: Un cambio en "cómo funciona abrir una lista" se implementa una vez en el patrón y se propaga automáticamente a las 6 especializaciones.

- **Test de perspectiva del actor**: Desde el punto de vista del Administrador, estas acciones son todas instancias de "abrir un catálogo para gestionarlo". No son operaciones conceptualmente diferentes, sino la misma operación aplicada a diferentes tipos de datos. ✅

- **Implementación**: Ver [Patrón abrirEntidad()](../02-detalle/_patterns/abrirEntidad/README.md) y sus [especializaciones](../02-detalle/_patterns/abrirEntidad/README.md#especializaciones-de-este-patrón).


- **Conclusión del Escenario**: La generalización es apropiada cuando múltiples casos de uso representan la misma conversación actor-sistema con diferencias solo en los datos manipulados. Este patrón no solo reduce redundancia, sino que también hace explícita una estructura conceptual del dominio: "gestionar catálogos de entidades" es una operación fundamental del sistema, independiente del tipo específico de entidad.

## Cuándo usar cada relación

|Relación|Cuándo usar|Ejemplo en SigHor|
|:-:|:-:|:-:|
|**`<<include>>`**|Lógica común y **obligatoria** que varios casos necesitan|`solicitarConfirmacion()` incluida por todos los `eliminar*()`|
|**`<<extend>>`**|Lógica **opcional/condicional** que extiende un caso base completo|`guardarCambiosDePrograma()` extiende `abrirProgramas()` si hay cambios sin guardar|
|**`generalization`**|Múltiples casos son **instancias del mismo concepto** con parámetros diferentes|`abrirProgramas()`, `abrirCursos()`, etc. especializan `abrirEntidad()`|

## Antipatrón: Cuándo NO generalizar

**Ejemplo rechazado**: Generalizar `crearPrograma()` y `editarPrograma()` bajo un caso abstracto `editarEntidadBase()`.

**Por qué NO**:
- Aunque ambos usen la misma interfaz (formulario de edición), desde la **perspectiva del actor** son intenciones diferentes.
- "Crear" significa "dar de alta algo nuevo". "Editar" significa "modificar algo existente".
- Ya existe el patrón **C→U** (Crear delgado → Usar/editar gordo) que resuelve la reutilización mediante dependencia secuencial, no herencia.
- La generalización aquí confundiría más que clarificaría.

**Lección**: La generalización debe reflejar que el actor percibe las acciones como "conceptualmente la misma cosa", no solo que compartan código o interfaz.
