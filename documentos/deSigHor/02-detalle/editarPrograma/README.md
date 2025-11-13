# pySigHor > editarPrograma > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/editarPrograma/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-17
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `editarPrograma()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la edición de programas académicos.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|editarPrograma()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar formulario de edición de programa académico con capacidad de modificación y guardado|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Programa seleccionado desde abrirProgramas() o programa recién creado desde crearPrograma()|
|**Postcondición exitosa**|Programa modificado guardado, usuario puede continuar editando en PROGRAMA_ABIERTO o volver al sistema|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: editarPrograma()](/images/RUP/00-casos-uso/02-detalle/editarPrograma/editarPrograma.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: edición de programa académico

<div align=center>

|![Wireframe: Edición de programa](/images/RUP/00-casos-uso/02-detalle/editarPrograma/editarPrograma-wireframe.svg)|
|-|
|**Estado**: EditandoDatos / GuardandoDatos|

</div>

**Correspondencia con especificación:**
- Sistema "presenta formulario de edición"
- Actor "visualiza campos editables"
- Sistema "permite modificar información"
- Actor "puede solicitar guardar o cancelar"

### validaciones del wireframe

- ¿El formulario muestra claramente los campos del programa?
- ¿Son intuitivos los campos de entrada?
- ¿Los botones de acción están bien posicionados?
- ¿Falta información que el wireframe revela?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita editar programa||
||**Sistema**|presenta formulario de edición|• Código, nombre, descripción del programa<br>• Permite solicitar modificar campos<br>• Permite solicitar guardar programa<br>• Permite solicitar guardar y salir<br>• Permite solicitar cancelar edición|
|**Administrador**|solicita modificar campos||(opcional)|
||**Sistema**|permite modificar información|• Campos editables habilitados|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**EditandoDatos**|Estado donde se muestra el formulario de edición del programa|Sistema debe presentar todos los campos del programa editables|
|**GuardandoDatos**|Estado donde se procesan las modificaciones del programa|Sistema debe guardar y confirmar los cambios realizados|

## funcionalidad unificada: editar = modificar = guardar

### concepto clave

- **editarPrograma()** es un caso de uso que abarca:
  - **Mostrar** formulario con datos del programa
  - **Modificar** campos según necesidades del administrador
  - **Guardar** cambios realizados

### campos de edición

- **Formulario de programa** permite modificar:
  - Código del programa
  - Nombre del programa
  - Descripción del programa

## opciones de navegación

### operaciones de programa

- **Solicitar guardar programa** → Permanecer en `editarPrograma()` (continuar editando)
- **Solicitar guardar y salir** → Navegar a `abrirProgramas()`
- **Solicitar cancelar edición** → Navegar a `abrirProgramas()`

### navegación del sistema

- **Continuar editando** → Permanecer en estado `PROGRAMA_ABIERTO`
- **Finalizar edición** → Navegar a `abrirProgramas()`

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **PROGRAMAS_ABIERTO** → `editarPrograma()` → **PROGRAMA_ABIERTO**
- **PROGRAMAS_ABIERTO** → `crearPrograma()` → **PROGRAMA_ABIERTO**

Y las transiciones de salida:
- **PROGRAMA_ABIERTO** → `abrirProgramas()` → **PROGRAMAS_ABIERTO**

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de realizar una acción
- **visualiza**: observa y comprende la información presentada
- **selecciona**: elige una opción específica del formulario

### sistema

- **presenta**: muestra de forma organizada el formulario y opciones
- **permite**: habilita funcionalidades de edición y guardado

## características metodológicas

### separación de responsabilidades

- **Actor**: Solo navega, modifica campos y selecciona opciones
- **Sistema**: Solo presenta formularios, no procesa lógica de negocio

### ausencia de detalles de implementación

- No especifica tecnología de interfaz
- No incluye detalles de presentación específica
- No menciona estructura de datos o almacenamiento

### conversación atómica

- El caso de uso representa una conversación completa
- Tiene objetivo claro: editar programa académico
- Termina con selección de acción específica

### rol del actor

- **Entrada**: Administrador (desde programas abiertos o creación)
- **Salida**: Administrador (con conocimiento de programa editado)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de edición de datos maestros

- **Punto de convergencia**: Recibe tanto programas nuevos como existentes (filosofía C→U)
- **Funcionalidad de edición**: Modificar información del programa
- **Navegación consistente**: Sigue el patrón establecido del sistema

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirProgramas()](../abrirProgramas/README.md) - Caso de uso de navegación
- [Filosofía C→U](../../../../extraDocs/008-filosofia-crud-creacion-edicion/README.md) - Metodología aplicada
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada