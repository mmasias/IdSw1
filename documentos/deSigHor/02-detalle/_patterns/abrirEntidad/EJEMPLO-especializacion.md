# Ejemplo: Cómo especializar el patrón abrirEntidad()

Este documento muestra cómo un caso de uso concreto especializa el patrón abstracto `abrirEntidad()`.

## Caso de uso hijo: abrirProgramas()

### Ubicación
`documentos/deSigHor/02-detalle/abrirProgramas/README.md`

### Contenido simplificado

```markdown
# pySigHor > abrirProgramas > Detalle y prototipado

## Especializa el patrón

Este caso de uso es una **especialización** de [abrirEntidad()](../_patterns/abrirEntidad/README.md)

## Parámetros concretos

|Parámetro|Valor|
|-|-|
|**{TipoEntidad}**|Programas|
|**{NombreEntidad}**|Programa|
|**{CamposFiltrable}**|código, nombre, descripción|
|**{CamposMostrar}**|código, nombre, descripción|
|**{EstadoDestino}**|PROGRAMAS_ABIERTO|

## Diagrama de especificación

Aplicando los parámetros al [patrón abstracto](../_patterns/abrirEntidad/especificacion.puml):

<div align=center>

![Caso de uso: abrirProgramas()](/images/.../abrirProgramas.svg)

</div>

**Código fuente:** Ver [patrón abrirEntidad](../_patterns/abrirEntidad/especificacion.puml)

## Prototipo de interfaz

<div align=center>

![Wireframe: Gestión de programas](/images/.../abrirProgramas-wireframe.svg)

</div>

**Código fuente:** [prototipo.puml](prototipo.puml)

## Particularidades de esta especialización

**Ninguna.** Este caso de uso sigue **exactamente** el patrón de `abrirEntidad()` sin variaciones.

## Conversación detallada

Ver [conversación del patrón abrirEntidad()](../_patterns/abrirEntidad/README.md#conversación-detallada-plantilla)
aplicando los parámetros definidos arriba.

## Conexión con diagrama de contexto

- **SISTEMA_DISPONIBLE** → `abrirProgramas()` → **PROGRAMAS_ABIERTO**

Transiciones de salida:
- **PROGRAMAS_ABIERTO** → `crearPrograma()` → **PROGRAMA_ABIERTO**
- **PROGRAMAS_ABIERTO** → `editarPrograma()` → **PROGRAMA_ABIERTO**
- **PROGRAMAS_ABIERTO** → `eliminarPrograma()` → **PROGRAMAS_ABIERTO**
- **PROGRAMAS_ABIERTO** → `completarGestion()` → **SISTEMA_DISPONIBLE**

## Referencias

- [Patrón abrirEntidad()](../_patterns/abrirEntidad/README.md) - Caso de uso abstracto padre
- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
- [Modelo del dominio](../../00-modelo-del-dominio/modelo-dominio.md)
```

### Ventajas de esta estructura

1. **Brevedad**: El README del hijo es muy corto (solo define parámetros)
2. **DRY**: No repite la especificación completa, solo referencia
3. **Trazabilidad**: Declaración explícita de herencia
4. **Mantenibilidad**: Cambios en el patrón se propagan automáticamente
5. **Flexibilidad**: Si el hijo tiene particularidades, se añaden en su sección

### Cuándo añadir particularidades

Si `abrirProgramas()` tuviera algo específico que NO está en el patrón:

```markdown
## Particularidades de esta especialización

### Validación adicional

Al presentar la lista de programas, el sistema también verifica:
- Si existen cursos asociados al programa
- Si el programa está activo o inactivo

Esta información se muestra visualmente en la lista con iconos:
- ✅ Programa activo con cursos
- ⚠️ Programa activo sin cursos
- ❌ Programa inactivo
```

Pero si no hay particularidades, simplemente se indica "Ninguna".
