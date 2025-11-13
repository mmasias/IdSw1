<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../02-detalle/README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../01-analisis/casos-uso/README.md)
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../conversation-log.md)

</div>

# pySigHor > Requisitos > Diagrama de contexto > Administrador

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Versión**: 6.0
- **Fecha**: 2025-07-11
- **Autor**: Equipo de desarrollo
- **Cambios principales**: Corrección semántica fundamental de nomenclatura (gerundios → participios, casos de uso centrados en usuario, eliminación de sesgo tecnológico)

## Introducción

Este documento presenta el diagrama de contexto para el actor "Administrador de Horarios", mostrando su perspectiva completa del sistema como una máquina de estados. El diagrama especifica la secuencialidad de navegación y hace explícitas las precondiciones que de otro modo requerirían especificación textual.

## Propósito

- Mostrar la perspectiva completa del sistema desde el punto de vista del Administrador de Horarios
- Especificar la secuencialidad de navegación mediante estados y transiciones
- Hacer explícitas las precondiciones de navegación de forma visual
- Validar que todos los casos de uso del administrador tienen lugar en el flujo del sistema
- Identificar posibles casos de uso omitidos o innecesarios para este actor
- Aplicar patrón granular optimizado para flujos naturales de interacción

## Diagrama

<div align=center>

|![Diagrama de Contexto - Administrador de Horarios](/images/RUP/00-casos-uso/01-actores-casos-uso/diagrama-contexto-administrador.svg)
|-
|Código fuente: [diagrama-contexto-administrador.puml](diagrama-contexto-administrador.puml)

</div>

## Estados del sistema

|Estado|Descripción|Función principal|
|-|-|-|
|**SESION_CERRADA**|Estado inicial del sistema|Punto de entrada, requiere autenticación|
|**SISTEMA_DISPONIBLE**|Hub central de navegación|Punto de acceso a todas las funcionalidades|
|**PROGRAMAS_ABIERTO**|Lista de programas académicos|Visualización y selección de programas|
|**PROGRAMA_ABIERTO**|Edición de programa|Modificación de datos de programa (crear/editar)|
|**CURSOS_ABIERTO**|Lista de cursos|Visualización y selección de cursos|
|**CURSO_ABIERTO**|Edición de curso|Modificación de datos de curso (crear/editar)|
|**PROFESORES_ABIERTO**|Lista de profesores|Visualización y selección de profesores|
|**PROFESOR_ABIERTO**|Edición de profesor|Modificación de datos de profesor|
|**PROFESOR_PREFERENCIAS_ABIERTO**|Configuración de preferencias|Configuración específica de preferencias del profesor|
|**EDIFICIOS_ABIERTO**|Lista de edificios|Visualización y selección de edificios|
|**EDIFICIO_ABIERTO**|Edición de edificio|Modificación de datos de edificio|
|**AULAS_ABIERTO**|Lista de aulas|Visualización y selección de aulas|
|**AULA_ABIERTA**|Edición de aula|Modificación de datos de aula|
|**RECURSOS_ABIERTO**|Lista de recursos|Visualización y selección de recursos|
|**RECURSO_ABIERTO**|Edición de recurso|Modificación de datos de recurso|
|**PROFESOR_ASIGNATURAS_ABIERTO**|Configuración de asignaciones|Asignación de profesores a cursos|
|**HORARIO_GENERADO**|Proceso de generación|Ejecución del algoritmo de optimización|
|**HORARIO_ABIERTO**|Consulta de resultados|Visualización de horarios generados|

## Transiciones principales

### Autenticación y navegación al menú
- `iniciarSesion()`: SESION_CERRADA → SISTEMA_DISPONIBLE (proceso de autenticación exitoso)
- `cerrarSesion()`: SISTEMA_DISPONIBLE → SESION_CERRADA

### Navegación a estados de listado
- `abrirProgramas()`: SISTEMA_DISPONIBLE → PROGRAMAS_ABIERTO
- `abrirCursos()`: SISTEMA_DISPONIBLE → CURSOS_ABIERTO
- `abrirProfesores()`: SISTEMA_DISPONIBLE → PROFESORES_ABIERTO
- `abrirEdificios()`: SISTEMA_DISPONIBLE → EDIFICIOS_ABIERTO
- `abrirAulas()`: SISTEMA_DISPONIBLE → AULAS_ABIERTO
- `abrirRecursos()`: SISTEMA_DISPONIBLE → RECURSOS_ABIERTO
- `asignarProfesorACurso()`: SISTEMA_DISPONIBLE → PROFESOR_ASIGNATURAS_ABIERTO
- `generarHorario()`: SISTEMA_DISPONIBLE → HORARIO_GENERADO
- `consultarHorario()`: SISTEMA_DISPONIBLE → HORARIO_ABIERTO

### Patrón granular optimizado con transiciones separadas

**Para entidades estándar (Programas, Cursos, Edificios, Aulas, Recursos)**:
- **X_ABIERTO → crearX() → X_ABIERTO** (transición separada)
- **X_ABIERTO → editarX() → X_ABIERTO** (transición separada)
- **X_ABIERTO → eliminarX() → X_ABIERTO** (operación in situ)
- **X_ABIERTO → editarX() → X_ABIERTO** (edición continua)
- **X_ABIERTO → abrirX() → X_ABIERTO** (retorno a lista)

**Para entidad Profesores (patrón extendido)**:
- **PROFESORES_ABIERTO → crearProfesor() → PROFESOR_ABIERTO** (transición separada)
- **PROFESORES_ABIERTO → editarProfesor() → PROFESOR_ABIERTO** (transición separada)
- **PROFESORES_ABIERTO → eliminarProfesor() → PROFESORES_ABIERTO** (operación in situ)
- **PROFESOR_ABIERTO → editarProfesor() → PROFESOR_ABIERTO** (edición continua)
- **PROFESOR_ABIERTO → configurarPreferenciasProfesor() → PROFESOR_PREFERENCIAS_ABIERTO** (funcionalidad específica)
- **PROFESOR_PREFERENCIAS_ABIERTO → abrirEdicionProfesor() → PROFESOR_ABIERTO** (retorno a edición general)
- **PROFESOR_ABIERTO → abrirProfesores() → PROFESORES_ABIERTO** (retorno a lista)

### Flujo natural crear-editar
- **Crear**: Datos mínimos → redirige inmediatamente a edición
- **Editar**: Estado común para modificación (crear/editar usan mismo estado)
- **Continuidad**: Usuario puede seguir editando sin cambiar contexto

## Precondiciones visuales

### Autenticación requerida
El diagrama hace explícito que para acceder a cualquier funcionalidad del sistema, el administrador debe:
1. Completar autenticación exitosa (SESION_CERRADA → SISTEMA_DISPONIBLE)

### Navegación centralizada desde menú
El acceso a estados de listado requiere pasar por SISTEMA_DISPONIBLE.

### Navegación granular entre estados CRUD
Los estados X_ABIERTO tienen navegación directa entre sus modos de visualización y edición, optimizando el flujo de trabajo.

### Secuencialidad obligatoria
Para realizar cualquier operación CRUD:
`SESION_CERRADA` → `iniciarSesion()` → `SISTEMA_DISPONIBLE` → `abrirX()` → `X_ABIERTO` → `crearX()` o `editarX()` → `X_ABIERTO`

## Validación de casos de uso

### Casos de uso incluidos
Todos los casos de uso identificados para el Administrador de Horarios aparecen en el diagrama:
- **32 casos de uso CRUD estándar**: 5 entidades × (crear + editar + eliminar + listar + editar continua + retorno) = 30 transiciones
- **8 casos de uso CRUD profesores**: Patrón extendido con estado adicional para preferencias
- **3 casos de uso especiales**: asignarProfesorACurso(), generarHorario(), consultarHorario()
- **6 casos de uso de navegación inicial**: abrirX() desde SISTEMA_DISPONIBLE  
- **2 casos de uso de autenticación/navegación**: iniciarSesion(), cerrarSesion()
- **9 casos de uso de retorno al menú**: completarGestion() desde estados X_ABIERTO y especiales

