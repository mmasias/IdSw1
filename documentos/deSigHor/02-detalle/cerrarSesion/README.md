# pySigHor > cerrarSesion > Detalle y prototipado

> |[🏠️](/RUP/README.md)|[ 📊](https://raw.githubusercontent.com/mmasias/pySigHor/main/images/RUP/99-seguimiento/diagrama-contexto-administrador.svg)|**Detalle**|[Análisis](/RUP/01-analisis/casos-uso/cerrarSesion/README.md)|Diseño|Desarrollo|Pruebas|
> |-|-|-|-|-|-|-|

## información del artefacto

- **Proyecto**: pySigHor - Modernización del Sistema Generador de Horarios
- **Fase RUP**: Inception (Inicio)
- **Disciplina**: Requisitos
- **Versión**: 1.0
- **Fecha**: 2025-07-13
- **Autor**: Equipo de desarrollo

## propósito

Especificación detallada del caso de uso `cerrarSesion()` mediante diagrama de estado, mostrando la conversación completa entre el Administrador y el Sistema para el proceso de cierre de sesión.

## información del caso de uso

|Atributo|Valor|
|-|-|
|**Nombre**|cerrarSesion()|
|**Actor primario**|Administrador|
|**Objetivo**|Terminar sesión activa y regresar al estado no autenticado del sistema|
|**Tipo**|Primario, esencial|
|**Nivel**|Objetivo de usuario|
|**Precondición**|Usuario autenticado como Administrador, sistema en estado SISTEMA_DISPONIBLE|
|**Postcondición exitosa**|Administrador se convierte en UsuarioNoRegistrado, sistema en estado SESION_CERRADA|
|**Postcondición de fallo**|N/A - caso de uso sin condiciones de fallo|

## diagrama de especificación

<div align=center>

|![Caso de uso: cerrarSesion()](/images/RUP/00-casos-uso/02-detalle/cerrarSesion/cerrarSesion.svg)|
|-|
|Código fuente: [especificacion.puml](especificacion.puml)|

</div>

## prototipo de interfaz

### propósito del prototipo
**Objetivo:** Que te digan que NO lo antes posible - validar la especificación antes de invertir en desarrollo.

### wireframes

#### pantalla 1: confirmación de cierre
<div align=center>

|![Wireframe: Cerrar sesión](/images/RUP/00-casos-uso/02-detalle/cerrarSesion/cerrarSesion-wireframe.svg)|
|-|
|**Estado**: SolicitandoCierre → ConfirmandoCierre|

</div>

**Correspondencia con especificación:**
- Administrador "solicita cerrar sesión"
- Sistema "presenta confirmación de cierre"

### validaciones del wireframe
- ¿El diálogo refleja correctamente la conversación actor-sistema?
- ¿El sistema permite claramente confirmar y cancelar?
- ¿La terminología "cerrar sesión" es clara para usuarios finales?
- ¿Se preserva la identidad visual consistente con el sistema?

**Código fuente:** [prototipo.puml](prototipo.puml)

## conversación detallada

### flujo principal (éxito)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita cerrar sesión||
||**Sistema**|presenta confirmación|¿Desea cerrar la sesión activa?|
||**Sistema**|permite confirmar|Confirmar cierre|
|**Administrador**|solicita confirmar cierre||

### flujo alternativo (cancelación)

|Actor|Acción|Sistema|Respuesta|
|-|-|-|-|
|**Administrador**|solicita cerrar sesión||
||**Sistema**|presenta confirmación|¿Desea cerrar la sesión activa?|
||**Sistema**|permite cancelar|Cancelar cierre|
|**Administrador**|solicita cancelar cierre||

## estados internos del caso de uso

|Estado|Descripción|Responsabilidad|
|-|-|-|
|**SolicitandoCierre**|Estado inicial donde se requiere cierre de sesión|Sistema debe presentar confirmación|
|**ConfirmandoCierre**|Usuario está decidiendo si confirmar o cancelar|Sistema espera decisión del usuario|
|**Punto de decisión**|Evaluación de confirmación del usuario|Sistema determina acción a seguir|

## validaciones del sistema

|Validación|Criterio|Resultado|
|-|-|-|
|**Cierre confirmado**|Administrador confirma cierre|Finalizar sesión, regresar a SESION_CERRADA|
|**Cierre cancelado**|Administrador cancela cierre|Mantener sesión, regresar a SISTEMA_DISPONIBLE|

## conexión con diagrama de contexto

Este caso de uso corresponde a la transición:
- **SISTEMA_DISPONIBLE** → `cerrarSesion()` → **SESION_CERRADA**

La especificación detalla la transición desde **SISTEMA_DISPONIBLE** hacia **SESION_CERRADA** del diagrama de contexto del Administrador de Horarios.

## vocabulario utilizado

### actor (Administrador)
- **solicita**: inicia conversación pidiendo algo al sistema

### sistema
- **presenta**: muestra información o solicitud de confirmación al actor
- **permite**: habilita funcionalidad para el actor

## características metodológicas

### separación de responsabilidades
- **Actor**: Solo solicita acciones al sistema
- **Sistema**: Solo presenta información y permite acciones, no implementa lógica de sesión

### ausencia de detalles de implementación
- No especifica tecnología de gestión de sesión
- No incluye detalles de interfaz específica
- No menciona base de datos o repositorios específicos

### conversación atómica
- El caso de uso representa una conversación completa
- Tiene objetivo claro: cerrar sesión activa
- Termina en estado definido: sesión cerrada o mantenida

### transformación del actor
- **Entrada**: Administrador (con sesión activa en el sistema)
- **Salida**: UsuarioNoRegistrado (sin permisos, requiere nueva autenticación)
- **Mecanismo**: Confirmación exitosa produce cambio de rol
- **Representación**: `Administrador → UsuarioNoRegistrado` en transición de salida

### trazabilidad con contexto
- Estados internos corresponden a flujo del diagrama de contexto
- Transición de salida conecta con estado inicial (SESION_CERRADA)
- Caso alternativo mantiene estado actual para permitir continuar operación

## referencias

- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
- [conversation-log.md](../../../../conversation-log.md) - Metodología de especificación detallada