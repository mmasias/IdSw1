# pySigHor > completarGestion > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/completarGestion/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-09
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `completarGestion()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la presentación del sistema principal.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|completarGestion()|
|**Actor primario**|Administrador|
|**Objetivo**|Disponibilizar sistema con capacidad de solicitar todas las funcionalidades|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador|
|**Postcondición exitosa**|Sistema disponibilizado, usuario puede solicitar cualquier funcionalidad|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: completarGestion()](/images/RUP/00-casos-uso/02-detalle/completarGestion/completarGestion.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo
**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: sistema principal
<div align=center>

|![Wireframe: Panel principal](/images/RUP/00-casos-uso/02-detalle/completarGestion/completarGestion-wireframe.svg)|
|-|
|**Estado**: PresentandoMenu|

</div>

**Correspondencia con especificación:**
- Sistema "presenta panel principal"
- Actor "visualiza opciones disponibles"

### validaciones del wireframe
- ¿El sistema refleja correctamente todas las opciones del diagrama de contexto?
- ¿Es clara la organización de las opciones por categorías?
- ¿La terminología es consistente con otros casos de uso?
- ¿Faltan elementos en la especificación que el wireframe revela?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita disponibilizar sistema||
||**Sistema**|permite solicitar|• abrirProgramas()<br>• abrirCursos()<br>• abrirProfesores()<br>• abrirEdificios()<br>• abrirAulas()<br>• abrirRecursos()<br>• asignarProfesorACurso()<br>• generarHorario()<br>• consultarHorario()<br>• cerrarSesion()|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**PresentandoMenu**|Estado donde se muestra el sistema principal con todas las opciones|Sistema debe presentar todas las opciones de navegación|
|**EsperandoSeleccion**|Usuario está evaluando opciones disponibles|Sistema permanece disponible para recibir selección|

## opciones del sistema

### gestión de datos maestros
- **Gestionar Programas**: Navegar a `abrirProgramas()`
- **Gestionar Cursos**: Navegar a `abrirCursos()`
- **Gestionar Profesores**: Navegar a `abrirProfesores()`
- **Gestionar Edificios**: Navegar a `abrirEdificios()`
- **Gestionar Aulas**: Navegar a `abrirAulas()`
- **Gestionar Recursos**: Navegar a `abrirRecursos()`

### funcionalidades especiales
- **Asignar Profesores**: Navegar a `asignarProfesorACurso()`
- **Generar Horario**: Navegar a `generarHorario()`
- **Consultar Horario**: Navegar a `consultarHorario()`

### funcionalidades del sistema
- **Cerrar Sesión**: Navegar a `cerrarSesion()`

## conexión con diagrama de contexto

Este caso de uso corresponde a la transición:
- **SISTEMA_DISPONIBLE** → `completarGestion()` → **SISTEMA_DISPONIBLE** (autorreflexivo)

Y también a todas las transiciones de retorno desde estados específicos:
- **PROGRAMAS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **CURSOS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **PROFESORES_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **EDIFICIOS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **AULAS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **RECURSOS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **PROFESOR_ASIGNATURAS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **HORARIO_GENERADO** → `completarGestion()` → **SISTEMA_DISPONIBLE**
- **HORARIO_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**

La especificación detalla el interior del estado **SISTEMA_DISPONIBLE** del diagrama de contexto del Administrador de Horarios.

## vocabulario utilizado

### actor (Administrador)
- **necesita**: expresa la intención de realizar una acción
- **visualiza**: observa y comprende las opciones presentadas
- **selecciona**: elige una opción específica del sistema

### sistema
- **permite**: habilita la capacidad de solicitar funcionalidades

## características metodológicas

### separación de responsabilidades
- **Actor**: Solo navega y selecciona opciones
- **Sistema**: Solo presenta opciones, no procesa lógica de negocio

### ausencia de detalles de implementación
- No especifica tecnología de interfaz
- No incluye detalles de presentación específica
- No menciona estructura de datos o almacenamiento

### conversación atómica
- El caso de uso representa una conversación completa
- Tiene objetivo claro: presentar opciones de navegación
- Termina con selección de opción específica

### rol del actor
- **Entrada**: Administrador (recién autenticado o regresando de otra función)
- **Salida**: Administrador (con conocimiento de opciones disponibles)
- **Estado**: Permanece como Administrador durante toda la conversación

### centralidad del caso de uso
- **Hub central**: Conecta con todos los demás casos de uso del sistema
- **Punto de retorno**: Destino común desde todas las funcionalidades
- **Patrón de navegación**: Establece el flujo de navegación del sistema

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada