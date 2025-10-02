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