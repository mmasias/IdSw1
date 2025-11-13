# pySigHor > eliminarPrograma > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/eliminarPrograma/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-18
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `eliminarPrograma()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la eliminación segura de programas académicos.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|eliminarPrograma()|
|**Actor primario**|Administrador|
|**Objetivo**|Eliminar programa académico de forma segura con confirmación previa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Programa seleccionado desde abrirProgramas(), usuario autenticado como Administrador|
|**Postcondición exitosa**|Programa eliminado del sistema, usuario regresa a lista de programas actualizada|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: eliminarPrograma()](/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de eliminación

<div align=center>

|![Wireframe: Eliminación de programa](/images/RUP/00-casos-uso/02-detalle/eliminarPrograma/eliminarPrograma-wireframe.svg)|
|-|
|**Estado**: ConfirmandoEliminacion / EliminandoPrograma|

</div>

**Correspondencia con especificación:**
- Sistema "presenta información del programa a eliminar"
- Actor "solicita confirmación de eliminación"
- Sistema "permite solicitar confirmar eliminación"
- Sistema "permite solicitar cancelar eliminación"

### validaciones del wireframe

- ¿Se presenta claramente la información del programa a eliminar?
- ¿Es claro el impacto de la eliminación?
- ¿Las opciones de confirmación están bien diferenciadas?
- ¿La advertencia de eliminación es suficientemente visible?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita eliminar programa||
||**Sistema**|presenta información del programa a eliminar|• Código, nombre, descripción del programa<br>• Presenta advertencia de eliminación<br>• Permite solicitar confirmar eliminación<br>• Permite solicitar cancelar eliminación|
|**Administrador**|solicita confirmación de eliminación||(opcional)|
||**Sistema**|permite solicitar confirmar eliminación|• Permite confirmar eliminación<br>• Permite cancelar eliminación|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ConfirmandoEliminacion**|Estado donde se presenta la información del programa a eliminar|Sistema debe presentar todos los datos del programa y advertencia de eliminación|
|**EliminandoPrograma**|Estado donde se procesa la eliminación del programa|Sistema debe procesar eliminación y presentar resultado|

## funcionalidad de eliminación segura

### concepto clave

- **eliminarPrograma()** es un caso de uso que abarca:
  - **Presentar** información completa del programa a eliminar
  - **Permitir solicitar** confirmación del administrador
  - **Procesar** eliminación del programa del sistema

### información presentada

- **Datos del programa** presentados para confirmación:
  - Código del programa
  - Nombre del programa
  - Descripción del programa
  - Advertencia sobre eliminación irreversible

## opciones de navegación

### operaciones de eliminación

- **Confirmar eliminación** → Programa eliminado, **&lt;&lt;include&gt;&gt;** `abrirProgramas()` 
- **Cancelar eliminación** → **&lt;&lt;include&gt;&gt;** `abrirProgramas()` sin cambios

### navegación del sistema

- **Eliminación exitosa** → **&lt;&lt;include&gt;&gt;** `abrirProgramas()` con lista actualizada
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirProgramas()` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **PROGRAMAS_ABIERTO** → `eliminarPrograma()` → **PROGRAMAS_ABIERTO**
- **PROGRAMA_ABIERTO** → `eliminarPrograma()` → **PROGRAMAS_ABIERTO**

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirProgramas()` → **PROGRAMAS_ABIERTO** (lista actualizada)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de eliminar un programa específico
- **solicita**: expresa confirmación de eliminación del programa

### sistema

- **presenta**: muestra información del programa seleccionado
- **permite solicitar**: habilita confirmación o cancelación de eliminación
- **procesa**: ejecuta eliminación del programa del sistema

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
- Tiene objetivo claro: eliminar programa con confirmación
- Termina con confirmación o cancelación explícita

### rol del actor

- **Entrada**: Administrador (desde programas abiertos)
- **Salida**: Administrador (con conocimiento de programa eliminado o cancelación)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de eliminación segura

- **Confirmación requerida**: Evita eliminaciones accidentales
- **Información completa**: Muestra qué se va a eliminar
- **Operación irreversible**: Claridad sobre las consecuencias
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirProgramas()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirProgramas()](../abrirProgramas/README.md) - Caso de uso de navegación
- [editarPrograma()](../editarPrograma/README.md) - Caso complementario del CRUD
- [crearPrograma()](../crearPrograma/README.md) - Caso complementario del CRUD
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada