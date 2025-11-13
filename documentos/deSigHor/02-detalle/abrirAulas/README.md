# pySigHor > abrirAulas > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/abrirAulas/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-17
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `abrirAulas()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la gestión de aulas.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|abrirAulas()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar lista de aulas con capacidad de filtrado y navegación a operaciones CRUD|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador en estado SISTEMA_DISPONIBLE|
|**Postcondición exitosa**|Lista de aulas mostrada, usuario puede filtrar, crear, editar, eliminar o volver al sistema|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: abrirAulas()](/images/RUP/00-casos-uso/02-detalle/abrirAulas/abrirAulas.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo
**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: gestión de aulas
<div align=center>

|![Wireframe: Gestión de aulas](/images/RUP/00-casos-uso/02-detalle/abrirAulas/abrirAulas-wireframe.svg)|
|-|
|**Estado**: MostrandoLista / FiltrandoLista|

</div>

**Correspondencia con especificación:**
- Sistema "presenta lista de aulas"
- Actor "visualiza aulas disponibles"
- Sistema "permite filtrar lista"
- Actor "puede seleccionar opciones de gestión"

### validaciones del wireframe
- ¿La tabla muestra claramente ID, nombre, capacidad y edificio?
- ¿Es intuitivo el campo de búsqueda?
- ¿Los botones de acción están bien posicionados?
- ¿Falta información que el wireframe revela?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita listar aulas||
||**Sistema**|presenta lista de aulas|• ID, nombre, capacidad, edificio de cada aula<br>• Permite solicitar filtrar lista<br>• Permite solicitar crear aula nueva<br>• Permite solicitar eliminar aula<br>• Permite solicitar editar aula|
|**Administrador**|solicita filtrar lista||(opcional)|
||**Sistema**|presenta lista filtrada|• Misma información con criterio aplicado|
|**Administrador**|solicita una de las opciones||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**MostrandoLista**|Estado donde se muestra la lista completa de aulas|Sistema debe presentar todas las aulas sin filtro|
|**FiltrandoLista**|Estado donde se aplica criterio de búsqueda|Sistema debe filtrar y mostrar solo aulas que coincidan|

## funcionalidad unificada: listar = filtrar = buscar

### concepto clave
- **abrirAulas()** es un caso de uso que abarca:
  - **Listar** (sin criterio) → muestra todas las aulas
  - **Filtrar/Buscar** (con criterio) → muestra aulas que coinciden

### criterios de filtrado
- **Campo de búsqueda** aplica filtro a:
  - ID del aula
  - Nombre del aula
  - Edificio del aula

## opciones de navegación

### operaciones CRUD
- **Solicitar crear aula** → Navegar a `crearAula()`
- **Solicitar editar aula** → Navegar a `editarAula()`
- **Solicitar eliminar aula** → Navegar a `eliminarAula()`

### navegación del sistema
- **Solicitar salir** → Navegar a `completarGestion()`

## conexión con diagrama de contexto

Este caso de uso corresponde a la transición:
- **SISTEMA_DISPONIBLE** → `abrirAulas()` → **AULAS_ABIERTO**

Y las transiciones de salida:
- **AULAS_ABIERTO** → `crearAula()` → **AULA_ABIERTO**
- **AULAS_ABIERTO** → `editarAula()` → **AULA_ABIERTO**
- **AULAS_ABIERTO** → `eliminarAula()` → **AULAS_ABIERTO**
- **AULAS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**

## vocabulario utilizado

### actor (Administrador)
- **solicita**: expresa la intención de realizar una acción
- **visualiza**: observa y comprende la información presentada
- **selecciona**: elige una opción específica o aula

### sistema
- **presenta**: muestra de forma organizada las aulas y opciones
- **permite**: habilita funcionalidades de filtrado y navegación

## características metodológicas

### separación de responsabilidades
- **Actor**: Solo navega, filtra y selecciona opciones
- **Sistema**: Solo presenta datos, no procesa lógica de negocio

### ausencia de detalles de implementación
- No especifica tecnología de interfaz
- No incluye detalles de presentación específica
- No menciona estructura de datos o almacenamiento

### conversación atómica
- El caso de uso representa una conversación completa
- Tiene objetivo claro: gestionar aulas
- Termina con selección de acción específica

### rol del actor
- **Entrada**: Administrador (desde sistema disponible)
- **Salida**: Administrador (con conocimiento de aulas disponibles)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de gestión de datos maestros
- **Punto de entrada**: Hub para todas las operaciones CRUD de aulas
- **Funcionalidad unificada**: Listar + filtrar en un solo caso de uso
- **Navegación consistente**: Sigue el patrón establecido del sistema

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [completarGestion()](../completarGestion/README.md) - Caso de uso previo
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada