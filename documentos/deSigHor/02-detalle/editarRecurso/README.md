<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > editarRecurso > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/editarRecurso/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-24
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `editarRecurso()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la edición de recursos.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|editarRecurso()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar datos de edición de recurso con capacidad de modificación y guardado|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Recurso seleccionado desde abrirRecursos() o recurso recién creado desde crearRecurso()|
|**Postcondición exitosa**|Recurso modificado guardado, usuario puede continuar editando en RECURSO_ABIERTO o volver al sistema|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: editarRecurso()](/images/RUP/00-casos-uso/02-detalle/editarRecurso/editarRecurso.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: edición de recurso

<div align=center>

|![Wireframe: Edición de recurso](/images/RUP/00-casos-uso/02-detalle/editarRecurso/editarRecurso-wireframe.svg)|
|-|
|**Estado**: PresentingData / ModifyingData|

</div>

**Correspondencia con especificación:**
- Actor "solicita editar recurso"
- Sistema "presenta"
- Actor "introduce" modificaciones
- Actor "solicita finalizar"

### validaciones del wireframe

- ¿Se presentan claramente todos los campos editables del recurso?
- ¿Es fácil modificar los datos del recurso?
- ¿Las opciones de guardado están bien diferenciadas?
- ¿La navegación permite continuar editando o salir?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita editar recurso||
||**Sistema**|presenta|• código del recurso<br>• nombre del recurso<br>• descripción del recurso|
|**Administrador**|introduce||modificaciones (opcional)|
|**Administrador**|solicita guardar||
||**Sistema**|presenta resultado|• recurso actualizado<br>• continuar editando|
|**Administrador**|solicita finalizar||
||**Sistema**|presenta resultado|• transferir a abrirRecursos()|

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**PresentingData**|Estado donde el sistema presenta los datos del recurso para edición|Sistema debe presentar código, nombre y descripción del recurso|
|**ModifyingData**|Estado donde el administrador introduce modificaciones|Administrador puede introducir modificaciones opcionales|

## funcionalidad de edición completa

### concepto clave - "el gordo"

- **editarRecurso()** es "el gordo" que:
  - **Presenta** todos los datos del recurso para edición
  - **Permite** modificación completa de información
  - **Procesa** guardado de cambios
  - **Mantiene** sesión de edición activa

### información presentada (completa)

- **Datos del recurso**:
  - Código del recurso (único, obligatorio)
  - Nombre del recurso (obligatorio)
  - Descripción del recurso (opcional)

### capacidades de edición

- **Modificación libre**: Todos los campos pueden ser editados
- **Guardado continuo**: Cambios guardados sin cerrar sesión
- **Validación**: Verificación de unicidad y completitud

## opciones de navegación

### operaciones de edición

- **Guardar y continuar** → Cambios guardados + mantiene `RECURSO_ABIERTO`
- **Guardar y salir** → Cambios guardados + **&lt;&lt;include&gt;&gt;** `abrirRecursos()`
- **Cancelar edición** → **&lt;&lt;include&gt;&gt;** `abrirRecursos()` sin cambios

### navegación del sistema

- **Guardado exitoso (continuar)** → Permanece en `RECURSO_ABIERTO`
- **Guardado exitoso (salir)** → **&lt;&lt;include&gt;&gt;** `abrirRecursos()` en `RECURSOS_ABIERTO`
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirRecursos()` en `RECURSOS_ABIERTO`

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **RECURSOS_ABIERTO** → `editarRecurso()` → **RECURSO_ABIERTO**
- **RECURSO_ABIERTO** → `editarRecurso()` → **RECURSO_ABIERTO** (edición continua)

Las transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirRecursos()` → **RECURSOS_ABIERTO** (al guardar y salir)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de editar un recurso
- **solicita**: expresa modificación de campos específicos
- **solicita**: expresa guardar cambios y salir o continuar

### sistema

- **presenta**: muestra datos completos del recurso para edición
- **permite solicitar**: habilita modificación de campos
- **permite solicitar**: habilita guardado y navegación

## características metodológicas

### separación de responsabilidades

- **Actor**: Solicita edición, solicita modificaciones, solicita guardado
- **Sistema**: Presenta datos, permite solicitar modificaciones, permite solicitar guardado

### ausencia de detalles de implementación

- No especifica tecnología de persistencia
- No incluye detalles de validación avanzada
- No menciona estructura de almacenamiento

### conversación de edición completa

- El caso de uso representa una conversación de edición detallada
- Tiene objetivo claro: editar recurso con datos completos
- Permite sesión continua de edición

### rol del actor

- **Entrada**: Administrador (desde recursos abiertos o recurso recién creado)
- **Salida**: Administrador (con recurso editado, en edición continua o lista de recursos)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de "el gordo" - edición completa

- **Presentación completa**: Muestra todos los campos editables
- **Edición continua**: Permite sesión de trabajo extendida
- **Guardado flexible**: Opciones de continuar o salir tras guardar
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirRecursos()` para salir

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirRecursos()](../abrirRecursos/README.md) - Caso de uso de navegación
- [crearRecurso()](../crearRecurso/README.md) - Caso de transferencia desde creación
- [eliminarRecurso()](../eliminarRecurso/README.md) - Caso complementario del CRUD
- [editarEdificio()](../editarEdificio/README.md) - Patrón de referencia para "el gordo"
- [editarAula()](../editarAula/README.md) - Patrón de referencia para "el gordo"
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada