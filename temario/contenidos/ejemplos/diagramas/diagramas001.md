# Diagramas

|**Diagrama de actividad**|**Diagrama de estados**|**Diagrama de secuencia**|**Diagrama de colaboración**|
|:-:|:-:|:-:|:-:|
|Qué se hace, en qué orden|En qué situación se encuentra la entidad, qué provoca los cambios|Quién hace qué, cuándo, con énfasis temporal|Quién se comunica con quién, qué mensajes intercambian

- Estados y actividad: isomórficos bajo las restricciones de no concurrencia y no jerarquías. Ambos modelan un proceso como flujo de control puro.
- Secuencia y colaboración: introducen *participantes* como una dimensión adicional. Distribuyen el proceso en entidades que interactúan mediante mensajes. A priori esta estructura no existe en actividad ni en estados.

## Un ejemplo

```java
searchAndProcess(int[] t, int k){
    int i = 0;
    while(i < t.length && t[i] != k){
        i++;
    }
    if(i < t.length && t[i] == k){
        A();
    }else{
        B();
    }
}
```

<div align=center>

|![](/images/modelosUML/diagramaActividad.svg)|![](/images/modelosUML/diagramaEstados.svg)|![](/images/modelosUML/diagramaSecuencia.svg)|![](/images/modelosUML/diagramaColaboracion.svg)|
|:-:|:-:|:-:|:-:|
|**Diagrama de actividad**|**Diagrama de estados**|**Diagrama de secuencia**|**Diagrama de colaboración**|

</div>

## Otro ejemplo

Juego del 3 en raya

<div align=center>

<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsActivity/instructionsActivity.svg">|<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsState/instructionsState.svg">
|-|-|
|Diagrama de actividad|Diagrama de estados

</div>

## Otro ejemplo

### Validación de una solicitud

<div align=center>

![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DA.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DE.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DS.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DC.svg)
|:-:|:-:|:-:|:-:|
|**Diagrama de actividad**|**Diagrama de estados**|**Diagrama de secuencia**|**Diagrama de colaboración**|

</div>

### La misma solicitud, ahora damos hasta tres intentos para reenviar

<div align=center>

![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DA-v2.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DE-v2.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DS-v2.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DC-v2.svg)
|:-:|:-:|:-:|:-:|
|**Diagrama de actividad**|**Diagrama de estados**|**Diagrama de secuencia**|**Diagrama de colaboración**|

</div>

### A nada que pidan más cosas (que tampoco son tantas...)

- Validación en tres niveles: formato, contenido técnico, autorización presupuestal.
- Posibilidad de corrección y reenvío en cada nivel (máximo 3 intentos por nivel).
- Aprobación requiere firma de supervisor (puede tardar días).
- Si solicitud > $10,000: requiere aprobación adicional de gerencia.
- Sistema debe recordar en qué punto quedó cada solicitud.
- Notificaciones automáticas cada 24h si está en espera.

![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DA-v3.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DE-v3.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DS-v3.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DC-v3.svg)
|:-:|:-:|:-:|:-:|
|**Diagrama de actividad**|**Diagrama de estados**|**Diagrama de secuencia**|**Diagrama de colaboración**|

### Comparación de complejidad

<div align=center>

|Aspecto|Actividad|Estados|Secuencia|Colaboración|
|-|:-:|:-:|:-:|:-:|
|**Líneas/nodos**|~80|~15|~100|~25|
|**Anidación**|5 niveles|0 niveles|6 niveles|0 niveles|
|**Legibilidad al crecer**|Se vuelve ilegible|Mantiene claridad|Se vuelve ilegible|Pierde contexto temporal|
|**Manejo de estados asíncronos**|Muy difícil|Natural|Complejo|No se representa bien|
|**Modificaciones**|Requiere rehacer secciones|Cambios localizados|Afecta múltiples secciones|Requiere renumeración|
|**Trazabilidad**|Se pierde en bucles|Clara|Se pierde en alternativas|Difícil seguimiento|

</div>


### 2Think

Cómo escala cada diagrama si ahora nos pidieran agregar el siguiente requisito: ***Las solicitudes pueden pausarse y reanudarse por el solicitante en cualquier momento***.