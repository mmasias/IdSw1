<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > guardarCambiosDePrograma > Detalle y prototipado

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Caso de uso**: guardarCambiosDePrograma()
- **Actor**: Sistema (invocado por otros casos de uso)
- **Tipo**: Secundario, `<<include>>` (para guardado explícito), `<<extend>>` (para guardado implícito)
- **Hilo funcional**: Programas (persistencia de datos)

## Propósito

Este caso de uso encapsula la lógica específica de validación y persistencia de los datos de un `Programa`. Es invocado por otros casos de uso para asegurar que los cambios realizados en un programa se guarden de forma consistente en el sistema.

## Justificación de su rol múltiple (`<<include>>` y `<<extend>>`)

`guardarCambiosDePrograma()` es un ejemplo potente de reutilización de lógica de negocio, ya que participa en el flujo del sistema de tres maneras distintas:

1.  **Como `<<include>>` en `crearPrograma()`**:
    *   **Contexto**: Tras la creación mínima de un programa, se invoca para persistir esa primera versión, asegurando que el programa "exista" en el sistema.
    *   **Justificación**: Es un paso obligatorio para que el programa creado sea persistente.

2.  **Como `<<include>>` en `editarPrograma()`**:
    *   **Contexto**: Cuando el actor, en el estado de edición de un programa, solicita explícitamente guardar los cambios.
    *   **Justificación**: Es un paso obligatorio para persistir las modificaciones realizadas por el actor.

3.  **Como `<<extend>>` a `abrirProgramas()`**:
    *   **Contexto**: Cuando el actor intenta salir de un estado de edición (`PROGRAMA_ABIERTO`) hacia la lista de programas (`abrirProgramas()`) y existen cambios sin guardar.
    *   **Justificación**: Es un flujo opcional y condicional que se inserta para prevenir la pérdida de datos, ofreciendo al actor la posibilidad de guardar, descartar o cancelar la salida.

## Diagrama de especificación

<div align=center>

![Caso de uso: guardarCambiosDePrograma()](/images/documentos/deSigHor/02-detalle/guardarCambiosDePrograma/guardarCambiosDePrograma.svg)

</div>

**Código fuente:** [especificacion.puml](especificacion.puml)

## Wireframes

<div align=center>

![Wireframe: Opciones de guardado al salir](/images/documentos/deSigHor/02-detalle/guardarCambiosDePrograma/guardarCambiosAntesDeSalir-wireframe.svg)

</div>

**Código fuente:** [wireframes.puml](wireframes.puml)

## Conversación detallada (Lógica de Guardado)

### Flujo principal: Guardar datos del programa

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Caso de Uso Invocador**|solicita guardar cambios de programa||
||**Sistema**|valida los datos del programa<br>persiste los cambios en el sistema|• Datos guardados exitosamente|

### Flujo alternativo: Datos inválidos

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Caso de Uso Invocador**|solicita guardar cambios de programa||
||**Sistema**|valida los datos del programa<br>detecta datos inválidos|• Retorna error de validación al caso de uso invocador|

## Estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ValidandoDatos**|El sistema verifica la integridad y validez de los datos del programa.|Sistema debe aplicar todas las reglas de negocio para la validación.|
|**PersistiendoDatos**|El sistema almacena los datos validados del programa en la capa de persistencia.|Sistema debe asegurar la integridad transaccional del guardado.|

## Conexión con otros casos de uso

-   **Incluido por**: `crearPrograma()` y `editarPrograma()`.
-   **Extiende a**: `abrirProgramas()` (y otros casos de uso de navegación que salgan de un contexto de edición de `Programa`).

## Vocabulario utilizado

### Caso de Uso Invocador (crearPrograma(), editarPrograma(), o la extensión de abrirProgramas())

-   **solicita guardar cambios de programa**: Pide al sistema que valide y persista los datos del programa.

### Sistema

-   **valida los datos del programa**: Verifica que los datos cumplen con las reglas de negocio.
-   **persiste los cambios en el sistema**: Almacena los datos del programa de forma duradera.
-   **retorna error de validación**: Informa al invocador que los datos no pudieron ser guardados.

## Referencias

- [Reflexiones sobre estructurar de casos de uso en SigHor](../../99-documentos/acercaDeEstructurar.md)
- [crearPrograma()](../crearPrograma/README.md)
- [editarPrograma()](../editarPrograma/README.md)
- [abrirProgramas()](../abrirProgramas/README.md)
