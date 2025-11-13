<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > solicitarConfirmacion > Detalle y prototipado

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Caso de uso**: solicitarConfirmacion()
- **Actor**: Sistema (iniciado por el Sistema, pero el Actor primario es el que lo incluye)
- **Tipo**: Secundario, abstracto, incluido
- **Hilo funcional**: Transversal
- **Fase RUP**: Elaboración (se detalla al refinar casos de uso primarios)

## Propósito

Proporcionar un mecanismo genérico y reutilizable para solicitar una confirmación al usuario antes de ejecutar una acción potencialmente destructiva o irreversible.

## Casos de uso relacionados

- **Incluido por**: Cualquier caso de uso que requiera una confirmación (ej. `eliminar<Entidad>()`).
- **Resultado**: Retorna un valor booleano (aceptado/cancelado) al caso de uso que lo incluye.

## Diagrama de especificación

<div align=center>

![Caso de uso: solicitarConfirmacion()](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion.svg)

</div>

**Código fuente:** [especificacion.puml](especificacion.puml)

## Wireframes

<div align=center>

![Wireframe: Confirmación genérica](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion-wireframe.svg)

</div>

**Código fuente:** [wireframes.puml](wireframes.puml)

## Conversación detallada

### Flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Sistema**|presenta solicitud de confirmación|• Pregunta genérica de confirmación<br>• Opción de aceptar<br>• Opción de cancelar|
|**Actor**|acepta confirmación||
||**Sistema**|retorna confirmación aceptada|

### Flujo alternativo: Cancelación

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Actor**|cancela confirmación||
||**Sistema**|retorna confirmación cancelada|

## Estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**EsperandoConfirmacion**|El sistema ha presentado la solicitud y espera la respuesta del actor.|Sistema debe esperar la decisión del actor.|

## Funcionalidad genérica de confirmación

### Concepto clave - Reutilización

- **solicitarConfirmacion()** es un caso de uso `<<include>>` que:
  - **Presenta** una pregunta de confirmación genérica.
  - **Espera** la decisión del actor (aceptar/cancelar).
  - **Retorna** el resultado al caso de uso que lo ha incluido.

### Información solicitada

- **Decisión del actor**: Aceptar o cancelar la acción.

## Conexión con diagrama de contexto

Este caso de uso no aparece directamente en el diagrama de contexto, ya que es un caso de uso `<<include>>` y es invocado por otros casos de uso primarios (ej. `eliminar<Entidad>()`).

## Vocabulario utilizado

### Actor (Administrador o cualquier actor que lo incluya)

- **acepta confirmación**: expresa la decisión de proceder con la acción.
- **cancela confirmación**: expresa la decisión de no proceder con la acción.

### Sistema

- **presenta solicitud de confirmación**: muestra la pregunta al actor.
- **retorna confirmación aceptada**: informa al caso de uso invocador que la acción fue confirmada.
- **retorna confirmación cancelada**: informa al caso de uso invocador que la acción fue cancelada.

## Características metodológicas

### Separación de responsabilidades

- **Actor**: Decide si acepta o cancela.
- **Sistema**: Presenta la solicitud y procesa la respuesta.

### Ausencia de detalles de implementación

- No especifica cómo se presenta la confirmación (diálogo, modal, etc.).
- No incluye lógica de negocio específica de la acción que se confirma.

### Conversación mínima y genérica

- Representa una conversación simple de pregunta-respuesta.
- Es completamente agnóstico a la acción que se está confirmando.

## Referencias

- [Reflexiones sobre estructurar de casos de uso en SigHor](../../99-documentos/acercaDeEstructurar.md)
- [eliminarEdificio()](../eliminarEdificio/README.md) - Ejemplo de caso de uso que lo incluiría.
