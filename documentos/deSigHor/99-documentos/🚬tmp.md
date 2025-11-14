# 2Think

## pySighor

<div align=center>

|||
|-|-|
**MdD**|[Diagrama](/documentos/deSigHor/00-modelo-del-dominio/modelo-dominio.md)
**eAyCdU**|[Diagrama](/documentos/deSigHor/01-actores-casos-uso/actores-casos-uso.md#diagrama) + [**DdC**](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)
**PCdU**| 🚬
**dCdU & pCdU**|[crearPrograma](/documentos/deSigHor/02-detalle/crearPrograma/#diagrama-de-especificación) / [editarPrograma](/documentos/deSigHor/02-detalle/editarPrograma/#diagrama-de-especificación)

</div>

### eCdU **🚬**

<details>

<div align=center>

![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma.svg)

</div>

<details>

|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarProfesor/eliminarProfesor.svg)|
|-|-|

<details>

#### Estructurar el modelo de casos de uso - 1

|![](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion.svg)|![](/images/documentos/deSigHor/02-detalle/solicitarConfirmacion/solicitarConfirmacion-wireframe.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/eliminarEdificio/eliminarEdificio.svg)
|-|-|-|

[Solicitar confirmación](/documentos/deSigHor/02-detalle/solicitarConfirmacion/README.md) / [En el proyecto](/documentos/deSigHor/99-documentos/diagramaConfirmacion.md)


<details>
#### Estructurar el modelo de casos de uso - 2

|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/crearProfesor/crearProfesor.svg)|![](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/00-casos-uso/02-detalle/editarProfesor/editarProfesor.svg)|
|-|-|

<details>

![](/images/documentos/deSigHor/02-detalle/guardarCambiosDePrograma/guardarCambiosDePrograma.svg)

- \<\<include\>\>:
  - crearPrograma() --> guardarCambiosDePrograma()
  - editarPrograma() --> guardarCambiosDePrograma()

<details>

##### ¿Y si me voy a abrirPrograma() con cambios pendientes?

<details>

![](https://raw.githubusercontent.com/mmasias/IdSw1/update2025/images/documentos/deSigHor/99-documentos/diagramaGuardarCambiosDePrograma.svg)

</details>

</details>

</details>
</details>

</details>

</details>

</details>

