<div align=right>

|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../../README.md)|
|-:|

</div>

# abrirEntidad(TipoEntidad) - Patrón abstracto

> **IMPORTANTE**: Este es un **caso de uso abstracto** (patrón de diseño).
> No se ejecuta directamente. Define el comportamiento que especializan los casos de uso concretos.

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Tipo**: Caso de uso abstracto (patrón de diseño)
- **Patrón**: Gestión de listas con filtrado
- **Relación UML**: `generalization` (herencia)
- **Número de especializaciones**: 6 casos de uso concretos

## Propósito del patrón

Este patrón encapsula el comportamiento común de **"abrir y gestionar un catálogo de entidades"**, que incluye:

1. Presentar lista completa de entidades
2. Permitir filtrado/búsqueda por campos específicos
3. Ofrecer navegación a operaciones CRUD
4. Retornar al menú principal

Desde la perspectiva del **Administrador**, todas estas acciones son conceptualmente la misma: **"Quiero ver y gestionar una categoría de cosas"**.

## Diagrama de generalización UML

Este diagrama muestra la relación de herencia entre el caso de uso abstracto y sus especializaciones:

<div align=center>

![Patrón abrirEntidad y sus especializaciones](/images/documentos/deSigHor/02-detalle/_patterns/abrirEntidad/generalization.svg)

</div>

**Código fuente:** [generalization.puml](generalization.puml)

## Parámetros de especialización

Cada caso de uso hijo debe definir estos parámetros concretos:

|Parámetro|Descripción|Tipo|Ejemplo|
|-|-|-|-|
|**{TipoEntidad}**|Nombre de la entidad en plural|String|"Programas", "Cursos", "Profesores"|
|**{NombreEntidad}**|Nombre de la entidad en singular|String|"Programa", "Curso", "Profesor"|
|**{CamposFiltrable}**|Lista de campos para filtrado|Array[String]|[código, nombre, descripción]|
|**{CamposMostrar}**|Campos a presentar en la lista|Array[String]|[código, nombre, descripción]|
|**{EstadoDestino}**|Estado del diagrama de contexto|State|PROGRAMAS_ABIERTO, CURSOS_ABIERTO|

## Información del caso de uso (plantilla)

|Atributo|Valor|
|-|-|
|**Nombre**|abrir{TipoEntidad}()|
|**Actor primario**|Administrador|
|**Objetivo**|Presentar lista de {TipoEntidad} con capacidad de filtrado por {CamposFiltrable} y navegación a operaciones CRUD|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador en estado SISTEMA_DISPONIBLE|
|**Postcondición exitosa**|Lista de {TipoEntidad} mostrada en estado {EstadoDestino}, usuario puede filtrar, crear, editar, eliminar o volver al menú|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## Diagrama de especificación (plantilla)

<div align=center>

![Patrón de especificación: abrirEntidad()](/images/documentos/deSigHor/02-detalle/_patterns/abrirEntidad/especificacion.svg)

</div>

**Código fuente:** [especificacion.puml](especificacion.puml)

## Wireframe genérico

<div align=center>

![Wireframe: Gestión de entidades](/images/documentos/deSigHor/02-detalle/_patterns/abrirEntidad/wireframe.svg)

</div>

**Código fuente:** [wireframe.puml](wireframe.puml)

## Conversación detallada (plantilla)

### Flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita abrir {TipoEntidad}||
||**Sistema**|presenta lista de {TipoEntidad}|• {CamposMostrar} de cada {NombreEntidad}<br>• Permite solicitar filtrar lista<br>• Permite solicitar crear {NombreEntidad} nuevo<br>• Permite solicitar eliminar {NombreEntidad}<br>• Permite solicitar editar {NombreEntidad}|
|**Administrador**|solicita filtrar lista||(opcional)|
||**Sistema**|presenta lista filtrada|• Misma información con criterio aplicado sobre {CamposFiltrable}|
|**Administrador**|solicita una de las opciones||

## Estados internos del caso de uso (genéricos)

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**MostrandoLista**|Estado donde se muestra la lista completa de {TipoEntidad}|Sistema debe presentar todos los {TipoEntidad} sin filtro|
|**FiltrandoLista**|Estado donde se aplica criterio de búsqueda|Sistema debe filtrar y mostrar solo {TipoEntidad} que coincidan con criterios sobre {CamposFiltrable}|

## Funcionalidad unificada: listar = filtrar = buscar

### Concepto clave

- **abrir{TipoEntidad}()** es un caso de uso que abarca:
  - **Listar** (sin criterio) → muestra todos los {TipoEntidad}
  - **Filtrar/Buscar** (con criterio) → muestra {TipoEntidad} que coinciden

### Criterios de filtrado

- **Campo de búsqueda** aplica filtro a todos los campos en {CamposFiltrable}
- El filtro es **inclusivo** (busca coincidencias parciales)
- La búsqueda es **no case-sensitive**

## Opciones de navegación (genéricas)

### Operaciones CRUD

- **Solicitar crear {NombreEntidad}** → Navegar a `crear{NombreEntidad}()`
- **Solicitar editar {NombreEntidad}** → Navegar a `editar{NombreEntidad}()`
- **Solicitar eliminar {NombreEntidad}** → Navegar a `eliminar{NombreEntidad}()`

