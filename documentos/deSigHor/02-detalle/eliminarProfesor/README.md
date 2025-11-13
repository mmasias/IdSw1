<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)

</div>

# pySigHor > eliminarProfesor > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/eliminarProfesor/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-20
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `eliminarProfesor()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la eliminación segura de profesores.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|eliminarProfesor()|
|**Actor primario**|Administrador|
|**Objetivo**|Eliminar profesor de forma segura con confirmación previa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Profesor seleccionado desde abrirProfesores(), usuario autenticado como Administrador|
|**Postcondición exitosa**|Profesor eliminado del sistema, usuario regresa a lista de profesores actualizada|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: eliminarProfesor()](/images/RUP/00-casos-uso/02-detalle/eliminarProfesor/eliminarProfesor.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de eliminación

<div align=center>

|![Wireframe: Eliminación de profesor](/images/RUP/00-casos-uso/02-detalle/eliminarProfesor/eliminarProfesor-wireframe.svg)|
|-|
|**Estado**: ConfirmandoEliminacion / EliminandoProfesor|

</div>

**Correspondencia con especificación:**
- Sistema "presenta información del profesor a eliminar"
- Actor "solicita confirmación de eliminación"
- Sistema "permite solicitar confirmar eliminación"
- Sistema "permite solicitar cancelar eliminación"

### validaciones del wireframe

- ¿Se presenta claramente la información del profesor a eliminar?
- ¿Es claro el impacto de la eliminación?
- ¿Las opciones de confirmación están bien diferenciadas?
- ¿La advertencia de eliminación es suficientemente visible?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita eliminar profesor||
||**Sistema**|presenta información del profesor a eliminar|• Código, nombres, apellidos del profesor<br>• Correo electrónico, teléfono<br>• Observaciones, cursos asignados<br>• Presenta advertencia de eliminación<br>• Permite solicitar confirmar eliminación<br>• Permite solicitar cancelar eliminación|
|**Administrador**|solicita confirmación de eliminación||(opcional)|
||**Sistema**|permite solicitar confirmar eliminación|• Permite confirmar eliminación<br>• Permite cancelar eliminación|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ConfirmandoEliminacion**|Estado donde se presenta la información del profesor a eliminar|Sistema debe presentar todos los datos del profesor y advertencia de eliminación|
|**EliminandoProfesor**|Estado donde se procesa la eliminación del profesor|Sistema debe procesar eliminación y presentar resultado|

## funcionalidad de eliminación segura

### concepto clave

- **eliminarProfesor()** es un caso de uso que abarca:
  - **Presentar** información completa del profesor a eliminar
  - **Permitir solicitar** confirmación del administrador
  - **Procesar** eliminación del profesor del sistema

### información presentada

- **Datos del profesor** presentados para confirmación:
  - Código del profesor
  - Nombres del profesor
  - Apellidos del profesor
  - Correo electrónico
  - Teléfono
  - Observaciones
  - Cursos asignados actualmente
  - Advertencia sobre eliminación irreversible

## opciones de navegación

### operaciones de eliminación

- **Confirmar eliminación** → Profesor eliminado, **&lt;&lt;include&gt;&gt;** `abrirProfesores()` 
- **Cancelar eliminación** → **&lt;&lt;include&gt;&gt;** `abrirProfesores()` sin cambios

### navegación del sistema

- **Eliminación exitosa** → **&lt;&lt;include&gt;&gt;** `abrirProfesores()` con lista actualizada
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirProfesores()` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **PROFESORES_ABIERTO** → `eliminarProfesor()` → **PROFESORES_ABIERTO**
- **PROFESOR_ABIERTO** → `eliminarProfesor()` → **PROFESORES_ABIERTO**

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirProfesores()` → **PROFESORES_ABIERTO** (lista actualizada)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de eliminar un profesor específico
- **solicita**: expresa confirmación de eliminación del profesor

### sistema

- **presenta**: muestra información del profesor seleccionado
- **permite solicitar**: habilita confirmación o cancelación de eliminación
- **procesa**: ejecuta eliminación del profesor del sistema

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
- Tiene objetivo claro: eliminar profesor con confirmación
- Termina con confirmación o cancelación explícita

### rol del actor

- **Entrada**: Administrador (desde profesores abiertos)
- **Salida**: Administrador (con conocimiento de profesor eliminado o cancelación)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de eliminación segura

- **Confirmación requerida**: Evita eliminaciones accidentales
- **Información completa**: Muestra qué se va a eliminar
- **Operación irreversible**: Claridad sobre las consecuencias
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirProfesores()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirProfesores()](../abrirProfesores/README.md) - Caso de uso de navegación
- [editarProfesor()](../editarProfesor/README.md) - Caso complementario del CRUD
- [crearProfesor()](../crearProfesor/README.md) - Caso complementario del CRUD
- [eliminarCurso()](../eliminarCurso/README.md) - Patrón de referencia para eliminación
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada
