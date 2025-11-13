<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../01-analisis/casos-uso/README.md)
|-:
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../conversation-log.md)

</div>

# Detalle y Prototipo de Casos de Uso

Esta carpeta contiene la especificación detallada y prototipado de cada caso de uso identificado en el sistema SigHor.

## Casos de uso especificados

### Gestión del sistema
- [iniciarSesion](iniciarSesion/) - Autenticación de usuarios
- [cerrarSesion](cerrarSesion/) - Cierre de sesión
- [completarGestion](completarGestion/) - Hub de convergencia del sistema

### Apertura de entidades
- [abrirProgramas](abrirProgramas/) - Gestión de programas académicos
- [abrirCursos](abrirCursos/) - Gestión de cursos
- [abrirProfesores](abrirProfesores/) - Gestión de profesores
- [abrirEdificios](abrirEdificios/) - Gestión de edificios
- [abrirAulas](abrirAulas/) - Gestión de aulas
- [abrirRecursos](abrirRecursos/) - Gestión de recursos

### CRUD de Programas
- [crearPrograma](crearPrograma/) - Creación de programas académicos
- [editarPrograma](editarPrograma/) - Edición de programas académicos
- [eliminarPrograma](eliminarPrograma/) - Eliminación de programas académicos

### CRUD de Cursos
- [crearCurso](crearCurso/) - Creación de cursos académicos
- [editarCurso](editarCurso/) - Edición de cursos académicos
- [eliminarCurso](eliminarCurso/) - Eliminación de cursos académicos

### CRUD de Profesores
- [crearProfesor](crearProfesor/) - Creación de profesores
- [editarProfesor](editarProfesor/) - Edición de profesores
- [eliminarProfesor](eliminarProfesor/) - Eliminación de profesores
- [configurarPreferenciasProfesor](configurarPreferenciasProfesor/) - Configuración de preferencias de recursos
- [asignarProfesorACurso](asignarProfesorACurso/) - Gestión de asignaciones profesor-curso

### CRUD de Edificios
- [crearEdificio](crearEdificio/) - Creación de edificios
- [editarEdificio](editarEdificio/) - Edición de edificios
- [eliminarEdificio](eliminarEdificio/) - Eliminación de edificios

### CRUD de Aulas
- [crearAula](crearAula/) - Creación de aulas
- [editarAula](editarAula/) - Edición de aulas
- [eliminarAula](eliminarAula/) - Eliminación de aulas

### CRUD de Recursos
- [crearRecurso](crearRecurso/) - Creación de recursos
- [editarRecurso](editarRecurso/) - Edición de recursos
- [eliminarRecurso](eliminarRecurso/) - Eliminación de recursos

### Gestión de Horarios
- [generarHorario](generarHorario/) - Generación automática de horarios
- [consultarHorario](consultarHorario/) - Consulta de horarios generados

## Estructura de cada caso de uso

Cada carpeta de caso de uso contiene:

- **README.md** - Especificación completa del caso de uso
- **especificacion.puml** - Diagrama de especificación en PlantUML
- **prototipo.puml** - Wireframes de prototipado en Salt

## Metodología aplicada

- **Filosofía C→U** - Casos de creación vinculados automáticamente con edición
- **Patrones "el delgado" y "el gordo"** - Creación mínima vs edición completa
- **Leyes del proyecto** - Vocabulario restringido y diseño sin implementación
- **Tecnología agnóstica** - Especificaciones independientes de la implementación