### Navegación del sistema

- **Solicitar salir** → `<<include>>` `completarGestion()`

## Conexión con diagrama de contexto (patrón)

Este caso de uso corresponde a la transición:
- **SISTEMA_DISPONIBLE** → `abrir{TipoEntidad}()` → **{EstadoDestino}**

Y las transiciones de salida:
- **{EstadoDestino}** → `crear{NombreEntidad}()` → **{NombreEntidad}_ABIERTO**
- **{EstadoDestino}** → `editar{NombreEntidad}()` → **{NombreEntidad}_ABIERTO**
- **{EstadoDestino}** → `eliminar{NombreEntidad}()` → **{EstadoDestino}**
- **{EstadoDestino}** → `completarGestion()` → **SISTEMA_DISPONIBLE**

## Vocabulario utilizado

### Actor (Administrador)

- **solicita**: expresa la intención de realizar una acción
- **visualiza**: observa y comprende la información presentada
- **selecciona**: elige una opción específica o {NombreEntidad}

### Sistema

- **presenta**: muestra de forma organizada los {TipoEntidad} y opciones
- **permite**: habilita funcionalidades de filtrado y navegación

## Características metodológicas

### Separación de responsabilidades

- **Actor**: Solo navega, filtra y selecciona opciones
- **Sistema**: Solo presenta datos, no procesa lógica de negocio compleja

### Ausencia de detalles de implementación

- No especifica tecnología de interfaz
- No incluye detalles de presentación específica (tablas, grids, cards)
- No menciona estructura de datos o almacenamiento
- No define algoritmos de filtrado

### Conversación atómica

- El caso de uso representa una conversación completa
- Tiene objetivo claro: gestionar {TipoEntidad}
- Termina con selección de acción específica

### Rol del actor

- **Entrada**: Administrador (desde menú principal, estado SISTEMA_DISPONIBLE)
- **Salida**: Administrador (con conocimiento de {TipoEntidad} disponibles)
- **Estado**: Permanece como Administrador durante toda la conversación

### Patrón de gestión de datos maestros

- **Punto de entrada**: Hub para todas las operaciones CRUD de {TipoEntidad}
- **Funcionalidad unificada**: Listar + filtrar en un solo caso de uso
- **Navegación consistente**: Sigue el patrón establecido del sistema

## Especializaciones de este patrón

|Caso de uso|{TipoEntidad}|{NombreEntidad}|{CamposFiltrable}|Ubicación|
|-|-|-|-|-|
|[abrirProgramas()](../../abrirProgramas/README.md)|Programas|Programa|código, nombre, descripción|documentos/deSigHor/02-detalle/abrirProgramas/|
|[abrirCursos()](../../abrirCursos/README.md)|Cursos|Curso|código, nombre, descripción|documentos/deSigHor/02-detalle/abrirCursos/|
|[abrirProfesores()](../../abrirProfesores/README.md)|Profesores|Profesor|código, nombre, apellidos|documentos/deSigHor/02-detalle/abrirProfesores/|
|[abrirAulas()](../../abrirAulas/README.md)|Aulas|Aula|ID, nombre, edificio|documentos/deSigHor/02-detalle/abrirAulas/|
|[abrirEdificios()](../../abrirEdificios/README.md)|Edificios|Edificio|ID, nombre|documentos/deSigHor/02-detalle/abrirEdificios/|
|[abrirRecursos()](../../abrirRecursos/README.md)|Recursos|Recurso|ID, nombre, descripción|documentos/deSigHor/02-detalle/abrirRecursos/|

## Justificación del patrón

### ¿Por qué generalizar?

Este patrón se identifica porque:

1. **Similitud estructural**: Los 6 casos de uso siguen **exactamente** la misma máquina de estados
2. **Perspectiva del actor**: El Administrador conceptualmente hace "lo mismo" (gestionar un catálogo)
3. **Diferencias paramétricas**: Solo cambian los datos específicos (qué campos, qué entidad)
4. **Mantenibilidad**: Un cambio en el comportamiento de "abrir lista" afecta a los 6 casos

### ¿Cuándo NO usar este patrón?

No usar este patrón cuando:

- El caso de uso tiene lógica de negocio específica diferente
- La navegación o flujo difiere sustancialmente
- Los campos no son simplemente parametrizables
- El actor percibe la acción como conceptualmente diferente

## Antipatrón: Sobregeneralización

**Cuidado**: No todo caso de uso que "se parece" debe generalizarse.

Por ejemplo, `consultarHorario()` también "muestra información", pero:
- No es CRUD (no permite crear/editar/eliminar)
- Maneja ausencia de datos de forma especial
- Tiene semántica diferente desde el actor

## Referencias

- [Diagrama de contexto - Administrador](../../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../../00-modelo-del-dominio/modelo-dominio.md)
- [Reflexiones sobre estructurar casos de uso](../../../99-documentos/acercaDeEstructurar.md)
- [Estructuración de casos de uso en RUP](/temario/contenidos/00010-eCdU.md)
