<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../02-detalle/README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../01-analisis/casos-uso/README.md)
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../conversation-log.md)

</div>

# SigHor - Actores y casos de uso

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Versión**: 1.0
- **Fecha**: 2025-07-04
- **Autor**: Equipo de desarrollo

## Introducción

Este documento identifica los actores del sistema y sus casos de uso correspondientes, basándose en el modelo del dominio establecido y el análisis del sistema legacy SigHor. Se enfoca en definir las interacciones fundamentales entre usuarios y sistema mediante casos de uso atómicos siguiendo el patrón CRUD.

## Propósito

- Identificar actores que interactúan con el sistema
- Definir casos de uso atómicos y específicos
- Establecer responsabilidades de cada actor
- Proporcionar base para especificación detallada de requisitos
- Facilitar identificación de funcionalidades del sistema

## Diagrama

<div align=center>

|![Actores y Casos de Uso](/images/RUP/00-casos-uso/01-actores-casos-uso/actores-casos-uso-001.svg)|![Actores y Casos de Uso](/images/RUP/00-casos-uso/01-actores-casos-uso/actores-casos-uso-002.svg)|![Actores y Casos de Uso](/images/RUP/00-casos-uso/01-actores-casos-uso/actores-casos-uso-003.svg)
|:-:|:-:|:-:
|Código fuente: [actores-casos-uso-001.puml](actores-casos-uso-001.puml)|Código fuente: [actores-casos-uso-002.puml](actores-casos-uso-002.puml)|Código fuente: [actores-casos-uso-003.puml](actores-casos-uso-003.puml)

</div>

## Actores identificados

|Actor|Descripción|Responsabilidades principales|
|-|-|-|
|**Administrador de Horarios**|Usuario principal del sistema con permisos completos para gestionar todas las entidades del dominio y ejecutar la generación de horarios|Gestión completa de datos académicos y del campus
|||Configuración de asignaciones y preferencias
|||Ejecución del algoritmo de generación
|||Consulta de resultados
|**Consultor de Horarios**|Usuario con permisos de solo lectura para consultar horarios generados|Visualización de horarios
|||Consulta de asignaciones
|||Acceso de solo lectura a resultados

## Casos de uso por actor

### Administrador de Horarios

|Entidad|Casos de uso CRUD|Casos de uso especiales|
|-|-|-|
|**Programa**|crearPrograma(), abrirProgramas(), editarPrograma(), eliminarPrograma()|
|**Curso**|crearCurso(), abrirCursos(), editarCurso(), eliminarCurso()|
|**Profesor**|crearProfesor(), listarProfesores(), editarProfesor(), eliminarProfesor()|configurarPreferenciasProfesor()
|**Edificio**|crearEdificio(), listarEdificios(), editarEdificio(), eliminarEdificio()|
|**Aula**|crearAula(), listarAulas(), editarAula(), eliminarAula()|
|**Recurso**|crearRecurso(), listarRecursos(), editarRecurso(), eliminarRecurso()|
|**Asignaciones**||asignarProfesorACurso()
|**Proceso central**||generarHorario()
|**Consulta**||consultarHorario()

### Consultor de Horarios

|Categoría|Casos de uso|
|-|-|
|**Consulta**|consultarHorario()

## Casos de uso detallados

### Gestión de entidades académicas

#### Programas académicos
- **crearPrograma()**: Registra nuevo programa académico en el sistema
- **abrirProgramas()**: Abre la gestión de programas académicos registrados
- **editarPrograma()**: Modifica información de programa existente
- **eliminarPrograma()**: Elimina programa del sistema

#### Cursos
- **crearCurso()**: Registra nueva asignatura con su información académica
- **abrirCursos()**: Abre la gestión de cursos académicos registrados
- **editarCurso()**: Modifica información de curso existente
- **eliminarCurso()**: Elimina curso del sistema

#### Profesores
- **crearProfesor()**: Registra nuevo docente en el sistema
- **listarProfesores()**: Muestra todos los profesores registrados
- **editarProfesor()**: Modifica información de profesor existente
- **eliminarProfesor()**: Elimina profesor del sistema
- **configurarPreferenciasProfesor()**: Define preferencias de recursos para cada profesor

### Gestión del campus físico

#### Edificios
- **crearEdificio()**: Registra nuevo edificio en el campus
- **listarEdificios()**: Muestra todos los edificios registrados
- **editarEdificio()**: Modifica información de edificio existente
- **eliminarEdificio()**: Elimina edificio del sistema

#### Aulas
- **crearAula()**: Registra nueva aula con sus características
- **listarAulas()**: Muestra todas las aulas disponibles
- **editarAula()**: Modifica información de aula existente
- **eliminarAula()**: Elimina aula del sistema

#### Recursos
- **crearRecurso()**: Define nuevo tipo de recurso disponible
- **listarRecursos()**: Muestra todos los recursos del sistema
- **editarRecurso()**: Modifica información de recurso existente
- **eliminarRecurso()**: Elimina recurso del sistema

### Asignaciones y configuración

#### Asignaciones académicas
- **asignarProfesorACurso()**: Establece relación profesor-curso

### Proceso central del sistema

#### Generación de horarios
- **generarHorario()**: Ejecuta algoritmo de optimización para crear horario que satisfaga todas las restricciones del dominio

#### Consulta de resultados
- **consultarHorario()**: Visualiza horarios generados y asignaciones realizadas

## Características de los casos de uso

### Atomicidad
Todos los casos de uso siguen el principio de atomicidad:
- Cada caso de uso representa una conversación completa actor-sistema
- Tienen inicio y fin claramente definidos
- Producen un resultado observable de valor para el actor
- No se descomponen en subcasos de uso

### Nomenclatura
Los casos de uso siguen convención que "huele a código":
- Verbos en infinitivo seguidos de sustantivo
- Nombres que sugieren implementación directa
- Correspondencia con operaciones CRUD estándar

### Trazabilidad al modelo del dominio
Cada caso de uso opera sobre entidades identificadas en el modelo del dominio:
- Programa, Curso, Profesor (entidades académicas)
- Edificio, Aula, Recurso (entidades del campus)
- Horario (entidad resultado del proceso)

## Consideraciones de diseño

### Separación de responsabilidades
- **Administrador**: Control completo del sistema y sus datos
- **Consultor**: Acceso de solo lectura, sin capacidad de modificación

### Cobertura funcional
Los casos de uso cubren el ciclo completo del sistema legacy:
1. Configuración de datos maestros (CRUD entidades)
2. Configuración de relaciones y preferencias
3. Ejecución del proceso de generación
4. Consulta de resultados

### Extensibilidad
La estructura permite agregar nuevos casos de uso sin afectar los existentes:
- Nuevos tipos de consulta
- Operaciones adicionales sobre entidades
- Nuevos actores con permisos específicos

## Referencias

- [Modelo del dominio](../00-modelo-del-dominio/modelo-dominio.md) - Base conceptual para identificación de casos de uso
- Sistema SigHor Original (1998) - Funcionalidad del sistema legacy
- [reverseEngineering.md](../../../extraDocs/000-ingenieria-inversa/reverseEngineering.md) - Análisis técnico del sistema original