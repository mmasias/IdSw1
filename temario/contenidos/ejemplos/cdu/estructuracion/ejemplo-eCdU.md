# Sistema de gestión hospitalaria

![](/images/temario/contenidos/ejemplo-eCdU.svg)

---

![](/images/temario/contenidos/ejemplo-eCdU-000.svg)

---

## Decisiones & criterios

|Cohesión funcional|Minimización de dependencias|Reutilización
|-|-|-
|Agruparlos acorde según su relación funcional|Minimizar las dependencias entre ellos|Operaciones comunes: casos de uso include
|Identificar operaciones comunes para crear casos de uso base|Las dependencias existentes dejarlas claramente documentadas|Las variaciones *se pueden separar* como casos de uso extend

|||||
|-|-|-|-|
|![](/images/temario/contenidos/ejemplo-eCdU-001-aEnfermera.svg)|![](/images/temario/contenidos/ejemplo-eCdU-001-aMedico.svg)|![](/images/temario/contenidos/ejemplo-eCdU-001-aPaciente.svg)|![](/images/temario/contenidos/ejemplo-eCdU-001-aAdmin.svg)

|Include|Extend
|-|-
|Representan funcionalidad obligatoria y común|Representan comportamiento opcional o alternativo
|Reducen la duplicación de especificaciones|Permiten la extensibilidad del sistema

![](/images/temario/contenidos/ejemplo-eCdU-002.svg)

## ¿Beneficios?

|Mantenibilidad|Comprensión|Escalabilidad
|-|-|-
|Facilita la modificación de funcionalidad específica|Organización jerárquica clara|Estructura preparada para añadir nuevas funcionalidades
|Permite la evolución independiente de los subsistemas|Separación lógica de funcionalidades|Patrones claros para la extensión del sistema

## ¿Cómo sé si...?

|Completitud|Consistencia|Viabilidad
|-|-|-
|Todos los requisitos funcionales están cubiertos|No hay redundancia en la funcionalidad|La estructura es implementable
|Cada caso de uso tiene un propósito claro|Las dependencias son bidireccionales donde es necesario|Las interfaces entre paquetes son claras
|Las relaciones están completamente especificadas|Los nombres son consistentes y significativos|Los patrones de comunicación son eficientes

## Entregables

1. Diagramas de paquetes de casos de uso.
1. Diagramas de casos de uso por paquete.
1. Especificación de relaciones entre casos de uso.
1. Matriz de trazabilidad de requisitos.
