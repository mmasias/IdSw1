<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > crearRecurso > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/crearRecurso/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-24
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `crearRecurso()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la creación de recursos aplicando la filosofía C→U como "el delgado".

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|crearRecurso()|
|**Actor primario**|Administrador|
|**Objetivo**|Crear recurso con datos mínimos y transferir inmediatamente a edición completa|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador en estado RECURSOS_ABIERTO|
|**Postcondición exitosa**|Recurso creado con datos mínimos, usuario en modo edición completa|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: crearRecurso()](/images/RUP/00-casos-uso/02-detalle/crearRecurso/crearRecurso.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: creación rápida de recurso

<div align=center>

|![Wireframe: Creación de recurso](/images/RUP/00-casos-uso/02-detalle/crearRecurso/crearRecurso-wireframe.svg)|
|-|
|**Estado**: RequiringData / ProvidingData|

</div>

**Correspondencia con especificación:**
- Actor "solicita crear recurso"
- Sistema "permite introducir"
- Actor "introduce" 
- Sistema "presenta resultado"

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
|**Administrador**|solicita crear recurso||
||**Sistema**|permite introducir|• código del recurso<br>• nombre del recurso|
|**Administrador**|introduce||• código del recurso<br>• nombre del recurso|
||**Sistema**|presenta resultado|• recurso creado con datos mínimos<br>• transferir a editarRecurso()|

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**RequiringData**|Estado donde el sistema permite introducir datos mínimos del recurso|Sistema debe permitir introducir código y nombre del recurso|
|**ProvidingData**|Estado donde el administrador introduce los datos del recurso|Administrador debe introducir código y nombre del recurso|

## funcionalidad de creación rápida

### concepto clave - "el delgado"

- **crearRecurso()** es "el delgado" que:
  - **Solicita** solo datos mínimos indispensables
  - **Crea** recurso con información básica
  - **Transfiere** inmediatamente a edición completa
  - **Aplica** filosofía C→U (Create→Update)

### información solicitada (mínima)

- **Datos esenciales del recurso**:
  - Código del recurso (único, obligatorio)
  - Nombre del recurso (obligatorio)

### campos no solicitados (se completan en edición)

- **Datos adicionales**: Descripción del recurso
- **Información de relaciones**: Preferencias de profesores, asignación a aulas

## opciones de navegación

### operaciones de creación

- **Crear y editar** → Recurso creado + **&lt;&lt;include&gt;&gt;** `editarRecurso()` para completar datos
- **Cancelar creación** → **&lt;&lt;include&gt;&gt;** `abrirRecursos()` sin cambios

### navegación del sistema

- **Creación exitosa** → **&lt;&lt;include&gt;&gt;** `editarRecurso()` en `RECURSO_ABIERTO`
- **Cancelación** → **&lt;&lt;include&gt;&gt;** `abrirRecursos()` en `RECURSOS_ABIERTO`

## conexión con diagrama de contexto

Este caso de uso corresponde a la transición:
- **RECURSOS_ABIERTO** → `crearRecurso()` → **RECURSO_ABIERTO**

La transición incluye:
- **&lt;&lt;include&gt;&gt;** `editarRecurso()` → **RECURSO_ABIERTO** (para completar datos)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de crear un nuevo recurso
- **introduce**: proporciona datos mínimos requeridos
- **solicita**: expresa crear y pasar inmediatamente a edición

### sistema

- **presenta**: muestra formulario con campos mínimos de creación
- **permite solicitar**: habilita creación con validación básica
- **permite solicitar**: habilita creación tras validación exitosa

## características metodológicas

### separación de responsabilidades

- **Actor**: Solicita creación e introduce datos mínimos
- **Sistema**: Presenta formulario mínimo y permite solicitar creación

### ausencia de detalles de implementación

- No especifica tecnología de persistencia
- No incluye detalles de validación avanzada
- No menciona estructura de almacenamiento

### conversación de creación mínima

- El caso de uso representa una conversación de creación rápida
- Tiene objetivo claro: crear recurso con datos mínimos
- Termina transfiriendo inmediatamente a edición completa

### rol del actor

- **Entrada**: Administrador (desde recursos abiertos)
- **Salida**: Administrador (con conocimiento de recurso creado en edición)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de "el delgado" - filosofía C→U

- **Creación mínima**: Solo solicita datos indispensables para crear
- **Transferencia inmediata**: Pasa directamente a edición completa
- **Eficiencia**: Minimiza fricción en el proceso de creación
- **Navegación incluida**: **&lt;&lt;include&gt;&gt;** `editarRecurso()` para completar información

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [abrirRecursos()](../abrirRecursos/README.md) - Caso de uso de navegación
- [editarRecurso()](../editarRecurso/README.md) - Caso de transferencia inmediata
- [eliminarRecurso()](../eliminarRecurso/README.md) - Caso complementario del CRUD
- [crearEdificio()](../crearEdificio/README.md) - Patrón de referencia para "el delgado"
- [crearAula()](../crearAula/README.md) - Patrón de referencia para "el delgado"
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada