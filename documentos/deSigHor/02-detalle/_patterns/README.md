<div align=right>

|[![](https://img.shields.io/badge/-Inicio-FFF?style=flat&logo=Emlakjet&logoColor=black)](../../../../README.md) [![](https://img.shields.io/badge/-RUP-FFF?style=flat&logo=Elsevier&logoColor=black)](../../../README.md) [![](https://img.shields.io/badge/-Detalle_&_Prototipo-FFF?style=flat&logo=typeorm&logoColor=black)](../README.md)|
|-:|

</div>

# Patrones de Casos de Uso (Casos de Uso Abstractos)

Esta carpeta contiene **casos de uso abstractos** que sirven como **patrones de diseño** para casos de uso concretos.

## ¿Qué es un caso de uso abstracto?

Un caso de uso abstracto es una **plantilla reutilizable** que:

- **NO se ejecuta directamente** (no tiene implementación propia)
- **Define comportamiento común** compartido por múltiples casos de uso
- **Usa generalización UML** (relación de herencia `<<generalization>>`)
- **Es parametrizable** (los hijos sustituyen parámetros por valores concretos)

## ¿Cuándo usar generalización?

### Usar generalización cuando:

1. **Múltiples casos de uso** siguen exactamente el mismo flujo
2. Las **diferencias son paramétricas** (nombres, campos, datos)
3. El **actor percibe** las acciones como "conceptualmente la misma"
4. **Reduce redundancia** real en la especificación

### NO usar generalización cuando:

1. Solo hay **un caso de uso** de ese tipo
2. Las diferencias son de **lógica de negocio**, no de datos
3. El **actor percibe** las acciones como conceptualmente diferentes
4. Crearía **confusión** en lugar de claridad

## Patrones disponibles

### 1. abrirEntidad(TipoEntidad)

**Carpeta:** [abrirEntidad/](abrirEntidad/)

**Propósito:** Gestión de listas con filtrado

**Especializaciones:**
- abrirProgramas()
- abrirCursos()
- abrirProfesores()
- abrirAulas()
- abrirEdificios()
- abrirRecursos()

**Justificación:** Los 6 casos siguen la misma máquina de estados, solo cambian los datos mostrados/filtrados.

---

### 2. eliminarEntidad(TipoEntidad) *(Pendiente)*

**Propósito:** Borrado seguro con confirmación

**Especializaciones previstas:**
- eliminarPrograma()
- eliminarCurso()
- eliminarProfesor()
- eliminarAula()
- eliminarEdificio()
- eliminarRecurso()

**Justificación:** Todos requieren confirmación explícita y muestran datos antes de eliminar.

---

## Estructura de un patrón

Cada patrón abstracto contiene:

```
_patterns/
└── nombrePatron/
    ├── README.md              # Especificación completa del patrón
    ├── generalization.puml    # Diagrama UML mostrando padre e hijos
    ├── especificacion.puml    # Máquina de estados con parámetros
    ├── wireframe.puml         # UI genérica (si aplica)
    └── EJEMPLO-especializacion.md  # Cómo usar el patrón
```

## Cómo especializar un patrón

### Paso 1: Leer el patrón padre

Estudia el README.md del patrón abstracto para entender:
- Los parámetros que debes definir
- El flujo genérico
- Las restricciones del patrón

### Paso 2: Crear tu especialización

En `02-detalle/tuCasoDeUso/README.md`:

```markdown
# tuCasoDeUso() - Especialización de nombrePatron()

## Especializa el patrón

[nombrePatron()](../_patterns/nombrePatron/README.md)

## Parámetros concretos

|Parámetro|Valor|
|-|-|
|{Parametro1}|ValorConcreto1|
|{Parametro2}|ValorConcreto2|

## Particularidades

*Solo si hay diferencias con el patrón*
```

### Paso 3: Añadir particularidades (si existen)

Si tu caso de uso tiene algo **específico** que no está en el patrón, documéntalo en la sección "Particularidades".

Si sigue el patrón exactamente, escribe "Ninguna. Sigue el patrón exacto de X."

## Ventajas pedagógicas

Este enfoque enseña a:

1. **Identificar patrones** en requisitos
2. **Abstraer comportamiento común**
3. **Aplicar DRY** (Don't Repeat Yourself) en especificaciones
4. **Usar generalización UML** correctamente
5. **Distinguir** cuándo generalizar y cuándo no

## Antipatrones a evitar

### Sobregeneralización

No generalizar solo porque "se parecen visualmente".

**Ejemplo**: `consultarHorario()` muestra información, pero:
- No es CRUD
- Maneja ausencia de datos especialmente
- Tiene semántica diferente

Conclusión: NO generalizar con `abrirEntidad()`.

### Generalización prematura

No crear un patrón abstracto hasta tener **al menos 3 casos concretos** que lo necesiten.

### Parámetros complejos

Si los "parámetros" requieren lógica compleja para ser sustituidos, probablemente no es generalización sino casos diferentes.

## Referencias

- [Reflexiones sobre estructurar casos de uso](../../99-documentos/acercaDeEstructurar.md)
- [Estructuración de casos de uso en RUP](/temario/contenidos/00010-eCdU.md)
- [Diagrama de contexto - Administrador](../../01-actores-casos-uso/diagrama-contexto-administrador.md)
