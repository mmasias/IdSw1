<div align=right>
 
|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Modelo_del_dominio-FFF?style=flat&logo=freedesktop.org&logoColor=black)](../../00-modelo-del-dominio/modelo-dominio.md) [![](https://img.shields.io/badge/-Actores_&_Casos_de_Uso-FFF?style=flat&logo=crewunited&logoColor=black)](../../01-actores-casos-uso/actores-casos-uso.md) [![](https://img.shields.io/badge/-Diagrama_de_contexto-FFF?style=flat&logo=diagramsdotnet&logoColor=black)](../../01-actores-casos-uso/diagrama-contexto-administrador.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md) [![](https://img.shields.io/badge/-Análisis-FFF?style=flat&logo=multisim&logoColor=black)](../../../01-analisis/casos-uso/README.md)|
|-:|
|[![](https://img.shields.io/badge/-Estado-FFF?style=flat&logo=greensock&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Propuesta_de_dashboard-FFF?style=flat&logo=composer&logoColor=black)](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg) [![](https://img.shields.io/badge/-Reflexiones-FFF?style=flat&logo=hootsuite&logoColor=black)](../../../../extraDocs/README.md) [![](https://img.shields.io/badge/-Log_de_conversación-FFF?style=flat&logo=gnometerminal&logoColor=black)](../../../../conversation-log.md)|

</div>

# pySigHor > generarHorario > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/generarHorario/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-25
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `generarHorario()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para la generación algorítmica de horarios académicos.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|generarHorario()|
|**Actor primario**|Administrador|
|**Objetivo**|Ejecutar algoritmo de generación de horarios con validaciones previas y manejo de reemplazo|
|**Tipo**|Primario, esencial, proceso algorítmico|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador, acceso desde menú principal (SISTEMA_DISPONIBLE)|
|**Postcondición exitosa**|Horario generado y guardado, usuario en HORARIO_ABIERTO viendo resultado|
|**Postcondición de fallo**|Datos insuficientes detectados, usuario informado y regreso a SISTEMA_DISPONIBLE|

## diagrama de especificación

<div align=center>

|![Caso de uso: generarHorario()](/images/RUP/00-casos-uso/02-detalle/generarHorario/generarHorario.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo

**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de reemplazo (horario existe)

<div align=center>

|![Wireframe: Confirmación de reemplazo de horario](/images/RUP/00-casos-uso/02-detalle/generarHorario/generarHorario-wireframe-confirmation.svg)|
|-|
|**Estado**: ProvidingConfirmation|

</div>

#### pantalla 2: datos insuficientes

<div align=center>

|![Wireframe: Datos insuficientes](/images/RUP/00-casos-uso/02-detalle/generarHorario/generarHorario-wireframe-insufficient.svg)|
|-|
|**Estado**: Choice point - datos insuficientes|

</div>

#### pantalla 3: generación en progreso

<div align=center>

|![Wireframe: Generación en progreso](/images/RUP/00-casos-uso/02-detalle/generarHorario/generarHorario-wireframe-generating.svg)|
|-|
|**Estado**: Choice point - generación exitosa|

</div>

**Correspondencia con especificación:**
- Actor "solicita generar horario"
- Sistema "presenta" confirmación si horario existe
- Sistema "presenta" datos insuficientes si aplica
- Actor "solicita confirmar" o "solicita cancelar"

### validaciones del wireframe

- ¿Se presenta claramente la advertencia de reemplazo de horario existente?
- ¿Es claro qué datos mínimos se requieren para la generación?
- ¿La información de progreso durante generación es adecuada?
- ¿Las opciones de confirmación y cancelación están bien diferenciadas?

**Código fuente:** [wireframes.puml](wireframes.puml)

## conversación detallada

### flujo principal (único)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita generar horario||
||**Sistema**|presenta|• datos disponibles para generación<br>• advertencia si horario existe|
|**Administrador**|solicita confirmar generación||
||**Sistema**|presenta resultado|• horario generado exitosamente<br>• transferir a consultarHorario()|
|**Administrador**|solicita cancelar generación||
||**Sistema**|presenta resultado|• operación cancelada<br>• transferir a completarGestion()|

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**RequiringGeneration**|Estado donde el administrador solicita generar horario|Actor debe solicitar generar horario|
|**ProvidingConfirmation**|Estado donde el sistema presenta datos y advertencias|Sistema debe presentar datos disponibles y advertencia si horario existe|
|**Choice point**|Punto de decisión con múltiples salidas|Evaluación de cancelación, datos insuficientes o generación exitosa|

## funcionalidad de generación algorítmica

### concepto clave - proceso algorítmico complejo

- **generarHorario()** implementa proceso algorítmico que:
  - **Valida** datos mínimos necesarios para generación
  - **Detecta** conflictos con horario existente
  - **Ejecuta** algoritmo de optimización de 4 fases
  - **Guarda** resultado automáticamente durante generación
  - **Transfiere** automáticamente a visualización

### validaciones implementadas

- **Datos mínimos**: Al menos 1 curso, 1 profesor, 1 aula configurados
- **Horario existente**: Detección y advertencia de reemplazo
- **Integridad**: Verificación de datos consistentes antes de generar

### características del algoritmo

- **4 fases**: PrepararH(), GeneraPreHorario(), GeneraHorario(), casos especiales
- **Optimización**: Minimización de conflictos y maximización de eficiencia
- **Persistencia**: Guardado automático durante proceso sin confirmación adicional
- **Resultado garantizado**: Con datos mínimos, siempre produce horario válido

## opciones de navegación

### operaciones de generación

- **Generar con confirmación** → Horario generado + **<<include>>** `consultarHorario()`
- **Cancelar generación** → **<<include>>** `completarGestion()` sin cambios
- **Datos insuficientes** → **<<include>>** `completarGestion()` con información

### navegación del sistema

- **Generación exitosa** → **<<include>>** `consultarHorario()` en `HORARIO_ABIERTO`
- **Cancelación** → **<<include>>** `completarGestion()` en `SISTEMA_DISPONIBLE`
- **Error datos** → **<<include>>** `completarGestion()` en `SISTEMA_DISPONIBLE`

## conexión con diagrama de contexto

Este caso de uso corresponde a las transiciones:
- **SISTEMA_DISPONIBLE** → `generarHorario()` → **HORARIO_ABIERTO** (éxito)
- **SISTEMA_DISPONIBLE** → `generarHorario()` → **SISTEMA_DISPONIBLE** (cancelación/error)

Las transiciones incluyen:
- **<<include>>** `consultarHorario()` → **HORARIO_ABIERTO** (tras generación exitosa)
- **<<include>>** `completarGestion()` → **SISTEMA_DISPONIBLE** (tras cancelación/error)

## vocabulario utilizado

### actor (Administrador)

- **solicita**: expresa la intención de generar horario
- **solicita**: expresa confirmación tras ver advertencia de reemplazo
- **solicita**: expresa cancelación de proceso
- **solicita**: expresa reconocimiento de error de datos

### sistema

- **presenta**: muestra validaciones de datos mínimos
- **presenta**: muestra confirmación de reemplazo con información detallada
- **presenta**: muestra progreso durante generación algorítmica
- **permite solicitar**: habilita confirmación tras mostrar advertencias
- **permite solicitar**: habilita cancelación en cualquier momento

## características metodológicas

### separación de responsabilidades

- **Actor**: Solicita generación, solicita confirmación de reemplazo, solicita reconocimiento
- **Sistema**: Presenta validaciones, presenta confirmaciones, permite solicitar acciones, ejecuta algoritmo

### ausencia de detalles de implementación

- No especifica detalles de las 4 fases algorítmicas
- No incluye detalles de optimización matemática
- No menciona estructura de almacenamiento de horario
- Trata algoritmo como "servicio" que genera resultado

### conversación de proceso algorítmico

- El caso de uso representa una conversación de proceso computacional intensivo
- Tiene objetivo claro: generar horario académico optimizado
- Termina transferiendo automáticamente a visualización del resultado

### rol del actor

- **Entrada**: Administrador (desde menú principal del sistema)
- **Salida**: Administrador (con horario generado visualizándose, o en menú tras error/cancelación)
- **Estado**: Permanece como Administrador durante toda la conversación

### patrón de proceso algorítmico

- **Validación previa**: Verificaciones de datos mínimos
- **Confirmación inteligente**: Solo si hay conflicto con horario existente
- **Ejecución transparente**: Algoritmo se ejecuta sin intervención del usuario
- **Transferencia automática**: **<<include>>** `consultarHorario()` para mostrar resultado

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [consultarHorario()](../consultarHorario/README.md) - Caso de transferencia automática
- [completarGestion()](../completarGestion/README.md) - Caso de navegación alternativa
- [Análisis algorítmico original](../../../../reverseEngineering.md) - Algoritmo de 4 fases
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada
- [QyA.log](../../../../QyA.log) - Decisiones de diseño para casos algorítmicos