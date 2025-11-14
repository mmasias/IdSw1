# 2Think

## pySighor

<div align=center>

|||
|-|-|
**Modelo del Dominio**|[Diagrama](/documentos/deSigHor/00-modelo-del-dominio/modelo-dominio.md)
**DISCIPLINA DE REQUISITOS**
**1. Encontrar actores y casos de uso**|[Diagrama](/documentos/deSigHor/01-actores-casos-uso/actores-casos-uso.md#diagrama) + [**DdC**](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)
**2. Priorizar casos de uso**| 🚬
**3. y 4. Detallar y prototipar casos de uso**|[crearPrograma](/documentos/deSigHor/02-detalle/crearPrograma/#diagrama-de-especificación) / [editarPrograma](/documentos/deSigHor/02-detalle/editarPrograma/#diagrama-de-especificación)

</div>

### 5. Estructurar casos de uso **🚬**

<div align=center>

![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma.svg)

</div>

|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarProfesor/eliminarProfesor.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarEdificio/eliminarEdificio.svg)
|-|-|-|

#### Estructurar el modelo de casos de uso - 1

<div align=center>

|![](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion.svg)|![](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion-wireframe.svg)
|-|-|

[CdU solicitarConfirmación()](/documentos/deSigHor/02-detalle/solicitarConfirmacion/README.md) / [CdU@DiagramaDeCdU](/documentos/deSigHor/99-documentos/diagramaConfirmacion.md)

</div>

#### Estructurar el modelo de casos de uso - 2

<div align=center>

|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/crearProfesor/crearProfesor.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/editarProfesor/editarProfesor.svg)|
|-|-|

![](/images/documentos/deSigHor/02-detalle/guardarCambiosDePrograma/guardarCambiosDePrograma.svg)

</div>

- \<\<include\>\>:
  - crearPrograma() --> guardarCambiosDePrograma()
  - editarPrograma() --> guardarCambiosDePrograma()

##### ¿Y si me voy a abrirPrograma() con cambios pendientes? (ver en [*DdC*](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg))

<div align=center>

|![](https://raw.githubusercontent.com/mmasias/IdSw1/update2025/images/documentos/deSigHor/99-documentos/diagramaGuardarCambiosDePrograma.svg)
|-

</div>

Esto justifica tanto los \<\<include>> como los \<\<extends>>

#### Estructurar el modelo de casos de uso - 3

|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/abrirProgramas/abrirProgramas.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/abrirCursos/abrirCursos.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/abrirAulas/abrirAulas.svg)
|-|-|-|

<div align=center>

|![](/images/documentos/deSigHor/02-detalle/_patterns/abrirEntidad/generalization.svg)
|-|

</div>

- generalización:
  - abrirProgramas() --|> abrirEntidad()
  - abrirCursos() --|> abrirEntidad()
  - abrirProfesores() --|> abrirEntidad()
  - abrirAulas() --|> abrirEntidad()
  - abrirEdificios() --|> abrirEntidad()
  - abrirRecursos() --|> abrirEntidad()

Esto demuestra herencia/especialización en casos de uso.