# Diagrama de Caso de Uso: solicitarConfirmacion()

## Propósito

Este diagrama ilustra cómo el caso de uso abstracto `solicitarConfirmacion()` es reutilizado por múltiples casos de uso primarios a través de una relación `<<include>>`.

Esto demuestra el Escenario 1 discutido en las [Reflexiones sobre la Estructuración de Casos de Uso](acercaDeEstructurar.md).

## Diagrama

<div align=center>

![Relación de Inclusión para solicitarConfirmacion()](/images/documentos/deSigHor/99-documentos/relacionConfirmacion.svg)

</div>

**Código fuente:** [relacionConfirmacion.puml](relacionConfirmacion.puml)

## Descripción

- El **Administrador** puede iniciar varios casos de uso de eliminación (`eliminarPrograma()`, `eliminarCurso()`, etc.).
- Cada uno de estos casos de uso, antes de proceder con la acción de borrado, **incluye** de forma obligatoria el comportamiento del caso de uso abstracto `solicitarConfirmacion()`.
- Esto asegura que siempre se pida confirmación al usuario de una manera consistente, centralizando la lógica de la confirmación en un único lugar.