### Casos de uso de navegación granular
El patrón granular y la optimización aplicada revelan:
- **Estados X_ABIERTO**: Casos de uso abrirX() desde SISTEMA_DISPONIBLE y navegación interna
- **Navegación unificada**: completarGestion() como caso de uso único para retorno al menú
- **Separación de responsabilidades**: iniciarSesion() autentica y da acceso al sistema, completarGestion() navega desde cualquier estado

### Optimización del flujo
- **Eliminación in situ**: eliminarX() permanece en X_ABIERTO (sin cambio de estado)
- **Edición continua**: editarX() autorreflexivo en X_ABIERTO
- **Estado especializado**: PROFESOR_PREFERENCIAS_ABIERTO para configuración específica
- **Navegación bidireccional**: Entre PROFESOR_ABIERTO y PROFESOR_PREFERENCIAS_ABIERTO
- **Caso de uso unificado**: completarGestion() reemplaza volverAlMenu() y complementa iniciarSesion()

## Características del diseño

### Patrón hub central
El SISTEMA_DISPONIBLE actúa como punto central de navegación para acceso inicial a funcionalidades.

### Granularidad optimizada
Estados X_ABIERTO proporcionan flujos naturales de trabajo con modos integrados de visualización y edición.

### Estados autorreflexivos
Los estados X_ABIERTO permiten edición continua sin cambios de contexto.

### Separación de responsabilidades
- **Estados X_ABIERTO**: Visualización, selección y modificación de datos integradas
- **Estado PROFESOR_PREFERENCIAS_ABIERTO**: Configuración específica de preferencias
- **Estados especiales**: Procesos únicos (generación, asignaciones, consulta)

### Extensibilidad
El diseño permite agregar nuevas entidades siguiendo el patrón X_ABIERTO establecido.

## Consideraciones de análisis

### Nivel conceptual
- **Enfoque**: Conceptos de negocio y casos de uso únicamente
- **Independencia tecnológica**: Sin asumir interfaz específica
- **Abstracción apropiada**: Nivel RUP Inception

### Validación de flujos
- **Completitud**: Todos los casos de uso tienen lugar en el diagrama
- **Coherencia**: Transiciones reflejan interacciones naturales
- **Optimización**: Flujos minimizan cambios de contexto innecesarios

### Patrón granular aplicado
- **Crear mínimo → editar**: Flujo natural de creación
- **Edición continua**: Optimización de experiencia de trabajo
- **Eliminación in situ**: Operación sin cambio de contexto
- **Navegación unificada**: completarGestion() como punto único de acceso al menú principal

### Separación de responsabilidades optimizada
- **iniciarSesion()**: Proceso de autenticación y acceso al sistema
- **completarGestion()**: Navegación al sistema disponible desde cualquier estado
- **Reutilización**: completarGestion() desde múltiples contextos

### Rigor metodológico aplicado
- **Transiciones separadas**: crear/editar como decisiones independientes del usuario (aplicado a todas las 6 entidades)
- **Sin ambigüedad semántica**: Cada transición representa una acción específica
- **UML estándar**: No implica secuencialidad entre casos de uso alternativos
- **Estados especializados**: PROFESOR_PREFERENCIAS_ABIERTO para funcionalidad específica
- **Consistencia base**: Patrón uniforme aplicado a 5 entidades estándar
- **Extensión controlada**: Profesores con patrón extendido para preferencias

## Referencias

- [Modelo del dominio](../00-modelo-del-dominio/modelo-dominio.md) - Entidades del sistema
- [Actores y casos de uso](actores-casos-uso.md) - Casos de uso del administrador
- Sistema SigHor Original (1998) - Flujo de navegación del sistema legacy
- [conversation-log.md](../../../conversation-log.md) - Proceso de diseño del diagrama de contexto