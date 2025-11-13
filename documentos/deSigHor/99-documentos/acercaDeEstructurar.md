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

---

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
