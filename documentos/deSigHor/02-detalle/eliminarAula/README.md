<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > eliminarAula > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/eliminarAula/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-24
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `eliminarAula()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la eliminación segura de aulas con confirmación previa.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|eliminarAula()|
|**Actor primario**|Administrador|
|**Objetivo**|Eliminar aula de forma segura con confirmación previa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Aula seleccionada desde abrirAulas(), usuario autenticado como Administrador|
|**Postcondición exitosa**|Aula eliminada del sistema, usuario regresa a lista de aulas actualizada|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: eliminarAula()](/images/RUP/00-casos-uso/02-detalle/eliminarAula/eliminarAula.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de eliminación

<div align=center>

|![Wireframe: Eliminación de aula](/images/RUP/00-casos-uso/02-detalle/eliminarAula/eliminarAula-wireframe.svg)|
|-|
|**Estado**: ConfirmandoEliminacion / EliminandoAula|

</div>

**Correspondencia con especificación:**
- Sistema "presenta información del aula a eliminar"
- Actor "solicita confirmación de eliminación"
- Sistema "permite solicitar confirmar eliminación"
- Sistema "permite solicitar cancelar eliminación"

### validaciones del wireframe

- ¿Se presenta claramente la información del aula a eliminar?
- ¿Es claro el impacto de la eliminación?
- ¿Las opciones de confirmación están bien diferenciadas?
- ¿La advertencia de eliminación es suficientemente visible?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita eliminar aula||
||**Sistema**|presenta información del aula a eliminar|• Código, nombre del aula<br>• Edificio asociado, capacidad<br>• Tipo, recursos, observaciones<br>• Presenta advertencia de eliminación<br>• Permite solicitar confirmar eliminación<br>• Permite solicitar cancelar eliminación|
|**Administrador**|solicita confirmación de eliminación||(opcional)|
||**Sistema**|permite solicitar confirmar eliminación|• Permite confirmar eliminación<br>• Permite cancelar eliminación|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ConfirmandoEliminacion**|Estado donde se presenta la información del aula a eliminar|Sistema debe presentar todos los datos del aula y advertencia de eliminación|
|**EliminandoAula**|Estado donde se procesa la eliminación del aula|Sistema debe procesar eliminación y presentar resultado|

## funcionalidad de eliminación segura

### concepto clave

- **eliminarAula()** es un caso de uso que abarca:
  - **Presentar** información completa del aula a eliminar
  - **Permitir solicitar** confirmación del administrador
  - **Procesar** eliminación del aula del sistema

### información presentada

- **Datos del aula** presentados para confirmación:
  - Código del aula
  - Nombre del aula
  - Edificio asociado
  - Capacidad del aula
  - Tipo de aula
  - Recursos disponibles
  - Observaciones
  - Advertencia sobre eliminación irreversible

## opciones de navegación

### operaciones de eliminación

- **Confirmar eliminación** → Aula eliminada, **&lt;&lt;include&gt;&gt;** `abrirAulas()` 
- **Cancelar eliminación** → **&lt;&lt;include&gt;&gt;** `abrirAulas()` sin cambios

### navegación del sistema

- **Eliminación exitosa** → **&lt;&lt;include&gt;&gt;** `abrirAulas()` con lista actualizada
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirAulas()` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **AULAS_ABIERTO** → `eliminarAula()` → **AULAS_ABIERTO**
- **AULA_ABIERTA** → `eliminarAula()` → **AULAS_ABIERTO**

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirAulas()` → **AULAS_ABIERTO** (lista actualizada)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de eliminar un aula específica
- **solicita**: expresa confirmación de eliminación del aula

### sistema

- **presenta**: muestra información del aula seleccionada
- **permite solicitar**: habilita confirmación o cancelación de eliminación
- **procesa**: ejecuta eliminación del aula del sistema

## características metodológicas

### separación de responsabilidades

- **Actor**: Solo solicita eliminación y confirmación
- **Sistema**: Solo presenta información y permite solicitar confirmación

### ausencia de detalles de implementación

- No especifica tecnología de persistencia
- No incluye detalles de eliminación física vs lógica
- No menciona estructura de almacenamiento

### conversación de confirmación

- El caso de uso representa una conversación de verificación
- Tiene objetivo claro: eliminar aula con confirmación
- Termina con confirmación o cancelación explícita

### rol del actor

- **Entrada**: Administrador (desde aulas abiertas)
- **Salida**: Administrador (con conocimiento de aula eliminada o cancelación)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de eliminación segura

- **Confirmación requerida**: Evita eliminaciones accidentales
- **Información completa**: Muestra qué se va a eliminar
- **Operación irreversible**: Claridad sobre las consecuencias
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirAulas()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirAulas()](../abrirAulas/README.md) - Caso de uso de navegación
- [editarAula()](../editarAula/README.md) - Caso complementario del CRUD
- [crearAula()](../crearAula/README.md) - Caso complementario del CRUD
- [eliminarEdificio()](../eliminarEdificio/README.md) - Patrón de referencia para eliminación
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada