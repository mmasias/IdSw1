<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > editarProfesor > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/editarProfesor/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-20
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `editarProfesor()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la edición de profesores.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|editarProfesor()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar datos de edición de profesor con capacidad de modificación y guardado|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Profesor seleccionado desde abrirProfesores() o profesor recién creado desde crearProfesor()|
|**Postcondición exitosa**|Profesor modificado guardado, usuario puede continuar editando en PROFESOR_ABIERTO o volver al sistema|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: editarProfesor()](/images/RUP/00-casos-uso/02-detalle/editarProfesor/editarProfesor.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: edición de profesor

<div align=center>

|![Wireframe: Edición de profesor](/images/RUP/00-casos-uso/02-detalle/editarProfesor/editarProfesor-wireframe.svg)|
|-|
|**Estado**: EditandoDatos / GuardandoDatos|

</div>

**Correspondencia con especificación:**
- Sistema "presenta datos de edición" 
- Actor "solicita modificar campos"
- Sistema "permite solicitar modificar información"
- Actor "solicita guardar y salir"

### validaciones del wireframe

- ¿Se presentan claramente todos los campos editables del profesor?
- ¿Es fácil modificar los datos del profesor?
- ¿Las opciones de guardado están bien diferenciadas?
- ¿La navegación permite continuar editando o salir?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita editar profesor||
||**Sistema**|presenta datos de edición|• Código, nombres, apellidos del profesor<br>• Correo electrónico, teléfono<br>• Observaciones del profesor<br>• Permite solicitar modificar campos<br>• Permite solicitar guardar profesor<br>• Permite solicitar cancelar edición|
|**Administrador**|solicita modificar campos||(opcional)|
||**Sistema**|permite solicitar modificar información|• Permite editar todos los campos<br>• Permite solicitar guardar cambios<br>• Permite solicitar continuar editando|
|**Administrador**|solicita guardar y salir||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**EditandoDatos**|Estado donde se presentan los datos de edición del profesor|Sistema debe presentar todos los campos editables del profesor|
|**GuardandoDatos**|Estado donde se procesan las modificaciones del profesor|Sistema debe procesar cambios y permitir continuar o salir|

## funcionalidad de edición completa

### concepto clave - "el gordo"

- **editarProfesor()** es "el gordo" que:
  - **Presenta** datos completos con todos los campos
  - **Permite** modificación de cualquier campo del profesor
  - **Mantiene** sesión de edición activa (puede continuar)
  - **Guarda** cambios cuando el administrador solicita

### información presentada

- **Datos básicos del profesor**:
  - Código del profesor
  - Nombres del profesor
  - Apellidos del profesor
- **Datos de contacto**:
  - Correo electrónico
  - Teléfono
- **Información adicional**:
  - Observaciones del profesor

## opciones de navegación

### operaciones de edición

- **Continuar editando** → Mantiene `PROFESOR_ABIERTO` en modo edición
- **Guardar y salir** → `abrirProfesores()` con lista actualizada
- **Cancelar edición** → `abrirProfesores()` sin cambios

### navegación del sistema

- **Continuar editando** → Permanece en `PROFESOR_ABIERTO`
- **Guardar y salir** → `PROFESORES_ABIERTO` via `abrirProfesores()`
- **Cancelación** → `PROFESORES_ABIERTO` sin modificaciones

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **PROFESORES_ABIERTO** → `editarProfesor()` → **PROFESOR_ABIERTO**
- **PROFESOR_ABIERTO** → `editarProfesor()` → **PROFESOR_ABIERTO** (continuar editando)

Ambas transiciones incluyen:
- **&lt;&lt;include&gt;&gt;** `abrirProfesores()` → **PROFESORES_ABIERTO** (al guardar y salir)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de editar un profesor específico
- **solicita**: expresa modificación de campos del profesor
- **solicita**: expresa guardado de cambios del profesor

### sistema

- **presenta**: muestra información editable del profesor seleccionado
- **permite solicitar**: habilita modificación y guardado de cambios
- **procesa**: ejecuta guardado de modificaciones del profesor

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
- Tiene objetivo claro: editar profesor con todos sus campos
- Permite continuar editando o guardar y salir

### rol del actor

- **Entrada**: Administrador (desde profesores abiertos o profesor recién creado)
- **Salida**: Administrador (con conocimiento de profesor modificado)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de "el gordo"

- **Edición completa**: Permite modificar todos los campos del profesor
- **Sesión continua**: Mantiene estado de edición activa
- **Flexibilidad**: Puede continuar editando o guardar y salir
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `abrirProfesores()` para mostrar lista actualizada

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirProfesores()](../abrirProfesores/README.md) - Caso de uso de navegación
- [crearProfesor()](../crearProfesor/README.md) - Caso complementario del CRUD
- [eliminarProfesor()](../eliminarProfesor/README.md) - Caso complementario del CRUD
- [editarCurso()](../editarCurso/README.md) - Patrón de referencia para "el gordo"
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada