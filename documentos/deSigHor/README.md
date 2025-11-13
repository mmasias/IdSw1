<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](02-detalle/README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../conversation-log.md)|

</div>

# Casos de Uso - Disciplina de Requisitos

Esta sección contiene toda la especificación de casos de uso del sistema SigHor modernizado, siguiendo la disciplina de Requisitos del proceso RUP.

## Contenido de la disciplina

### [00 - Modelo del dominio](00-modelo-del-dominio/modelo-dominio.md)
Representa las entidades conceptuales del dominio del problema y sus relaciones, independiente de cualquier implementación tecnológica.

### [01 - Actores y casos de uso](01-actores-casos-uso/actores-casos-uso.md)
- **Identificación de actores**: Usuarios que interactúan con el sistema
- **Casos de uso del sistema**: Funcionalidades principales organizadas por actor
- **[Diagrama de contexto](01-actores-casos-uso/diagrama-contexto-administrador.md)**: Estados y transiciones del sistema para el actor Administrador

### [02 - Detalle y prototipado](02-detalle/README.md)
Especificación completa de cada caso de uso incluyendo:
- **Diagramas de especificación**: Estados internos y conversación detallada
- **Wireframes de prototipado**: Interfaces de usuario tecnología-agnóstica
- **Vocabulario restringido**: Aplicación de las leyes del proyecto

## Metodología aplicada

### Filosofía C→U (Crear → Usar)
- **"El delgado"**: Casos de creación mínimos que redirigen a edición
- **"El gordo"**: Casos de edición completos con funcionalidad continua
- **Vinculación automática**: Crear lleva siempre a editar del mismo objeto

### Patrones de casos de uso
- **Apertura de entidades**: Presentación de listas para selección
- **CRUD completo**: Crear (delgado) + Editar (gordo) + Eliminar (seguro)
- **Configuración específica**: Casos especializados como configurarPreferenciasProfesor()
- **Gestión de horarios**: Algoritmo de optimización y consulta

### Leyes del proyecto aplicadas
- **Vocabulario puro**: "solicita", "presenta", "permite"
- **Tecnología agnóstica**: Sin referencias a implementación específica
- **Estados simples**: Diagramas de estado con nombres vacíos `" "`
- **Separación de responsabilidades**: Actor vs Sistema claramente diferenciados

## Cobertura funcional

El proyecto cubre completamente:
- **Gestión del sistema**: Sesiones y navegación principal
- **Gestión de entidades**: Programas, Cursos, Profesores, Edificios, Aulas, Recursos
- **Configuración específica**: Preferencias de profesores, asignaciones
- **Generación de horarios**: Algoritmo de optimización de 4 fases
- **Consulta de resultados**: Visualización de horarios generados

## Referencias

- [Análisis MVC de casos de uso](../01-analisis/casos-uso/README.md)
- [Dashboard de seguimiento](../99-seguimiento/README.md)
- [Leyes del proyecto](../../extraDocs/999-leyes-proyecto/)
- [Log de conversaciones](../../conversation-log.md)