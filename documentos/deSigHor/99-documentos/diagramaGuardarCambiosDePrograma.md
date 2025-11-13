# Diagrama de Caso de Uso: guardarCambiosDePrograma()

## Propósito

Este diagrama ilustra el rol múltiple del caso de uso `guardarCambiosDePrograma()`, mostrando cómo es **incluido** por los casos de uso `crearPrograma()` y `editarPrograma()`, y a su vez **extiende** al caso de uso `abrirProgramas()`.

Esto demuestra el Escenario 2 discutido en las [Reflexiones sobre la Estructuración de Casos de Uso](acercaDeEstructurar.md).

## Diagrama

<div align=center>

![Relaciones de guardarCambiosDePrograma()](/images/documentos/deSigHor/99-documentos/diagramaGuardarCambiosDePrograma.svg)

</div>

**Código fuente:** [diagramaGuardarCambiosDePrograma.puml](diagramaGuardarCambiosDePrograma.puml)

## Descripción

- El caso de uso `guardarCambiosDePrograma()` encapsula la lógica de validación y persistencia de un `Programa`.
- **Inclusión (`<<include>>`)**:
    - `crearPrograma()`: Incluye `guardarCambiosDePrograma()` para persistir la versión mínima del programa recién creado.
    - `editarPrograma()`: Incluye `guardarCambiosDePrograma()` para guardar explícitamente las modificaciones realizadas por el Administrador.
- **Extensión (`<<extend>>`)**:
    - `abrirProgramas()`: Es extendido por `guardarCambiosDePrograma()` cuando el Administrador intenta salir de un estado de edición de programa con cambios sin guardar. En este contexto, `guardarCambiosDePrograma()` gestiona la interacción para decidir si guardar, descartar o cancelar la salida.