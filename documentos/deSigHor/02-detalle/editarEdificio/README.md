<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > editarEdificio > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/editarEdificio/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-24
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `editarEdificio()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la edición de edificios.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|editarEdificio()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar datos de edición de edificio con capacidad de modificación y guardado|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Edificio seleccionado desde abrirEdificios() o edificio recién creado desde crearEdificio()|
|**Postcondición exitosa**|Edificio modificado guardado, usuario puede continuar editando en EDIFICIO_ABIERTO o volver al sistema|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: editarEdificio()](/images/RUP/00-casos-uso/02-detalle/editarEdificio/editarEdificio.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: edición de edificio

<div align=center>

|![Wireframe: Edición de edificio](/images/RUP/00-casos-uso/02-detalle/editarEdificio/editarEdificio-wireframe.svg)|
|-|
|**Estado**: EditandoDatos / GuardandoDatos|

</div>

**Correspondencia con especificación:**
- Sistema "presenta datos de edición" 
- Actor "solicita modificar campos"
- Sistema "permite solicitar modificar información"
- Actor "solicita guardar y salir"

### validaciones del wireframe

- ¿Se presentan claramente todos los campos editables del edificio?
- ¿Es fácil modificar los datos del edificio?
- ¿Las opciones de guardado están bien diferenciadas?
- ¿La navegación permite continuar editando o salir?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita editar edificio||
||**Sistema**|presenta datos de edición|• Código, nombre del edificio<br>• Ubicación, descripción<br>• Observaciones del edificio<br>• Permite solicitar modificar campos<br>• Permite solicitar guardar edificio<br>• Permite solicitar cancelar edición|
|**Administrador**|solicita modificar campos||(opcional)|
||**Sistema**|permite solicitar modificar información|• Permite editar todos los campos<br>• Permite solicitar guardar cambios<br>• Permite solicitar continuar editando|
|**Administrador**|solicita guardar y salir||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**EditandoDatos**|Estado donde se presentan los datos de edición del edificio|Sistema debe presentar todos los campos editables del edificio|
|**GuardandoDatos**|Estado donde se procesan las modificaciones del edificio|Sistema debe procesar cambios y permitir continuar o salir|

## funcionalidad de edición completa

### concepto clave - "el gordo"

- **editarEdificio()** es "el gordo" que:
  - **Presenta** datos completos con todos los campos
  - **Permite** modificación de cualquier campo del edificio
  - **Mantiene** sesión de edición activa (puede continuar)
  - **Guarda** cambios cuando el administrador solicita

### información presentada

- **Datos básicos del edificio**:
  - Código del edificio
  - Nombre del edificio
- **Datos de ubicación**:
  - Ubicación del edificio
  - Descripción del edificio
- **Información adicional**:
  - Observaciones del edificio

## opciones de navegación

### operaciones de edición

- **Continuar editando** → Mantiene `EDIFICIO_ABIERTO` en modo edición
- **Guardar y salir** → `abrirEdificios()` con lista actualizada
- **Cancelar edición** → `abrirEdificios()` sin cambios

### navegación del sistema

- **Continuar editando** → Permanece en `EDIFICIO_ABIERTO`
- **Guardar y salir** → `EDIFICIOS_ABIERTO` via `abrirEdificios()`
- **Cancelación** → `EDIFICIOS_ABIERTO` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **EDIFICIOS_ABIERTO** → `editarEdificio()` → **EDIFICIO_ABIERTO**
- **EDIFICIO_ABIERTO** → `editarEdificio()` → **EDIFICIO_ABIERTO** (continuar editando)

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirEdificios()` → **EDIFICIOS_ABIERTO** (al guardar y salir)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de editar un edificio específico
- **solicita**: expresa modificación de campos del edificio
- **solicita**: expresa guardado de cambios del edificio

### sistema

- **presenta**: muestra información editable del edificio seleccionado
- **permite solicitar**: habilita modificación y guardado de cambios
- **procesa**: ejecuta guardado de modificaciones del edificio

## características metodológicas

### separación de responsabilidades

- **Actor**: Solo solicita edición, modificación y guardado
- **Sistema**: Solo presenta información y permite solicitar modificaciones

### ausencia de detalles de implementación

- No especifica tecnología de persistencia
- No incluye detalles de validación de campos
- No menciona estructura de almacenamiento

### conversación de edición continua

- El caso de uso representa una conversación de modificación
- Tiene objetivo claro: editar edificio con todos sus campos
- Permite continuar editando o guardar y salir

### rol del actor

- **Entrada**: Administrador (desde edificios abiertos o edificio recién creado)
- **Salida**: Administrador (con conocimiento de edificio modificado)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de "el gordo"

- **Edición completa**: Permite modificar todos los campos del edificio
- **Sesión continua**: Mantiene estado de edición activa
- **Flexibilidad**: Puede continuar editando o guardar y salir
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirEdificios()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirEdificios()](../abrirEdificios/README.md) - Caso de uso de navegación
- [crearEdificio()](../crearEdificio/README.md) - Caso complementario del CRUD
- [eliminarEdificio()](../eliminarEdificio/README.md) - Caso complementario del CRUD
- [editarCurso()](../editarCurso/README.md) - Patrón de referencia para "el gordo"
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada