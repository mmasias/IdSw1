<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../02-detalle/README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../01-analisis/casos-uso/README.md)
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../conversation-log.md)

</div>

# SigHor - Modelo del dominio

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Versión**: 1.1
- **Fecha**: 2025-07-04
- **Autor**: Equipo de desarrollo

## Introducción

Este documento describe el modelo conceptual del dominio para el Sistema Generador de Horarios (SigHor). El modelo establece el vocabulario común y las relaciones fundamentales entre las entidades del negocio académico, enfocándose en los conceptos esenciales del problema de asignación de horarios universitarios.

## Propósito

- Establecer un vocabulario común para el proyecto
- Definir las entidades principales del dominio académico
- Documentar las relaciones conceptuales entre entidades
- Servir como base para el desarrollo de casos de uso y requisitos
- Facilitar la comunicación entre stakeholders técnicos y de negocio

## Diagrama

<div align=center>

|![Modelo del Dominio](/images/RUP/00-casos-uso/00-modelo-del-dominio/modelo-dominio.svg)
|:-:
|Código fuente: [modelo-dominio.puml](./modelo-dominio.puml)

</div>

## Problema que resuelve

El algoritmo de generación de horarios busca crear instancias de **Horario** que satisfagan:

1. **Profesor disponible** - Sin conflictos en la agenda del docente
2. **Curso en su BloqueHorario preferido** - Respetando el patrón horario asignado (H1-H8, HE, HV)
3. **Aula adecuada** - Con capacidad suficiente y recursos que prefiere el profesor
4. **Sin conflictos temporales** - Evitando solapamientos de aulas, profesores o grupos

## Glosario

|Entidad|Descripción|Características|
|-|-|-|
|**Horario**|Representa la solución del problema: la asignación exitosa que conecta un Profesor, un Curso y un Aula en un momento específico.|Materializa la solución del algoritmo de optimización
|||Integra todas las restricciones y preferencias del dominio
|||Resultado final visible para usuarios del sistema
|**Profesor**|Representa a los docentes que imparten cursos en la universidad.|Imparte cursos específicos
|||Tiene preferencias sobre recursos de aulas (proyector, laboratorio, etc.)
|||Debe estar disponible en el horario asignado
|**Curso**|Representa las asignaturas que se dictan en la institución académica.|Pertenece a uno o más programas académicos
|||Tiene asociado un BloqueHorario preferido para su dictado
|||Es impartido por un profesor
|**BloqueHorario**|Define los patrones temporales predefinidos para la asignación de cursos.|**H1-H4**: Bloques horarios principales
|||**H5-H8**: Bloques alternativos ("overflow")
|||**HE**: Horarios especiales
|||**HV**: Horarios varios
|**Aula**|Representa los espacios físicos donde se realizan las clases.|Pertenece a un edificio específico
|||Ofrece recursos específicos (proyector, laboratorio, capacidad, etc.)
|||Debe tener capacidad adecuada para el curso asignado
|**Edificio**|Agrupa las aulas por ubicación física en el campus.
|**Programa**|Representa las carreras o programas académicos de la universidad.|Agrupa cursos relacionados académicamente
|||Define el contexto académico de los cursos
|**Recurso**|Define las características y equipamiento disponible.|Profesores tienen preferencias sobre recursos específicos
|||Aulas ofrecen recursos específicos
|||La coincidencia entre preferencias y oferta mejora la asignación

## Relaciones

### Relaciones académicas
- **Profesor imparte Curso**: Relación fundamental de enseñanza
- **Programa contiene Curso**: Los cursos pertenecen a programas académicos específicos
- **Curso asociado a BloqueHorario**: Cada curso tiene un patrón temporal preferido

### Relaciones del campus físico
- **Edificio contiene Aula**: Organización física del campus universitario

### Relaciones de asignación
- **Horario referencia Profesor, Curso y Aula**: La entidad central que materializa las asignaciones del algoritmo

### Relaciones de preferencias
- **Profesor prefiere Recurso**: Preferencias del docente sobre equipamiento
- **Aula ofrece Recurso**: Recursos disponibles en cada espacio físico

## Cambios en las relaciones del modelo

### Refinamiento aplicado
**Cambio 1: Dirección corregida en Programa-Curso**
- **Antes**: `Programa *-r- Curso` (dirección incorrecta)
- **Ahora**: `Curso -r-* Programa` (dirección natural)
- **Justificación**: "Curso pertenece a Programa" es más intuitivo que al revés

**Cambio 2: De composición a agregación en Horario**
- **Antes**: `Horario *-- Entidad` (composición - "Horario posee")
- **Ahora**: `Horario o-- Entidad` (agregación - "Horario referencia")
- **Justificación**: Las entidades (Profesor, Curso, Aula) existen independientemente del Horario

### Semántica mejorada
- **Agregación (`o--`)**: Horario es una **asignación temporal** que conecta entidades preexistentes
- **Independencia**: Si se elimina un Horario, las entidades referenciadas permanecen intactas
- **Realidad del dominio**: Refleja mejor cómo funciona el algoritmo de generación de horarios

## Vocabulario

### Conceptos Clave

- **BloqueHorario**: Patrón temporal predefinido (ej: "LXV 07-08" para H1)
- **Asignación**: Proceso de crear instancias de Horario que satisfagan todas las restricciones
- **Preferencias**: Recursos que un profesor valora para el dictado de su curso
- **Capacidad**: Número de estudiantes que puede albergar un aula
- **Conflicto**: Situación donde se violan restricciones temporales o de recursos

### Patrones de BloqueHorario

<div align=center>

| Código | Patrón | Descripción |
|--------|--------|-------------|
| H1 | LXV 07-08 | Lunes, Miércoles, Viernes 7-8 AM |
| H2 | MJS 07-08 | Martes, Jueves, Sábado 7-8 AM |
| H3 | LXV 09-10 | Lunes, Miércoles, Viernes 9-10 AM |
| H4 | MJS 09-10 | Martes, Jueves, Sábado 9-10 AM |
| H5 | LXV 11-12 | Lunes, Miércoles, Viernes 11-12 PM |
| H6 | MJS 11-12 | Martes, Jueves, Sábado 11-12 PM |
| H7 | LXV 05-06 | Lunes, Miércoles, Viernes 5-6 PM |
| H8 | MJS 05-06 | Martes, Jueves, Sábado 5-6 PM |
| HE | Especiales | Horarios fuera de patrones regulares |
| HV | Varios | Horarios de fin de semana o especiales |

</div>

## Restricciones del dominio

|De horario|De curso|De aula|De profesor|
|-|-|-|-|
|Los días válidos son: Lunes (L), Martes (M), Miércoles (X), Jueves (J), Viernes (V), Sábado (S)|Cada curso debe ser asignado preferiblemente a su BloqueHorario|Debe tener capacidad positiva|No puede estar en dos lugares al mismo tiempo
|Las horas válidas van de 5 AM a 12 PM|Debe estar asignado a al menos un programa académico|No puede estar en uso simultáneo por múltiples cursos|Sus preferencias de recursos deben considerarse en la asignación
|No puede haber solapamiento de profesor o aula en el mismo horario|Debe tener un profesor asignado|Los recursos ofrecidos deben coincidir con las preferencias del profesor
|La capacidad del aula debe ser suficiente para el curso

## Consideraciones de Diseño

### Simplicidad conceptual

- El modelo se enfoca en conceptos de negocio fundamentales
- Evita detalles de implementación o algoritmos
- Facilita la comprensión por parte de stakeholders no técnicos

### Horario como entidad integradora

- Centraliza la solución del problema de optimización
- Conecta todas las entidades principales del dominio
- Representa el objetivo final del sistema

### Organización por contextos

- **Campus Universitario**: Agrupa conceptos del espacio físico
- **Relaciones académicas**: Separadas de las físicas
- **Preferencias**: Modeladas como dependencias conceptuales

### Extensibilidad

- El modelo permite extensiones futuras sin cambios estructurales
- Las relaciones están diseñadas para soportar evolución del sistema
- Mantiene compatibilidad conceptual con el sistema legacy

## Referencias

- Sistema SigHor Original (1998) - Documentación de Ingeniería Inversa
- [reverseEngineering.md](../../../extraDocs/000-ingenieria-inversa/reverseEngineering.md) - Análisis técnico del sistema legacy
- [reflexiones.md](../../../extraDocs/000-ingenieria-inversa/reflexiones.md) - Análisis de resultados del algoritmo original
- [reflexionesAlgoritmo.md](../../../extraDocs/000-ingenieria-inversa/reflexionesAlgoritmo.md) - Análisis detallado del algoritmo