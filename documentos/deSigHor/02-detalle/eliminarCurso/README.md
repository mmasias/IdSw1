# pySigHor > eliminarCurso > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/eliminarCurso/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-19
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `eliminarCurso()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la eliminación segura de cursos académicos.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|eliminarCurso()|
|**Actor primario**|Administrador|
|**Objetivo**|Eliminar curso académico de forma segura con confirmación previa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Curso seleccionado desde abrirCursos(), usuario autenticado como Administrador|
|**Postcondición exitosa**|Curso eliminado del sistema, usuario regresa a lista de cursos actualizada|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: eliminarCurso()](/images/RUP/00-casos-uso/02-detalle/eliminarCurso/eliminarCurso.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de eliminación

<div align=center>

|![Wireframe: Eliminación de curso](/images/RUP/00-casos-uso/02-detalle/eliminarCurso/eliminarCurso-wireframe.svg)|
|-|
|**Estado**: ConfirmandoEliminacion / EliminandoCurso|

</div>

**Correspondencia con especificación:**
- Sistema "presenta información del curso a eliminar"
- Actor "solicita confirmación de eliminación"
- Sistema "permite solicitar confirmar eliminación"
- Sistema "permite solicitar cancelar eliminación"

### validaciones del wireframe

- ¿Se presenta claramente la información del curso a eliminar?
- ¿Es claro el impacto de la eliminación?
- ¿Las opciones de confirmación están bien diferenciadas?
- ¿La advertencia de eliminación es suficientemente visible?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita eliminar curso||
||**Sistema**|presenta información del curso a eliminar|• Código, nombre, descripción del curso<br>• Créditos, horas teóricas, horas prácticas<br>• Programa académico asociado<br>• Presenta advertencia de eliminación<br>• Permite solicitar confirmar eliminación<br>• Permite solicitar cancelar eliminación|
|**Administrador**|solicita confirmación de eliminación||(opcional)|
||**Sistema**|permite solicitar confirmar eliminación|• Permite confirmar eliminación<br>• Permite cancelar eliminación|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ConfirmandoEliminacion**|Estado donde se presenta la información del curso a eliminar|Sistema debe presentar todos los datos del curso y advertencia de eliminación|
|**EliminandoCurso**|Estado donde se procesa la eliminación del curso|Sistema debe procesar eliminación y presentar resultado|

## funcionalidad de eliminación segura

### concepto clave

- **eliminarCurso()** es un caso de uso que abarca:
  - **Presentar** información completa del curso a eliminar
  - **Permitir solicitar** confirmación del administrador
  - **Procesar** eliminación del curso del sistema

### información presentada

- **Datos del curso** presentados para confirmación:
  - Código del curso
  - Nombre del curso
  - Descripción del curso
  - Créditos académicos
  - Horas teóricas y prácticas
  - Programa académico asociado
  - Advertencia sobre eliminación irreversible

## opciones de navegación

### operaciones de eliminación

- **Confirmar eliminación** → Curso eliminado, **&lt;&lt;include&gt;&gt;** `abrirCursos()` 
- **Cancelar eliminación** → **&lt;&lt;include&gt;&gt;** `abrirCursos()` sin cambios

### navegación del sistema

- **Eliminación exitosa** → **&lt;&lt;include&gt;&gt;** `abrirCursos()` con lista actualizada
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirCursos()` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **CURSOS_ABIERTO** → `eliminarCurso()` → **CURSOS_ABIERTO**
- **CURSO_ABIERTO** → `eliminarCurso()` → **CURSOS_ABIERTO**

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirCursos()` → **CURSOS_ABIERTO** (lista actualizada)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de eliminar un curso específico
- **solicita**: expresa confirmación de eliminación del curso

### sistema

- **presenta**: muestra información del curso seleccionado
- **permite solicitar**: habilita confirmación o cancelación de eliminación
- **procesa**: ejecuta eliminación del curso del sistema

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
- Tiene objetivo claro: eliminar curso con confirmación
- Termina con confirmación o cancelación explícita

### rol del actor

- **Entrada**: Administrador (desde cursos abiertos)
- **Salida**: Administrador (con conocimiento de curso eliminado o cancelación)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de eliminación segura

- **Confirmación requerida**: Evita eliminaciones accidentales
- **Información completa**: Muestra qué se va a eliminar
- **Operación irreversible**: Claridad sobre las consecuencias
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirCursos()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirCursos()](../abrirCursos/README.md) - Caso de uso de navegación
- [editarCurso()](../editarCurso/README.md) - Caso complementario del CRUD
- [crearCurso()](../crearCurso/README.md) - Caso complementario del CRUD
- [eliminarPrograma()](../eliminarPrograma/README.md) - Patrón de referencia para eliminación
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada