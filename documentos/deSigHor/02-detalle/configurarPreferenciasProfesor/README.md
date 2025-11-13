<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > configurarPreferenciasProfesor > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/configurarPreferenciasProfesor/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## Información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Caso de uso**: configurarPreferenciasProfesor()
- **Actor**: Administrador de Horarios
- **Tipo**: CRUD "El gordo" - Configuración específica
- **Hilo funcional**: Profesores

## Propósito

Permitir que el administrador configure el orden de prioridad de recursos para un profesor específico.

## Casos de uso relacionados

- **Origen**: Se accede desde editarProfesor() cuando el sistema está en estado PROFESOR_ABIERTO
- **Algoritmo dependiente**: generarHorario() utiliza estas preferencias
- **Navegación**: Retorna a editarProfesor() mediante abrirEdicionProfesor()

## Diagrama de especificación

<div align=center>

![configurarPreferenciasProfesor](/images/RUP/00-casos-uso/02-detalle/configurarPreferenciasProfesor/configurarPreferenciasProfesor.svg)

</div>

**Código fuente:** [especificacion.puml](especificacion.puml)

## Wireframes

<div align=center>

![configurarPreferenciasProfesor-wireframe](/images/RUP/00-casos-uso/02-detalle/configurarPreferenciasProfesor/configurarPreferenciasProfesor-wireframe.svg)

</div>

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita configurar preferencias del profesor||
||**Sistema**|presenta datos de configuración|• Lista de recursos disponibles<br>• Orden de prioridad actual del profesor<br>• Permite solicitar modificar orden<br>• Permite solicitar guardar configuración<br>• Permite solicitar cancelar configuración|
|**Administrador**|solicita modificar orden||(opcional)|
||**Sistema**|permite solicitar modificar prioridades|• Permite cambiar orden de recursos<br>• Permite solicitar guardar cambios<br>• Permite solicitar continuar configurando|
|**Administrador**|solicita guardar y salir||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**ConfigurandoPreferencias**|Estado donde se presentan los recursos con orden de prioridad|Sistema debe presentar lista de recursos ordenable|
|**GuardandoConfiguracion**|Estado donde se procesan las modificaciones de preferencias|Sistema debe procesar cambios y permitir continuar o salir|

## funcionalidad de configuración completa

### concepto clave - "el gordo"

- **configurarPreferenciasProfesor()** es "el gordo" que:
  - **Presenta** lista completa de recursos con orden actual
  - **Permite** modificación del orden de prioridad
  - **Mantiene** sesión de configuración activa (puede continuar)