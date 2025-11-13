<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > crearProfesor > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/crearProfesor/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-20
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `crearProfesor()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la creación de profesores aplicando la filosofía C→U como "el delgado".

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|crearProfesor()|
|**Actor primario**|Administrador|
|**Objetivo**|Crear profesor con datos mínimos y transferir inmediatamente a edición completa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador en estado PROFESORES_ABIERTO|
|**Postcondición exitosa**|Profesor creado con datos mínimos, usuario en modo edición completa|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: crearProfesor()](/images/RUP/00-casos-uso/02-detalle/crearProfesor/crearProfesor.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: creación rápida de profesor

<div align=center>

|![Wireframe: Creación de profesor](/images/RUP/00-casos-uso/02-detalle/crearProfesor/crearProfesor-wireframe.svg)|
|-|
|**Estado**: CreandoProfesor|

</div>

**Correspondencia con especificación:**
- Sistema "presenta formulario de creación"
- Actor "solicita crear profesor"
- Sistema "permite solicitar crear con datos mínimos"
- Actor "solicita crear y editar"

### validaciones del wireframe

- ¿Se solicitan únicamente los campos mínimos necesarios?
- ¿Es claro que se transferirá inmediatamente a edición completa?
- ¿La navegación es directa y eficiente?
- ¿Los campos obligatorios están claramente marcados?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita crear profesor||
||**Sistema**|presenta formulario de creación|• Campo código del profesor<br>• Campo nombres del profesor<br>• Campo apellidos del profesor<br>• Permite solicitar crear profesor<br>• Permite solicitar cancelar creación|
|**Administrador**|solicita crear profesor||(con datos mínimos)|
||**Sistema**|permite solicitar crear con datos mínimos|• Valida código único<br>• Valida nombres no vacíos<br>• Valida apellidos no vacíos<br>• Permite solicitar crear y editar|
|**Administrador**|solicita crear y editar||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**CreandoProfesor**|Estado donde se presenta el formulario de creación con campos mínimos|Sistema debe presentar solo los campos esenciales para crear el profesor|

## funcionalidad de creación rápida

### concepto clave - "el delgado"

- **crearProfesor()** es "el delgado" que:
  - **Solicita** solo datos mínimos indispensables
  - **Crea** profesor con información básica
  - **Transfiere** inmediatamente a edición completa
  - **Aplica** filosofía C→U (Create→Update)

### información solicitada (mínima)

- **Datos esenciales del profesor**:
  - Código del profesor (único, obligatorio)
  - Nombres del profesor (obligatorio)
  - Apellidos del profesor (obligatorio)

### campos no solicitados (se completan en edición)

- **Datos de contacto**: Correo electrónico, teléfono
- **Información adicional**: Observaciones del profesor

## opciones de navegación

### operaciones de creación

- **Crear y editar** → Profesor creado + **&lt;&lt;include&gt;&gt;** `editarProfesor()` para completar datos
- **Cancelar creación** → **&lt;&lt;include&gt;&gt;** `abrirProfesores()` sin cambios

### navegación del sistema

- **Creación exitosa** → **&lt;&lt;include&gt;&gt;** `editarProfesor()` en `PROFESOR_ABIERTO`
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirProfesores()` en `PROFESORES_ABIERTO`

## conexión con diagrama de contexto

Este caso de uso corresponde a la transición:
- **PROFESORES_ABIERTO** → `crearProfesor()` → **PROFESOR_ABIERTO**

La transición incluye:
- **&lt;&lt;include&gt;&gt;** `editarProfesor()` → **PROFESOR_ABIERTO** (para completar datos)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de crear un nuevo profesor
- **solicita**: expresa creación con datos mínimos proporcionados
- **solicita**: expresa crear y pasar inmediatamente a edición

### sistema

- **presenta**: muestra formulario con campos mínimos de creación
- **permite solicitar**: habilita creación con validación básica
- **valida**: verifica unicidad de código y completitud de campos obligatorios

## características metodológicas

### separación de responsabilidades

- **Actor**: Solo solicita creación y proporciona datos mínimos
- **Sistema**: Solo presenta formulario mínimo y permite solicitar creación

### ausencia de detalles de implementación

- No especifica tecnología de persistencia
- No incluye detalles de validación avanzada
- No menciona estructura de almacenamiento

### conversación de creación mínima

- El caso de uso representa una conversación de creación rápida
- Tiene objetivo claro: crear profesor con datos mínimos
- Termina transfiriendo inmediatamente a edición completa

### rol del actor

- **Entrada**: Administrador (desde profesores abiertos)
- **Salida**: Administrador (con conocimiento de profesor creado en edición)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de "el delgado" - filosofía C→U

- **Creación mínima**: Solo solicita datos indispensables para crear
- **Transferencia inmediata**: Pasa directamente a edición completa
- **Eficiencia**: Minimiza fricción en el proceso de creación
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `editarProfesor()` para completar información

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirProfesores()](../abrirProfesores/README.md) - Caso de uso de navegación
- [editarProfesor()](../editarProfesor/README.md) - Caso de transferencia inmediata
- [eliminarProfesor()](../eliminarProfesor/README.md) - Caso complementario del CRUD
- [crearCurso()](../crearCurso/README.md) - Patrón de referencia para "el delgado"
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada