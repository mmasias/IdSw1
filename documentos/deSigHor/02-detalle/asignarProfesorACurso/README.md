<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > asignarProfesorACurso > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/asignarProfesorACurso/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Caso de uso**: asignarProfesorACurso()
- **Actor**: Administrador de Horarios
- **Tipo**: Gestión de asignaciones específicas
- **Hilo funcional**: Asignaciones Profesor-Curso

## Propósito

Permitir que el administrador gestione las asignaciones de cursos específicos a un profesor determinado.

## Casos de uso relacionados

- **Origen**: Se accede desde editarProfesor() cuando el sistema está en estado PROFESOR_ABIERTO
- **Algoritmo dependiente**: generarHorario() utiliza estas asignaciones
- **Navegación**: Retorna a editarProfesor() mediante editarProfesor()

## Diagrama de especificación

<div align=center>

![asignarProfesorACurso](/images/RUP/00-casos-uso/02-detalle/asignarProfesorACurso/asignarProfesorACurso.svg)

</div>

**Código fuente:** [especificacion.puml](especificacion.puml)

## Wireframes

<div align=center>

![asignarProfesorACurso-wireframe](/images/RUP/00-casos-uso/02-detalle/asignarProfesorACurso/asignarProfesorACurso-wireframe.svg)

</div>

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita asignar cursos al profesor||
||**Sistema**|presenta gestión de asignaciones|• Lista de cursos disponibles<br>• Lista de cursos ya asignados al profesor<br>• Permite solicitar asignar curso disponible<br>• Permite solicitar desasignar curso asignado<br>• Permite solicitar guardar asignaciones<br>• Permite solicitar cancelar gestión|
|**Administrador**|solicita asignar curso disponible||(opcional)|
||**Sistema**|permite solicitar gestionar asignaciones|• Permite mover curso de disponibles a asignados<br>• Permite solicitar continuar gestionando<br>• Permite solicitar guardar cambios|
|**Administrador**|solicita guardar y salir||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**GestionandoAsignaciones**|Estado donde se presentan cursos disponibles y asignados|Sistema debe presentar listas organizadas de cursos|
|**GuardandoAsignaciones**|Estado donde se procesan los cambios en asignaciones|Sistema debe procesar cambios y permitir continuar o salir|

## funcionalidad de gestión de asignaciones completa

### concepto clave - "gestión de relaciones"

- **asignarProfesorACurso()** es gestión de relaciones que:
  - **Presenta** lista de cursos disponibles y ya asignados
  - **Permite** asignar y desasignar cursos específicos
  - **Mantiene** sesión de gestión activa (puede continuar)
  - **Guarda** cambios cuando el administrador solicita